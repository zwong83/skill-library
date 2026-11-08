# Test Design and Doubles

## Behavioral structure

Name tests by condition and observable outcome. Keep setup focused on behavior; hide irrelevant construction behind builders or fixtures without hiding the values that matter to the scenario.

## Double selection

- Fake: working in-memory implementation with simplified constraints; useful when behavior matters across many tests.
- Stub: returns controlled values or failures; useful for indirect inputs.
- Spy: records calls for later assertions; use when an emitted collaboration is part of the contract.
- Mock: pre-programmed interaction expectation; use sparingly for strict outbound protocols.

Prefer state/output assertions unless the interaction itself is the required behavior. Verify no forbidden side effect for authorization, validation, duplicate, or failed operations.

## Determinism seams

Inject or control clock, scheduler, random source, identifier generator, filesystem abstraction, environment/config provider, and external ports when needed. Avoid global mutation and arbitrary sleeps. For concurrency, coordinate with barriers/latches or deterministic schedulers supported by the ecosystem and assert invariants rather than timing luck.

Do not reproduce a third-party library inside a fake. When its actual semantics matter, use an integration test.
