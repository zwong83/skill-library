# Clean, Onion, and Hexagonal Architecture

These models use different diagrams and vocabulary but share a central rule: business/application policy must not depend on delivery, frameworks, databases, brokers, or other volatile mechanisms.

```text
Inbound Adapter → Input Port / Use Case → Domain Policy
                                      ↓
                              Output Port
                                      ↑
                              Outbound Adapter
```

## Roles

- **Inbound adapters:** HTTP controllers, UI presenters, CLI commands, message consumers, schedulers, and tests that invoke use cases.
- **Input ports/use cases:** application operations and their typed request/result contracts.
- **Domain/policy:** framework-independent business decisions and invariants.
- **Output ports:** inward-owned capabilities required from persistence, cache, messaging, time, files, or external services.
- **Outbound adapters:** SQL/ORM repositories, Redis adapters, Kafka/RabbitMQ/RocketMQ publishers, HTTP clients, and filesystem implementations.
- **Composition root:** selects concrete adapters, binds configuration, validates startup, and owns process lifecycle.

## Rules

- Ports are justified at semantic, volatility, trust, ownership, or test boundaries; do not create an interface for every class.
- Port contracts use caller/application/domain language and do not expose vendor SDK types or exceptions.
- Adapters translate protocol/data/error semantics without redefining business policy.
- Framework dependency injection is a composition mechanism, not the architecture itself.
- Input and output mappings should be explicit when models differ, but avoid mapping identical data through several ceremonial types.
- Tests can drive use cases through input ports, verify domain policy directly, and contract-test adapters against port behavior.

Clean/Hexagonal architecture is useful when external integrations are volatile, test isolation matters, or framework independence has demonstrated value. For simple CRUD, its additional contracts and mapping may cost more than they protect.
