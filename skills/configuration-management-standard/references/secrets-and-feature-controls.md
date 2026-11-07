# Secrets and Feature Controls

## Secret Boundary

A secret grants access or proves identity, such as a password, private key, token, credential, or signing material. A sensitive business value is not automatically a secret, but still needs classification and protection.

- Use a designated secret-management mechanism rather than ordinary configuration storage.
- Grant least-privilege access to the workload identity that needs the secret.
- Define creation, distribution, activation, rotation, revocation, expiry, recovery, destruction, and audit.
- Prefer short-lived or dynamically issued credentials where the platform supports them.
- Redact secrets from logs, traces, metrics labels, errors, health endpoints, crash dumps, commands, CI output, and generated examples.
- Define dual-read/dual-write or overlapping validity where rotation cannot be atomic.
- Test provider outage, revoked value, expired value, partial rotation, and rollback behavior.

Environment variables can be convenient but may leak through process inspection, diagnostics, or dumps. Select the delivery mechanism from the threat model and runtime, not convenience alone.

## Feature Controls

Feature flags alter behavior at runtime but require a release lifecycle beyond ordinary configuration:

- owner, purpose, type, safe default, targeting scope, and expiry;
- deterministic subject key for percentage rollout;
- privacy-minimized evaluation context;
- provider-unavailable behavior and local caching;
- audit, metrics, exposure tracking, and authorization;
- staged rollout, kill switch, rollback, and permanent-code cleanup.

Do not use a feature flag as authorization. A flag may hide or release a capability, but server-side authorization must still enforce access. Route rollout and cleanup decisions through `deployment-release-standard`.

## Primary References

- [OWASP Secrets Management Cheat Sheet](https://cheatsheetseries.owasp.org/cheatsheets/Secrets_Management_Cheat_Sheet.html)
- [Kubernetes Secrets](https://kubernetes.io/docs/concepts/configuration/secret/)
- [OpenFeature Introduction](https://openfeature.dev/docs/reference/intro/)
- [OpenFeature Evaluation Context](https://openfeature.dev/docs/reference/concepts/evaluation-context/)
