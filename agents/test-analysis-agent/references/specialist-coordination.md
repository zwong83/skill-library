# Test Specialist Coordination

`test-analysis-agent` owns the unified TA artifact. Every executable case receives one test level/specialist classification and one execution owner. Specialists return evidence; they do not rewrite the TA oracle or broaden the approved behavior. Test Analysis, TDD and all nine testing specialists follow seven mandatory steps directly in their own `SKILL.md`; their `AGENTS.md` files are compatibility pointers. Every handoff includes numbered outcomes, with workflow completion separate from the case verdict.

The user independently invokes analysis and each execution specialist. Analysis refines cases using standards without spawning execution agents. No Implementation/SDD parent or testing coordinator is required. Approved direct source/case expectations may replace a formal TA matrix unless the project requires one. Preserve explicit case ownership, stable snapshots and exclusive writes; report adjacent work to the requester rather than dispatching it.

| Specialist | Required preconditions | Primary output |
|---|---|---|
| `bdd-testing-agent` | Approved FRS feature behavior/acceptance for the selected increment, or named equivalent approved criteria if no FRS exists; PRD/design/contracts as supporting context; one owner, actual boundary and mode-appropriate authorization; execution needs target implementation/environment, while specification can precede coding | Traceable Given/When/Then scenarios, authorized test bindings and retained acceptance evidence or optional `bdd-test-report.md`; required unimplemented cases and approved deferred scope recorded separately |
| `unit-testing-agent` | Approved behavior, approved unit cases/oracles, current code/tests, project commands, write authorization when changing tests | Test files plus retained unit results or optional `unit-test-evidence.md` |
| `integration-testing-agent` | Approved boundary, approved integration cases, representative environment/version, data, isolation/cleanup, applicable authorization | Test/config files plus integration boundary evidence or optional `integration-test-evidence.md` |
| `contract-testing-agent` | TA Required decision or equivalent explicit standalone scope/rationale; approved contract/evolution policy, approved contract cases, provider/consumer/version inventory, authoritative contract and verification workflow | `contract-test-report.md` and compatibility verdict |
| `tdd-agent` | implementation authorization, approved selected task, stable case oracle, approved design constraints, current code/tests | Production/test changes plus observed Red-Green-Refactor cycle evidence |
| `ui-testing-agent` | Approved UI states, approved UI cases, supported matrix, environment/data/auth state, visual/accessibility baselines where applicable | `ui-test-report.md` or equivalent UI artifacts and results |
| `system-e2e-testing-agent` | TA Required decision or equivalent explicit standalone scope/rationale; approved critical journey, approved journey cases, deployed component revisions/topology, identities/data, dependencies, observability, cleanup, environment authorization | `system-e2e-test-report.md` and journey verdict |
| `performance-testing-agent` using `performance-testing-standard` | approved execution cases, measurable objectives, workload/data model, target environment, baseline where compared, instrumentation, qualified generator and abort plan, explicit load authorization; plan/review mode does not authorize runs | `performance-test-report.md` and retained raw evidence |
| `security-testing-agent` | Approved threats/controls and security cases, explicit target authorization, permitted techniques, identities/data, rate/stop limits, monitoring and evidence handling | `security-test-report.md` and security verdict |
| `regression-testing-agent` | Base/target revisions, actual diff/impact, approved case plan or equivalent source/case expectations, suite inventory, specialist evidence, environment/data, known failures/flakes | `regression-test-report.md` and unified regression verdict |

## Dedicated testing skills

Each testing specialist applies only its matching standard and relevant supporting references. Approved designs, contracts and other specialists' evidence are inputs, not additional skill invocations. Adjacent work returns to the user; keep active TDD cycles with TDD.

| Agent | Dedicated skill |
|---|---|
| `bdd-testing-agent` | `bdd-testing-standard` |
| `unit-testing-agent` | `unit-testing-standard` |
| `integration-testing-agent` | `integration-testing-standard` |
| `contract-testing-agent` | `contract-testing-standard` |
| `ui-testing-agent` | `ui-testing-standard` |
| `system-e2e-testing-agent` | `system-e2e-testing-standard` |
| `performance-testing-agent` | `performance-testing-standard` |
| `security-testing-agent` | `security-testing-standard` |
| `regression-testing-agent` | `regression-testing-standard` |

