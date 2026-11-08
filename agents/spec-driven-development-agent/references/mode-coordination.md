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
| Converge | `convergence-review-agent` | No corrections without separate authorization |
| Archive | Coordinator after convergence and explicit archive authorization | No |

## Handoff packet

Pass only the selected change's relevant context:

- requested mode and delivery state;
- project root, applicable instructions, OpenSpec executable/version, active schema, and selected change;
- governing source paths, versions, statuses, and unresolved-item result;
- artifact status, strict-validation result, and dynamic instruction/context paths;
- approved scope and System Design decisions;
- TA artifact/status, scenario-task mapping, and test-level allocation when applicable;
- routing matrix for implementation concerns;
- authorization already granted and actions still requiring authorization;
- evidence destination and known risks.

Specialists return updated status, artifacts or files changed, exact verification, limitations, drift/conflicts, evidence, and next action. They must not broaden authorization or silently modify upstream decisions.
