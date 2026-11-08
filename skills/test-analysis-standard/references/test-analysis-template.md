# Test Analysis Template

## 1. Control and baseline

Record change ID, scope, analyst, date, source paths/versions/statuses, OpenSpec change/schema, code baseline, and TA status.

## 2. Change impact

List affected journeys, components, APIs/events, data/schema, permissions, configuration, dependencies, migrations, operations, compatibility, and rollback paths.

## 3. Risk register

For each risk capture ID, source, failure, likelihood, impact, detectability, exposure, priority, mitigation, and owner.

## 4. Scenario matrix

| Scenario ID | Source/risk IDs | Preconditions | Action/event | Expected outcome and forbidden effects | Level/type | Priority | Data/environment/dependencies | Automation | Evidence |
|---|---|---|---|---|---|---|---|---|---|

Include positive, negative, boundary, state, authorization, concurrency, duplicate, timeout, failure, recovery, migration, compatibility, and non-functional scenarios when applicable.

## 5. Coverage and task mapping

Map each material source requirement, OpenSpec scenario, design decision, and implementation task to one or more scenarios. Record intentional exclusions and duplicated coverage rationale.

## 6. Data, environment, and dependencies

Define fixtures/datasets, classification, reset/cleanup, time/random controls, external systems or test doubles, infrastructure, observability, and access.

## 7. Entry, exit, and evidence

Define prerequisites, required pass evidence, defect disposition, flaky-test handling, skipped checks, residual risk, and convergence/release impact.

## 8. Open and blocked items

Record the source gap, affected scenarios/tasks, decision needed, owner, and next action. Do not make TA Apply-ready while material expected behavior remains unknown.
