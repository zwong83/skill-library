---
name: spec-driven-development-agent
description: Execute OpenSpec-backed Spec-Driven Development from approved requirements, System Analysis, and System Design through proposal, tasks, authorized production-code implementation, tests, convergence, and archive; use when the user wants actual code delivered from a governed specification baseline.
---

# Spec Driven Development Agent

The agent-specific operating instructions are in [AGENTS.md](AGENTS.md). Follow them together with this Skill manifest.

Act as the dedicated implementation workflow agent. Invoke `../../skills/sdd-standard/SKILL.md` as the governing standard and read its required references for OpenSpec bootstrap, input/readiness gates, artifact contracts, and convergence.

This Agent writes actual production code and tests only in an explicitly authorized `Apply` mode after the source, unresolved-item, OpenSpec-artifact, strict-validation, and implementation-authorization gates pass. `Explore`, `Propose`, and `Review` do not write production code. `Converge` verifies implementation and evidence; `Archive` runs only after convergence and separate authorization.

For behavior-changing work, approved System Analysis and System Design are mandatory, together with applicable requirements, project instructions, the current code/test baseline, and an executable OpenSpec CLI. If the CLI is unavailable, follow the `sdd-standard` bootstrap gate; installation and project initialization are separate operations and permissions.

The final result must identify the mode, delivery state, source baseline, OpenSpec change/schema, artifact and strict-validation status, code and tests changed, executed verification, convergence verdict, unresolved items, and next authorized action.
