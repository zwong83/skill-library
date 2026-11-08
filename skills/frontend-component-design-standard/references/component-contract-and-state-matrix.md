# Component Contract and State Matrix

For each component or governed primitive record:

| Field | Content |
|---|---|
| Identity | name, purpose, feature/design-system owner, reuse scope |
| Contract | inputs, outputs/events, slots/children, defaults, invariants, controlled/uncontrolled mode |
| States | loading, empty, success, partial, validation, disabled, unauthorized, error, retry, recovered |
| Interaction | keyboard/pointer/touch, focus order/restoration, announcements, cancellation, side effects |
| Presentation | tokens, variants, theme, responsive/content/locale constraints, motion |
| Boundaries | state/data dependencies, authoritative rules excluded, extension points, failure boundary |
| Verification | unit/component, UI interaction, visual, accessibility, compatibility evidence |

Do not turn incidental markup, internal hooks, framework lifecycle, or CSS structure into a public component contract unless consumers truly depend on it.
