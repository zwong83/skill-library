# System Design Specialist Routing

Classify each profile as `Required`, `Conditional`, or `Not Applicable`. Record the trigger, source IDs, selected specialist/skills, and rationale. Do not load a profile merely because its section exists in the template.

| Profile | Trigger | Specialist | Lazy-loaded skills |
|---|---|---|---|
| Architecture | Components, modules, layers, dependency direction, composition, transactions, topology, OO model, or pattern choice changes | `architecture-agent` | `layered-architecture-standard`; conditional `object-oriented-design`, `design-patterns`, `plantuml-syntax` |
| Interface and data | API/service contracts, durable data, transactions, cache, messaging, consistency, or boundary errors change | `interface-data-agent` | Conditional `api-design-standard`, `database-persistence-standard`, `caching-standard`, `messaging-standard`, `error-handling-standard`, `plantuml-syntax` |
| Frontend design | Web UI, frontend application, rendering/routing, component/state/data, UX engineering, browser, accessibility, frontend performance/security/observability/delivery concerns are in scope | `frontend-design-agent` | Conditional `frontend-architecture-standard`, `frontend-component-design-standard`, `frontend-state-data-standard`, `frontend-experience-standard`, `frontend-performance-standard`, `frontend-security-standard`, `frontend-observability-standard`, `frontend-build-delivery-standard`, `plantuml-syntax` |
| Quality attributes | Security/privacy, resilience/recovery, latency/throughput, capacity, scalability, or abuse/failure risk is material | `quality-attributes-agent` | Conditional `software-security-standard`, `resilience-standard`, `performance-capacity-standard`, `plantuml-syntax` |
| Delivery and operations | Configuration/secrets, build/promotion, deployment/release, telemetry, alerts, runbooks, incidents, support, or readiness changes | `delivery-operations-agent` | Conditional `configuration-management-standard`, `deployment-release-standard`, `operability-standard`, `logging-standard`, `tracing-standard`, `plantuml-syntax` |
| Independent review | Full SD draft, readiness claim, or explicit audit | `system-design-review-agent` | System Design quality gate and conditional `testing-strategy-standard` |

## Routing rules

- A profile may be `Not Applicable` only with a reason tied to scope and sources.
- Cross-profile dependencies are passed as changed decision IDs or compact handoffs, not by loading another profile's full skills or full reasoning.
- Error semantics belong primarily to Interface/Data; retry and recovery policy belongs primarily to Quality Attributes.
- For frontend scope, Interface/Data supplies backend authority and the draft contract; Frontend Design supplies journey-driven contract feedback and client design. The Coordinator owns `Contract-Ready` reconciliation before parallel detail.
- Security posture belongs to Quality Attributes; concrete secret/config delivery belongs to Delivery/Operations.
- The Review profile consumes the Index, applicable Backend/Frontend/Integration documents, machine-readable contracts, and unresolved open decisions. It does not require specialist handoffs or reload every specialist skill.
- For a small change, route only the affected profile plus review when readiness is claimed.
- For a broad design, profiles may run independently from the same minimal baseline; the Coordinator writes accepted decisions directly to their authoritative target and resolves conflicts before readiness.
