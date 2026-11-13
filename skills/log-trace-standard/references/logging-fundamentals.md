# Logging fundamentals

Logging records application or system events for people and machines. It is more than printing: a logging system adds severity, timestamp, logger identity, structured fields, exception data, context, routing, filtering, and configuration.

Distinguish logs, metrics, traces, and audit records. Logs explain individual events; metrics measure quantity and rate; traces connect work across components; audit records provide a durable, controlled history when legal or business accountability is required. Ordinary logs should not be treated as the sole audit system.

Classify events as application, infrastructure, operational, business, or audit events. Prefer stable event names such as `payment.created`, `job.failed`, or `connection_pool.exhausted`. The goal is enough high-quality information to understand behavior, not maximum volume.

## Concrete example

For a completed payment, emit `payment.created` with `payment_id`, `amount_currency`, and `trace_id`; use a metric for the total count and a trace span for downstream timing.
