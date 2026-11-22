# Test Analysis Template

## 1. Control and baseline

Record change ID, scope, analyst, date, source paths/versions/statuses, optional supplied task/change identifiers, code baseline, and TA status.

## 2. Change impact

List affected journeys, components, APIs/events, data/schema, permissions, configuration, dependencies, migrations, operations, compatibility, and rollback paths.

## 3. Risk register

For each risk capture ID, source, failure, likelihood, impact, detectability, exposure, priority, mitigation, and owner.

## 4. Test Case Matrix

| Case ID | Source/risk IDs | Category | Preconditions | Exact input/action | Expected outcome and forbidden effects | Level/type | Governing specialist | Execution owner / TDD route | Priority | Data/environment/dependencies | Automation | Expected output/evidence | Status |
|---|---|---|---|---|---|---|---|---|---|---|---|---|---|

Give every material behavior at least one positive case. Include negative and exact boundary partitions (for example below/at/above a threshold) whenever applicable, plus state, authorization, concurrency, duplicate, timeout, failure, recovery, migration, compatibility, UI, performance, regression, and other non-functional cases. Record `Not Applicable` with rationale instead of silently omitting an expected category.

## 5. Coverage and task mapping

For BDD-selected cases, record the source-to-Given/When/Then-scenario-to-test mapping, approval/open questions, actual underlying test level, one execution owner and existing evidence reuse. BDD is an approach, not an extra level or an automatic second suite. Preserve active TDD ownership and conditional contract/E2E obligations.

Reference the authoritative BDD scenario location/version and IDs used by implementation and testing; do not copy those definitions into a second maintained scenario set. Link the matrix's exact expectations to those scenarios and add case-specific data or boundary details only where needed. Keep binding/test references and each run's evidence separate, and record proposed scenario gaps/changes for the owning source rather than silently redefining expectations here.

Map each material source requirement, approved source scenario, design decision, and supplied implementation task to one or more cases. Initial requirements-based analysis uses source/risk IDs; task mapping is added when tasks exist. Show positive/negative/boundary completeness, governing specialist, execution owner/TDD route, expected output, intentional exclusions, and duplicated coverage rationale.

For available test coverage, record the existing test/evidence reference and whether each case needs new coverage, a rerun, or may reuse retained evidence with rationale. TDD-authored tests do not need duplicate ownership or recreation; scoped results must still match the required snapshot and conditions.

### Conditional specialist applicability

Apply the [contract/system-E2E selection criteria](test-level-selection.md#conditional-contract-and-systeme2e-testing). Record both decisions for every change; use separate rows for materially different scopes.

| Specialist | Affected scope and source/risk IDs | Required / Not Applicable | Criterion and rationale | Required or alternative coverage case IDs and evidence criteria | Owner and residual gaps |
|---|---|---|---|---|---|
| contract-testing-agent | | | | | |
| system-e2e-testing-agent | | | | | |

Unresolved applicability is an open decision that blocks TA readiness. Planned execution prerequisites belong below; unavailable resources are not a reason for `Not Applicable`.

## 6. Data, environment, and dependencies

Define fixtures/datasets, classification, reset/cleanup, time/random controls, external systems or test doubles, infrastructure, observability, and access.

## 7. Entry, exit, and evidence

Define prerequisites, required pass evidence, defect disposition, flaky-test handling, skipped checks, residual risk, and convergence/release impact.

## 8. Open and blocked items

Record the source gap, affected scenarios/tasks, decision needed, owner, and next action. Do not make TA-Ready while material expected behavior remains unknown.
