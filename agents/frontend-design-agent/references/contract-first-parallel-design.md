# Contract-First Parallel Frontend Design

The main coordinator owns the [mandatory API and coordination workflow](../../system-design-agent/SKILL.md#mandatory-workflow); [frontend-design-agent/SKILL.md](../SKILL.md) owns frontend branch execution.

## Stage 1: shared baseline and API draft

The main coordinator establishes known domain/data/source-of-truth ownership, business states, transaction/consistency expectations and server authorization from approved sources and backend evidence. It drafts the shared OpenAPI contract with `api-design-standard`. A complete backend SD is not a prerequisite.

## Stage 2: joint contract readiness

Backend and frontend coordinators review the same draft in `contract-review` mode. Frontend walks approved journeys, permitted actions, inputs/results and loading/empty/error/conflict/recovery states, exposing missing operations/fields, fan-out, client joins, ambiguous errors, unsafe retries and unsupported navigation/optimistic updates.

When missing interaction choices affect that review, Frontend can use a bounded `ux-baseline` Experience pass without requiring detailed architecture/components or a complete visual system. Accepted existing UX is reused; generated proposals are not approval.

The main coordinator resolves changes and records `Contract-Ready`, version/hash and review evidence. Branches neither independently edit the shared API nor move authoritative server rules into the client. Frontend-only work may reuse a confirmed unchanged contract; work without a shared API dependency records the applicable gate as `Not Applicable`.

## Stage 3: parallel detailed design

After the gate, the backend and frontend branches run in parallel. Frontend runs ordered sibling agents: conditional Experience UX baseline → Frontend Architecture → Components and State → Experience detail → Quality and Delivery. Each dedicated agent follows its own mandatory workflow and receives accepted predecessor decisions; approved experience and quality constraints are supplied before Architecture starts. The frontend coordinator resolves later findings through the original owners and returns one consolidated design. Changes go through the main coordinator and reopen only affected work. Unaffected work can continue against its valid baseline. Every returned design identifies the accepted contract version/hash.

## Handoff

The main coordinator writes accepted backend, frontend and integration content into the final SD set and records readiness in the Index. Frontend implementation begins only through SDD after applicable design readiness and separate implementation authorization.
