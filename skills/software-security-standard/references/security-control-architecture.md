# Security Control Architecture

Use this reference to turn identified risks into owned controls. Select only controls justified by the system's assets, threats, data, policy, and operating model.

## Security context

Record protected assets, human and workload actors, identity sources, entry points, trust boundaries, data flows, data classifications, tenants, privileged operations, third parties, deployment zones, and recovery dependencies. Model both intended flows and credible abuse paths.

## Control placement

| Boundary | Typical security responsibility |
|---|---|
| Interface/Delivery | Validate protocol shape and credential presentation, establish a trusted principal from approved identity evidence, constrain request size/rate where required, apply destination-specific output encoding and transport controls, and map failures safely. |
| Application/Use Case | Authorize every protected use case and object/tenant scope, coordinate step-up or transaction authorization, enforce idempotency and workflow-level abuse controls, and emit approved audit outcomes. |
| Domain/Policy | Enforce business security invariants and protected state transitions that remain true regardless of transport or storage mechanism. |
| Ports | Express required identity, authorization, key, secret, audit, time, data-protection, or external-security capabilities in inward-facing language without leaking vendor types. |
| Infrastructure/Adapters | Implement identity-provider, policy-engine, database, transport, cryptographic, key-vault, secret-manager, audit-store, dependency, and platform controls; translate failures without redefining policy. |
| Composition/Operations | Bind trusted implementations and identities, validate secure configuration, manage certificates/keys/secrets and rotation, restrict runtime privileges and network paths, patch dependencies, protect backups, monitor controls, and support incident/recovery procedures. |

Security controls may span layers, but each decision and enforcement point needs one accountable owner. Middleware may perform common authentication or coarse checks; it must not replace use-case, object, tenant, field, or business-invariant authorization.

## Identity, authentication, and sessions

- Define identity authority, proof/credential type, trust establishment, lifecycle, recovery, revocation, timeout, replay protection, and failure behavior.
- Convert external claims into an explicit internal principal only after validation. Do not trust identity, role, tenant, ownership, or privilege values supplied by an untrusted client.
- Derive tenant/security context from an authoritative binding and preserve its integrity across sessions, service calls, webhooks, jobs, queues, and event streams. Define how account, session, message, resource, and payload tenant identifiers are reconciled; reject and audit mismatches rather than selecting whichever value is convenient.
- Authenticate workloads as well as people when service-to-service calls cross a trust boundary. Prefer short-lived, scoped workload identity over shared static credentials when supported by approved infrastructure.
- Define session/token storage, transport, binding, expiry, renewal, logout/revocation, and compromise response. Avoid exposing credentials in URLs, logs, traces, metrics, or client-readable storage without an explicit safe design.

## Authorization and isolation

- Build an access-control matrix for subject, action, object/resource, tenant, field/data class, context, decision, enforcement point, and audit requirement.
- Enforce least privilege and deny by default. Check authorization on every protected operation and after relevant state or context changes.
- Cover horizontal access, vertical privilege escalation, cross-tenant access, indirect object references, administrative paths, batch operations, exports, and background jobs.
- Keep UI visibility and route-level checks as usability or coarse controls; they are not authoritative authorization.
- Place business authorization and protected state-transition rules in application/domain policy so alternate interfaces cannot bypass them.

## Data protection and cryptography

- Classify data and threat exposure before selecting encryption in transit, at rest, field/record level, tokenization, integrity protection, signing, or irreversible transformation.
- Use approved, maintained libraries and platform protocols. Do not invent algorithms, modes, padding, key derivation, random generation, or signature formats.
- Distinguish encryption, hashing, message authentication, and digital signatures. Passwords normally require an approved adaptive password-hashing scheme, not reversible encryption.
- Define key purpose and separation, owner, generation, storage, access, distribution, versioning, rotation, revocation, compromise response, recovery, destruction, audit, and availability behavior.
- Keep keys separate from protected data and application source/configuration. Define behavior when a key service is unavailable; do not silently fall back to plaintext or an unapproved key.
- Include backups, replicas, caches, queues, search indexes, exports, analytics, logs, traces, and temporary files in the data-protection decision.

## Secrets

- Store secrets in an approved secret-management capability, not source code, images, repository history, client bundles, logs, test fixtures, or ordinary configuration files.
- Scope secret access to the minimum workload and operation, prefer short-lived credentials, rotate and revoke, audit access, and define bootstrap and recovery paths.
- Distinguish a secret from ordinary configuration. Masking a secret in logs does not make hardcoding or uncontrolled storage acceptable.

## Input, output, and integration boundaries

