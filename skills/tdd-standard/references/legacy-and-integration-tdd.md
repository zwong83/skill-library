# Legacy and Integration TDD

## Legacy code

When behavior is insufficiently protected, first add characterization tests that capture confirmed current behavior. Do not treat accidental behavior as a requirement; label uncertainty and seek a decision. Introduce the smallest seam needed for deterministic testing, then start Red-Green-Refactor for the intended change.

Avoid broad cleanup before protection. Refactor only affected code under tests and approved scope.

## Integration-driven cycle

An integration test may provide the Red when the requirement depends on database constraints, transaction semantics, serialization, framework wiring, broker/cache behavior, or a real protocol. Keep the boundary focused and environment repeatable.

Use a thin integration test to prove wiring/semantics and unit tests for detailed rule combinations. Do not run an expensive full-system suite for every micro-cycle when a narrower trustworthy test exists.

## Outside-in TDD

An outer acceptance/contract test may guide a slice while inner unit tests drive components. Keep outer tests few and stable. Do not create speculative layers or mocks; let approved architecture and emerging behavior guide concrete seams without changing material design silently.
