# Runtime Logging and Tracing

Start with the relevant contract in [the skill](../SKILL.md). Inspect the affected runtime, framework, collector, telemetry libraries, and configuration. Select the one implementation reference that addresses the issue first. Add a language example only if native APIs or framework configuration affect the change.

| Task | References |
|---|---|
| Decide what an application should log | [Logging fundamentals](logging-fundamentals.md) |
| Decide whether a signal should be a log, metric, or trace | [Observability boundaries](observability.md) |
| Write a readable message or follow an existing prefix convention | [Message style](log-writing-style.md) |
| Map application behavior to a log level | [Log levels](log-levels.md) |
| Emit structured fields through the runtime logger | [Structured logging](structured-logging.md) |
| Bind trace, span, request, or correlation IDs to a log | [Trace context](trace-context.md) |
| Correlate log events across services or workers | [Distributed logging](distributed-logging.md) |
| Instrument HTTP request or response logging | [HTTP logging](http-logging.md) |
| Instrument queue publishing, consumption, or redelivery | [Messaging logs](mq-logging.md) |
| Preserve exception detail at the owning boundary | [Exception logging](exception-logging.md) |
| Redact values or check logging of sensitive data | [Sensitive data](security-and-sensitive-data.md) |
| Change environment-specific levels, sinks, or collector settings | [Production configuration](production-configuration.md) |
| Set up file handling, rotation, or retention | [Files and rotation](log-files-and-rotation.md) |
| Diagnose logging overhead or dropped records | [Logging performance](performance.md) |

For framework APIs, choose the example for the project's language only. [Java](languages/java.md), [C#](languages/csharp.md), [C++](languages/cpp.md), [Go](languages/golang.md), [Node.js](languages/nodejs.md), [Python](languages/python.md), [Rust](languages/rust.md).

For an artifact requested by the task, use the [logging requirements template](../templates/logging-requirements.md) for a specification or the [structured event schema](../templates/structured-log-schema.json) for a machine-readable schema. For a review, choose the [logging code checklist](../checklists/logging-code-review.md), [production readiness checklist](../checklists/production-readiness.md), or [security checklist](../checklists/security-review.md) according to its scope.
