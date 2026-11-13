# Caching Review Checklist

Report each item as `Pass`, `Gap`, `Needs decision`, or `Not applicable`.

- A measurable requirement justifies the cache.
- Source of truth and tolerated staleness are explicit for every value.
- One primary technology per workload matches the sharing scope, freshness, and failure requirements. The chosen pattern or HTTP policy fits that technology.
- Every additional layer addresses a distinct requirement and has an explicit lookup order, freshness policy, invalidation path, and fallback.
- Redis or another cache technology has an explicit role; cache behavior is not confused with sessions, messaging, locking, rate limiting, or authoritative storage.
- Key namespace, version, tenant scope, cardinality, value schema, serializer, and size are defined.
- TTL, jitter, soft/hard expiry, refresh, and no-expiry exceptions are justified.
- Write/invalidation ordering, races, reconciliation, and schema migration are handled.
- Cold cache, miss, eviction, restart, cache outage, and source outage preserve the approved behavior.
- Stampede, penetration, avalanche, hot-key, and fallback-load risks are bounded.
- Sensitive data, authorization, tenant isolation, retention, and deletion are addressed.
- Capacity, eviction policy, timeouts, pools, retries, and operational ownership are explicit.
- Redis data type/command complexity, transaction/script semantics, topology, persistence, replication/failover, Cluster slot constraints, and client behavior are verified when applicable.
- Metrics, traces, logs, dashboards, and alerts reveal cache and source impact.
- Tests cover concurrency, staleness, invalidation races, corrupt values, failure, and rollout/rollback.
