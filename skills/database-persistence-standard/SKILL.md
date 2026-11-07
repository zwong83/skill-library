---
name: database-persistence-standard
description: Design, implement, or review reliable data persistence, including datastore selection, ownership, logical and physical models, constraints, access paths, queries, indexes, transactions, isolation, locking, concurrency, migrations, backfills, retention, backup, restore, pooling, security, and operations.
---

# Database Persistence Standard

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
12. Keep persistence errors and models behind stable application boundaries; coordinate failure translation with `error-handling-standard`.

## Workflow

1. Identify the source of truth, owning component, data classification, invariants, lifecycle, and consumers.
2. Capture read/write patterns, cardinality, volume, growth, hotspots, latency, availability, consistency, RPO, and RTO.
3. Select the datastore and record rejected alternatives, operational dependencies, and portability assumptions.
4. Define the logical schema, relationships, constraints, keys, tenant boundary, retention, and deletion behavior.
5. Define queries, access paths, indexes, pagination, batching, and plan-verification evidence.
6. Define transaction boundaries, isolation, locks, conflict handling, idempotency, and multi-resource consistency.
7. Define migration, backfill, rollout, mixed-version compatibility, validation, and recovery.
8. Define pooling, timeouts, replication, backup/restore, monitoring, capacity, and operational ownership.
9. Add unit, integration, concurrency, migration, performance, and restore verification.
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

## Reference Routing

- Read [data-model-and-access.md](references/data-model-and-access.md) for ownership, datastore selection, schemas, constraints, queries, indexes, pagination, and pooling.
- Read [transactions-migrations-and-operations.md](references/transactions-migrations-and-operations.md) for transactions, isolation, locking, migrations, backfills, backup, restore, and operational checks.
- Invoke `layered-architecture-standard` for repository, port, adapter, dependency, and transaction-boundary placement.
- Invoke `messaging-standard` when consistency crosses a message broker or requires outbox/inbox behavior.
- Invoke `caching-standard` when cached state changes consistency or invalidation behavior.
- Invoke `software-security-standard` for access, encryption, secrets, privacy, audit, and destructive-data controls.
- Invoke `resilience-standard` for database dependency timeouts, overload, degradation, and recovery behavior.

## System Design and SDD Boundary

- In System Design, decide ownership, datastore, schema, invariants, access paths, transaction and consistency strategy, migration approach, retention, and recovery objectives.
- In SDD, implement approved entities or records, migrations, repositories, queries, indexes, transaction code, pool settings, backfills, telemetry, and tests.
- If implementation reveals a material ownership, datastore, schema, invariant, transaction, consistency, migration, or recovery change, return it to System Design before coding proceeds.

## Standards Basis

Use the official documentation for the selected datastore and driver. The bundled PostgreSQL references illustrate mature relational behavior but are not universal rules; verify semantics against the deployed product and version.

## Expected Output

Return the datastore decision, ownership and data classification, logical schema, constraints, access patterns and indexes, transaction and concurrency model, migration and backfill plan, retention and deletion behavior, backup and restore plan, capacity and operations, security controls, verification evidence, assumptions, and unresolved decisions.
