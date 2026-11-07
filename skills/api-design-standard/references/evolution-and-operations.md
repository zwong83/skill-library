# Evolution and Operations

## Compatibility and Versioning

Classify each change as compatible, conditionally compatible, or breaking for every supported consumer and serializer. An additive field is not automatically safe when consumers reject unknown fields, generated enums are exhaustive, response signatures are verified, or payload limits are tight.

Define:

- compatibility window and supported versions;
- whether versioning is by path, header, media type, service/package, or schema evolution;
- consumer discovery and migration ownership;
- deprecation notice, telemetry, deadline, and removal criteria;
- rollback and mixed-version behavior during deployment.

Prefer tolerant readers, explicit defaults, additive evolution, and capability negotiation where appropriate. Do not maintain indefinite versions without an ownership and retirement plan.

## Pagination, Filtering, and Queries

- Choose offset pagination only when data volume, mutation rate, and consistency permit it.
- For cursor pagination, define cursor opacity, ordering keys, tie-breakers, direction, expiry, and behavior when records change.
- Require deterministic ordering. Never expose an unbounded collection.
- Define filter operators, sort allowlists, search semantics, maximum page size, maximum result window, and invalid-query behavior.
- Protect expensive queries with complexity, cost, timeout, and rate controls.

## Deadlines, Limits, and Traffic

Define maximum request and response sizes, item counts, concurrency, requests per identity or tenant, burst capacity, deadline, and server processing budget. Coordinate retries with `resilience-standard`; a client retry must not multiply overload or duplicate unsafe effects.

Rate-limit responses should identify the policy outcome without exposing sensitive internals. Decide whether limits are global, tenant, user, token, client, operation, or resource scoped, and how distributed enforcement remains sufficiently consistent.

## Observability

For each important operation define:

- request, success, rejected, failed, timeout, and cancelled metrics;
- latency distributions and meaningful dimensions with bounded cardinality;
- structured event names, feature tags, correlation identifiers, and redaction;
- server and client span names, propagation, and asynchronous links;
- audit events for security-relevant actions;
- deprecation and version-usage telemetry.

Avoid logging complete payloads by default.

## Review Checklist

- Does the contract express business semantics rather than implementation accidents?
- Can a caller distinguish validation, authentication, authorization, conflict, missing resource, throttling, dependency failure, and internal failure safely?
- Are duplicate, concurrent, cancelled, and timed-out requests defined?
- Are all collections, payloads, and query costs bounded?
- Can old and new consumers coexist during rollout and rollback?
- Are security decisions enforced server-side at the correct resource boundary?
- Are deprecation and consumer migration measurable?
- Do contract, compatibility, negative, authorization, and resilience tests cover the critical behavior?

## Primary References

- [RFC 9110: HTTP Semantics](https://www.rfc-editor.org/rfc/rfc9110.html)
- [RFC 9457: Problem Details for HTTP APIs](https://www.rfc-editor.org/rfc/rfc9457.html)
- [gRPC Guides](https://grpc.io/docs/guides/)
- [gRPC Status Codes](https://grpc.io/docs/guides/status-codes/)
- [gRPC Deadlines](https://grpc.io/docs/guides/deadlines/)
- [gRPC Retry](https://grpc.io/docs/guides/retry/)
