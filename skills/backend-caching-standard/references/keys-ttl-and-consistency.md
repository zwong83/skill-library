# Keys, TTL, and Consistency

## Key contract

Define a stable, documented format such as:

```text
<environment>:<service>:<feature>:v<schema>:<tenant-scope>:<entity>:<opaque-id>
```

Include only dimensions required for uniqueness and isolation. Bound key length and cardinality. Version keys or values when incompatible schema changes must coexist. Never rely on broad production key scans for normal invalidation.

## Value contract

Specify schema/version, serializer, compression threshold, maximum size, null/not-found representation, creation/source timestamp, and compatibility behavior. Validate decoded values and treat corrupt or unknown versions as misses unless a stricter contract applies.

## TTL and refresh

TTL follows business staleness tolerance and recovery needs, not an arbitrary universal default. Define:

- base TTL and bounded jitter to avoid synchronized expiry;
- hard expiry and any soft/stale-while-revalidate window;
- refresh ownership, concurrency, timeout, and fallback;
- treatment of no-expiry keys and memory pressure;
- deployment/schema migration behavior.

## Write and invalidation

For cache-aside updates, treat the authoritative write and cache invalidation as separate failure-prone actions. Define ordering, retry/reconciliation, and the stale window. Common options include invalidate-after-write, versioned keys, event/CDC-driven invalidation, or a project-approved coordination pattern.

Delayed double-delete may reduce a specific read/write race, but it is not a universal consistency guarantee. If selected, document the race being mitigated, delay basis, retry/durability of the second delete, process-crash behavior, residual stale window, source load, and reconciliation. Prefer versioning or durable invalidation events when they better match the required guarantee.

Never claim atomic cache/database consistency without a mechanism that actually spans both systems. Design consumers of invalidation events to be idempotent and tolerant of duplicates, delay, and reordering.

Redis documents cache-aside as loading on miss with TTL-bounded staleness and invalidating after source updates: [Redis cache-aside](https://redis.io/docs/latest/develop/use-cases/cache-aside/).
