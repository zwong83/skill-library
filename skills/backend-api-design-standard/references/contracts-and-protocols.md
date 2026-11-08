# Contracts and Protocols

## Protocol Selection

| Style | Prefer when | Watch for |
|---|---|---|
| HTTP resource API | Broad interoperability, browser/public clients, cacheable resources, request-response workflows | Incorrect method semantics, chatty calls, weak schema discipline |
| gRPC | Strongly typed internal calls, generated clients, low-latency unary or streaming interactions | Deadline propagation, protobuf evolution, browser reach, debugging tooling |
| GraphQL | Consumers need flexible graph-shaped reads and an owned schema | Query cost, authorization depth, N+1 access, nullability, schema governance |
| Messaging or streaming | Temporal decoupling, asynchronous completion, fan-out, replay, event-driven workflows | Delivery semantics, ordering, idempotency, schema evolution; use `backend-messaging-standard` |

Document why the selected style fits the interaction. Multiple styles may coexist, but each adds governance and operational cost.

## Operation Contract

For each operation define:

- stable name and business purpose;
- caller or consumer classes;
- authorization subject, action, resource, tenant, and policy outcome;
- input fields, constraints, defaults, omission, nullability, and maximum sizes;
- output fields and visibility rules;
- side effects, transaction boundary, consistency, and completion point;
- duplicate and concurrent-request behavior;
- timeout or deadline, cancellation, retry safety, and rate limits;
- error identifiers and public mapping;
- emitted events or asynchronous follow-up;
- metrics, logs, traces, audit events, and tests.

## HTTP Rules

- Use methods according to their defined semantics. Do not hide mutations behind safe methods.
- Select status codes that describe the protocol outcome, then expose a stable application error identifier and safe details.
- Use RFC 9457 problem details when it improves consistency, with controlled extension members and a stable problem type.
- Define request and response media types, character encoding, content negotiation, and maximum body size.
- Use conditional requests and caching headers only when validators, freshness, and invalidation semantics are correct.
- For create or command operations vulnerable to duplicate delivery, define idempotency-key scope, storage duration, request fingerprint behavior, replayed response behavior, and conflict behavior.
- Define URI, query, and header naming consistently. Avoid leaking table structure or framework class names.
- Make bulk and partial operations explicit: atomic, best effort, or per-item results.

## gRPC Rules

- Select unary, server-streaming, client-streaming, or bidirectional streaming from the interaction, not novelty.
- Set and propagate deadlines. Define server cancellation behavior and cleanup.
- Map failures to appropriate gRPC status codes while carrying stable, safe application details.
- Preserve protobuf field numbers and wire compatibility. Never reuse removed field numbers; reserve removed names and numbers.
- Prefer additive fields and services. Review presence, defaults, `oneof`, enums, unknown fields, and numeric widening carefully.
- Define retry policy only for methods with safe semantics and bounded retry budgets.
- Plan reflection, health checking, authentication metadata, interceptors, and observability deliberately.

## GraphQL Rules

- Design the schema around domain capabilities, not persistence entities.
- Make nullability intentional. Distinguish absent, null, empty, and error outcomes.
- Enforce field-level and object-level authorization without relying only on the top-level resolver.
- Bound depth, complexity, aliases, list sizes, and batching. Prevent N+1 access with measured loaders or query planning.
- Define stable mutation payloads, typed errors, idempotency where needed, and pagination semantics.
- Deprecate schema fields with migration guidance before removal.

## Shared Security and Data Boundaries

- Authentication establishes identity; authorization decides whether that identity may perform the action on the resource.
- Never trust caller-supplied tenant, owner, role, price, or security-sensitive state without server-side verification.
- Use explicit allowlists and structural validation. Normalize only when the contract defines normalization.
- Redact secrets and sensitive values from errors, logs, traces, analytics, and example payloads.
- Keep transport, domain, and persistence models separate when coupling would expose internal fields or constrain evolution.
