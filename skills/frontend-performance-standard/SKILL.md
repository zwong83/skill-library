---
name: frontend-performance-standard
description: Design, implement, or review measurable web-frontend loading, rendering, interaction, responsiveness, bundle, image/font, memory, caching, and real-user performance budgets and regression evidence; not for backend capacity planning.
---

# Frontend Performance Standard

Use this skill when user-perceived loading, rendering, interaction, memory, or asset cost can affect product success.

## Core rules

1. Translate critical journeys and supported devices/networks into measurable route and interaction objectives; do not use “fast” as acceptance.
2. Define field and controlled-lab evidence separately. Record metric definitions, percentiles, population, environment, tool/version, and known bias.
3. Allocate budgets across document/data, JavaScript, CSS, images, fonts, third-party code, rendering/hydration, long tasks, and memory.
4. Measure before optimizing and preserve correctness, accessibility, security, and maintainability.
5. Define code splitting, preload/prefetch, caching, image/font strategy, rendering/hydration, scheduling, virtualization, and worker use only when justified by measured risk.
6. Include cold/warm navigation, cache state, authentication/personalization, device capability, network variability, third-party behavior, and failure/degraded paths.
7. Detect memory/listener/resource leaks and unbounded client collections or subscriptions for long-lived sessions.
8. Compare like-for-like baselines and establish regression thresholds, ownership, and release consequences.

## Workflow

1. Identify critical routes/journeys, target populations, device/network assumptions, and approved objectives.
2. Build route/asset/interaction/memory budgets and measurement design.
3. Establish a reproducible baseline, identify bottlenecks, and select the smallest justified design controls.
4. Define lab, RUM, regression, release, and production guardrail evidence.

## Reference routing

- Read [budgets-and-evidence.md](references/budgets-and-evidence.md) for the performance decisions, budgets, and evidence mapping written into Frontend SD.
- Invoke `backend-performance-capacity-standard` for end-to-end/backend capacity or load/stress concerns.
- Invoke `frontend-architecture-standard` for rendering/code-split boundaries, `frontend-build-delivery-standard` for artifact/CDN behavior, and `frontend-observability-standard` for RUM.

## Output

Return route/journey objectives, device/network/population assumptions, asset/render/interaction/memory budgets, baseline and bottleneck evidence, selected controls, lab/RUM/regression plan, thresholds/gates, limitations, residual risk, and unresolved decisions.
