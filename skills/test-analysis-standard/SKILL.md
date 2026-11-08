---
name: test-analysis-standard
description: Analyze approved requirements, System Design, OpenSpec artifacts, and change impact to produce a complete traceable Test Case Matrix, specialist allocation, prerequisites, outputs, coverage, and evidence criteria before implementation; use for TA, not test-code generation.
---

# Test Analysis Standard

Use this skill after behavior and design are sufficiently resolved and before implementation begins. TA defines what must be proven and at which level; it does not write test code or replace the governing requirements.

## Core rules

1. Derive test cases from requirements, acceptance criteria, design decisions, state models, interfaces, data invariants, risks, and code-change impact.
2. Preserve traceability from source ID to risk, case, selected test level/specialist, expected evidence, and residual gap.
3. Select the lowest-cost trustworthy level, then add broader tests only for cross-boundary, user-visible, compatibility, performance, or regression risk.
4. Give every material behavior at least one positive case. Add negative and boundary cases for every applicable input/state partition, and record `Not Applicable` with rationale where a category genuinely does not apply.
5. Cover alternate valid flow, validation, authorization, forbidden side effects, state transition, duplicate, concurrency, timeout, dependency failure, recovery, migration, compatibility, observability, UI, performance, and regression risk where applicable.
6. Separate unit/component, integration, contract, UI, system/end-to-end, acceptance, performance, security, regression, and other non-functional cases. Do not label a mocked unit test as integration.
7. Define the oracle precisely: exact inputs/actions, output, state, side effects, absence of forbidden effects, events, telemetry, and cleanup.
8. Expose missing acceptance behavior or design ambiguity as blockers; do not invent an expected result to complete TA.
9. Treat test data, environments, external dependencies, clocks, randomness, concurrency, specialist prerequisites, and evidence destinations as explicit analysis inputs.

## Workflow

1. Confirm source baseline, selected change, affected components, and unresolved-item result.
2. Build the change-impact and risk register.
3. Identify test conditions and partition them into concrete cases, including positive, negative, and boundary categories.
4. Assign level/type, governing specialist, execution owner, TDD route, priority, automation intent, prerequisites, environment, data, dependencies, output/evidence, and disposition.
5. Map cases to implementation tasks and release/convergence gates.
6. Record coverage gaps, assumptions, blocked cases, residual risk, and owners.
7. Run the TA readiness gate before Apply.

## Reference routing

- Read [test-analysis-template.md](references/test-analysis-template.md) to create a TA artifact.
- Read [test-level-selection.md](references/test-level-selection.md) when unit/integration/contract/system level selection or duplication is unclear.
- Invoke `unit-testing-standard` only to refine unit/component case expectations.
- Invoke `integration-testing-standard` only to refine real-boundary cases and environment needs.
- Invoke `contract-testing-standard` for provider/consumer schema, protocol, semantic, version, and compatibility cases.
- Invoke `ui-testing-standard` for component/interaction, visual, accessibility, compatibility, and UI-journey cases.
- Invoke `system-e2e-testing-standard` for critical multi-component journeys that cannot be proven at a lower level.
- Invoke `performance-capacity-standard` for measurable benchmark, load, stress, spike, soak, capacity, and performance-regression cases.
- Invoke `security-testing-standard` for authorized verification of approved security controls and required safety/evidence prerequisites.
- Invoke `regression-testing-standard` for impact-based regression selection and verdict requirements.
- Invoke `testing-strategy-standard` when the broader portfolio, non-functional scope, release gate, or organizational test policy is unresolved.

## Readiness gate

TA is Apply-ready only when material requirements and design decisions are resolved; every material source/risk maps to complete cases; positive coverage exists; applicable negative and boundary partitions are present or explicitly not applicable; oracles, governing specialists, and execution owners are explicit; levels are justified; prerequisites, data, environments, dependencies, outputs, and evidence are available or planned; tasks are traceable; and skipped/blocked coverage is visible with an owner or accepted residual risk.

## Output

Produce `test-analysis.md` in the project-approved evidence location. If stored inside an OpenSpec change without schema support, label it as a supplemental extension rather than a built-in artifact. Return baseline, risk register, complete Test Case Matrix, category/level/governing-specialist/execution-owner allocation, specialist prerequisites and expected outputs, data/environment/authorization plan, task mapping, coverage gaps, residual risk, and readiness verdict.
