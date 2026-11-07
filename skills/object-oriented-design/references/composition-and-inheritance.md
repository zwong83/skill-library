# Composition, Delegation, and Inheritance

Choose the mechanism that best matches the change boundary and behavioral contract.

## Composition and delegation

Prefer composition or delegation when:

- behavior varies independently from the host object's identity or lifecycle;
- policies must be selected, configured, tested, or replaced;
- multiple behaviors must be combined;
- inheritance would expose protected state or couple subclasses to implementation details;
- the target language favors protocols, traits, functions, modules, or explicit collaborators.

Composition adds collaborators and wiring. Keep ownership, lifetime, failure propagation, and configuration explicit.

## Inheritance

Use inheritance only when:

- the subtype is behaviorally substitutable for the base contract;
- the abstraction is stable and represents a genuine taxonomy or framework extension point;
- preconditions are not strengthened, postconditions are not weakened, and invariants remain valid;
- lifecycle and state semantics are compatible;
- composition or a tagged variant would be less clear.

Avoid inheritance used solely for code reuse, shared fields, convenience access, or framework habit. A subclass that disables methods, throws unsupported errors, requires type checks, or changes base semantics indicates a broken abstraction.

## Interfaces, protocols, and traits

Introduce an abstraction when at least one applies:

- a consumer needs a stable boundary independent of implementation;
- multiple legitimate implementations exist or are expected for a concrete reason;
- an external resource or side effect needs isolation;
- architectural dependency direction requires a port;
- the language's trait/protocol mechanism expresses shared behavior safely.

Do not add abstractions only to satisfy a slogan or mock every concrete type. An abstraction should have a clear consumer and semantic contract.

## Decision record

Record:

- varying dimension and expected change;
- selected mechanism and target-language representation;
- ownership and lifecycle;
- substitutability or composition contract;
- alternatives and trade-offs;
- tests that protect the decision.
