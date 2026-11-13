---
name: exception-error-standard
description: Design, implement, refactor, or review error and exception handling across synchronous APIs, jobs, and message consumers, including taxonomy, throw/return choices, propagation, translation, retries, compensation, boundary mapping, logging, security, and verification.
---

# Exception and Error Handling

Use this skill to make failures explicit, actionable, safe, and consistent. Error handling is part of the system contract, not a collection of local `try/catch` blocks.

## Core rules

- **Every application-defined error and exception must carry a reusable code declared in an error-code enum.** Define one enum member for each distinct failure in the owning domain or shared application contract. Reuse that member when the same failure is thrown, returned as a typed result, translated, or mapped at a boundary. Create the member if it is missing.
- **Every error-code enum member must declare a stable integer `code` and a non-empty text `message` safe to expose.** The enum is the source for both fields. Use the same pair for the same failure in exceptions, typed results, and public error mappings. Serialize `code` as a number in formats that support numeric fields. Keep per-occurrence details and causes separate. Preserve compatibility with existing published contracts. Use a closed, typed equivalent where the language has no native enum.
- Translate infrastructure and vendor failures to the matching application enum member. For an unexpected failure with no specific mapping, use the application enum's internal-error member and retain the original cause in protected diagnostics.
- **Require one reusable exception class per domain exception.** Look for the domain's existing class for the same business failure and reuse it at every throw or translation site. If none exists, define it once in the owning domain and create a fresh instance for each occurrence. Initialize its message from the enum and attach context and causes separately.
- Extend the appropriate domain base exception when one exists. Introduce a specialized subclass only when it represents a distinct domain failure or needs a different catch, recovery, or boundary mapping. In languages without exception classes, reuse the idiomatic named error type for that failure.
- Expected business outcomes may use typed results, discriminated unions, status values, or documented exceptions according to language conventions. Do not use exceptions for ordinary control flow when the language has a clearer outcome model.
- Throw or return an error at the layer that detects a failed contract. Catch only to recover, retry, compensate, translate, add meaningful context, perform required cleanup, or map at a boundary.
- Preserve the original cause and stack/diagnostic chain safely. Never swallow failures or replace them with an uninformative generic error.
- Domain/application code must not expose HTTP status classes, Redis/Kafka exceptions, SQL exceptions, or vendor SDK errors as its public contract.
- Log the final owned outcome once. Do not `catch -> log -> throw` at every layer.
- Retry only transient, idempotent or safely deduplicated operations with bounded attempts, backoff, jitter, timeout budget, and a terminal action.
- Do not expose stack traces, secrets, internal topology, raw queries, or sensitive payloads to clients or untrusted messages.
- Cancellation, deadline expiry, validation, business rejection, conflict, dependency failure, and internal defect are different outcomes; do not collapse them into one generic server error.

## Mandatory workflow

**Complete steps 1 through 7 in order for every error and exception handling task.** Identify the task mode and scope first. Carry out each applicable step and record its outcome. For an existing system, confirm applicable decisions against the current contract and evidence. A focused task can make a step brief, but it still needs an outcome. Use `Not applicable` only when a step does not apply and record why. Mark a step `Blocked` when it lacks a required input or decision, and stop dependent work.

For a focused refactor, incident, or review, identify the observable failure or responsibility being changed.

1. Inventory failure modes from requirements, invariants, dependencies, concurrency, security, and operations.
2. Define taxonomy, retryability, severity, ownership, and client/operator visibility. Assign or reuse an enum member with a stable integer `code` and a text `message` for each error or exception in scope. When implementing, add missing definitions and replace inline codes and messages in the affected paths.
3. Define throw/return rules and translations at interface, application, domain, and infrastructure boundaries. Identify the reusable type for each domain exception in scope and justify any specialized subtype. When implementing, create missing types and migrate affected duplicate definitions to the shared type where compatibility permits.
4. Specify API, job, scheduler, and message-consumer terminal behavior.
5. Define timeout, retry, idempotency, compensation, circuit-breaking, fallback, and dead-letter behavior where applicable.
6. Align logging, tracing, metrics, alerts, and sensitive-data handling.
7. Verify the applicable happy paths, material failure classes, translation, retry exhaustion, duplicate delivery, cancellation, and redaction. Confirm that exceptions and typed results for the same failure use the same enum member and that boundary mappings preserve its numeric `code` and text `message`. Run the relevant checks for implementation, specify them for design, and assess available evidence for review.

## Exception responsibilities

When helper roles are unclear, separate assertions that raise on failure, factories that return exceptions, translators that preserve causes, and handlers that map failures at application boundaries. Use the project language and naming conventions. Before refactoring, read callers and preserve throw or return behavior, exception types, codes, causes, messages, and boundary mappings. Keep compatibility aliases when the project policy requires them.

## Readiness gate

Require the operation/use-case contract, business failure semantics, external interface behavior, dependency failure modes, timeout/cancellation expectations, and security/data-classification constraints that affect errors. For SDD, require the approved SD error model and target language/framework conventions. Block implementation-ready status when retryability, terminal behavior, public error exposure, or ownership of recovery remains unresolved.

Claim completion only after every workflow step has a recorded outcome. A blocked applicable step prevents a readiness claim. Report planned checks as pending verification until they run.

## Choose references for the task

Start with the reference that resolves the current failure or design decision. Add another only when the task changes a separate contract, boundary, recovery behavior, or review requirement.

| Decision or symptom | Start here |
|---|---|
| Define, reuse, or review an enum code and its default message | [Error codes and default messages](references/error-codes-and-messages.md) |
| Choose an error category, reusable exception type, subtype, typed outcome, or public error shape | [Taxonomy and contracts](references/taxonomy-and-contracts.md) |
| Decide where to throw, return, catch, translate, log, or expose a failure | [Propagation and boundaries](references/propagation-and-boundaries.md) |
| Refactor generic exception helpers or clarify assertion, factory, translator, or handler roles | [Exception refactoring examples](references/examples.md). Read the section for the role being changed, or the naming migration map when callers must move. |
| Decide whether to retry, fall back, compensate, open a circuit, or take terminal action | [Retry and recovery](references/retry-and-recovery.md) |
| Review or approve an error design or implementation | [Review checklist](references/review-checklist.md), scoped to the change |

For example, start a helper refactor with the relevant examples and verify existing callers and behavior. Add boundary guidance if the public mapping changes. If the only question is whether a timed-out operation can be repeated, start with retry and recovery.

## SD and SDD boundary

System Design defines the taxonomy, ownership, cross-component failure contracts, boundary mappings, retry/timeout principles, and recovery model. SDD/OpenSpec defines concrete error types/results, codes, handlers, mappings, retry policies, configuration, implementation tasks, and tests for the approved change.

## Expected output

Include a brief numbered record of steps 1 through 7 with the outcome and evidence or next action for each step. Explain any `Not applicable` or `Blocked` outcomes.

Report the affected error behavior, preserved contracts, risks, and verification. For a full error design, include applicable failure modes, taxonomy, propagation and mappings, recovery, telemetry ownership, and security decisions. For reviews, include source locations and actionable severity.
