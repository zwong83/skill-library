# Test Level Selection

Choose the lowest level that exercises the real risk with a trustworthy oracle.

| Question | Prefer |
|---|---|
| Pure rule, calculation, state transition, local invariant | Unit/component |
| Framework mapping, serialization, repository query, database constraint, broker/cache adapter | Integration |
| Provider/consumer schema, protocol, semantic, or version compatibility | Contract |
| User-visible component state, interaction, visual, accessibility, browser/device behavior | UI at the smallest trustworthy layer |
| Critical multi-component journey or deployed-system behavior | System/end-to-end |
| Business acceptance and policy outcome | Acceptance |
| Approved security control or abuse-case verification | Security with explicit target authorization and safety limits |
| Performance/capacity, resilience, migration, accessibility, operations | Relevant non-functional type and specialist |
| Existing behavior affected by direct or transitive change | Regression across the selected underlying levels |

Do not duplicate every scenario at every level. Use broader tests for boundaries and journeys that lower-level tests cannot prove. A test with mocked adapters remains a unit/component test; an integration test exercises at least one real integration boundary with representative behavior.

Escalate level when the risk depends on framework configuration, transaction behavior, serialization, network protocol, database semantics, broker delivery, cache consistency, security enforcement, deployment topology, or multiple components collaborating.
