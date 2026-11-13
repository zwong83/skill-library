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
| Converge | Coordinator applies the convergence gate | No corrections without separate authorization |
| Archive | Coordinator after convergence and explicit archive authorization | No |

## Compact handoff envelope

Pass only the selected change's relevant context. Prefer path/version/ID/section references over copied content:

- requested mode and delivery state;
- project root, applicable instructions, OpenSpec executable/version, active schema, and selected change;
- governing source paths, versions, statuses, and unresolved-item result;
- artifact status, strict-validation result, and dynamic instruction/context paths;
- approved scope, SD Index version/status, and only affected Backend/Frontend/Integration decision IDs and contract versions;
- for frontend scope, approved Frontend SD decision IDs, versioned `Contract-Ready` interface, support/experience/quality commitments, and frontend task boundaries;
- TA artifact/status, complete case matrix, case-task-specialist mapping, and test-level/type allocation when applicable;
- specialist prerequisites, expected reports/evidence, and current unit/integration/contract/UI/system-E2E/performance/security/regression status;
- routing matrix for implementation concerns;
- authorization already granted and actions still requiring authorization;
- evidence destination and known risks.

Specialists return only updated status, artifacts/files changed, exact verification, limitations, drift/conflicts, evidence, and next action. Omit repeated source summaries, unchanged decisions, generic explanation, and internal reasoning. Handoffs are transient unless project audit rules require retention. Specialists must not broaden authorization or silently modify upstream decisions.

## Runtime delegation

Delegated Agents do not change lifecycle ordering, ownership, or authorization. The Coordinator starts at most the selected current mode for a change and validates its returned handoff before advancing. The Coordinator runs Converge directly. Other modes with specialists may use runtime delegation or sequential execution.

Pass explicit paths, versions, IDs, bounded tasks/cases, write ownership, expected evidence, and granted authorization because delegated Agents must not depend on hidden parent conversation. Run write-heavy work concurrently only when file/module ownership is disjoint or the runtime provides isolated worktrees; otherwise keep one writer and execute sequentially.
