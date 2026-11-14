---
name: cache-standard
description: Choose the cache technology that best fits a requirement, then select a compatible pattern. Design, implement, review, or troubleshoot in-process, Redis, Memcached, browser, and CDN caching using references for the selected technology and pattern.
---

# Cache Standard

Use this skill to treat caching as an explicit consistency and failure design. A cache is not automatically required because Redis or an in-memory store is available.

## Core rules

- Prove the cache's purpose with a latency, throughput, dependency-load, availability, or cost requirement. Prefer no cache when the source can meet the requirement directly.
- Name the authoritative source of truth and the tolerated staleness for every cached value.
- For application-managed read caching, prefer cache-aside when the app owns cache population and can tolerate bounded staleness. For browser and CDN response caching, define HTTP cache policy and validation behavior.
- Define key namespace, version, tenant scope, value schema, serialization, TTL, jitter, maximum size, invalidation owner, and behavior on cache failure.
- Treat cache misses, eviction, expiration, restart, and partial outage as normal conditions. Correctness must not depend on cache persistence unless the component is intentionally designed as an authoritative datastore.
- Prevent penetration, stampede, avalanche, and hot-key overload with bounded mechanisms suited to the workload; do not add distributed locks by reflex.
- Never cache secrets, authorization decisions, sensitive data, or negative results without explicit classification, scope, lifetime, and invalidation decisions.
- Cache keys and values must not cross tenant/user boundaries. Avoid embedding raw sensitive identifiers where a scoped opaque representation is sufficient.
- Observe hit/miss/stale/error rates, latency, evictions, memory pressure, key cardinality, refresh behavior, and source fallback load.

## Mandatory workflow

**Complete steps 1 through 7 in order for every cache task.** Identify the task mode and scope first. Apply every relevant step to the work itself and record its outcome. For an existing cache, confirm applicable decisions against the current contract and evidence. A focused task can make a step brief, but it still needs an outcome. Mark a step `Not applicable` only when it genuinely does not apply, and give the reason. If a required input or decision is missing, mark the step `Blocked` and stop work that depends on it.

For troubleshooting, inspect cache and client versions, eviction policy, access distribution, value sizes, and fallback load as applicable. Use hit rate, evictions, payload size, and source latency to distinguish invalidation faults from capacity or expiry problems.

