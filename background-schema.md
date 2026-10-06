# 5. Background Schema

This document defines the backend data model: what the app stores, how records relate, who can access them, and how storage is managed.

**Project:** [App name]  
**Status:** [Draft / Agreed / Revised]  
**Owner:** [Name or role]  
**Last updated:** [YYYY-MM-DD]

## Data inventory

| Entity ID | Entity | Purpose | Source | Owner | Sensitivity |
| --- | --- | --- | --- | --- | --- |
| E-01 | [Entity name] | [Why it exists] | [User input, import, or service] | [Responsible role] | [Classification] |

Identify which system is the source of truth when data comes from an external service. Include only data needed for the product's features.

## Entity definitions

Repeat this section for every entity or collection.

### E-01: [Entity name]

| Field | Data type | Required | Default | Constraints | Description |
| --- | --- | --- | --- | --- | --- |
| [Field name] | [Type and size] | [Yes / No] | [Value or none] | [Unique, range, or other rule] | [Meaning] |

- **Primary identifier:** [How records are uniquely identified]
- **Relationships:** [Linked entities, cardinality, and foreign keys where applicable]
- **Indexes:** [Indexes required for expected queries]
- **Ownership:** [User, team, tenant, or other ownership boundary]
- **Lifecycle:** [Creation, updates, archiving, and deletion]
- **Time rules:** [Timezone, timestamp format, and date boundaries where relevant]

## Relationship map

| Source entity | Relationship | Target entity | Deletion behavior |
| --- | --- | --- | --- |
| [Entity] | [One-to-one, one-to-many, or many-to-many] | [Entity] | [Restrict, cascade, or retain] |

Add an entity relationship diagram when it makes the model easier to understand.

## Access control

Define how identities are verified, then describe permissions separately. Document the actual roles required by the app.

| Role | Resource | Create | Read | Update | Delete | Record scope or conditions |
| --- | --- | --- | --- | --- | --- | --- |
| [Role] | [Entity or resource] | [Allow / Deny] | [Allow / Deny] | [Allow / Deny] | [Allow / Deny] | [Own records, team, tenant, or all] |

Specify field-level restrictions, administrator exceptions, permission assignment, and audit requirements where applicable. Enforce authorization on the server for every request, deny unspecified access, and prevent access outside the user's allowed record scope.

## Data storage

| Data category | Storage location or service | Format | Protection | Retention and deletion |
| --- | --- | --- | --- | --- |
| Structured records | [Database] | [Tables or collections] | [Access and encryption rules] | [Policy] |
| Uploaded files | [Storage] | [Allowed formats and size limits] | [Visibility and access rules] | [Policy] |
| Logs and audit records | [Storage] | [Format] | [Access and redaction rules] | [Policy] |

Mark unused categories as `Not applicable`. Distinguish persistent records from caches and temporary files.

## Validation and integrity

Define required fields, uniqueness, allowed values, referential integrity, duplicate handling, and transaction boundaries for related writes. State how input validation and database constraints work together.

## Backups, recovery, and migrations

Describe backup frequency, retention, storage protection, recovery targets, and restore verification. Define how schema versions, migrations, initial data, and rollback or recovery are handled without losing existing records.

## Completion criteria

This document is ready when every persistent feature has defined entities and relationships, each operation has explicit permissions, and storage, deletion, backup, and schema-change behavior are documented.
