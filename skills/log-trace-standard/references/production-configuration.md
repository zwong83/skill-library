# Production configuration

Keep levels, sinks, endpoints, sampling, redaction, rotation, and retention configurable by environment. Treat configuration as code, validate it at startup, and fail safely when a required secure sink or redaction rule is unavailable. Prefer stable schema/version fields and document collector expectations. Avoid enabling DEBUG globally as an incident response shortcut without a volume and data-safety plan.

## Concrete example

Development may use `DEBUG` and a readable console formatter; production may use `INFO`, JSON to stdout, centralized redaction, and a 1% sample for successful high-volume requests.
