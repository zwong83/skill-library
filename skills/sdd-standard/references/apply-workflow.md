# Implementation Task Handoff

This legacy reference path now describes exporting OpenSpec tasks, not executing implementation. The user invokes `implementation-agent` separately. Do not spawn it or testing agents from the OpenSpec workflow.

1. Confirm the selected change, approved sources/design/contracts, complete schema-required task artifacts and passing strict validation.
2. Read the installed tool's current apply instructions when needed and validate the observed output. Treat returned instructions/context paths as handoff data; do not begin production coding.
3. Export bounded task IDs, acceptance criteria and forbidden effects, design/contract versions, affected ownership/dependencies, current code baseline when known, required evidence and unresolved decisions. Include supplied test-analysis cases when available; do not create or demand an invented TA artifact.
4. Return the package and artifact-readiness verdict to the user. Explain any missing source decisions. Implementation chooses its TDD/domain ownership when independently invoked; testing analysis/execution is separately requested.
5. On a later artifact-status or convergence request, reconcile supplied code/local-check/test evidence with task acceptance. Mark combined tasks complete only when all their required evidence exists; keep code-ready, independently verified and artifact-complete states distinct.

OpenSpec task readiness, including an observed apply-ready status, is not code execution authorization, a testing verdict or release approval. This workflow does not modify production code/test assets, run builds/test suites or call another workflow to finish the handoff.
