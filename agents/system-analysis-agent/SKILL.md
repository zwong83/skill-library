---
name: system-analysis-agent
description: Create or review a visual-first System Analysis with system-level and per-feature As-Is, problem, To-Be, state, logical-data, and integration views while keeping physical implementation decisions for System Design.
---

# System Analysis Agent

## Input and output contract

This summary follows the detailed workflow and linked gates below. Record source owners, locations/versions and decision status; keep unknowns explicit.

- **Required inputs:** Mode, identity and complete accepted requirements for new analysis; complete analysis for refinement/review.
- **Conditional inputs:** Governing FRS or authorized testable equivalent for detailed features; current/change evidence and applicable quality/integration constraints.
- **Optional context:** Research, screenshots and notation preferences unless decision-critical.
- **Outputs:** Visual-first System Analysis, feature/diagram coverage, logical flows/data/states and traceable gaps.
- **Destination and consumer:** Use the workflow's existing, requested or documented default artifact/handoff location. Return results to the invoking agent or user for the identified downstream owner; this does not authorize automatic invocation or duplicate artifacts.
- **Completion:** Apply source/visual coverage gates; material unresolved logic or missing required views prevents design readiness.


The agent-specific operating instructions are in [AGENTS.md](AGENTS.md). Follow them together with this Skill manifest.

Act as the dedicated System Analysis workflow agent. Invoke `../../skills/system-analysis-standard/SKILL.md` as the governing standard, read its references when required, and produce a logical analysis rather than a low-level technical design.

Use diagrams as the primary view for the overall system and every feature. Also invoke `plantuml-syntax` and use its relevant reference before creating PlantUML. Require a feature/diagram coverage matrix, brownfield As-Is/problem views, target main flow, per-feature To-Be technical logic, and applicable logical state/data/integration views. Invoke `software-security-standard` in System Analysis mode when security is applicable. Keep only precise rules, constraints, exceptions, decisions, acceptance criteria, evidence, and traceability in concise text.

Inputs are classified as follows: a requirements baseline and task/project identity are mandatory; FRS, Change Requests, security/privacy, performance, integration, data-retention, availability, recovery, and operational constraints are conditional and must be supplied when applicable or marked `Not Applicable`; examples, screenshots, diagrams, logs, and preferred notation are optional.

The normal output is `output/SA/SA-<project-name>.md`. Do not begin substantive analysis without a requirements baseline or an explicitly documented provisional-analysis decision.
