# Logging security review

- [ ] Secrets and credentials are excluded by allowlist/redaction
- [ ] Personal, financial, health, and payload data have an explicit decision
- [ ] Exception and framework-generated logs are covered
- [ ] Logs are access-controlled and encrypted in transit/at rest as required
- [ ] Retention and deletion match policy
- [ ] Test cases include realistic secret patterns and malformed input

## Concrete example

Send a test request containing `Authorization: Bearer test-token` and `password=example`; verify the emitted event contains `[REDACTED]` and no raw credential.
