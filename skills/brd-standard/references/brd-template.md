# Structured BRD Template

Use this as a baseline, adapting or omitting modules that do not apply. A BRD may contain more or fewer sections when the domain requires it, but the business intent and approval trail must remain clear.

## Document control

Capture project name, document version, status, date, business owner, intended reviewers, target market, delivery approach, and the distinction between confirmed facts and proposals.

### Confirmed facts and document status

Record which statements are confirmed, proposed, assumed, or pending approval. Include the current review stage and the next approval action.

## 1. Executive Summary

Summarize the business context, problem/opportunity, proposed business outcome, primary users, and product or process boundaries.

### Business context

### Problem or opportunity

### Proposed business outcome

### Summary of scope and release

## 2. Business Objectives and Success Metrics

State objectives as outcomes. Add measurable targets only when a baseline or owner can support them. Separate business KPIs from delivery milestones.

### Business objectives

### KPI and target table

### Baseline, measurement method, and owner

## 3. Stakeholders and User Roles

List business owners, decision-makers, operators, affected staff, customers, partners, and their responsibilities. Do not infer approval authority.

### Stakeholder register

### Responsibilities and decision rights

### Communication and approval needs

## 4. Project Scope

Separate MVP/in-scope work from explicit exclusions, later phases, and out-of-scope ideas. Identify assumptions that would change the boundary.

### In scope

### Out of scope

### Release boundaries

### Scope assumptions

## 5. Functional Business Requirements

Group requirements by business capability. Recommended fields: ID, requirement, priority, decision status, acceptance criteria, dependency, and release.

### Capability overview

### Capability module template

Use the following subheadings for each major business capability:

#### `<Capability name>`

##### Business objective

##### Actors and responsibilities

##### Business workflow

##### Requirements

##### Business rules

##### Exceptions and failure scenarios

##### Acceptance criteria

##### Dependencies and release

##### Open decisions

## 6. Domain Rules and Capacity/Availability

For booking, pre-order, inventory, production, scheduling, eligibility, or quota-based products, state lead times, cut-offs, capacity units, blackout dates, concurrency expectations, expiry, and release rules.

### Eligibility and timing rules

### Capacity model and reservation rules

### Blackout dates, cut-offs, and exceptions

### Concurrency and release behavior

## 7. Delivery, Fulfilment, or Service Operations

Describe service areas, time slots, fees, handoffs, failure scenarios, exceptions, and who can change status. Separate confirmed policy from proposed policy.

### Service model and coverage

### Scheduling and fee rules

### Operational handoffs and status changes

### Failure, exception, and recovery handling

## 8. Cart, Intake, or Checkout

Describe what the customer or operator must provide, validation before submission, price/quantity confirmation, duplicate-submission behavior, and the record created on success.

### Entry conditions and required information

### Validation and recalculation

### Submission and idempotency rules

### Success, failure, and user notification

## 9. Case, Order, or Workflow Management

Define lifecycle states, allowed transitions, exception states, cancellation, rejection, refund or reversal handling, history, and access rules.

### Lifecycle and state definitions

### Allowed transitions

### Cancellation, rejection, and reversal

### History, audit, and access control

## 10. Payment or Commercial Handling

Document supported payment models, payment and refund statuses, reconciliation expectations, duplicate payment handling, and sensitive-data boundaries. Do not declare a provider approved without confirmation.

### Payment policy and supported methods

### Payment and refund lifecycle

### Reconciliation and duplicate handling

### Sensitive-data and compliance boundaries

## 11. Administration and Operations Portal

Define administrator functions, role boundaries, configuration ownership, auditability, operational views, and reporting responsibilities.

### Administrative capabilities

### Roles and permissions

### Configuration ownership

### Audit and operational views

## 12. Notifications and Communications

For each trigger, identify recipient, channel, required content, retry/failure behavior, and whether notification failure affects the business transaction.

### Notification trigger matrix

### Channel and consent rules

### Delivery failure and retry behavior

## 13. Reporting and Analytics

Define report questions, metrics, time windows, filters, data freshness, and metric definitions. Distinguish orders, paid amounts, refunds, and net results.

### Business questions and reports

### Metric definitions and calculation rules

### Filters, time windows, and freshness

### Data quality and reconciliation

## 14. Non-Functional Requirements

Cover availability, performance, security, privacy, data isolation, reliability, maintainability, observability, backup/recovery, usability, accessibility, and compliance. Make targets measurable or label them proposed.

### Performance and availability

### Security, privacy, and data isolation

### Reliability, recovery, and observability

### Usability, accessibility, and compliance

## 15. Business Rules Register

Give important cross-module rules stable IDs. Rules should be concise, deterministic, and traceable to one or more requirements and UAT scenarios.

### Rule definition table

### Rule exceptions and precedence

### Requirement and UAT traceability

## 16. Data Requirements

Describe business entities, required fields or snapshots, retention needs, access boundaries, audit history, and data ownership. Keep physical schema design in a technical artifact.

### Business entities and purpose

### Historical snapshots and audit records

### Access, retention, deletion, and ownership

## 17. Interface and Integration Requirements

Add this section when external services or internal systems matter. Describe the business purpose, data exchanged, timing, failure behavior, ownership, and approval status. Leave endpoint and protocol details to SA/SRS.

### Integration inventory

### Business data exchanged

### Timing, failure, and fallback behavior

### Ownership and approval status

## 18. Assumptions and Constraints

List confirmed constraints separately from assumptions: operating geography, currency, staffing, legal/compliance review, vendor limitations, launch conditions, and resource limits.

### Assumptions

### Business and operational constraints

### Legal, compliance, and vendor constraints

## 19. Risks and Dependencies

For each item, capture impact, likelihood when known, mitigation, trigger, owner, and external dependency. Do not turn a risk into a requirement without a decision.

### Risk register

### Dependency register

### Mitigation ownership and escalation

## 20. Release Plan, UAT, and Release Gate

Show phases or milestones only as planning information unless committed. Define UAT scenarios, expected outcomes, P0/Must gates, operational readiness, and who accepts the result.

### Release phases and deliverables

### UAT scenarios and expected outcomes

### Operational readiness checklist

### Release acceptance gate

## 21. Open Business Decisions and Approval/Change Control

Track each decision with an ID, question, options, recommendation if useful, decision owner, due date if known, and status. End with approval areas, approvers, status, version history, and how approved changes are assessed.

### Open decision register

### Merchant or business-owner sign-off

### Version history and change-control rules

## Suggested traceability

Use a compact mapping when the document is complex:

`Objective -> Requirement -> Business Rule -> UAT -> Approval`

Do not create traceability rows merely for appearance; include them when they reveal coverage gaps or conflicting decisions.
