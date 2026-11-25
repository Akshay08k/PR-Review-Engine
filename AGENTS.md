# AGENTS.md — PR Review Engine

This file consolidates working context and operational rules extracted from the repository documentation so AI agents and contributors have an accurate baseline before acting.

## 1. Project Identity & Current Status

- **Project:** PR Review Engine
- **Stage:** Product discovery (`Initial product direction documented`, `Implementation status: Not started / not specified`, baseline dated `2026-11-25` per `01_PROJECT_GOVERNANCE/PROGRESS.md`).
- **Repository contents:** Product-discovery Markdown docs only—no application code, tests, build configuration, or finalized architecture exists yet.
- **Vision (`02_PRODUCT_DEFINITION/PROJECT_OVERVIEW.md`):** Help human reviewers make faster, more consistent, evidence-based PR decisions. This is **not** a thin LLM diff-comment wrapper and **not** a replacement for human accountability.
- **Current scope (`README.md`):** Two conceptual pillars—**Context Engine** and **Decision Engine**. Security, permissions, compliance architecture, tech stack, and implementation framework are intentionally **deferred**.

### Status Vocabulary (`README.md`)
Use these labels strictly and never upgrade a status to `Agreed` or `Implemented` without evidence:
- `Discussed` — raised and explored in conversation
- `Proposed` — candidate direction, not yet approved as final
- `Agreed principle` — guiding principle accepted in discussion
- `Open` — requires a future decision
- `Deferred` — intentionally postponed
- `Implemented` — built and verified in the project

---

## 2. Source-of-Truth Documentation Map

Read these in order before proposing structural changes or implementation (`README.md`, `01_PROJECT_GOVERNANCE/AGENT_GUIDE.md`):

1. `README.md` — Entry point, scope boundaries, reading order, and status vocabulary.
2. `02_PRODUCT_DEFINITION/PROJECT_OVERVIEW.md` — Vision, problem statement, 7-step proposed product workflow, intended reviewer outcomes, and non-goals.
3. `02_PRODUCT_DEFINITION/PRODUCT_PRINCIPLES.md` — The 10 agreed/established guiding principles.
4. `03_ENGINE_DESIGN/CONTEXT_ENGINE.md` — Pillar 1: context discovery starting points, 13 candidate sources, context tiers, metadata considerations, and open questions.
5. `03_ENGINE_DESIGN/DECISION_ENGINE.md` — Pillar 2: 6 candidate evaluation dimensions, evidence types, 3-tier finding classification, scoring options, and open questions.
6. `04_DISCOVERY/OPEN_QUESTIONS.md` — Unresolved product, engine, tech, and deferred security/compliance questions.
7. `01_PROJECT_GOVERNANCE/PROGRESS.md` — Status source of truth, completed docs checklist, unresolved decisions, suggested discussion order, and update log protocol.
8. `01_PROJECT_GOVERNANCE/AGENT_GUIDE.md` — Contributor and AI agent rules (uncertainty labeling, traceability, scope discipline, and implementation gates).

---

## 3. Agreed / Established Product Principles (`02_PRODUCT_DEFINITION/PRODUCT_PRINCIPLES.md`)

1. **Review with existing context:** Work effectively whether context is rich or minimal beyond the diff.
2. **Context is discovered, not only supplied:** Start from the PR and discover relevant context rather than forcing manual attachments.
3. **Missing context ≠ defect:** Unverifiable behavior (e.g., no linked business requirement) must be reported as not independently verifiable, not penalized with a defect or failing score.
4. **Separate facts, inferences, and unknowns:** Make evidence provenance explicit; never present uncertain inferences as confirmed defects.
5. **Findings require evidence:** Explain what is wrong or potentially wrong, why it matters, and cite supporting files, lines, tests, requirements, schemas, or history.
6. **Prefer deterministic evidence:** Use suitable deterministic tools for build, test execution, and static analysis rather than asking an LLM to guess results.
7. **Distinguish defects from concerns:** When expected behavior cannot be established, report a potential concern or unanswered question.
8. **Avoid indiscriminate collection:** Retrieve context relevant to the change and review question; do not ingest everything blindly.
9. **Scores must not hide blockers:** High aggregate scores must not neutralize critical defects.
10. **More than an LLM API wrapper:** Value comes from discovery, evidence gathering, evaluation orchestration, validation, explainability, and decision support.

---

## 4. Proposed Product Architecture (Not Yet Finalized)

### Proposed End-to-End Workflow (`02_PRODUCT_DEFINITION/PROJECT_OVERVIEW.md`)
1. Start from the PR and identify what changed.
2. Discover relevant context from available sources.
3. Separate explicit facts, inferred context, and unknowns.
4. Evaluate the change using deterministic checks and reasoned analysis.
5. Record findings with supporting evidence.
6. Produce an explainable assessment and recommendation.
7. Communicate review limitations when context or evidence is missing.

