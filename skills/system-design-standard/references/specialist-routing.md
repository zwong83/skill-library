# System Design Specialist Routing

Classify each profile as `Required`, `Conditional`, or `Not Applicable`. Record the trigger, source IDs, selected specialist/skills, and rationale. Do not load a profile merely because its section exists in the template.

| Profile | Trigger | Specialist | Lazy-loaded skills |
|---|---|---|---|
| Architecture | Current/target context, components, modules, layers, dependency direction, composition, transactions, deployment/middleware topology, OO model, or pattern choice changes | `architecture-agent` | `backend-layered-architecture-standard`; conditional `object-oriented-design`, `design-patterns`, `plantuml-syntax` |
| Interface and data | API/service contracts, logical/physical data model, proposed DDL/DML, access paths, transactions, migration, cache, messaging, consistency, or boundary errors change | `interface-data-agent` | Conditional `backend-api-design-standard`, `db-standard`, `cache-standard`, `message-standard`, `exception-error-standard`, `plantuml-syntax` |
| Frontend design | Web UI, frontend application, rendering/routing, component/state/data, UX engineering, browser, accessibility, frontend performance/security/observability/delivery concerns are in scope | `frontend-design-agent` | Conditional `frontend-architecture-standard`, `frontend-component-design-standard`, `frontend-state-data-standard`, `frontend-experience-standard`, `frontend-performance-standard`, `frontend-security-standard`, `frontend-observability-standard`, `frontend-build-delivery-standard`, `plantuml-syntax` |
| Quality attributes | Security/privacy, resilience/recovery, latency/throughput, capacity, scalability, or abuse/failure risk is material | `quality-attributes-agent` | Conditional `software-security-standard`, `backend-resilience-standard`, `backend-performance-capacity-standard`, `plantuml-syntax` |
| Delivery and operations | Configuration/secrets, build/promotion, deployment/release, telemetry, alerts, runbooks, incidents, support, or readiness changes | `delivery-operations-agent` | Conditional `backend-configuration-management-standard`, `deployment-release-standard`, `backend-operability-standard`, `log-trace-standard`, `plantuml-syntax` |

## Routing rules

- A profile may be `Not Applicable` only with a reason tied to scope and sources.
- Every feature must have one owning specialist and target document for its technical-flow diagram. Conditional state/data/middleware/frontend views must be assigned when applicable.
- Architecture owns system-level As-Is/problem/To-Be structure and target topology; Interface/Data owns physical data, DDL/DML, transaction, database/cache/message behavior; Delivery/Operations owns deployable runtime topology and operational realization. The Coordinator reconciles shared topology views.
- Cross-profile dependencies are passed as changed decision IDs or compact handoffs, not by loading another profile's full skills or full reasoning.
- Error semantics belong primarily to Interface/Data; retry and recovery policy belongs primarily to Quality Attributes.
- For frontend scope, Interface/Data supplies backend authority and the draft contract; Frontend Design supplies journey-driven contract feedback and client design. The Coordinator owns `Contract-Ready` reconciliation before parallel detail.
- Security posture belongs to Quality Attributes; concrete secret/config delivery belongs to Delivery/Operations.
- The Coordinator applies the quality gate to the Index, applicable Backend/Frontend/Integration documents, machine-readable contracts, and unresolved open decisions. Use specialist evidence only where needed to resolve a gap.
- For a small change, route only the affected profile. The Coordinator applies the quality gate when readiness is claimed.
- For a broad design, profiles may run independently from the same minimal baseline; the Coordinator writes accepted decisions directly to their authoritative target and resolves conflicts before readiness.
