---
name: layered-architecture-standard
description: Design or review language-neutral software layers, module boundaries, dependency direction, ports and adapters, ownership, transaction boundaries, and test seams for System Design, SDD, implementation, or refactoring; do not force a fixed layer count or object-oriented style.
---

# Layered Architecture Standard

Use this skill to turn system responsibilities into enforceable boundaries. Layers are dependency and ownership rules, not folders added for ceremony.

## Core rules

- Start from business capabilities, change boundaries, data ownership, deployment constraints, and quality attributes; do not select layers from a framework template alone.
- Separate policy from mechanism. Domain/application policy must not depend directly on databases, caches, brokers, transport frameworks, or vendor SDKs.
- Dependencies point toward the code that owns the policy. Infrastructure implements inward-facing ports; it does not redefine domain behavior.
- Keep a responsibility in one authoritative layer. Avoid pass-through services, duplicate models, and interfaces with only one speculative implementation unless they protect a real boundary or test seam.
- Do not force OOP, repositories, domain entities, or ports onto data-oriented, functional, pipeline, event-sourced, or language-native designs that have clearer boundaries.
- A deployment unit, service, package, and layer are different concepts. State which boundary is being designed.
- Cross-cutting concerns must enter through explicit composition, middleware/interceptors, decorators, policy modules, or platform instrumentation without reversing dependency direction.

## Workflow

1. Classify the task as System Design, SDD/implementation design, refactoring, or review.
2. Identify capabilities, use cases, invariants, data owners, external actors, trust boundaries, and runtime/deployment constraints.
3. Choose the smallest architecture model that makes responsibilities and dependency direction clear.
4. Define each layer/module's purpose, owned decisions, public contracts, allowed dependencies, forbidden dependencies, and transaction responsibility.
5. Place external systems behind adapters where substitution, isolation, testing, or policy protection justifies the boundary.
6. Trace representative commands, queries, events, failures, and transactions across the layers.
7. Define composition root, dependency injection/wiring, testing seams, and automated dependency checks where practical.
8. Run the review checklist and report unresolved ownership or dependency cycles.

## Readiness gate

Require the target scope, governing requirements/analysis, capability boundaries, data ownership, and material deployment or integration constraints for an implementation-ready design. For SDD or refactoring, also require the approved System Design and current module/dependency structure. If ownership, transaction boundaries, or dependency direction remain materially unresolved, label the result provisional and block implementation-ready status.

## Reference routing

- Read [references/architecture-models.md](references/architecture-models.md) when selecting layered, feature-modular, clean, hexagonal, or hybrid boundaries.
- Read [references/dependency-and-boundary-rules.md](references/dependency-and-boundary-rules.md) when defining allowed imports, ports/adapters, transactions, cross-cutting concerns, or tests.
- Read [references/review-checklist.md](references/review-checklist.md) before approving a design or refactor.

## SD and SDD boundary

For System Design, specify logical layers/modules, responsibilities, dependency direction, major ports/adapters, data and transaction ownership, cross-boundary flows, and rationale. Use component and sequence diagrams where they clarify behavior.

For SDD/OpenSpec, convert the approved design into concrete packages/modules, public interfaces, adapter implementations, dependency rules, migration steps, tests, and bounded implementation tasks. Do not silently change the approved architecture; update the owning SD decision first.

## Expected output

Provide the selected model and rationale, a responsibility/dependency matrix, boundary contracts, representative flow, transaction and failure ownership, composition strategy, test strategy, violations or risks, and traceability to requirements and design decisions.
