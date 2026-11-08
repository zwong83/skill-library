---
name: frontend-security-standard
description: Design, implement, or review web-client security for untrusted content, XSS, CSRF, CSP, browser storage, sessions/tokens, third-party scripts, dependencies, clickjacking, redirects, uploads/downloads, source maps, and sensitive-data exposure; server authorization remains authoritative.
---

# Frontend Security Standard

Use this skill for browser/client-specific controls within an approved security architecture and data classification.

## Core rules

1. Treat the browser, DOM, URL, storage, messages, third-party scripts, extensions, and client-supplied identity/role/tenant values as untrusted boundaries.
2. Prevent unsafe interpretation with context-appropriate encoding, safe framework APIs, sanitized rich content, and constrained dynamic URL/style/script behavior. Avoid unsafe DOM or code-evaluation escape hatches.
3. Define session/token transport, storage, expiry/renewal/logout/revocation, cross-tab behavior, and compromise response with the approved identity architecture; never treat client secrecy as durable protection.
4. Define CSRF protection from the actual credential transport and request model. Do not add or omit controls by slogan.
5. Design CSP, framing/clickjacking, trusted origins, redirects/navigation, cross-origin communication, downloads/uploads, and browser policy headers with backend/edge ownership.
6. Minimize sensitive data in HTML, hydration payloads, URLs, browser storage, caches, telemetry, analytics, error messages, bundles, and source maps.
7. Govern third-party scripts, packages, provenance/integrity, permissions, update ownership, failure behavior, and privacy impact.
8. UI hiding and route guards improve UX but never replace server-side authorization, tenant/object isolation, or authoritative validation.
9. Define positive and negative security evidence, including forbidden side effects and audit/telemetry, without exposing secrets or exploit-ready data.

## Workflow

1. Confirm assets/data, trust boundaries, identity/session model, approved security controls, external scripts, storage, and deployment context.
2. Build the client threat/control matrix and assign browser, frontend, backend, edge, identity, and delivery ownership.
3. Define implementation contracts, failure behavior, evidence, and residual risks.
4. Escalate missing server/security decisions instead of inventing client-side substitutes.

## Reference routing

- Read [client-threat-control-matrix.md](references/client-threat-control-matrix.md) for the client threat/control decisions written into Frontend SD.
- Invoke `software-security-standard` for the governing threat/control architecture and `security-testing-standard` for authorized verification.
- Invoke `frontend-state-data-standard` for browser persistence and `frontend-build-delivery-standard` for headers, source maps, artifacts, and dependencies.

## Output

Return client assets/trust boundaries, threat/control/ownership matrix, content/DOM rules, session/storage contract, CSRF/CSP/origin/framing/navigation controls, third-party/dependency rules, sensitive-data exclusions, failure/evidence requirements, residual risks, and unresolved upstream decisions.
