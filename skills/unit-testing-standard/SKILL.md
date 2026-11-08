---
name: unit-testing-standard
description: Design, write, or review deterministic unit and component tests across languages, including behavior-focused assertions, boundaries, state, side effects, isolation, test doubles, clocks/randomness, concurrency, parameterization, coverage quality, diagnostics, and maintainability; not for real infrastructure integration.
---

# Unit Testing Standard

Use this skill when behavior can be verified within one unit or component without real network, database, broker, cache, filesystem, or external service integration.

## Core rules

1. Test observable behavior, contracts, invariants, state transitions, and side effects rather than private implementation steps.
2. Keep tests deterministic, isolated, order-independent, fast enough for routine execution, and diagnostic on failure.
3. Use real value objects and collaborators when simple; use doubles only at meaningful boundaries or to force hard-to-reach outcomes.
4. Do not mock the subject under test, value types, or every internal call. Overspecified interaction tests obstruct safe refactoring.
5. Control time, randomness, identifiers, locale, scheduling, environment, and global state through explicit seams.
6. Assert returned values, state, emitted effects, collaborator contracts, and absence of forbidden effects as required by the scenario.
7. Implement every TA case assigned to unit/component level. For each assigned behavior cover positive, negative, and boundary partitions where applicable, plus error propagation, duplicate/concurrent behavior, forbidden effects, and resource cleanup; record explicit `Not Applicable` or blocked dispositions instead of silent gaps.
8. Use parameterized/property-based cases when they clarify broad input behavior; keep individual failures understandable.
9. Coverage numbers expose untested code but do not prove meaningful assertions.
10. Follow project test conventions unless they weaken correctness or evidence; never invent a framework API without checking the project.

## Workflow

1. Select traceable TA/OpenSpec scenarios assigned to unit/component level.
2. Identify the behavior boundary, collaborators, inputs, outputs, state, and effects.
3. Choose real collaborators, fakes, stubs, spies, or mocks deliberately.
4. Arrange minimal data, act once on the behavior, and assert the complete oracle.
5. Confirm positive, negative, and boundary completeness for every assigned behavior, then add state/error/duplicate/concurrency cases where applicable without duplicating equivalent coverage.
6. Run focused tests, then the required broader suite and quality checks.
7. Review readability, determinism, diagnostic value, mutation sensitivity where used, and maintenance cost.

## Reference routing

- Read [test-design-and-doubles.md](references/test-design-and-doubles.md) when choosing seams or doubles.
- Read [unit-test-quality-gate.md](references/unit-test-quality-gate.md) when reviewing or handing off tests.
- Invoke `tdd-standard` when implementation must follow Red-Green-Refactor.
- Invoke `integration-testing-standard` when correctness depends on a real adapter, datastore, broker, cache, framework, serialization, or network boundary.

## Output

Return scenario/source IDs, tests added or reviewed, doubles and rationale, commands/results, coverage limitations, flaky or blocked cases, files changed when authorized, and residual risk. Never report tests as passing unless executed.
