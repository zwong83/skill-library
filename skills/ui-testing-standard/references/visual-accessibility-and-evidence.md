# Visual, Accessibility, and Evidence

## Visual baselines

Pin relevant browser/runtime, viewport, device scale, theme, locale, fonts, animations, time, and data. Review a baseline change against the approved design; do not auto-accept a new image merely to make the test pass. Record the reviewer and reason for intentional changes.

## Accessibility

Use automated rules for detectable issues, then add keyboard order, visible focus, dialog/focus restoration, semantic announcements, zoom/reflow, contrast, and assistive-technology checks according to user and compliance risk. An automated scanner passing is not proof of complete accessibility.

## Diagnostics and privacy

Retain the smallest useful failure artifacts: expected/actual/diff images, trace, console/network failures, DOM/accessibility snapshot, browser/version, viewport, and test data identity. Redact tokens, personal data, internal identifiers, and sensitive page content before retaining or publishing artifacts.
