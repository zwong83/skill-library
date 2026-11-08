# Architecture Selection

Select architecture from complexity and change pressure, not familiarity or folder templates.

## Decision drivers

Assess business-rule complexity, number of use cases and integrations, rate of change, data/transaction ownership, team boundaries, framework coupling, independent testability, deployment model, performance constraints, and expected system lifetime.

| Situation | Strong starting point | Avoid |
|---|---|---|
| Small CRUD or short-lived application with limited rules | MVC plus a thin application/service and repository boundary | Full DDD tactical modeling and a port for every class |
| Moderate application with clear use cases and framework conventions | Controller-Service-Repository or Interface-Application-Infrastructure | Business rules in controllers or persistence models |
| Complex domain with invariants, state transitions, and domain vocabulary | DDD layered, usually organized by bounded context/feature | Anemic entities with all policy in generic services |
| Multiple volatile external systems or strong framework independence/test seams | Clean/Hexagonal/Ports and Adapters | Interfaces that protect no meaningful boundary |
| Product capabilities owned and changed independently | Feature-modular, optionally with internal layers per feature | One global horizontal layer containing unrelated features |
| Transformation-heavy or functional/data-oriented workload | Pipeline or language-native modules with explicit policy/I/O boundaries | Forced repositories, entities, and class hierarchies |

## Hybrid designs

Models may be combined deliberately:

- MVC can be the inbound adapter of a DDD or Clean architecture.
- A feature module can contain Interface, Application, Domain, and Infrastructure sub-boundaries.
- A modular monolith can use ports for external systems without becoming microservices.
- A simple feature can remain Controller-Service-Repository while a complex bounded context uses richer domain modeling.

Record which model applies at which boundary. Do not use multiple labels for the same code without defining their mapping.

## Selection output

Document the selected model, scope, drivers, rejected simpler and more complex alternatives, layer/module mapping, expected benefits, added cost, enforcement approach, and trigger for future simplification or evolution.
