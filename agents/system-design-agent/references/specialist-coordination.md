# System Design Specialist Coordination

The System Design Coordinator owns the source baseline, routing, reconciliation, authoritative document set, readiness status, and approval boundary. Specialists return compact handoffs; they do not create persistent packet documents or edit authoritative SD files unless the Coordinator explicitly assigns a bounded section.

## Minimal context envelope

Provide each specialist only what it needs:

- requested concern and target document: Backend, Frontend, Integration, or Index;
- governing requirement/SA IDs and statuses, not full source restatements;
- current accepted decision IDs and contract version relevant to that concern;
- confirmed constraints and applicable existing-system facts;
- unresolved items that may affect the work;
- expected verification evidence.

Do not send unrelated source documents, other specialists' full reasoning, or the complete SD set when a stable ID, section link, contract fragment, or short accepted-decision summary is sufficient.

## Compact handoff contract

Return only these fields:

1. **Accepted decisions** — stable ID, concise normative result, status, and target document/section.
2. **Contract changes** — affected contract/version, exact semantic change, compatibility impact, and `None` when unchanged.
3. **Dependencies and impacts** — only new or changed cross-boundary dependencies, affected decision IDs, and required follow-up.
4. **Blockers** — unresolved decision, impact, owner when known, and target document; use `None` when clear.
5. **Verification** — requirement/decision-to-evidence mapping and readiness recommendation.

Attach a focused diagram, model fragment, or material ADR only when it is itself needed in the target SD. Preserve alternatives and trade-offs only for a material decision whose rationale must survive review. Omit repeated background, generic explanation, settled facts, unchanged content, obviously rejected options, duplicated schemas, and chain-of-thought.

The handoff is transient unless an audit requires retention. The Coordinator writes accepted content once into its target document and discards redundant handoff prose.

## Conflict and decision handling

Do not silently overwrite another accepted decision. Return the conflict as a blocker with affected IDs and impact. The Coordinator records only unresolved material cross-document decisions in `open-decisions.md` and sends the smallest relevant context back to the owning specialist or source owner.

Minor editorial differences that do not change behavior, ownership, contracts, controls, targets, or verification are resolved directly by the Coordinator and do not need a register entry.

## Backend-first contract, then parallel detail

When a frontend is in scope:

1. Architecture, Interface/Data, and Quality specialists establish sufficiently stable backend domain ownership, source of truth, transactions/consistency, server authorization, state/error semantics, and a versioned draft contract.
2. `frontend-design-agent` receives only relevant journeys, support commitments, backend ownership decisions, and the draft contract. It returns contract changes or confirms `None`.
3. The Coordinator records `Contract-Ready` only when applicable operations, schemas, errors, authorization context/results, idempotency/concurrency, pagination/filter/sort, limits, cancellation/deadlines, compatibility, examples, and ownership are resolved.
4. Backend and frontend detail may then proceed in parallel. A material contract change reopens only affected decisions, tasks, mocks/fixtures, contract tests, and readiness.

Do not wait for every backend deployment detail before frontend design, and do not move authoritative domain rules or security enforcement into the client for convenience.

## Authoritative write targets

- Backend SD: backend internals, architecture, domain/data/transaction ownership, server controls, runtime quality, delivery, operations, and backend verification.
- Frontend SD: frontend rendering, routing, modules, components, state/data use, experience, client quality, delivery, and frontend verification.
- Integration SD: cross-boundary ownership and behavior, contract references, authentication/session exchange, authorization context/results, errors, idempotency/concurrency, pagination/filter/sort, deadlines/cancellation/retries, compatibility, mixed versions, examples/mocks/fixtures, and contract tests.
- SD Index: source and artifact versions, routing/status, readiness, unresolved decisions, review verdict, and approvals.
- Machine-readable contract: authoritative field/protocol structure. Do not duplicate its full schema in Markdown.

If documents disagree, the machine-readable contract owns field/protocol structure, Integration SD owns cross-boundary semantics, Backend SD owns backend internals, and Frontend SD owns frontend internals. The conflict blocks readiness until resolved.

## Review handoff

The Review Agent receives the applicable four-document SD set, machine-readable contracts, source baseline, and unresolved `open-decisions.md` entries. It does not need specialist handoffs. Its verdict and actionable findings return to the Coordinator; the final verdict is recorded in the Index, with a separate report only when audit retention is required.
