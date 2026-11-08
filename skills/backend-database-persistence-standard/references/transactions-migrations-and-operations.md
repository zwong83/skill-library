# Transactions, Migrations, and Operations

## Transactions and Isolation

Define the invariant protected by each transaction and the exact resources it covers. Keep external network calls outside database transactions unless the consistency design explicitly requires and safely handles them.

Review relevant anomalies: dirty read, non-repeatable read, phantom, lost update, write skew, and serialization failure. Select the lowest isolation level that still preserves the required invariant, based on the selected database's actual behavior.

For concurrent updates choose and document one or more of:

- atomic database statement or constraint;
- optimistic concurrency using a version or compare-and-set condition;
- pessimistic row or advisory lock with ordering and timeout;
- serializable transaction with bounded retry of the whole transaction;
- single-writer or partitioned ownership.

Define deadlock detection, retry ownership, maximum attempts, idempotency, and user-visible conflict behavior. Never retry an unknown or non-idempotent partial outcome blindly.

## Multi-Resource Consistency

When a workflow spans a database and another system, state whether it uses an outbox, inbox, saga, reconciliation job, idempotent consumer, or another explicit consistency mechanism. Do not imply atomicity across independent resources without a supported distributed transaction and operational plan.

## Migration Lifecycle

Prefer staged expand-migrate-contract evolution:

1. Expand with a backward-compatible schema change.
2. Deploy code that can coexist with old and new schema or data shapes.
3. Backfill or migrate data with bounded, resumable work.
4. Validate completeness, correctness, and performance.
5. Switch reads and writes through a controlled rollout.
6. Observe for the agreed compatibility window.
7. Contract only after old code and consumers are absent.

Assess lock duration, table rewrite, replication lag, disk growth, index build mode, transaction log growth, and rollback implications using the deployed database's documentation.

## Backfills

A production backfill needs:

- stable selection and checkpointing;
- idempotent or safely resumable processing;
- batch size, rate limit, pause, and kill switch;
- transaction scope and conflict behavior;
- progress, throughput, error, lag, and saturation metrics;
- reconciliation queries and acceptance thresholds;
- handling for rows modified while the backfill runs;
- capacity and cleanup planning.

Rollback may require a forward repair rather than reversing a destructive migration. State the actual recovery path.

## Backup, Restore, and Recovery

Define RPO and RTO, backup frequency, retention, encryption, access control, geographic or failure-domain placement, and restore ownership. Verify restore procedures on a schedule, including application compatibility, keys, dependent schemas, and point-in-time recovery where required.

Replication improves availability but is not a substitute for backup. Define failover, consistency or lag expectations, read routing, split-brain prevention, and failback.

## Operational Review

- Are growth, capacity thresholds, partitions, and maintenance owned?
- Can schema changes coexist with rolling deployment and rollback?
- Are slow queries, locks, deadlocks, saturation, errors, storage, lag, and backup freshness observable?
- Are retention, archival, erasure, and legal hold requirements enforceable?
- Has restore been demonstrated against RPO and RTO?
- Are migration, concurrency, load, failover, and recovery tests representative?

## Primary References

- [PostgreSQL: Concurrency Control](https://www.postgresql.org/docs/current/mvcc.html)
- [PostgreSQL: Transaction Isolation](https://www.postgresql.org/docs/current/transaction-iso.html)
- [PostgreSQL: Indexes](https://www.postgresql.org/docs/current/indexes.html)
- [PostgreSQL: Using EXPLAIN](https://www.postgresql.org/docs/current/using-explain.html)
