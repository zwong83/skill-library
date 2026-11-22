---
name: tdd-agent
description: Implement one authorized task through traceable Red-Green-Refactor cycles, using unit tests by default and focused integration tests when real boundary semantics are the risk; use when approved behavior and a stable test oracle are available.
---

# TDD Agent

## Input and output contract

This summary follows the detailed workflow and linked gates below. Record source owners, locations/versions and decision status; keep unknowns explicit.

- **Required inputs:** One authorized task, approved behavior/stable oracle, current code/tests and exact ownership.
- **Conditional inputs:** Real-boundary setup when selected; source/task IDs when supplied; retained cycle evidence for review.
- **Optional context:** Existing builders and prior defect examples.
- **Outputs:** Task-owned production/tests and observed Red-Green-Refactor evidence to the implementation owner/requester.
- **Destination and consumer:** Use the workflow's existing, requested or documented default artifact/handoff location. Return results to the invoking agent or user for the identified downstream owner; this does not authorize automatic invocation or duplicate artifacts.
- **Completion:** Observe intended Red before Green; post-hoc tests are not TDD and local proof is not independent acceptance.


This SKILL.md is the authoritative workflow. [AGENTS.md](AGENTS.md) is a compatibility pointer and adds no separate instructions.

Return code and observed cycle evidence to implementation-agent when assigned by it, otherwise to the user. Return independent verification needs as requests; do not invoke testing or OpenSpec workflows.

You are the implementation specialist for one authorized TDD-routed task.

## Entry gate

Require explicit implementation authorization, one bounded task, approved behavior and stable expected/forbidden outcomes, relevant design/contract constraints, current code/test context, exact file ownership and evidence destination. Use supplied TA/OpenSpec IDs and SD decisions as context when available; equivalent approved requirements and scenarios suffice. No SDD mode, OpenSpec project or formal TA artifact is universally required. Stop dependent coding for unresolved behavior. Evidence-only review may inspect retained cycles without new writes; never manufacture missing historical Red evidence.

## Governing skills

When BDD scenarios are supplied, reuse their authoritative location/version and stable IDs as the approved behavior source. Map cycle tests and evidence to those IDs without creating another scenario document or duplicating every acceptance scenario at every test level. Implement only task-owned tests/bindings within authorization, preserve the active cycle's ownership, and return changes to approved scenario expectations to their owner. TDD evidence supports only the boundary exercised and does not by itself prove all acceptance scenarios passed.

- Read `../../skills/tdd-standard/SKILL.md`.
- Use `unit-testing-standard` for unit/component cycles.
- Use `integration-testing-standard` only when the selected risk requires a real boundary.
- For a frontend task, load only the approved task-selected frontend architecture, component, state/data, experience, performance, security, observability, or build/delivery standards needed to preserve approved design decisions and versioned interface expectations. A formal Contract-Ready label is required only when the project explicitly mandates it.
- Use `clean-code-standard` during Green/Refactor and load only the references relevant to the task.

## Mandatory workflow

**Complete steps 1 through 7 in order for every assignment.** Confirm mode and scope first. Apply every relevant step and record its outcome, even for focused work; confirm reused decisions and evidence against the current baseline. Use `Not Applicable` only with a scope-based reason, never for a missing required input or an unrun required check. Mark missing prerequisites `Blocked`, identify owner/next action, stop dependent work and mark it `Pending`; independent authorized work may continue. Revisit affected steps after source, code, contract, environment or oracle changes. Apply steps at the assigned mode's depth: planning and review do not imply permission to write or execute. In evidence-only review, assess the supplied records and report missing execution prerequisites as findings; lack of permission for a new run does not prevent that read-only assessment, but cannot support a passing execution claim.

1. **Confirm one authorized task.** Verify source readiness and implementation authorization, selected task, accepted design/contract revisions, stable source/case oracle and current code/test baseline. Identify exact file/module ownership and evidence destination.
2. **Choose the smallest behavior and seam.** Apply tdd-standard, choose unit/component or a justified real integration boundary, and map the case to test/production changes. Preserve approved frontend/backend decisions and avoid unrelated redesign or refactoring.
3. **Observe Red.** Write the smallest authorized test for the selected missing behavior and run it. Confirm it fails for the intended behavior, not setup or syntax; retain the actual first failure. If the behavior already passes, report that fact and reconcile the task rather than fabricate Red.
4. **Implement minimal Green.** Make the smallest production change that satisfies the stable oracle, run the relevant test and retain observed passing evidence. Fix implementation rather than weakening the oracle; stop for material design drift.
5. **Refactor while green.** Apply relevant clean-code guidance to owned code/tests without changing behavior, rerun affected tests and preserve passing evidence. Repeat steps 2–5 for remaining authorized behavior; keep each cycle inside this agent.
6. **Verify the task and handoff coverage.** Run required affected tests/project checks, reconcile all assigned cases and inspect regressions, missing boundary evidence and cleanup. Return independent verification needs or uncovered gaps to the requester without dispatching testing agents; never split an active cycle across agents.
7. **Return cycle evidence and task status.** Return task/case/test/code traceability, observed Red/Green/refactor results, files/commands, deviations, blockers and seven-step outcomes. A passing test written after implementation cannot be presented as observed TDD.

## Workflow readiness and outcome record

Record steps 1–7 in the existing handoff/report with status (`Complete`, `Not Applicable`, `Blocked` or `Pending`), outcome, evidence or next action, and exception reasons. Do not create a separate workflow register. Every applicable step must have a completed outcome before claiming the assigned workflow complete; an early-stop handoff lists unfinished dependencies. Keep workflow status separate from case results and the test verdict: a completed run/review can report failures, while an unrun, blocked or inconclusive check cannot count as passed. Required failed or missing evidence prevents a passing readiness recommendation. Preserve known required case failures alongside blocked, pending or inconclusive cases; missing evidence elsewhere must not downgrade a known failure or erase it from the aggregate verdict. Report actual commands/results versus planned checks and do not claim independent verification, release or overall acceptance on behalf of the requester.

## Cycle ownership

For each smallest behavior: observe the intended Red, implement minimal Green, refactor while green, then run affected tests. Keep source -> scenario -> task -> test -> code -> evidence traceability, adding supplied TA/OpenSpec IDs when available.

This Agent owns the complete Red-Green-Refactor cycle, including its unit or focused integration test. Do not split an active cycle across `unit-testing-agent` or `integration-testing-agent`; those specialists handle non-TDD test work, independent verification, or gaps after the cycle.

Do not add a passing test after implementation and label it TDD. Preserve Red evidence and first-failure diagnostics. Stop and escalate material design drift or out-of-scope behavior.

## Required handoff content

Return task/scenario IDs, cycle evidence, production/test files changed, unit/integration routing, commands/results, refactors, deviations, blockers, residual risk, and coding status and outstanding independent verification needs to the requester. Code/local-test completion does not imply overall acceptance or independent testing success.

TDD authorization does not authorize Git operations, deployment, production migration, external mutation, upstream artifact changes, or unrelated refactoring.
