---
name: authorization-standard
description: Design, implement or review permission policies and enforcement for authenticated or explicitly anonymous actors, including roles, attributes, relationships, tenant/object/field access and policy lifecycle.
---

# Authorization Standard

Determine whether a trusted actor may perform a specific action on a resource in its current context. Consume the authentication principal contract; possession of a valid session or JWT does not grant every operation.

## Core rules

- Derive rules from approved business requirements and data ownership. Do not invent roles, privileged exceptions, tenant boundaries or policy requirements to fill a gap.
- Apply least privilege and default denial when no applicable allow rule exists. Enforce decisions server-side on every protected operation and resource; UI visibility or a gateway's coarse check is insufficient.
- Obtain subject, tenant, ownership and resource attributes from authoritative bindings. Never accept a caller's asserted role/tenant/owner as proof. Opaque identifiers do not replace access checks.
- Separate policy ownership, decision evaluation and enforcement. Define consistency when permissions, ownership or resource state change; a decision detached from the protected effect may become stale.
- Define permission rules for explicitly anonymous actions too. Protect background jobs, alternate interfaces, batch/export and delegated service actions where applicable.

## Mandatory workflow

**Complete steps 1 through 7 in order for every authorization task.** Record the task mode, scope and an outcome for each step. Confirm existing rules against approved behavior and evidence. A focused task may shorten a step but must retain its outcome. Mark `Not Applicable` only with a reason. Mark missing required decisions `Blocked`, identify the owner/next action and stop dependent work; report dependent steps as `Pending`. Revisit affected steps after policy, contract or data-ownership changes.

1. **Establish the policy baseline.** Identify approved actions, resources, human/workload/anonymous actors, trusted principal attributes, ownership and tenant boundaries. Record administrative/delegated operations, state constraints and governing requirement/operation IDs. Separate unresolved business policy from implementation choices.
2. **Select the permission model.** Assess role-based, attribute-based, ownership/relationship-based or combined rules against actual requirements. Prefer the simplest model that expresses them correctly; do not assume roles alone cover object ownership or tenant scope. Name the policy owner and authoritative sources for each attribute/relationship.
3. **Specify the permission matrix.** For each actor/action/resource, record allow/deny conditions, tenant/object/field scope, state preconditions, constrained output and privileged exceptions. Cover list/search/count/export as well as individual reads/writes, and record delegation limits. Requests cannot gain access by supplying another tenant or object identifier.
4. **Place enforcement and data filtering.** Identify application/use-case enforcement, resource lookup and field filtering boundaries; preserve checks through alternate APIs, jobs and message consumers. Define atomicity or revalidation when policy/resource state can change between check and effect. Return schema/index/query requirements to Architecture rather than designing competing DDL.
5. **Define policy lifecycle and failure behavior.** Cover provisioning, permission/role changes, removal, account/tenant changes, policy versioning and propagation. If decisions are cached or claims are long-lived, specify approved staleness, invalidation and revocation behavior. Missing policy/attribute dependencies must not accidentally allow access; any degraded access requires an explicit approved rule.
6. **Define denial and audit contracts.** Specify safe unauthenticated/forbidden/not-found behavior according to the accepted API and disclosure policy, without leaking resource existence or sensitive fields. Provide Diagnostics with decision category, policy/version, safe subject/resource correlation and audit requirements, excluding credentials and sensitive payloads. Send public error/API changes through the contract owner.
7. **Verify boundaries and report.** Define positive and negative cases for horizontal/vertical privilege escalation, cross-tenant/object/field access, bulk/list/export filtering, stale policy, ownership changes, alternate entrypoints and dependency failures. Each denial case includes expected absence of protected mutations/events/notifications and required safe audit evidence. Run checks only in an authorized implementation/test scope; label design plans as pending verification.

## Readiness gate

Require an approved policy source, trusted principal contract, complete applicable permission matrix, authoritative attributes, enforcement/filtering owners, policy lifecycle, failure behavior and verification criteria. All steps need recorded outcomes and applicable steps must be complete before claiming completion. Unresolved policy, isolation, stale-access or enforcement decisions block readiness. Review completion does not imply the reviewed policy passed.

## Expected output and boundaries

Return a numbered seven-step record with `Complete`, `Not Applicable`, `Blocked` or `Pending`, evidence/next action and reasons for exceptions. Include permission and enforcement matrices, policy lifecycle/consistency, data/API/middleware impacts, denial/audit semantics, verification and unresolved owner actions. Do not silently broaden access or change approved public contracts.

This skill does not invoke other skills. Consume authentication, data and middleware decisions as input and return required changes to their owners. In System Design, produce policy/enforcement design, not production authorization code or executed security tests.

## Standards basis

Use project-approved policy and the selected framework/policy engine's official documentation. Apply relevant [OWASP authorization guidance](https://cheatsheetseries.owasp.org/cheatsheets/Authorization_Cheat_Sheet.html) to enforcement and verification; it does not supply missing business permissions or approve risk exceptions.
