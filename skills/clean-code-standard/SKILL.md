---
name: clean-code-standard
description: Write, refactor, or review maintainable code across languages. Use for naming, functions, control flow, comments and API docs, object modeling, design-pattern selection, or SOLID review. Load only the guidance needed for the task.
---

# Clean Code Standard

Use this skill for code writing, refactoring, review, and focused object or module design. Prefer the simplest language-appropriate design that expresses the required behavior and preserves its contracts.

## Core rules

- Preserve correctness, contracts, compatibility, security, performance, concurrency, and observability before improving style.
- Follow the target language, paradigm, framework, formatter/linter, and repository conventions unless a concrete defect justifies a local change.
- Prefer clear names, types, data structures, function boundaries, and control flow over explanatory comments.
- Keep abstractions cohesive and at a useful level. Do not optimize for arbitrary line counts, argument counts, or nesting limits without context.
- Make dependencies, mutation, side effects, resource ownership, nullability/absence, failure, cancellation, and lifecycle visible in contracts.
- Remove accidental duplication, dead code, misleading indirection, speculative abstractions, and stale comments; preserve intentional repetition when abstraction would couple unrelated concepts.
- Do not broaden a focused change into an unauthorized architecture rewrite. Route structural concerns to the owning design skill and update approved artifacts before changing architecture.

## Mandatory workflow

**Follow steps 1 through 7 in order whenever this skill is used.** Record each outcome before moving on. A focused task can make a step brief. Explain any `Not applicable` outcome. Mark a step `Blocked` when a missing requirement or decision prevents completion and stop dependent work. Use [reference routing](#reference-routing) at each step as its questions arise.

1. **Establish behavior.** Confirm the governing requirements, expected behavior, contracts, and consumers. Identify the task mode, affected scope, language and paradigm, repository conventions, and verification baseline. For standalone design consultation with missing authoritative inputs, state material assumptions and label the work exploratory.
2. **Set responsibilities.** Confirm or assign the functions, modules, or objects that own the rules, dependencies, state, and resources. Use object modeling when identity, lifecycle, invariants, or polymorphic collaboration justify it.
3. **Review the design with SOLID where applicable.** Use concrete evidence to identify responsibility, extension, substitution, interface, or dependency problems. Apply only the principles that address those problems. Compare the current design with a minimal correction or a simpler language-native option.
4. **Choose a pattern if needed.** Compare a suitable pattern with the simplest direct approach for a recurring construction, coupling, variation, state, or coordination problem. Record the choice and tradeoffs. If the choice changes responsibilities or contracts, revisit the affected decisions in steps 2 and 3 before proceeding.
5. **Clean up the implementation.** Write or refactor only authorized code. Improve names, types, functions, and control flow, and make errors, nullability, side effects, and resource ownership explicit. Preserve the contracts established above. In design or review, describe the proposed implementation or report the finding with evidence and impact. Record when the current code already meets the requirement.
6. **Write or update comments.** With the implementation or proposed approach clear, document public contracts and remaining non-obvious rationale, invariants, or constraints. Check the documentation against the applicable code paths and remove comments made stale by the change.
7. **Verify and report.** Run project-required checks and the checks relevant to the change, such as formatting, linting, static analysis, behavior tests, or dependency checks. For review, assess available evidence. For design, specify verification and acceptance criteria. Apply the readiness gate and record outcomes, checks run, pending verification, residual risks, and next actions.

## Reference routing

At each step, read and apply only the file or section that answers the current question. Reuse guidance already read. Open another reference only for a separate requirement or finding. A step can have an outcome without opening any reference.

| Step | When guidance is needed | Read |
|---|---|---|
| 1. Behavior | Establish the source of truth and baseline | Use the requirements, contracts, code, and tests relevant to the task. |
| 2. Responsibilities | Identity, values, invariants, state, ownership, lifecycle, or aggregates | [Object modeling](references/object-modeling/object-modeling.md) |
| 2. Responsibilities | Assignment of responsibilities, cohesion, coupling, or object contracts | [Class responsibilities](references/object-modeling/class-responsibilities.md) |
| 2. Responsibilities | Composition, delegation, interfaces, traits, or inheritance | [Composition and inheritance](references/object-modeling/composition-and-inheritance.md) |
| 2. Responsibilities | Structural changes to an existing object model | [Object refactoring](references/object-modeling/refactoring-guide.md) |
| 2. Responsibilities | Translating an object model into the target language | The relevant section of [object design language mapping](references/object-modeling/language-mapping.md) |
| 3. SOLID | Concrete responsibility, extension, substitution, interface, or dependency concern | The relevant principle in the [SOLID catalog](references/solid/principle-catalog.md). Read [limitations](references/solid/limitations.md) when abstraction costs or false positives affect the decision. |
| 3. SOLID | Applying a relevant principle in a specific ecosystem | The applicable guide for [Java/JVM](references/solid/java-jvm.md), [Python](references/solid/python.md), [JavaScript/TypeScript](references/solid/javascript-typescript.md), or [C#](references/solid/csharp.md). Use [SOLID language mapping](references/solid/language-mapping.md) for other languages or paradigm fit. |
| 4. Pattern | Recurring construction, coupling, variation, state, or coordination problem | The applicable section of the [pattern catalog](references/patterns/pattern-catalog.md). Use [pattern language mapping](references/patterns/language-mapping.md) when the target language affects the choice. |
| 5. Implementation | Names, vocabulary, units, or naming conventions | [Naming](references/naming.md) |
| 5. Implementation | Functions, arguments, control flow, side effects, duplication, nullability, or resource lifecycle | [Functions and control flow](references/functions-and-control-flow.md) |
| 6. Comments | Non-obvious intent, invariants, concurrency, security, algorithms, workarounds, or TODOs | The relevant section of [comment types](references/comments/comment-types.md) |
| 6. Comments | Public contracts, docstrings, or generated API documentation | [API docs and docstrings](references/comments/api-docs-and-docstrings.md) |
| 7. Verification | Broad code review or convergence check | [General review checklist](references/review-checklist.md) |
| 7. Verification | Focused comment or documentation review | [Comment review checklist](references/comments/review-checklist.md) |

For a docstring-only change, confirm the public contract in step 1, record steps 2 through 5 as `Not applicable` because the design and implementation are unaffected, load the docstring guidance in step 6, and verify it against the code in step 7 using the applicable documentation checks.

Invoke `exception-error-standard` for material failure taxonomy, typed outcomes, translation, recovery, or error boundaries. Invoke `backend-layered-architecture-standard` for changes to backend module layering, dependencies, ports/adapters, or transaction ownership. Invoke `log-trace-standard` when the task concerns runtime events or spans.

## Readiness gate

Claim completion only after all seven steps have outcomes. Implementation and refactoring require the governing behavior, the target code, and verification appropriate to the change. Review or exploration may continue with stated limits. Material architecture or contract changes belong in the owning SD/SDD artifact. Blocked steps and pending verification prevent a readiness claim when they affect the requested outcome.

## Lifecycle position

In System Design, use the applicable object-modeling, pattern, or SOLID references for material design decisions. In SDD/OpenSpec and implementation, use the relevant references to translate approved decisions into language-appropriate code and verification.

## Expected output

Report the seven workflow outcomes in order and identify the references used where relevant. For implementation, include scoped changes and verification evidence. For design, include the chosen responsibilities or pattern, material alternatives, tradeoffs, and verification. For review, distinguish correctness defects, maintainability risks, and optional preferences. Give actionable findings with locations, impact, minimal corrections, and checks.
