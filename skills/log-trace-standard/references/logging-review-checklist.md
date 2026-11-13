# Logging Review Checklist

Report each item as `Pass`, `Gap`, `Needs decision`, or `Not applicable`.

- Every event answers a concrete diagnostic, security, audit, or operational question.
- The owning boundary is correct and the same outcome is not logged repeatedly.
- Event names/templates and field types are stable; values are structured and bounded.
- Business events use a stable, low-cardinality `feature` attribute when feature-level filtering is useful; any `[feature]` display prefix is derived from that field rather than parsed from the message.
- Severity matches the outcome and operational contract.
- A default operational sink and error-focused sink exist for file-based deployments, or equivalent platform streams are defined; any intentional duplication is performed by routing rather than duplicate application emissions.
- Additional audit, security, access, debug, performance, integration, or feature sinks are justified by distinct access, integrity, retention, volume, or ownership requirements.
- Errors preserve safe cause/classification without dumping raw payloads.
- Active trace/request/job/message correlation is attached through supported context.
- Secrets and sensitive data are excluded, masked, or pseudonymized according to approved policy.
- Untrusted fields are sanitized and bounded against log injection.
- Volume, hot paths, retries, batching, sampling/rate limiting, storage, and retention are considered.
- Local files define rotation, retention/quota, compression, permissions, disk-full behavior, and bounded queue/backpressure controls.
- Logging/export failure does not unexpectedly fail or stall the business operation.
- Required security/audit events cannot be silently disabled.
- Tests verify fields, redaction, correlation, duplicate control, injection safety, and failure behavior.
