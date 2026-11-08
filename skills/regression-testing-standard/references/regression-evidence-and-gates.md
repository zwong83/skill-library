# Regression Evidence and Gates

## Result classification

Classify each non-pass as product defect, test defect, environment failure, known accepted issue, blocked prerequisite, or inconclusive/flaky result. Preserve the original failure and any retry evidence.

## Minimum report

Record base and target revisions, change IDs, environment and dependency versions, selected suites/cases, commands, counts, duration, pass/fail/skip/retry, artifacts, defect links, exclusions, gaps, and residual risk.

## Verdicts

- `Regression-Passed`: all required evidence passed and remaining exclusions/gaps are explicitly owned and accepted outside the claimed scope.
- `Regression-Failed`: a required test found a product defect or approved behavior is not preserved.
- `Regression-Blocked`: required execution or trustworthy interpretation is impossible because prerequisites, environment, data, ownership, or stability are missing.

Do not use pass percentage alone. A single failed critical journey, compatibility contract, migration, authorization, or data-integrity case can fail the gate.
