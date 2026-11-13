# Architecture Selection

Select the layering inside the affected backend module. Begin with its requirements, existing boundaries, and sources of change.

## Decision drivers

Assess business-rule complexity, number of use cases and integrations, rate of change, data and transaction ownership, framework coupling, and independent testability. Include deployment and performance constraints only where they affect the module's boundaries.

1. Identify the hard requirements and the design pressures that matter to the module.
2. Eliminate models that cannot meet those requirements. Compare plausible models using policy isolation, dependency direction, testability, and the cost of extra layers or migration. Evaluate the existing model by the same criteria. Keep it when it still fits and the alternatives add no material benefit.
3. Select either a single model or a hybrid as the module's layering design. Include a hybrid in the comparison when different boundaries have distinct needs. Choose it when the combination satisfies those needs and the added complexity is justified. Feature-based packaging can coexist with either choice.

| Situation | Candidate to evaluate | Avoid |
|---|---|---|
| Small CRUD module with limited rules | MVC at delivery, with thin application and persistence boundaries where useful | Full DDD tactical modeling and a port for every class |
| Module with clear use cases and framework conventions | Controller-Service-Repository or Interface-Application-Infrastructure | Business rules in controllers or persistence models |
| Complex domain with invariants, state transitions, and domain vocabulary | DDD layered, usually organized by bounded context/feature | Anemic entities with all policy in generic services |
| Multiple volatile external systems or strong framework independence/test seams | Clean/Hexagonal/Ports and Adapters | Interfaces that protect no meaningful boundary |
| Product capabilities owned and changed independently | Feature-modular, optionally with internal layers per feature | One global horizontal layer containing unrelated features |
| Transformation-heavy or functional/data-oriented workload | Pipeline or language-native modules with explicit policy/I/O boundaries | Forced repositories, entities, and class hierarchies |
| Different boundaries within one module have distinct requirements, such as rich domain rules and isolation from a vendor SDK | [Hybrid layering](#hybrid-designs), such as DDD for domain rules and Hexagonal ports for the external integration | Combining models without a requirement, a clear owner, and dependency rules for each boundary |

## Hybrid designs

Compare the hybrid with the simplest viable single model. For each model used in the hybrid, state the boundary it applies to, the requirement it addresses, who owns the behavior, and which dependencies are allowed. Check that the combined boundaries preserve transaction and data ownership and avoid dependency cycles. Load only the references for the models and decisions involved.

Examples:

- MVC can be the inbound adapter of a DDD or Clean architecture.
- A feature module can contain Interface, Application, Domain, and Infrastructure sub-boundaries.
- A modular monolith can use ports for external systems without becoming microservices.
- A simple feature can remain Controller-Service-Repository while a complex bounded context uses richer domain modeling.
- A module can use DDD layering for business rules and Hexagonal ports for an external integration that needs independent testing or isolation from its SDK.

Record which model applies at which boundary. Do not use multiple labels for the same code without defining their mapping.

## Selection output

Document the selected model, affected module, requirements that decided the choice, and how the layers will be enforced. Record tradeoffs for plausible alternatives when they affected the decision.
