---
name: logging-standard
description: Design, implement, or review production application logging across programming languages. Use for structured events, severity, diagnostic context, trace correlation, security/audit events, redaction, volume, retention, and log-quality testing; do not add logs that duplicate telemetry, expose sensitive data, or merely narrate control flow.
---

# Logging Standard

Use this skill to make logs useful for incident diagnosis, security investigation, support, and operational analysis. A log is a durable event record, not a substitute for metrics, traces, tests, error handling, or a debugger.

## When to use

- adding or reviewing application, integration, audit, or security-event logs;
- defining a structured log schema, severity policy, event names, or correlation fields;
- diagnosing missing context, noisy duplicates, unsafe payloads, log injection, or excessive volume;
- implementing a feature whose failures, state transitions, privileged actions, or external dependencies must be diagnosable;
- specifying logging requirements in System Design or SDD/OpenSpec artifacts.

Do not log every function entry/exit, every loop item, successful hot-path detail, or the same exception at every layer. Record events at the boundary that owns the outcome and can add meaningful context.

## Workflow

1. Identify the diagnostic, security, audit, or operational question the log must answer.
2. Choose the owning event boundary and avoid duplicate recording across layers.
3. Define a stable event name, severity, outcome, error classification, and structured attributes.
4. Add request/job/message and trace context through supported instrumentation rather than manually inventing correlation identifiers.
5. Apply data classification, minimization, redaction, sanitization, access, retention, and deletion rules.
6. Estimate event rate, payload size, cardinality, cost, and alerting implications.
7. Ensure logging failure or backend unavailability does not corrupt the primary business operation unless an approved audit requirement explicitly demands fail-closed behavior.
8. Test event emission, fields, correlation, redaction, injection safety, duplicate suppression, and failure behavior.

## Reference routing

- Read [references/event-schema.md](references/event-schema.md) when defining structured fields, event names, outcomes, or trace correlation.
- Read [references/severity-and-noise.md](references/severity-and-noise.md) when choosing levels, reducing duplicates, or controlling volume.
- Read [references/security-and-privacy.md](references/security-and-privacy.md) for sensitive-data exclusion, sanitization, audit integrity, access, and retention.
- Read [references/review-checklist.md](references/review-checklist.md) during code review or convergence verification.

## Core rules

- Prefer structured, parameterized events with stable field names and types.
- Record what happened, where, outcome, relevant bounded context, and a safe error classification; do not depend on free-form messages alone.
- Keep event names and templates stable. Put per-request values in attributes, not event names.
- Correlate logs with active `TraceId`/`SpanId` or equivalent context when available. Do not use trace context as authentication or authorization evidence.
- Log an error once at the layer that owns or translates it. Lower layers may add telemetry only when they contribute distinct diagnostic value.
- Preserve the original exception/cause through the language's structured error mechanism where safe; avoid concatenating raw payloads into messages.
- Never record secrets, passwords, access/refresh tokens, private keys, connection strings, raw session identifiers, or unapproved sensitive personal/payment/health data.
- Sanitize untrusted values for control characters and output delimiters to prevent log injection.
- Avoid unbounded collections, request/response bodies, SQL text with values, file contents, or arbitrary object serialization.
- Separate operational logs from immutable audit requirements when their integrity, retention, access, or fail-closed rules differ.
- Make logging observable: dropped records, exporter failures, queue saturation, and storage pressure need bounded operational signals.

## Logging and tracing relationship

Invoke `tracing-standard` when causality, cross-service propagation, latency breakdown, asynchronous work, or sampling must be designed. For new OpenTelemetry-style events and exceptions, prefer named structured log events correlated with the current span; use span-event APIs only when required by an existing instrumentation contract or compatibility constraint.

## Expected output

For implementation or review, provide:

1. event purpose and owning boundary;
2. event name, severity, outcome, and structured field schema;
3. correlation and trace-context behavior;
4. sensitive-data and sanitization decisions;
5. expected volume, retention/access implications, and duplicate/noise controls;
6. failure behavior and verification evidence;
7. actionable findings with source locations when reviewing code.

Follow the target language's established logging library and project conventions; do not introduce a new framework without a demonstrated need.
