# State Ownership and Data Flow

| State/data item | Class | Source of truth/owner | Lifetime/scope | Read/write path | Freshness/invalidation | Failure/recovery | Persistence/security | Evidence |
|---|---|---|---|---|---|---|---|---|

For each query or mutation record contract/version, parameters/body, response/error mapping, authorization context, cache identity, deduplication, cancellation/deadline, retry/idempotency, pagination, concurrency/conflict, optimistic behavior, invalidation/refetch, loading/error/empty UI state, telemetry, and tests.

Record contract feedback when the UI would otherwise require excessive request fan-out, unstable client joins, duplicated business rules, unsafe retries, ambiguous errors, or missing pagination/filter/sort semantics. Resolve it through the System Design Coordinator before declaring `Contract-Ready`.
