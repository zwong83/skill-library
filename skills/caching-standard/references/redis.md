# Redis-Specific Guidance

Apply this reference only after Redis is selected and the deployed server, topology, persistence, and client versions are known.

## Role gate

Redis can act as a cache, session/state store, counter/rate limiter, coordination service, stream, Pub/Sub transport, or authoritative datastore. State the selected role before designing keys or availability. This skill governs caching; if Redis is used for messaging, durable state, locking, sessions, or rate limiting, add a separate contract for that role rather than silently treating it as cache behavior.

A cache must remain correct after Redis data loss. An authoritative or coordination role needs explicit durability, consistency, recovery, and correctness analysis.

## Data model and commands

- Select a Redis data type for the required operations and memory profile rather than serializing every value into a string. Consider strings for opaque values/counters, hashes or JSON for records, sets for uniqueness, sorted sets for ranked/time-window data, and streams only for an intentional append-log/consumer-group design. See [Redis data types](https://redis.io/docs/latest/develop/data-types/) and [Compare data types](https://redis.io/docs/latest/develop/data-types/compare-data-types/).
- Prefer one atomic command for counters, conditional writes, membership, and bounded updates. Do not implement read-modify-write in application code when a suitable atomic operation exists.
- Use `MULTI`/`EXEC`, `WATCH`, or server-side functions/scripts only after defining their actual atomicity, error, retry, timeout, and cluster behavior. Redis transactions group command execution but do not provide relational rollback semantics. See [Redis transactions](https://redis.io/docs/latest/interact/transactions/).
- Bound pipelines, batches, scripts/functions, response size, command complexity, connection pools, command timeouts, and end-to-end deadlines. A script or large command can monopolize server execution.
- Do not use `KEYS` or unbounded scans on production request paths. Maintain explicit indexes or versioned namespaces when bulk invalidation is required.

## Cache lifecycle

- Set an explicit TTL for ordinary cache entries unless a reviewed requirement justifies no expiry.
- Select `maxmemory` and eviction behavior from workload and correctness needs; monitor evictions, expired keys, rejected writes, fragmentation, and fallback load. See [Redis key eviction](https://redis.io/docs/latest/reference/eviction/).
- Define cache warmup, cold-start load, mass-expiry protection, hot-key behavior, schema/key migration, and safe rollback.
- If client-side caching is selected, define tracking/invalidation, local TTL, reconnect behavior, per-instance memory, and behavior during lost invalidations. See [Redis client-side caching](https://redis.io/docs/latest/develop/reference/client-side-caching/).

## Topology and durability

- Decide standalone, replication with Sentinel, or Cluster from capacity, failure domains, availability, operational maturity, and key-operation requirements. Sentinel provides high availability for non-Cluster deployments; Cluster adds sharding and has different client and multi-key constraints. See [Redis Sentinel](https://redis.io/docs/latest/operate/oss_and_stack/management/sentinel/) and [Redis Cluster specification](https://redis.io/docs/latest/operate/oss_and_stack/reference/cluster-spec/).
- Redis replication is asynchronous in common topologies. Replica reads and failover can expose stale data or acknowledged-write loss windows; do not claim linearizable reads or zero data loss without a verified mechanism and configuration.
- In Cluster, multi-key commands, transactions, and scripts generally require all involved keys to map to the same hash slot. Use hash tags only when deliberate co-location, hotspot, migration, and tenant-isolation consequences are acceptable. See [Redis multi-key operations](https://redis.io/docs/latest/develop/using-commands/multi-key-operations/).
- Treat RDB, AOF, replication, failover, and backup as separate decisions. Persistence changes recovery point, startup, I/O, and storage behavior; it does not make a cache/database dual write atomic. See [Redis persistence](https://redis.io/docs/latest/management/persistence/).
- Define client discovery/redirection, reconnect, topology refresh, failover timeout, retry, and uncertain-write behavior. Retry only operations proven safe to repeat.

## Coordination caution

Do not implement distributed locks without lease expiry, unique ownership, safe conditional release, clock/pause/network-partition analysis, fencing or equivalent stale-owner protection where required, and proof that the protected invariant tolerates the lock's guarantees. Redis availability is not proof of lock correctness.
