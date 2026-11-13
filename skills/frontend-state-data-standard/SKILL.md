---
name: frontend-state-data-standard
description: Design or review frontend server, client, URL, form, session, derived, and persisted state ownership plus API data flow, caching, optimistic updates, cancellation, retries, offline behavior, and consistency; not for backend source-of-truth design.
---

# Frontend State and Data Standard

Use this skill after backend data ownership and the shared interface contract are known or explicitly proposed.

## Core rules

1. Classify each value as server, client UI, URL/navigation, form draft, session, derived, or persisted browser state and name one owner/source of truth.
2. Do not copy server state into unrelated client stores without a synchronization requirement. Derive values instead of storing duplicate truth.
3. Define query/mutation contracts, cache identity, freshness/staleness, invalidation, pagination, cancellation, deduplication, refetch, and dependency-error behavior.
4. Use optimistic updates only with an explicit eligibility rule, temporary identity/version behavior, rollback/reconciliation, duplicate handling, and user feedback.
5. Coordinate retry, timeout, idempotency, concurrency, and conflict behavior with the approved API contract; the client must not create unsafe retries.
6. Treat URL state as a shareable/navigation contract when appropriate. Define parsing, defaults, compatibility, invalid values, history, and restoration.
7. Define form state, validation sources/timing, server-field/global errors, dirty/reset/submission state, and navigation interruption.
8. Minimize browser persistence. Define classification, scope, expiry, version/migration, logout/tenant change, corruption, quota, and privacy/security behavior.
9. Make offline/service-worker behavior conditional and explicit; stale or queued work must not violate pricing, inventory, authorization, or other server authority.

## Workflow

1. Build the state ownership and data-flow inventory from journeys, routes, components, and contracts.
2. Define query/mutation, cache, optimistic/concurrency, URL/form/session, persistence, and offline decisions.
3. Map errors, loading, cancellation, recovery, telemetry, and verification for each material flow.
4. Return contract feedback instead of inventing missing backend semantics.

## Reference routing

- Read [state-ownership-and-data-flow.md](references/state-ownership-and-data-flow.md) for the design matrix.
- Invoke `backend-api-design-standard` and `contract-testing-standard` for shared request/response/error compatibility.
- Invoke `cache-standard` only for principles shared with browser/client cache; this skill owns frontend state placement and UX behavior.
- Invoke `frontend-security-standard` for storage, identity, and sensitive-data boundaries.

## Output

Return state ownership matrix, data-flow/query/mutation catalogue, cache/freshness/invalidation rules, optimistic/rollback/concurrency behavior, URL/form/session contracts, persistence/offline decisions, error/loading/recovery behavior, contract feedback, verification intent, and unresolved decisions.
