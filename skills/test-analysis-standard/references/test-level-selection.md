# Test Level Selection

Choose the lowest level that exercises the real risk with a trustworthy oracle.

| Question | Prefer |
|---|---|
| Pure rule, calculation, state transition, local invariant | Unit/component |
| Framework mapping, serialization, repository query, database constraint, broker/cache adapter | Integration |
| Producer/consumer schema or protocol compatibility | Contract |
| Critical multi-component journey or deployed-system behavior | System/end-to-end |
| Business acceptance and policy outcome | Acceptance |
| Security, performance, resilience, migration, accessibility, operations | Relevant non-functional type |

Do not duplicate every scenario at every level. Use broader tests for boundaries and journeys that lower-level tests cannot prove. A test with mocked adapters remains a unit/component test; an integration test exercises at least one real integration boundary with representative behavior.

Escalate level when the risk depends on framework configuration, transaction behavior, serialization, network protocol, database semantics, broker delivery, cache consistency, security enforcement, deployment topology, or multiple components collaborating.
