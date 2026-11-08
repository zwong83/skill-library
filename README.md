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
- `frontend-architecture-standard` — Design frontend rendering, routing, module, server/client, dependency, composition, and failure boundaries.
- `frontend-component-design-standard` — Design component responsibilities, APIs, composition, UI states, forms, and design-system integration.
- `frontend-state-data-standard` — Design frontend state ownership, API data flow, cache, optimistic updates, URL/form/session/storage, and recovery.
- `frontend-experience-standard` — Define responsive, accessible, localized, themed, motion-aware, browser/device UI behavior.
- `frontend-performance-standard` — Define route, asset, rendering, interaction, memory, RUM, and regression budgets.
- `frontend-security-standard` — Design browser/client controls for content, sessions, storage, origins, policies, dependencies, and sensitive data.
- `frontend-observability-standard` — Define client errors, RUM, journey events, correlation, release/source-map, privacy, dashboards, and alerts.
- `frontend-build-delivery-standard` — Define reproducible frontend builds, artifacts, public configuration, caching, promotion, rollout, and rollback.
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
- `test-analysis-standard` — Derive the complete change-specific Test Case Matrix, specialist allocation, prerequisites, evidence, and pre-Apply TA gate.
- `unit-testing-standard` — Design and implement deterministic behavior-focused unit and component tests.
- `integration-testing-standard` — Verify real databases, brokers, caches, services, frameworks, and other integration boundaries.
- `contract-testing-standard` — Verify provider/consumer API, event, message, schema, version, and semantic compatibility.
- `ui-testing-standard` — Verify UI rendering, interaction, visual behavior, accessibility, compatibility, and critical journeys.
- `system-e2e-testing-standard` — Verify critical multi-component journeys in a representative deployed environment.
- `security-testing-standard` — Verify approved security controls within explicit target authorization and safety limits.
- `regression-testing-standard` — Select and verify risk-based regression coverage across test levels from actual change impact.
- `tdd-standard` — Implement approved behavior through traceable Red-Green-Refactor cycles.
- `software-security-standard` — Identify, design, implement, and verify risk-based software security controls across SA, SD, SDD, code, and operations.
- `error-handling-standard` — Design and review error taxonomy, throw/return/catch boundaries, translation, retries, recovery, and safe public mappings.
- `caching-standard` — Design and review cache necessity, source of truth, keys, TTL, consistency, invalidation, resilience, Redis integration, and cache operations.
- `messaging-standard` — Design and review message contracts, delivery, idempotency, ordering, retry, dead letters, replay, and RabbitMQ/RocketMQ/Kafka behavior.
- `logging-standard` — Design and review structured, correlated, secure, and operationally useful application logging.
- `tracing-standard` — Design and review distributed tracing, context propagation, span boundaries, sampling, correlation, and trace quality.
- `code-comments` — Write and review maintainable comments and docstrings that explain intent, contracts, invariants, risks, and non-obvious constraints.
- `sdd-standard` — Turn an approved requirements, SA, and SD baseline into an OpenSpec change, implementation tasks, verification evidence, convergence, and archive.

### Agents

Agents are focused workflows. Coordinators own lifecycle gates, routing, handoffs, conflicts, and final status; specialists load only the standards needed for one stage or design concern.

- `business-agent` — Produces BRDs with `brd-standard`.
- `product-agent` — Coordinates BRD intake and PRD/SRS/FRS stage routing.
  - `prd-agent` — Produces PRDs with `prd-standard`.
  - `software-requirements-agent` — Produces SRS documents with `srs-standard`.
  - `functional-requirements-agent` — Produces FRS documents with `frs-standard`.
