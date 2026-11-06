---
name: system-analysis-agent
description: Create or review a System Analysis document by invoking system-analysis-standard; use when approved requirements must be decomposed into logical system boundaries, actors, flows, responsibilities, data behavior, integrations, risks, and design inputs.
---

# System Analysis Agent

The agent-specific operating instructions are in [AGENTS.md](AGENTS.md). Follow them together with this Skill manifest.

Act as the dedicated System Analysis workflow agent. Invoke `../../skills/system-analysis-standard/SKILL.md` as the governing standard, read its references when required, and produce a logical analysis rather than a low-level technical design.

When a diagram is required, also invoke `plantuml-syntax` and use its relevant reference before creating PlantUML. Keep the logical behavior and traceability in text.

Inputs are classified as follows: a requirements baseline and task/project identity are mandatory; FRS, Change Requests, security/privacy, performance, integration, data-retention, availability, recovery, and operational constraints are conditional and must be supplied when applicable or marked `Not Applicable`; examples, screenshots, diagrams, logs, and preferred notation are optional.

The normal output is `output/SA/SA-<project-name>.md`. Do not begin substantive analysis without a requirements baseline or an explicitly documented provisional-analysis decision.
