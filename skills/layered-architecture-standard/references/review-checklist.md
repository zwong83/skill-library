# Layered Architecture Review Checklist

Report each item as `Pass`, `Gap`, `Needs decision`, or `Not applicable`.

- Every layer/module owns concrete decisions and is not merely pass-through ceremony.
- Capability, data, transaction, and failure ownership are explicit.
- Allowed and forbidden dependencies are documented and enforceable.
- Domain/application policy is independent of transport, persistence, cache, broker, and vendor SDK types.
- Ports protect meaningful boundaries and use inward-facing language.
- Adapters translate data and errors without redefining business rules.
- Representative command, query, event, and failure flows respect the dependency direction.
- Cross-cutting concerns do not create hidden reverse dependencies.
- Shared modules have narrow ownership and no dependency cycles.
- The composition root and runtime wiring are explicit.
- Unit, contract, integration, architecture, and end-to-end tests are assigned to the right boundaries.
- SD decisions map to concrete SDD modules/tasks without silent architecture changes.
