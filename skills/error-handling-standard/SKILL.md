---
name: error-handling-standard
description: Design, implement, or review language-neutral error handling across synchronous APIs, jobs, and message consumers, including taxonomy, throw/return choices, propagation, translation, retries, compensation, boundary mapping, logging, security, and verification.
---

# Error Handling Standard

Use this skill to make failures explicit, actionable, safe, and consistent. Error handling is part of the system contract, not a collection of local `try/catch` blocks.

## Core rules

- Define stable error categories and machine-readable codes before choosing exception classes or framework handlers.
- Expected business outcomes may use typed results, discriminated unions, status values, or documented exceptions according to language conventions. Do not use exceptions for ordinary control flow when the language has a clearer outcome model.
- Throw or return an error at the layer that detects a failed contract. Catch only to recover, retry, compensate, translate, add meaningful context, perform required cleanup, or map at a boundary.
- Preserve the original cause and stack/diagnostic chain safely. Never swallow failures or replace them with an uninformative generic error.
- Domain/application code must not expose HTTP status classes, Redis/Kafka exceptions, SQL exceptions, or vendor SDK errors as its public contract.
- Log the final owned outcome once. Do not `catch -> log -> throw` at every layer.
- Retry only transient, idempotent or safely deduplicated operations with bounded attempts, backoff, jitter, timeout budget, and a terminal action.
- Do not expose stack traces, secrets, internal topology, raw queries, or sensitive payloads to clients or untrusted messages.
- Cancellation, deadline expiry, validation, business rejection, conflict, dependency failure, and internal defect are different outcomes; do not collapse them into one generic server error.

## Workflow

1. Inventory failure modes from requirements, invariants, dependencies, concurrency, security, and operations.
2. Define taxonomy, stable codes, retryability, severity, ownership, and client/operator visibility.
3. Define throw/return rules and translations at interface, application, domain, and infrastructure boundaries.
4. Specify API, job, scheduler, and message-consumer terminal behavior.
5. Define timeout, retry, idempotency, compensation, circuit-breaking, fallback, and dead-letter behavior where applicable.
6. Align logging, tracing, metrics, alerts, and sensitive-data handling.
7. Test happy paths, every material failure class, translation, retry exhaustion, duplicate delivery, cancellation, and redaction.

## Readiness gate

Require the operation/use-case contract, business failure semantics, external interface behavior, dependency failure modes, timeout/cancellation expectations, and security/data-classification constraints that affect errors. For SDD, require the approved SD error model and target language/framework conventions. Block implementation-ready status when retryability, terminal behavior, public error exposure, or ownership of recovery remains unresolved.

## Reference routing

- Read [references/taxonomy-and-contracts.md](references/taxonomy-and-contracts.md) when defining error categories, stable codes, or public contracts.
- Read [references/propagation-and-boundaries.md](references/propagation-and-boundaries.md) when deciding where to throw, catch, translate, log, or expose a failure.
- Read [references/retry-and-recovery.md](references/retry-and-recovery.md) when designing retries, fallback, compensation, circuit breakers, or terminal handling.
- Read [references/review-checklist.md](references/review-checklist.md) before approving design or code.

## SD and SDD boundary

System Design defines the taxonomy, ownership, cross-component failure contracts, boundary mappings, retry/timeout principles, and recovery model. SDD/OpenSpec defines concrete error types/results, codes, handlers, mappings, retry policies, configuration, implementation tasks, and tests for the approved change.

## Expected output

Provide a failure-mode register, error taxonomy and contract, propagation/translation map, boundary responses, retry/recovery matrix, logging/tracing ownership, security decisions, and verification plan. For reviews, include source locations and actionable severity.