### Pillar 1: Context Engine (`03_ENGINE_DESIGN/CONTEXT_ENGINE.md`)
- **Starting signals:** PR title, description, source/target branches, changed files and diff, commit messages, branch name (title/description may be absent, vague, or inaccurate, so diff and repo remain essential).
- **Candidate context sources (inventory only, not a v1 commitment):**
  - *Foundational:* PR diff, changed file content.
  - *Very high / high value:* Surrounding code (callers, callees, classes, interfaces, models, services), related implementations/patterns, tests, Git history & prior PRs (when relevant), linked work items/tickets.
  - *Useful / context-dependent / supplementary:* PR title & description, documentation/specs, DB schema & SQL objects, API contracts & consumers, commit messages & branch name, PR comments/discussion.
- **Context quality tiers:** `Rich context`, `Limited context`, `Minimal context` — proceed where possible and disclose missing verification coverage.
- **Open representation considerations:** Source type/id, repo path & line range, relationship to changed symbols, explicit vs. inferred, retrieval reason, freshness/commit association, confidence/reliability, supporting vs. contradicting role.

### Pillar 2: Decision Engine (`03_ENGINE_DESIGN/DECISION_ENGINE.md`)
- **Candidate evaluation dimensions (names, overlap, weights open):**
  - `Technical Correctness` (build/compilation, types, nulls, exceptions, static analysis)
  - `Logic & Behavior` (conditions, control flow, edge cases, consistency with surrounding code)
  - `Code Quality` (maintainability, complexity, duplication, separation of responsibilities)
  - `Test Confidence` (existing/new tests, execution results, coverage gaps)
  - `Business Requirement Compliance` (alignment with requirements, acceptance criteria, specs, QA scenarios)
  - `Change Risk` (scope, affected components, dependencies, impact)
- **Proposed finding classification:**
  - `Confirmed finding` — strong, direct evidence (e.g., failing test or clear constraint violation).
  - `Potential concern` — plausible issue without conclusive proof in available context.
  - `Not verifiable / insufficient context` — expected behavior or evidence is unavailable.
- **Scoring & recommendation (`Open`):** Weighted category scores, finding/severity deductions, and a hybrid model have been discussed (hybrid noted as promising, **none finalized**). Critical blockers must remain visible independently of any aggregate score.

### Explicit Non-Goals at This Stage (`02_PRODUCT_DEFINITION/PROJECT_OVERVIEW.md`)
- Automatically fixing code or automatically approving/merging PRs.
- A finalized dashboard or analytics product.
- A finalized security/permissions architecture.
- A specific LLM provider, model, framework, language, or scoring formula/threshold system.

---

## 5. Open Questions & Deferred Areas (`04_DISCOVERY/OPEN_QUESTIONS.md`)

Do **not** treat any of the following as decided:
- **Product definition:** Exact reviewer decision, score meaning (merge safety vs. code quality vs. combined), initial supported workflows.
- **Context Engine:** MVP source set, symbol/dependency traversal depth, similarity search, Git history triggers, noise/size bounds, conflicting/stale context handling, initial integrations.
- **Decision Engine:** Final categories, score meaning, deterministic vs. AI boundary, classification/prioritization/deduplication rules, confidence/missing-context impact, blocker overrides, recommendation states/thresholds, AI finding validation.
- **Tech & architecture:** Language, framework, model/provider strategy, static-analysis tools, context indexing/retrieval representation, deployment/operating model.
- **Security & compliance (`Deferred`):** Repository access/authorization, data retention/deletion, tenant isolation, secret handling, auditability/compliance, sending code to external model providers.

---

## 6. Mandatory Rules for AI Agents & Contributors (`01_PROJECT_GOVERNANCE/AGENT_GUIDE.md`)

1. **Preserve discovery-stage status:** Do not treat proposals as approved architecture. Do **not** choose a language, framework, database, LLM provider, vector DB, hosting model, repository integration, or scoring formula unless the project owner explicitly asks.
2. **Do not silently expand scope:** Stay focused on context discovery/assembly, evidence-based evaluation, and explainable findings/scoring/recommendations. Do not imply deferred security/permissions work is solved.
3. **Make uncertainty explicit:** Label statements as `Existing discussion / agreed principle`, `Proposal`, `Assumption`, `Open question`, or `Decision required`. Never turn assumptions into facts.
4. **Traceability on proposed findings/behaviors:** Specify (a) what is observed, (b) supporting source, (c) reasonable conclusion, (d) what remains unknown, and (e) confirmed vs. potential concern.
5. **Ask before foundational choices:** When materially different product or technical directions exist, present options and trade-offs rather than picking one silently.
6. **Do not start large-scale implementation:** Clarify required behavior and obtain explicit project-owner direction first.
7. **Progress tracking (`01_PROJECT_GOVERNANCE/PROGRESS.md`):** Update `01_PROJECT_GOVERNANCE/PROGRESS.md` only when a meaningful discussion, decision, research task, or milestone completes using dated entries (`Discussed`, `Decided`, `Proposed`, `Open`, `Next`). Do not mark work complete merely because a proposal was written.

### Suggested Next Discussion Sequence (`01_PROJECT_GOVERNANCE/PROGRESS.md`, non-binding)
1. Define what the PR score is intended to communicate.
2. Finalize evaluation dimensions and missing-context representation.
3. Define finding types, severity, confidence, and evidence requirements.
4. Define the first Context Engine discovery workflow from a PR diff.
5. Identify the smallest useful prototype scope.
6. Compare technology and implementation approaches only after steps 1–5.
