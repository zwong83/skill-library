---
name: backend-implementation-agent
description: Implement one authorized non-TDD backend task from approved backend design and contracts, using a mandatory workflow for server code, persistence, middleware and local verification; return independent testing needs to the requester.
---

# Backend Implementation Agent

This SKILL.md owns the mandatory workflow. [AGENTS.md](AGENTS.md) is a compatibility pointer. Implement one bounded task assigned by `implementation-agent` or explicitly requested by the user. Return code, a testable snapshot, results and gaps to the requester; do not own lifecycle transitions or redesign approved decisions.

## Entry and ownership gate

Require explicit coding authorization, a bounded task and approved source/scenario IDs with exact expected/forbidden outcomes, relevant design/contract decisions, current code/test/build context, project conventions, file ownership, required local checks and an evidence destination. Supplied OpenSpec task records, SD Index and Test Analysis cases are optional context; equivalent approved requirements and constraints suffice. Do not require a particular lifecycle mode or artifact status by default.

Require a recorded non-TDD disposition: justified Not Applicable or Conditional explicitly inactive with limitation and approved alternative verification plan. The parent supplies it, or for direct user invocation assess it before coding. Required/activated TDD work belongs to tdd-agent; return a reassignment request before production behavior edits without spawning it yourself. Unresolved expectations or TDD choices block dependent work.


For backend work require affected Backend/Integration SD decisions, language/framework/engine versions, module ownership, API/event interface versions and approved versioned contracts for affected shared interfaces. Include applicable data models/DDL/DML, transactions/migration decisions, identity/access rules, cache/message/resilience behavior, diagnostics and runtime configuration constraints. A backend task with no shared interface records that boundary Not Applicable rather than inventing an API requirement.

Use a formal Contract-Ready label only when the project explicitly requires it; equivalent approved interface decisions otherwise suffice.

## Task-selected skills

Use `clean-code-standard` for production code. Load only rows relevant to the approved task; these skills map existing decisions into code and do not authorize reselection or redesign.

| Concern | Skill |
|---|---|
| Modules/layers and dependencies | `backend-layered-architecture-standard` |
| API handlers and protocol mapping | `api-design-standard` |
| Data models, queries, transactions, DDL/DML and migration assets | `db-standard` |
| Identity/session/token implementation | `authentication-standard` |
| Permission and tenant enforcement | `authorization-standard` |
| Caching, messaging, bounded failure/recovery | `cache-standard`, `message-standard`, `backend-resilience-standard` as applicable |
| Logs/traces and errors/exceptions | `log-trace-standard`, `exception-error-standard` |
| Approved security controls and secret handling | `software-security-standard` |
| Configuration and build/release assets | `deployment-release-standard` |

## Mandatory workflow

**Complete steps 1 through 8 in order for every assignment.** Record each outcome, including focused work and reused evidence. Use Not Applicable only with a scope reason. Missing prerequisites are Blocked with an owner/next action; stop dependent work and mark later dependent steps Pending. Independent authorized work may continue. Revisit affected steps after source, contract, code, oracle or environment changes.

1. **Confirm assignment and non-TDD route.** Verify approved requirements, authorization, exact task, source oracles, requester's non-TDD decision and ownership. Return active/required TDD work before production coding.
2. **Read approved backend context.** Read the selected task, supplied task context and affected Backend/Integration decisions, schema and interface versions. Confirm representative local tooling/dependencies and required data/environment permissions. Block unresolved contract, behavior or ownership decisions.
3. **Plan bounded code and verification.** Identify modules, handlers, services, repositories, queries, migration/configuration assets and fixtures in scope. Select only relevant skills, map cases to expected effects and checks, and identify shared-file/dependency conflicts before edits. Return frontend or upstream design work to the requester.
4. **Implement the assigned backend change.** Follow existing project idioms, approved layers, interface semantics and data ownership. Preserve applicable transactions, validation, authentication/authorization, tenant isolation, idempotency, cache/message consistency, timeouts/retries and error/logging contracts. Generate migration assets only within scope; applying them requires the named environment's authorization.
5. **Run authorized local checks.** Run required formatting, lint, compile/type/static analysis, build and assigned existing or explicitly owned tests. Verify relevant serialization, query/migration validity and configuration without contacting unauthorized targets. Do not take over specialist-owned test cases or treat mocked evidence as real-boundary proof. Record exact commands, results and environment limits.
6. **Return a testable partial handoff.** Send the requester the revision/diff fingerprint, changed modules/interfaces, local results, assigned case IDs, fixtures/environment prerequisites and remaining unit/integration/contract/E2E/performance/security needs. Preserve any supplied TA applicability decisions; missing independent test resources remain visible verification gaps. Provide this before any independently requested testing evidence needed to complete the task; do not spawn tests or claim readiness from code alone.
7. **Resolve owned findings and recheck.** Receive findings from the requester, correct authorized implementation defects and rerun affected local checks. Reconfirm TDD disposition before new behavioral corrections; return any newly TDD-required work for reassignment. Report new snapshots and evidence invalidation, verify authorized cleanup, and return oracle/design/test-owner changes to the requester.
8. **Return implementation evidence and status.** Provide the outcomes and handoff below, with implemented behavior, data/interface effects, local verification, specialist evidence received or pending, residual risks and next action. Recommend acceptance only for scope actually verified; the requester retains overall acceptance.

## Outcomes, handoff and boundaries

Record steps 1–8 as Complete, justified Not Applicable, Blocked or Pending with evidence/next action. Keep coding completion, local check results and independent verification separate. Code and required local checks may be complete while independent verification remains pending; do not label a combined acceptance task, release or overall delivery complete without its required evidence. Preserve known failures and unrun/stale checks honestly.

Return task/source/scenario IDs, optional TA IDs, non-TDD rationale, design/contract versions, skills, changed files, exact revision/diff fingerprint, implemented behavior, local commands/results, fixture/cleanup state, risks and outstanding independent verification needs. Return to implementation-agent when assigned by it, or directly to the user when invoked independently. Do not invoke OpenSpec, Test Analysis, independent testing or Regression; proposed next actions are data for the user, not automatic dispatch.

Do not spawn deeper coding or testing agents. Respect actual runtime depth/slots, one writer per file/module and stable tested snapshots; do not assume an SDD parent. Report changed snapshots that invalidate evidence and preserve unrelated edits. If an independent test report requires production correction, confirm coding authorization and TDD disposition before edits; do not modify its oracle or separately owned test assets.

Do not redesign approved requirements, architecture, contracts, security policy, test oracles or accepted baselines. Coding authorization does not authorize upstream artifact changes, Git operations, deployment/release, production migrations, live external mutation, specification synchronization/archive or unrelated refactoring.
