# Requirements and System Design Skill Library

Reusable, tool-agnostic workflows for AI agents that create and review business, product, software-requirement, functional-requirement, system-analysis, and system-design documents.

This library is not limited to Codex. Its core content is Markdown-based and can be used by any AI agent or runtime that can read `SKILL.md` and follow Markdown instructions. Codex-specific metadata is included where useful, but it is optional to other runtimes.

## What is included

### Skills

Skills provide reusable domain instructions, templates, quality gates, and references.

- `brd-standard` — Create or audit decision-ready Business Requirements Documents.
- `prd-standard` — Create or audit AI-ready Product Requirements Documents.
- `srs-standard` — Create or audit Software Requirements Specifications.
- `frs-standard` — Create or audit detailed Functional Requirements Specifications.
- `system-analysis-standard` — Analyze system boundaries, actors, logical flows, responsibilities, data behavior, integrations, risks, and design inputs.
- `system-design-standard` — Design architecture, components, interfaces, data, sequences, security, reliability, operations, deployment, and verification.
- `plantuml-syntax` — Reference PlantUML syntax and diagram types for requirements and system documentation.

### Agents

Agents are focused workflows that gather the correct inputs, invoke the corresponding Skill, enforce readiness gates, and produce a defined deliverable.

- `business-agent` — Uses `brd-standard` and produces BRDs.
- `product-agent` — Uses `prd-standard`, `srs-standard`, and `frs-standard`; enforces the BRD intake and unresolved-decision gates.
- `system-analysis-agent` — Uses `system-analysis-standard` and produces logical System Analysis documents.
- `system-design-agent` — Uses `system-design-standard` and produces technical System Design documents.

## Product lifecycle

The library supports a traceable requirements-to-design flow:

```text
Business Requirements
        ↓
Product Requirements
        ↓
Software Requirements
        ↓
Functional Requirements
        ↓
System Analysis
        ↓
System Design
```

The default outputs are separate documents because each artifact has a different audience, purpose, change cadence, and approval gate:

```text
output/BRD/BRD-<project-name>.md
output/PRD/PRD-<project-name>.md
output/SRS/SRS-<project-name>.md
output/FRS/FRS-<project-name>.md
output/SA/SA-<project-name>.md
output/SD/SD-<project-name>.md
```

Critical paths should remain traceable:

```text
BRD objective/requirement
  → PRD goal/user story
  → SRS requirement
  → FRS feature/functional requirement
  → SA logical responsibility/flow
  → SD design decision/component/interface/data model
  → Acceptance criteria / UAT / test evidence
```

## Portable structure

```text
agents/
├── business-agent/
├── product-agent/
├── system-analysis-agent/
└── system-design-agent/

skills/
├── brd-standard/
├── frs-standard/
├── plantuml-syntax/
├── prd-standard/
├── srs-standard/
├── system-analysis-standard/
└── system-design-standard/
```

Each Skill contains a required `SKILL.md` plus optional references and metadata:

```text
<skill-name>/
├── SKILL.md
├── references/
└── agents/openai.yaml
```

Each Agent contains its own `AGENTS.md` and a Skill entrypoint that points to the governing standard Skill:

```text
<agent-name>/
├── AGENTS.md
├── SKILL.md
└── agents/openai.yaml
```

## Using the library

### Any AI agent or runtime

1. Read the relevant `skills/<skill-name>/SKILL.md`.
2. Read the linked references only when the current task needs them.
3. For an Agent workflow, read `agents/<agent-name>/AGENTS.md` and then follow its required Skill.
4. Preserve `Confirmed`, `Proposed`, `Assumption`, `TBC`, `Pending Approval`, `Open`, and `Deferred` statuses.
5. Do not claim approval or implementation readiness while material decisions, dependencies, acceptance criteria, or sign-offs remain unresolved.

### Codex and other compatible runtimes

`agents/openai.yaml` provides optional UI metadata for runtimes that support it. Runtimes that do not use this metadata can ignore the file and use the Markdown instructions directly.

The core workflows do not require a specific model, framework, programming language, vendor, or deployment platform.

## Diagram policy

Use `plantuml-syntax` when a diagram materially improves understanding. System Analysis and System Design are Diagram-first for boundaries, relationships, flows, states, data ownership, and deployment; text remains authoritative for rules, constraints, exceptions, decisions, acceptance criteria, and unresolved items.

Every diagram should have a title, scope, explanation, source traceability, and required legend or assumptions.

## Design principles

- Keep business, product, functional, logical-analysis, and technical-design concerns separate.
- Make mandatory, conditional, and optional inputs explicit.
- Resolve or visibly record unresolved decisions; do not silently invent answers.
- Keep requirements and design artifacts testable and traceable.
- Prefer simple, reviewable documents over unnecessary detail or duplicated content.
