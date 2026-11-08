# DDD Layered Architecture

Use DDD layering when business concepts, invariants, state transitions, and bounded contexts are substantial enough to benefit from an explicit domain model.

```text
Interface
   ↓
Application
   ↓
Domain
   ↑
Infrastructure implements inward contracts
```

## Layer responsibilities

- **Interface:** transport/message/UI mapping, authentication context intake, input-shape validation, and public outcome mapping.
- **Application:** use cases, orchestration, authorization coordination, transaction boundary, idempotency, loading/saving aggregates, and publishing approved outcomes.
- **Domain:** entities, value objects, aggregates, invariant enforcement, domain services, policies, state transitions, calculations, and domain events where useful.
- **Infrastructure:** repository implementations, ORM mappings, database/cache/broker/API adapters, framework integration, and technical configuration.

## DDD rules

- Organize domain language within a bounded context. The same word may have different models across contexts; translate explicitly.
- An aggregate protects a consistency boundary, not a database object graph. Keep transactions and synchronous invariant enforcement within the smallest valid boundary.
- Repository contracts normally represent aggregate/domain persistence needs, not one generic repository per table.
- Use a domain service only for domain behavior that does not naturally belong to an entity/value/policy; do not turn it into a general orchestration container.
- Application services coordinate but should not duplicate domain invariants. Domain objects should not depend on controllers, ORM sessions, Redis clients, brokers, or HTTP SDKs.
- Domain events describe domain facts. Their publication, durability, integration-event transformation, and external delivery belong to application/infrastructure coordination.

## Model mapping

Separate transport DTOs, application commands/results, domain objects, persistence records, and integration events when they differ in trust, semantics, lifecycle, ownership, or compatibility. Mapping belongs at the boundary that understands both models.

Avoid forcing aggregates, entities, value objects, factories, repositories, and domain events into every CRUD feature. DDD is justified by domain complexity, not project prestige.