- Perform syntactic and protocol validation at delivery boundaries and semantic/invariant validation in application/domain policy.
- Use parameterized APIs for SQL and other interpreters; apply context-appropriate output encoding; constrain files, URLs, redirects, deserialization, templates, and command execution according to the actual attack surface.
- Authenticate and authorize integrations, validate message/source integrity where required, constrain egress and callbacks, define authoritative tenant/resource binding plus mismatch behavior, define replay/idempotency/ordering behavior, and treat external data as untrusted even from a known partner.
- Apply rate, quota, size, timeout, concurrency, and resource controls where abuse could affect availability or cost.

## Audit, privacy, errors, and observability

- Define security/audit events around authentication, authorization decisions, privileged changes, sensitive-data access, policy/configuration changes, key/secret lifecycle, and control failures when justified.
- Record actor/workload, action, target, tenant, outcome, time, correlation, and policy/control context without recording credentials or unnecessary sensitive content.
- Specify audit integrity, access, retention, deletion, review, alerting, and time synchronization. Diagnostic logs do not automatically satisfy audit requirements.
- Return safe public errors while preserving protected diagnostic context for authorized operators. Avoid account, object, tenant, policy, key, topology, dependency, or stack disclosures that help an attacker.
- Minimize personal data collection and propagation; define purpose, lawful/approved use, retention, deletion, export, and access boundaries where privacy applies.

## Dependency, build, and runtime controls

- Inventory first- and third-party dependencies and artifacts, establish trusted sources, review high-risk additions, and define vulnerability/update ownership.
- Use reproducible or controlled builds where required, protect build credentials, and preserve artifact provenance/integrity according to project policy.
- Define secure defaults, environment separation, least-privilege runtime identity, file/network permissions, administrative access, patching, backup protection, rollback, and incident response.

## Operational and platform control families

### Identity and access platforms

- IAM, identity-provider, MFA, step-up authentication, and privileged-access capabilities implement approved identity and access policy; they do not decide business authorization by themselves.
- Define source of identity truth, federation/trust, enrollment and recovery, credential/session lifecycle, role/attribute provisioning, privilege review, revocation propagation, break-glass behavior, audit, and outage handling before selecting a product.

### WAF and edge protection

- Use a WAF, API gateway security policy, bot/abuse control, or equivalent only when the threat model and operating environment justify it.
- Define protected entry points, deployment/termination point, rule ownership, change control, tuning, false-positive handling, bypass paths, logging/privacy, fail-open/fail-closed behavior, capacity, and emergency rollback.
- Treat edge filtering as defense in depth. It must not replace application authorization, parameterized database access, input validation, output encoding, dependency patching, or root-cause remediation.

### IDS/IPS and network detection

- IDS/IPS is a platform/network detection or prevention capability, not an application business-control layer. Define monitored segments/flows, encrypted-traffic visibility and privacy constraints, signatures/behavior rules, tuning, alert/block ownership, false-positive response, bypass/evasion assumptions, and availability impact.
- Prevention actions that can block production traffic require explicit operational ownership, safe rollout, rollback, and incident procedures.

### SIEM and security monitoring

- Define event producers, schemas, timestamps, identity/tenant/correlation fields, secure transport, buffering/loss behavior, integrity, retention, access, correlation/detection logic, alert severity, triage owner, escalation, and investigation/runbook links.
- A SIEM consumes security telemetry; it does not automatically become the authoritative audit record or repair missing, excessive, untrusted, or sensitive application events.

### Patch and remediation management

- Maintain ownership and inventory for application dependencies, language/runtime, operating system, containers/images, gateways, WAF/IDS agents, databases, brokers, identity components, and other deployed software.
- Define supported versions, vulnerability intake, risk triage, remediation targets from approved policy, testing, staged rollout, rollback, emergency fixes, compensating controls, exceptions with expiry, end-of-life handling, and evidence.
- Do not claim that automatic updating is always safe or that patching alone removes configuration, authorization, design, or zero-day risk.

### Secure coding responsibility

- Translate approved security requirements into language/framework-appropriate coding constraints, including trusted-boundary validation, parameterized interpreter access, context-aware output handling, safe parsing/deserialization, memory/resource safety, race/concurrency protection, safe errors, secret handling, and reviewable security-sensitive code.
- Use `clean-code-standard` for general implementation quality, while this skill remains authoritative for security outcomes, threat assumptions, prohibited behavior, and security evidence.

### Organizational governance dependency

- Security training and awareness can reduce human and process risk but is not an application control. Record applicable role-based training, policy acknowledgement, secure-development competency, incident/reporting awareness, owners, evidence, and gaps only when required by approved organizational policy.
- Do not use training as a compensating claim for a missing technical control unless an authorized risk owner explicitly accepts that limitation.

### Deferred security-testing specialization

- SAST, DAST, software-composition/dependency analysis, secret scanning, configuration/container scanning, vulnerability scanners, fuzzing, penetration testing, and manual security review are verification techniques with different visibility and limitations.
- This control-architecture reference records where evidence is required but does not select products or define the detailed testing workflow. Defer that work to the dedicated security-testing scope when requested; until then, do not claim an unexecuted technique as passing evidence.
