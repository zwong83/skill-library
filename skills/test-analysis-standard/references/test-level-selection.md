# Test Level Selection

Choose the lowest level that exercises the real risk with a trustworthy oracle.

| Question | Prefer |
|---|---|
| Isolated backend/frontend rule, calculation, validation, transformation, decision, state transition, local invariant | Logic unit; unit-testing-agent outside active TDD |
| Logic across real framework mapping, serialization, repository query, database constraint, broker/cache or service adapter | Integration; integration-testing-agent outside active TDD |
| Provider/consumer schema, protocol, semantic, or version compatibility | Contract |
| User-visible component state, DOM/widget interaction, visual, accessibility, browser/device behavior | UI at the smallest trustworthy layer; ui-testing-agent outside active TDD |
| Critical multi-component journey or deployed-system behavior | System/end-to-end |
| Business acceptance and policy outcome | Acceptance |
| Approved security control or abuse-case verification | Security with explicit target authorization and safety limits |
| Performance/capacity or performance regression | Performance with `performance-testing-standard`; plan execution prerequisites and explicit load authorization |
| Resilience, migration, accessibility, operations | Relevant non-functional type and specialist |
| Existing behavior affected by direct or transitive change | Regression across the selected underlying levels |

Do not duplicate every scenario at every level. Use broader tests for boundaries and journeys that lower-level tests cannot prove. A test with mocked adapters remains a unit/component test; an integration test exercises at least one real integration boundary with representative behavior.

Escalate level when the risk depends on framework configuration, transaction behavior, serialization, network protocol, database semantics, broker delivery, cache consistency, security enforcement, deployment topology, or multiple components collaborating.

## Conditional contract and system/E2E testing

Test Analysis records a separate `Required` or `Not Applicable` decision for each of these specialists for every analyzed change. Scope decisions to affected contracts, consumers, versions or journeys; an unchanged endpoint or the mere presence of an API/browser does not trigger both agents. An approved requirement, acceptance criterion or release policy explicitly demanding the testing makes it `Required`.

| Specialist | Required when | Not Applicable when |
|---|---|---|
| `contract-testing-agent` | The change directly or transitively affects a material provider/consumer compatibility commitment that the selected lower-level cases cannot prove. Examples include independently released consumers/providers, public or third-party APIs, multiple supported consumers/versions, rolling-version coexistence, or shared event/message schemas; assess schema, serialization, validation, errors and semantic changes. | No compatibility commitment is affected, or named integration cases demonstrably cover the entire affected consumer/version and semantic obligation with no independent compatibility gap. A single coordinated release may support this decision but is not sufficient by itself. |
| `system-e2e-testing-agent` | The change directly or transitively affects a critical business journey or deployed-system obligation whose cross-component result cannot be proven by the selected lower-level cases. Examples include login-to-purchase/payment/order completion, asynchronous delivery and durable effects, cross-service identity/tenant isolation, recovery, or changed deployment/routing/configuration that can break the assembled journey. | No critical journey/deployed-system obligation is affected, or named lower-level cases cover the affected risk completely and no assembled-system proof is required. A local logic/UI change may qualify only after its downstream impact is assessed. |

For each decision record scope, source/risk IDs, triggering criterion or exclusion rationale, required case IDs or alternative coverage case IDs, evidence criteria, owner and residual gaps. Existing suitable tests may fulfill a `Required` decision; reuse them and retain one execution owner rather than duplicating tests. A UI-driven journey counts as E2E proof only if it also verifies the required authoritative downstream outcomes and effects.

`Not Applicable` is a scope decision, not a passing test result or an accepted omission. Missing tools, environments, credentials, time or permission cannot justify it. When applicability or an oracle is materially unresolved, record an open decision with owner/next action and return `TA-Blocked`. Once scope and cases are resolved, future execution prerequisites may be planned with owners and TA may be ready; missing execution prerequisites still block the required run and any passing claim.

Reassess these decisions when contracts, consumer/version support, journey criticality, dependencies, topology or change impact changes. Test Analysis owns planned applicability. The user independently invokes relevant specialists for Required scopes when execution prerequisites are met; no agent automatically dispatches another workflow. Retain Not Applicable rationale without execution. Explicit standalone testing may use equivalent scope/rationale inputs without a formal TA artifact, while respecting any supplied approved applicability decision. Return new risks as analysis-review requests to the user.
