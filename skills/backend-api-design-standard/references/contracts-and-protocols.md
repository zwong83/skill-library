# Contracts and Protocols

## API Design Selection

1. Identify the consumers and what each interaction must do. Decide whether callers need an immediate result, an asynchronous completion status, a live stream, or independently consumed events. Note client and gateway support, trust boundaries, compatibility commitments, latency and traffic targets, and ownership.
2. Compare plausible designs. Eliminate candidates that fail hard requirements. For the viable options, compare client and tooling support, contract evolution, operational cost, and the complexity of serving the required behavior.
3. Select the simplest design that satisfies the requirements and record what decided the choice. Use multiple styles when different interactions justify them, with explicit ownership and a completion contract at each boundary. For example, an HTTP API can accept a long-running job and expose its status while a broker distributes completion events to independent consumers.
4. **Follow the rules for every selected candidate.** Read the rules listed in its row and apply them to the contract, implementation, or review for that interaction. When a design combines candidates, apply each rule set at the boundary it governs. Use the applicable rules as verification criteria in workflow step 8.

| Candidate | Evaluate when | Watch for | Required rules when selected |
|---|---|---|---|
| HTTP resource or operation API | Browser or public clients, broad interoperability, cacheable reads, or commands with clear request and response semantics | Method semantics, chatty calls, schema discipline, and a status contract for long-running work | [HTTP rules](#http-rules) |
| gRPC | Supported clients benefit from typed RPCs, generated bindings, or client or bidirectional streaming | Deadline propagation, protobuf evolution, browser reach, and tooling | [gRPC rules](#grpc-rules). For streaming methods, also apply [direct client streaming rules](#direct-client-streaming-rules). |
| GraphQL | Consumers need flexible selections across related data and a team can own the shared schema | Query cost, authorization depth, N+1 access, nullability, and schema governance | [GraphQL rules](#graphql-rules) and the applicable transport rules. |
| Direct client streaming, such as SSE, WebSocket, or gRPC streaming | A connected consumer needs ongoing updates or a bidirectional session | Client and proxy support, backpressure, cancellation, reconnect and resume behavior | [Direct client streaming rules](#direct-client-streaming-rules) and the rules for the selected protocol. |
| Brokered messages or event streams | Producers and consumers need temporal decoupling, durable delivery, independent fan-out, or replay | Delivery semantics, ordering, idempotency, and schema evolution | Invoke `message-standard` and follow its applicable rules. |

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

## Direct Client Streaming Rules

- Define the message schema, stream direction, ordering, and how the stream reports errors and completion.
- Define authentication and authorization at connection setup and for subscriptions or messages as applicable. Specify what happens when access expires or is revoked.
- Bound message size, concurrent streams, and buffering. Define slow-consumer behavior, idle limits, cancellation, and resource cleanup.
- Specify reconnect behavior, whether resume is supported, and how clients handle missed or duplicate messages.

## Shared Security and Data Boundaries

- Authentication establishes identity; authorization decides whether that identity may perform the action on the resource.
- Never trust caller-supplied tenant, owner, role, price, or security-sensitive state without server-side verification.
- Use explicit allowlists and structural validation. Normalize only when the contract defines normalization.
- Redact secrets and sensitive values from errors, logs, traces, analytics, and example payloads.
- Keep transport, domain, and persistence models separate when coupling would expose internal fields or constrain evolution.
