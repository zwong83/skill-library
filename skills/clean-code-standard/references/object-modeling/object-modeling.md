# Object Modeling

Use object modeling to capture behavior, invariants, identity, and lifecycle—not to convert every noun into a class.

## Concept categories

| Category | Meaning | Typical design concern |
|---|---|---|
| Entity | Has continuity and identity across state changes | Identity, lifecycle, invariants, persistence boundaries |
| Value | Defined by its attributes rather than identity | Immutability, validation, equality, units |
| Policy | Chooses or calculates behavior from rules | Inputs, variation, auditability, testability |
| Domain service | Coordinates domain behavior that belongs to no single object | Cohesion, transaction boundary, dependencies |
| Application service | Orchestrates a use case across domain and ports | Authorization, sequencing, idempotency, error mapping |
| Adapter | Translates between domain/application contracts and external systems | Mapping, failures, retries, compatibility |
| Resource | Owns an external or finite lifecycle | Acquisition, release, concurrency, failure |
| Message/event | Describes an immutable fact, request, or response | Schema, ordering, delivery, versioning |

These are reasoning categories, not required class suffixes.

## Modeling sequence

1. Start from approved scenarios, state transitions, business rules, and system boundaries.
2. Identify information that must stay valid together; write the invariant before choosing a type.
3. Decide whether the concept needs stable identity or can be an immutable value.
4. Assign state-changing behavior to the boundary that can protect the invariant.
5. Identify ownership, creation, lifetime, persistence, and deletion rules.
6. Define relationships with direction, cardinality, mutability, consistency, and cascade behavior.
7. Separate domain policy from orchestration and infrastructure translation.
8. Test the model against success, failure, edge, concurrent, and recovery scenarios.

## Relationship questions

- Who owns creation and destruction?
- Can the related object exist independently?
- Is the relationship navigated in one or both directions?
- Must updates be atomic or eventually consistent?
- Is a reference, identifier, snapshot, event, or query more appropriate?
- What happens when the related object is unavailable, deleted, stale, or concurrently changed?

## Aggregate boundaries

Use an aggregate only when a cluster of entities and values must preserve invariants within one consistency boundary.

- Identify one Aggregate Root as the external access point for invariant-preserving changes.
- Keep internal entities and values reachable through the root's behavior rather than exposing uncontrolled mutation.
- Reference another aggregate by identity or an explicit snapshot/message unless the approved consistency model requires otherwise.
- Align the aggregate with a transaction boundary; do not load or lock unrelated state merely for navigation convenience.
- Define optimistic locking/versioning, conflict detection, retry, and concurrent-modification behavior where multiple writers are possible.
- Define when domain events are recorded and published, including transaction/outbox behavior and duplicate handling.
- Ensure persistence and reconstitution restore valid state without bypassing invariants or invoking unintended side effects.
- Split an aggregate when contention, transaction size, ownership, or independent lifecycle outweigh the need for immediate consistency.

## Modeling traps

- noun-to-class modeling without behavior or invariants;
- persistence schema driving the domain model by default;
- bidirectional relationships with unclear ownership;
- mutable value objects or entities exposing unrestricted setters;
- domain objects coupled to web, database, queue, or framework APIs;
- “service” objects that accumulate every rule and leave domain objects as data bags;
- aggregates so large that transactions, contention, and tests become fragile.
