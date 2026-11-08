---
name: frontend-component-design-standard
description: Design or review maintainable web UI component responsibilities, APIs, composition, state variants, forms, design-system integration, accessibility semantics, and reuse boundaries; not for page-level rendering architecture or visual asset creation.
---

# Frontend Component Design Standard

Use this skill when component responsibilities, contracts, composition, form behavior, or design-system integration need implementation-ready decisions.

## Core rules

1. Give each component a coherent user-facing responsibility and explicit owner; split by independent behavior/change, not arbitrary size limits.
2. Define inputs, outputs/events, slots/children, defaults, controlled/uncontrolled behavior, invariants, side effects, focus semantics, and lifecycle.
3. Cover loading, empty, success, partial, validation, disabled, unauthorized, dependency-error, timeout, retry, and recovered states where applicable.
4. Prefer composition over variant explosions and duplicated components. Promote reuse only after a stable shared concept exists.
5. Keep authoritative business rules outside presentation components; components may present approved outcomes and perform local shape/interaction validation.
6. Use design tokens and governed primitives for visual consistency; define variants, responsive behavior, themes, content overflow, and localization constraints.
7. Define forms by field contract, validation timing, server-error mapping, submission/idempotency state, focus/error summary, cancellation, and unsaved-change behavior.
8. Preserve semantic structure, keyboard behavior, accessible names/relationships, announcements, and reduced-motion behavior as component contracts.

## Workflow

1. Derive component responsibilities from approved journeys, route/module boundaries, UX states, and design-system assets.
2. Create the component/state/variant matrix and public contracts.
3. Decide composition, ownership, reuse, forms, accessibility, and test seams.
4. Map each material state and interaction to verification evidence and unresolved design dependencies.

## Reference routing

- Read [component-contract-and-state-matrix.md](references/component-contract-and-state-matrix.md) for the required component packet.
- Invoke `frontend-experience-standard` for responsive, accessibility, localization, theme, motion, and support-matrix decisions.
- Invoke `frontend-state-data-standard` when state or data ownership crosses component boundaries.
- Invoke `ui-testing-standard` for implementation-level component, interaction, visual, and accessibility verification.

## Output

Return component register, responsibilities/ownership, component APIs, composition map, state/variant matrix, form contracts, design-system/token dependencies, accessibility semantics, test seams/evidence, alternatives, and unresolved decisions.
