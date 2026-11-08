# Frontend Performance Budgets and Evidence

| Budget | Define |
|---|---|
| Journey/route | population, percentile, cold/warm state, device/network, visible completion and interaction objective |
| Assets | document/data, JS, CSS, image, font, third-party compressed/transferred/executed cost |
| Main thread | parse/compile, rendering, hydration, long tasks, interaction work, scheduling/yield behavior |
| Memory/resources | heap trend, listeners/subscriptions, DOM size, caches/collections, cleanup on navigation |
| Delivery | CDN/browser cache state, compression, prioritization, preload/prefetch and invalidation |
| Evidence | lab configuration, field/RUM definition, baseline, repetitions/population, regression threshold, owner/gate |

Use the project's current approved metric definitions and tooling. Do not hardcode ecosystem-wide thresholds when the product requirement or deployed measurement definition differs.
