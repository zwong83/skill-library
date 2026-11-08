# System Design Specialist Routing

Classify each profile as `Required`, `Conditional`, or `Not Applicable`. Record the trigger, source IDs, selected specialist/skills, and rationale. Do not load a profile merely because its section exists in the template.

| Profile | Trigger | Specialist | Lazy-loaded skills |
|---|---|---|---|
| Architecture | Components, modules, layers, dependency direction, composition, transactions, topology, OO model, or pattern choice changes | `architecture-agent` | `layered-architecture-standard`; conditional `object-oriented-design`, `design-patterns`, `plantuml-syntax` |
| Interface and data | API/service contracts, durable data, transactions, cache, messaging, consistency, or boundary errors change | `interface-data-agent` | Conditional `api-design-standard`, `database-persistence-standard`, `caching-standard`, `messaging-standard`, `error-handling-standard`, `plantuml-syntax` |
| Quality attributes | Security/privacy, resilience/recovery, latency/throughput, capacity, scalability, or abuse/failure risk is material | `quality-attributes-agent` | Conditional `software-security-standard`, `resilience-standard`, `performance-capacity-standard`, `plantuml-syntax` |
| Delivery and operations | Configuration/secrets, build/promotion, deployment/release, telemetry, alerts, runbooks, incidents, support, or readiness changes | `delivery-operations-agent` | Conditional `configuration-management-standard`, `deployment-release-standard`, `operability-standard`, `logging-standard`, `tracing-standard`, `plantuml-syntax` |
| Independent review | Full SD draft, readiness claim, or explicit audit | `system-design-review-agent` | System Design quality gate and conditional `testing-strategy-standard` |

## Routing rules

- A profile may be `Not Applicable` only with a reason tied to scope and sources.
- Cross-profile dependencies are passed as decision IDs or packet summaries, not by loading another profile's full skills.
- Error semantics belong primarily to Interface/Data; retry and recovery policy belongs primarily to Quality Attributes.
- Security posture belongs to Quality Attributes; concrete secret/config delivery belongs to Delivery/Operations.
- The Review profile consumes packets and the merged draft. It does not reload every specialist skill.
- For a small change, route only the affected profile plus review when readiness is claimed.
- For a broad design, profiles may run independently from the same baseline; the Coordinator resolves conflicts before merge.
