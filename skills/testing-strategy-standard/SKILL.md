---
name: testing-strategy-standard
description: Design, implement, or review a risk-based software testing strategy, including requirement traceability, static testing, unit/component, integration, contract, system, end-to-end, acceptance, security, performance, resilience, migration, compatibility, test data and environments, automation, coverage, flaky-test control, release gates, and evidence.
---

# Testing Strategy Standard

Use this skill when a feature, system, migration, or release needs a deliberate test portfolio and evidence. It coordinates specialized test concerns without forcing one test pyramid or toolchain onto every architecture.

## Core Rules

1. Derive testing from requirements, risks, architecture boundaries, failure modes, change impact, and user journeys. Do not equate testing with executing existing test files.
2. Testing can reveal defects and reduce uncertainty; it cannot prove the absence of defects.
3. Assign each behavior to the lowest-cost test level that provides trustworthy evidence, then retain broader tests for cross-boundary and user-visible risks.
4. Balance static review, unit/component, integration, contract, system/end-to-end, acceptance, and non-functional testing according to the system.
5. Test success, validation, authorization, failure, boundary, state, concurrency, duplicate, timeout, recovery, compatibility, and observability behavior where applicable.
6. Keep tests deterministic, isolated, repeatable, and diagnostic. Control time, randomness, external dependencies, concurrency, and shared state.
7. Treat test data and environments as governed assets. Minimize sensitive data and define reset, ownership, fidelity, and drift.
8. Use coverage and mutation or fault evidence as signals, not substitute targets for meaningful assertions.
9. Flaky tests are defects. Quarantine only with owner, reason, impact, expiry, and restoration plan; never silently ignore them.
10. Define release gates from risk and evidence. A passing checkbox without trustworthy execution evidence is not completion.
11. Preserve traceability from requirement and design decision to scenario, test, result, and defect disposition.

## Workflow

1. Identify scope, changed behavior, requirements, architecture, critical journeys, risks, and acceptance criteria.
2. Build a risk register using likelihood, impact, detectability, change complexity, and exposure.
3. Select test levels, types, techniques, environments, data, tools, and ownership for each risk.
4. Specify scenarios and oracles, including negative, boundary, state, concurrency, failure, recovery, and compatibility behavior.
5. Define automation, isolation, doubles/fixtures, external dependency strategy, and diagnostic evidence.
6. Define non-functional security, performance, resilience, migration, accessibility, and operational tests when applicable.
7. Define execution order, pipeline gates, flaky-test policy, defect disposition, reporting, and exit criteria.
8. Execute or review evidence, report limitations, and update traceability and residual risk.

## Readiness Gate

A test strategy is ready only when:

- scope, requirements, risks, critical journeys, and acceptance criteria are traceable;
- selected levels and types cover each material risk without unjustified duplication;
- scenarios include relevant negative, boundary, state, concurrency, failure, and recovery behavior;
- environments, data, dependencies, isolation, and cleanup are defined;
- automation and manual testing choices have a clear reason and owner;
- non-functional and migration/compatibility concerns are included when applicable;
- gates, exit criteria, defect handling, flaky-test control, and evidence retention are explicit;
- skipped or impossible tests and residual risks are visible and owned.

## Reference Routing

- Read [risk-portfolio-and-techniques.md](references/risk-portfolio-and-techniques.md) for risk analysis, test levels/types, scenario design, techniques, and portfolio selection.
- Read [automation-data-environments-and-evidence.md](references/automation-data-environments-and-evidence.md) for automation, isolation, doubles, environments, data, flakiness, gates, reporting, and evidence.
- Invoke `test-analysis-standard` after approved requirements/design to derive change-specific scenarios, level allocation, task mapping, and the pre-Apply TA gate.
- Invoke `unit-testing-standard` for deterministic unit/component test design and review.
- Invoke `integration-testing-standard` for real adapter, datastore, broker, cache, framework, serialization, and service-boundary tests.
- Invoke `contract-testing-standard` for provider/consumer schema, protocol, semantic, version, and compatibility verification.
- Invoke `ui-testing-standard` for UI component/interaction, visual, accessibility, compatibility, and critical UI journey tests.
- Invoke `system-e2e-testing-standard` for critical multi-component business and operational journeys in a representative deployed environment.
- Invoke `regression-testing-standard` for change-impact suite selection, cross-level regression execution, and a unified regression verdict.
- Invoke `tdd-standard` only when implementation is authorized and the task will follow Red-Green-Refactor.
- Invoke `software-security-standard` for authoritative threat/control design and `security-testing-standard` for authorized, bounded verification of those controls.
- Invoke `backend-performance-capacity-standard` for workload, performance, capacity, benchmark, load, stress, spike, soak, scalability, and performance-regression tests.
- Invoke `backend-resilience-standard` for timeout, retry, overload, degradation, dependency-loss, failover, and recovery scenarios.
- Invoke `backend-api-design-standard`, `backend-database-persistence-standard`, `backend-caching-standard`, and `backend-messaging-standard` for contract-, migration-, consistency-, and technology-specific tests.
- Invoke `deployment-release-standard` and `backend-operability-standard` for pipeline gates, production verification, drills, telemetry, and operational readiness evidence.

## System Design and SDD Boundary

- In System Design, decide risk coverage, required test levels/types, environments, evidence, non-functional verification, and release/operational gates.
- In SDD, implement approved test cases, fixtures, doubles, harnesses, datasets, pipeline jobs, reports, and traceability; execute and record actual results.
- Return missing acceptance behavior, material architecture assumptions, or changed risk decisions to the owning requirements or System Design artifact.

## Expected Output

Return scope and risks, traceability matrix, selected test portfolio, scenarios and techniques, environment/data/dependency strategy, automation and flakiness policy, non-functional plan, execution and gates, evidence and defect results, residual risk, assumptions, and unresolved decisions.
