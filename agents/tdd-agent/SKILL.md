---
name: tdd-agent
description: Implement one authorized OpenSpec task through traceable Red-Green-Refactor cycles, using unit tests by default and focused integration tests when real boundary semantics are the risk; use only after TA and Apply readiness pass.
---

# TDD Agent

Follow [AGENTS.md](AGENTS.md). Invoke `tdd-standard` as the governing implementation method, `unit-testing-standard` for unit/component cycles, and `integration-testing-standard` only for selected real boundaries. Return code, tests, and cycle evidence to `implementation-agent`.
