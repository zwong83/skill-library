---
name: backend-api-design-standard
description: Design, implement, or review stable HTTP, gRPC, GraphQL, and internal service APIs, including protocol choice, resource and operation semantics, schemas, validation, errors, idempotency, pagination, compatibility, versioning, authentication and authorization boundaries, rate limits, observability, and deprecation.
---

# Backend API Design Standard

Use this skill when an API is introduced, changed, reviewed, or implemented. Produce a contract that callers and providers can evolve independently without guessing.

## Core Rules

1. Select the API design from caller needs, interaction shape, latency, compatibility, and operational constraints. Step 2 governs the choice for each interaction.
2. Define every operation's purpose, caller, authorization subject/action/resource, input, output, side effects, consistency, and completion semantics.
3. For every field, specify type, format, constraints, required/optional status, nullable status, default behavior, omission semantics, repetition, and unknown-field behavior.
4. Follow protocol semantics. For HTTP, use methods, status codes, headers, caching, and conditional requests consistently. For gRPC, define service methods, protobuf compatibility, status mapping, deadlines, and cancellation.
5. Use stable, machine-readable errors. Coordinate public error contracts with `exception-error-standard`; do not expose stack traces or internal implementation details.
6. Define duplicate handling, idempotency, concurrency behavior, deadlines, cancellation, safe retry conditions, rate limits, and partial-success behavior.
7. Prefer backward-compatible additive evolution. State versioning, support, deprecation, migration, and removal rules before the first breaking change.
8. Keep transport DTOs separate from domain and persistence models when their responsibilities or evolution differ.
9. Treat authentication, authorization, tenant isolation, input limits, sensitive-field handling, and audit requirements as contract properties.
10. Make pagination, filtering, sorting, batching, and query limits deterministic and bounded.

## Mandatory Workflow

**Complete steps 1 through 8 in order for every API design, implementation, or review task.** Record the outcome of each step for the affected contract. A focused change may confirm existing decisions with evidence. Mark a step or check `Not applicable` with a reason when it falls outside the interaction or task scope. If a required input or decision is missing, mark the affected step `Blocked` and stop dependent work.

1. Confirm consumers, use cases, trust boundaries, data classification, expected traffic, latency goals, and compatibility commitments. Distinguish hard requirements from preferences.
2. **Select or confirm the best-fit API design for each interaction.** Use [API design selection](references/contracts-and-protocols.md#api-design-selection) to compare plausible interaction styles, protocols, and contract shapes against the requirements. Eliminate options that fail a hard requirement and select the simplest viable design that fits the remaining priorities. Record the deciding requirements and tradeoffs. Confirm an approved design against the current requirements and route material changes through System Design.
3. Define resources or operations and their state transitions, side effects, consistency, and ownership.
4. Specify request, response, event, and error schemas field by field.
5. Define authentication, authorization, validation, idempotency, concurrency, pagination, limits, deadlines, and cancellation.
6. Define compatibility, versioning, deprecation, and consumer migration behavior.
7. Define the applicable metrics, structured logs, and traces. Plan contract, compatibility, and negative tests with evidence criteria.
8. Apply the readiness gate and relevant review checks before starting affected implementation. Record evidence, gaps, and pending verification. For implementation and review tasks, also report the checks actually run and their results.

## Readiness Gate

Claim implementation readiness only after all eight steps have a recorded outcome and every applicable criterion below is satisfied. Assign unresolved decisions to an owner. A blocked step prevents readiness for the affected work.

- consumers and ownership are known;
- operations, schemas, validation, and side effects are unambiguous;
- authorization and tenant boundaries are explicit;
- errors, idempotency, concurrency, deadlines, and retry safety are defined;
- list operations are bounded and deterministic;
- compatibility, versioning, and deprecation are defined;
- rate and payload limits are specified;
- observability and contract verification are planned.

## Reference Routing

- Start step 2 with [API design selection](references/contracts-and-protocols.md#api-design-selection). Read and apply the rules listed for each selected candidate. Consult another candidate's rules during selection only when they resolve a decision. Read [operation contracts](references/contracts-and-protocols.md#operation-contract) or [shared security and data boundaries](references/contracts-and-protocols.md#shared-security-and-data-boundaries) for the contract question at hand.
- Read the relevant sections of [evolution and operations](references/evolution-and-operations.md) for compatibility, pagination, limits, observability, or deprecation. Apply the relevant [review checklist](references/evolution-and-operations.md#review-checklist) items in step 8.
- Invoke `software-security-standard` for identity, authorization, isolation, sensitive data, validation, secrets, cryptography, audit, abuse controls, and security evidence.
- Invoke `contract-testing-standard` for provider/consumer conformance and compatibility verification of the approved contract.
- Invoke `exception-error-standard` for the internal error model and public error translation.
- Invoke `backend-resilience-standard` for deadlines, retries, circuit breakers, overload control, degradation, and recovery.
- Invoke `log-trace-standard` when event and span contracts are needed.

## System Design and SDD Boundary

- In System Design, decide protocol, ownership, operation semantics, schemas, authorization boundaries, compatibility, idempotency, consistency, limits, and failure behavior.
- In SDD, implement the approved contract with concrete framework mappings, serializers, validators, handlers, middleware, client settings, and tests.
- If implementation reveals a material contract, ownership, protocol, security, compatibility, or consistency change, return the decision to System Design before coding proceeds.

## Standards Basis

Use the current official protocol specification and deployed framework documentation. HTTP semantics should align with RFC 9110; HTTP problem responses may use RFC 9457. gRPC APIs should align with official gRPC guidance and protobuf compatibility rules. Do not treat framework defaults as the contract.

## Expected Output

Return a brief numbered record of the eight steps with the outcome and evidence or next action for each. For a full design, include the selection rationale, operation catalogue, schemas, authorization matrix, validation and errors, idempotency and concurrency, pagination and limits, compatibility and deprecation, observability, and verification plan. For focused work, report the affected contract and cite existing decisions that still apply.