## Existing TDD coverage

For BDD, reference one authoritative scenario set by location/version and stable IDs across Test Analysis, implementation and testing. Link cases to its scenarios and existing bindings/tests instead of copying their definitions into a new testing document. Repeated execution produces new run evidence, not new scenario versions. Record source-approved changes or coverage additions centrally and reassess affected tests/results; preserve one writer per shared asset and active TDD ownership.

Testing after implementation starts with the available test inventory and retained evidence. Unit/integration agents are independently invoked for requested reruns, independent verification or gaps; they are not mandatory merely because a TDD task finished. Reuse suitable test assets instead of recreating cases. Reuse observed results only when snapshot, relevant environment/dependencies/configuration, oracle, scope and provenance satisfy current requirements. Explicitly requested execution or required CI/project gates still run. Distinguish reused evidence from new execution, and retain broader integration/regression or specialist checks that focused TDD did not prove.

## Routing rules

- BDD is an acceptance specification/automation approach, not a separate level. Select it for requested BDD work or shared business examples that benefit from executable acceptance. Record the actual underlying level and one owner; link to existing TDD/integration/UI/E2E tests where suitable rather than duplicating them. Keep active TDD cycles with TDD and preserve contract/E2E applicability. Use the [BDD ownership guidance](../../../skills/test-analysis-standard/references/test-level-selection.md#bdd-acceptance-approach-and-ownership); analysis may consult the standard for cases but never dispatches the agent.

- Contract and system/E2E testing are conditional. TA applies the [selection criteria](../../../skills/test-analysis-standard/references/test-level-selection.md#conditional-contract-and-systeme2e-testing) and records `Required` or justified `Not Applicable` for each affected scope. The user selects the relevant execution workflow; honor supplied Required scopes or equivalent standalone assignments and retain justified exclusions. Return unresolved applicability or changed impact as requests for analysis review, without spawning agents.

- Separate logic from UI ownership: unit-testing-agent owns isolated backend/frontend logic; integration-testing-agent owns logic across named real boundaries; ui-testing-agent owns rendered states, DOM/widget interaction, visuals, accessibility and browser/device behavior. A frontend file or unit-test runner alone does not determine ownership. Preserve TDD ownership for active cycles.
- Require each testing specialist to return a scenario checklist for its assigned scope, mapped to approved cases, evidence and explicit gaps/exclusions. New or ambiguous oracles return to TA; neither coverage percentages nor connectivity checks prove all scenarios.
- Assign the lowest trustworthy primary level and add broader cases only for distinct boundary, journey, compatibility, performance, or user-visible risks.
- Every material behavior needs positive coverage. Add negative and boundary cases for every applicable input/state partition; record `Not Applicable` with rationale rather than silently omitting a category.
- A case must contain source/risk IDs, category, preconditions, exact input/action, expected outcome and forbidden effects, environment/data, automation intent, test level/specialist, execution owner, evidence, and an owning task when one is supplied. Initial analysis needs source/risk traceability, not a pre-existing implementation task.
- When TDD is `Required` or activated `Conditional`, set `tdd-agent` as execution owner while retaining Unit or Integration as the test level and governing standard. Do not split its per-cycle tests into separate execution Agents.
- For non-TDD work, assign the appropriate BDD acceptance, unit, integration, contract, UI, system/E2E, performance, or security Agent as execution owner. Use those specialists after TDD only for independent verification or uncovered gaps.
- `regression-testing-agent` independently assesses regression evidence and reports gaps; it does not override a failed specialist result or edit production behavior.

TA is `TA-Ready` only when all material sources and risks map to one or more complete cases, each case has a test level/specialist and one execution owner, required prerequisites are available or planned, and gaps/blockers/residual risks are explicit.
