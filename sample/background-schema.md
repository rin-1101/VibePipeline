# 5. Background Schema: MarketLens AI

**Status:** Proposed sample specification  
**Owner:** Backend and ML leads  
**Last updated:** 2026-10-06

## Data inventory

| ID | Table | Purpose | Source and sensitivity |
| --- | --- | --- | --- |
| E-01 | `users` | Identity and application role. | Identity provider; personal data. |
| E-02 | `instruments` | Supported stocks and exchange metadata. | Approved universe; shared app metadata. |
| E-03 | `datasets` | Immutable import snapshots and provenance. | Worker; licensed or synthetic data. |
| E-04 | `daily_prices` | Versioned bars for each dataset. | Validated imports; market-data restrictions apply. |
| E-05 | `model_versions` | Training configuration, artifacts, and publication state. | Worker; internal artifacts, published metadata subset. |
| E-06 | `forecasts` | Operational predictions and their provenance. | Worker; shared published results. |
| E-07 | `watchlist_items` | Personal saved instruments. | User; private account data. |
| E-08 | `evaluations` | Historical results and promotion evidence. | Worker; published reports or private candidate results. |
| E-09 | `jobs` | Background work, retries, and failure state. | Admin/worker; internal operations. |
| E-10 | `audit_events` | Accountability for administrative actions. | API/worker; restricted security records. |

## Field conventions

Use UUID primary keys, UTC `timestamptz` for events, and exchange-local `date` for trading sessions. Unless marked optional, fields are required. Foreign-key fields reference the named table's `id`. Apply `NOT NULL`, checks, and uniqueness in PostgreSQL as well as API validation.

| Entity | Fields and types | Key constraints |
| --- | --- | --- |
| E-01 | `id uuid`, `oidc_issuer text`, `oidc_subject text`, `display_name varchar(120)`, `role varchar(16)`, `status varchar(16)`, `created_at timestamptz` | Unique issuer/subject pair; role analyst/admin; status active/disabled. Store no identity-provider password. |
| E-02 | `id uuid`, `symbol varchar(16)`, `exchange varchar(16)`, `company_name text`, `currency char(3)`, `exchange_timezone text`, `calendar_code text`, `is_active boolean` | Unique symbol/exchange; approved universe only. |
| E-03 | `id uuid`, `source text`, `is_demo boolean`, `adjustment_policy text`, `is_point_in_time boolean`, `content_hash char(64)`, `artifact_path text`, `data_start date`, `data_end date`, `ingested_at timestamptz`, `status varchar(16)` | Unique content hash; start <= end; validated snapshots are immutable; status pending/validated/rejected. |
| E-04 | `id uuid`, `dataset_id uuid`, `instrument_id uuid`, `session_date date`, `available_at timestamptz`, `open numeric(20,8)`, `high numeric(20,8)`, `low numeric(20,8)`, `close numeric(20,8)`, `adjusted_close numeric(20,8)`, `volume bigint` | Unique dataset/instrument/session; prices positive; volume >= 0; raw OHLC ordered; do not compare adjusted close against raw high/low. |
| E-05 | `id uuid`, `instrument_id uuid`, `dataset_id uuid`, `horizon smallint`, `training_start date`, `training_end date`, `feature_spec jsonb`, `hyperparameters jsonb`, `random_seed integer`, `code_revision text`, `lock_hash char(64)`, `artifact_path text`, `artifact_hash char(64)`, `status varchar(16)`, `trained_at timestamptz` | Horizon 1/5; status candidate/active/retired/rejected; one active model per instrument/horizon/data mode. Data mode derives from dataset. |
| E-06 | `id uuid`, `instrument_id uuid`, `dataset_id uuid`, `model_id uuid`, `cutoff_date date`, `target_date date`, `horizon smallint`, `base_adjusted_close numeric(20,8)`, `median_return double precision`, `median_price numeric(20,8)`, `lower_price numeric(20,8)`, `upper_price numeric(20,8)`, `nominal_coverage numeric(4,3)`, `generated_at timestamptz`, `published_at timestamptz` optional | Unique instrument/dataset/model/cutoff/horizon; target after cutoff; finite values; 0 < lower <= median <= upper; nominal coverage 0.800. |
| E-07 | `id uuid`, `user_id uuid`, `instrument_id uuid`, `created_at timestamptz` | Unique user/instrument; ownership enforced by server; cascade on user deletion. |
| E-08 | `id uuid`, `model_id uuid`, `dataset_id uuid`, `test_start date`, `test_end date`, `sample_count integer`, `metrics jsonb`, `split_spec jsonb`, `report_path text`, `passes_gate boolean`, `evaluated_at timestamptz` | Metrics contain error, baseline error, coverage, interval width, quantile loss, and direction counts; immutable report per evaluated model. |
| E-09 | `id uuid`, `requested_by uuid` optional, `type varchar(16)`, `payload jsonb`, `idempotency_key text`, `status varchar(16)`, `attempt_count integer`, `created_at timestamptz`, `started_at timestamptz` optional, `finished_at timestamptz` optional, `heartbeat_at timestamptz` optional, `error_code text` optional | Type import/train/forecast; status queued/running/succeeded/failed; unique idempotency key; no secrets in payload or errors. |
| E-10 | `id uuid`, `actor_user_id uuid` optional, `actor_service text` optional, `action text`, `resource_type text`, `resource_id uuid` optional, `created_at timestamptz`, `metadata jsonb` | Exactly one actor identity; append-only; metadata excludes credentials and personal watchlist contents. |

