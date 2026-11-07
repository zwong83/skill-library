# Context and Correlation

## Propagation

- Use project-approved standard propagators and carriers for HTTP/RPC headers, message metadata, jobs, and async execution.
- Extract at trusted ingress boundaries, make the context active only for the operation scope, inject at egress, and restore/clear context correctly.
- Do not store active context in global mutable state.
- Prevent context leakage across requests, threads, tasks, coroutines, or reused workers.
- Treat remote context and baggage as untrusted metadata; never use them as authentication, authorization, tenancy, or billing truth.

## Parent versus link

Use parent/child for a direct causal operation with one logical parent. Use links when work combines multiple causes, processes a batch, continues from stored/scheduled context, or cannot be represented accurately as a tree. Document message redelivery and retry topology.

For message batches, attach links to the message creation contexts when the consumer span is created. Per-message attributes belong on the corresponding links when supported; batch-wide attributes belong on the span. Links added after creation may not influence head-sampling decisions.

## Messaging lifecycle

Model the broker/client operations supported by the selected semantic convention, typically message creation/send, receive, process, and settle. Define:

- whether each delivery/processing attempt creates a distinct span and how retry/redelivery attempt is identified;
- success, retryable failure, rejection, timeout, cancellation, and final exhaustion;
- acknowledgement, negative acknowledgement, release/requeue, settlement, offset commit, and dead-letter behavior;
- partial success for batches, including message-level outcomes in safe bounded logs or link attributes;
- propagation and correlation when a message is retried, copied, routed, or dead-lettered.

Record the OpenTelemetry semantic-convention version, instrumentation library/version, enabled stability/migration options, and whether old/new fields are emitted together. Test upgrades against dashboards, queries, sampling, and alert rules rather than assuming conventions remain unchanged. The current messaging conventions are still marked development and define compatibility migration behavior; see [OpenTelemetry messaging span conventions](https://opentelemetry.io/docs/specs/semconv/messaging/messaging-spans/).

## Baggage

Propagate only bounded, approved cross-cutting metadata. Baggage may cross service boundaries and can create privacy, security, and cost risk. Never put secrets or unrestricted user-controlled data in baggage.

## Log correlation

Attach active trace and span identifiers through the logging/tracing integration. Do not manually parse or regenerate identifiers when the instrumentation can supply them. A log may exist without a trace; diagnostic code must not fail when no span is active or when a trace is unsampled.

OpenTelemetry `SpanContext` follows W3C Trace Context. Use ecosystem-supported propagation rather than custom formats unless a compatibility requirement is approved.
