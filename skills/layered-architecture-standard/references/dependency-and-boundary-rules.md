# Dependency and Boundary Rules

## Responsibility matrix

For every layer or module record:

| Concern | Required decision |
|---|---|
| Purpose | Decisions and behavior owned here |
| Public contract | Commands, queries, events, functions, or interfaces exposed |
| Allowed dependencies | Stable inward contracts and approved shared primitives |
| Forbidden dependencies | Frameworks, adapters, sibling internals, or transport types that must not leak in |
| Data ownership | State and schema owned or accessed |
| Transaction ownership | Where atomic work begins, commits, or compensates |
| Failure ownership | Errors created, translated, retried, or exposed |
| Tests | Unit, contract, integration, architecture, or end-to-end evidence |

## Boundary rules

- Transport DTOs do not become domain models by default; map at a boundary when semantics, versioning, or trust differ.
- Persistence models do not dictate domain behavior when storage concerns would leak inward.
- Ports use business/application language and return outcomes the caller can act on; do not leak vendor exceptions or SDK types.
- Adapters translate external errors and data into the port contract while preserving safe cause information.
- Transactions belong to the use case or component that owns the atomic invariant. Do not hide multi-resource atomicity assumptions.
- Caches are infrastructure optimizations unless the product contract explicitly makes cached state authoritative.
- Message consumers and scheduled jobs are delivery adapters; they invoke application behavior and map completion/failure to broker or scheduler semantics.
- Shared libraries must have a narrow, stable purpose. A generic `common` module must not become an unowned dependency hub.

## Cross-cutting concerns

Authentication context, authorization, validation, transactions, logging, tracing, metrics, retries, and caching may cross layers, but ownership remains explicit. Prefer composition around use cases or adapters. Do not let observability or framework annotations become a hidden dependency from policy code to infrastructure.

## Enforcement

Use language-appropriate module visibility, package boundaries, lint/import rules, architecture tests, dependency graphs, and CI checks. A diagram alone does not enforce a dependency rule.
