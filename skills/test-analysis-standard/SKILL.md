---
name: test-analysis-standard
description: Analyze approved requirements, System Design, OpenSpec artifacts, and change impact to produce traceable risk-based test scenarios, level selection, data/environment needs, coverage, priorities, and evidence criteria before implementation; use for TA, not test-code generation.
---

# Test Analysis Standard

Use this skill after behavior and design are sufficiently resolved and before implementation begins. TA defines what must be proven and at which level; it does not write test code or replace the governing requirements.

## Core rules

1. Derive scenarios from requirements, acceptance criteria, design decisions, state models, interfaces, data invariants, risks, and code-change impact.
2. Preserve traceability from source ID to risk, scenario, selected test level, expected evidence, and residual gap.
3. Select the lowest-cost trustworthy level, then add broader tests only for cross-boundary or user-visible risk.
4. Cover success, alternate valid flow, validation, boundary, authorization, forbidden side effects, state transition, duplicate, concurrency, timeout, dependency failure, recovery, migration, compatibility, and observability where applicable.
5. Separate unit/component, integration, contract, system/end-to-end, acceptance, and non-functional scenarios. Do not label a mocked unit test as integration.
6. Define the oracle precisely: output, state, side effects, absence of forbidden effects, events, telemetry, and cleanup.
7. Expose missing acceptance behavior or design ambiguity as blockers; do not invent an expected result to complete TA.
8. Treat test data, environments, external dependencies, clocks, randomness, and concurrency as explicit analysis inputs.

## Workflow

1. Confirm source baseline, selected change, affected components, and unresolved-item result.
2. Build the change-impact and risk register.
3. Identify test conditions and partition them into concrete scenarios.
4. Assign level/type, priority, automation intent, environment, data, dependencies, and evidence.
5. Map scenarios to implementation tasks and release/convergence gates.
6. Record coverage gaps, assumptions, blocked scenarios, residual risk, and owners.
7. Run the TA readiness gate before Apply.

## Reference routing

- Read [test-analysis-template.md](references/test-analysis-template.md) to create a TA artifact.
- Read [test-level-selection.md](references/test-level-selection.md) when unit/integration/contract/system level selection or duplication is unclear.
- Invoke `unit-testing-standard` only to refine unit/component scenario expectations.
- Invoke `integration-testing-standard` only to refine real-boundary scenarios and environment needs.
- Invoke `testing-strategy-standard` when the broader portfolio, non-functional scope, release gate, or organizational test policy is unresolved.

## Readiness gate

TA is Apply-ready only when material requirements and design decisions are resolved, critical risks have scenarios, scenario oracles are explicit, levels are justified, data/environments/dependencies are available or planned, tasks are traceable, and skipped/blocked coverage is visible with an owner or accepted residual risk.

## Output

Produce `test-analysis.md` in the project-approved evidence location. If stored inside an OpenSpec change without schema support, label it as a supplemental extension rather than a built-in artifact. Return baseline, risk register, scenario matrix, test-level allocation, data/environment plan, task mapping, coverage gaps, residual risk, and readiness verdict.
