# In-Process Caching

## Placement and consistency

- Use a request-scoped cache for reuse within one request. Use a process-wide cache when repeated work across requests justifies the memory cost and each app instance can tolerate its own cache state.
- Treat a process restart or rolling deployment as a cold start. If an instance can miss invalidation events, define bounded expiry, versioning, or reconciliation. A local cache in front of Redis needs its own freshness limit and invalidation behavior.
- Scope keys by the data or tenant boundary when needed. Use immutable values or defensive copies when callers could otherwise mutate shared state.

## Memory, expiry, and eviction

- Set an entry or weight limit and bound individual values. Use weight when values vary greatly in size. Include overhead and per-instance duplication when budgeting memory.
- Choose expiry after write for a fixed age bound. Use expiry after access when removing idle entries is the goal. Pair access expiry with an age bound if frequently accessed values must still be refreshed.
- Use the project's existing cache library and verify its expiry, weight, refresh, and removal behavior. [Caffeine eviction](https://github.com/ben-manes/caffeine/wiki/Eviction) · [ASP.NET Core memory caching](https://learn.microsoft.com/en-us/aspnet/core/performance/caching/memory)

## Concurrent loads and verification

- Coalesce expensive misses per key if supported. Define loader deadlines, what waiters observe on failure, and how failed loads are removed or retried. Bound warmup and refresh concurrency to protect the source.
- Measure per-instance hit rate, entry count or weight, eviction, loader latency and errors, and source load. Verify concurrent misses, eviction, restart, and freshness across instances when those cases affect the requirement.
