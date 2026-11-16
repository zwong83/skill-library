# OpenSpec Mode Boundaries

The user independently invokes specification management, implementation and testing. This contract governs only OpenSpec artifact work. It is not a mandatory handoff contract for coding or testing agents.

| Mode | Owner | Permitted scope |
|---|---|---|
| Explore / Propose / Review | OpenSpec agent, optionally openspec-planning-agent | Inspect sources and create/review/validate specification artifacts. |
| Handoff | OpenSpec agent | Export approved tasks, source/design/contract versions and optional observed apply instructions. |
| Converge | OpenSpec agent | Read supplied implementation snapshots and retained testing evidence; compare to specifications. |
| Sync / Archive | OpenSpec agent | Explicitly authorized specification synchronization/archive after applicable gates. |

There is no Apply coding, Test Analysis or Regression execution mode here. Do not spawn external workflows or execute their checks to fill missing evidence. Suggest the appropriate independent invocation to the user. Only the artifact-planning specialist may be delegated within this workflow, respecting actual depth/slots and exclusive artifact writes; sequential artifact work is a fallback.

A compact artifact handoff contains project/change identity, active schema where available, source/design/contract versions, bounded tasks and acceptance criteria, expected evidence, current artifact status/validation and unresolved decisions. OpenSpec paths/IDs are optional context to receiving workflows rather than their universal prerequisites.

Evidence returned by other workflows must identify the exact revision/snapshot, scope/cases, environment, commands and observed results, limitations and owner. Record missing or stale evidence without claiming success. Independent workflows may operate on compatible stable baselines; conflicting artifact/code writes or changed contracts require explicit reconciliation. Approval and authorization do not transfer automatically with a handoff.
