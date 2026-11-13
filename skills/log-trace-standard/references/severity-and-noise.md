# Severity and Noise Control

Use project-defined levels first. Generic intent:

| Level | Typical use |
|---|---|
| Trace/Debug | Temporary or selectively enabled implementation detail needed for diagnosis |
| Info | Meaningful lifecycle, business, integration, or state-transition milestone under normal operation |
| Warn | Unexpected or degraded condition that was handled but may require attention |
| Error | Operation failed, data may need reconciliation, or human/automated intervention may be required |
| Fatal/Critical | Process/service cannot safely continue or a critical control failed |

Do not classify normal validation, expected “not found,” client cancellation, or business rejection as server errors unless the operational contract says otherwise.

## Duplicate control

- Choose one owner to record the final outcome.
- Do not log and rethrow at every layer.
- Retry attempts may be debug/warn while the final exhausted outcome is error; include attempt count and policy without duplicating full stack traces.
- Prefer one summary event for a batch plus bounded failure samples rather than one event per record.
- Use rate limiting, aggregation, or sampling for repetitive diagnostics while preserving required security/audit events.

## Performance and cost

- Avoid expensive attribute computation when the level/event is disabled.
- Avoid synchronous remote logging on latency-sensitive paths unless explicitly required.
- Bound queues and define drop/backpressure policy.
- Estimate event rate and storage/retention cost before enabling verbose production logs.
- Alert on meaningful event patterns, not raw volume alone.
