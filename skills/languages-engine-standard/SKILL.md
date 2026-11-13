---
name: languages-engine-standard
description: Select or review frontend and backend languages and frameworks, database engines, and query languages or interfaces from project requirements. Use for stack selection, material technology changes, and evidence-based confirmation of an existing stack.
---

# Languages and Database Engine Standard

Choose the best-fit combination for the project's actual frontend surfaces, backend workloads, and persistent data. Treat languages, runtimes, frameworks, database engines, and query interfaces as separate decisions with compatibility dependencies. A framework, runtime, or ORM may constrain a choice and should be recorded when it matters.

## Mandatory workflow

**Complete steps 1 through 8 in order for every selection or review.** Record an outcome for every step. Use `Not applicable` with a reason when a surface, service, or datastore is outside scope or unnecessary. Mark a decision `Blocked` when a missing requirement or unverified capability prevents a defensible choice. Continue independent decisions and hold dependent work.

1. **Identify the decisions in scope.** Use the governing requirements, System Analysis, and approved design or current stack where available. Identify each affected frontend surface, backend workload, and durable datastore. For an existing system, compare retaining the current stack with viable changes when there is a material reason to reconsider it.
2. **Separate hard requirements from preferences.** Record source IDs or evidence. Capture applicable target platforms, runtime and hosting constraints, integrations, performance and resource budgets, data guarantees, availability and recovery objectives, team skills, licensing, cost, and maintenance commitments. Clarify missing inputs only when they can change the decision.
3. **Select or confirm the frontend language and framework for each surface.** Compare plausible pairings using [frontend language criteria](references/selection-criteria.md#frontend-language). Verify the target runtime, rendering or distribution model, and platform capabilities needed for the required journeys.
4. **Select or confirm the backend language and framework for each workload.** Use [backend language criteria](references/selection-criteria.md#backend-language) to compare pairings by runtime and deployment fit, integrations, workload behavior, and ownership. Add a language only when a distinct workload or constraint justifies supporting it.
5. **Select or confirm the database engine for each durable workload.** Start with the data model, access patterns, transaction and consistency guarantees, scale, and recovery needs. Compare plausible engines and deployment modes using [database engine criteria](references/selection-criteria.md#database-engine). Justify any additional engine with a concrete requirement and an ownership plan.
6. **Select or confirm the query language or interface for each engine.** Use [query language and interface criteria](references/selection-criteria.md#query-language-and-interface). Record the native language and dialect when one applies, or the supported query API when the engine uses one. Verify that required reads, writes, transactions, and migrations work with the chosen engine version and backend driver. Record an ORM, query builder, or SDK separately when it affects those guarantees.
7. **Check the combination end to end.** Validate the frontend-to-backend contract and the backend-to-database driver, engine, and query compatibility. Check build and deployment targets and upgrade or migration impact where applicable. Use existing evidence or official version-specific documentation for hard requirements. Specify a focused prototype or benchmark with acceptance criteria if documentation cannot establish a material capability. Revisit affected choices when the combination fails a hard requirement.
8. **Record the decision and its readiness.** For each choice, state the requirement that decided it, the material tradeoff, and the evidence or outstanding check. Mark choices that depend on unresolved requirements or checks as provisional. An unresolved hard requirement blocks implementation readiness for the affected scope. Record who owns each blocker and the next action. Carry material changes to an approved stack into its owning System Design decision.

For steps 3 through 6, use the relevant candidate table to build a shortlist. Include other candidates when a requirement makes them plausible. Discard candidates that fail hard requirements before comparing the remaining options. Rank viable choices by the project's priorities and choose the simplest combination that satisfies them. Use the existing stack as evidence when relevant and account for migration and ongoing support costs.

For steps 3 and 4, record the language and framework separately. Verify that the specific framework version supports the chosen language, runtime, and deployment target. Record the standard library or platform APIs as the choice when they cover the requirements.

## Reference routing

Read only the linked sections for decisions in scope. Use official documentation for the shortlisted technologies when verifying capabilities, versions, support, or compatibility. Once choices are made, use `frontend-architecture-standard` for frontend boundaries, `backend-layered-architecture-standard` for backend module layering, and `db-standard` for detailed persistence design or implementation when those tasks are in scope.

## Expected output

Return a numbered record of the eight steps and a decision table with columns for scope, choice, deciding requirements, alternatives and material tradeoffs, and evidence or pending verification. Identify relevant framework, runtime, engine, dialect, or driver versions where they affect the decision. Distinguish a recommendation from an approved stack decision and an executed verification from a planned check.
