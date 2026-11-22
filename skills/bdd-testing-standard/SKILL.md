---
name: bdd-testing-standard
description: Discover and specify business behavior through concrete Given/When/Then examples, then automate, execute or review acceptance scenarios with traceable evidence; use for BDD without assuming a particular test level or runner.
---

# BDD Testing Standard

## Input and output contract

This summary follows the detailed workflow and linked gates below. Record source owners, locations/versions and decision status; keep unknowns explicit.

- **Required inputs:** Selected scope and approved FRS behavior/acceptance or named equivalent; existing authoritative scenario location/version.
- **Conditional inputs:** Code/bindings/environment/data and permissions for automation/execution; retained results for review; proposals may be drafted pending source decisions.
- **Optional context:** PRD goals, design and prior examples unless decision-critical.
- **Outputs:** One shared scenario set by IDs/version, authorized bindings, separate run evidence and scoped BDD status.
- **Destination and consumer:** Use the workflow's existing, requested or documented default artifact/handoff location. Return results to the invoking agent or user for the identified downstream owner; this does not authorize automatic invocation or duplicate artifacts.
- **Completion:** Apply seven-step gates; BDD-Specified is not BDD-Passed and repeated phases do not create scenario copies.


BDD connects shared business understanding to executable examples. Use it before coding to clarify acceptance behavior or after coding to automate and verify approved scenarios. It complements TDD and does not authorize production implementation. Requirements owners decide behavior; test authors make it observable. Formal OpenSpec, Test Analysis and a specific Gherkin runner are not prerequisites unless required by the project.

## Primary input and scope

Use Product's approved FRS feature behavior and acceptance criteria as the primary oracle. Record the approved version and selected delivery increment, feature/requirement/acceptance IDs, actors, preconditions, actions, business rules, expected outcomes, exceptions and forbidden effects. A list of available feature names cannot establish these expectations. PRD goals/user outcomes and relevant design/API contracts provide supporting context; conflicting or missing expectations return to Product or the owning requirements authority through the requester, rather than being resolved from current code. If no FRS exists, use and explicitly identify equivalent approved acceptance criteria.

Distinguish approved feature scope from implementation availability. Specify scenarios for all selected approved behavior even before coding. Execute against the relevant implemented version and suitable environment; retain required unimplemented cases as pending/unrun or blocked when they cannot be exercised, or failed when an authorized run observes an unmet expectation. Do not fabricate failed runs. Keep approved later-increment features in a separate deferred-scope record; missing implementation alone is not a scope exclusion or Not Applicable decision.

## Mandatory workflow

Maintain one authoritative, versioned scenario set per feature/scope for both implementation guidance and acceptance testing. Select the existing project location: approved FRS scenarios may remain authoritative and link to ordinary tests, or maintained executable feature files may be referenced by the FRS. Record stable scenario IDs, location/version and requirement links. Do not maintain independently edited copies in FRS, implementation plans, Test Analysis and test reports. If another format is generated, identify its source and regeneration process explicitly.

Keep three concerns distinct: scenarios define expected behavior, bindings/fixtures implement the test mechanism, and run evidence records observed results for a revision/environment. Reference the same scenarios from all three. Repeated phases/runs do not require rewriting scenarios; amend them only for approved behavior changes, clarifications or coverage gaps grounded in approved behavior. Preserve IDs where meaning is unchanged, record the source decision/version and reassess affected automation and retained evidence. Framework changes and failing tests do not justify weakening the oracle.

**Complete steps 1 through 7 in order for every assignment**, according to specify, automate, execute or review mode. Record Complete, justified Not Applicable, Blocked with owner/next action, or Pending for each step. Revisit impacted decisions after source, test or environment changes. Planning and review do not imply execution or write permission.

