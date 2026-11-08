# Journey and Boundary Matrix

For each journey record:

| Field | Content |
|---|---|
| Traceability | source/TA IDs, actor, business goal, priority, owner |
| Start | identity/tenant, authoritative initial state, configuration/feature state, input/data |
| Path | ordered components/services/interfaces/stores/async stages and external dependencies |
| Oracle | visible outcome, authoritative state, events, forbidden effects, telemetry, completion deadline |
| Variants | positive, material negative/boundary, authorization/isolation, duplicate, partial failure, recovery |
| Evidence | commands/job, correlation ID, artifacts, cleanup, result, defect disposition |

Include a journey only when its risk cannot be proven by unit, integration, contract, or UI-component evidence. Avoid duplicating every data partition at E2E level.
