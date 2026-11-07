---
name: sdd-standard
description: Run OpenSpec-backed Spec-Driven Development from an approved requirements, System Analysis, and System Design baseline through proposal, delta specs, design delta, tasks, implementation, convergence, and archive. Use for implementation-bound feature changes; do not use to create upstream BRD, PRD, SA, or SD artifacts.
---

# OpenSpec-Backed Spec-Driven Development

Use this skill to turn an approved requirements and design baseline into a persistent, executable, and verifiable OpenSpec change. The governing principle is:

```text
Approved intent and design -> OpenSpec change artifacts -> Tasks -> Code and tests -> Convergence -> Archive
```

SDD is the delivery process, not one additional monolithic document. The default deliverable is an OpenSpec change directory whose artifacts remain traceable to BRD, PRD, SRS/FRS, SA, and SD sources.

This skill requires the OpenSpec CLI with the `spec-driven` schema or a compatible project schema.

## Lifecycle position and boundaries

```text
BRD -> PRD -> SRS/FRS -> SA -> SD -> SDD/OpenSpec -> Implementation -> Verification
```

- BRD, PRD, SRS/FRS, SA, and SD remain authoritative for their respective concerns.
- OpenSpec `proposal.md` records the current change, not the whole product case.
- OpenSpec capability specs state the testable behavior changed by this change.
- OpenSpec `design.md` records the implementation-level design delta and decisions; it must not duplicate or silently replace the approved SD.
- OpenSpec `tasks.md` is the ordered execution plan, not a requirements source.
- Code and tests do not supersede the approved artifacts. If they diverge, fix the originating artifact and regenerate downstream work before continuing.

Do not use this skill for unconstrained ideation, upstream business/product definition, standalone system analysis, standalone system design, deployment execution, or release approval.

## OpenSpec dependencies

Use the installed OpenSpec CLI as the authority for the active schema, artifact graph, templates, output paths, status, and apply context. Never assume that every project uses the default file set.

The CLI must be installed and executable before any project context, schema, or change command runs. Read [references/openspec-bootstrap.md](references/openspec-bootstrap.md) when OpenSpec availability, installation, version, PATH, or initialization is unknown. CLI installation and project initialization are separate state-changing operations with separate authorization gates.

When available, route work through these companion skills:

- `openspec-explore` for exploration and clarification without implementation;
- `openspec-propose` for creating a change and its apply-required artifacts;
- `openspec-apply-change` for implementing tasks from the selected change;
- `openspec-archive-change` for syncing delta specs and archiving only after this skill's convergence gate passes.

If a companion skill is unavailable, follow the equivalent OpenSpec CLI instructions. Do not claim that an OpenSpec project, change, artifact, or status exists without checking it.

## Non-negotiable rules

- Read [references/input-and-readiness-gates.md](references/input-and-readiness-gates.md) before proposing, applying, converging, or archiving a change.
- Do not silently install, upgrade, or switch the OpenSpec CLI. Detect the local version without a network update check; if unavailable or incompatible, report the exact state and follow the bootstrap gate.
- Block implementation readiness when a material `Assumption`, `TBC`, `TBD`, `Open Question`, `Pending Approval`, unresolved conflict, missing acceptance criterion, or missing owner remains in an applicable source.
- Do not invent scope, behavior, interface contracts, data ownership, security controls, NFR targets, migration policy, operational ownership, or approval status.
- Invoke/read `software-security-standard` in SDD/implementation mode when a change affects identity, authentication, authorization, tenant/data isolation, sensitive data, cryptography, key/secrets, validation, audit, privacy, dependencies, deployment security, abuse resistance, or security evidence. Preserve approved SD decisions and update the owning upstream artifact before changing security architecture.
- Invoke/read `api-design-standard`, `database-persistence-standard`, and `resilience-standard` in SDD/implementation mode when applying approved API, persistence, or resilience decisions. Use them for concrete mappings and conformance; return material protocol/contract, data ownership/store/transaction, or failure/recovery strategy changes to System Design.
- No production implementation may begin until all apply-required artifacts are complete, strict validation passes, the unresolved gate passes, and the user explicitly authorizes implementation.
- Explicit Apply authorization includes the approved code/tests plus routine task-status and verification-evidence updates inside the selected change that are necessary to keep execution traceable. It does not include upstream requirement/spec/design changes, new scope, main-spec synchronization, archive, Git operations, deployment, or unrelated artifacts.
- Task completion is not convergence. Do not archive solely because every checkbox is marked complete.
- If implementation exposes a specification or design defect, pause implementation, update the artifact that owns the decision, revalidate, update affected tasks, and then resume.
- OpenSpec CLI installation/update, shell or PATH modification, project initialization, artifact creation, code modification, commits, pushes, specification synchronization, and archive operations are state-changing actions; obtain the authorization required by the active environment immediately before performing them.

## Task modes

Classify the request before acting:

