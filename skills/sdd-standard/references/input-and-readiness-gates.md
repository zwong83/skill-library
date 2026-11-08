# SDD Inputs and Readiness Gates

Use this reference before proposing, analyzing tests, applying, converging, or archiving an OpenSpec change.

## Input classification

### Mandatory inputs

For every mode:

- task mode: Explore, Propose, Review, Test Analysis, Apply, Regression, Converge, or Archive;
- project root and feature/change identity;
- OpenSpec CLI state, resolved executable, locally detected version, install scope/method when discoverable, and compatibility status; if unavailable, record the proposed official/project-approved installation source, version, scope, and authorization state;
- OpenSpec context state; when initialized, include the active schema and change status; when uninitialized, record `Active schema: None` and separately identify any intended schema as proposed;
- source-document locations, versions, statuses, and owners;
- applicable project instructions, coding standards, test commands, and validation commands.

For a new or behavior-changing feature:

- approved System Analysis defining scope, actors, logical behavior, flows, states, integrations, and ownership;
- approved System Design defining technical boundaries, interfaces, data design, security, reliability, operations, and implementation constraints;
- approved SRS and FRS requirements and acceptance criteria when the project lifecycle maintains those artifacts;
- current code and test baseline for the affected scope.

If the project does not maintain a separate SRS or FRS, an authorized product/engineering owner must explicitly record `Not Applicable`, provide the rationale, and identify the equivalent normative source that contains complete, testable requirements and acceptance criteria. The agent must not decide non-applicability from absence alone, and a PRD may substitute only when this equivalence is explicitly approved.

For Apply mode:

- a selected OpenSpec change;
- complete apply-required artifacts;
- passing strict OpenSpec validation;
- applicable `TA-Ready` Test Analysis with complete case-to-task-to-specialist allocation, or a recorded and approved `Not Applicable` rationale;
- for frontend work, approved frontend SD decisions and the applicable versioned frontend/backend interface recorded as `Contract-Ready`;
- explicit implementation authorization.

For Regression mode:

- the selected change and approved TA matrix;
- known base and target revisions plus the actual changed-file/diff scope;
- available suite inventory, historical baseline, required environments/data/dependencies, and known flaky/quarantined tests;
- completed specialist evidence required before the regression verdict;
- authorization for any test execution or environment use not already covered.

For Converge mode:

- the complete approved OpenSpec artifact set;
- implementation diff or exact changed-file set;
- task completion state;
- unit, integration, contract, UI, system/E2E, performance, security, regression, static-analysis, build, migration, and operational evidence required by the change.

For Archive mode:

- a `Converged` verdict;
- completed required artifacts and tasks;
- delta-spec sync assessment;
- explicit archive authorization.

### Conditional inputs

These become mandatory when they affect the change:

- BRD and PRD for business scope, outcomes, policy, user behavior, or release acceptance;
- Change Request for modifications to approved or deployed behavior;
- UX specifications for user-interface behavior;
- API, event, schema, and integration contracts;
- security, privacy, legal, compliance, data-classification, retention, and audit requirements;
- performance, capacity, availability, consistency, recovery, observability, deployment, rollout, rollback, migration, and operational constraints;
- existing main OpenSpec capability specs when modifying behavior;
- ADRs, platform standards, vendor constraints, compatibility requirements, and deprecation policy;
- dependency repositories or multi-application plans when the change crosses boundaries.

Record an applicable conditional input as `Not Applicable` only with a reason. Absence is not evidence of non-applicability.

### Optional context

- prototypes, benchmarks, examples, diagrams, reference implementations, cost estimates, and preferred libraries;
- exploratory notes that do not establish approved scope or behavior.

Optional context must not silently override an approved source.

## Unresolved-item gate

Search every applicable input and active OpenSpec artifact for:

- `Assumption`, unless explicitly accepted by the authorized owner;
- `TBC`, `TBD`, `TODO`, placeholder text, or missing values;
- `Open Question`, `Pending Approval`, `Proposed`, `Draft`, `Unknown`, or unresolved comments;
- contradictory requirements, scenarios, flows, interfaces, data definitions, or NFR targets;
- missing acceptance criteria, error behavior, edge cases, ownership, dependencies, or sign-offs;
- ambiguous migration, compatibility, rollout, rollback, security, privacy, or operational behavior.

An item is material when it can change scope, externally visible behavior, acceptance, interface or data contracts, security/privacy posture, NFR targets, implementation architecture, migration, operations, ownership, cost, schedule, or release safety.

If any material item is unresolved:

1. Set the state to `Blocked`.
2. Do not declare artifacts apply-ready and do not implement.
3. Produce a decision-needed register:

   | Source | ID/Section | Unresolved item | Impact | Decision required | Owner |
   |---|---|---|---|---|---|

4. Resolve it in the authoritative upstream source or OpenSpec artifact.
5. Re-read affected downstream artifacts and rerun validation.

## Cross-artifact consistency gate

Before `Apply-Ready`, verify:

- proposal scope matches the approved source baseline;
- capability names and delta specs match the proposal;
- each requirement is unambiguous, testable, and represented by at least one scenario;
- design decisions satisfy the requirements and do not contradict the approved SD;
- tasks cover every in-scope requirement, design change, test, migration, documentation, and operational action;
- applicable TA cases cover positive and applicable negative/boundary partitions, allocate material risks to justified test levels/specialists, and map to implementation tasks and expected evidence;
- no task introduces behavior absent from the approved specs;
- removals and renames include compatibility and migration handling where applicable;
- traceability identifiers are stable and complete;
- OpenSpec strict validation passes.

## Readiness verdict

Return exactly one verdict:

- `Blocked` — mandatory input, material decision, approval, or dependency is missing.
- `Draft` — inputs are sufficient for artifact work, but artifacts or validation are incomplete.
- `Apply-Ready` — all gates pass; code changes still require explicit authorization.

Include evidence for the verdict. Do not infer approval from silence, document presence, or a completed task list.
