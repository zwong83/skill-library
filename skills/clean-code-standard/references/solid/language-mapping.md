# SOLID Language and Paradigm Mapping

Apply SOLID to semantic boundaries, not Java syntax.

## Mapping rules

- A “responsibility” may belong to a module, type, function, service, process, or package—not necessarily a class.
- An “interface” may be a protocol, trait, function signature, module contract, structural type, message schema, or consumer-owned port.
- A “subtype” includes implementations, adapters, mocks, structural types, trait objects, and remotely accessed services that claim the same contract.
- “Dependency inversion” concerns policy direction and contract ownership; a DI container is optional.
- “Extension” may use composition, higher-order functions, data variants, pattern matching, plugins, configuration, or message handlers.

## Go

Use small consumer-owned interfaces, packages, structs, embedding, and function values. Avoid creating provider-owned interfaces or Java-style layers without a boundary need. LSP applies to interface implementations; ISP should not reduce meaningful contracts to arbitrary one-method wrappers.

## Rust

Use traits, enums, generics, modules, functions, ownership, and explicit errors. Closed variants may be clearer as enums and exhaustive matching than OCP-oriented plugin abstractions. LSP includes ownership, lifetime, error, panic, Send/Sync, and performance expectations in the effective contract.

## Functional and data-oriented systems

Assess responsibility, substitution, consumer contracts, and dependency direction at function, module, data-type, and pipeline boundaries. Do not introduce mutable objects or nominal interfaces solely to make SOLID terminology fit.

## Unknown languages

Identify the language's module/type system, polymorphism mechanism, error model, ownership/mutation rules, and concurrency model. Translate each principle into those native boundaries before reviewing the design.
