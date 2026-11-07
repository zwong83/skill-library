# Span Design

## Boundaries

Instrument operations whose latency, failure, or causality matters: inbound server work, outbound client calls, queue production/consumption, scheduled jobs, data-store calls, and substantial internal stages. Avoid spans for getters, pure calculations, trivial wrappers, or every function.

## Naming and kind

- Use a stable operation class such as route/RPC/message operation, not an instance identifier.
- Follow approved semantic conventions for server, client, producer, consumer, and internal operations.
- Keep names human-readable and low-cardinality.

## Lifecycle

- Start at the logical beginning and end at actual completion, including async completion.
- End exactly once on success, failure, cancellation, and timeout.
- Do not mutate a span after it ends.
- Use explicit start timestamps only when instrumenting work that already began.

## Attributes

- Prefer semantic-convention attributes.
- Add sampling-relevant attributes at creation when available.
- Keep keys/types stable and values bounded.
- Avoid payloads, secrets, variable span-name content, stack dumps, and duplicate resource metadata.

## Status and errors

OpenTelemetry defines `Unset`, `Ok`, and `Error`. Normal success generally remains unset; instrumentation should not set `Ok` automatically unless its convention requires it. Set `Error` when the operation failed according to its contract, not merely because an expected rejection or handled condition occurred.

For new events and exceptions, prefer named structured logs correlated with the current span as OpenTelemetry migrates away from new Span Event API usage. Existing instrumentation may retain span-event compatibility. See [OpenTelemetry Tracing API](https://opentelemetry.io/docs/specs/otel/trace/api/) and [Span Event API deprecation](https://opentelemetry.io/blog/2026/deprecating-span-events/).
