---
name: system-e2e-testing-standard
description: Design, implement, execute, or review traceable system and end-to-end tests for critical multi-component journeys in a representative deployed environment, including data, identities, async completion, observability, cleanup, and failure evidence; not for exhaustive lower-level coverage.
---

# System and End-to-End Testing Standard

## Input and output contract

This summary follows the detailed workflow and linked gates below. Record source owners, locations/versions and decision status; keep unknowns explicit.

- **Required inputs:** Approved critical journey/cases, actors/start/end states and system/component boundary.
- **Conditional inputs:** Deployed versions/topology, identities/data/dependencies, observability/cleanup and authorization for execution; correlated evidence for review.
- **Optional context:** Journey incidents and representative traffic examples.
- **Outputs:** Authorized tests and journey report with authoritative effects, fidelity gaps and E2E verdict.
- **Destination and consumer:** Use the workflow's existing, requested or documented default artifact/handoff location. Return results to the invoking agent or user for the identified downstream owner; this does not authorize automatic invocation or duplicate artifacts.
- **Completion:** Required cross-component outcomes need evidence; UI success or an HTTP response alone cannot prove the journey.


Use this skill when a business or operational outcome can be proven only through multiple deployed components, services, interfaces, data stores, or asynchronous stages working together.

## Core rules

1. Trace every journey to approved requirements, approved source/test cases, actors, starting state, business outcome, and critical risk.
2. Keep the E2E portfolio small and risk-based. Lower levels should prove detailed rule partitions; E2E proves wiring, configuration, identity, routing, persistence, and cross-component outcome.
3. Define the exact system boundary, deployed versions, topology, feature/configuration state, external dependency treatment, and meaningful differences from production.
4. Use controlled identities, tenants, data, time, and correlation IDs. Isolate and clean up all created state, including asynchronous messages, files, cache entries, and external test records.
5. Cover the critical positive journey and material negative, boundary, authorization/isolation, partial-failure, duplicate, timeout, recovery, and rollback paths that cannot be trusted from lower-level evidence alone.
6. Use condition-based completion with bounded deadlines for asynchronous flows; do not rely on arbitrary sleeps or unlimited polling.
7. Assert business outcome, authoritative state, user-visible result, emitted/consumed events, forbidden side effects, and required telemetry across the journey.
8. Preserve diagnostics from each component without leaking secrets or unnecessary sensitive data.
9. Treat environment drift, shared-state collisions, unstable dependencies, and flaky journeys as defects or explicit blockers.
10. Do not run destructive, high-load, or production-impacting journeys without separate explicit authorization and safety controls.

## Workflow

1. Select approved source/test cases requiring system/E2E proof and define the journey graph and boundary.
2. Confirm environment/topology, deployed revisions, identities, data, external dependencies, observability, isolation, cleanup, and authorization.
3. Implement critical journeys with stable business-level oracles and bounded async coordination.
4. Execute focused journeys, collect cross-component evidence, classify product/test/environment failures, and verify cleanup.
5. Report journey coverage, results, gaps, flakiness, environment fidelity, residual risk, and verdict.

## Reference routing

- Read [journey-and-boundary-matrix.md](references/journey-and-boundary-matrix.md) to define actors, stages, components, states, and oracles.
- Read [environment-data-and-evidence.md](references/environment-data-and-evidence.md) for deployed environment, data, async coordination, cleanup, and diagnostics.
- Invoke `ui-testing-standard` when the journey enters through a UI and UI behavior is part of the oracle.
- Invoke `contract-testing-standard` for provider/consumer compatibility that does not require the whole journey.
- Invoke `integration-testing-standard` for a focused real boundary rather than the complete system outcome.
- Invoke `backend-resilience-standard` or `deployment-release-standard` only when the journey includes their approved concerns.

## Output

Produce `system-e2e-test-report.md` or equivalent retained evidence. Return source/case IDs, journey and component graph, deployed revisions/configuration, environment/data/identity/dependency plan, test files changed when authorized, commands/results, cross-component artifacts, cleanup result, fidelity gaps, flakiness/blockers, residual risk, and `E2E-Passed`, `E2E-Failed`, or `E2E-Blocked`.
