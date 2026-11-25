# Context Engine

## 1. Purpose

The Context Engine aims to build a relevant understanding of a Pull Request and the software system it changes.

It addresses the problem that reviewers manually gather information from multiple places before they can confidently evaluate a change.

## 2. Starting point

The PR is the natural starting point. The engine should inspect the change and use it to guide further discovery.

Potential starting information includes:

- PR title.
- PR description.
- Source and target branches.
- Changed files and diff.
- Commit messages.
- Branch name.

A title or description may be absent, vague, or inaccurate. The diff and repository must therefore remain important sources.

## 3. Candidate context sources

The following sources have been discussed. Their availability depends on repository host, project configuration, and access that may be granted in a future design.

| Source | Potential contribution | Current view |
|---|---|---|
| PR diff | Exact additions, deletions, and modifications | Foundational |
| Changed file content | Full local context around changed lines | Foundational |
| Surrounding code | Callers, callees, related classes, interfaces, models, services | Very high value |
| Related implementations | Existing patterns and comparable workflows | High value |
| Tests | Expected behavior, assertions, regression coverage | High value |
| PR title and description | Developer-stated intent and scope | Useful when present |
| Commit messages and branch name | Additional clues about intent | Supplementary |
| Git history and prior PRs | Earlier decisions, bug fixes, reversions, and evolution | High value when relevant |
| Work items / tickets | Problem statement, acceptance criteria, reproduction steps | High value when linked |
| Database schema and SQL objects | Nullability, constraints, relationships, procedures, triggers | Context-dependent |
| API contracts and consumers | Request/response expectations and breaking-change impact | Context-dependent |
| Documentation / specifications | Business rules, architecture, operating procedures | Useful when available |
| PR comments / discussion | Clarifications and reviewer/developer decisions | Supplementary |

This table is a candidate inventory, not a commitment to integrate every source in the first version.

## 4. Example of context discovery

Suppose a PR modifies `SupplierService.CreatePurchaseOrder()`.

Potential discoveries include:

1. The changed method and its diff.
2. The method's callers and dependencies.
3. Supplier validation services or similar implementations.
4. Tests covering purchase-order creation and supplier status.
5. Supplier entity definitions and relevant database constraints.
6. Recent changes to the same method or workflow.
7. A linked work item, if one exists.
8. Relevant API or UI consumers, if the change affects a contract.

The purpose is to assemble context specifically relevant to the changed behavior, not to crawl everything without a reason.

## 5. Context quality and availability

The engine should be able to work with different levels of available context:

### Rich context
PR, linked work item, acceptance criteria, tests, documentation, and repository context.

### Limited context
PR title or description, diff, changed files, and repository context.

### Minimal context
Diff and repository context, perhaps with commit messages.

The review should still proceed where possible. The output should identify limitations and avoid claiming that unavailable requirements were verified.

## 6. Context representation — open design

A future design needs to decide how discovered information is represented and stored for evaluation. Possible metadata to consider:

- Source type and source identifier.
- Repository path and line range, where applicable.
- Relationship to changed files or symbols.
- Whether the information is explicit or inferred.
- Retrieval reason.
- Freshness or commit/version association.
- Confidence or reliability.
- Whether the context supports or contradicts a finding.

These are design considerations, not a finalized schema.

## 7. Important open questions

- How does the engine identify relevant symbols and dependencies?
- How far should it follow callers and callees?
- How should it search for similar implementations?
- When is Git history worth retrieving?
- How does it avoid irrelevant or excessive context?
- How should it handle conflicting sources?
- How should context be bounded, ranked, and deduplicated?
- Which integrations are necessary for an initial prototype?

## 8. Current boundary

Security, repository permissions, data handling, tenant isolation, and compliance are important but intentionally deferred for a separate design discussion. This document does not authorize access to any repository or external system.
