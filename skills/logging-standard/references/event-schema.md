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

## Correlation

When an active trace exists, use instrumentation/bridges to attach trace and span identifiers. If a span identifier is recorded, its trace identifier should also be present. Correlation fields are diagnostic metadata and must not be trusted for access control.
