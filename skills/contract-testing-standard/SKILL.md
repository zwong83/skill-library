---
name: contract-testing-standard
description: Design, implement, execute, or review consumer/provider contract and compatibility tests for HTTP, gRPC, GraphQL, events, messages, and shared schemas; use when independent components must evolve safely, not for full end-to-end journeys.
---

# Contract Testing Standard

Use this skill when a provider and one or more consumers need machine-verifiable evidence that requests, responses, messages, schemas, errors, and compatibility commitments remain mutually usable.

## Core rules

1. Identify the provider, each consumer, operation/message, contract source, supported versions, ownership, and compatibility policy.
2. Test consumer-observed semantics, not only schema shape: required/optional/null/omitted/default behavior, constraints, errors, headers/metadata, ordering scope, idempotency, pagination, deadlines, and side effects where contractual.
3. Distinguish consumer-driven contracts, provider conformance, schema/protocol compatibility, and deployed integration checks; state which claim each test can support.
4. Verify positive, negative, and boundary examples for every changed contractual partition, including unknown fields, missing/extra values, enum evolution, malformed content, version negotiation, and stable errors where applicable.
5. Prefer backward-compatible additive evolution. Evaluate removals, renames, narrowing, required-field changes, semantic changes, and default changes against every supported consumer.
6. Use generated or synthetic fixtures without secrets or unnecessary production data. Pin the contract, generator, serializer, protocol, and dependency versions needed to reproduce evidence.
7. Publish and verify contracts through the project-approved workflow; do not treat an unverified local snapshot as provider/consumer compatibility evidence.
8. Avoid duplicating full business journeys. Escalate real datastore/framework/network semantics to integration testing and multi-component user outcomes to System E2E.
9. Record base/target contract versions, consumer matrix, exact verification, broker/registry state when used, failures, pending consumers, and residual compatibility risk.
10. A provider cannot be released as compatible while a required supported consumer is failing, unverified, or silently excluded.

## Workflow

1. Select TA cases and build the provider/consumer/version matrix.
2. Resolve the authoritative contract, compatibility promise, ownership, publication/verification flow, and test environment.
3. Implement consumer expectations, provider verification, and schema/protocol compatibility checks at the lowest trustworthy boundary.
4. Execute positive, negative, boundary, version, and error cases; classify stale contracts, implementation defects, consumer defects, and infrastructure failures.
5. Publish or retain approved evidence and report unsupported consumers, breaking changes, migration needs, and residual risk.

## Reference routing

- Read [contract-matrix.md](references/contract-matrix.md) to define consumers, operations/messages, versions, and case allocation.
- Read [compatibility-and-evidence.md](references/compatibility-and-evidence.md) for evolution rules, publication, verification, and verdicts.
- Invoke `api-design-standard` for the approved contract and evolution policy.
- Invoke `messaging-standard` for event/message delivery semantics beyond schema compatibility.
- Invoke `integration-testing-standard` when real framework, serializer, registry, broker, or transport behavior is the selected risk.
- Invoke `system-e2e-testing-standard` only when the claim depends on a complete multi-component journey.

## Output

Produce `contract-test-report.md` or equivalent retained evidence. Return source/TA case IDs, provider/consumer/version matrix, contract locations and hashes/versions, cases and fixtures, commands/results, publication/verification evidence, breaking or pending changes, unverified consumers, migration requirements, residual risk, and `Contract-Passed`, `Contract-Failed`, or `Contract-Blocked`.
