---
name: regression-testing-standard
description: Select, execute, and review risk-based regression coverage across unit, integration, contract, UI, end-to-end, performance, and other existing suites from a verified change impact; use after change scope is known, not as a substitute for feature-specific test analysis.
---

# Regression Testing Standard

Use this skill to determine what existing behavior must be re-proven after code, configuration, schema, dependency, infrastructure, or contract changes.

## Core rules

1. Select regression coverage from the verified diff, affected dependencies, contracts, data, configuration, runtime topology, incidents, and defect history; do not equate regression with running every available test.
2. Preserve traceability from change and risk to selected suites/cases, results, defects, exclusions, and residual risk.
3. Combine fast broad signals with targeted real-boundary and critical-journey evidence. A passing unit suite does not prove integration or UI compatibility.
4. Include the new feature's positive, negative, and boundary cases plus existing behavior that can be affected directly or transitively.
5. Convert every confirmed defect into durable coverage at the lowest trustworthy level, then add broader protection only when the failure crossed a boundary or journey.
6. Record the base and target revisions, environment, data, dependency versions, commands, shard/retry behavior, skips, and result provenance.
7. Treat flaky, quarantined, missing, stale, or non-executed tests as visible risk; retries do not turn an unstable result into clean evidence.
8. Separate functional regression from visual, performance, security, migration, compatibility, resilience, and operational regression while keeping a unified verdict.
9. Do not update assertions or baselines merely to match changed behavior unless the governing requirement/design approves that behavior.
10. A regression verdict cannot be `Passed` while a required suite is failing, blocked, silently skipped, or lacks trustworthy evidence.

## Workflow

1. Confirm the base/target revisions, approved change, actual diff, TA matrix, and prior baseline.
2. Build direct and transitive impact paths across modules, interfaces, data, configuration, dependencies, deployment, and user journeys.
3. Select required suites/cases by risk and test level; identify gaps and assign them to the owning specialist.
4. Execute in a diagnostic order: fast/static and unit signals, integration/contract, UI/system journeys, then applicable non-functional regression.
5. Triage failures as product defect, test defect, environment issue, known accepted issue, or inconclusive evidence.
6. Publish scope, results, exclusions, gaps, defects, residual risk, and `Regression-Passed`, `Regression-Failed`, or `Regression-Blocked`.

## Reference routing

- Read [impact-selection-and-suites.md](references/impact-selection-and-suites.md) to select coverage from change impact.
- Read [regression-evidence-and-gates.md](references/regression-evidence-and-gates.md) for result classification, evidence, and verdict rules.
- Invoke `unit-testing-standard`, `integration-testing-standard`, `contract-testing-standard`, `ui-testing-standard`, `system-e2e-testing-standard`, or `security-testing-standard` only for gaps or failures owned by that level/type.
- Invoke `performance-capacity-standard` for performance baselines and load/stress/spike/soak regression.
- Invoke the relevant security, resilience, migration, deployment, or operability Skill only when that regression risk is in scope.

## Output

Produce `regression-test-report.md` or equivalent project-approved evidence. Return base/target revisions, impact map, selected and excluded suites with rationale, exact execution/results, failures and disposition, flakiness/quarantine, coverage gaps, residual risk, and regression verdict.
