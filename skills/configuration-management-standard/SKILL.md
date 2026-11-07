---
name: configuration-management-standard
description: Design, implement, or review application and service configuration, including configuration schemas, defaults, precedence, validation, environment separation, dynamic refresh, feature controls, secrets boundaries, ownership, audit, rollout, rollback, and failure behavior.
---

# Configuration Management Standard

Use this skill when runtime behavior depends on environment-specific values, operational settings, feature controls, credentials, certificates, endpoints, quotas, or configuration changes.

## Core Rules

1. Separate code, non-sensitive configuration, secrets, and release controls. Do not use one mechanism as an ungoverned substitute for another.
2. Define every configuration key with type, purpose, owner, default, required status, valid range, sensitivity, scope, source, reload behavior, and failure policy.
3. Use one deterministic precedence order. Make the effective value and its non-sensitive provenance diagnosable.
4. Validate configuration structurally and semantically before serving traffic. Fail startup for unsafe required values; do not silently invent production defaults.
5. Separate environments and tenants without duplicating application code or embedding environment values in build artifacts.
6. Keep secrets out of source control, images, ordinary configuration stores, logs, traces, errors, and diagnostics. Use a governed secrets lifecycle.
7. Treat dynamic configuration as distributed state: define propagation, consistency, stale behavior, concurrency, rollback, and partial-update handling.
8. Version, review, audit, test, and roll out material configuration changes like code changes.
9. Minimize configuration surface. Remove obsolete keys and temporary flags with migration evidence.
10. Define secure behavior when configuration or its provider is missing, malformed, unavailable, stale, or unauthorized.

## Workflow

1. Inventory configuration consumers, keys, owners, environments, tenants, sensitive values, and current sources.
2. Classify each value as code constant, deploy-time config, runtime dynamic config, secret, feature flag, or external policy.
3. Define schema, validation, defaults, precedence, source authority, and effective-value diagnostics.
4. Define loading, caching, refresh, consistency, restart, and provider-failure behavior.
5. Define access, encryption, redaction, rotation, revocation, audit, and emergency handling for secrets.
6. Define change workflow, compatibility, staged rollout, rollback, drift detection, and cleanup.
7. Add configuration contract, negative, security, refresh, rollback, and recovery tests.
8. Review against the readiness gate.

## Readiness Gate

Configuration is implementation-ready only when:

- every material key has an owner, schema, source, scope, and sensitivity classification;
- required/default/invalid behavior and precedence are deterministic;
- secrets use an approved lifecycle and never rely on source-code storage;
- dynamic refresh and stale/provider-failure behavior are explicit;
- environment, tenant, and privilege boundaries are enforced;
- rollout, rollback, audit, drift detection, and cleanup are defined;
- diagnostics expose safe provenance without exposing values;
- verification covers startup, change, failure, recovery, and rotation;
- unresolved safety or ownership decisions block affected implementation.

## Reference Routing

- Read [schema-loading-and-change.md](references/schema-loading-and-change.md) for key schemas, precedence, validation, refresh, compatibility, drift, rollout, and rollback.
- Read [secrets-and-feature-controls.md](references/secrets-and-feature-controls.md) for secrets lifecycle and the boundary between configuration and feature flags.
- Invoke `software-security-standard` for secret/key protection, access, audit, privacy, and secure failure.
- Invoke `deployment-release-standard` when configuration changes participate in rollout, rollback, promotion, or feature release.
- Invoke `resilience-standard` when a configuration provider is a runtime dependency.
- Invoke `logging-standard` and `operability-standard` for safe diagnostics, drift alerts, ownership, and runbooks.

## System Design and SDD Boundary

- In System Design, decide configuration ownership, source, schema, sensitivity, precedence, refresh model, failure behavior, secret lifecycle, and change governance.
- In SDD, implement approved bindings, validators, adapters, refresh handlers, safe diagnostics, rotation hooks, deployment mappings, and tests.
- Return material source, precedence, security, consistency, or failure-policy changes to System Design before implementation.

## Expected Output

Return the configuration inventory and classification, schema and precedence, loading and refresh model, secret lifecycle, access and audit controls, rollout/rollback and drift plan, failure behavior, observability, verification evidence, assumptions, and unresolved decisions.
