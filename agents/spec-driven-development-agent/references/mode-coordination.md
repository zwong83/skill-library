# SDD Mode Coordination

The SDD Coordinator owns mode selection, source/readiness state, authorization boundaries, specialist handoffs, lifecycle status, and final reporting.

## Mode routing

| Mode | Specialist | Production code |
|---|---|---|
| Explore | `openspec-planning-agent` | No |
| Propose | `openspec-planning-agent` | No |
| Review | `openspec-planning-agent` | No |
| Test Analysis (TA) | `test-analysis-agent` | No |
| Apply | `implementation-agent` | Yes, only after apply readiness and explicit authorization |
| Regression | `regression-testing-agent` | No production corrections; test changes require Apply authorization and owning specialist |
| Converge | `convergence-review-agent` | No corrections without separate authorization |
| Archive | Coordinator after convergence and explicit archive authorization | No |

## Handoff packet

Pass only the selected change's relevant context:

- requested mode and delivery state;
- project root, applicable instructions, OpenSpec executable/version, active schema, and selected change;
- governing source paths, versions, statuses, and unresolved-item result;
- artifact status, strict-validation result, and dynamic instruction/context paths;
- approved scope and System Design decisions;
- TA artifact/status, complete case matrix, case-task-specialist mapping, and test-level/type allocation when applicable;
- specialist prerequisites, expected reports/evidence, and current unit/integration/contract/UI/system-E2E/performance/security/regression status;
- routing matrix for implementation concerns;
- authorization already granted and actions still requiring authorization;
- evidence destination and known risks.

Specialists return updated status, artifacts or files changed, exact verification, limitations, drift/conflicts, evidence, and next action. They must not broaden authorization or silently modify upstream decisions.
