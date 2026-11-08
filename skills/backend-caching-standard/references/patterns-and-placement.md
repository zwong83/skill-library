# Cache Patterns and Placement

## Decision before pattern

Record the uncached baseline, target improvement, read/write ratio, update rate, item size, access distribution, tolerated staleness, source protection requirement, and behavior if the cache is unavailable. A cache that lacks a measurable purpose adds inconsistency and operational cost.

## Placement

| Placement | Strength | Main risk |
|---|---|---|
| Request/process-local | Lowest latency and no network hop | Per-instance inconsistency, memory duplication, invalidation difficulty |
| Distributed cache | Shared state and centralized capacity | Network dependency, hot keys, serialization, shared blast radius |
| CDN/edge | Offloads static/public or safely scoped content | Purge complexity, privacy, regional variation |
| Client/browser | Reduces requests and supports offline behavior | Weak invalidation control and untrusted storage |
| Multi-level | Combines latency and shared reuse | More consistency states and duplicated invalidation paths |

## Patterns

- **Cache-aside:** application reads cache, loads source on miss, stores bounded result, and invalidates/updates after source changes. Prefer as a clear default for read-heavy data with acceptable bounded staleness.
- **Read-through:** cache provider loads the source. Use only when the provider owns a well-defined loader contract and failure behavior.
- **Write-through:** write completes through the cache to the authoritative store. Define atomicity and failure semantics; do not assume both writes are one transaction.
- **Write-behind:** cache acknowledges before durable source update. Use only with an explicit durability, ordering, replay, recovery, and loss contract.
- **Refresh-ahead:** refresh before expiry for predictable hot data. Bound refresh concurrency and preserve source protection.
- **Negative caching:** cache safe not-found or rejection outcomes briefly only when authorization, creation races, and invalidation are understood.

Do not cache highly volatile or security-critical decisions merely to reduce latency. If stale data would violate correctness, authorization, financial limits, inventory guarantees, or legal obligations, use a stronger design or bypass the cache.
