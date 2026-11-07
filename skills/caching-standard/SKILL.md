---
name: caching-standard
description: Design, implement, or review application and distributed caching across languages and platforms, including cache necessity, source of truth, key/schema design, TTL, invalidation, consistency, stampede protection, resilience, Redis integration, observability, security, and testing.
---

# Caching Standard

Use this skill to treat caching as an explicit consistency and failure design. A cache is not automatically required because Redis or an in-memory store is available.

## Core rules

- Prove the cache's purpose with a latency, throughput, dependency-load, availability, or cost requirement. Prefer no cache when the source can meet the requirement directly.
- Name the authoritative source of truth and the tolerated staleness for every cached value.
- Default to cache-aside for read optimization unless another pattern's ownership and consistency semantics are explicitly justified.
- Define key namespace, version, tenant scope, value schema, serialization, TTL, jitter, maximum size, invalidation owner, and behavior on cache failure.
- Treat cache misses, eviction, expiration, restart, and partial outage as normal conditions. Correctness must not depend on cache persistence unless the component is intentionally designed as an authoritative datastore.
- Prevent penetration, stampede, avalanche, and hot-key overload with bounded mechanisms suited to the workload; do not add distributed locks by reflex.
- Never cache secrets, authorization decisions, sensitive data, or negative results without explicit classification, scope, lifetime, and invalidation decisions.
- Cache keys and values must not cross tenant/user boundaries. Avoid embedding raw sensitive identifiers where a scoped opaque representation is sufficient.
- Observe hit/miss/stale/error rates, latency, evictions, memory pressure, key cardinality, refresh behavior, and source fallback load.

## Workflow

1. Define the workload, source SLO, target SLO, access distribution, update frequency, value size, and failure tolerance.
2. Decide whether caching is justified and select local, distributed, CDN/edge, client, or multi-level placement.
3. Select cache pattern and define source-of-truth, consistency, staleness, read/write, and invalidation semantics.
4. Specify key and value contracts, TTL/refresh, eviction assumptions, capacity, and tenant/security boundaries.
5. Design cache-miss, source failure, cache failure, stampede, hot-key, mass-expiry, and deployment behavior.
6. Define observability, operations, rollout, warmup, migration, and rollback.
7. Test correctness with cold/empty cache, stale entries, concurrent misses, partial failure, eviction, schema changes, and invalidation races.

## Readiness gate

Require a named source of truth, measurable cache objective, tolerated staleness, read/write behavior, data classification, tenant scope, source capacity, and cache/source failure expectations. For SDD, require the approved cache decision plus deployed cache/client constraints. Do not declare a cache implementation ready while invalidation ownership, correctness on cache loss, or sensitive-data handling is unresolved.

## Reference routing

- Read [references/patterns-and-placement.md](references/patterns-and-placement.md) when deciding whether and where to cache or selecting a read/write pattern.
- Read [references/keys-ttl-and-consistency.md](references/keys-ttl-and-consistency.md) when defining keys, schemas, TTL, refresh, invalidation, or consistency.
- Read [references/resilience-security-and-operations.md](references/resilience-security-and-operations.md) for stampede, hot keys, outages, sensitive data, observability, and capacity.
- Read [references/redis.md](references/redis.md) only when Redis is selected or being evaluated.
- Read [references/review-checklist.md](references/review-checklist.md) before approval.

## SD and SDD boundary

System Design defines why caching exists, placement, technology decision, source of truth, consistency/staleness contract, invalidation ownership, resilience, security, capacity, and operational model. SDD/OpenSpec defines concrete key formats, value schemas, TTL/jitter values, APIs/adapters, configuration, algorithms, rollout tasks, and tests for the approved change.

## Expected output

Provide a cache decision record, data/ownership matrix, read/write/invalidation flows, key/value/TTL contract, failure and stampede behavior, security and tenant isolation, capacity and observability plan, rollout/migration strategy, and verification evidence.
