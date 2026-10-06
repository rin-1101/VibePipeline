# 6. Implementation Plan: MarketLens AI

**Status:** Proposed sample specification; all tasks not started  
**Owner:** Engineering lead  
**Last updated:** 2026-10-06

## Objective and planning assumptions

Deliver a research-oriented pilot covering F-01 through F-07. Use the other documents in this folder as the requirements baseline. The first milestone is a clearly labeled synthetic-data demonstration; a live-data pilot additionally requires provider rights, eligible evaluated models, integrated identity, and operational verification.

Assume a small team with frontend, backend, ML, and operations responsibilities. Estimates below are person-days of effort, not promised calendar dates; procurement and review lead times are excluded.

## Build order and tasks

| Task | Work and references | Depends on | Owner | Estimate | Completion check |
| --- | --- | --- | --- | --- | --- |
| T-01 | Confirm data mode/provider rights, identity provider, hosting, release gates, and dependency versions. All features. | None | Product/engineering | 2-3 days | Decisions recorded; live access rights and unresolved blockers identified; stack versions locked before coding. |
| T-02 | Set up React, FastAPI, PostgreSQL, migrations, worker skeleton, environment configuration, and CI. | T-01 | Backend/frontend | 2-3 days | Local build starts successfully; readiness checks and clean database migration work. |
| T-03 | Implement E-02/E-03/E-04, immutable snapshots, calendar rules, validated CSV fixtures, and the provider adapter. F-03. | T-02 | Backend/ML | 3-5 days | Repeat imports are idempotent; invalid bars rejected; synthetic mode labeled; source and adjustment policy recorded. |
| T-04 | Implement design tokens, navigation, accessible shared controls, chart scaffold, and responsive shell. P-01 through P-07. | T-02 | Frontend | 2-3 days | Shared components follow the design brief and work at 360px and desktop widths. |
| T-05 | Implement OIDC sessions, E-01, ownership checks, role enforcement, and audit foundation. F-01; E-10. | T-02 | Backend | 3-4 days | Sign-in/sign-out work; expired sessions are rejected; analyst admin access and cross-user watchlist access are denied. |
| T-06 | Build causal features, per-symbol/horizon models, chronological folds, final holdout reports, and E-05/E-08. F-06. | T-03 | ML | 4-6 days | Reproducible reports include baseline and coverage; leakage checks pass; failed candidates remain unavailable. |
| T-07 | Implement job claiming, promotion gates, forecast generation, E-06/E-09, and forecast API. F-04/F-07. | T-05, T-06 | Backend/ML | 3-4 days | Published responses trace to eligible models; quantile crossings are rejected; partial batches stay invisible. |
| T-08 | Connect search, stock history, forecast views, and evaluation pages. F-02/F-03/F-04/F-06; P-02/P-03/P-04/P-06. | T-03, T-04, T-05, T-07 | Frontend/backend | 3-5 days | Complete stock-to-forecast journey works, including stale, demo, and unavailable states. |
| T-09 | Add persistent watchlist and its page. F-05; P-05; E-07. | T-04, T-05, T-08 | Frontend/backend | 1-2 days | Add/remove persists; duplicate adds are safe; user isolation is verified. |
| T-10 | Add admin job UI, model promotion, freshness monitoring, alerts, and retry policy. F-07; P-07. | T-04, T-07 | Backend/operations | 2-3 days | Only admins queue/promote; jobs survive worker interruption; audit trail and sanitized failures are visible. |
| T-11 | Validate requirements, model gates, accessibility, compatibility, load, security, and recovery. All features. | T-08, T-09, T-10 | Entire team | 3-5 days | Required checks have recorded results; critical defects resolved; live mode uses licensed inputs and eligible models. |
| T-12 | Deploy pilot, check service health, verify rollback, and hand over operations documentation. | T-11 | Operations | 1-2 days | Staging and target-host smoke checks pass; freshness/alerts work; recovery procedure is demonstrated. |

T-03, T-04, and T-05 may overlap after the foundation is stable. T-06 follows validated data, and forecast UI integration follows a concrete forecast API. Keep work ordered by these dependencies even if multiple team members are available.

## First complete feature

Before expanding to all five symbols, complete one stock with the one-session horizon: validated import, model evaluation, authorized API, historical chart, forecast display, and unavailable/error handling. Use this journey to settle the contracts before adding the remaining stock/horizon pairs.

## Milestones

| Milestone | Tasks | Evidence |
| --- | --- | --- |
| Foundation ready | T-01, T-02, T-04, T-05 | Local application and authenticated shell with locked dependencies. |
| Data and model experiment ready | T-03, T-06 | Immutable synthetic or licensed datasets and reproducible evaluation reports; quality gates may fail. |
| Demonstration ready | T-07, T-08 | Complete labeled demo journey with visible uncertainty and provenance. |
| Feature-complete candidate | T-09, T-10 | Personal watchlist and restricted admin operations. |
| Live pilot ready | T-11, T-12 | Recorded live-data, identity, model, load, deployment, and recovery checks. |

Dates are assigned after T-01 confirms team capacity and external dependencies. Completing a synthetic demonstration does not establish live model performance or deployment readiness.

## Meaningful verification

- **Data and ML:** Features cannot see later bars; training labels do not overlap evaluation windows; historical revision limitations are recorded; baseline comparisons use identical test rows; interval metrics and price conversions are independently checked.
- **Access:** Anonymous requests fail; analysts cannot invoke admin endpoints; users cannot read or remove other watchlists; worker credentials cannot assign roles.
- **Interaction:** Search, range changes, horizon changes, save/remove, session expiry, stale datasets, missing models, and provider failures produce the documented flows.
- **Operations:** Jobs are claimed once, interrupted jobs are safely retried, promotion is atomic, deployment health is checked, and a backup is restored with its referenced artifacts.
- **Usability:** Keyboard navigation, chart text alternatives, contrast, mobile layout, and pilot tasks meet the agreed criteria.

Record actual commands, environment, dataset hashes, model IDs, dates, and results after running checks. None of these checks have been performed merely by writing this plan.

## Risks and responses

| Risk | Response | Owner |
| --- | --- | --- |
| Models do not beat the baseline or meet interval gates | Keep affected pairs unavailable; report results and evaluate a new future holdout before reconsidering promotion. | ML lead |
| Data provider limits or license prevent display | Continue a labeled synthetic demonstration; revise coverage or obtain appropriate rights before live mode. | Product lead |
| Leakage or retrospective data revisions exaggerate evaluation | Use causal features, purged chronological splits, frozen snapshots, and explicit retrospective labels. | ML lead |
| Partial jobs or interrupted imports corrupt published results | Use immutable inputs, transactional writes, heartbeat recovery, and atomic publication. | Backend lead |
| Operational restore exceeds pilot targets | Test early, measure restoration, and adjust storage or procedures before release. | Operations lead |

## Definition of done

Every included feature meets [Product Requirements](product-requirements.md); visible behavior matches [App Flow](app-flow.md) and [Design Brief](design-brief.md); data and permissions match [Background Schema](background-schema.md); engineering checks match [Technical Requirements](technical-requirements.md).

The live pilot additionally requires licensed data, eligible enabled models, deployment evidence, and a tested operational handover. Track missing evidence as outstanding work, not as completed implementation.
