# System Design Index Template

Keep this document short. It is the navigation, status, and approval authority, not a summary copy of the technical design.

## Document control

Record project/system, SD version, status, date, author/owner/reviewers, target release, and approval status.

## Source baseline

List governing BRD/PRD/SRS/FRS/SA/Change Request or equivalent path, version, status, and relevant IDs. Record only material unresolved source items and the next owner action.

## Authoritative artifact register

| Artifact | Path | Version/hash | Status | Owner |
|---|---|---|---|---|
| Backend SD | | | Backend-Ready / Blocked / N/A | |
| Frontend SD | | | Frontend-Ready / Blocked / N/A | |
| Integration SD | | | Integration-Ready / Blocked / N/A | |
| Contract artifact(s) | | | Draft / Contract-Ready / Blocked / N/A | |
| Database design artifact(s) | | | Draft / Data-Ready / Blocked / N/A | |

List only applicable contract formats, such as OpenAPI, AsyncAPI, GraphQL schema, or Protobuf. Do not create unused placeholders.

## Feature and diagram coverage

Use the matrix from [feature-diagram-coverage.md](feature-diagram-coverage.md). Include every in-scope feature, source/SA IDs, owning document, diagram IDs, current/problem coverage for brownfield changes, target technical-flow coverage, conditional component/data/state/middleware views, verification, and status. Keep diagrams in their authoritative Backend/Frontend/Integration documents; the Index stores links and readiness only.

## Data and middleware artifact status

When applicable, record versions/statuses for the physical model, data dictionary, proposed DDL, DML/query catalog, transaction/concurrency matrix, indexes/access paths, migration/backfill/recovery artifacts, and middleware register/topology. Use `Not Applicable` with a source-based rationale for unaffected categories.

## Specialist routing and status

| Profile | Required / Conditional / N/A | Trigger/source IDs | Status | Target document |
|---|---|---|---|---|

Keep this table compact. Do not duplicate specialist reasoning.

## Readiness

Record:

- `Contract-Ready`: status, contract version/hash, date, and unresolved impact;
- `Backend-Ready`, `Frontend-Ready`, and `Integration-Ready` as applicable;
- `Data-Ready` and `Middleware-Ready` when those scopes are applicable;
- overall `SD-Ready`: Ready / Conditionally Ready / Blocked;
- implementation prerequisites and next authorized lifecycle action.

## Open decisions and risks

List only unresolved items that can change scope, behavior, ownership, contracts, controls, targets, implementation, or release safety. Link the optional working `open-decisions.md`; do not duplicate resolved history.

## Review verdict and approvals

Record the independent review verdict, review date/version, actionable blocker/major finding IDs, disposition, required sign-offs, and actual approval status. Do not infer approval from document presence or a `Ready` review verdict.

## Change history

Record material document-set or contract-version changes. Routine editorial edits need not be repeated across every document.
