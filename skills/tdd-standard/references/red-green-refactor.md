# Red-Green-Refactor

## Red

- Select one behavior and one reason to fail.
- Write the smallest test with a complete oracle.
- Run it and confirm failure points to missing/incorrect behavior.
- If it fails because setup, syntax, environment, or an unrelated defect is broken, fix that prerequisite and re-establish the intended Red.

## Green

- Implement only enough approved behavior to pass.
- Do not hardcode a single example when the requirement is general.
- Keep security, error, state, transaction, and side-effect constraints intact.
- Run the focused test and relevant nearby tests.

## Refactor

- Improve production and test names, duplication, responsibilities, seams, fixtures, and clarity.
- Preserve externally observable behavior and approved architecture.
- Keep all affected tests green throughout or use very small reversible steps.

## Evidence

Record scenario/task ID, test name, expected Red reason, observed Red result, Green result, refactor summary, and broader suite result. Evidence may be concise command/output references; do not fabricate screenshots or logs.
