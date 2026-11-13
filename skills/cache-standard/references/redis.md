# Redis Mechanism Selector

Identify the Redis role and the decision at hand. Record the deployment type, server and client versions, and managed-service limits that affect the choice. During evaluation, state which versions or capabilities still need confirmation.

| Requirement | Mechanisms to evaluate | Reference |
|---|---|---|
| Model data, update it atomically, or reduce round trips | Data types, conditional commands, `MULTI/EXEC`, `WATCH`, Lua, Functions, pipelines, bounded key access | [Data and commands](redis-data-and-commands.md) |
| Bound freshness, fit memory, or prevent miss storms | Key and field expiry, TTL preservation, `maxmemory`, eviction, tracking and invalidation, coalescing, jitter | [Cache lifecycle](redis-cache-lifecycle.md) |
| Plan for restart, failover, sharding, or recovery | Standalone, replication, Sentinel, Cluster, hash slots, RDB, AOF, restore | [Topology and recovery](redis-topology-and-recovery.md) |
| Investigate latency, memory growth, rejected writes, hot keys, big keys, or connection failures | Command timing, memory and eviction signals, client pools, sharding and fallback load | [Redis operations](redis-operations.md) |
| Use Redis for events, durable state, sessions, counters, quotas, or coordination | Streams, Pub/Sub, atomic updates, leases, fencing, durability and loss contracts | [Redis roles beyond caching](redis-other-roles.md) |

For disposable cache entries, verify correctness and source capacity after Redis data loss. If Redis is authoritative, stores sessions, coordinates workers, or carries events, define a separate contract for that role. Use only the mechanisms justified by its requirements. Confirm exact commands, options, and availability in the [Redis command reference](https://redis.io/docs/latest/commands/) for the deployed version and product.