1. **Establish scope and sources.** Identify the approved FRS baseline or named equivalent acceptance source, selected features/delivery increment, rules, affected operations, examples, source versions, requested mode, ownership and applicable permissions. Reconcile supplied specifications/tasks against approved feature behavior rather than assuming a structurally valid specification is complete. Record material omissions, required unimplemented behavior and approved later-increment scope separately. Missing decisions return to Product or the owning requirements authority and block dependent automation, but proposed examples may be drafted and clearly marked unapproved.
2. **Discover concrete examples.** Capture the business rule, representative examples, counterexamples and questions using available business, developer and tester input. Cover relevant valid/invalid paths, limits, roles, states, errors and forbidden side effects. Do not manufacture stakeholder consensus or turn current implementation behavior into the expected result.
3. **Specify behavior precisely.** Locate and reuse the authoritative scenario set before adding or revising justified changes/gaps. Use Given for relevant initial state, When for the business action/event, and Then for observable outcomes and forbidden effects. Prefer one behavior per scenario, domain language over click scripts, exact values where material, and stable source/scenario IDs. Use Scenario Outline examples for distinct meaningful partitions, with each row reported separately; keep Background short and free of hidden dependencies. Record approval and open decisions before treating examples as executable acceptance oracles; hand off references to the same set for implementation and testing.
4. **Choose the boundary and reuse strategy.** Record the actual test level and one owner per executable case. Prefer existing tests, fixtures and bindings over duplicate checks. Choose the smallest boundary that proves the rule: mocks can prove local logic but not durable, transport or assembled-system effects. API is an interface, not automatically integration/E2E proof. Keep active TDD cycles with TDD, preserve supplied contract/E2E applicability and assign broader coverage only for distinct risks. BDD scenarios never replace separately required security, performance, UI or compatibility evidence by naming alone.
5. **Prepare executable examples within scope.** Follow the project's established runner and conventions; do not mandate a new framework solely for BDD. For authorized automation create test bindings/fixtures that call the selected system boundary and assert real outcomes. Avoid no-op, always-pass or pending bindings, broad ambiguous expressions and assertions that merely restate mocked responses. Control data, identities, time, asynchronous waits, isolation and cleanup. Scenario order must not determine results. Specification/review mode records or inspects this design without assuming writes or environment use.
6. **Execute or inspect retained evidence.** Run authorized selected scenarios with explicit code/test versions, environment/configuration and commands, or review supplied evidence for those conditions. Report every scenario/example row, undefined/ambiguous steps, failures, skips, pending cases and flakes. Parsing and dry runs validate syntax/bindings only. Preserve original failures; correct test defects within authorization and rerun affected cases. Report production defects and unresolved rules to the requester without changing production behavior. Reuse prior results only when provenance, scope, oracle and relevant revisions/conditions remain suitable; requested or project-required runs still execute.
7. **Reconcile coverage and report.** Map approved behavior to scenarios, underlying tests and observed results. Separate scenario approval, automation readiness and execution success. Return BDD-Specified only for a complete approved specification, BDD-Passed only with adequate passing evidence for every required assigned check, BDD-Failed for known required failures, or BDD-Blocked for unresolved required decisions/evidence without a known failure. Keep concurrent blockers visible. Record exclusions, untested risks, next owners and all seven outcomes; do not claim business sign-off or release approval.

## Evidence contract

Retain source/scenario/case IDs, source approval/version, exact examples and forbidden effects, underlying level/boundary, execution owner, automation asset locations, changed files, data/cleanup plan, code/test/environment versions, commands/results, per-example dispositions, raw evidence references, reused evidence rationale, gaps and residual risk. Existing CI reports and feature files are sufficient when traceable; a separate report is optional.

Show FRS feature/acceptance-to-scenario-to-test links or the explicitly named equivalent source. Record selected delivery scope, implementation/execution readiness, required unimplemented cases and approved deferred features separately so coverage cannot shrink to only what currently works.

Reports reference the authoritative scenario location/version and IDs, binding/test asset versions and per-run results. Retained run snapshots may preserve historical inputs for reproducibility, but are evidence, not another editable scenario source. Existing TDD/unit/integration tests can support scenario coverage through traceability without copying each scenario into another suite; report the actual boundary each test proves.

Executable Gherkin is optional; Given/When/Then in Markdown may be a specification linked to ordinary automated tests. Report that mapping honestly instead of claiming the Markdown executes. An unavailable environment is Blocked for required execution, not Not Applicable. A passing scenario using doubles supports only its actual isolation boundary.

## Focused reference

Use [scenario and evidence example](references/scenario-and-evidence.md) when choosing scenario granularity, partitions or traceability fields. This standard does not invoke other skills or agents; return adjacent work to the requester.
