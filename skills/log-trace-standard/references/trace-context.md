# Trace context and correlation

`trace_id` identifies a distributed trace; `span_id` identifies one operation within it; `request_id` identifies an inbound request; `correlation_id` is an application-defined grouping key such as a workflow, batch, or transaction. Define and preserve their semantics rather than treating them as synonyms.

Extract or create context at the boundary, attach it to the current execution context, propagate it downstream, and detach it after processing. Prefer W3C Trace Context and OpenTelemetry where supported. Obtain IDs from the framework context so callers do not manually repeat them on every log statement. Verify propagation through thread pools, futures, coroutines, schedulers, and workers, and prevent context leakage between requests.

## Concrete example

An inbound request creates `trace_id=T1`, the payment span uses `span_id=S2`, and an outbound queue message carries `traceparent` for the consumer. The consumer restores `T1` before emitting `payment.notification.started`.
