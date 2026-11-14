# Responsibilities and Boundaries

Responsibility assignment should minimize the number of reasons a boundary changes while keeping behavior close to the information and invariant it governs.

## Responsibility types

- **Knowing:** facts, derived values, configuration, or state owned by the object.
- **Doing:** calculations, state transitions, validation, orchestration, or translation.
- **Deciding:** policy selection, authorization, eligibility, routing, or prioritization.
- **Creating:** construction that owns required validation and lifecycle rules.
- **Coordinating:** sequencing collaborators without absorbing their domain responsibilities.

## Assignment criteria

For every responsibility, ask:

- Which boundary owns the required information and invariant?
- Which change driver would cause this responsibility to evolve?
- Does moving it reduce or increase coupling?
- Is it domain policy, use-case orchestration, infrastructure, presentation, or integration translation?
- Can the behavior be tested through a stable contract without exposing internal state?
- Does the chosen boundary have a clear owner and lifecycle?

## Cohesion and coupling

High cohesion means responsibilities support one coherent purpose; it does not require one-method classes. Low coupling means collaborators know the smallest stable contract they need; it does not require an interface between every pair.

Review:

- unrelated dependencies, data, or change drivers in one object;
- orchestration mixed with domain policy or infrastructure details;
- callers reaching through several objects to perform one operation;
- repeated extraction of internal data followed by external decision-making;
- abstractions whose implementations or consumers do not share a meaningful contract;
- dependency cycles or upward dependencies from policy to mechanisms.

## Contract design

A public contract should define:

- purpose and consumer;
- accepted inputs and preconditions;
- returned result and postconditions;
- preserved invariants;
- expected errors and failure ownership;
- mutation and transaction behavior;
- idempotency, ordering, timeout, cancellation, and concurrency when relevant;
- compatibility and versioning expectations.

Avoid exposing representation details simply to make tests or frameworks convenient. Introduce seams at meaningful behavior or boundary contracts.
