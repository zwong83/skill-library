# Functions and Control Flow

## Cohesion and abstraction

- Give each function/module one coherent purpose at its abstraction level. A function may perform several steps when they form one use case or algorithm.
- Extract code when the new boundary names a meaningful concept, isolates change/side effects, reduces duplication, or improves testing. Do not create pass-through functions that only make navigation harder.
- Keep orchestration separate from low-level mechanism when mixing them obscures the normal flow.

## Arguments and dependencies

- Keep required inputs explicit and typed. Reduce argument count when it reflects missing cohesion, not to satisfy a numeric rule.
- Use a parameter object only when the values form a stable concept or evolve together; do not hide unrelated dependencies in a bag of fields.
- Avoid boolean/flag arguments when they select substantially different behavior; prefer separate named operations or a meaningful strategy/state. A simple, obvious toggle may remain.
- Do not mutate input values unexpectedly. Make ownership and mutation explicit according to language conventions.
- Inject or pass external dependencies visibly; avoid service locators and hidden mutable globals.

## Normal flow and control flow

- Make the successful business path easy to follow. Use guard clauses or early returns when they remove nesting without scattering cleanup or invariants.
- Replace deeply nested conditionals with named predicates, tables, state machines, polymorphism, pattern matching, or focused functions only when the alternative is clearer.
- Keep command and query behavior distinct when hidden side effects would surprise callers.
- Do not use exceptions, sentinel values, `null`, or comments as ordinary branching when the language has clearer typed control flow.

## Failures and resource lifecycle

- Avoid magic return codes. Use the target language's idiomatic exceptions, `Result`/`Either`, error values, discriminated unions, or typed outcomes.
- Do not mandate unchecked exceptions outside languages and projects where that choice is appropriate. Java-specific checked/unchecked decisions belong in a language reference or project standard.
- Define the normal flow and failure contract before adding `try/catch/finally`. Catch only when the current boundary can recover, translate, add meaningful context, clean up, or produce the terminal result.
- Preserve the original cause and add safe operation context. Define error types from caller decisions rather than vendor class hierarchies.
- Use language-native deterministic cleanup (`finally`, context managers, `defer`, RAII, `using`, structured concurrency, or equivalents). Cleanup must not silently hide the primary failure.
- Invoke `error-handling-standard` for complete taxonomy, propagation, retry, recovery, and boundary rules.

## Absence and nullability

- Prefer non-null contracts and types that represent absence explicitly, such as `Option`, `Maybe`, `Optional`, nullable unions, or a domain-specific outcome.
- Do not return or pass `null` when it would violate the declared contract or force every caller to guess. Validate untrusted nullable input at the boundary.
- Do not replace every nullable value with an exception; distinguish optional data, not-found, invalid input, and failed operations.
- Avoid null-object implementations unless their behavior is a valid substitutable domain/default behavior rather than a way to hide missing state.

## Duplication, state, and side effects

- Remove duplicated knowledge or policy, not merely similar syntax. Two code blocks that may evolve independently can remain separate.
- Keep state transitions, I/O, persistence, messaging, time, randomness, and external calls visible and testable.
- Minimize mutable shared state; when mutation is required, define ownership, synchronization, atomicity, and lifecycle.
- Avoid clever expressions that compress multiple decisions or side effects into one unreadable statement.

## Verification

Characterize existing behavior before risky refactoring. Test public behavior, invariants, edge cases, failure paths, resource cleanup, concurrency, and compatibility. Use formatter/linter output as evidence of conformance, not as proof of maintainability or correctness.
