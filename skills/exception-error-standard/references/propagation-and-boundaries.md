# Propagation and Boundary Rules

## Throw, return, and catch

- Use the target language's idiomatic failure mechanism while preserving a typed, testable contract.
- Throw/return at detection: invalid state, failed invariant, unavailable dependency, timeout, or violated precondition.
- Catch locally only when the code can take responsibility for the next action.
- Translate at a semantic boundary: vendor error to infrastructure outcome, infrastructure outcome to application error, application outcome to API/message/job result.
- Add context as structured fields or a wrapped cause; do not replace the original failure or concatenate sensitive payloads.
- Use unconditional cleanup constructs for resources. Do not hide a primary failure with a cleanup failure; preserve both according to language support.

## Layer ownership

| Boundary | Responsibility |
|---|---|
| Interface/API | Validate transport shape, map application outcomes to protocol responses, apply safe public messages |
| Application/use case | Coordinate business outcome, transaction, idempotency, and recoverable dependency behavior |
| Domain/policy | Raise/return business invariant and state-transition outcomes without framework/vendor types |
| Infrastructure/adapter | Translate database, cache, broker, network, and SDK failures into port-level outcomes |
| Process boundary | Handle uncaught terminal failures, lifecycle, crash/restart policy, and final telemetry |

Message consumers map outcomes to ack, retry/nack, defer, quarantine, or dead-letter semantics. Scheduled jobs map outcomes to success, retryable failure, terminal failure, partial completion, or reconciliation work. Never acknowledge work before required durable effects are complete unless the design explicitly accepts loss.

## Logging

Invoke `log-trace-standard` for event design and cross-boundary causality. Record the final owned outcome once; intermediate layers may add trace context only when they contribute distinct diagnostic value. Preserve a stable error code and trace correlation without exposing sensitive details.
