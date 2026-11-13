---
name: db-standard
description: Design, implement, review, or troubleshoot reliable data persistence, including datastore selection, ownership, logical and physical models, constraints, access paths, queries, indexes, transactions, isolation, locking, concurrency, migrations, backfills, retention, backup, restore, pooling, security, and operations.
---

# Database Standard

Use this skill when a change introduces or modifies durable state, a datastore, schema, query, index, transaction, migration, backfill, retention policy, or recovery behavior.

## Core Rules

1. Begin with data ownership, invariants, access patterns, volume, growth, latency, consistency, availability, retention, and recovery objectives.
2. Select a datastore from workload and operational requirements. Do not introduce polyglot persistence without a clear benefit and ownership plan.
3. Define the logical model independently from framework entities. Make identity, units, nullability, defaults, lifecycle, tenant scope, and audit fields explicit.
4. Enforce critical invariants with appropriate database constraints as well as application validation. Do not rely on comments or UI validation for data integrity.
5. Design access paths from real queries. Add indexes deliberately and verify plans; every index consumes storage and write capacity.
6. Keep transactions as small as correctness permits. State isolation needs, tolerated anomalies, locking strategy, deadlock handling, and concurrent-write behavior.
7. Use optimistic or pessimistic concurrency only with a documented conflict model and caller behavior.
8. Make queries bounded. Prevent full scans, unbounded lists, accidental fan-out, and N+1 access on critical paths.
9. Treat migrations as production changes. Use compatible staged evolution, resumable backfills, validation, observability, and a realistic recovery plan.
10. Treat backups as unproven until restore has been tested against stated recovery objectives.
11. Use parameterized queries and least-privilege database identities. Protect sensitive fields through `software-security-standard`.
12. Keep persistence errors and models behind stable application boundaries; coordinate failure translation with `exception-error-standard`.

## Mandatory workflow

**Complete steps 1 through 10 in order for every database task.** Identify the task mode and scope first. Carry out each applicable step and record its outcome. For an existing system, confirm applicable decisions against the current contract and evidence. A focused task can make a step brief, but it still needs an outcome. Use `Not applicable` only when a step does not apply and record why. Mark a step `Blocked` when it lacks a required input or decision, and stop dependent work.

Identify whether the task is selection, design, implementation, troubleshooting, or review. For an existing system, start with the affected operation and inspect the relevant datastore version, driver, pool, framework, SQL conventions, migrations, query plans, or transaction mechanism. Preserve established architecture and conventions. Reconsider the datastore only when the task or workload calls for it. Use intentional predicates for updates and deletes, and check affected row counts when correctness depends on them.

For destructive changes, large writes or backfills, or changes to transaction and lock behavior, identify affected data, performance and concurrency impact, and recovery before acting. Separate proposing or preparing a change from running it on a live database.

1. Identify the source of truth, owning component, data classification, invariants, lifecycle, and consumers.
2. Capture read/write patterns, cardinality, volume, growth, hotspots, latency, availability, consistency, RPO, and RTO.
3. Select the datastore and record the requirement-based rationale, operational dependencies, consequences, and portability assumptions without requiring a solution-comparison table.
4. Define the logical schema, relationships, constraints, keys, tenant boundary, retention, and deletion behavior.
5. Define queries, access paths, indexes, pagination, batching, and plan-verification evidence.
6. Define transaction boundaries, isolation, locks, conflict handling, idempotency, and multi-resource consistency.
7. Define migration, backfill, rollout, mixed-version compatibility, validation, and recovery.
8. Define pooling, timeouts, replication, backup/restore, monitoring, capacity, and operational ownership.
9. Verify the applicable cases with unit, integration, concurrency, migration, performance, or restore checks. Run the relevant checks for implementation, specify them for design, and assess available evidence for review.
10. Review against the readiness gate.

## Readiness Gate

Persistence design is implementation-ready only when:

- ownership, source of truth, classification, lifecycle, and invariants are explicit;
- datastore choice and operational responsibility are justified;
- schema, keys, constraints, tenant boundaries, and deletion semantics are defined;
- critical queries, indexes, limits, and plan-verification method are known;
- transactions, isolation, concurrency, deadlocks, and retries are defined;
- migrations and backfills are compatible, bounded, observable, and recoverable;
- capacity, connection limits, retention, backup, restore, RPO, and RTO are addressed;
- security and verification evidence are planned;
- unresolved decisions are assigned and block affected implementation.

