---
name: integration-testing-standard
description: Design, write, or review application-logic integration tests across real application boundaries such as databases, brokers, caches, HTTP/gRPC services, filesystems, frameworks, serialization, configuration, and security adapters, including environment fidelity, isolation, cleanup, failure behavior, and evidence; not for mocked unit tests.
---

# Integration Testing Standard

## Input and output contract

This summary follows the detailed workflow and linked gates below. Record source owners, locations/versions and decision status; keep unknowns explicit.

- **Required inputs:** Approved scenarios/oracles, named real boundary and relevant application/dependency scope/versions.
- **Conditional inputs:** Representative infrastructure/data/isolation/cleanup and authorization for runs/writes; original evidence for review.
- **Optional context:** Prior defects, fixtures and coverage history.
- **Outputs:** Authorized tests, real-boundary matrix, commands/results, fidelity limits and residual risk.
- **Destination and consumer:** Use the workflow's existing, requested or documented default artifact/handoff location. Return results to the invoking agent or user for the identified downstream owner; this does not authorize automatic invocation or duplicate artifacts.
- **Completion:** Preserve real-boundary proof and case outcomes; mocks or connectivity alone cannot establish integration behavior.


Use this skill when application logic depends on at least one real integration boundary or runtime/framework mapping. Focus on data exchange, persistence, transactions, delivery, rule enforcement and failure/recovery behavior. UI interaction assertions remain with `ui-testing-standard`, compatibility as the primary risk with `contract-testing-standard`, and full deployed journeys with `system-e2e-testing-standard`; those specialists can reuse boundary-testing methods without changing case ownership.

## Core rules

1. Name the boundary and risk being integrated. “Integration test” is not synonymous with slow or multi-class test.
2. Exercise the real adapter/protocol/system whose semantics matter; mock only dependencies outside the selected boundary.
3. Use a representative product/version/configuration and record meaningful differences from production.
4. Isolate tests by database/schema/tenant/topic/key/namespace or lifecycle as appropriate; clean up reliably even after failure.
5. Control test data, clocks, asynchronous completion, retries, and eventual consistency with bounded condition-based waits, not arbitrary sleeps.
6. Verify success, validation, authorization/isolation, transaction boundaries, serialization, constraints, duplicate/idempotent behavior, timeout/failure, recovery, and emitted effects where applicable.
7. For database tests, prove constraints, queries, transactions, isolation/conflicts, migrations, and rollback behavior that unit tests cannot.
8. For messaging/cache tests, prove real delivery/acknowledgement/offset, ordering scope, retry/DLQ, schema, TTL/invalidation, and failure behavior selected by the design.
9. Keep credentials and sensitive production data out of test code and evidence.
10. Record exact environment, dependency versions, commands, results, skips, retries, and limitations.

## Existing tests and TDD evidence

Start by mapping assigned cases to existing tests, including TDD tests. Reuse suitable test assets; add or extend tests only for uncovered behavior or distinct risks. Assign a new run when requested, required by a project/CI gate, or needed because code/test revisions, dependencies, configuration, environment, data or the coverage scope changed. Preserve active TDD-cycle ownership.

In a review or evidence-reuse assignment, accept retained results only when their exact code/test snapshot, relevant environment/configuration/dependencies, case oracles, scope and provenance satisfy the current verification requirement. Record the evidence reference and reuse rationale; do not describe it as a new run. Missing, stale, flaky or insufficient evidence remains a gap and requires an appropriate check, not a pass. Focused TDD results do not automatically prove broader integration, regression or other specialist coverage. Reusing test files does not imply that their earlier results remain valid.

## Workflow

1. Select approved source scenarios (including supplied TA/OpenSpec cases) assigned to integration level and define the boundary matrix.
2. Choose environment, dependency lifecycle, data, isolation, and cleanup.
3. Establish prerequisites and observable oracles across the boundary.
4. Build and implement the assigned boundary scenario checklist: positive/negative/edge data, mapping/serialization, constraints, commit/rollback, authorization/isolation, duplicates/order/concurrency, partial failure, timeout/retry, recovery and cleanup where applicable. Map each to an approved case/oracle, record exclusions and return missing cases to the requester for analysis clarification. State untested combinations; connectivity and happy-path checks alone do not establish scenario completeness.
5. Run requested/required cases and affected suites in execution mode. Repeat where isolation/flakiness risk warrants it, retaining failures. For evidence review, apply the reuse criteria to the real-boundary results; do not infer fidelity from mocked or stale evidence.
6. Record fidelity gaps, evidence, residual risk, and ownership.

## Reference routing

- Read [integration-boundary-matrix.md](references/integration-boundary-matrix.md) to select real boundaries and scenarios.
- Read [environment-data-and-reliability.md](references/environment-data-and-reliability.md) for environments, data, isolation, cleanup, async waits, and flakiness.
- Invoke the corresponding API, database, cache, messaging, security, resilience, or configuration Skill only for the selected real boundary.
- Invoke `contract-testing-standard` when the primary risk is provider/consumer compatibility rather than real-boundary behavior.
- Invoke `unit-testing-standard` for behavior that does not require real infrastructure.
- Invoke `tdd-standard` when an integration test intentionally drives a boundary implementation.

## Output

Return source/scenario IDs, real boundaries and versions, environment/data/isolation design, tests and files changed when authorized, commands/results, fidelity limitations, flaky/blocked cases, evidence, and residual risk.
