---
name: log-trace-standard
description: Design, implement, review, or troubleshoot structured application logs and distributed tracing. Use for event and span contracts, severity, audit logging, redaction, sinks and rotation, context propagation, sampling, and runtime instrumentation.
---

# Log and Trace Standard

Identify the diagnostic, operational, or audit question. Logs record meaningful events at the owning boundary. Traces explain causal paths and latency across operations. Select logging, tracing, or their shared context based on the task. Follow the project's approved telemetry contract and existing libraries. For metrics-only work, use the applicable operability skill.

## Mandatory workflow

**Complete steps 1 through 7 in order for every logging or tracing task.** Identify the task mode and scope first. Carry out each applicable step and record its outcome. For an existing system, confirm applicable decisions against the current contract and evidence. A focused task can make a step brief, but it still needs an outcome. Use `Not applicable` only when a step does not apply and record why. Mark a step `Blocked` when it lacks a required input or decision, and stop dependent work.

1. Identify the diagnostic, audit, or operational question. Select logging, tracing, or both based on the requirement.
2. Confirm the applicable service boundaries, telemetry contract, runtime, libraries, collectors, and current evidence. Select the references that address the affected signal and requirement.
3. Define or confirm the logging contract when logging is in scope. Establish event ownership, schema, severity, privacy, and sink or retention policy as applicable.
4. Define or confirm the tracing contract when tracing is in scope. Establish span ownership, naming, lifecycle, status, attributes, sampling, and cost controls as applicable.
5. Define or confirm any context propagation, trust boundaries, and log-to-trace correlation the task requires. Check the impact on consumers of the existing telemetry.
6. Define or implement the applicable configuration and instrumentation. For reviews or investigations, assess the implementation and isolate the cause or gap.
7. Verify the behaviors affected by the task. Run the relevant checks for implementation, specify them for design, and assess available evidence for review.

## Logging

- Define stable event names, levels, outcomes, structured attributes, and the layer that owns each event. Log failures once at the owning boundary, preserving the original cause through safe structured exception handling.
- Keep variable data in bounded fields. Use stable service and operation identifiers, and a low-cardinality feature field when useful. Preserve the `【Service/Operation】` message prefix where the project uses or requires it. Keep the structured fields available for filtering and correlation.
- Separate operational and audit sinks when access, integrity, retention, or failure requirements differ. Prefer platform collection for containers and managed runtimes. Configure levels, sinks, sampling, rotation, and retention for the deployment.
- Sanitize untrusted fields and exclude secrets and unapproved sensitive data. Keep logging failure from disrupting business operations unless the approved audit contract requires fail-closed behavior.

## Tracing

- Prefer maintained automatic instrumentation and approved semantic conventions. Add custom spans for meaningful operations that existing instrumentation does not expose.
- Define stable, low-cardinality span names, kinds, attributes, status, and ownership. End each span exactly once, including cancellation, timeouts, and failures. Follow the operation's contract for error and success status.
- Preserve parent/child causality. Use links for fan-in, batches, scheduled work, or other relationships with multiple causal inputs.
- Propagate standard context across HTTP/RPC, messages, jobs, and async boundaries. Validate context at trust boundaries and keep it separate from authorization and business state.
- Define sampling and retention with investigation needs, privacy, cardinality, and cost in mind. Exclude secrets, raw payloads, and unapproved sensitive data from spans and baggage.

## Correlation and verification

Attach active trace and span IDs to structured logs through the instrumentation. Keep request, correlation, business, and message IDs distinct. Logs must still work without an active span. Prefer correlated named log events for new OpenTelemetry instrumentation where supported, and preserve existing span-event contracts when compatibility requires them.

In System Design, define the applicable event and span ownership, schemas, propagation, volume, privacy, routing, and investigation requirements. During implementation, inspect the runtime, library, collector, and existing configuration. Verify the behaviors affected by the task, such as event emission and redaction, sink behavior, context propagation, span lifecycle and status, sampling, or telemetry failure. Report concrete contracts, findings, and observed verification evidence.

## Readiness and output

Claim completion only after every workflow step has a recorded outcome. A blocked applicable step prevents a readiness claim. Report planned checks as pending verification until they run.

Include a brief numbered record of steps 1 through 7 with the outcome and evidence or next action for each step. Explain any `Not applicable` or `Blocked` outcomes.

## Choose references for the task

Start with the best matching reference. Add another only for a distinct requirement or finding. Use the runtime selector only when the implementation, transport, or deployed configuration affects the answer.

| Decision or symptom | Start here |
|---|---|
| Define event names, structured fields, business context, or required log attributes | [Event schema](references/event-schema.md) |
| Choose severity or reduce noisy, repeated, or expensive log events | [Severity and noise](references/severity-and-noise.md) |
| Route default, error, audit, security, or access logs and define rotation or retention | [Sink routing and files](references/sink-routing-and-files.md) |
| Decide what may be logged, how to redact it, or how to protect audit records | [Security and privacy](references/security-and-privacy.md) |
| Design span boundaries, names, attributes, lifecycle, error status, or exception reporting | [Span design](references/span-design.md) |
| Fix missing context, orphan spans, async links, baggage, or log-to-trace correlation | [Context and correlation](references/context-and-correlation.md) |
| Choose trace sampling, manage cardinality, or control tracing cost | [Sampling and cost](references/sampling-and-cost.md) |
| Implement or troubleshoot a particular framework, transport, message style, sink, or deployment | [Runtime implementation selector](references/runtime-implementation.md). Choose the relevant row or language. |
| Conduct a formal review | [Logging review](references/logging-review-checklist.md) or [tracing review](references/tracing-review-checklist.md), according to the affected signal. Use both for a review covering both signals. |

For example, a file rotation issue starts with sink routing and files. Add the runtime rotation reference if the collector or filesystem setup affects the fix. A trace that stops at a queue starts with context and correlation, with messaging instrumentation examples only if needed.