Claim completion only after every workflow step has a recorded outcome. A blocked applicable step prevents a readiness claim. Report planned checks as pending verification until they run.

## Choose references for the task

Read the reference or section that addresses the current decision first. Add another only if it answers a distinct requirement or a finding changes the scope. Use the readiness gate for a full design or readiness review and assess the items affected by a focused change.

| Decision or symptom | Start here |
|---|---|
| Select a datastore or justify moving off an existing one | [Database selection](references/selection.md). Use [store selection](references/data-model-and-access.md#store-selection) when the decision must be recorded in System Design. |
| Design entities, relationships, keys, constraints, or normalization | [Database design](references/design.md). Use [ownership](references/data-model-and-access.md#ownership-and-source-of-truth) or [logical and physical model](references/data-model-and-access.md#logical-and-physical-model) when the decision concerns data authority, tenant scope, retention, or physical representation. |
| Investigate a slow query, choose an index, or design pagination or batching | [Queries and access paths](references/data-model-and-access.md#queries-and-access-paths) or [pagination and batching](references/data-model-and-access.md#pagination-and-batching), depending on the issue. |
| Write or review SQL/DML, persistence framework code, or database access tests | [Implementation and DML](references/implementation.md). For a pool or driver issue, start with [connections and drivers](references/data-model-and-access.md#connections-and-drivers). |
| Diagnose deadlocks or choose isolation, locking, conflict handling, or a cross-resource consistency strategy | [Transactions and isolation](references/transactions-migrations-and-operations.md#transactions-and-isolation) or [multi-resource consistency](references/transactions-migrations-and-operations.md#multi-resource-consistency) for a cross-resource write. |
| Evolve a schema or move existing data | [Migration lifecycle](references/transactions-migrations-and-operations.md#migration-lifecycle). Use [backfills](references/transactions-migrations-and-operations.md#backfills) when data must be rewritten. |
| Set recovery objectives, verify a restore, or review database operations | [Backup, restore, and recovery](references/transactions-migrations-and-operations.md#backup-restore-and-recovery) or [operational review](references/transactions-migrations-and-operations.md#operational-review), based on the task. |

For example, investigate a slow query using the access-path section and its execution plan. Add transaction guidance if lock evidence explains the slowdown. Datastore selection applies only if there is a separate reason to evaluate the datastore.

### Related skills

Use these when the task crosses the corresponding boundary.

- Invoke `backend-layered-architecture-standard` for repository, port, adapter, dependency, and transaction-boundary placement.
- Invoke `message-standard` when consistency crosses a message broker or requires outbox/inbox behavior.
- Invoke `cache-standard` when cached state changes consistency or invalidation behavior.
- Invoke `software-security-standard` for access, encryption, secrets, privacy, audit, and destructive-data controls.
- Invoke `backend-resilience-standard` for database dependency timeouts, overload, degradation, and recovery behavior.

## System Design and SDD Boundary

- In System Design, decide ownership, datastore, conceptual/logical/physical schema, invariants, access paths, transaction and consistency strategy, migration approach, retention, and recovery objectives. Produce dialect/version-specific proposed DDL for affected structures plus a parameterized DML/query catalog for state-changing operations and critical reads; these are reviewed design artifacts, not applied migrations.
- In SDD, validate those artifacts against the actual datastore/toolchain and implement approved entities or records, executable migrations, repositories, queries, indexes, transaction code, pool settings, backfills, telemetry, and tests without silently changing the approved data contract.
- If implementation reveals a material ownership, datastore, schema, invariant, transaction, consistency, migration, or recovery change, return it to System Design before coding proceeds.

## Standards Basis

Use the official documentation for the selected datastore and driver. The bundled PostgreSQL references illustrate mature relational behavior but are not universal rules; verify semantics against the deployed product and version.

## Expected Output

Include a brief numbered record of steps 1 through 10 with the outcome and evidence or next action for each step. Explain any `Not applicable` or `Blocked` outcomes.

Report the affected decisions, artifacts, risks, and verification. For a full design, include applicable datastore and ownership decisions, models, proposed DDL and parameterized DML, access paths, transaction and concurrency behavior, migration and recovery, operations, security, and unresolved decisions.
