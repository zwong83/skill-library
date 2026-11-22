---
name: test-analysis-standard
description: Analyze approved requirements, relevant design and change impact to produce a complete traceable Test Case Matrix, specialist allocation, prerequisites, outputs, coverage, and evidence criteria before coding or during a later coverage review; use for TA, not test-code generation.
---

# Test Analysis Standard

## Input and output contract

This summary follows the detailed workflow and linked gates below. Record source owners, locations/versions and decision status; keep unknowns explicit.

- **Required inputs:** Analysis/review scope, approved behavior/acceptance, relevant design and change-impact context.
- **Conditional inputs:** Diff/snapshot and tests/results for post-implementation review; task IDs/formal artifacts only when supplied or required.
- **Optional context:** Prior defects and supplementary risk evidence.
- **Outputs:** Case Matrix/plan, allocation, applicability decisions, prerequisites and TA readiness in the existing/requested artifact.
- **Destination and consumer:** Use the workflow's existing, requested or documented default artifact/handoff location. Return results to the invoking agent or user for the identified downstream owner; this does not authorize automatic invocation or duplicate artifacts.
- **Completion:** Resolve source/risk/oracle/owner coverage and conditional decisions; planned setup may suffice for analysis, never for a test pass.


Use this skill independently for initial test planning or coverage review after a change. TA defines what must be proven and at which level; it does not write code, execute tests or replace requirements. Formal OpenSpec artifacts and lifecycle modes are optional context, not universal prerequisites. Preserve any explicitly mandated project gates.

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

1. Confirm source baseline, selected scope/change, affected components, and unresolved-item result.
2. Build the change-impact and risk register. When tests/evidence exist, inventory TDD and other coverage before proposing more tests. Identify suitable existing tests, reusable current evidence, required reruns and missing coverage; initial analysis does not require tests to exist yet.
3. Identify test conditions and partition them into concrete cases, including positive, negative, and boundary categories.
4. Apply the conditional contract/system-E2E criteria in [test-level-selection.md](references/test-level-selection.md#conditional-contract-and-systeme2e-testing) and record each applicability decision and rationale. Assign level/type, governing specialist, execution owner, TDD route, priority, automation intent, prerequisites, environment, data, dependencies, output/evidence, and disposition.
5. Map cases to approved sources and risks. Link supplied implementation tasks or acceptance gates when available; initial analysis does not require task-planning artifacts.
6. Record coverage gaps, assumptions, blocked cases, residual risk, and owners.
7. Run the analysis readiness gate and return the scoped plan or coverage-review findings to the user without invoking another workflow.

## Reference routing

- Read [test-analysis-template.md](references/test-analysis-template.md) to create a TA artifact.
- Consult [bdd-testing-standard](../bdd-testing-standard/SKILL.md) in specification mode for business acceptance examples. Record BDD as the approach, the actual underlying level and one execution owner; reuse existing scenarios/tests and preserve active TDD ownership. BDD is selected when requested or useful for shared executable acceptance, not mandatory for every change.
- Read [test-level-selection.md](references/test-level-selection.md) for the required contract/system-E2E applicability decisions and whenever level selection or duplication is unclear.
- Invoke `unit-testing-standard` only to refine unit/component case expectations.
- Invoke `integration-testing-standard` only to refine real-boundary cases and environment needs.
- Invoke `contract-testing-standard` for provider/consumer schema, protocol, semantic, version, and compatibility cases.
- Invoke `ui-testing-standard` for component/interaction, visual, accessibility, compatibility, and UI-journey cases.
- Invoke `system-e2e-testing-standard` for critical multi-component journeys that cannot be proven at a lower level.
- Invoke [performance-testing-standard](../performance-testing-standard/SKILL.md) in planning mode for measurable performance/capacity cases, approved targets, representative workloads, comparable baselines and explicit execution prerequisites. Do not run load or invoke execution agents during TA.
- Invoke `security-testing-standard` for authorized verification of approved security controls and required safety/evidence prerequisites.
- Invoke `regression-testing-standard` for impact-based regression selection and verdict requirements.
- Invoke `testing-strategy-standard` when the broader portfolio, non-functional scope, release gate, or organizational test policy is unresolved.

## Readiness gate

Return `TA-Ready` only when both conditional-specialist applicability decisions are resolved with traceable rationale and coverage; material requirements and design decisions are resolved; every material source/risk maps to complete cases; positive coverage exists; applicable negative and boundary partitions are present or explicitly not applicable; oracles, governing specialists, and execution owners are explicit; levels are justified; prerequisites, data, environments, dependencies, outputs, and evidence are available or planned; source/risk traceability is complete and supplied tasks are linked when available; and skipped/blocked coverage is visible with an owner or accepted residual risk.

## Output

Produce `test-analysis.md` or update the supplied plan in the user-approved evidence location. A supplied OpenSpec change can be referenced, but no OpenSpec project or schema is required. TA readiness is plan quality, not code authorization or execution success. Return baseline, risk register, complete Test Case Matrix, category/level/governing-specialist/execution-owner allocation, specialist prerequisites and expected outputs, data/environment/authorization plan, task mapping, coverage gaps, residual risk, and readiness verdict.
