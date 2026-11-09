# AI-Ready PRD Template

Adapt this template to the product and release size. Keep the business and product decisions explicit; use `TBD`, `Proposed`, or `Pending Approval` rather than inventing missing information.

## Document control

Record product name, PRD version, status, author, product owner, reviewers, date, target release, and linked research or source documents.

### Product and release identity

### Review status and source evidence

## 1. Overview

State what the product or feature is, who it serves, the target release, and the one-sentence value proposition.

### Product summary

### Target release and value proposition

### Product status and assumptions

## 2. Problem Statement

Describe who has the problem, current behavior, pain or opportunity, evidence, why it matters now, and what happens if it is not addressed.

### User pain or opportunity

### Current behavior and alternatives

### Evidence and urgency

### Consequence of not solving the problem

## 3. Target Users

Define the primary and secondary personas only when supported by evidence. Include role/context, goals, behaviors, pain points, current alternatives, accessibility or regional needs, and relevant adoption constraints. Mark willingness-to-pay claims as research or assumptions.

### Primary persona

### Secondary personas

### Goals, behaviors, and pain points

### Accessibility, region, and adoption constraints

## 4. Goals and Success Metrics

List product outcomes and measurable metrics. Include baseline, target, measurement window, owner, and instrumentation status when known. Keep delivery milestones in the timeline section instead of presenting them as product success.

### Product goals

### Success metric table

### Baseline and measurement plan

### Guardrail metrics

## 5. User Stories and Journeys

Write stories in the form `As a [user], I want to [action], so that [benefit]`. Group them by journey and include entry conditions, happy path, alternate path, and critical failure path.

### Journey map

### User story register

### Happy path and alternate paths

### Acceptance criteria and edge cases

## 6. Functional Requirements

Group requirements by capability. Recommended fields: ID, user story, requirement, priority, decision status, acceptance criteria, analytics signal, dependency, and release.

### Capability overview

Record a compact source-to-operation catalogue. For each independently testable action capture source/operation IDs, actor, entry or trigger, rules and observable success/failure, acceptance IDs, and delivery/decision status. Split actions with different permissions, outcomes or phases. Link to the [functional coverage reference](functional-coverage.md); use an existing governing catalogue rather than copying it.

### Capability module template

Use the following subheadings for each major product capability:

#### `<Capability name>`

##### User goal and related story

##### Entry point and user flow

##### Functional requirements

##### State, validation, and permissions

##### Loading, empty, error, and recovery states

##### Acceptance criteria

##### Analytics and success signal

##### Priority, release, and dependencies

## 7. Non-Functional Requirements

Include applicable performance, availability, security, privacy, accessibility, compatibility, reliability, observability, and compliance expectations. Make values measurable or label them proposed.

### Performance and availability

### Security and privacy

### Accessibility and compatibility

### Reliability, observability, and compliance

## 8. Technical Considerations

Keep only approved or explicitly proposed constraints, such as required platforms, external integrations, data residency, browser support, or migration limits. Put detailed API, schema, architecture, and implementation instructions in SA/SRS unless the user explicitly requests an AI-coding implementation PRD.

### Confirmed product constraints

### Required integrations and platform boundaries

### Proposed implementation notes

### Deferred technical decisions

## 9. UI/UX Requirements

Describe key screens, navigation, interaction states, content rules, validation, loading/empty/error states, responsive behavior, accessibility, localization, and design references. Use wireframes or diagrams when available, but do not rely on visuals without describing the required behavior.

### Information architecture and navigation

### Key screens and entry points

### Interaction and content rules

### Loading, empty, error, and success states

### Responsive, accessibility, and localization requirements

## 10. Out of Scope

List explicit exclusions for this release. Include likely scope-creep requests when they would otherwise be inferred from the product idea.

### Explicit exclusions

### Deferred opportunities

### Scope-change rule

## 11. Timeline and Milestones

Show phases, sequencing, deliverables, dependencies, and target dates. Mark each date or estimate as committed, proposed, or TBC.

### Build sequence

### Milestone and deliverable table

### Release dependencies and gates

## 12. Risks and Mitigations

For each risk, record impact, likelihood when known, trigger, mitigation, contingency, owner, and dependency. Distinguish product risk from implementation risk.

### Product risks

### Delivery and implementation risks

### Mitigation and contingency plan

## 13. Open Questions and Approval

Track unresolved decisions with ID, question, options, recommendation if useful, decision owner, status, and due date when known. Add release acceptance criteria, approvers, approval status, version history, and change-control rules for material initiatives.

### Open question register

### Release acceptance criteria

### Approval and sign-off

### Version history and change control

## Traceability

For critical paths, maintain:

`Goal -> User Story -> Functional Requirement -> Acceptance Criteria -> Metric`

Add `-> UAT Scenario` when the project has a formal acceptance process.
