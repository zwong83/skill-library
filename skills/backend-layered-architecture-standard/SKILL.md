---
name: backend-layered-architecture-standard
description: Select, design, implement, or review layering inside backend modules. Choose the model that fits the module's requirements and define layer responsibilities, allowed dependencies, contracts, mappings, adapters, and transaction ownership.
---

# Backend Layered Architecture Standard

Use this skill for the internal structure of backend modules. Cover responsibilities and dependencies within a module and the public contracts through which modules interact. Treat deployment topology, service decomposition, frontend architecture, and datastore or middleware selection as inputs owned by their respective designs.

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

## Mandatory workflow

**Complete steps 1 through 8 in order for every backend module layering task.** Carry out each applicable step and record its outcome. For an existing module, confirm applicable decisions against its approved design and current dependencies. A focused task can make a step brief. Record a reason for any `Not applicable` step. If a required input or decision is missing, mark the affected step `Blocked` and stop dependent work.

1. Classify the task as System Design, SDD/implementation design, refactoring, or review. Identify the affected backend modules and the decision being made.
2. Identify module use cases, business invariants, data ownership, integration boundaries, and requirements for change isolation and testability.
3. **Select or confirm the best-fit layering for each affected module.** Use [architecture selection](references/architecture-selection.md) to compare plausible single-model and hybrid designs against the module's hard requirements and tradeoffs. Choose the simplest option that satisfies them and record the evidence. Select a hybrid when distinct requirements justify combining models at different boundaries. Record the requirement, responsibility, and allowed dependencies at each boundary. An approved model may be retained only when it still fits the current requirements. If it no longer fits, record the better option and take the change through the owning design decision before implementing it. Mark this step `Blocked` if a missing requirement prevents a defensible choice.
4. Define each selected layer/module's purpose, owned decisions, public contracts, models, allowed dependencies, forbidden dependencies, transaction/failure ownership, and mapping boundaries.
5. Place external systems and security mechanisms behind adapters where substitution, isolation, testing, policy protection, or approved platform integration justifies the boundary.
6. Trace representative commands, queries, events, failures, and transactions across the layers.
7. Define composition root, dependency injection/wiring, testing seams, and automated dependency checks where practical.
8. Apply the relevant [review checklist](references/review-checklist.md) items and report unresolved ownership or dependency cycles. Record checks run, evidence reviewed, and any verification still pending.

## Readiness gate

Require the target scope, governing requirements/analysis, capability boundaries, data ownership, and material deployment or integration constraints for an implementation-ready design. For SDD or refactoring, also require the approved System Design and current module/dependency structure. If ownership, transaction boundaries, or dependency direction remain materially unresolved, label the result provisional and block implementation-ready status.

Claim completion only after all eight steps have a recorded outcome. A blocked applicable step prevents a readiness claim. Report planned checks as pending verification.

## Reference routing

Start step 3 with [architecture selection](references/architecture-selection.md). Open a candidate reference during selection only to verify a capability that affects the choice. Once the model is selected or confirmed, load the reference that answers the current requirement. Add another only for a distinct requirement or finding. A hybrid loads only the references for the boundaries it actually combines.

| Requirement | Reference |
|---|---|
| Controller, service, and repository responsibilities in a straightforward module | [Traditional layering and MVC](references/mvc-layered.md) |
| Rich domain rules, invariants, or state transitions within a module | [DDD layering](references/ddd-layered.md) |
| Ports and adapters, framework independence, or external dependency isolation | [Clean and Hexagonal layering](references/clean-hexagonal.md) |
| Feature ownership, public module contracts, or cross-module dependencies | [Feature modules](references/feature-modular.md) |
| A specific import, mapping, transaction, failure, security placement, or enforcement question | [Dependency and boundary rules](references/dependency-and-boundary-rules.md). Read the relevant section. |
| Workflow step 8 | [Review checklist](references/review-checklist.md). Apply items within scope. |

For example, an import cycle between existing feature modules starts with feature modules. Add dependency rules if the fix needs a specific enforcement mechanism. Use `software-security-standard` only when a material security control needs more than assigning it an owner and a layer.

## SD and SDD boundary

For System Design, specify logical layers/modules, responsibilities, dependency direction, major ports/adapters, data and transaction ownership, cross-boundary flows, and rationale. Use component and sequence diagrams where they clarify behavior.

For SDD/OpenSpec, convert the approved design into concrete packages/modules, public interfaces, adapter implementations, dependency rules, migration steps, tests, and bounded implementation tasks. Do not silently change the approved architecture; update the owning SD decision first.

## Expected output

Include a brief numbered record of steps 1 through 8 with the outcome and evidence or next action for each step. Explain any `Not applicable` or `Blocked` outcomes.

Report the selected or confirmed model, the requirements behind it, and the affected ownership, contracts, dependencies, and verification. For a full module design, include the layer and dependency matrix, representative flows, composition, and enforcement. Keep focused outputs to the affected boundaries.
