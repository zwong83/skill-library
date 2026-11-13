# Redis Cache Lifecycle

## Expiry and invalidation

- Set value and expiry in the same command when possible. A separate write and expiry can leave a persistent key if the client fails between them. Verify whether updates preserve expiry. For example, replacing a string with `SET` clears its TTL unless expiry is set again or preserved with the appropriate option.
- Distinguish whole-key TTL from field expiration. Use field expiration only when the deployed server and client support it and independent field lifetime is required.
- Redis removes expired keys when accessed and through background expiration. A TTL is a freshness ceiling for the entry, subject to how the application populates and refreshes it. It does not prove freshness relative to a concurrent source update. For stale refills or failed invalidation, use [cache consistency](cache-consistency.md).
- Specify what happens after a source write. Choose post-commit invalidation, versioning, or durable reconciliation based on the allowed stale window. Specify which process owns invalidation, retries, and cache refill.
- Bound mass expiry and concurrent refill with jitter, request coalescing, refresh limits, and budgeted fallback. For nonexistent items, validate input and use bounded, scoped negative caching only when creation and authorization races are acceptable.

## Memory and eviction

- Choose an explicit `maxmemory` policy. `allkeys-*` policies can select keys across the cache. `volatile-*` policies only select keys with expiry. `noeviction` can reject writes that need memory instead of evicting keys. Estimate headroom for allocator fragmentation, clients, replication, and persistence overhead.
- Compare LRU, LFU, random, or shortest-remaining-TTL eviction where supported and appropriate. Use actual traffic skew, expiry distribution, and miss cost. Expiry controls age. Eviction controls capacity and can remove a key before its TTL.
- If a Redis deployment mixes disposable and durable data, make role isolation and eviction eligibility explicit. Prefer separate deployments when one role's memory pressure or eviction behavior would endanger the other.

## Client-side caching

If client-side caching is selected, confirm client tracking support, invalidation delivery, reconnect or lost-invalidation handling, and per-instance memory. Clear or revalidate locally cached data when the tracking channel is no longer trustworthy. Treat the local cache as a separate consistency layer with a bounded lifetime.

[EXPIRE](https://redis.io/docs/latest/commands/expire/) · [SET](https://redis.io/docs/latest/commands/set/) · [Key eviction](https://redis.io/docs/latest/develop/reference/eviction/) · [Client-side caching](https://redis.io/docs/latest/develop/reference/client-side-caching/)
