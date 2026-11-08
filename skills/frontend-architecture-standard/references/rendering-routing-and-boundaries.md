# Rendering, Routing, and Boundaries

Record each decision with drivers, selected option, alternatives, consequences, owner, status, and verification.

| Concern | Required decision |
|---|---|
| Rendering | CSR/SSR/static/streaming/hybrid by route; freshness, personalization, SEO, latency, and failure behavior |
| Execution | server/client boundary, trusted operations, serialization, hydration, sensitive-data exclusions |
| Modules | feature ownership, shared platform/design-system boundary, allowed/forbidden dependencies |
| Routing | route/layout ownership, parameters, deep links, redirects, guards, loading/error/not-found, restoration |
| Composition | application shell, lazy/code-split units, extension points, cross-feature communication |
| Failure | component/route error boundaries, degraded content, retry/reload, telemetry and user recovery |
| Delivery | artifact/hosting relationship, runtime/config dependencies, mixed-version compatibility |

Treat microfrontends, service workers/offline, and advanced rendering as conditional decisions. Mark them `Not Applicable` when no requirement justifies their complexity.
