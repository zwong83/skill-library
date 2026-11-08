---
name: frontend-experience-standard
description: Design or review implementation-ready responsive, accessibility, localization, theme, motion, content, browser/device/input, and complete UI-state behavior for web frontends; use to translate approved UX into engineering contracts, not to invent product or brand direction.
---

# Frontend Experience Standard

Use this skill to convert approved UX, visual/design-system references, accessibility obligations, localization, and platform support into explicit engineering decisions.

## Core rules

1. Preserve approved user goals and visual direction; identify missing UX decisions instead of inventing product behavior or brand assets.
2. Define responsive/adaptive behavior by content and task needs, including layout changes, overflow, touch targets, virtual keyboard, orientation, zoom, and reflow.
3. Make semantic structure, accessible names/relationships, keyboard operation, focus order/restoration, announcements, contrast, reduced motion, and assistive-technology expectations explicit.
4. Define localization for language, locale fallback, pluralization, interpolation, date/time/number/currency, timezone, text expansion, RTL/bidirectionality, sorting, and translated assets/content ownership.
5. Define theme/tokens, high-contrast needs, motion purpose/timing/cancellation, and reduced-motion alternatives without encoding inaccessible meaning by color or motion alone.
6. Cover loading, empty, partial, validation, disabled, unauthorized, offline/interrupted, timeout, error, retry, and recovery states consistently.
7. Select browser/device/viewport/input combinations from approved commitments and risk; do not promise support that cannot be tested and operated.
8. Treat consent, analytics, experimentation, and personalization as privacy-governed behavior with explicit fallback and user impact.

## Workflow

1. Confirm journeys, UX/design sources, content ownership, accessibility target, locales, support matrix, and unresolved decisions.
2. Build responsive, UI-state, accessibility, localization, theme/motion, and platform matrices.
3. Map requirements to components/routes, implementation constraints, test evidence, and owners.
4. Report gaps that block an implementation-ready frontend design.

## Reference routing

- Read [experience-matrix.md](references/experience-matrix.md) for the experience decisions and matrices written into Frontend SD.
- Invoke `frontend-component-design-standard` for component contracts and `ui-testing-standard` for implementation verification.
- Invoke `frontend-performance-standard` when responsive/media/font decisions affect measurable performance.
- Invoke `frontend-security-standard` when personalization, consent, identity, or client storage affects privacy/security.

## Output

Return responsive and UI-state matrices, accessibility contract, localization/RTL/content rules, theme/motion decisions, browser/device/viewport/input support matrix, privacy/consent dependencies, verification plan, gaps, and unresolved decisions.
