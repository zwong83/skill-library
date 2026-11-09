# System Design Data, DDL, DML, and Middleware Artifacts

Load this reference when a feature reads or changes durable data, introduces schema/access-path work, or uses database/cache/queue/stream/search/scheduler/object-storage or equivalent middleware.

## Data design authority

Backend SD owns data semantics, ownership, invariants, transactions, access behavior, migration, and recovery. Versioned database artifacts under `output/SD/database/` own physical structure and proposed SQL when no project convention exists. These are design artifacts; do not execute them or report them as applied migrations.

Use only applicable artifacts:

```text
output/SD/database/
├── data-dictionary.md
├── schema.sql
├── dml-catalog.md
├── transaction-concurrency-matrix.md
├── indexes-and-access-paths.md
└── migrations/
    ├── <change>-forward.sql
    ├── <change>-backfill.sql
    └── <change>-recovery.md
```

Do not create placeholders for unaffected concerns.

## Required data views and records

When durable data is in scope, define:

1. conceptual/logical model linked to SA concepts;
2. physical ERD with tables/collections, keys, relationships, cardinality, tenant/ownership boundary, and lifecycle;
3. data dictionary with type, unit/format, nullability, default, classification, source, invariant, retention, and audit behavior;
4. dialect/version-specific proposed DDL for affected structures, including keys, constraints, indexes, partitions, comments, and ownership/security assumptions;
5. DML/query catalog for every feature's state-changing operation and critical read path;
6. transaction/concurrency matrix covering boundary, isolation, locks/versioning, idempotency, deadlock/conflict behavior, and multi-resource consistency;
7. index/access-path plan tied to bounded queries, cardinality, ordering/pagination, expected plan, and verification;
8. forward migration, compatibility/backfill, validation, rollback or roll-forward/recovery, and mixed-version sequence;
9. retention/deletion, backup/restore, RPO/RTO, capacity, pooling, timeout, observability, and ownership.

## DML/query catalog

For each affected feature operation record:

| DML ID | Feature/flow ID | Purpose | Tables/data | Parameterized statement or repository contract | Cardinality/bounds | Transaction | Lock/conflict | Index/access path | Errors/result | Verification |
|---|---|---|---|---|---|---|---|---|---|---|

Use parameterized SQL or a precise language-neutral repository/query contract. Never concatenate user input into SQL. Include insert/update/delete/upsert, idempotent writes, optimistic/pessimistic conditions, soft/hard deletion, batch limits, pagination, and critical reads only where applicable. Do not dump generated ORM boilerplate.

## Middleware design register

Record every current or proposed middleware dependency, including database, cache, broker/stream, search, scheduler, object storage, gateway, or equivalent platform service.

| Middleware ID | Current/Proposed | Type/product/version | Feature IDs | Purpose | Owner | Topology | Data/contract | Consistency | Failure/recovery | Capacity | Security | Observability/operations | Status |
|---|---|---|---|---|---|---|---|---|---|---|---|---|---|

Do not introduce middleware merely to fill the register. A `Not Applicable` decision needs a scope-based rationale.

For each selected middleware, provide:

- deployment/topology diagram with producers/consumers/clients, clusters/nodes when relevant, zones, trust boundaries, ownership, and dependencies;
- per-feature runtime sequence showing read/write/publish/consume/invalidate/acknowledge behavior and transaction boundary;
- configuration and contract summary, including versions and compatibility assumptions;
- consistency, ordering, duplicate/idempotency, timeout, retry/backoff, DLQ/quarantine/replay, fallback/degradation, reconciliation, and recovery as applicable;
- data classification, authentication/authorization, encryption/secrets boundary, tenant isolation, retention, and audit;
- throughput, payload/value size, connection/concurrency, storage/retention, headroom, quotas, and scaling;
- logs, metrics, traces, alerts, dashboards, runbooks, support owner, maintenance, backup/restore where applicable, and verification.

Use `backend-caching-standard` for cache semantics, `backend-messaging-standard` for queues/streams, `backend-database-persistence-standard` for durable stores, and the applicable operational/security/resilience standards. Load only the technology reference that is actually selected.
