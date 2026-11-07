# Architecture Models

Choose a model because it clarifies ownership and change, not because its labels are fashionable.

## Practical models

| Model | Useful when | Main caution |
|---|---|---|
| Feature-modular | Product capabilities change independently and need cohesive code ownership | Do not recreate horizontal coupling inside every feature |
| Traditional layered | Request/data processing is straightforward and framework conventions are valuable | Prevent domain/application policy from leaking into controllers or persistence |
| Ports and adapters / hexagonal | External systems and delivery mechanisms must be isolated from use cases | Add ports only at meaningful volatility or policy boundaries |
| Clean/onion-style dependency rule | Business policy must remain independent of frameworks and infrastructure | Do not create mapping and abstraction layers with no decision-making value |
| Pipeline/data-oriented | Work is naturally a sequence of transformations | Make state, retries, partial failure, and observability explicit |
| Event-driven | Capabilities communicate asynchronously and temporal decoupling is required | Define message ownership, delivery semantics, idempotency, ordering, and recovery |

These models can be combined. A feature module may contain interface, application, domain/policy, and adapter boundaries while the whole system remains a modular monolith. Microservices do not remove the need for internal boundaries.

## Default conceptual responsibilities

- **Interface/delivery:** protocol parsing, authentication context intake, validation of transport shape, response/message mapping, and boundary-level failure handling.
- **Application/use case:** orchestration, authorization policy coordination, transaction intent, idempotency coordination, and use-case outcomes.
- **Domain/policy:** business invariants, decisions, state transitions, calculations, and domain errors without vendor dependencies.
- **Ports/contracts:** capabilities required by inward policy, expressed in domain/application terms.
- **Infrastructure/adapters:** database, cache, broker, filesystem, clock, external API, framework, and vendor SDK integration.
- **Composition/bootstrap:** concrete wiring, configuration binding, process lifecycle, and startup validation.

Not every system needs every label. Merge responsibilities when the resulting boundary remains explicit and testable.
