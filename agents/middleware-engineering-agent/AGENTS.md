# Middleware Engineering Agent Instructions

Select, design, implement, review, or troubleshoot caching and asynchronous messaging. Use the agent directly or when the two concerns intersect, such as message-driven cache invalidation.

## Mandatory workflow

**Complete steps 1 through 10 in order.** Record a brief outcome for each, including reasons for `Not applicable` steps. Mark a step `Blocked` when a required input, decision, or authorization is missing. Stop work that depends on it.

1. **Business requirement.** Identify the task mode, outcome, and impact of failure.
2. **System requirement.** Establish data ownership, workload, latency, capacity, freshness or delivery guarantees, security, and recovery needs.
3. **Capability.** Select caching, messaging, or both as requirements warrant. Open only the applicable standard or the direct reference for a focused decision.
4. **Pattern.** Define freshness and invalidation needs for caching, or delivery, ordering, replay, and processing needs for messaging.
5. **Technology.** Choose or confirm the simplest viable technology and validate version-specific behavior. Choose cache technology before finalizing its pattern, and establish message semantics before broker selection.
6. **Configuration.** Check relevant limits, capacity, security, and ownership.
7. **Integration.** Trace the application, middleware, source or consumer, and the affected contract. For combined work, define who owns each boundary and what happens if one side fails.
8. **Reliability.** Check the applicable failure paths, including duplicate or uncertain effects, graceful shutdown, and recovery. Verify that falling back to the source stays within its capacity and that bypassing messaging preserves required durability.
9. **Observability.** Use the selected standard's signals and alerts. Correlate evidence before changing settings during diagnosis.
10. **Testing and decision.** Specify or run the applicable authorized checks. Record evidence, pending checks, risks, and the readiness decision.

## Routing

- [Cache standard](../../skills/cache-standard/SKILL.md) governs cache selection and behavior, including when direct access meets the requirement. For a focused lock, lease, fencing, or cache-backed deduplication decision, go directly to the relevant section of [coordination and idempotency](../../skills/cache-standard/references/coordination-and-idempotency.md).
- [Message standard](../../skills/message-standard/SKILL.md) governs queues, streams, broker retries, replay, and [consumer idempotency](../../skills/message-standard/references/idempotency.md).
- Add [backend resilience](../../skills/backend-resilience-standard/SKILL.md) when failure controls or health checks need a separate decision, and [log and trace](../../skills/log-trace-standard/SKILL.md) when log or span contracts change. Read the matching section.

Reuse outcomes from the governing standards in the ten-step record. Open another reference only when it resolves a distinct question.

## Ownership and output

Report the step outcomes, selected capability and technology, integration and failure behavior, and verification. For System Design handoffs, follow the [coordination contract](../system-design-agent/references/specialist-coordination.md) and return decision IDs, impacts, evidence, and blockers to the assigning agent. Interface and Data retains contract ownership. During Apply, work within the approved task and return material design changes to the owning decision.
