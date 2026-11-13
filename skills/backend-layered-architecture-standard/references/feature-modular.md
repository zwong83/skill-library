# Feature-Modular Architecture

Feature-modular architecture groups backend code by business capability or use case. Each module can choose its own internal layering based on its requirements.

```text
orders/
  interface/
  application/
  domain/
  infrastructure/

catalog/
  interface/
  application/
  domain/
  infrastructure/
```

Small features may use fewer internal boundaries:

```text
health-check/
  endpoint
  check
```

## Rules

- Give each feature/module an owner, public contract, data responsibility, allowed dependencies, and internal implementation boundary.
- Other modules depend on the public contract, not internal controllers, repositories, tables, or adapter classes.
- Prefer explicit commands/queries/events or narrow module APIs over a shared database as the integration contract.
- Prevent cyclic feature dependencies. Extract a genuinely shared policy/value only when ownership and stability are clear.
- Keep `common`, `shared`, and `utils` small and governed; they must not become dependency dumping grounds.
- A feature may choose MVC, DDD layered, Clean/Hexagonal, pipeline, or direct language-native structure internally according to its complexity.
- Moving from modular monolith to services changes deployment and distributed-system semantics; folder separation alone does not make a service boundary.

Feature-modular organization is often preferable to one global `controllers/services/repositories` tree because it localizes change and ownership. Do not duplicate infrastructure clients or cross-cutting policies independently in every feature when a governed adapter/platform boundary is appropriate.
