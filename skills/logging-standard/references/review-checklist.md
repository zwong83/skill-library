# Logging Review Checklist

Report each item as `Pass`, `Gap`, `Needs decision`, or `Not applicable`.

- Every event answers a concrete diagnostic, security, audit, or operational question.
- The owning boundary is correct and the same outcome is not logged repeatedly.
- Event names/templates and field types are stable; values are structured and bounded.
- Severity matches the outcome and operational contract.
- Errors preserve safe cause/classification without dumping raw payloads.
- Active trace/request/job/message correlation is attached through supported context.
- Secrets and sensitive data are excluded, masked, or pseudonymized according to approved policy.
- Untrusted fields are sanitized and bounded against log injection.
- Volume, hot paths, retries, batching, sampling/rate limiting, storage, and retention are considered.
- Logging/export failure does not unexpectedly fail or stall the business operation.
- Required security/audit events cannot be silently disabled.
- Tests verify fields, redaction, correlation, duplicate control, injection safety, and failure behavior.
