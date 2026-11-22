---
name: authentication-standard
description: Select, design, implement or review identity verification and session/token lifecycles for browser, native and service clients, including cookies, opaque sessions, JWT validation and federated login.
---

# Authentication Standard

## Input and output contract

This summary follows the detailed workflow and linked gates below. Record source owners, locations/versions and decision status; keep unknowns explicit.

- **Required inputs:** Actors/clients, identity journeys, trust boundaries and requirements.
- **Conditional inputs:** Provider/session/API context, assurance/recovery/privacy rules and relevant existing evidence.
- **Optional context:** Alternative mechanisms and incident examples.
- **Outputs:** Authentication/session flows, validation/lifecycle/revocation decisions and verification needs.
- **Destination and consumer:** Use the workflow's existing, requested or documented default artifact/handoff location. Return results to the invoking agent or user for the identified downstream owner; this does not authorize automatic invocation or duplicate artifacts.
- **Completion:** Apply seven-step readiness; design does not authorize implementation.


Establish who the caller is and how that identity remains trustworthy over its lifecycle. Authorization policy is a separate decision. Select mechanisms from requirements and approved identity infrastructure; do not assume every application needs JWTs or a new identity provider.

## Core rules

- Distinguish identity proof, application session state, credential transport and token representation. A cookie may carry an opaque session identifier or a token; JWT is a format, not a complete authentication or revocation design.
- Define the identity authority and trusted principal for people and workloads. Validate external evidence before accepting subject, tenant or privilege claims. Client-supplied identity/tenant values and tracing context are not authentication evidence.
- Use established framework/provider capabilities and approved cryptography. Keep passwords, session identifiers, tokens, authorization headers and signing keys out of public errors, logs, traces, URLs and example fixtures.
- Preserve approved policies and compatibility; unresolved identity, lifetime, revocation or recovery requirements are decisions to resolve, not values to invent.

## Mandatory workflow

**Complete steps 1 through 7 in order for every authentication task.** Identify mode and scope first and record each outcome. Confirm existing decisions against the actual clients, contract and evidence. Focused work may make a step brief but does not omit its outcome. Mark `Not Applicable` only with a reason. If a required input or decision is missing, mark the step `Blocked`, identify the owner/next action and stop dependent work; record dependent steps as `Pending`. Revisit affected steps when the baseline changes.

1. **Establish identity requirements.** Identify human/service actors, browser/native/backend clients, trust boundaries, tenant binding, approved identity providers and login journeys. Capture applicable assurance/MFA, recovery, revocation, privacy, availability and compatibility requirements. Define which operations are public and which require an authenticated principal without deciding their business permissions.
2. **Select a coherent mechanism.** Compare applicable options below, confirm supported framework/provider behavior and record the requirement-driven choice. Separate authentication protocol, session state, credential transport and representation. Reuse accepted infrastructure unless requirements justify changing it; OAuth access delegation alone is not proof of user login.
3. **Define credential validation and principal establishment.** Specify accepted credential types, validation owner, issuer/trust configuration, identity/tenant binding and rejection behavior. For JWTs, require signature verification with configured algorithm/key trust, intended issuer/audience/token purpose and required time/claim checks; do not select trust from an untrusted token header or accept an ID token as an API access token. Define discovery/key refresh, rollover and unknown-key handling without unbounded token-selected network access.
4. **Define session and token lifecycle.** Cover creation, rotation after authentication/privilege changes, storage, expiry, renewal, logout, revocation, account disablement, recovery and compromise response. Specify access/refresh-token responsibilities, refresh replay handling and revocation propagation when applicable. Record the maximum accepted stale-authentication window and its requirement; logging out of a client does not inherently invalidate a bearer token elsewhere.
5. **Define client and boundary protections.** For browser cookies, specify TLS, Secure/HttpOnly where applicable, narrow domain/path, SameSite behavior compatible with the actual flow, and CSRF protections for ambient credentials; SameSite is not a complete CSRF design. Define browser/native credential storage, redirect/callback and origin constraints, replay/fixation controls and safe failure UX. For OAuth/OIDC, use current provider-supported secure flows, including applicable PKCE, state/nonce and redirect validation; do not invent a custom protocol.
6. **Define failure and integration contracts.** Cover identity-provider/key-store/session-store outages, invalid/expired/revoked credentials, renewal races, abuse throttling and recovery limits. Missing identity evidence must not grant authenticated access. Return required session/token/key data to Architecture, cache/availability needs to Middleware, audit/redaction requirements to Diagnostics and operational key/configuration needs to Delivery. Propose any HTTP/header/cookie/status changes through the API owner.
7. **Verify and report.** Specify or assess successful login and applicable invalid issuer/audience/signature/purpose, expiry, key rollover, fixation/replay, logout/revocation, disabled accounts, CSRF, recovery and dependency-failure cases. For authorized implementation, run relevant checks; for design, state planned verification and acceptance criteria. Return evidence, gaps and residual limitations without claiming tests ran when they did not.

## Mechanism selection

| Candidate | Evaluate when | Decisions that remain necessary |
|---|---|---|
| Opaque server session with browser cookie | A browser application can maintain server-side session state | Store capacity/availability, cookie/CSRF controls, expiry, rotation, logout and revocation |
| Opaque bearer access token | API access needs centrally controlled token validity | Issuance and validation/introspection trust, caching/staleness, availability and revocation |
| JWT access token | Consumers need verifiable claims across agreed trust boundaries | Key trust/rotation, token purpose, issuer/audience/claim validation, lifetime and revocation tradeoffs |
| Federated login with an approved identity provider | SSO or external identity proof is required | Protocol/provider validation plus the application's own session, account mapping and logout behavior |
| Workload identity | Services/jobs authenticate without a human login | Credential provisioning, rotation, audience/scope, delegation and trust-boundary enforcement |

Choose combinations when their responsibilities differ; do not present session, cookie and JWT as mutually exclusive alternatives. Select no authentication for a genuinely public operation only with its approved scope recorded; separately evaluate abuse and data-access requirements.

## Readiness gate

Require a known identity authority, trusted principal/tenant mapping, justified mechanism, validation rules, protected storage/transport, lifecycle/revocation, failure behavior and verification plan for applicable scope. Every workflow step needs an outcome and every applicable step must be complete before claiming completion. `Blocked` or `Pending` applicable decisions prevent readiness. A completed review may report a flawed design without approving it.

## Expected output and boundaries

Return a numbered seven-step record with `Complete`, `Not Applicable`, `Blocked` or `Pending`, evidence/next action and reasons for exceptions. Include the mechanism rationale, authentication/session state flow, credential-validation contract, lifecycle and revocation policy, data/middleware/API impacts, safe audit requirements, verification and unresolved decisions. In System Design, return design only; implementation follows its separately authorized lifecycle.

This skill does not invoke other skills. Consume authorization and other specialist decisions as input and return gaps to their owner. In `identity-access-agent`, its output precedes authorization design.

## Standards basis

Use approved policy and the selected framework/provider's official documentation. Check version-specific details when applying [OWASP session guidance](https://cheatsheetseries.owasp.org/cheatsheets/Session_Management_Cheat_Sheet.html), [JWT validation guidance in RFC 8725](https://www.rfc-editor.org/rfc/rfc8725.html) and [OAuth security guidance in RFC 9700](https://www.rfc-editor.org/rfc/rfc9700.html). These references do not choose the project's identity policy or imply execution authorization.
