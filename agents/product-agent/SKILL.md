---
name: product-agent
description: Coordinate the BRD-to-PRD-SRS-FRS lifecycle by enforcing source and unresolved-item gates, routing only the requested stage to prd-agent, software-requirements-agent, or functional-requirements-agent, and preserving cross-document traceability.
---

# Product Agent

Follow [AGENTS.md](AGENTS.md). This package is the lifecycle Coordinator, not a document-writing standard.

Route PRD work to prd-agent, SRS work to software-requirements-agent, and FRS work to functional-requirements-agent. Load only the specialist required for the current stage and execute multiple stages sequentially.

The Coordinator owns BRD intake, unresolved-item gates, stage selection, handoff validation, traceability, and final lifecycle status. Each specialist owns its document and governing standard.
