# Test Specialist Coordination

`test-analysis-agent` owns the unified TA artifact. Every executable case receives one test level/specialist classification and one execution owner. Specialists return evidence; they do not rewrite the TA oracle or broaden the approved behavior.

| Specialist | Required preconditions | Primary output |
|---|---|---|
| `unit-testing-agent` | Approved behavior, `TA-Ready` unit case IDs/oracles, current code/tests, project commands, write authorization when changing tests | Test files plus retained unit results or optional `unit-test-evidence.md` |
| `integration-testing-agent` | Approved boundary, `TA-Ready` integration cases, representative environment/version, data, isolation/cleanup, applicable authorization | Test/config files plus integration boundary evidence or optional `integration-test-evidence.md` |
| `contract-testing-agent` | Approved contract/evolution policy, TA contract cases, provider/consumer/version inventory, authoritative contract and verification workflow | `contract-test-report.md` and compatibility verdict |
| `tdd-agent` | Apply readiness, implementation authorization, selected task, stable case oracle, approved design constraints, current code/tests | Production/test changes plus observed Red-Green-Refactor cycle evidence |
| `ui-testing-agent` | Approved UI states, `TA-Ready` UI cases, supported matrix, environment/data/auth state, visual/accessibility baselines where applicable | `ui-test-report.md` or equivalent UI artifacts and results |
| `system-e2e-testing-agent` | Approved critical journey, TA E2E cases, deployed component revisions/topology, identities/data, dependencies, observability, cleanup, environment authorization | `system-e2e-test-report.md` and journey verdict |
| `performance-testing-agent` | Measurable objectives, workload/data model, target environment, baseline where compared, instrumentation, generator and abort plan, explicit load authorization | `performance-test-report.md` and retained raw evidence |
| `security-testing-agent` | Approved threats/controls and security cases, explicit target authorization, permitted techniques, identities/data, rate/stop limits, monitoring and evidence handling | `security-test-report.md` and security verdict |
| `regression-testing-agent` | Base/target revisions, actual diff/impact, TA matrix, suite inventory, specialist evidence, environment/data, known failures/flakes | `regression-test-report.md` and unified regression verdict |

## Routing rules

- Assign the lowest trustworthy primary level and add broader cases only for distinct boundary, journey, compatibility, performance, or user-visible risks.
- Every material behavior needs positive coverage. Add negative and boundary cases for every applicable input/state partition; record `Not Applicable` with rationale rather than silently omitting a category.
- A case must contain source/risk IDs, category, preconditions, exact input/action, expected outcome and forbidden effects, environment/data, automation intent, test level/specialist, execution owner, evidence, and owning task.
- When TDD is `Required` or activated `Conditional`, set `tdd-agent` as execution owner while retaining Unit or Integration as the test level and governing standard. Do not split its per-cycle tests into separate execution Agents.
- For non-TDD work, assign the appropriate unit, integration, contract, UI, system/E2E, performance, or security Agent as execution owner. Use those specialists after TDD only for independent verification or uncovered gaps.
- `regression-testing-agent` consumes evidence and coordinates gaps; it does not override a failed specialist result or edit production behavior.

TA is `TA-Ready` only when all material sources and risks map to one or more complete cases, each case has a test level/specialist and one execution owner, required prerequisites are available or planned, and gaps/blockers/residual risks are explicit.