- `system-analysis-agent` — Produces logical System Analysis documents with `system-analysis-standard`.
- `system-design-agent` — Coordinates compact specialist handoffs and owns the authoritative SD document set and readiness index.
  - `architecture-agent` — Architecture, modules, layers, dependencies, composition, and topology.
  - `interface-data-agent` — APIs, persistence, transactions, caching, messaging, consistency, and errors.
  - `frontend-design-agent` — Reviews the shared contract and returns only accepted frontend decisions, contract changes, impacts, blockers, and verification.
  - `quality-attributes-agent` — Security, resilience, performance, capacity, scalability, and recovery.
  - `delivery-operations-agent` — Configuration, deployment/release, observability, operability, and support.
  - `system-design-review-agent` — Independent SD quality, traceability, testability, and readiness review.
- `spec-driven-development-agent` — Coordinates OpenSpec modes and authorization boundaries.
  - `openspec-planning-agent` — Explore, Propose, and Review without production code.
  - `test-analysis-agent` — Owns the pre-Apply Test Case Matrix, readiness gate, and specialist allocation.
    - `unit-testing-agent` — Implements and verifies assigned unit/component cases outside end-to-end TDD tasks.
    - `integration-testing-agent` — Implements and verifies assigned real-boundary cases.
    - `contract-testing-agent` — Verifies provider/consumer contract and compatibility cases.
    - `ui-testing-agent` — Verifies UI behavior, visuals, accessibility, compatibility, and journeys.
    - `system-e2e-testing-agent` — Verifies critical multi-component deployed-system journeys.
    - `performance-testing-agent` — Runs governed benchmark/load/stress/spike/soak/capacity testing.
    - `security-testing-agent` — Runs authorized, non-destructive verification of approved controls.
    - `regression-testing-agent` — Selects and verifies cross-level regression coverage and verdicts.
  - `implementation-agent` — Applies authorized, apply-ready tasks with tests and evidence.
    - `frontend-implementation-agent` — Implements bounded approved frontend tasks from task-relevant Frontend/Integration SD decisions and the Contract-Ready interface.
  - `tdd-agent` — Implements TDD-routed tasks through Red-Green-Refactor.
  - `convergence-review-agent` — Independently verifies code/artifact/evidence convergence.

Agent-capable runtimes may execute independent specialists concurrently from the same validated baseline. Runtimes without sub-Agent support can execute the same routing sequentially; the Coordinator and handoff contracts remain authoritative in either case.

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
System Design: Backend ownership baseline
        ↓
Joint frontend/backend Contract-Ready gate
        ↓
Backend and frontend detailed design in parallel
        ↓
Spec-Driven Development / OpenSpec
        ↓
Test Analysis (TA)
        ↓
TDD / Implementation + Test Specialists
        ↓
Unit / Integration / Contract / UI / System E2E / Performance / Security Evidence
        ↓
Regression Verification
        ↓
Convergence
```

The default outputs are separate documents because each artifact has a different audience, purpose, change cadence, and approval gate:

```text
output/BRD/BRD-<project-name>.md
output/PRD/PRD-<project-name>.md
output/SRS/SRS-<project-name>.md
output/FRS/FRS-<project-name>.md
output/SA/SA-<project-name>.md
output/SD/SD-<project-name>-index.md
output/SD/SD-<project-name>-backend.md       # when backend scope exists
output/SD/SD-<project-name>-frontend.md      # when frontend scope exists
output/SD/SD-<project-name>-integration.md   # when a cross-boundary contract exists
output/SD/contracts/                          # only applicable machine-readable contracts

openspec/changes/<change-name>/
├── proposal.md
├── specs/<capability>/spec.md
├── design.md
├── tasks.md
├── test-analysis.md   # optional supplemental TA extension
├── contract-test-report.md # when compatibility evidence is required
├── ui-test-report.md  # when UI evidence is required
├── system-e2e-test-report.md # when system journey evidence is required
├── performance-test-report.md # when performance evidence is required
├── security-test-report.md # when security evidence is required
├── regression-test-report.md  # when regression evidence is required
└── verification.md    # optional supplemental evidence extension
```

Critical paths should remain traceable:

```text
BRD objective/requirement
  → PRD goal/user story
  → SRS requirement
  → FRS feature/functional requirement
  → SA logical responsibility/flow
  → SD Index / Backend SD / Frontend SD / Integration SD / Contract-Ready interface
  → OpenSpec proposal/capability requirement/design delta/task
  → TA risk / complete case matrix / specialist allocation
  → TDD cycle / code change / unit, integration, contract, UI, system-E2E, performance, and security evidence
  → regression scope / execution / verdict
  → convergence
