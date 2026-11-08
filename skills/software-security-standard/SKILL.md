---
name: software-security-standard
description: Identify, design, implement, or review risk-based software security controls across System Analysis, System Design, SDD, code, and verification, including threat modeling, authentication, authorization, tenant isolation, cryptography, key and secret management, input/output safety, audit, privacy, supply-chain security, and security evidence.
---

# Software Security Standard

Use this skill to make software security explicit, owned, testable, and traceable throughout the delivery lifecycle. Apply controls according to assets, threats, data sensitivity, trust boundaries, approved policy, and risk; do not add security theater or invent compliance requirements.

## Core rules

- Identify assets, actors, identities, entry points, data flows, trust boundaries, abuse cases, and material threats before selecting controls.
- Use least privilege, deny by default, complete mediation, separation of duties where justified, and defense in depth. Authorization must be enforced server-side at the boundary that owns the protected action or invariant.
- Treat authentication and authorization as different decisions. A valid identity is not permission to perform an action or access an object, tenant, or field.
- Classify data before deciding protection. Specify confidentiality, integrity, availability, privacy, retention, deletion, residency, and audit needs where applicable.
- Use established, maintained cryptographic libraries and approved platform capabilities. Do not design custom cryptographic algorithms or hardcode algorithms, keys, tokens, passwords, or secrets without an approved constraint.
- Design the complete key and secret lifecycle: generation, storage, access, distribution, use, rotation, revocation, recovery, destruction, auditing, and failure behavior.
- Validate untrusted input at trust boundaries, enforce business invariants in the owning policy layer, encode output for its destination, and use parameterized interfaces for interpreters such as databases.
- Fail securely and expose only safe error information. Preserve diagnostic cause internally without leaking secrets, personal data, internal topology, or exploit-relevant detail.
- Separate security audit evidence from ordinary diagnostic logs when retention, access, integrity, or review requirements differ. Never log credentials, session tokens, encryption keys, or unnecessary sensitive data.
- Treat IAM/MFA, WAF, IDS/IPS, SIEM, patching, and similar products as conditional control capabilities, not universal components or substitutes for secure application behavior. Product selection requires approved constraints, ownership, integration design, and operational capacity.
- Make security controls verifiable. An unexecuted check is not passing evidence, and a residual risk is not accepted unless an authorized owner records the decision.

## Control-family boundary

| Family | Treatment in this skill |
|---|---|
| Identity and access platforms | Design identity trust, MFA/step-up conditions, authorization, privileged access, lifecycle, and integration boundaries when required; do not assume a specific IAM product. |
| Secure coding and application controls | Define language/framework-appropriate prevention rules and implementation responsibilities; coordinate with `clean-code-standard`, error, logging, and architecture skills where applicable. |
| WAF and edge protection | Conditional defense-in-depth at the delivery/edge boundary; never a replacement for parameterized queries, validation, output encoding, authorization, or application fixes. |
| IDS/IPS and security monitoring | Conditional platform/network detection or prevention owned with Security Operations; define visibility, response, privacy, tuning, and failure implications. |
| SIEM/security analytics | Conditional collection, correlation, alerting, investigation, retention, and access capability; it does not automatically satisfy authoritative audit-record requirements. |
| Patch management | Required ownership for supported software, dependencies, runtime/platform components, remediation decisions, rollout, rollback, exceptions, and end-of-life risk. |
| Security training and awareness | Organizational governance dependency. Record applicable requirements, owners, and gaps, but do not treat training as a software control or design a training program here. |
| SAST, DAST, software-composition/dependency analysis, secret/configuration scanning, and vulnerability scanning | Security-verification techniques governed by `security-testing-standard` when in scope; require authorized targets, safe execution, finding validation, evidence handling, and ownership. |

## Lifecycle modes

| Mode | Security responsibility |
|---|---|
| System Analysis | Identify assets, actors, trust boundaries, sensitive data, abuse cases, security requirements, risks, and unresolved policy decisions without choosing implementation mechanisms. |
| System Design | Select control architecture, enforcement points, identity and authorization flows, data protection, key/secret ownership, audit behavior, operational controls, and verification strategy. |
| SDD/OpenSpec | Define concrete contracts, libraries/platform integrations, configuration semantics, negative scenarios, tasks, tests, migration, rollout, and rollback while preserving approved SD decisions. |
| Implementation/review | Implement or inspect the approved controls, run applicable security checks, collect evidence, and report drift or residual risk. |

