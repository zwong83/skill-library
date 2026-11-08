---
name: frontend-build-delivery-standard
description: Design, implement, or review reproducible frontend builds, environment/runtime configuration, dependency/browser targets, asset identity, source maps, CDN/browser caching, immutable promotion, feature release, compatibility, rollout, rollback, and delivery evidence.
---

# Frontend Build and Delivery Standard

Use this skill when frontend source must become reproducible, identifiable, safely configured, cacheable, promotable, observable, and recoverable artifacts.

## Core rules

1. Produce immutable, identifiable artifacts from pinned source/dependencies/toolchain with reproducible commands and recorded provenance.
2. Separate build-time public configuration, runtime public configuration, feature controls, and secrets. Never embed server secrets or production credentials in client artifacts.
3. Define environment/config schema, validation, defaults, precedence, refresh, stale/failure behavior, audit, and rollback.
4. Define supported browser targets, transpilation/polyfill policy, module format, dependency compatibility, and bundle verification from approved support commitments.
5. Use content identity for assets and explicit HTML/data/service-worker/CDN/browser cache lifecycles so rollout and rollback do not serve incompatible mixed versions.
6. Govern source maps, manifests, integrity/provenance, compression, headers, third-party assets, and artifact retention/access.
7. Separate artifact promotion from feature exposure. Define mixed-version client/server compatibility, flags, canary/phased rollout, health/evidence, rollback/roll-forward, and stale-client behavior.
8. Include installation/PWA/service-worker update and recovery behavior only when selected; prevent stale caches from pinning broken or unsafe versions.
9. Deployment design does not authorize a live release.

## Workflow

1. Confirm source/toolchain/dependency, environments, browser support, hosting/CDN, configuration, compatibility, security, and release constraints.
2. Define build/artifact, config/flags, assets/cache, source-map/provenance, promotion/exposure, rollout/recovery, and evidence contracts.
3. Map implementation tasks and verification without embedding live secrets or executing release.
4. Report compatibility gaps, operational ownership, residual risks, and unresolved decisions.

## Reference routing

- Read [build-artifact-release-matrix.md](references/build-artifact-release-matrix.md) for the delivery packet.
- Invoke `configuration-management-standard` and `deployment-release-standard` for shared configuration/release governance.
- Invoke `frontend-performance-standard` for asset budgets, `frontend-security-standard` for artifact/header/source-map security, and `frontend-observability-standard` for release attribution.

## Output

Return toolchain/dependency/browser baseline, reproducible build and artifact contract, public config/flag matrix, asset/CDN/browser cache lifecycle, source-map/provenance/retention controls, promotion/exposure/compatibility strategy, rollout/rollback/recovery evidence, owners, residual risks, and unresolved decisions.
