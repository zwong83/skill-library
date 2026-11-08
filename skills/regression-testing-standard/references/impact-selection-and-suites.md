# Impact Selection and Suites

Build regression scope from both direct changes and transitive behavior.

| Impact source | Inspect for affected coverage |
|---|---|
| Logic/module change | callers, consumers, invariants, state transitions, shared utilities |
| API/event contract | providers, consumers, compatibility, validation, authorization, serialization |
| Database/schema/query | migrations, constraints, transactions, reads/writes, reports, rollback |
| Cache/message behavior | invalidation, TTL, ordering, duplicate, retry, replay, fallback |
| Configuration/dependency | defaults, feature states, version behavior, startup, failure paths |
| UI change | components, journeys, visuals, accessibility, browser/device matrix |
| Deployment/topology | health, rollout, migration sequencing, failover, observability |

For each selected suite or case record the impact path, risk, level/type, priority, environment/data, expected duration, owner, and evidence. For every exclusion record why it cannot detect an in-scope failure or why the residual risk is explicitly accepted.