| Mode | Outcome |
|---|---|
| Explore | Clarify the problem or investigate the codebase; no application code is written. |
| Propose | Create or complete an OpenSpec change and its apply-required artifacts. |
| Review | Evaluate source readiness, artifact quality, traceability, and OpenSpec validation without implementation. |
| Apply | Implement authorized tasks from an apply-ready change with tests. |
| Converge | Compare implementation and evidence against proposal, specs, design, and tasks. |
| Archive | Sync applicable delta specs and archive a converged change. |

If the requested mode or change is ambiguous, inspect `openspec list --json` and ask the user to select rather than guessing.

Task mode and delivery state are independent. For example, an agent may enter `Explore` mode while the delivery state remains `Blocked`; exploration does not make the change apply-ready.

## Workflow

### 1. Establish request and source readiness

Classify the requested mode, identify the proposed project/change, and run the mandatory-input and unresolved-item checks before initializing OpenSpec or creating a change. Read-only CLI availability and context checks are allowed, but an upstream readiness failure must be reported before requesting initialization.

If a material source is missing or unresolved, set the delivery state to `Blocked`. Explore mode may be used to resolve the gap, but no OpenSpec initialization, proposal creation, or implementation may proceed.

### 2. Establish OpenSpec context

1. Detect the OpenSpec executable and local version without requesting an online update check. Prefer `openspec version --json` when supported and fall back to `openspec --version`; validate structured output before relying on it.
2. If the command is unavailable, report `Blocked: OpenSpec CLI unavailable`, read [references/openspec-bootstrap.md](references/openspec-bootstrap.md), identify an official/project-approved installation source and proposed version/scope, and obtain authorization before installing. After installation, verify the resolved executable and version before continuing.
3. Record the executable, version, install scope/method when discoverable, and any project compatibility constraint. Do not silently upgrade an installed version.
4. Run `openspec list --json` as a read-only project-context check.
5. Interpret the result without guessing:
   - explicit missing-project/change-directory result -> `OpenSpec state: Uninitialized`;
   - other non-success result -> `Blocked: OpenSpec context error` with the exact error;
   - successful result -> record active changes and continue.
6. Before initialization, report:

   ```text
   OpenSpec state: Uninitialized
   Intended schema: <proposed schema>
   Active schema: None
   ```

   An intended schema is not an active schema and must not be reported as selected or validated.
7. For an existing change, run:

   ```bash
   openspec status --change "<change-name>" --json
   ```

8. Read `schemaName`, `applyRequires`, artifact dependencies, and statuses from a successful response. Missing fields or invalid JSON are an OpenSpec context error, not permission to assume defaults.
9. If the project is not initialized and the source-readiness gate has passed, explain the state and obtain separate authorization before running `openspec init` from the intended project root. Do not treat CLI installation as authorization to initialize a project.

### 3. Complete the source-readiness gate

Identify and completely read every mandatory and applicable conditional input. Record the exact source, version, status, and owner. Scan for unresolved items and contradictions across the requirements, SA, SD, existing code behavior, and active OpenSpec artifacts.

If a material issue remains, stop at `Blocked`, provide a decision-needed register, and use Explore mode to resolve it. Do not create an implementation-ready claim from assumptions.

### 4. Create or complete the OpenSpec change

For a new change, derive or obtain a kebab-case change name and create it only after checking for collisions. Use OpenSpec's artifact graph rather than hard-coding order:

```bash
openspec new change "<change-name>"
openspec status --change "<change-name>" --json
openspec instructions <artifact-id> --change "<change-name>" --json
```

For each `ready` artifact:

1. Read its instruction, template, rules, output path, and completed dependencies.
2. Apply the artifact contract in [references/openspec-artifact-contract.md](references/openspec-artifact-contract.md).
3. Create the artifact at the returned output path.
4. Re-run status and continue until every artifact listed in `applyRequires` is complete.

For OpenSpec's default `spec-driven` schema, the normal dependency flow is:

```text
proposal -> capability specs -> design -> tasks
```

### 5. Validate and approve implementation readiness

Before implementation:

1. Run OpenSpec strict validation for the selected change:

   ```bash
   openspec validate "<change-name>" --type change --strict --no-interactive --json
   ```

2. Confirm every apply-required artifact is complete.
3. Confirm every changed behavior has testable scenarios and every task traces to a requirement and design decision where applicable.
4. Re-run the unresolved and cross-artifact consistency gates.
5. Present the scope, risks, planned tasks, validation result, and remaining non-blocking limitations.
6. Obtain explicit user authorization to implement. Artifact approval and implementation authorization are separate decisions.

### 6. Apply tasks

Use OpenSpec's dynamic apply instructions:

```bash
openspec instructions apply --change "<change-name>" --json
```

