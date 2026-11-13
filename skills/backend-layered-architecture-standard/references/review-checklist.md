# Layered Architecture Review Checklist

Report each item as `Pass`, `Gap`, `Needs decision`, or `Not applicable`.

- Every layer/module owns concrete decisions and is not merely pass-through ceremony.
- Each affected backend module has a named layering design, either a single model or a hybrid, justified by its requirements. For a hybrid, each constituent model has a defined boundary, owner, and dependency rules.
- MVC presentation responsibilities are not confused with complete application/domain/infrastructure architecture.
- Capability, data, transaction, and failure ownership are explicit.
- Allowed and forbidden dependencies are documented and enforceable.
- Domain/application policy is independent of transport, persistence, cache, broker, and vendor SDK types.
- Ports protect meaningful boundaries and use inward-facing language.
- Adapters translate data and errors without redefining business rules.
- Transport DTOs, application contracts, domain models, persistence records, and integration messages are reused or mapped by an explicit semantic decision rather than ceremony.
- Representative command, query, event, and failure flows respect the dependency direction.
- Cross-cutting concerns do not create hidden reverse dependencies.
- Authentication, authorization, business security invariants, encryption, key/secrets, audit, and secure configuration have explicit enforcement points and owners; middleware or UI checks are not treated as complete authorization.
- Shared modules have narrow ownership and no dependency cycles.
- Controllers, application services, domain objects/services, repositories, cache/broker clients, and composition code are placed according to the selected model without vendor leakage inward.
- The composition root and runtime wiring are explicit.
- Unit, contract, integration, architecture, and end-to-end tests are assigned to the right boundaries.
- SD decisions map to concrete SDD modules/tasks without silent architecture changes.
