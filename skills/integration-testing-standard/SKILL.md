---
name: integration-testing-standard
description: Design, write, or review integration tests across real application boundaries such as databases, brokers, caches, HTTP/gRPC services, filesystems, frameworks, serialization, configuration, and security adapters, including environment fidelity, isolation, cleanup, failure behavior, and evidence; not for mocked unit tests.
---

# Integration Testing Standard

Use this skill when correctness depends on the behavior of at least one real integration boundary or runtime/framework mapping.

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

## Workflow

1. Select TA/OpenSpec scenarios assigned to integration level and define the boundary matrix.
2. Choose environment, dependency lifecycle, data, isolation, and cleanup.
3. Establish prerequisites and observable oracles across the boundary.
4. Implement assigned positive, negative, and boundary cases plus material transaction, failure, recovery, compatibility, and cleanup cases for the selected boundary.
5. Run focused tests repeatedly to detect isolation/flakiness, then required suites.
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
