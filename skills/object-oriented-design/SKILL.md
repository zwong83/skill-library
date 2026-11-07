---
name: object-oriented-design
description: Model, review, or refactor object-oriented and hybrid software designs when identity, encapsulated mutable state, lifecycle, invariants, aggregate boundaries, or polymorphic object collaboration is central. Do not force OOP onto functional, data-oriented, or language-native designs.
---

# Object-Oriented Design

Use this skill to turn approved behavior and system boundaries into a coherent object model. OOP is one implementation paradigm, not a universal default. First confirm that the target language, codebase, and problem benefit from objects with identity, state, behavior, lifecycle, or polymorphic contracts.

## When to use

- defining or reviewing domain objects, services, modules, classes, interfaces, protocols, or traits;
- assigning responsibilities and invariants to object boundaries;
- modeling identity, value semantics, ownership, lifecycle, associations, aggregates, and state transitions;
- deciding between composition, delegation, inheritance, polymorphism, and data-oriented alternatives;
- refining a System Design or OpenSpec design delta into implementation-level object collaborations;
- refactoring an object model with excessive coupling, poor cohesion, anemic objects, god objects, or unsafe inheritance.

Do not use this skill merely because the implementation language supports classes. Prefer functions, modules, immutable data, algebraic data types, tables, pipelines, or message passing when they express the problem more directly.

## Required workflow

1. **Confirm paradigm fit.** Identify why identity, encapsulated state, lifecycle, or polymorphic behavior makes an object model useful.
2. **Establish source behavior.** Read the approved requirements, SA flows/states, SD boundaries, contracts, and constraints. Do not invent domain rules.
3. **Discover concepts and invariants.** Separate entities, values, policies, services, adapters, resources, and messages by semantics rather than nouns alone.
4. **Assign responsibilities.** Place behavior with the information and invariant it protects; keep orchestration distinct from domain rules and infrastructure.
5. **Define relationships.** Specify ownership, cardinality, direction, lifecycle, mutation, consistency, and dependency boundaries.
6. **Choose collaboration mechanisms.** Compare direct calls, composition, delegation, protocols/interfaces, inheritance, events, messages, and language-native alternatives.
7. **Define contracts.** State preconditions, postconditions, invariants, errors, state transitions, concurrency, cancellation, and resource lifetime where relevant.
8. **Review quality.** Invoke `solid-principles` conditionally for an OO design-quality review. Invoke `design-patterns` only when a recurring design problem justifies a named pattern.
9. **Map to the target language.** Load [references/language-mapping.md](references/language-mapping.md) and follow project coding standards before producing language-specific code.
10. **Trace and verify.** Map objects and collaborations to source requirements, design decisions, tasks, and tests.

For formal lifecycle delivery, missing mandatory upstream requirements, SA, or SD must block an approved or implementation-ready OOD conclusion. For independent consultation or Explore mode, continue from user-provided scenarios only when clearly labeled as exploratory; list assumptions, unknowns, and rules that cannot be verified, and do not claim lifecycle approval.

## Reference routing

- Read [references/object-modeling.md](references/object-modeling.md) when identifying entities, values, services, invariants, state, or relationships.
- Read [references/class-responsibilities.md](references/class-responsibilities.md) when assigning behavior, defining boundaries, or reviewing cohesion and coupling.
- Read [references/composition-and-inheritance.md](references/composition-and-inheritance.md) when choosing composition, delegation, interfaces, traits, or inheritance.
- Read [references/language-mapping.md](references/language-mapping.md) before translating the design into a specific ecosystem.
- Read [references/refactoring-guide.md](references/refactoring-guide.md) when improving an existing object model rather than designing a new one.

## Lifecycle placement

### System Design

Use OOD at a high level for domain concepts, component/module responsibilities, major interfaces, dependency direction, ownership, and important class or object diagrams. Keep production code and incidental implementation detail out of System Design.

### SDD / OpenSpec design

Use OOD in detail for class/interface/protocol responsibilities, object collaboration, lifecycle, state, dependency injection, error behavior, concurrency, pattern roles, and test seams. Treat this as a design delta to the approved SD, not a replacement architecture.

### Implementation and review

Translate the approved design using the target language's native constructs. During review, evaluate whether the code preserves responsibilities, invariants, contracts, ownership, and traceability; do not judge quality by class count or pattern count.

## Design rules

- Prefer high cohesion and explicit dependency direction over arbitrary “small classes.”
- Encapsulate invariants, not merely fields; avoid getters/setters that expose uncontrolled mutation.
- Distinguish entities with identity from immutable values with structural equality.
- Make ownership and lifecycle explicit, especially for mutable state, resources, subscriptions, and concurrent collaborators.
- Prefer composition and delegation for independently varying behavior. Use inheritance only for a genuine substitutable relationship with a stable contract.
- Define interfaces at consumer boundaries when possible; do not create an interface for every class without a testing, substitution, ownership, or architectural reason.
- Keep domain policy independent from storage, transport, framework, and vendor details unless the approved design requires otherwise.
- Do not confuse dependency injection with Dependency Inversion; wiring is a mechanism, while dependency direction is the design property.
- Use diagrams to clarify relationships and collaborations, but keep contracts, invariants, decisions, and exceptions in authoritative text.

## Expected output

Produce only the detail needed by the requested lifecycle stage. A complete OOD decision should include:

1. paradigm-fit statement and source traceability;
2. object/module catalog with responsibilities and ownership;
3. identities, values, invariants, states, and lifecycle rules;
4. relationships, dependency direction, and collaboration flows;
5. public contracts and error/concurrency behavior where relevant;
6. composition/inheritance and extension decisions with rationale;
7. conditional SOLID and design-pattern findings;
8. language mapping, alternatives, trade-offs, risks, and verification strategy.

Use language-neutral modeling or pseudocode until the target language and project conventions are known.
