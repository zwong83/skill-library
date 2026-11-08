---
name: api-design-standard
description: Design, implement, or review stable HTTP, gRPC, GraphQL, and internal service APIs, including protocol choice, resource and operation semantics, schemas, validation, errors, idempotency, pagination, compatibility, versioning, authentication and authorization boundaries, rate limits, observability, and deprecation.
---

# API Design Standard

Use this skill when an API is introduced, changed, reviewed, or implemented. Produce a contract that callers and providers can evolve independently without guessing.

## Core Rules

1. Select HTTP, gRPC, GraphQL, streaming, or messaging from caller needs, interaction shape, latency, compatibility, and operational constraints. Do not choose by habit.
2. Define every operation's purpose, caller, authorization subject/action/resource, input, output, side effects, consistency, and completion semantics.
3. For every field, specify type, format, constraints, required/optional status, nullable status, default behavior, omission semantics, repetition, and unknown-field behavior.
4. Follow protocol semantics. For HTTP, use methods, status codes, headers, caching, and conditional requests consistently. For gRPC, define service methods, protobuf compatibility, status mapping, deadlines, and cancellation.
5. Use stable, machine-readable errors. Coordinate public error contracts with `error-handling-standard`; do not expose stack traces or internal implementation details.
6. Define duplicate handling, idempotency, concurrency behavior, deadlines, cancellation, safe retry conditions, rate limits, and partial-success behavior.
7. Prefer backward-compatible additive evolution. State versioning, support, deprecation, migration, and removal rules before the first breaking change.
8. Keep transport DTOs separate from domain and persistence models when their responsibilities or evolution differ.
9. Treat authentication, authorization, tenant isolation, input limits, sensitive-field handling, and audit requirements as contract properties.
10. Make pagination, filtering, sorting, batching, and query limits deterministic and bounded.

## Workflow

1. Confirm consumers, use cases, trust boundaries, data classification, expected traffic, latency goals, and compatibility commitments.
2. Choose the interaction style and protocol. Record alternatives and the reason for the selection.
3. Define resources or operations and their state transitions, side effects, consistency, and ownership.
4. Specify request, response, event, and error schemas field by field.
5. Define authentication, authorization, validation, idempotency, concurrency, pagination, limits, deadlines, and cancellation.
6. Define compatibility, versioning, deprecation, and consumer migration behavior.
7. Add observability and verification: metrics, structured logs, traces, contract tests, compatibility tests, and negative tests.
8. Review against the readiness gate before implementation.

## Readiness Gate

An API is implementation-ready only when:

- consumers and ownership are known;
- operations, schemas, validation, and side effects are unambiguous;
- authorization and tenant boundaries are explicit;
- errors, idempotency, concurrency, deadlines, and retry safety are defined;
- list operations are bounded and deterministic;
- compatibility, versioning, and deprecation are defined;
- rate and payload limits are specified;
- observability and contract verification are planned;
- unresolved decisions are assigned and block affected implementation.

## Reference Routing

- Read [contracts-and-protocols.md](references/contracts-and-protocols.md) for protocol selection and concrete HTTP, gRPC, GraphQL, schema, security, and DTO rules.
- Read [evolution-and-operations.md](references/evolution-and-operations.md) for compatibility, pagination, limits, observability, deprecation, and review checks.
- Invoke `software-security-standard` for identity, authorization, isolation, sensitive data, validation, secrets, cryptography, audit, abuse controls, and security evidence.
- Invoke `contract-testing-standard` for provider/consumer conformance and compatibility verification of the approved contract.
- Invoke `error-handling-standard` for the internal error model and public error translation.
- Invoke `resilience-standard` for deadlines, retries, circuit breakers, overload control, degradation, and recovery.
- Invoke `logging-standard` and `tracing-standard` when event and span contracts are needed.

## System Design and SDD Boundary

- In System Design, decide protocol, ownership, operation semantics, schemas, authorization boundaries, compatibility, idempotency, consistency, limits, and failure behavior.
- In SDD, implement the approved contract with concrete framework mappings, serializers, validators, handlers, middleware, client settings, and tests.
- If implementation reveals a material contract, ownership, protocol, security, compatibility, or consistency change, return the decision to System Design before coding proceeds.

## Standards Basis

Use the current official protocol specification and deployed framework documentation. HTTP semantics should align with RFC 9110; HTTP problem responses may use RFC 9457. gRPC APIs should align with official gRPC guidance and protobuf compatibility rules. Do not treat framework defaults as the contract.

## Expected Output

Return the API decision, protocol rationale, operation catalogue, schema definitions, authorization matrix, validation and error contract, idempotency and concurrency behavior, pagination and limits, compatibility and deprecation plan, observability, verification plan, assumptions, and unresolved decisions.
