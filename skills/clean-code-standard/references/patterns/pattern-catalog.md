# Pattern Catalog

This catalog describes pattern intent without assuming a programming language. For each pattern, first test whether a simpler function, module, data structure, or explicit state transition is sufficient.

## Creational patterns

| Pattern | Use when | Main trade-off |
|---|---|---|
| Builder | Construction has many independent options, validation steps, or representations. | More construction machinery and API surface. |
| Factory Method | The caller should depend on a product contract while creation varies by subtype, configuration, or runtime context. | Creation indirection and possible registry complexity. |
| Abstract Factory | Several related products must be created as a compatible family. | Family abstractions become costly when variants change independently. |
| Prototype | New values are best produced by copying a configured exemplar. | Copy depth, identity, and mutation semantics must be explicit. |
| Singleton | A process-wide resource truly has one lifecycle and ownership boundary. | Hidden global state, poor test isolation, and lifecycle coupling; prefer explicit dependency ownership. |

## Structural patterns

| Pattern | Use when | Main trade-off |
|---|---|---|
| Adapter | An existing component has the right capability but the wrong interface or data shape. | Translation code and possible semantic mismatch. |
| Bridge | Two dimensions vary independently and should evolve without a product matrix. | More indirection and abstractions. |
| Composite | Leaves and groups should be processed through a common tree-like contract. | Uniform operations may hide leaf/container differences. |
| Decorator | Behavior should be layered around an object or operation at runtime. | Ordering, identity, and debugging become harder with many layers. |
| Facade | Consumers need a stable, smaller entry point to a complex subsystem. | The facade can become a leaky or oversized coordinator. |
| Flyweight | Many values share immutable intrinsic data while context-specific state remains external. | Identity and cache lifecycle become more complex. |
| Proxy | Access needs a boundary for authorization, caching, lazy loading, remoting, rate limiting, or instrumentation. | Hidden latency, failure, or side effects at the boundary. |

## Behavioral patterns

| Pattern | Use when | Main trade-off |
|---|---|---|
| Chain of Responsibility | Multiple handlers may process a request and the sender should not know the selected handler. | Ordering, fall-through, and unhandled requests need explicit rules. |
| Command | An action must be represented as data for queueing, retry, undo, audit, scheduling, or authorization. | More objects/messages and serialization concerns. |
| Iterator | Traversal should be separated from collection representation or support lazy/streamed access. | Lifetime, mutation, and resource ownership need care. |
| Mediator | Many collaborators have a changing interaction graph that should be centralized. | The mediator can accumulate unrelated business logic. |
| Memento | State snapshots are needed for undo, rollback, checkpoints, or recovery. | Snapshot size, consistency, retention, and sensitive data exposure. |
| Observer | Multiple consumers need notification of a change without the producer knowing their details. | Delivery, ordering, backpressure, failure, and lifecycle coupling. |
| State | Behavior changes according to an explicit lifecycle or finite-state model. | State transitions, invalid events, persistence, and recovery must be defined. |
| Strategy | A family of interchangeable algorithms or policies should be selected by configuration or context. | Strategy discovery and shared input contracts add indirection. |
| Template Method | A stable algorithm skeleton has controlled variation in a few steps. | Inheritance or callback ordering can become rigid; prefer composition when possible. |
| Visitor | Operations vary independently over a stable set of element types. | Adding element types becomes expensive and dispatch can be awkward in some languages. |

## Pattern comparison prompts

- **Strategy vs State:** Strategy is usually selected by a caller or policy; State changes because the object’s lifecycle changes. Verify who owns the transition.
- **Decorator vs Proxy:** Decorator adds composable behavior; Proxy primarily controls access or represents another boundary. The same implementation can serve both intents, so document the intent.
- **Adapter vs Facade:** Adapter preserves an existing capability behind a different contract; Facade presents a simplified subsystem workflow.
- **Mediator vs Observer:** Mediator coordinates interactions; Observer publishes notifications. Decide whether a command/response or an event is intended.
- **Factory vs Builder:** Factory chooses or creates a product; Builder assembles a complex value and validates construction.
- **Template Method vs Strategy:** Template Method fixes the skeleton and varies steps; Strategy replaces an algorithm as a collaborator. Prefer the form that matches the change boundary and language idiom.

## Pattern decision

Record the problem, requirement or code evidence, constraints, and the simplest direct alternative. For the selected approach, identify the target-language roles, ownership, lifecycle, and extension point. Explain the cost in indirection, debugging, or resources and define the checks that verify the behavior. Cover failure, concurrency, and observability where the pattern changes them.
