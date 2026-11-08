---
name: ui-testing-standard
description: Design, implement, execute, or review traceable user-interface tests across component rendering, interaction, state, accessibility, visual behavior, browser/device compatibility, and critical UI journeys; use for observable UI risk, not backend-only behavior.
---

# UI Testing Standard

Use this skill when correctness depends on what a user can see, operate, navigate, or understand through a graphical interface.

## Core rules

1. Trace every test to an approved UI requirement, TA case, defect, compatibility risk, or accessibility obligation.
2. Separate component/rendering, interaction/state, visual, accessibility, compatibility, and end-to-end journey evidence; one category does not prove the others.
3. Cover positive, negative, and boundary behavior for assigned UI cases, including loading, empty, error, disabled, unauthorized, slow, interrupted, and recovery states where applicable.
4. Assert user-observable outcomes and forbidden effects. A screenshot alone is not a complete behavioral oracle.
5. Prefer stable role, label, text, or explicit test identifiers over DOM structure, CSS implementation, timing, or coordinates.
6. Use condition-based waits for observable readiness; do not hide race conditions with arbitrary sleeps or unconditional retries.
7. Govern visual baselines by environment, viewport, theme, fonts, data, ownership, review, and intentional-update evidence.
8. Treat automated accessibility checks as one layer; include keyboard, focus, semantics, contrast, zoom/reflow, and assistive-technology review according to risk.
9. Define the supported browser, device, viewport, locale, theme, input method, and network matrix from product commitments and risk rather than testing every combination.
10. Preserve diagnostics such as screenshots, video, traces, console/network errors, accessibility findings, and environment metadata without exposing sensitive data.

## Workflow

1. Select TA cases assigned to UI and confirm observable states, supported matrix, and exact oracle.
2. Allocate each case to component, interaction, visual, accessibility, compatibility, or UI end-to-end coverage.
3. Define data, authentication/authorization state, environment, isolation, reset, selectors, and evidence.
4. Implement the smallest stable tests that prove the assigned risk without duplicating lower-level coverage.
5. Execute focused checks, then required browser/device/journey suites; classify failures and flakiness.
6. Record results, artifacts, baseline changes, untested combinations, accessibility limitations, and residual risk.

## Reference routing

- Read [ui-test-matrix.md](references/ui-test-matrix.md) to allocate UI cases and define states and environments.
- Read [visual-accessibility-and-evidence.md](references/visual-accessibility-and-evidence.md) for visual baselines, accessibility, diagnostics, and evidence.
- Invoke `unit-testing-standard` for UI logic or component behavior that can be proven without a real browser/runtime boundary.
- Invoke `integration-testing-standard` for browser-to-service, authentication, API, storage, or framework boundaries whose real semantics matter.
- Invoke `regression-testing-standard` when selecting an impacted UI regression suite.

## Output

Return source/TA case IDs, UI category and supported matrix, tests and files changed when authorized, environment/data/selectors, commands and actual results, screenshots/traces/accessibility/visual evidence, baseline decisions, flaky or blocked cases, untested combinations, and residual risk. Never report an unexecuted browser or accessibility check as passing.