```

## Portable structure

```text
agents/
├── architecture-agent/
├── business-agent/
├── convergence-review-agent/
├── contract-testing-agent/
├── delivery-operations-agent/
├── functional-requirements-agent/
├── frontend-design-agent/
├── frontend-implementation-agent/
├── implementation-agent/
├── integration-testing-agent/
├── interface-data-agent/
├── openspec-planning-agent/
├── performance-testing-agent/
├── prd-agent/
├── product-agent/
├── quality-attributes-agent/
├── regression-testing-agent/
├── security-testing-agent/
├── software-requirements-agent/
├── system-analysis-agent/
├── system-design-agent/
├── system-design-review-agent/
├── system-e2e-testing-agent/
├── spec-driven-development-agent/
├── tdd-agent/
├── test-analysis-agent/
├── ui-testing-agent/
└── unit-testing-agent/

skills/
├── api-design-standard/
├── brd-standard/
├── caching-standard/
├── clean-code-standard/
├── code-comments/
├── configuration-management-standard/
├── contract-testing-standard/
├── design-patterns/
├── database-persistence-standard/
├── deployment-release-standard/
├── error-handling-standard/
├── frontend-architecture-standard/
├── frontend-build-delivery-standard/
├── frontend-component-design-standard/
├── frontend-experience-standard/
├── frontend-observability-standard/
├── frontend-performance-standard/
├── frontend-security-standard/
├── frontend-state-data-standard/
├── frs-standard/
├── integration-testing-standard/
├── layered-architecture-standard/
├── logging-standard/
├── messaging-standard/
├── object-oriented-design/
├── operability-standard/
├── performance-capacity-standard/
├── plantuml-syntax/
├── prd-standard/
├── regression-testing-standard/
├── resilience-standard/
├── sdd-standard/
├── security-testing-standard/
├── software-security-standard/
├── solid-principles/
├── srs-standard/
├── system-analysis-standard/
├── system-design-standard/
├── system-e2e-testing-standard/
├── tdd-standard/
├── test-analysis-standard/
├── testing-strategy-standard/
├── unit-testing-standard/
├── ui-testing-standard/
└── tracing-standard/
```

Each Skill contains a required `SKILL.md` plus optional references and metadata:

```text
<skill-name>/
├── SKILL.md
├── references/
└── agents/openai.yaml
```

Each Agent contains an authoritative `AGENTS.md` and a compact Skill entrypoint for discovery:

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
- For frontend scope, establish backend domain/data/transaction/security authority first, jointly reach a versioned `Contract-Ready` interface, then allow backend and frontend detailed design and implementation tasks to proceed in parallel through the shared SD/SDD lifecycle.
- Keep authoritative business rules and authorization on the server; frontend architecture, components, state/data, experience, performance, security, observability, and delivery map approved outcomes without creating a competing source of truth.
- Treat software security as a lifecycle concern: identify assets, threats, trust boundaries, and security requirements in SA; design owned controls in SD; make them concrete and verifiable in SDD and implementation.
- Treat logging and tracing as intentional observability contracts, and comments as maintained explanations of non-obvious intent—not as automatic code volume.
- Prefer small authoritative documents over unnecessary detail or duplicated content. Machine-readable contracts own field/protocol structure; Integration SD owns cross-boundary semantics; Backend and Frontend SD own their respective internals; the Index owns status and readiness.
- Use transient compact coordinator-to-specialist handoffs containing only accepted decisions, contract changes, dependencies/impacts, blockers, and verification. Do not persist full specialist packets, repeated source summaries, internal reasoning, or rejected-option histories by default.
- Keep at most one temporary SD coordination file, `open-decisions.md`, for unresolved material cross-document decisions; record the final review verdict and routing/status table in the Index.
