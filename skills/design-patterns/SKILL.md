---
name: design-patterns
description: Select, explain, compare, or review reusable software design patterns across programming languages and paradigms. Use when a design problem involves coupling, variation, object creation, coordination, state, extensibility, or refactoring; do not force a pattern when simpler code is clearer.
---

# Design Patterns

Use this skill as a language-neutral decision aid for software design. A pattern is a named, reusable response to a recurring design problem—not a requirement to add abstractions. Start from the problem, constraints, and desired change boundary; select an idiom appropriate to the target language and runtime.

## Scope and boundaries

This skill applies to:

- choosing, comparing, explaining, or reviewing design patterns;
- reducing coupling or isolating a dimension that is expected to vary;
- designing extensible components, workflows, stateful behavior, or coordination;
- refactoring rigid conditionals, subclass growth, duplicated algorithms, or integration seams;
- recording pattern-related decisions in System Design, SDD, ADR, or code-review artifacts.

Do not invoke a pattern merely because it has a familiar name. Prefer direct code, a small function, a data table, a module, or a language-native construct when it communicates the design more clearly.

## Required decision workflow

1. **State the concrete problem.** Identify the coupling, variation, lifecycle, coordination, or construction problem and the change that should become easier.
2. **Capture constraints.** Consider language, paradigm, runtime, concurrency model, performance, memory, failure behavior, testability, team conventions, and operational boundaries.
3. **Compare alternatives.** At minimum compare a simple direct implementation with the candidate pattern. Include a language-native alternative when one exists.
4. **Select by intent, not by class diagram.** Explain why the pattern fits, why nearby patterns do not, and what complexity it introduces.
5. **Map to the target language.** Use interfaces, functions, closures, modules, traits, protocols, algebraic data types, message passing, or other idioms as appropriate. Do not mechanically translate an object-oriented hierarchy into every language.
6. **Define roles and boundaries.** Name participants, ownership, collaboration, lifecycle, error behavior, synchronization, and extension points in the vocabulary of the target language.
7. **Record trade-offs and verification.** Document benefits, costs, failure modes, migration impact, test strategy, observability needs, and a removal or simplification trigger when useful.

## Pattern catalog

The catalog is organized by intent. Read [references/pattern-catalog.md](references/pattern-catalog.md) when a detailed comparison or pattern review is needed.

| Intent | Patterns | Typical problem |
|---|---|---|
| Creation | Builder, Factory Method, Abstract Factory, Prototype, Singleton | Keep construction, variants, copying, or lifecycle policy separate from use |
| Structure | Adapter, Bridge, Composite, Decorator, Facade, Flyweight, Proxy | Compose responsibilities, isolate interfaces, or control access |
| Behavior | Chain of Responsibility, Command, Iterator, Mediator, Memento, Observer, State, Strategy, Template Method, Visitor | Vary algorithms, coordinate collaborators, model state, or separate operations |

The GoF names are useful vocabulary, not an exhaustive taxonomy. Pipelines, dependency injection, repository, unit of work, event-driven, actor, functional, reactive, and distributed-system patterns may be more appropriate depending on the problem. Label non-GoF patterns accurately and do not imply that a GoF pattern is required.

## Language and paradigm mapping

Read [references/language-mapping.md](references/language-mapping.md) when the target language or paradigm is known, when a Java-centric solution would be misleading, or when translating a pattern across ecosystems.

General mapping rules:

- **Class-oriented languages:** interfaces, composition, delegation, inheritance, modules, and dependency injection may express the roles.
- **Python:** protocols/duck typing, callables, decorators, generators, context managers, dataclasses, and modules may be clearer than class hierarchies.
- **JavaScript/TypeScript:** functions, closures, modules, middleware, event emitters, promises, discriminated unions, and structural typing are often the natural representation.
- **Go:** small interfaces, composition, function values, explicit constructors, channels, and context propagation usually matter more than inheritance-style patterns.
- **C#:** interfaces, delegates, events, records, dependency injection, async streams, and pattern matching can express the same intent.
- **Rust:** traits, enums, ownership/borrowing, iterators, closures, `Result`/`Option`, and channels often make the design safer and more explicit.
- **Functional or data-oriented systems:** higher-order functions, immutable data, algebraic data types, folds, pipelines, and explicit state transitions may replace several classic OO patterns.
- **Concurrent or distributed systems:** message passing, actors, queues, sagas, idempotency, circuit breakers, and retry/bulkhead policies are architectural choices; do not describe them as GoF patterns without qualification.

## Evaluation checklist

For each proposed pattern, answer:

- What problem and expected change does it address?
- What is the simplest non-pattern alternative?
- Which dimension varies, and where is that variation isolated?
- What are the participants, ownership, lifecycle, and dependency direction?
- How are errors, cancellation, retries, timeouts, ordering, and concurrency handled?
- What are the costs in indirection, cognitive load, allocation, latency, memory, and debugging?
- How will the design be unit-tested, integration-tested, observed, and evolved?
- What would indicate that the pattern should be removed or replaced?

## Common failure modes

- **Pattern cargo cult:** adding a named pattern without a concrete problem.
- **Premature abstraction:** designing extension points before a real variation or second implementation exists.
- **Mechanical translation:** copying Java/Spring class structures into a language with better native constructs.
- **Global-state disguise:** using Singleton or service locators to hide dependencies and complicate tests.
- **Overloaded coordinator:** turning Mediator, Facade, or an orchestration service into a second business-logic monolith.
- **Inheritance trap:** using Template Method or subclassing where composition, functions, traits, or data-driven rules are safer.
- **Unbounded event coupling:** using Observer or event buses without ownership, delivery, ordering, failure, and lifecycle rules.

## Expected output

When this skill is used, produce a concise pattern decision that includes:

1. Problem and constraints.
2. Selected pattern or explicit decision to use no pattern.
3. Target-language representation and participant responsibilities.
4. Alternatives considered and trade-offs.
5. Error, concurrency, testability, and operational implications when relevant.
6. Traceability to the requirement, System Analysis flow, System Design decision, ADR, or code location that motivated it.

Use language-neutral pseudocode in the core explanation. Load a language-specific reference or consult the project’s coding standards before giving production-level code.
