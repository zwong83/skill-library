---
name: sdd-standard
description: Run OpenSpec-backed Spec-Driven Development from an approved requirements, System Analysis, and System Design baseline through proposal, delta specs, design delta, tasks, implementation, convergence, and archive. Use for implementation-bound feature changes; do not use to create upstream BRD, PRD, SA, or SD artifacts.
---

# OpenSpec-Backed Spec-Driven Development

Use this governing skill to preserve the chain from approved intent to artifacts, code, tests, evidence, convergence, and archive. Select one mode and load only its routed references; do not preload implementation skills during planning.

## Modes

| Mode | Outcome | Routed Agent | Production code |
|---|---|---|---|
| Explore | Clarify sources, code, constraints, and decisions | openspec-planning-agent | No |
| Propose | Create/complete apply-required OpenSpec artifacts | openspec-planning-agent | No |
| Review | Evaluate readiness, artifacts, traceability, validation | openspec-planning-agent | No |
| Test Analysis | Derive the traceable Test Case Matrix and specialist allocation before Apply | test-analysis-agent | No |
| Apply | Implement authorized tasks with tests/evidence | implementation-agent | Yes, after explicit authorization |
| Regression | Select and verify impacted behavior across required test levels | regression-testing-agent | No production corrections |
| Converge | Compare implementation and evidence to all governing artifacts | convergence-review-agent | Corrections require authorization |
| Archive | Synchronize as applicable and archive a converged change | SDD Coordinator | No |

Mode and delivery state are independent. Valid states include Blocked, Drafting, Review-Ready, Apply-Ready, Implementing, Verification-Failed, Not-Converged, Converged, and Archived.

## Non-negotiable gates

- Read [references/input-and-readiness-gates.md](references/input-and-readiness-gates.md) before Propose, Test Analysis, Apply, Regression, Converge, or Archive.
- Block when mandatory sources are missing, unapproved, contradictory, or contain material assumptions, TBC/TBD, open questions, pending approvals, unresolved proposals, missing acceptance criteria, or missing owners.
- For behavior-changing implementation, require approved System Analysis and System Design plus applicable requirements and Change Request.
- Detect the local OpenSpec executable/version without an online update check. Read [references/openspec-bootstrap.md](references/openspec-bootstrap.md) only when installation, compatibility, PATH, or project initialization is unresolved.
- Do not silently install/upgrade OpenSpec, edit PATH, initialize a project, create scope, write code, synchronize specs, archive, commit, push, or deploy.
- Before behavior-changing Apply, require selected change/schema, complete apply-required artifacts, strict validation, `TA-Ready` analysis or justified `Not Applicable`, complete traceability, resolved material implementation concerns, and explicit user authorization.
- Artifact approval is not implementation authorization. Task completion is not convergence.
- If implementation reveals a source or design defect, stop and update the owning artifact through its authorized lifecycle.

## Mode routing

### Explore, Propose, Review

Use [references/openspec-artifact-contract.md](references/openspec-artifact-contract.md) and the active schema's dynamic instructions. OpenSpec determines artifact names, dependencies, templates, paths, and apply requirements. Validate observed structured output before relying on it; never fabricate project, change, schema, artifact, or status.

A normal spec-driven flow may be proposal -> capability specs -> design -> tasks, but the active schema is authoritative.

### Test Analysis

After apply-required artifacts are complete and before behavior-changing Apply, invoke `test-analysis-agent`. Store `test-analysis.md` in the project-approved evidence location and label it supplemental when the active OpenSpec schema does not define it. The TA must contain a complete Test Case Matrix, case-to-task-to-specialist routing, and each specialist's prerequisites/output expectations. TA readiness is not implementation authorization.

### Apply

Read [references/apply-workflow.md](references/apply-workflow.md). Use the current dynamic apply instructions, read every returned context file, implement one bounded approved task at a time, load only task-selected technical skills, and record exact evidence.

### Converge

Read and execute [references/convergence-gate.md](references/convergence-gate.md). Verify:

Source requirement -> capability requirement/scenario -> design decision -> TA case -> task -> specialist test -> code/evidence -> regression result.

Checked tasks or passing unit tests alone do not prove convergence.

### Archive

Archive only after a Converged verdict, delta/main-spec synchronization assessment, and explicit archive authorization. Use the installed OpenSpec version's observed commands and report the exact result. Archive authorization does not imply Git push or deployment authorization.

## Authorization boundaries

Treat installation/upgrade, PATH/profile changes, project initialization, artifact scope changes, production code/tests/config/schema changes, external state changes, Git operations, main-spec synchronization, archive, and deployment/release as distinct actions. Obtain the authorization required by the active environment immediately before each mutation.

Apply authorization covers approved code/tests and routine task/evidence updates inside the selected change. It does not cover upstream redesign, unrelated changes, main-spec synchronization, archive, Git, or deployment.

## Handoff

Every handoff reports mode, delivery state, project/OpenSpec context, selected change/schema, source baseline and unresolved result, artifact/validation status, tasks/files changed when applicable, exact verification, convergence verdict, risks/limitations, evidence location, and the next action with its authorization requirement.

Do not replace BRD, PRD, SRS/FRS, SA, or SD with OpenSpec artifacts. Do not include secrets or private production data, and never report checks or approval that were not observed.
