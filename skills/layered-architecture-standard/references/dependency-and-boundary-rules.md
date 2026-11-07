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

## Default dependency matrix

| Source | May depend on | Must not depend on directly |
|---|---|---|
| Interface/Delivery | Application input contracts and approved presentation primitives | Database/cache/broker SDKs, persistence records, unrelated feature internals |
| Application | Domain policy, inward ports, application contracts | Controllers/views, concrete adapters, ORM sessions, vendor clients |
| Domain | Domain-owned types and minimal approved language primitives | Application orchestration, transport/framework, database/cache/broker/vendor types |
| Infrastructure/Adapters | The inward port it implements and required vendor libraries | Other adapter internals or authority to redefine business rules |
| Composition/Bootstrap | All concrete modules required for wiring | Business behavior beyond startup/lifecycle policy |

Dependencies may be compile-time imports, runtime calls, schema ownership, annotations, code generation, configuration, or shared data. Check all forms, not imports alone.

## Model and mapping boundaries

- Transport DTOs represent external protocol/version/trust contracts.
- Application commands/queries/results represent use-case contracts.
- Domain models represent business meaning and invariants.
- Persistence records represent storage schema and ORM/query concerns.
- Integration messages represent cross-capability compatibility contracts.

Reuse a type when these meanings genuinely coincide and coupling is accepted. Map when trust, semantics, lifecycle, ownership, versioning, nullability, or security differs. Mapping belongs at the boundary that understands both sides.

## Transaction and failure ownership

- The application/use-case boundary normally owns a local transaction because it knows the complete atomic operation; domain policy defines invariants but should not open database transactions.
- Adapters translate database/cache/broker/network failures into inward error contracts. Interface adapters map application outcomes to HTTP, message acknowledgement/retry, CLI, or scheduler semantics.
- Multi-resource work requires an explicit consistency pattern; a layer diagram does not make database, Redis, and broker actions atomic.
- Logging records the final owned outcome once. Tracing and metrics may cross boundaries through instrumentation without leaking vendor APIs into domain policy.
- Cache and message brokers are infrastructure adapters unless the approved architecture gives them a distinct authoritative role.

## Cross-cutting concerns

Authentication context, authorization, validation, transactions, logging, tracing, metrics, retries, and caching may cross layers, but ownership remains explicit. Prefer composition around use cases or adapters. Do not let observability or framework annotations become a hidden dependency from policy code to infrastructure.

## Enforcement

Use language-appropriate module visibility, package boundaries, lint/import rules, architecture tests, dependency graphs, and CI checks. A diagram alone does not enforce a dependency rule.
