# Language and Paradigm Mapping

Use this reference after identifying the target language, runtime, and project conventions. The mapping is about design intent; it is not a prescription to use every construct listed.

## Class-oriented languages

Interfaces, abstract types, composition, delegation, inheritance, modules, constructors, and dependency injection can express pattern roles. Prefer composition when a behavior varies independently. Make ownership, mutability, lifecycle, and error behavior explicit rather than relying on a class diagram.

## Java and JVM languages

Interfaces, records/data classes, sealed types, lambdas, modules, dependency injection, streams, and explicit lifecycle scopes may express pattern intent. Spring or another framework can provide wiring, but framework annotations must not replace clear ownership, contracts, failure behavior, or tests. Apply the same guidance to Kotlin, Scala, and other JVM languages using their native idioms.

## Python

- Protocols or duck typing may replace nominal interfaces.
- Functions, callables, closures, decorators, and `functools` may express Strategy, Decorator, Command, or Factory roles without wrapper classes.
- Generators and iterators can express lazy traversal; context managers can express resource lifecycle and scoped behavior.
- Dataclasses and explicit factory functions often suffice for Builder-like construction.
- Modules and dependency injection are usually safer than Singleton or service-locator globals.

## JavaScript and TypeScript

- Functions, closures, modules, middleware, and higher-order functions often express Strategy, Decorator, Chain, and Factory roles.
- Event emitters, observables, queues, and async iterators need explicit delivery, cancellation, error, and listener-lifecycle rules.
- TypeScript interfaces, discriminated unions, and exhaustive `switch` logic can model variants and State without deep inheritance.
- Promise composition and pipeline functions may be clearer than Template Method hierarchies.

## Go

- Small interfaces, composition, function values, explicit constructors, and package boundaries are the usual extension mechanisms.
- A map of handlers or function values may be a better Strategy/Factory representation than a class hierarchy.
- Channels, contexts, and worker pipelines are concurrency tools; define ownership, cancellation, backpressure, and shutdown behavior.
- Avoid interfaces that exist only to imitate another language’s abstractions; define them at the consumer boundary.

## C#

- Interfaces, delegates, events, records, pattern matching, dependency injection, async streams, and immutable values can express common pattern intents.
- Use `IEnumerable`/iterators and `IAsyncEnumerable` for traversal where appropriate.
- Make cancellation tokens, async failure, event subscription, and disposal part of the design contract.

## Rust

- Traits, enums, pattern matching, iterators, closures, and generic bounds often replace classic inheritance patterns.
- `Result` and `Option` make error and absence behavior explicit; include them in the contract rather than hiding failures behind proxies or callbacks.
- Ownership and borrowing determine lifecycle and sharing. Use `Arc`, locks, channels, or interior mutability only when the ownership model requires them.
- Enums and explicit transitions often model State more safely than a family of mutable state objects.

## Functional and data-oriented styles

Higher-order functions, immutable data, algebraic data types, folds, pipelines, reducers, and explicit state transitions can collapse several GoF patterns into simpler transformations. Prefer data and functions when the problem is primarily computation; use objects when identity, lifecycle, encapsulation, or resource ownership is central.

## Concurrent and distributed systems

Message passing, actors, queues, event streams, sagas, circuit breakers, bulkheads, idempotency keys, and retry policies are architecture or reliability patterns rather than direct GoF equivalents. Specify delivery guarantees, ordering, duplication, timeout, cancellation, backpressure, persistence, and observability.

## Other languages

When a language is not listed, identify its native abstraction model, module system, type system, ownership/mutation rules, error model, and concurrency model before choosing a representation. Preserve the design intent and use the project’s established idioms instead of forcing a class hierarchy.

## Translation rule

Translate the **intent** and the **change boundary**, not the source language’s syntax or inheritance structure. Before recommending a pattern, inspect the project’s existing idioms and coding standards, and explain why the chosen representation is native to the target ecosystem.
