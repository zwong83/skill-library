---
name: backend-layered-architecture-standard
description: Select, design, implement, or review language-neutral MVC/three-layer, DDD layered, Clean/Hexagonal, feature-modular, or hybrid architectures, including layer responsibilities, dependency direction, DTO/domain/persistence mapping, ports/adapters, transactions, failures, infrastructure, and test seams; do not force one model onto every system.
---

# Backend Layered Architecture Standard

Use this skill to select an appropriate layering model and turn its responsibilities into enforceable boundaries. Layers are dependency and ownership rules, not folders added for ceremony.

## Core rules

- Start from business capabilities, change boundaries, data ownership, deployment constraints, and quality attributes; do not select layers from a framework template alone.
- Separate policy from mechanism. Domain/application policy must not depend directly on databases, caches, brokers, transport frameworks, or vendor SDKs.
- Dependencies point toward the code that owns the policy. Infrastructure implements inward-facing ports; it does not redefine domain behavior.
- Keep a responsibility in one authoritative layer. Avoid pass-through services, duplicate models, and interfaces with only one speculative implementation unless they protect a real boundary or test seam.
- Do not force OOP, repositories, domain entities, or ports onto data-oriented, functional, pipeline, event-sourced, or language-native designs that have clearer boundaries.
- A deployment unit, service, package, and layer are different concepts. State which boundary is being designed.
- MVC is primarily an interface/presentation pattern; Controller-Service-Repository is an application layering convention; DDD, Clean, and Hexagonal architectures define broader policy and dependency boundaries. Do not treat these labels as interchangeable.
- Cross-cutting concerns must enter through explicit composition, middleware/interceptors, decorators, policy modules, or platform instrumentation without reversing dependency direction.
- Security controls may span layers, but authentication, authorization, business security invariants, encryption, key/secrets access, audit, and secure configuration need explicit enforcement points and owners. Invoke/read `software-security-standard` when these controls are material; this skill owns their architectural placement, not their full security specification.

## Default reference model

Use this model when a concrete baseline is needed, then merge or rename layers to fit the language and system:

```text
Interface / Delivery
        ↓
Application / Use Cases
        ↓
Domain / Business Policy
        ↑
Ports ← Infrastructure / Adapters

Composition / Bootstrap wires the system.
```

- **Interface/Delivery:** HTTP/UI/controller, message consumer, CLI, scheduler, transport validation, and protocol mapping.
- **Application:** use-case orchestration, transaction intent, authorization coordination, idempotency, and application outcomes.
- **Domain:** business invariants, decisions, calculations, state transitions, entities/values where appropriate, and domain errors.
- **Ports:** inward-owned contracts for persistence, cache, messaging, clock, files, and external services.
- **Infrastructure/Adapters:** database, Redis, broker, HTTP client, filesystem, framework, and vendor SDK implementations.
- **Composition/Bootstrap:** concrete wiring, configuration binding, startup validation, and process lifecycle.

Not every system needs six physical directories. Merge layers only when responsibilities, dependency direction, and testability remain clear.

## Workflow

1. Classify the task as System Design, SDD/implementation design, refactoring, or review.
2. Identify capabilities, use cases, invariants, data owners, external actors, trust boundaries, and runtime/deployment constraints.
3. Compare MVC/three-layer, DDD layered, Clean/Hexagonal, feature-modular, and simpler language-native alternatives; select the smallest model that addresses actual complexity.
4. Define each selected layer/module's purpose, owned decisions, public contracts, models, allowed dependencies, forbidden dependencies, transaction/failure ownership, and mapping boundaries.
5. Place external systems and security mechanisms behind adapters where substitution, isolation, testing, policy protection, or approved platform integration justifies the boundary.
6. Trace representative commands, queries, events, failures, and transactions across the layers.
7. Define composition root, dependency injection/wiring, testing seams, and automated dependency checks where practical.
8. Run the review checklist and report unresolved ownership or dependency cycles.

## Readiness gate

Require the target scope, governing requirements/analysis, capability boundaries, data ownership, and material deployment or integration constraints for an implementation-ready design. For SDD or refactoring, also require the approved System Design and current module/dependency structure. If ownership, transaction boundaries, or dependency direction remain materially unresolved, label the result provisional and block implementation-ready status.

## Reference routing

- Read [references/architecture-selection.md](references/architecture-selection.md) first when the architecture model has not already been approved.
- Read [references/mvc-layered.md](references/mvc-layered.md) for MVC or Controller-Service-Repository systems.
- Read [references/ddd-layered.md](references/ddd-layered.md) for domain-centric systems with substantial business invariants and bounded contexts.
- Read [references/clean-hexagonal.md](references/clean-hexagonal.md) for Clean Architecture, Onion, or Ports-and-Adapters boundaries.
- Read [references/feature-modular.md](references/feature-modular.md) for package-by-feature, modular monolith, or capability-owned modules.
- Read [references/dependency-and-boundary-rules.md](references/dependency-and-boundary-rules.md) when defining allowed imports, ports/adapters, transactions, cross-cutting concerns, or tests.
- Invoke/read `software-security-standard` when the architecture must place or review identity, authorization, tenant isolation, encryption, key/secrets, audit, privacy, or security verification controls.
- Read [references/review-checklist.md](references/review-checklist.md) before approving a design or refactor.

## SD and SDD boundary

For System Design, specify logical layers/modules, responsibilities, dependency direction, major ports/adapters, data and transaction ownership, cross-boundary flows, and rationale. Use component and sequence diagrams where they clarify behavior.

For SDD/OpenSpec, convert the approved design into concrete packages/modules, public interfaces, adapter implementations, dependency rules, migration steps, tests, and bounded implementation tasks. Do not silently change the approved architecture; update the owning SD decision first.

## Expected output

Provide the selected model and rationale, layer/module and model-mapping tables, allowed/forbidden dependency matrix, boundary contracts, representative request/message flow, transaction, failure, and security-control ownership, composition strategy, enforcement/test strategy, violations or risks, and traceability to requirements and design decisions.
