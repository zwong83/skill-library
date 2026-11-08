# Test Analysis Template

## 1. Control and baseline

Record change ID, scope, analyst, date, source paths/versions/statuses, OpenSpec change/schema, code baseline, and TA status.

## 2. Change impact

List affected journeys, components, APIs/events, data/schema, permissions, configuration, dependencies, migrations, operations, compatibility, and rollback paths.

## 3. Risk register

For each risk capture ID, source, failure, likelihood, impact, detectability, exposure, priority, mitigation, and owner.

## 4. Test Case Matrix

| Case ID | Source/risk IDs | Category | Preconditions | Exact input/action | Expected outcome and forbidden effects | Level/type | Governing specialist | Execution owner / TDD route | Priority | Data/environment/dependencies | Automation | Expected output/evidence | Status |
|---|---|---|---|---|---|---|---|---|---|---|---|---|---|

Give every material behavior at least one positive case. Include negative and exact boundary partitions (for example below/at/above a threshold) whenever applicable, plus state, authorization, concurrency, duplicate, timeout, failure, recovery, migration, compatibility, UI, performance, regression, and other non-functional cases. Record `Not Applicable` with rationale instead of silently omitting an expected category.

## 5. Coverage and task mapping

Map each material source requirement, OpenSpec scenario, design decision, and implementation task to one or more cases. Show positive/negative/boundary completeness, governing specialist, execution owner/TDD route, expected output, intentional exclusions, and duplicated coverage rationale.

## 6. Data, environment, and dependencies

Define fixtures/datasets, classification, reset/cleanup, time/random controls, external systems or test doubles, infrastructure, observability, and access.

## 7. Entry, exit, and evidence

Define prerequisites, required pass evidence, defect disposition, flaky-test handling, skipped checks, residual risk, and convergence/release impact.

## 8. Open and blocked items

Record the source gap, affected scenarios/tasks, decision needed, owner, and next action. Do not make TA Apply-ready while material expected behavior remains unknown.
