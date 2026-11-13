---
name: deployment-release-standard
description: Design, implement, or review safe software build, deployment, and release processes, including immutable artifacts, provenance, environments, promotion, compatibility, database and configuration sequencing, rolling/canary/blue-green rollout, feature release, health gates, rollback or roll-forward, approvals, evidence, and cleanup.
---

# Deployment and Release Standard

Use this skill when software, configuration, schema, infrastructure, or a feature must move safely from source through environments into user-visible operation.

## Core Rules

1. Distinguish build, deploy, and release. Deployment places an artifact in an environment; release exposes behavior to users.
2. Build once, identify immutably, verify, and promote the same artifact. Do not rebuild differently for each environment.
3. Make the pipeline reproducible, least-privileged, auditable, and protected against untrusted inputs and secret leakage.
4. Define compatibility across application, API, event, data, configuration, dependency, and client versions during rollout and rollback.
5. Select rolling, canary, blue-green, recreate, or feature-controlled release from risk, state, capacity, observability, and recovery needs.
6. Use explicit entry, success, guardrail, pause, abort, promotion, and completion criteria.
7. Treat database and irreversible state changes separately; rollback may require roll-forward repair.
8. Make readiness, drain, graceful shutdown, startup, and traffic-switch behavior part of the deployment contract.
9. Feature flags need safe defaults, targeting privacy, ownership, expiry, and cleanup; they do not replace authorization.
10. Keep evidence for artifact identity, approvals, validation, deployment, exposure, rollback, and post-release verification.
11. Do not mutate production, deploy, or release merely because this skill was invoked; obtain required authorization immediately before external changes.

## Workflow

1. Define release unit, artifact, environments, owners, users, risk, dependencies, and compatibility window.
2. Define build provenance, dependency controls, verification, storage, signing/attestation where required, and promotion.
3. Define environment configuration, secrets, infrastructure, database, cache, messaging, and dependency prerequisites.
4. Select rollout and feature-release strategies with capacity and failure-domain rationale.
5. Define pre-deploy checks, migration order, readiness, drain, health gates, telemetry, and staged exposure.
6. Define pause, abort, rollback, roll-forward, restore, reconciliation, and manual intervention.
7. Define approvals, separation of duties, audit evidence, notifications, runbooks, and ownership.
8. Validate in representative environments and perform post-release verification and cleanup.

## Readiness Gate

A release design is ready only when:

- artifact identity, source, provenance, verification, and promotion path are known;
- environment, configuration, secret, schema, and dependency prerequisites are explicit;
- mixed-version and rollback compatibility are demonstrated or risk-approved;
- strategy, capacity, readiness, drain, health, and exposure gates are defined;
- database/state changes have a realistic recovery path;
- guardrails, pause, abort, rollback/roll-forward, and reconciliation are tested;
- feature controls have safe defaults, ownership, expiry, and cleanup;
- approvals, evidence, operator ownership, and post-release verification exist;
- unresolved safety, compatibility, or recovery decisions block release.

## Reference Routing

- Read [artifacts-pipeline-and-environments.md](references/artifacts-pipeline-and-environments.md) for immutable artifacts, provenance, CI/CD controls, promotion, environments, and compatibility.
- Read [rollout-release-and-recovery.md](references/rollout-release-and-recovery.md) for strategy selection, gates, feature controls, migrations, rollback, roll-forward, and evidence.
- Invoke `db-standard` for migration/backfill compatibility and recovery.
- Check rollout surge, canary representativeness, scaling, and failover headroom against the approved capacity model.
- Invoke `backend-resilience-standard` for drain, health, degraded behavior, dependency loss, and recovery.
- Invoke `software-security-standard` for pipeline, artifact, dependency, identity, secret, and supply-chain controls.

## System Design and SDD Boundary

- In System Design, decide deployment topology, compatibility, rollout/release strategy, health semantics, migration order, recovery strategy, and operational ownership.
- In SDD, implement approved manifests, pipeline definitions, feature controls, probes, hooks, migration tasks, verification, telemetry, and runbooks.
- Return material topology, compatibility, data, security, exposure, or recovery changes to System Design.

## Expected Output

Return the release unit and artifact model, pipeline and environment design, compatibility matrix, rollout and feature-release strategy, migration sequence, gates and telemetry, rollback/roll-forward and reconciliation plan, approvals/evidence, cleanup, assumptions, and unresolved decisions.