1. Define the workload, source SLO, target SLO, sharing scope, tolerated staleness, privacy boundary, and failure tolerance.
2. For each distinct workload, use [technology selection](references/patterns-and-placement.md#choose-the-cache-technology) to choose one primary cache technology or decide the source can serve it directly. Rule out options that cannot meet a hard requirement. Among viable choices, prefer the one that meets the target with the least operational and consistency cost. For work on an existing cache, start with the deployed technology and reconsider it only if the requirements call for it.
3. Select the [pattern](references/patterns-and-placement.md#choose-the-pattern) that meets the read, write, freshness, and failure requirements on the chosen technology. If a required pattern needs a capability the technology cannot provide, revisit the technology choice. Add another cache layer only when it solves a distinct requirement the primary cannot meet, with separate freshness, invalidation, and failure rules for each layer.
4. Specify key and value contracts, TTL/refresh, eviction assumptions, capacity, and tenant/security boundaries.
5. Design cache-miss, source failure, cache failure, stampede, hot-key, mass-expiry, and deployment behavior.
6. Define observability, operations, rollout, warmup, migration, and rollback.
7. Verify the applicable cases, such as cold or empty cache, stale entries, concurrent misses, partial failure, eviction, schema changes, and invalidation races. Run the relevant checks for an implementation. For a design, specify how each applicable case will be verified. For a review, assess the available evidence and identify gaps.

## Readiness gate

Require a named source of truth, measurable cache objective, tolerated staleness, read/write behavior, data classification, tenant scope, source capacity, and cache/source failure expectations. For SDD, require the approved cache decision plus deployed cache/client constraints. Do not declare a cache implementation ready while invalidation ownership, correctness on cache loss, or sensitive-data handling is unresolved.

Claim completion only after every workflow step has a recorded outcome. A blocked applicable step prevents a readiness claim. Report checks that have been planned but not run as pending verification.

## Choose references for the task

When the technology is undecided, start with [technology selection](references/patterns-and-placement.md#choose-the-cache-technology). Compare only candidates that could meet the requirements and open their technology references only if a capability needs confirmation. Once selected, read the technology reference or the pattern reference that resolves the current task. Use the matching row or section below. Add another reference only when it answers a separate requirement raised by the selected technology or pattern. When investigating a cache hierarchy, identify where the response was served or became stale before reading other layers.

| Cache layer | Requirement or symptom | Start here |
|---|---|---|
| In-process | Per-instance state, memory limits, expiry, concurrent loads, or invalidation across instances | [In-process caching](references/in-process.md) |
| Browser | HTTP cache directives, validators, versioned assets, personalized responses, or a service worker returning stale content | [Browser caching](references/browser.md) |
| CDN | Edge eligibility, cache key or response variants, origin load, edge TTL, purge, or shared-cache data exposure | [CDN caching](references/cdn.md) |
| Redis | Data types, command semantics, key expiry, eviction, client tracking, topology, or recovery | [Redis mechanism selector](references/redis.md). Use the relevant linked reference. For a latency or memory incident, start directly with [Redis operations](references/redis-operations.md). |
| Memcached | Memcached expiry, eviction, memory, hit rate, or connection behavior | [Memcached](references/memcached.md) |

| General requirement | Start here |
|---|---|
| Whether to cache, where to place it, or which read/write pattern fits | [Patterns and placement](references/patterns-and-placement.md) |
| Key or value format, TTL, refresh, or invalidation contract | [Keys, TTL, and consistency](references/keys-ttl-and-consistency.md) |
| Stale reads after writes, concurrent refill, or failed invalidation | [Cache consistency](references/cache-consistency.md). Add the key and TTL reference if the contract itself changes. |
| Stampede, penetration, mass expiry, hot keys, fallback, data protection, or capacity | [Resilience, security, and operations](references/resilience-security-and-operations.md) |
| Refill lock, Redis lease, fencing, or cache-backed duplicate suppression | Read the applicable section of [coordination and idempotency](references/coordination-and-idempotency.md). For a focused coordination decision, start here and establish the protected resource and failure contract. |
| Formal design, implementation, or readiness review | [Review checklist](references/review-checklist.md). Assess items relevant to the review scope. |

A JVM cache growing without bound starts with the in-process memory section. A browser reusing old JavaScript starts with browser freshness and validation. A CDN serving the wrong language starts with CDN keys and variants. If an edge purge succeeded but a browser still serves old content, move to the browser reference after confirming the edge response is current.

## SD and SDD boundary

System Design defines why caching exists, placement/topology, technology/version decision, source of truth, key namespace and schema pattern, value schema/version, TTL/jitter and refresh contract, consistency/staleness, invalidation ownership, failure/fallback, resilience, security, capacity, observability, operations, rollout, and per-feature read/write/invalidate sequences. SDD/OpenSpec implements the approved keys, values, adapters, configuration, algorithms, rollout tasks, telemetry, and tests without redefining the cache contract.

## Expected output

Include a brief numbered record of steps 1 through 7 with each outcome, evidence or next action, and reasons for any `Not applicable` or `Blocked` steps.

For a selection task, state the primary technology, the requirements that drove the choice, the selected pattern or HTTP policy, and what needs verification. If a second layer is justified, name the separate requirement it meets. For a full design, document applicable ownership, key/value/TTL or HTTP policy, invalidation, failure behavior, isolation, capacity, observability, rollout, and verification. For a focused task, report the affected decision or behavior and its evidence.
