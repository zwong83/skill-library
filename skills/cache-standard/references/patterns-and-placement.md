# Cache Patterns and Placement

## Choose the cache technology

Record the uncached baseline and target improvement. Identify what is cached, who can reuse it, where the latency or load occurs, and how much staleness the workload allows. Also consider item size, access distribution, update rate, source protection, and behavior when the cache is unavailable. Skip the cache when the source meets the target or the data cannot safely be reused.

| Requirement that drives the choice | Best candidate to evaluate | Check before selecting |
|---|---|---|
| Reuse computation or data within a request or app instance with no network hop | [In-process](in-process.md) | Each instance may hold a different value. Verify the freshness and memory budget per instance. |
| Reuse disposable values across app instances using simple key/value operations | [Memcached](memcached.md) | Confirm simple operations and loss on eviction or restart are sufficient, and check the existing platform and tooling. |
| Share application data across instances with Redis-specific data types, atomic updates, or topology, or reuse an existing Redis cache that meets the target | [Redis](redis.md) | Verify the specific capability on the deployed version and that its operating cost fits the workload. |
| Avoid repeat HTTP transfers for the same user agent | [Browser](browser.md) | Check that response freshness, validation, and local storage meet the privacy and update requirements. |
| Serve safely shared responses near users or reduce repeated requests to the origin | [CDN](cdn.md) | Verify that edge sharing is safe and the key includes every input that affects the response. |

When multiple choices fit, prefer the existing supported option if it meets the target without introducing another service or consistency boundary. Choose one primary technology for the workload. For example, Redis may already be the right choice for simple shared key/value caching if it is deployed and supported. Record the requirement that decided the choice and any evidence still needed.

## Choose the pattern

For in-process, Redis, or Memcached caching, choose the pattern based on who owns population, where writes become authoritative, and what freshness the consumer needs. Verify that the library or client supports the required behavior.

- **Cache-aside:** application reads cache, loads source on miss, stores bounded result, and invalidates/updates after source changes. Prefer as a clear default for read-heavy data with acceptable bounded staleness.
- **Read-through:** cache provider loads the source. Use only when the provider owns a well-defined loader contract and failure behavior.
- **Write-through:** write completes through the cache to the authoritative store. Define atomicity and failure semantics; do not assume both writes are one transaction.
- **Write-behind:** cache acknowledges before durable source update. Use only with an explicit durability, ordering, replay, recovery, and loss contract.
- **Refresh-ahead:** refresh before expiry for predictable hot data. Bound refresh concurrency and preserve source protection.
- **Negative caching:** cache safe not-found or rejection outcomes briefly only when authorization, creation races, and invalidation are understood.

For browser or CDN caching, select an HTTP policy. Use versioned URLs for immutable assets, validation or short freshness for mutable responses, and explicit private or shared scope. Choose the policy in the [browser](browser.md) or [CDN](cdn.md) reference based on where the response is reused.

## When a second layer is justified

Add a layer when it addresses a separate measured or required outcome. For example, add an in-process cache in front of Redis only if the Redis network hop prevents meeting the latency target and the app can tolerate separate per-instance freshness. Add browser caching alongside a CDN when repeat downloads on the same device are a distinct concern from origin load. Define lookup order, each layer's TTL, invalidation and fallback, and how to verify which layer served the response.

Do not cache highly volatile or security-critical decisions merely to reduce latency. If stale data would violate correctness, authorization, financial limits, inventory guarantees, or legal obligations, use a stronger design or bypass the cache.
