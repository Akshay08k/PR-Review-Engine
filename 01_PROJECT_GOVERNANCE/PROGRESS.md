# Project Progress

> This file is the project status source of truth. Update it as discussions produce decisions and as work is completed.

## Current status

**Stage:** Product discovery  
**Overall state:** Initial product direction documented  
**Implementation status:** Not started / not specified  
**Last updated:** 2026-11-25

## Progress summary

| Area | Status | Notes |
|---|---|---|
| Problem identification | Discussed | PR reviews require manual context gathering and reviewer effort; review quality can vary |
| Product vision | Discussed | Evidence-based PR decision support, not merely LLM-generated comments |
| Context Engine | Initial direction documented | Candidate sources and discovery principles identified |
| Decision Engine | Initial direction documented | Candidate evaluation dimensions and evidence principles identified |
| Scoring model | Open | Weighted, defect-driven, or hybrid model not finalized |
| Context retrieval design | Open | Relevance selection, traversal, ranking, and context limits not defined |
| Technology stack | Deferred | To be decided later |
| Security and permissions | Deferred | Explicitly postponed for a separate discussion |
| Implementation framework | Deferred | To be decided later |
| Prototype | Not started | No implementation milestone recorded |

## Discussed principles

- The PR should be the starting point for context discovery.
- PR descriptions and linked work items are useful but optional.
- The engine should still review PRs with limited or minimal context.
- Missing business requirements should not automatically count as a defect or a failing score.
- The engine should distinguish confirmed findings, potential concerns, and unverifiable behavior.
- Findings should be supported by evidence.
- Deterministic checks should be used where appropriate.
- Critical findings must not be hidden by a high aggregate score.
- The product should provide value beyond a single LLM API call.

## Completed documentation

- [x] Initial project overview recorded.
- [x] Problem and proposed solution documented.
- [x] Context source inventory recorded.
- [x] Context Engine initial direction documented.
- [x] Decision Engine initial direction documented.
- [x] Product principles recorded.
- [x] Open questions and deferred decisions recorded.
- [x] Agent guidance created.

## Decisions not yet made

- Final evaluation categories and their definitions.
- Scoring formula, weights, thresholds, and recommendation states.
- Minimum viable context sources.
- Context discovery and relevance-ranking approach.
- AI versus deterministic analysis boundaries.
- Finding validation strategy.
- Technology stack and implementation framework.
- Security, permissions, and compliance design.

## Suggested next discussion sequence

These are suggested discussion steps, not commitments to implementation:

1. Define what the PR score is intended to communicate.
2. Finalize evaluation dimensions and how missing context is represented.
3. Define finding types, severity, confidence, and evidence requirements.
4. Define the first Context Engine discovery workflow from a PR diff.
5. Identify the smallest useful prototype scope.
6. Only then compare technology and implementation approaches.

## Update log

### 2026-11-25 — Initial documentation baseline

- Captured the problem statement and product vision from discussion.
- Recorded Context Engine and Decision Engine as the two initial pillars.
- Documented candidate context sources.
- Recorded principles for missing context, evidence, and uncertainty.
- Kept scoring, technology, framework, and security decisions open or deferred.

## How to update this file

For each meaningful project session, add a dated entry containing:

- **Discussed:** what topic was explored.
- **Decided:** only explicit decisions; otherwise write `None`.
- **Proposed:** useful ideas not yet accepted.
- **Open:** questions still unresolved.
- **Next:** one concrete next step.

Change the status table only when the status genuinely changes. Do not mark a topic complete simply because it has been discussed.
