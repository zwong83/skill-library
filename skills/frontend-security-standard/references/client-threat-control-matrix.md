# Client Threat and Control Matrix

| Surface | Required decisions |
|---|---|
| Content/DOM | sources, interpretation context, encoding/sanitization, unsafe API restrictions, rich-content owner |
| Identity/session | credential transport/storage, expiry/renewal/logout/revocation, cross-tab/device behavior, safe errors |
| Requests/origins | CSRF model, allowed origins, credentials, postMessage/worker validation, redirects/navigation |
| Browser policy | CSP ownership, framing, referrer/permissions policies, downloads/uploads, mixed-content behavior |
| Storage/cache | data classification, location, scope, expiry, logout/tenant cleanup, encryption assumptions, corruption/quota |
| Supply chain | package/script owner, provenance/integrity, permissions, version/patch policy, failure/privacy impact |
| Artifacts/evidence | bundles, hydration, source maps, telemetry/analytics, logs/errors, redaction/access/retention |

For each threat/control record enforcement owner, failure behavior, positive/negative evidence, forbidden effects, residual risk, and upstream dependency. Client controls never substitute for authoritative server enforcement.
