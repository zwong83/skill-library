---
name: unit-testing-standard
description: Design, write, or review deterministic application-logic unit tests across backend and frontend languages, including behavior-focused assertions, boundaries, state, side effects, isolation, test doubles, clocks/randomness, concurrency, parameterization, coverage quality, diagnostics, and maintainability; not for real infrastructure integration.
---

# Unit Testing Standard

## Input and output contract

This summary follows the detailed workflow and linked gates below. Record source owners, locations/versions and decision status; keep unknowns explicit.

- **Required inputs:** Approved isolated logic cases/oracles, code/test scope and project conventions.
- **Conditional inputs:** Tooling and write/run authorization for implementation/execution; original commands/results for review.
- **Optional context:** Fixtures, coverage/mutation history and known flakes.
- **Outputs:** Unit tests or findings, scenario mapping, isolation choices, commands/results and coverage limits.
- **Destination and consumer:** Use the workflow's existing, requested or documented default artifact/handoff location. Return results to the invoking agent or user for the identified downstream owner; this does not authorize automatic invocation or duplicate artifacts.
- **Completion:** Preserve deterministic isolated proof; incomplete or unrun cases cannot count as passed.


Use this skill for isolated logic such as business rules, calculations, validation, transformations, decisions, state transitions and non-rendered modules, without real network, database, broker, cache, filesystem or external service integration. Frontend logic can be tested directly; rendering, DOM/widget interaction, visual and accessibility assertions belong to `ui-testing-standard`. UI specialists may reuse isolation and doubles techniques here without transferring UI case ownership.

## Core rules

1. Test observable behavior, contracts, invariants, state transitions, and side effects rather than private implementation steps.
2. Keep tests deterministic, isolated, order-independent, fast enough for routine execution, and diagnostic on failure.
3. Use real value objects and collaborators when simple; use doubles only at meaningful boundaries or to force hard-to-reach outcomes.
4. Do not mock the subject under test, value types, or every internal call. Overspecified interaction tests obstruct safe refactoring.
5. Control time, randomness, identifiers, locale, scheduling, environment, and global state through explicit seams.
6. Assert returned values, state, emitted effects, collaborator contracts, and absence of forbidden effects as required by the scenario.
7. Implement every approved source/test case assigned to logic unit level. For each assigned behavior cover positive, negative, and boundary partitions where applicable, plus error propagation, duplicate/concurrent behavior, forbidden effects, and resource cleanup; record explicit `Not Applicable` or blocked dispositions instead of silent gaps.
8. Use parameterized/property-based cases when they clarify broad input behavior; keep individual failures understandable.
9. Coverage numbers expose untested code but do not prove meaningful assertions.
10. Follow project test conventions unless they weaken correctness or evidence; never invent a framework API without checking the project.

## Existing tests and TDD evidence

Start by mapping assigned cases to existing tests, including TDD tests. Reuse suitable test assets; add or extend tests only for uncovered behavior or distinct risks. Assign a new run when requested, required by a project/CI gate, or needed because code/test revisions, dependencies, configuration, environment, data or the coverage scope changed. Preserve active TDD-cycle ownership.

In a review or evidence-reuse assignment, accept retained results only when their exact code/test snapshot, relevant environment/configuration/dependencies, case oracles, scope and provenance satisfy the current verification requirement. Record the evidence reference and reuse rationale; do not describe it as a new run. Missing, stale, flaky or insufficient evidence remains a gap and requires an appropriate check, not a pass. Focused TDD results do not automatically prove broader integration, regression or other specialist coverage. Reusing test files does not imply that their earlier results remain valid.

## Workflow

1. Select traceable approved source scenarios (including supplied TA/OpenSpec cases) assigned to logic unit level.
2. Identify the behavior boundary, collaborators, inputs, outputs, state, and effects.
3. Choose real collaborators, fakes, stubs, spies, or mocks deliberately.
4. Arrange minimal data, act once on the behavior, and assert the complete oracle.
5. Reconcile a scenario checklist against every assigned rule and decision: positive/negative/boundary inputs, empty/null/missing values, decision combinations, state transitions, errors, duplicate/concurrent calls, cleanup and forbidden effects where applicable. Use decision tables, equivalence partitions or property-based tests for large spaces. Record exclusions and return missing cases/oracles to the requester for analysis clarification; coverage percentages do not prove all scenarios or exhaustive combinations.
6. Run requested/required focused tests and affected broader checks in execution mode. For evidence review, assess retained results against the reuse criteria and report remaining checks without implying a new run.
7. Review readability, determinism, diagnostic value, mutation sensitivity where used, and maintenance cost.

## Reference routing

- Read [test-design-and-doubles.md](references/test-design-and-doubles.md) when choosing seams or doubles.
- Read [unit-test-quality-gate.md](references/unit-test-quality-gate.md) when reviewing or handing off tests.
- Invoke `tdd-standard` when implementation must follow Red-Green-Refactor.
- Invoke `integration-testing-standard` when correctness depends on a real adapter, datastore, broker, cache, framework, serialization, or network boundary.

## Output

Return scenario/source IDs, tests added or reviewed, doubles and rationale, commands/results, coverage limitations, flaky or blocked cases, files changed when authorized, and residual risk. Never report tests as passing unless executed.
