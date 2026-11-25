# Project Overview

## 1. Product vision

The PR Review Engine is intended to help human reviewers make faster, more consistent, evidence-based decisions about Pull Requests.

It is not intended to be merely an LLM prompt that receives a diff and returns review comments. The product direction is to understand a change in the context of the surrounding software system, evaluate the available evidence, identify potential defects and risks, and provide an explainable assessment.

The engine should assist reviewers. It should not present uncertain AI conclusions as facts or silently replace human accountability.

## 2. Problem statement

Reviewing a PR often requires a reviewer to perform several separate tasks:

- Understand what changed and why.
- Explore the affected code and its dependencies.
- Find related implementations and existing behavior.
- Inspect tests and determine what they cover.
- Locate work items, acceptance criteria, specifications, or other business context when available.
- Consider database and API implications.
- Identify defects, regressions, and risks.
- Decide whether the PR is ready, needs further review, or requires changes.

Relevant information is often scattered across the repository, version-control history, work-management tools, tests, schemas, and documentation. Reviewers manually connect these sources, and review quality can depend heavily on individual experience and familiarity with the system.

A further problem is inconsistent PR context. Some developers provide detailed descriptions and linked work items; others provide only a short title, commit message, or code changes. A useful review process cannot assume every PR is perfectly documented.

Technical correctness also does not guarantee business correctness. Code can compile and pass tests while still implementing the wrong business behavior.

## 3. Proposed product response

The product should:

1. Start from the PR and identify what changed.
2. Discover relevant context from available sources.
3. distinguish explicit facts, inferred context, and unknowns.
4. Evaluate the change using suitable deterministic checks and reasoned analysis.
5. Record findings with supporting evidence.
6. Produce an explainable assessment and recommendation.
7. Communicate review limitations when context or evidence is missing.

## 4. Core product pillars

### Context Engine

Discovers and assembles the relevant information needed to understand a PR in its application context.

### Decision Engine

Evaluates the PR using available context and evidence, identifies findings and risks, and produces an assessment and recommendation.

These are conceptual product components. Their technical boundaries and implementation are not yet finalized.

## 5. Intended outcome

A reviewer should be able to understand:

- What the PR changes.
- What relevant context was found.
- What was checked.
- What findings were identified and why.
- What could not be verified.
- How confident the assessment is.
- What action is recommended.

## 6. Non-goals at this stage

The following are not currently defined as part of the initial product scope:

- Automatically fixing code.
- Automatically approving or merging PRs.
- A finalized dashboard or analytics product.
- A finalized security and permissions architecture.
- A specific LLM provider, model, framework, or programming language.
- A finalized scoring formula or threshold system.
