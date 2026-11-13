# Redis Operations

Start with the affected request, tenant or key family, time window, and topology. Compare application command latency and fallback load with per-node Redis signals. Use representative samples and approved read-only diagnostics. Bound scans and diagnostic work on shared or busy instances.

| Symptom | Evidence and next decision |
|---|---|
| High latency or timeouts | Compare client queue/pool wait, network latency, retries, command timings, slow log entries, CPU, persistence work, and failover events. The slow log measures server-side execution time and does not account for client or network time. |
| High memory or rejected writes | Compare working-set and per-key sizes with eviction policy, fragmentation, client buffer use, and replication or persistence overhead. Check whether the keys are eligible for eviction. |
| One shard is overloaded | Check per-shard throughput and command distribution. Distinguish a hot key with many requests from a big key with expensive operations or large replies. For hot keys consider local caching or coalescing when freshness permits. For big keys bound ranges, replies, and batches. Measure serialization, replication, and deletion costs before splitting data. |
| Hit rate falls or source load spikes | Correlate expirations, evictions, cold starts, changed key namespaces, invalidation volume, and refill concurrency. Check [cache lifecycle](redis-cache-lifecycle.md) before changing TTL or eviction. |
| Intermittent errors during failover | Correlate topology changes with reconnects, redirections, pool errors, stale replica reads, and uncertain writes. Retry only operations safe to repeat. Review [topology and recovery](redis-topology-and-recovery.md) if the client contract needs to change. |

Use scoped samples from commands such as `INFO`, `SLOWLOG GET`, `MEMORY USAGE`, and `PTTL` when supported and authorized. Treat diagnostic output as potentially sensitive. Protect the backing store before warmup, bulk invalidation, or increasing retry concurrency. Verify the fix using the same latency, throughput, memory, error, eviction, connection, and source-load signals that established the fault.

[Redis latency diagnosis](https://redis.io/docs/latest/operate/oss_and_stack/management/optimization/latency/) · [SLOWLOG GET](https://redis.io/docs/latest/commands/slowlog-get/) · [MEMORY USAGE](https://redis.io/docs/latest/commands/memory-usage/)
