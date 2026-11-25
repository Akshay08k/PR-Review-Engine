# Guide for AI Agents and Contributors

## 1. Read before acting

Before proposing changes or implementation:

1. Read `README.md`.
2. Read `02_PRODUCT_DEFINITION/PROJECT_OVERVIEW.md`.
3. Read `02_PRODUCT_DEFINITION/PRODUCT_PRINCIPLES.md`.
4. Read the relevant engine document (`03_ENGINE_DESIGN/CONTEXT_ENGINE.md`, `03_ENGINE_DESIGN/DECISION_ENGINE.md`).
5. Read `04_DISCOVERY/OPEN_QUESTIONS.md`.
6. Read the latest `01_PROJECT_GOVERNANCE/PROGRESS.md`.

## 2. Preserve the discovery-stage status

This project is still defining its product behavior. Do not treat proposed ideas as approved architecture.

Do not choose a programming language, framework, database, LLM provider, vector database, hosting model, repository integration, or scoring formula unless the project owner explicitly asks for a recommendation or decision.

## 3. Do not silently expand scope

The current product discussion is focused on:

- Context discovery and assembly.
- Evidence-based PR evaluation.
- Explainable findings, scoring, and recommendations.

Security and permissions architecture has been deferred. Do not make it the focus of unrelated work, but do not imply that it has been solved.

## 4. Make uncertainty explicit

When documenting or proposing something, label it as one of:

- Existing discussion / agreed principle.
- Proposal.
- Assumption.
- Open question.
- Decision required.

Do not turn an assumption into a project fact.

## 5. Evidence and traceability

When proposing a finding or product behavior, explain:

- What the system observes.
- What source supports it.
- What conclusion can reasonably be drawn.
- What remains unknown.
- Whether the conclusion is confirmed or only a potential concern.

## 6. Progress tracking

Update `01_PROJECT_GOVERNANCE/PROGRESS.md` when a meaningful discussion, decision, research task, or implementation milestone is completed.

For each update:
- Record what was completed.
- Record decisions and their status.
- Record open questions.
- Record the next concrete step.
- Do not mark work complete merely because a proposal was written.

## 7. Ask before making foundational decisions

If a task requires choosing between materially different product directions or technical architectures and the choice has not been made, present the options and trade-offs rather than silently choosing one.

## 8. Implementation readiness

Do not begin large-scale implementation based only on this initial documentation. First clarify the required behavior and obtain explicit direction from the project owner.
