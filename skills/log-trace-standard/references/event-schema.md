# Structured Event Schema

Use the project's established schema or OpenTelemetry-compatible log model when available. Do not invent parallel field names for existing semantic conventions.

## Core fields

Include fields only when meaningful:

| Field | Purpose |
|---|---|
| event timestamp | When the event occurred |
| observed timestamp | When a collector observed an external event, when applicable |
| event name/type | Stable, low-cardinality event class |
| severity | Source text/normalized level according to the platform |
| body/message | Human-readable summary without sensitive payloads |
| service/resource | Originating service, instance category, environment, or deployment resource |
| instrumentation scope | Library/module that emitted the event |
| attributes | Structured bounded context |
| trace/span context | Correlation to active distributed work |
| outcome/error classification | Success, failure, rejection, timeout, cancellation, and stable error code/type |

OpenTelemetry's current log data model includes timestamp, observed timestamp, trace and span identifiers, severity, body, resource, instrumentation scope, attributes, and event name. See [OpenTelemetry Logs Data Model](https://opentelemetry.io/docs/specs/otel/logs/data-model/).

## Attribute design

- Use stable keys and types across services.
- Prefer approved semantic conventions for common protocols and resources.
- Put identifiers and values in attributes, not event names or templates.
- Bound string length and collection size.
- Record business identifiers only when approved and necessary; prefer scoped, pseudonymous, or hashed values when policy allows.
- Distinguish client rejection, dependency failure, timeout, cancellation, conflict, and internal defect rather than logging every failure as “error.”
- Do not record both a raw object and duplicated extracted fields.

## Feature classification

Use a structured `feature` attribute when operators need to filter events by user-facing capability or bounded business area. Keep its vocabulary stable and low-cardinality, such as `checkout`, `catalog`, or `order-management`.

- Use `feature` for the business capability and `component` for the technical emitter, such as `payment-service`.
- Put the concrete action in `operation` and use a stable event name such as `checkout.payment_authorization_failed`.
- Never put request, user, tenant, order, or other per-instance identifiers in `feature`.
- Shared infrastructure may use an agreed value such as `platform`, with `component` identifying the subsystem.
- A text renderer may display the structured value as `[checkout]` for fast scanning. Do not make parsers depend on extracting it from the message.

Example rendered event:

```text
2026-11-07T14:32:18.451+08:00 ERROR [checkout] Payment authorization failed | event=checkout.payment_authorization_failed component=payment-service operation=authorize_payment outcome=failure order_id=ORD-20261107-001 payment_provider=stripe error_type=provider_timeout retry_attempt=3 trace_id=4bf92f3577b34da6a3ce929d0e0e4736 span_id=00f067aa0ba902b7
```

The corresponding structured record should retain separately queryable fields:

```json
{
  "timestamp": "2026-11-07T14:32:18.451+08:00",
  "severity": "ERROR",
  "message": "Payment authorization failed",
  "event": "checkout.payment_authorization_failed",
  "feature": "checkout",
  "component": "payment-service",
  "operation": "authorize_payment",
  "outcome": "failure",
  "order_id": "ORD-20261107-001",
  "payment_provider": "stripe",
  "error_type": "provider_timeout",
  "retry_attempt": 3,
  "trace_id": "4bf92f3577b34da6a3ce929d0e0e4736",
  "span_id": "00f067aa0ba902b7"
}
```

Treat identifiers in examples as illustrative. Production inclusion still depends on data classification, minimization, and retention requirements.

## Correlation

When an active trace exists, use instrumentation/bridges to attach trace and span identifiers. If a span identifier is recorded, its trace identifier should also be present. Correlation fields are diagnostic metadata and must not be trusted for access control.
