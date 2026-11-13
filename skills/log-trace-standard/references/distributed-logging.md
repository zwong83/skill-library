# Distributed logging

A distributed event path may cross a gateway, services, databases, queues, and workers. Keep service identity, operation name, trace context, outcome, and duration available at boundaries. Log retries and fallbacks at a useful level with attempt and limit fields; avoid one log per internal hop when a metric or trace span is sufficient.

For asynchronous work, preserve parent context where the tracing model supports it, or record an explicit workflow/message identity. Do not assume a new thread or queue consumer inherits logging context automatically.

## Concrete example

For `checkout.completed`, the gateway, order service, payment service, and notification worker all retain `trace_id=T1`; the worker also records `message_id=M9` so a retry can be investigated independently.
