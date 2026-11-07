# Security Verification Gate

Report each item as `Pass`, `Gap`, `Needs decision`, or `Not applicable`, with evidence. Never report an unexecuted check as passing.

## Context and requirements

- Protected assets, actors, workload identities, entry points, trust boundaries, data flows, tenants, and data classifications are explicit.
- Applicable security, privacy, compliance, retention, audit, deployment, and incident requirements have authoritative sources and owners.
- Threats, abuse cases, assumptions, exceptions, and residual risks are recorded without invented approval.
- Every material control traces to a requirement/risk, enforcement point, implementation/configuration, owner, and verification method.

## Identity and access

- Authentication validates approved identity evidence and defines lifecycle, recovery, revocation, replay, expiry, and failure behavior.
- Authorization is server-side, deny-by-default, and covers use case, object, tenant, field, state, administrative, batch, export, and background-job access where applicable.
- Tenant/security context is derived from an authoritative binding and protected across sessions, service calls, webhooks, jobs, queues, and event streams; account/message/resource/payload mismatches fail closed and are covered by negative tests.
- Horizontal, vertical, and cross-tenant bypass tests exist for material authorization paths.
- Service/workload identities and privileged operations use scoped access and auditable ownership.

## Data, cryptography, keys, and secrets

- Data protection covers all applicable states and copies, including transit, storage, fields, backups, caches, queues, exports, logs, traces, and temporary data.
- Approved cryptographic libraries/protocols are used; custom cryptography and silent plaintext fallback are absent.
- Key lifecycle, separation, access, rotation, revocation, compromise, recovery, destruction, audit, and availability behavior are defined and tested as applicable.
- Passwords and irreversible credentials use approved one-way protection rather than reversible encryption.
- Secrets are absent from source, client artifacts, ordinary configuration, logs, traces, metrics, test fixtures, and build output; access and rotation are scoped and evidenced.

## Boundary and implementation safety

- Untrusted input, output contexts, interpreters, files, URLs, deserialization, templates, and external messages are handled according to their real attack surface.
- Public errors and telemetry avoid credential, personal-data, authorization, topology, key, internal-state, and stack disclosures.
- Rate, quota, timeout, size, concurrency, and resource-abuse controls are verified where availability or cost can be attacked.
- Whenever a protected operation, webhook, job, command, or event can be retried, duplicated, replayed, delayed, or reordered, tests verify the approved behavior and the absence of duplicate external calls, protected state transitions, records, messages/events, or misleading audit outcomes.
- Dependencies, build artifacts, configuration, deployment identity, permissions, network paths, backups, and patch/vulnerability ownership have applicable evidence.

## Audit and operations

- Required security events are complete, correlated, access-controlled, retained, reviewable, and protected to the required integrity level.
- Alerts and runbooks cover material control failures, credential/key compromise, suspicious access, and recovery paths where applicable.
- Security control degradation and dependency outage behavior fails according to the approved risk decision.

## Evidence

Use the checks required by the approved design and risk profile, such as unit, integration, contract, end-to-end, negative authorization, tenant-isolation, cryptographic/configuration, secret-scanning, dependency, static, dynamic, fuzz, penetration, backup/recovery, and manual review evidence.

For each material negative scenario, evidence must identify the actor/workload, tenant/security context, precondition, malicious or invalid action, expected denial/failure, forbidden side effects, required audit outcome, and observed result. A denial assertion alone is insufficient when a provider call, data mutation, event, notification, privilege/session change, or sensitive audit payload could already have occurred.

For every skipped or unavailable check, record the reason, impact, compensating control, owner, and required follow-up. An exception requires an authorized owner, scope, rationale, expiry/review date, and residual-risk statement.
