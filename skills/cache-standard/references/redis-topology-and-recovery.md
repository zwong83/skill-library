# Redis Topology and Recovery

| Requirement | Mechanism | Decision to verify |
|---|---|---|
| Simple, disposable cache that can tolerate restart | Standalone | Rebuild time, cold source load, fallback limits, and outage tolerance |
| Replicas and automatic failover without sharding | Replication with Sentinel or managed failover | Failure domains, quorum where applicable, client discovery, reconnect and promotion behavior |
| Shard data and throughput across primaries | Redis Cluster | Slot distribution, per-shard skew, cluster-aware clients, resharding behavior and multi-key constraints |
| Recover state from periodic snapshots | RDB | Snapshot frequency, recoverable data window, snapshot overhead, and actual restore time |
| Replay writes from an append-only log | AOF | Sync policy and loss window, rewrite overhead, storage capacity, startup time, and backup/restore |

Replication is normally asynchronous. Specify whether reads use primaries or replicas, what lag is acceptable, and what happens when an acknowledged write is missing after failover. Replica acknowledgements can reduce the risk of losing writes. Verify the guarantee for the product and configuration before claiming zero loss or strong consistency.

Cluster uses hash slots to route keys. Multi-key operations, transactions, and scripts generally need the relevant keys in one slot. Use hash tags only to colocate keys that must be operated on together. Validate tenant boundaries, per-slot skew, cluster redirections, resharding, and client topology refresh before relying on that layout.

Treat persistence, replication, failover, and backups as separate decisions. No Redis persistence mode makes a write to Redis and a database atomic. Exercise restart, restore, failover, and uncertain command outcomes in a representative environment. For a disposable cache, test recovery and budget backing-store load when all entries disappear.

[Replication](https://redis.io/docs/latest/operate/oss_and_stack/management/replication/) · [Sentinel](https://redis.io/docs/latest/operate/oss_and_stack/management/sentinel/) · [Cluster specification](https://redis.io/docs/latest/operate/oss_and_stack/reference/cluster-spec/) · [Persistence](https://redis.io/docs/latest/operate/oss_and_stack/management/persistence/)
