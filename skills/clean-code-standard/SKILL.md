---
name: clean-code-standard
description: Design, write, refactor, or review readable and maintainable production code across languages, focusing on naming, functions, control flow, side effects, duplication, nullability, resource lifecycle, and conditional use of error-handling, comments, SOLID, patterns, and layered-architecture skills; do not enforce Java-specific rules universally.
---

# Clean Code Standard

Use this skill as the implementation-quality entrypoint for code writing, refactoring, and code review. Clean code communicates approved behavior with the least justified cognitive load; it is not a mandate for short functions, more classes, more interfaces, or named patterns.

## Core rules

- Preserve correctness, contracts, compatibility, security, performance, concurrency, and observability before improving style.
- Follow the target language, paradigm, framework, formatter/linter, and repository conventions unless a concrete defect justifies a local change.
- Prefer clear names, types, data structures, function boundaries, and control flow over explanatory comments.
- Keep abstractions cohesive and at a useful level. Do not optimize for arbitrary line counts, argument counts, or nesting limits without context.
- Make dependencies, mutation, side effects, resource ownership, nullability/absence, failure, cancellation, and lifecycle visible in contracts.
- Remove accidental duplication, dead code, misleading indirection, speculative abstractions, and stale comments; preserve intentional repetition when abstraction would couple unrelated concepts.
- Do not broaden a focused change into an unauthorized architecture rewrite. Route structural concerns to the owning design skill and update approved artifacts before changing architecture.

## Workflow

1. Identify the approved behavior, target language/paradigm, project conventions, affected scope, consumers, and verification baseline.
2. Review names and vocabulary using [references/naming.md](references/naming.md).
3. Review functions, arguments, control flow, state, side effects, duplication, nullability, and resource lifecycle using [references/functions-and-control-flow.md](references/functions-and-control-flow.md).
4. Route only the concerns actually present to the conditional skills below.
5. Make the smallest behavior-preserving improvement that resolves the demonstrated problem.
6. Run formatters, linters, type/static checks, tests, architecture checks, and other project-required verification.
7. Run [references/review-checklist.md](references/review-checklist.md) and report remaining risks or unresolved design decisions.

## Conditional skill routing

- Invoke `error-handling-standard` when failure taxonomy, typed outcomes/exceptions, throw/catch/translation, retries, recovery, or boundary mapping is material. Do not copy Java-specific exception rules into language-neutral code.
- Invoke `code-comments` when public contracts or non-obvious intent, invariants, concurrency, security, compatibility, algorithms, or workarounds still require explanation after the code is clarified.
- Invoke `solid-principles` only when an object/module design has concrete responsibility, substitutability, interface, extensibility, or dependency-direction evidence. Do not review all five principles by ritual.
- Invoke `design-patterns` only when a recurring coupling, variation, construction, state, or coordination problem justifies comparing a named pattern with simpler alternatives.
- Invoke `layered-architecture-standard` when the change affects module/layer responsibilities, dependency direction, ports/adapters, transactions, composition, or architecture test seams.

## Readiness gate

Require the target code or design, approved behavior/acceptance criteria, language and project conventions, and relevant tests or verification commands. If behavior is unclear or a refactor lacks enough characterization evidence, review may continue but do not claim a safe completed refactor. Material architecture or contract changes must return to the owning SD/SDD artifact.

## Lifecycle position

Use this skill primarily in SDD/OpenSpec design refinement, implementation, refactoring, code review, and convergence. System Design should call architecture, error, pattern, and SOLID skills directly rather than treating Clean Code as an architecture standard.

## Expected output

For implementation, produce scoped code and verification evidence. For review, report actionable findings with source locations, concrete impact, minimal correction, conditional-skill rationale, and required verification. Distinguish correctness defects, maintainability risks, and optional style preferences; explicitly recommend no change when the current code is clear and adequate.
