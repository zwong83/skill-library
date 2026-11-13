# Security and sensitive data

Never log passwords, access/refresh tokens, API keys, private keys, authentication credentials, CVV/security codes, or full payment-card numbers. Review personal, financial, health, session, and customer payload data explicitly. Prefer allowlists of fields over denylist-only redaction.

Redaction must happen before serialization and at every sink or forwarding boundary. Protect log access, transport, retention, backups, and exports. Test redaction with realistic secret shapes and verify exception messages and framework-generated request logs are covered.

## Concrete example

```text
Before: authorization=Bearer eyJ... password=hunter2
After:  authorization=[REDACTED] password=[REDACTED]
```
