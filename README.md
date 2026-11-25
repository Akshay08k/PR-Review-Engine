# PR Review Engine

> Working project documentation — initial discovery stage

## Purpose

This documentation captures the product direction and decisions discussed so far. It is intended to give future human contributors and AI coding agents a shared understanding of the project before implementation begins.

**Important:** This is a product-discovery baseline, not a finalized technical specification. Do not assume that open questions have been decided.

## Start here

1. Read `02_PRODUCT_DEFINITION/PROJECT_OVERVIEW.md` for the product vision and problem.
2. Read `02_PRODUCT_DEFINITION/PRODUCT_PRINCIPLES.md` for the principles that should guide decisions.
3. Read `03_ENGINE_DESIGN/CONTEXT_ENGINE.md` and `03_ENGINE_DESIGN/DECISION_ENGINE.md` for the two initial product pillars.
4. Read `04_DISCOVERY/OPEN_QUESTIONS.md` before proposing architecture or implementation.
5. Check `01_PROJECT_GOVERNANCE/PROGRESS.md` before doing project work and update it when a meaningful decision or milestone is completed.
6. Follow `01_PROJECT_GOVERNANCE/AGENT_GUIDE.md` (and `AGENTS.md`) when acting as an AI coding or research agent.

## Current scope

The project is currently exploring two core capabilities:

- **Context Engine:** discover and assemble relevant context for a Pull Request.
- **Decision Engine:** evaluate the PR using available evidence and produce an explainable assessment and recommendation.

Security, permissions, compliance architecture, detailed technology choices, and implementation framework are intentionally deferred.

## Status vocabulary

- **Discussed:** raised and explored in conversation.
- **Proposed:** a candidate direction, not yet approved as final.
- **Agreed principle:** a guiding principle accepted in discussion.
- **Open:** requires a future decision.
- **Deferred:** intentionally postponed.
- **Implemented:** built and verified in the project.

Do not change a status to `Agreed` or `Implemented` without evidence.
