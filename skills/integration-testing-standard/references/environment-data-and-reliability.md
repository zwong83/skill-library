# Environment, Data, and Reliability

## Environment

Use project-standard local services, containers, emulators, embedded components, shared environments, or dedicated test instances according to semantic fidelity and cost. Pin or report meaningful versions. An emulator is acceptable only when its differences do not invalidate the tested risk.

## Isolation and cleanup

Prefer a fresh database/schema/container/namespace where affordable. Otherwise use unique test identifiers and deterministic cleanup. Do not depend on execution order or pre-existing shared data. Verify cleanup after both success and failure.

## Asynchronous behavior

Wait on observable conditions with a deadline and useful diagnostics. Avoid fixed sleeps. Capture messages, offsets, state, logs/traces, or reconciliation results needed to explain failure. Ensure retries do not turn unknown partial outcomes into false success.

## Test data

Use minimal representative data with explicit classification and lifecycle. Cover versioned schemas, boundary sizes, tenant separation, historical/migration shapes, duplicates, invalid state, and conflicts when relevant. Do not copy sensitive production data without explicit authorization and controls.

## Reliability

Repeat critical integration tests when assessing isolation or flakiness, but preserve first-failure evidence. Quarantine requires owner, linked defect, impact, expiry, and restoration criteria. A retry pass does not erase the original failure.