## Input and readiness gate

Require the target scope, governing requirements/design, protected assets and data, actors or workload identities, trust boundaries, applicable policy/compliance constraints, and current implementation context needed by the selected mode. Authentication providers, tenant model, data classification, cryptographic/key platform, secrets platform, retention, audit, deployment, and incident requirements become mandatory when they affect the decision.

Do not invent a missing security policy or mark security `Not Applicable` merely because no requirement was supplied. Record the gap, impact, decision owner, and whether it blocks the requested readiness level. Block implementation-ready status when a material authorization rule, trust boundary, data classification, encryption/key decision, secret ownership, audit obligation, or security acceptance criterion remains unresolved.

## Workflow

1. Classify the lifecycle mode and read the authoritative requirements, analysis, design, change artifacts, code, and approved security standards applicable to the scope.
2. Establish the security context: assets, actors, identities, entry points, data flows, trust boundaries, data classifications, abuse cases, dependencies, and operational environment.
3. Assess threats and risk using the project's approved method. Record likelihood/impact or equivalent rationale without claiming unsupported precision.
4. Build a control-ownership matrix covering prevention, detection, response, recovery, enforcement point, owner, configuration, failure mode, and verification evidence.
5. Define identity, authentication, session/token, authorization, object/tenant/field isolation, and privileged-operation controls.
6. Define data protection, cryptography, key/secrets lifecycle, privacy, retention/deletion, backup/restore, and safe observability behavior.
7. Define boundary validation, output handling, external integration, dependency/supply-chain, deployment, secure configuration, identity platform, edge/WAF, detection/IDS/IPS, SIEM, patching, and organizational dependencies where applicable; mark unjustified control families `Not Applicable` with rationale.
8. Define security requirements and negative scenarios, then map each material control to tests, analysis, review, operational evidence, and an owner. Each negative scenario must identify the actor/workload, tenant/security context, precondition, malicious or invalid action, expected denial/failure, forbidden side effects, required audit outcome, and evidence.
9. Run the verification gate and report gaps, exceptions, residual risks, expiry/review dates, and required upstream decisions.

## Reference routing

- Read [references/security-control-architecture.md](references/security-control-architecture.md) when placing or designing authentication, authorization, encryption, secrets, validation, audit, privacy, dependency, or operational controls.
- Read [references/security-verification-gate.md](references/security-verification-gate.md) before approving a security design, implementation, or release-readiness claim.
- Invoke `security-testing-standard` when approved controls require concrete static, dependency, configuration, dynamic, or control-specific negative verification.

## Relationship to other skills

- `layered-architecture-standard` decides where a control is enforced and how security dependencies cross layers; this skill defines the security outcome and control requirements.
- `logging-standard` and `tracing-standard` define telemetry mechanics; this skill defines security/audit evidence, access, retention, integrity, and sensitive-data exclusions.
- `error-handling-standard` defines failure contracts; this skill defines secure failure behavior and disclosure limits.
- `clean-code-standard` governs general implementation quality; this skill supplies the security-sensitive coding outcomes and constraints that implementation must preserve.
- SA, SD, and SDD remain authoritative for lifecycle-specific artifacts. Correct the upstream artifact when implementation reveals a missing or invalid security decision.

## Standards basis

Use project-approved standards first. For general application-security coverage, consult the current stable [OWASP Application Security Verification Standard](https://asvs.owasp.org/). For secure-development lifecycle practices, consult the current final [NIST Secure Software Development Framework](https://csrc.nist.gov/projects/ssdf). Use focused OWASP cheat sheets only as implementation guidance; they do not replace project policy, threat modeling, or risk acceptance.

## Expected output

Provide the security context and assumptions, trust/data-flow boundaries, threat and abuse-case register, security requirements, control-ownership matrix, access-control matrix, data-protection and key/secret decisions, audit and operational controls, verification/evidence matrix, gaps and exceptions, residual risks, owners, and traceability to requirements, design, tasks, code, and tests as appropriate to the selected mode.
