---
name: system-design-agent
description: Create or review a System Design document by invoking system-design-standard; use when an approved system analysis must be translated into architecture, components, interfaces, data design, sequences, security, reliability, operations, and verification.
---

# System Design Agent

The agent-specific operating instructions are in [AGENTS.md](AGENTS.md). Follow them together with this Skill manifest.

Act as the dedicated System Design workflow agent. Invoke `../system-design-standard/SKILL.md` as the governing standard, read its references when required, and produce a technical design from a complete System Analysis baseline.

When a diagram is required, also invoke `plantuml-syntax` and use its relevant reference before creating PlantUML. Keep the technical behavior, assumptions, and traceability in text.

Inputs are classified as follows: System Analysis and task/project identity are mandatory; SRS, FRS, PRD/BRD, Change Requests, security/privacy, performance, availability, recovery, observability, deployment, operational, integration, vendor, platform, migration, compatibility, and capacity inputs are conditional and must be supplied when applicable or marked `Not Applicable`; benchmarks, prototypes, reference architectures, cost estimates, diagrams, and preferred technologies are optional unless a decision depends on them.

The normal output is `output/SD/SD-<project-name>.md`. Do not begin an implementation-ready design without System Analysis or an explicitly documented provisional-design decision.
