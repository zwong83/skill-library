# MVC and Traditional Layered Architecture

MVC separates interface responsibilities. A backend commonly combines it with Controller-Service-Repository layering; this is not automatically DDD.

```text
View / Client
     ↕
Controller / Interface
     ↓
Application Service / Use Case
     ↓
Repository Contract
     ↓
Persistence Adapter / Database
```

## Responsibilities

- **View/client/view model:** presentation state and rendering contract; no server-side business authority.
- **Controller/interface:** parse protocol input, establish authentication context, validate transport shape, call one or more application operations, and map outcomes to protocol responses.
- **Application service/use case:** orchestrate the operation, authorization policy, transaction, idempotency, and calls to business policy and dependencies.
- **Domain/model:** business concepts and rules when they exist. Do not let “Model” ambiguously mean DTO, database row, and business object at once.
- **Repository contract:** persistence capability needed by the application/domain, expressed without ORM or vendor types when isolation is required.
- **Infrastructure:** ORM, SQL, Redis, broker, external API, filesystem, and framework implementation.

## Boundary rules

- Controllers must not own business rules, database transactions, repository queries, or broker/cache SDK calls.
- Application services must not become pass-through wrappers. If no orchestration or policy boundary exists, a simpler structure may be clearer.
- Repository implementations do not decide business behavior; they translate persistence concerns.
- Framework annotations are acceptable at outer boundaries but must not force transport/persistence types through core contracts.
- Map request/response DTOs, application commands/results, domain models, and persistence records only where their semantics, trust, lifecycle, or compatibility differ. Do not duplicate identical models ceremonially.

## Typical flow

```text
CreateOrderRequest
  → OrderController
  → CreateOrderUseCase
  → Order policy/model
  → OrderRepository
  → SQL/ORM adapter
  → CreateOrderResult
  → HTTP response
```

Select traditional layering when its boundaries satisfy the module's requirements for ownership, dependency isolation, and testing. Add richer domain or port boundaries when the requirements justify them.
