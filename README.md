# Requirements, System Design, and SDD Skill Library

Reusable workflows for AI agents that create and review business, product, software-requirement, functional-requirement, system-analysis, and system-design documents, then drive approved changes through OpenSpec-backed Spec-Driven Development.

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
- `clean-code-standard` — Write, refactor, and review maintainable code using language-neutral naming, function, control-flow, failure, nullability, side-effect, and verification guidance.
- `design-patterns` — Select and explain language-appropriate design patterns without forcing Java/Spring or any other ecosystem’s implementation style.
- `object-oriented-design` — Model responsibilities, identity, values, invariants, relationships, ownership, lifecycle, and object collaboration using language-appropriate abstractions.
- `solid-principles` — Review object-oriented and modular design quality using language-neutral SOLID reasoning without forcing extra abstractions.
- `layered-architecture-standard` — Design and review language-neutral layers, modules, dependency direction, ports/adapters, transaction ownership, and test seams.
- `api-design-standard` — Design stable HTTP, gRPC, GraphQL, and internal service contracts, compatibility, limits, security boundaries, and evolution.
- `database-persistence-standard` — Design durable-data ownership, stores, schemas, access paths, transactions, migrations, retention, backup, and restore.
- `resilience-standard` — Design bounded deadlines, retries, isolation, overload protection, degradation, health, reconciliation, and recovery.
- `configuration-management-standard` — Design configuration schemas, sources, precedence, validation, refresh, secrets boundaries, drift, and change lifecycle.
- `performance-capacity-standard` — Design measurable performance objectives, workload models, capacity, headroom, scaling, and regression evidence.
- `deployment-release-standard` — Design immutable artifacts, promotion, rollout, feature release, migration sequencing, recovery, and release evidence.
- `operability-standard` — Design service ownership, SLIs/SLOs, telemetry, alerts, diagnostics, runbooks, incidents, maintenance, and readiness.
- `testing-strategy-standard` — Design risk-based test portfolios, environments, data, automation, non-functional tests, gates, and evidence.
- `software-security-standard` — Identify, design, implement, and verify risk-based software security controls across SA, SD, SDD, code, and operations.
- `error-handling-standard` — Design and review error taxonomy, throw/return/catch boundaries, translation, retries, recovery, and safe public mappings.
- `caching-standard` — Design and review cache necessity, source of truth, keys, TTL, consistency, invalidation, resilience, Redis integration, and cache operations.
- `messaging-standard` — Design and review message contracts, delivery, idempotency, ordering, retry, dead letters, replay, and RabbitMQ/RocketMQ/Kafka behavior.
- `logging-standard` — Design and review structured, correlated, secure, and operationally useful application logging.
- `tracing-standard` — Design and review distributed tracing, context propagation, span boundaries, sampling, correlation, and trace quality.
- `code-comments` — Write and review maintainable comments and docstrings that explain intent, contracts, invariants, risks, and non-obvious constraints.
- `sdd-standard` — Turn an approved requirements, SA, and SD baseline into an OpenSpec change, implementation tasks, verification evidence, convergence, and archive.

### Agents

Agents are focused workflows that gather the correct inputs, invoke the corresponding Skill, enforce readiness gates, and produce a defined deliverable.

- `business-agent` — Uses `brd-standard` and produces BRDs.
- `product-agent` — Uses `prd-standard`, `srs-standard`, and `frs-standard`; enforces the BRD intake and unresolved-decision gates.
- `system-analysis-agent` — Uses `system-analysis-standard` and produces logical System Analysis documents.
- `system-design-agent` — Uses `system-design-standard` and produces technical System Design documents.
- `spec-driven-development-agent` — Uses `sdd-standard` to create OpenSpec artifacts, implement approved production code and tests, verify convergence, and archive completed changes.

## Product lifecycle

The library supports a traceable requirements-to-delivery flow:

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
        ↓
Spec-Driven Development / OpenSpec
        ↓
Implementation and Convergence
```

The default outputs are separate documents because each artifact has a different audience, purpose, change cadence, and approval gate:

```text
output/BRD/BRD-<project-name>.md
output/PRD/PRD-<project-name>.md
output/SRS/SRS-<project-name>.md
output/FRS/FRS-<project-name>.md
output/SA/SA-<project-name>.md
output/SD/SD-<project-name>.md

openspec/changes/<change-name>/
├── proposal.md
├── specs/<capability>/spec.md
├── design.md
├── tasks.md
└── verification.md    # optional sdd-standard extension
```

Critical paths should remain traceable:

```text
BRD objective/requirement
  → PRD goal/user story
  → SRS requirement
  → FRS feature/functional requirement
  → SA logical responsibility/flow
  → SD design decision/component/interface/data model
  → OpenSpec proposal/capability requirement/design delta/task
  → Code change / acceptance criteria / test evidence / convergence
```

## Portable structure

```text
agents/
├── business-agent/
├── product-agent/
├── system-analysis-agent/
├── system-design-agent/
└── spec-driven-development-agent/

skills/
├── api-design-standard/
├── brd-standard/
├── caching-standard/
├── clean-code-standard/
├── code-comments/
├── configuration-management-standard/
├── design-patterns/
├── database-persistence-standard/
├── deployment-release-standard/
├── error-handling-standard/
├── frs-standard/
├── layered-architecture-standard/
├── logging-standard/
├── messaging-standard/
├── object-oriented-design/
├── operability-standard/
├── performance-capacity-standard/
├── plantuml-syntax/
├── prd-standard/
├── resilience-standard/
├── sdd-standard/
├── software-security-standard/
├── solid-principles/
├── srs-standard/
├── system-analysis-standard/
├── system-design-standard/
├── testing-strategy-standard/
└── tracing-standard/
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

`sdd-standard` uses the OpenSpec CLI and the active project schema as the authority for change artifacts, templates, paths, status, and archive behavior. Its readiness and convergence gates add lifecycle controls around OpenSpec without replacing upstream BRD, PRD, SRS/FRS, SA, or SD sources.

## Diagram policy

Use `plantuml-syntax` when a diagram materially improves understanding. System Analysis and System Design are Diagram-first for boundaries, relationships, flows, states, data ownership, and deployment; text remains authoritative for rules, constraints, exceptions, decisions, acceptance criteria, and unresolved items.

Every diagram should have a title, scope, explanation, source traceability, and required legend or assumptions.

## Design principles

- Keep business, product, functional, logical-analysis, and technical-design concerns separate.
- Make mandatory, conditional, and optional inputs explicit.
- Resolve or visibly record unresolved decisions; do not silently invent answers.
- Keep requirements and design artifacts testable and traceable.
- Apply object-oriented design, SOLID, and design patterns conditionally according to the selected language, paradigm, problem, and lifecycle stage.
- Use `clean-code-standard` as the implementation/refactoring review entrypoint; keep naming and function/control-flow guidance in it while routing structural concerns to the specialized Skills.
- Make layer/dependency, error, caching, and messaging behavior explicit at SD level and concrete/testable at SDD level; do not introduce infrastructure without a requirement.
- Treat software security as a lifecycle concern: identify assets, threats, trust boundaries, and security requirements in SA; design owned controls in SD; make them concrete and verifiable in SDD and implementation.
- Treat logging and tracing as intentional observability contracts, and comments as maintained explanations of non-obvious intent—not as automatic code volume.
- Prefer simple, reviewable documents over unnecessary detail or duplicated content.
