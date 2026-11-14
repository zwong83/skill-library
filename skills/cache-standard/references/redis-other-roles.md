# Redis Roles Beyond Caching

| Role | Mechanism to evaluate | Contract to establish |
|---|---|---|
| Live notifications and best-effort invalidation hints | Pub/Sub | At-most-once delivery. A disconnected subscriber can miss messages. Define reconnection and reconciliation when missing an event matters. |
| Replayable event log or consumer group | Streams | IDs, retention and trimming, acknowledgement, pending entries, recovery of abandoned work, and idempotent processing. Verify durability under the selected persistence and failover model. |
| Session or authoritative application state | Keys and suitable Redis data types | Expiry, eviction isolation, consistency, accepted loss, backup, and restore. Route durable-state design through `db-standard`. |
| Counter, quota, or rate limit | Atomic increment, conditional set, or a bounded script | Define window, key cardinality, expiry, atomicity of update plus expiry, and fail-open or fail-closed behavior. |
| Lock, lease, singleton task, or leader coordination | Scoped lease with unique ownership and conditional release | Use the [Redis lease](coordination-and-idempotency.md#redis-lease) and the [lock contract](coordination-and-idempotency.md#lock-and-lease-contract) sections as applicable. |
| Cache-backed duplicate suppression | Stable deduplication key and bounded retention | Use [cache-backed deduplication](coordination-and-idempotency.md#cache-backed-deduplication) to define loss and concurrent-attempt behavior. |

Route replay, delivery, ordering, or consumer concerns through `message-standard`. For a cache refill lock, decide whether duplicate work is harmless and whether local request coalescing meets the requirement. Do not treat cache availability, lock acquisition, or replica acknowledgement as proof that a protected business invariant holds.

[Redis Pub/Sub](https://redis.io/docs/latest/develop/pubsub/) · [Redis Streams](https://redis.io/docs/latest/develop/data-types/streams/)
