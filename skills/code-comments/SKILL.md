---
name: code-comments
description: Write or review maintainable code comments, docstrings, and API documentation across programming languages. Use when intent, contracts, invariants, algorithms, concurrency, security, compatibility, or workarounds are not clear from code alone; do not narrate obvious code or preserve stale and commented-out implementations.
---

# Code Comments

Use this skill to explain information that cannot be expressed clearly enough through names, types, structure, tests, and design artifacts. Comments are part of the maintained code contract and must change with the code they describe.

## When to comment

- public API behavior, parameters, return values, errors, side effects, lifecycle, compatibility, or examples need documentation;
- a business rule, invariant, security control, concurrency requirement, unit, protocol, or data-format constraint is non-obvious;
- the code uses an intentional workaround, surprising order, performance trade-off, approximation, algorithm, or external-system limitation;
- a regex, bit operation, numerical method, state transition, or generated/unsafe boundary needs rationale;
- an actionable TODO/FIXME records approved incomplete work that cannot be resolved in the current scope.

Do not comment obvious assignments, loops, branches, getters/setters, or syntax. First improve names, types, function boundaries, and control flow; add a comment only for remaining intent or constraint.

## Workflow

1. Identify the reader and the question the comment must answer.
2. Decide whether code, naming, types, tests, ADR/SDD, or API documentation is the better location.
3. Write the smallest accurate explanation of why, contract, invariant, risk, or non-obvious mechanism.
4. Place it at the boundary it governs and use the language's standard doc-comment/docstring format.
5. Link to a stable issue, specification, protocol, or decision when the external source matters; do not copy a long document into code.
6. Verify the comment against all code paths, failure behavior, units, concurrency, and current implementation.
7. Remove stale, redundant, misleading, historical, or commented-out code.

## Reference routing

- Read [references/comment-types.md](references/comment-types.md) for intent, invariant, algorithm, workaround, security, concurrency, and TODO comments.
- Read [references/api-docs-and-docstrings.md](references/api-docs-and-docstrings.md) for public contracts and language-native documentation.
- Read [references/review-checklist.md](references/review-checklist.md) during code review or SDD convergence.

## Core rules

- Explain **why**, **contract**, **constraint**, or **risk**; let code express ordinary **what** and **how**.
- Keep comments local to the behavior they govern, except public contracts that belong at API/type/module boundaries.
- State units, ranges, ordering, thread-safety, ownership, mutation, nullability, error, and lifecycle semantics when they are not enforced by the type system.
- Describe rationale and trade-offs without blaming people or preserving temporary history that belongs in version control.
- Never include secrets, credentials, private incident details, personal data, or internal-only sensitive values.
- Do not use comments to disable code. Delete dead code and rely on version control.
- TODO/FIXME must be actionable: state the missing outcome, trigger/constraint, and stable issue/reference or owner according to project convention. Do not use it to hide required work while marking a task complete.
- Keep generated-code comments in the generator/template; do not hand-edit generated outputs unless the project explicitly permits it.
- Update or remove comments in the same change that invalidates them.

## Relationship to design and code quality

- Use `object-oriented-design`, `solid-principles`, or `design-patterns` for structural design decisions; comments should explain the resulting non-obvious contract, not replace the design.
- Use `logging-standard` for runtime diagnostic events. A comment is not runtime evidence, and a log message is not source documentation.
- Use project coding/documentation standards for language-specific tags, formatting, generated docs, and lint rules.

## Expected output

When writing comments, produce only the necessary language-native comment/docstring with enough surrounding context to place it correctly. When reviewing, report stale, missing, misleading, redundant, sensitive, or non-actionable comments with the affected location, reader impact, and a suggested correction. Explicitly recommend no new comment when clearer code is the better fix.
