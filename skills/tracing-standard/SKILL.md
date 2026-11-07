---
name: tracing-standard
description: Design, implement, or review distributed tracing across languages and services. Use for span boundaries, stable names, context propagation, links, attributes, status, sampling, async messaging, log correlation, privacy, cost, and trace-quality testing; do not create spans for every function or use trace context as business/security state.
---

# Tracing Standard

Use this skill to expose causality, latency, failure location, and cross-boundary execution paths. A trace is not a call log: instrument operations that matter for diagnosis, performance, reliability, or service ownership.

## When to use

- tracing inbound/outbound requests, RPCs, database calls, queues, jobs, workflows, or meaningful internal stages;
- designing parent/child relationships, span links, propagation, sampling, or trace/log correlation;
- diagnosing broken context, orphan spans, unstable names, excessive attributes, missing failures, or trace cost;
- specifying distributed-trace requirements in System Design or SDD/OpenSpec;
- reviewing custom instrumentation around gaps not covered by maintained auto-instrumentation.

Prefer maintained automatic instrumentation and semantic conventions for common frameworks/protocols. Add custom spans only where they reveal important application work not already visible.

## Workflow

1. Identify the operational question and critical path the trace must explain.
2. Map process/service/message boundaries and select meaningful operations as spans.
3. Define stable low-cardinality span names, kinds, parents or links, and start/end ownership.
4. Propagate context through supported carriers across synchronous and asynchronous boundaries.
5. Define bounded attributes at span creation when they may affect sampling; follow approved semantic conventions.
6. Define error/status behavior, cancellation, timeout, retry, and partial-success semantics.
7. Design head/tail sampling, retention, cost, and investigation requirements without assuming every trace is retained.
8. Correlate structured logs/events with active trace context and apply the same sensitive-data rules.
9. Test context propagation, topology, timing, status, errors, sampling behavior, and span completion.

## Reference routing

- Read [references/span-design.md](references/span-design.md) for boundaries, naming, attributes, status, lifecycle, and errors.
- Read [references/context-and-correlation.md](references/context-and-correlation.md) for propagation, messaging, links, baggage, and logs.
- Read [references/sampling-and-cost.md](references/sampling-and-cost.md) for sampling, cardinality, performance, retention, and privacy.
- Read [references/review-checklist.md](references/review-checklist.md) during code review or convergence.

## Core rules

- Use stable operation names; never embed user IDs, order IDs, URLs with variable path segments, SQL values, or error messages in span names.
- Create one span per meaningful operation, not per helper or trivial function.
- Every started span must end exactly once, including error, timeout, and cancellation paths; use language-native scopes/finally constructs.
- Preserve causal parent/child relationships. Use links for fan-in, batch, scheduled, or otherwise non-tree causal relationships.
- Propagate standard context rather than inventing incompatible headers. Validate trust boundaries and never treat incoming trace/baggage fields as authorization.
- Follow semantic conventions for common protocols and attributes. Keep custom keys stable, documented, bounded, and vendor-neutral.
- Keep span status unset for normal success unless project conventions require explicit success; set error only according to the operation's contract and semantic convention.
- Record exceptions/events through the current supported library guidance. For new OpenTelemetry-style events, prefer structured log events correlated with the span because the Span Event API is being deprecated; retain compatibility where existing instrumentation requires it.
- Do not put secrets, tokens, raw payloads, or unapproved personal data in span attributes, baggage, links, events, or status descriptions.
- Do not manually create child spans around operations already instrumented unless the additional span answers a distinct diagnostic question.

## Relationship to logging

Invoke `logging-standard` when defining events, severity, error records, audit/security logs, redaction, or log volume. Traces show causal paths and timing; logs provide queryable event detail. Correlate them through active context without duplicating the same large payload.

## Expected output

Provide:

1. traced operation and diagnostic goal;
2. span boundaries, names, kinds, parent/link topology, and lifecycle owner;
3. propagation and async/message behavior;
4. attributes, status, error, retry, timeout, and cancellation semantics;
5. sampling, cost, privacy, and retention decisions;
6. log/event correlation;
7. verification plan and actionable review findings.

Follow the target language's OpenTelemetry or project-approved tracing library and semantic conventions; do not add vendor lock-in without an approved reason.
