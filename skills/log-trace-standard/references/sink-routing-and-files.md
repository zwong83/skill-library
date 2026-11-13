# Sink Routing and File Policy

Design logical sinks first. A sink may be a local file, `stdout`/`stderr`, a collector stream, an audit store, or a security platform. Do not require local files where the runtime expects platform-managed collection.

## Baseline routing

For a file-based application, use this default unless project or platform conventions require different names:

| Destination | Default contents | Decision |
|---|---|---|
| `application.log` | The complete operational timeline at the configured production threshold, normally `INFO` and above | Required default sink |
| `error.log` | A routed copy of `ERROR` and `FATAL/CRITICAL` events | Required error-focused sink |

The duplicate error record is intentional: `application.log` preserves chronology while `error.log` provides a focused failure view. Preserve the same event identity, timestamp, trace context, and structured fields in both; do not emit the event twice from application code. If duplicate storage is unacceptable, define exclusive routing explicitly and document that the default file no longer contains a complete timeline.

An error file is not an alerting system. Generate alerts from ingested structured events, rates, and service-level signals.

For container, serverless, or centrally collected deployments, send structured operational events to the platform-supported stream, commonly `stdout`, and errors to the supported severity stream, commonly `stderr`, only when that split matches the collector contract. Implement `application` and `error` as downstream logical streams or indexes instead of writing container-local files.

## Additional destinations

Create another sink only when it has a distinct operational contract:

| Candidate | Separate destination when | Default decision |
|---|---|---|
| Audit | Integrity, restricted access, legal retention, deletion, or fail-closed behavior differs from operational logging | Separate canonical audit sink; avoid copying sensitive audit payloads into `application.log` |
| Security | Events require restricted access, security monitoring, tamper controls, or direct SIEM routing that differs from normal operations | Route to the approved security sink; a separate local `security.log` is optional, not the control itself |
| HTTP access | The edge/proxy does not already provide the required record, or access events have distinct volume and retention | Separate only to avoid duplicating proxy/ingress access logs |
| Debug/trace | A bounded diagnostic session requires verbose data with short retention | Disabled by default in production; enable temporarily and remove or expire automatically |
| Performance/slow operation | High-volume timing records need different sampling/retention and cannot be represented adequately by metrics and traces | Usually use metrics/traces; add a slow-event sink only for a demonstrated query or workflow |
| Integration/message/job | Volume, ownership, access, or retention materially differs from application events | Keep in the default sink unless an isolation criterion is met |
| Feature-specific | Never merely because events belong to `checkout`, `catalog`, or another feature | Keep together and query the structured `feature` field |

Do not use a separate file merely to compensate for missing structured fields or search capability.

## Routing rules

- Route with structured severity and event-category fields, not message-prefix parsing.
- Configure routing in the logging pipeline; application code emits one event to its logger.
- Define the canonical copy for audit/security events and document any redacted operational summary.
- Preserve ordering metadata, event identity, trace context, and schema across destinations.
- Prevent recursive logging when a sink, exporter, or rotation operation fails.
- Test that ordinary events do not leak into restricted sinks and restricted payloads do not leak into general sinks.

## File lifecycle controls

Every local file destination must define:

- size- or time-based rotation and safe rollover behavior;
- retention duration, maximum file count or disk quota, and deletion responsibility;
- compression rules and whether active files may be compressed;
- owner/group and least-privilege read/write permissions;
- behavior under disk-full, permission, lock, and rotation failures;
- bounded asynchronous queue, drop/backpressure behavior, and exporter health signals;
- environment separation and protection against serving log files through public application paths.

Keep file paths and lifecycle values configurable per environment. Do not hardcode production paths, retention, or credentials in application code.
