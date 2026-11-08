# Build, Artifact, and Release Matrix

| Concern | Required decisions |
|---|---|
| Build | source revision, lock/dependency/toolchain versions, commands, deterministic inputs, CI ownership, provenance |
| Artifact | immutable identity, manifests/chunks/assets, integrity/signing where required, storage/promotion/retention |
| Configuration | build-time vs runtime public values, schema/validation/defaults, flags, refresh/stale/failure, audit/rollback |
| Compatibility | browser/polyfill/module targets, client/server/API versions, stale clients/tabs, mixed rollout |
| Cache/CDN | HTML/data/asset/service-worker policies, content identity, invalidation, purge, fallback, rollback behavior |
| Diagnostics | release ID, source maps, manifests, symbolication, access/retention, post-release evidence |
| Release | promotion, exposure, canary/phases, gates, health, rollback/roll-forward, owner/approval boundaries |

Do not place secrets in client-visible configuration or assume cache purge is instantaneous. Design mixed-version behavior and recovery explicitly.
