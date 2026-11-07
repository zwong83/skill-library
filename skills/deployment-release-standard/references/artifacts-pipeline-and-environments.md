# Artifacts, Pipeline, and Environments

## Artifact Contract

Record artifact type, immutable identifier or digest, source revision, build recipe/toolchain, dependency lock state, generated assets, tests, security evidence, provenance, storage, retention, and promotion history. Preserve the exact verified artifact across environments; inject environment configuration separately.

Where required by risk or policy, produce and verify signatures, attestations, and a software bill of materials. Do not claim supply-chain compliance without the required evidence.

## Pipeline Controls

- Pin or govern tools, dependencies, actions, and base images.
- Isolate untrusted pull-request or contribution execution from release credentials.
- Use short-lived workload identity and least privilege where supported.
- Keep secrets out of repository, artifact, logs, command arguments, and ordinary cache.
- Protect approval and production stages with explicit identities and audit.
- Make retries idempotent and prevent a partially failed stage from being reported as successful.
- Retain evidence linking source, artifact, verification, approval, deployment, and release.

## Environment and Promotion

Define each environment's purpose, fidelity, data policy, access, configuration authority, dependencies, test scope, promotion criteria, and drift controls. Lower environments should provide enough fidelity for the decisions made there without copying sensitive production data unnecessarily.

Promotion gates may include static checks, unit/integration/contract tests, migration rehearsal, security checks, performance evidence, artifact verification, configuration validation, and approval. Gate selection should be risk-based and fast enough to remain used.

## Compatibility Matrix

Assess coexistence among:

- old/new service instances;
- old/new API and event consumers;
- old/new schema and data shapes;
- old/new configuration and feature-control versions;
- clients that update slowly or cannot be forced;
- dependencies and infrastructure versions.

Use expand-migrate-contract for incompatible schema evolution. A deployment is not rollback-safe merely because the previous binary still exists.

## Primary References

- [Google SRE: Release Engineering](https://sre.google/sre-book/release-engineering/)
- [OWASP CI/CD Security Cheat Sheet](https://cheatsheetseries.owasp.org/cheatsheets/CI_CD_Security_Cheat_Sheet.html)
