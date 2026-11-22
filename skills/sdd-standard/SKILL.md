---
name: sdd-standard
description: Manage OpenSpec specifications and change artifacts from approved requirements and design, prepare task handoffs, review supplied implementation/testing evidence for convergence, and synchronize or archive explicitly requested changes; does not execute coding or testing workflows.
---

# OpenSpec Specification and Change Management

## Input and output contract

This summary follows the detailed workflow and linked gates below. Record source owners, locations/versions and decision status; keep unknowns explicit.

- **Required inputs:** Requested OpenSpec mode, change/scope, governing source context and action authority.
- **Conditional inputs:** CLI/schema/project context for artifact operations; approved requirements/design for dependent planning; supplied implementation/test evidence for convergence; sync/archive authorization.
- **Optional context:** Prior change examples and supplied TA/task context unless project-required.
- **Outputs:** Mode-specific specification/change/task artifacts, validation/convergence findings and next handoff in project locations.
- **Destination and consumer:** Use the workflow's existing, requested or documented default artifact/handoff location. Return results to the invoking agent or user for the identified downstream owner; this does not authorize automatic invocation or duplicate artifacts.
- **Completion:** Apply mode-specific source/evidence gates; artifact readiness neither authorizes coding nor proves testing.


This skill owns OpenSpec artifacts and their lifecycle, not overall software delivery. The user invokes OpenSpec, Implementation and Testing independently. Requirements/design, task records, code snapshots and evidence connect them; no delivery coordinator or automatic cross-workflow dispatch is implied.

## Modes and responsibility

| Mode | Work owned here |
|---|---|
| Explore | Inspect requirements, design, code context and unresolved decisions without production edits. |
| Propose | Create/update proposal, specs, design mapping and task artifacts under the active schema. |
| Review | Validate artifacts, semantic coverage and source/contract alignment. |
| Handoff | Export approved task/context references for a separately invoked implementation or testing workflow. |
| Converge | Review supplied code snapshot and retained verification evidence against approved specifications. |
| Sync / Archive | Perform explicitly authorized specification synchronization or archive after the applicable gates. |

Implementation, Test Analysis, test execution and Regression are not modes of this workflow. OpenSpec may expose apply instructions: reading/exporting them is Handoff, not permission to implement. Do not invoke implementation or testing agents, edit their code/tests, generate test verdicts, or launch test/build/load/scanning commands. Artifact validation is permitted within this workflow. Evidence review can report missing or inconsistent results; it cannot invent execution or override a failed testing verdict.

## Mandatory workflow

Complete steps 1–7 in order at the depth of the requested mode. Record Complete, Not Applicable with a scope reason, Blocked with owner/next action, or Pending for dependent work. Missing evidence is not a justified exclusion. Revisit affected steps when sources or versions change.

1. Confirm the requested OpenSpec mode, project/change, scope and action authorization. Discover the installed executable/version and active schema locally; do not invent status or silently install/initialize tools.
2. Read [input and readiness gates](references/input-and-readiness-gates.md), the approved source/design/contract baseline and only relevant project/change context. Resolve material ambiguity at its source before dependent artifact work.
3. Read [artifact requirements](references/openspec-artifact-contract.md) and the active schema's dynamic instructions. Preserve its actual paths, dependencies and templates; technical mappings describe approved decisions rather than reselecting them.
4. Perform only the requested artifact action. For Handoff use [task handoff guidance](references/apply-workflow.md); return tasks and optional OpenSpec instructions as data for the user to pass onward. Do not start coding or testing.
5. Validate affected artifacts and semantic traceability. Distinguish a passing OpenSpec validation from complete requirements coverage and from tested software.
6. For Converge, review supplied evidence using [convergence guidance](references/convergence-gate.md). Missing or failing required evidence yields Not Converged with a requested next action. For Sync/Archive require the applicable convergence/sync assessment and explicit authorization, then use the installed tool's observed capabilities.
7. Return changed artifacts, source/version references, exact validation/review evidence, readiness or convergence status, unresolved items and suggested independent next invocation. Do not execute that next workflow automatically.

## Boundaries and outputs

Artifact readiness means the specification/task package is ready to consume; it does not authorize coding or prove test readiness. Retain OpenSpec's observed status names as tool data, not cross-workflow gates. Test plans and results are external inputs when required by the change; a specific TA file/status is not mandatory for every OpenSpec assignment. Required missing verification still prevents convergence/archive.

Use [bootstrap guidance](references/openspec-bootstrap.md) only when installation, compatibility, PATH or initialization is unresolved. Installation, project initialization, code/test changes, external mutations, Git operations, spec synchronization, archive and deployment retain their respective authorization boundaries. Approval of an artifact does not authorize another workflow.

Return the requested mode, project/change/schema, artifact paths/versions, validation, scope and evidence coverage, blockers/owners, and next action. Do not replace governing requirements or System Design with OpenSpec artifacts, expose secrets, or weaken specifications to fit failing code.
