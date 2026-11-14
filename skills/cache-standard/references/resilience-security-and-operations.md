# Cache Resilience, Security, and Operations

## Failure behavior

- **Cache unavailable:** decide fail-open to source, fail-closed, degraded response, or queued recovery per data class and source capacity.
- **Source unavailable:** decide whether stale data may be served, for how long, and how users/operators are informed.
- **Concurrent miss/stampede:** use request coalescing, single-flight, bounded lock/lease, refresh-ahead, or probabilistic early refresh. Always define timeout and lock-owner failure behavior.
- **Penetration:** validate requests, use bounded negative caching where safe, and avoid unbounded arbitrary-key access.
- **Avalanche:** jitter expiries, limit refresh concurrency, protect the source, and plan warmup.
- **Hot key:** measure skew, reduce payload/work, replicate or shard only when supported, and avoid a single global lock.

Fallback to the source must be load-shed and budgeted; an unlimited fail-open can turn a cache outage into a database outage.

## Security

Classify values before caching. Define tenant/user scope, authorization re-check requirements, encryption in transit/at rest where applicable, access control, network boundary, deletion, retention, and incident handling. Do not put tokens, passwords, raw sessions, private keys, or unrestricted personal/payment/health data in cache.

## Capacity and observability

Model working-set size, replicas/overhead, serialization size, growth, peak concurrency, network bandwidth, TTL distribution, and eviction policy. Monitor hit/miss/stale ratios, cache/source latency, error/timeout rate, memory, evictions, expired keys, connection pools, hot keys, refreshes, and fallback load.

Define rotation of schema versions, safe flush policy, backup/persistence expectations if any, operational ownership, dashboards, alerts, and recovery procedures. Alert on actionable changes such as a sustained drop in hit rate with rising source load or connection pool exhaustion. Correlate client, network, cache, and source evidence before changing settings. Never run broad destructive cache operations without an explicit scoped target and authorization.
