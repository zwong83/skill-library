# Cache Consistency

Define the source of truth and the maximum acceptable staleness. For cache-aside writes, decide whether to invalidate after the database commit, update the cache, or use an outbox/event to repair invalidation failures. Analyze concurrent readers, stale resurrection, delete/update races, retries, and partial failure.

If stale reads are allowed, state the bound and expose it in tests and operations. If they are not allowed, a cache may be the wrong abstraction for that read path. Never claim strong consistency from TTL alone.

| Observed failure | Mechanism to consider |
|---|---|
| Source commit succeeds, but the cache delete fails | Retry invalidation within a bounded policy. Use a durable outbox or change event when a process crash could lose the retry and violate the stale window. Make invalidation idempotent. |
| A reader starts before the commit, loads the old value, and refills the cache after the writer deletes the key | Use an authoritative generation or version check to reject stale refills when supported by the design. Define how the reader discovers the current generation and test this exact interleaving. |
| Duplicate or reordered invalidation events leave an old value cached | Carry source versions and apply changes monotonically, or invalidate without overwriting a newer value. Verify duplicate handling and replay. |

For a full key, TTL, or invalidation contract, use [Keys, TTL, and Consistency](keys-ttl-and-consistency.md). For command-specific expiry or tracking behavior, use [Redis cache lifecycle](redis-cache-lifecycle.md).
