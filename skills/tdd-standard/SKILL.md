---
name: tdd-standard
description: Implement approved software behavior through disciplined Red-Green-Refactor cycles, selecting unit or integration tests from traceable scenarios, proving each test fails for the intended reason before minimal implementation, and preserving clean design and evidence; not for unresolved requirements or post-hoc test decoration.
---

# TDD Standard

Use this skill only after expected behavior and its test oracle are resolved and implementation is authorized. TDD is an implementation workflow, not a substitute for requirements, System Design, or Test Analysis.

## Core rules

1. Shape one small observable behavior from an approved scenario before each cycle.
2. Red: add one test and observe it fail for the intended missing behavior, not compilation/setup/environment noise unless that is the intended boundary.
3. Green: write the simplest production change that satisfies the new behavior while preserving existing tests and approved design.
4. Refactor: improve names, duplication, structure, seams, and comments while all relevant tests remain green; do not add behavior during refactor.
5. Record the Red evidence. A test first seen passing does not prove it could detect the missing behavior.
6. Prefer fast unit/component cycles. Use an integration test to drive behavior only when the real boundary semantics are the risk.
7. Do not over-mock internal implementation or design abstractions solely to satisfy a test.
8. Keep each cycle traceable to TA/OpenSpec/source IDs and an implementation task.
9. Run the focused test every cycle and broader affected suites at safe checkpoints.
10. Stop when behavior is ambiguous, the test cannot express a stable oracle, or implementation requires a material design change.

## Workflow

1. Select one approved task and its TA/OpenSpec scenario.
2. Choose unit/component or integration level using the risk and boundary.
3. Write the smallest meaningful failing test and capture the expected failure.
4. Implement minimal code until the focused test passes.
5. Run affected tests; refactor under green.
6. Repeat for the next behavior, including material negative and edge cases.
7. Run required format/static/build/unit/integration checks and record evidence.
8. Mark the task complete only when behavior, code quality, tests, and evidence are complete.

## Reference routing

- Read [red-green-refactor.md](references/red-green-refactor.md) for cycle discipline and evidence.
- Read [legacy-and-integration-tdd.md](references/legacy-and-integration-tdd.md) for characterization, seams, and boundary-driven TDD.
- Invoke `unit-testing-standard` for unit/component cycle design.
- Invoke `integration-testing-standard` only when the selected behavior depends on a real integration boundary.
- Invoke `clean-code-standard` during Green/Refactor and its conditional Skills only when their concern is present.

## Boundary

TDD authorization does not authorize upstream behavior/design changes, unrelated refactoring, Git operations, deployment, migrations against live systems, or external mutation. Spikes may explore uncertainty, but discard or separately review spike code before restarting with a failing test.

## Output

Return task and scenario IDs, cycle summary, Red failure evidence, production/test files changed, unit/integration routing, commands/results, refactors, deviations, blockers, and remaining risk. Never claim TDD when tests were added only after implementation without observed Red evidence.
