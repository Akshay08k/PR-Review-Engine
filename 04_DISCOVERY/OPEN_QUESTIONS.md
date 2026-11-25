# Open Questions and Deferred Decisions

This file prevents unresolved topics from being mistaken for decisions.

## Product definition

- What precise decision should the PR Review Engine help a reviewer make?
- Should the primary output be merge safety, overall review quality, or separate assessments?
- Which users and repository workflows should the first version support?

## Context Engine

- What is the minimum viable set of context sources?
- How should relevant code be discovered from a diff?
- How should callers, callees, related implementations, and tests be selected?
- How should retrieval depth and context size be controlled?
- How should conflicting or stale context be handled?
- Should Git history be searched by default or only when signals justify it?
- Which work-management and documentation integrations matter first?

## Decision Engine

- What are the final evaluation categories?
- What does the score represent?
- Which evidence is deterministic and which requires AI reasoning?
- How are findings classified and prioritized?
- How should confidence and missing context affect the result?
- What should happen when a critical finding exists despite a high score?
- What recommendation states and thresholds should exist?

## Technology and architecture

- What language and framework should be used?
- What model/provider strategy is appropriate?
- What analysis tools should be integrated?
- How should context be represented, indexed, and retrieved?
- What validation strategy should be used for AI findings?
- What is the initial deployment and operating model?

## Security and compliance — deferred

- Repository access and authorization.
- Data retention and deletion.
- Tenant isolation.
- Secret handling.
- Auditability and compliance requirements.
- Whether and how source code may be sent to external model providers.

These topics are deliberately deferred, not resolved.