- Read every path returned in `contextFiles` before changing code.
- Implement one bounded task at a time and keep changes within the approved scope.
- Add or update tests as required by the related scenarios and design.
- Treat the approved System Design as authoritative. Use specialized skills below to map approved decisions into implementation and verify conformance, not to reopen architecture or strategy. If a task requires a material change to architecture/paradigm, module/layer boundaries, dependency direction, public interfaces, data or transaction ownership, security posture, cache/messaging strategy, major failure behavior, deployment, or observability strategy, stop and update/approve SD before continuing.
- Invoke `clean-code-standard` as the implementation-quality entrypoint when a task writes, refactors, or reviews production code. It owns naming and function/control-flow review and conditionally invokes `layered-architecture-standard`, `error-handling-standard`, `code-comments`, `solid-principles`, and `design-patterns` only when their specific concerns are present.
- Invoke `api-design-standard` when implementing approved handlers, controllers, resolvers, services, serializers, validators, authentication/authorization mappings, errors, idempotency, pagination, limits, versioning, client contracts, or contract tests. Do not change the approved API strategy or externally observable contract silently.
- Invoke `database-persistence-standard` when implementing approved records/entities, repositories, queries, indexes, transactions, isolation, migrations, backfills, pool settings, retention, backup/restore hooks, or persistence tests. Do not change approved ownership, datastore, invariants, or consistency strategy silently.
- Invoke `resilience-standard` when implementing approved deadlines, cancellation, retry parameters, circuits, bulkheads, concurrency/queue bounds, backpressure, rate limits, degradation, probes, reconciliation, failover, alerts, or resilience tests. Do not change the approved resilience or recovery strategy silently.
- Invoke `caching-standard` when implementing approved cache keys, value schemas, TTL/refresh, invalidation, consistency, fallback, Redis integration, or cache observability; do not introduce or change cache strategy in SDD.
- Invoke `messaging-standard` when implementing approved message contracts, topics/exchanges/queues/groups, producer/consumer behavior, acknowledgements/offsets, idempotency, ordering, retries, dead letters, or replay. Load only the selected broker reference and do not change messaging strategy in SDD.
- Invoke `software-security-standard` to implement and verify approved security controls. Include negative authorization/isolation scenarios with authoritative tenant/context binding, forbidden-side-effect assertions, replay/duplicate/concurrency behavior, key/secret and control-failure behavior, safe errors/telemetry, dependency/configuration checks, and required evidence; do not change security posture in SDD.
- Invoke `logging-standard` and `tracing-standard` to map approved observability contracts to concrete runtime events, audit/security evidence, span boundaries, propagation, sampling, correlation, and tests. Invoke `code-comments` only where approved intent, contracts, invariants, concurrency, security, compatibility, algorithms, or workarounds are not clear from code alone.
- Mark a task complete only after its code and required verification pass.
- Persist routine implementation and verification evidence within the selected change as part of authorized Apply work. If evidence reveals a requirements, capability-spec, or design defect, stop and correct the owning artifact through its separately authorized mode before continuing.
- Pause on ambiguity, failing prerequisites, design drift, out-of-scope impact, or unresolved security/operational concerns.
- Keep proposal, specs, design, tasks, code, and tests synchronized by correcting the owning artifact first.

### 7. Run convergence

After implementation, read and execute [references/convergence-gate.md](references/convergence-gate.md). Convergence must verify the complete chain:

```text
Source requirement
  -> OpenSpec capability requirement/scenario
  -> Design decision
  -> Task
  -> Code change
  -> Test or other verification evidence
```

Record the result as `Converged` or `Not Converged`. If the active schema has no verification artifact, store evidence in a project-approved change-local or review artifact and clearly label it as an SDD extension rather than a built-in OpenSpec artifact.

An explicitly authorized Converge mode includes routine persistence of convergence evidence for the selected change, but not code corrections, upstream artifact changes, main-spec synchronization, or archive.

### 8. Sync and archive

Archive only when:

- all required artifacts are complete;
- all in-scope tasks are genuinely complete;
- strict OpenSpec validation passes;
- convergence is `Converged`;
- delta-spec synchronization has been assessed;
- material exceptions are resolved or explicitly removed from the release scope;
- the user authorizes the archive action.

Use the OpenSpec archive workflow so applicable delta specs are compared with main specs before the change directory is moved. Preserve all artifacts and verification evidence in the archive.

## Status model

Use these delivery states consistently:

| State | Meaning |
|---|---|
| `Exploring` | The problem or solution is still being clarified; no implementation is allowed. |
| `Blocked` | A mandatory input, material decision, artifact, or approval is missing. |
| `Draft` | Change artifacts exist but are not apply-ready. |
| `Apply-Ready` | Inputs and artifacts passed all readiness gates; implementation still requires authorization. |
| `Implementing` | Authorized tasks are being executed. |
| `Implemented-Not-Verified` | Tasks are marked complete but convergence has not passed. |
| `Converged` | Implementation and evidence satisfy the approved artifact set. |
| `Archived` | The converged change has been synchronized as applicable and archived. |

Never equate `all_done` task status with `Converged`.

## Deliverables

Use the paths returned by OpenSpec. Under the default schema, a change normally contains:

```text
openspec/changes/<change-name>/
├── .openspec.yaml
├── proposal.md
├── specs/<capability>/spec.md
├── design.md
├── tasks.md
└── verification.md             # optional SDD extension when the schema has no verification artifact
```

The final delivery summary must identify the selected change and schema, source baseline, artifact status, strict-validation result, task progress, convergence verdict, outstanding items, delta-spec sync status, and next authorized action.
