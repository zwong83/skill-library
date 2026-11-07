---
name: solid-principles
description: Review or improve object-oriented and modular designs using language-neutral SOLID principles. Use for responsibility, extensibility, behavioral subtyping, consumer-specific interfaces, dependency direction, and design-focused refactoring; do not apply SOLID mechanically or force class abstractions onto non-OO code.
---

# SOLID Principles

Use SOLID as a design-review lens, not a scorecard or mandate to create more classes and interfaces. Evaluate concrete change pressure, contracts, consumers, dependency direction, and target-language idioms before recommending a refactor.

## When to use

- reviewing object, class, module, protocol, trait, or service design;
- investigating mixed responsibilities, rigid extension points, broken substitutability, oversized interfaces, or inverted dependency direction;
- refining OOD in System Design or SDD/OpenSpec design artifacts;
- reviewing or refactoring implementation code while preserving approved behavior;
- explaining a SOLID trade-off or comparing a simpler alternative.

Do not use SOLID as a general formatting, style, architecture, or functional-programming checklist. A design can be good without an interface per class, dependency injection everywhere, or extension points for hypothetical changes.

## Review workflow

1. Establish the approved behavior, design boundary, target language, consumers, and expected change drivers.
2. Identify concrete evidence: a difficult change, defect, unsafe contract, dependency cycle, test burden, or repeated modification.
3. Evaluate the relevant principle; do not review all five by ritual when only one is implicated.
4. Compare the current design, a minimal correction, and a language-native alternative.
5. Preserve behavior, invariants, compatibility, error semantics, and operational constraints.
6. Recommend a refactor only when its benefit exceeds added indirection, types, wiring, runtime cost, and maintenance burden.
7. Define tests or other evidence that prove substitutability, responsibility boundaries, extension behavior, and dependency rules.

## Principle routing

Read [references/principle-catalog.md](references/principle-catalog.md) for detailed definitions, evidence, false positives, and refactoring options.

| Principle | Review question |
|---|---|
| SRP | Does this boundary have one coherent responsibility and change reason at its abstraction level? |
| OCP | Is a demonstrated variation isolated behind a stable mechanism without making ordinary changes harder? |
| LSP | Can every subtype/implementation honor the consumer-visible contract without surprise? |
| ISP | Does each consumer depend only on the coherent capabilities it needs? |
| DIP | Do high-level policies own or depend on stable contracts rather than volatile mechanisms? |

## Language routing

- Read [references/language-mapping.md](references/language-mapping.md) first for paradigm selection and unknown languages.
- Read [references/java-jvm.md](references/java-jvm.md) for Java, Kotlin, Scala, or JVM framework designs.
- Read [references/python.md](references/python.md) for Python protocols, duck typing, modules, and callables.
- Read [references/javascript-typescript.md](references/javascript-typescript.md) for JavaScript/TypeScript modules, functions, structural typing, and unions.
- Read [references/csharp.md](references/csharp.md) for C# interfaces, delegates, records, events, async, and disposal.
- Read [references/limitations.md](references/limitations.md) whenever a recommendation risks over-abstraction or the code is not primarily object-oriented.

## Relationship to other skills

- Use `object-oriented-design` to create or revise the underlying object model, responsibilities, relationships, contracts, and lifecycle.
- Use `design-patterns` only when a recurring design problem justifies comparing named patterns.
- Use language/project coding standards for syntax, naming, framework, error-handling, and production-code rules.

SOLID does not replace OOD, architecture, design patterns, or coding standards.

## Review output

For each actionable finding, report:

1. principle and affected boundary;
2. concrete evidence and source location/design element;
3. violated or risky contract, responsibility, consumer need, or dependency direction;
4. impact on correctness, changeability, testability, compatibility, or operations;
5. minimal language-appropriate correction;
6. alternatives and cost of the correction;
7. verification needed.

Distinguish confirmed violations from design concerns and optional improvements. If the current design is simpler and adequate, explicitly recommend no SOLID-driven refactor.
