# OOD Language and Paradigm Mapping

Translate object-model intent into native constructs. Do not mechanically reproduce Java-style classes and interfaces.

## Java and JVM languages

Use classes, interfaces, records/data classes, sealed types, enums, lambdas, modules, and framework boundaries according to the language. Prefer constructor-visible dependencies and explicit lifecycle scopes. Kotlin and Scala may express values, variants, and behavior through data classes, sealed hierarchies, extension functions, traits, and functional constructs rather than Java-style boilerplate.

## C#

Use classes, interfaces, records, structs, delegates, events, pattern matching, async streams, dependency injection, and deterministic disposal. Include cancellation, nullability, ownership, and disposal in contracts.

## Python

Use modules, classes, dataclasses, protocols, abstract base classes, callables, properties, context managers, and duck typing according to actual needs. Avoid nominal interfaces and elaborate hierarchies when a small protocol or function is clearer. Define mutability and resource lifetime explicitly.

## JavaScript and TypeScript

Use modules, functions, closures, objects, classes, interfaces, structural types, discriminated unions, promises, and async iterators. Favor discriminated unions for closed variants and functions for stateless behavior. Account for runtime validation because TypeScript types do not exist at runtime.

## Go

Go is composition-oriented rather than class-inheritance-oriented. Use packages, structs, small consumer-owned interfaces, embedding, function values, explicit constructors, contexts, and channels. Do not introduce Java-style interface layers or getters/setters without a concrete boundary need.

## Rust

Use structs, enums, traits, generics, modules, ownership/borrowing, iterators, closures, and message passing. Enums often model closed state or variant behavior better than trait-object hierarchies. Treat ownership and mutation as primary design constraints.

## Functional and data-oriented systems

Use immutable records, algebraic data types, pure functions, reducers, folds, pipelines, explicit state transitions, and data locality when those fit better. OOD skills may still help identify boundaries and invariants, but do not convert them into object graphs unnecessarily.

## Unknown languages

First determine the language's type system, module system, mutation model, error model, resource ownership, concurrency model, and established project idioms. Preserve the design intent while choosing the smallest native representation.
