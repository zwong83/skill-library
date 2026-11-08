# UI Test Matrix

Allocate each TA case to the smallest UI layer that proves the risk.

| Category | Primary evidence | Typical risks |
|---|---|---|
| Component/rendering | Isolated render and behavior assertions | conditional content, formatting, local validation |
| Interaction/state | User events and state transitions | focus, enablement, navigation, async state, forbidden actions |
| Visual | Reviewed image difference against governed baseline | layout, clipping, overlap, typography, theme |
| Accessibility | Automated and targeted manual evidence | semantics, name/role/value, keyboard, focus, contrast, reflow |
| Compatibility | Selected browser/device/viewport/locale matrix | platform-specific behavior and responsive layout |
| UI end-to-end | Critical user journey through deployed boundaries | routing, authentication, service integration, persistence |

For each case record the category, positive/negative/boundary classification, preconditions, exact user action, expected visible state, forbidden action or side effect, data, environment, matrix subset, automation, evidence, and owner.

Include relevant initial, loading, success, empty, partial, validation, unauthorized/forbidden, dependency-error, timeout, offline/interrupted, retry, and recovered states. Mark a state `Not Applicable` only with a reason traceable to the approved behavior.
