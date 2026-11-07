# SOLID Principle Catalog

## Single Responsibility Principle

A boundary should have one coherent responsibility and one primary reason to change at its abstraction level. The boundary may contain multiple operations when they protect the same invariant or support one capability.

Evidence of risk:

- unrelated stakeholders or policies repeatedly change the same boundary;
- domain rules, orchestration, persistence, transport, and presentation are inseparable;
- tests require unrelated setup or failures propagate across concerns;
- the boundary cannot be described coherently without joining unrelated purposes.

Avoid splitting solely by method count, file length, imports, or naming heuristics. Excessive extraction can replace one understandable unit with a distributed workflow.

## Open/Closed Principle

Isolate a demonstrated and meaningful dimension of variation behind a stable mechanism while allowing ordinary changes to remain direct.

Evidence of risk:

- adding a known variant repeatedly edits central policy and breaks unrelated cases;
- extension requires copying orchestration or modifying many consumers;
- a stable contract exists but implementations are selected through growing conditional logic.

OCP does not mean “never modify existing code.” Do not add registries, factories, strategies, plugins, or inheritance for hypothetical variation.

## Liskov Substitution Principle

Every subtype or implementation must honor the consumer-visible contract of the abstraction.

Check:

- preconditions are not strengthened;
- postconditions and guarantees are not weakened;
- invariants, error semantics, side effects, ordering, and lifecycle remain compatible;
- unsupported operations, nullability, latency, consistency, and resource ownership do not surprise consumers;
- tests written against the abstraction pass for every implementation.

LSP applies to interfaces, protocols, traits, structural types, mocks, adapters, and service implementations—not only class inheritance.

## Interface Segregation Principle

Consumers should depend on coherent contracts tailored to their needs rather than unrelated capabilities.

Evidence of risk:

- implementations contain no-op or unsupported operations;
- consumers mock or import many members they never use;
- one contract changes for unrelated consumer groups;
- permissions or lifecycle differ across subsets of operations.

Do not split interfaces mechanically into one-method fragments. Group operations by consumer role, invariant, transaction, and lifecycle.

## Dependency Inversion Principle

High-level policy should not be controlled by volatile low-level mechanisms. Both should meet at a stable contract owned near the policy/consumer boundary.

Evidence of risk:

- domain or application policy imports database, HTTP, queue, filesystem, framework, or vendor details;
- tests require live infrastructure to exercise policy;
- replacing a mechanism changes high-level rules;
- service locators or globals hide dependencies and lifecycle.

DIP does not require an interface for every class. Direct concrete dependencies are appropriate for stable values, local implementation details, and boundaries without a real substitution or architecture need.