Store server-side sessions in a separate infrastructure table with hashed token, user ID, idle/absolute expiration, and creation time. It is not a user-facing product entity. Expired sessions are deleted daily and session tokens never appear in logs.

## Relationships and integrity

Users have many watchlist items; instruments have many prices, models, and forecasts; datasets have many prices and may support many models; models have evaluations and forecasts. Evaluation report files contain fold predictions; those are not operational `forecasts` rows.

Require forecast instrument/horizon to match the model, cutoff bars to exist in its inference dataset, and inference data mode and adjustment policy to match training. The inference dataset may be newer than the training dataset. Require evaluation rows to reference the evaluated model and its immutable evaluation snapshot.

Deleting an instrument, dataset, or model referenced by a forecast is restricted. Archive or deactivate instead. Use a transaction for promotion: lock the instrument/horizon/data-mode slot, verify eligibility, retire the previous active model, and activate the candidate. Publish forecast batches atomically.

Index daily prices by dataset/instrument/session, published forecasts by instrument/horizon/cutoff, jobs by status/created time, and audit events by creation time. A separate mode selector keeps synthetic forecasts out of live-data responses.

## Access control

| Identity | Read | Create/update/delete |
| --- | --- | --- |
| Anonymous | Login page and minimum public health response. | No app data changes. |
| Analyst | Own user/session metadata, supported instruments, validated chart data allowed by license, published forecasts, own watchlist, published evaluations. | Create/delete own watchlist entries only. |
| Administrator | Analyst access plus jobs, candidate evaluations, and sanitized model metadata. | Queue jobs, promote eligible models, disable accounts through audited administration; no direct arbitrary price or forecast edits. |
| Worker service | Required datasets, prices, model artifacts, evaluations, and jobs. | Import validated data; create models/evaluations/forecasts; update job state; append service audit events. Cannot alter user roles or watchlists. |
| Maintenance operator | Restricted backup and migration access. | Restore, migrations, and approved retention tasks through separate credentials. |

Analyst queries derive user ID from the authenticated session. A submitted user ID never grants access to another account's watchlist. Only approved published report fields reach analyst APIs; filesystem paths, OIDC subjects, logs, and secrets stay private. Default-deny all unspecified operations.

## Storage and retention

| Category | Location | Example pilot policy |
| --- | --- | --- |
| Users and watchlists | PostgreSQL private database | Retain while account is active; delete watchlist and identifying profile on approved account deletion. |
| Market datasets and bars | PostgreSQL plus private snapshot volume | Keep while referenced by retained models; provider license governs archival and deletion. |
| Model artifacts and reports | Private read-restricted volume | Retain active and previous eligible models plus their provenance; retire unused candidates after 90 days if unreferenced. |
| Operational forecasts | PostgreSQL | Retain one year for traceability, subject to input-data rights. |
| Job records and logs | Database and restricted logs | Retain jobs 90 days and sanitized logs 30 days. |
| Audit events | Restricted database table | Retain one year under the approved pilot policy. |

These are example policies, subject to organizational and data-provider approval before live deployment. Use encrypted host volumes, TLS in transit, private network access, and separate worker/API database credentials. There is no public file-upload storage in the MVP.

## Backups and migrations

Back up the database and referenced artifact volume nightly to separate encrypted storage; retain 14 daily backups. Pilot recovery targets are at most 24 hours of data loss and restoration within four hours. Verify consistency through a manifest linking record IDs to artifact hashes, and test restoration before release.

Use Alembic migrations and synthetic seed records in development. Back up before production schema changes, apply compatible migrations before new workers start, and restore from backup if a migration cannot be safely reversed. Never overwrite immutable snapshots to repair historical data; create a new version.
