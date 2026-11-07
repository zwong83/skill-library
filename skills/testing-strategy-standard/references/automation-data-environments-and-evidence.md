# Automation, Data, Environments, and Evidence

## Automation Selection

Automate repeatable, high-value checks that need frequent or precise execution. Keep exploratory, usability, visual judgment, or rare complex recovery work manual when automation cost exceeds durable value. Record the reason either way.

Automated tests should be deterministic, independent, order-insensitive, bounded, and diagnostic. Control clocks, randomness, locale, network, external systems, scheduling, and shared state. Prefer language-native fakes for owned boundaries and realistic emulators/containers/test instances when behavior fidelity matters. Verify test doubles against real contracts.

## Test Data

- Generate the smallest representative data set that proves behavior.
- Define ownership, classification, provenance, lifecycle, reset, retention, and deletion.
- Do not copy production personal or secret data without explicit authorization, protection, and necessity.
- Include boundary sizes, skew, historical shapes, invalid states, and migration versions where relevant.
- Keep fixtures readable and avoid hidden cross-test coupling.

## Environments

Define purpose, topology, version, configuration, dependencies, data, access, fidelity, drift detection, capacity, cost, reset, and owner. Use production-like environments for decisions that depend on production topology or performance, while acknowledging differences explicitly.

Ephemeral environments reduce interference but do not automatically reproduce shared infrastructure, scale, or managed-service behavior. Shared environments require namespace/isolation and cleanup controls.

## Flakiness and Failure Diagnosis

A retry may gather evidence but must not turn an initial failure into a silent pass. Record first-attempt and retry outcomes. Quarantine only to protect the pipeline temporarily, with owner, linked defect, impact, expiry, and restoration criterion.

Capture test name/scenario, source/artifact version, environment, seed, inputs or safe fixture identity, timing, logs/traces, dependency state, expected/actual result, and cleanup status.

## Gates and Evidence

Define mandatory checks by risk and stage. Record exact command or job, version, start/end, result, skipped tests, retries, flaky outcomes, environment, artifacts, coverage limitations, defects, approvals, and residual risk. A gate should block only when its evidence is trustworthy and its failure has an accountable resolution path.

Exit criteria may include required scenario pass, no open defects above an approved severity, migration/recovery evidence, non-functional thresholds, traceability completeness, and accepted residual risk. Never report unexecuted tests as passing.

## Production Verification

Post-deployment smoke, synthetic, canary, telemetry, business, audit, and reconciliation checks complement pre-production testing. They do not justify skipping safe pre-production evidence. Define automatic abort and operator escalation with `deployment-release-standard` and `operability-standard`.
