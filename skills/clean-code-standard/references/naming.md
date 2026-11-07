# Naming Standard

Names form the code's working vocabulary. Choose them for the reader who must understand, search, change, and operate the behavior.

## Intention-revealing names

- Name the concept, responsibility, unit, state, or outcome rather than its storage shape or temporary implementation.
- Include important qualifiers such as unit, scope, direction, lifecycle, or security meaning when the type or surrounding context does not make them clear.
- Avoid vague names such as `data`, `info`, `item`, `value`, `handler`, `manager`, `process`, or `util` unless the scope gives them one precise meaning.

## Avoid disinformation

- Do not use a familiar technical/domain term for something with different semantics.
- Do not call a value a list, set, map, cache, transaction, lock, event, command, or ID unless it honors the relevant contract.
- Rename stale concepts after behavior changes; do not leave a misleading name and explain the truth only in a comment.

## Make meaningful distinctions

- Distinguish concepts by responsibility or semantics, not noise words, numeric suffixes, arbitrary abbreviations, or type-only prefixes.
- Names such as `customer`, `billingCustomer`, and `shippingRecipient` communicate different roles; `customerData`, `customerInfo`, and `customerObject` usually do not.
- Keep paired concepts parallel: `source/destination`, `requested/approved`, `createdAt/expiresAt`, `encode/decode`.

## Pronounceable and searchable names

- Prefer names teammates can say consistently in reviews and incidents.
- Use established domain/technical abbreviations only when the team and ecosystem recognize them unambiguously.
- Give searchable names to important concepts, constants, error codes, feature flags, units, and protocol fields. Do not scatter unexplained literals or one-letter identifiers outside tiny conventional scopes.

## Avoid encodings

- Do not encode type, visibility, interface/implementation status, ownership, or scope into a name when the language, type system, module, or tooling already expresses it.
- Keep a project-required convention only when it adds interoperability or tool value; do not introduce a second naming dialect locally.

## Type, class, module, and package names

- Prefer nouns or noun phrases that identify a coherent concept, role, capability, policy, value, collection, or adapter.
- Avoid generic suffixes such as `Manager`, `Processor`, `Helper`, or `Service` when a more precise responsibility exists.
- Name interfaces/protocols/traits for the capability or consumer contract, not mechanically with an `I` prefix or `Impl` suffix unless project convention requires it.

## Function and method names

- Prefer verbs or verb phrases that describe the observable action or result.
- Name queries for the value they return and commands for the change they perform; do not hide mutation behind a query-shaped name.
- Use affirmative predicate names that read naturally in conditions, such as `isEligible`, `hasPermission`, or language-native equivalents.
- Make asynchronous, fallible, mutating, destructive, or unit-sensitive behavior visible when the language/project convention expects it.

## Problem and solution domain vocabulary

- Use problem-domain language for business rules, states, actors, and outcomes so code aligns with requirements and conversations.
- Use solution-domain language for genuine technical mechanisms such as serializers, repositories, adapters, partitions, caches, and transactions.
- At boundaries, make translations explicit instead of mixing business and vendor terminology in one contract.

## Scope and consistency

Short names are acceptable in small conventional scopes; wider-lived or public concepts need more context. Use one term per concept and one concept per term within a bounded context. Before renaming public or persisted identifiers, assess API, schema, serialization, metrics, logs, dashboards, documentation, migration, and compatibility impact.
