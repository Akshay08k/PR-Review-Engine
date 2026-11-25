# Decision Engine

## 1. Purpose

The Decision Engine evaluates a PR using the change and the context gathered for it. It should help a reviewer understand correctness, quality, test confidence, and risk, then provide an explainable recommendation.

The exact scoring model is not yet decided.

## 2. Candidate evaluation dimensions

These dimensions were discussed as possible categories:

| Dimension | What it may evaluate |
|---|---|
| Technical Correctness | Build/compilation results, type issues, null handling, exceptions, static-analysis findings, technical correctness |
| Logic & Behavior | Incorrect conditions, control flow, edge cases, unintended behavior, consistency with surrounding code |
| Code Quality | Maintainability, complexity, duplication, architecture and separation of responsibilities |
| Test Confidence | Existing and new tests, relevant scenarios, execution results, gaps in coverage |
| Business Requirement Compliance | Whether implementation matches available requirements, acceptance criteria, specifications, or QA scenarios |
| Change Risk | Scope, affected components, dependencies, and potential impact of the change |

These are proposed dimensions only. Names, boundaries, overlap, weights, and calculation rules remain open.

## 3. Available evidence

Potential evidence includes:

- Compiler and build output.
- Test execution results.
- Static-analysis output.
- PR diff and source code.
- Repository patterns and related implementations.
- Database and API contracts.
- Linked requirements and work items.
- Documentation and QA scenarios.
- Git history.

Use deterministic tools for checks that can be reliably verified by tools. AI reasoning may help interpret code and context, but its conclusions should be traceable and treated according to their certainty.

## 4. Finding classification

The system should distinguish at least these conceptual cases:

### Confirmed finding
A problem supported by strong, direct evidence, such as a failing test or a demonstrable violation of a known constraint.

### Potential concern
A plausible issue where the available context does not establish that the behavior is definitely wrong.

### Not verifiable / insufficient context
The engine cannot determine the expected behavior or lacks the evidence needed to assess a criterion.

This classification is a proposed direction and needs a formal taxonomy later.

## 5. Example

Available code:

```csharp
if (supplier != null)
{
    CreatePurchaseOrder(supplier);
}
```

Available business requirement:

> Inactive suppliers must not be used to create purchase orders.

A review can identify that the code checks whether the supplier exists but does not check whether it is active. The finding can cite the requirement and changed code.

If the requirement is absent, the engine should not automatically declare a business defect. It may inspect surrounding code, tests, entities, and existing validation patterns. If those do not establish the expected behavior, it should report an appropriately qualified concern or state that the behavior could not be verified.

## 6. Missing context

Missing requirements must not automatically receive a zero score or be treated as a defect.

For example:

> Business requirement verification: Not evaluated. No linked requirement or acceptance criteria were available.

The engine can still evaluate technical correctness, code quality, tests, and other dimensions where evidence exists.

## 7. Score and recommendation

The discussion identified several possible approaches:

- Weighted category scores.
- Deductions based on findings and severity.
- A hybrid model where category evaluation informs a score, while critical findings can independently affect the recommendation.

The hybrid approach was considered promising, but **no approach has been finalized**.

A high score must not hide a critical issue. The final model should make serious blockers visible independently of any aggregate score.

## 8. Open questions

- What exactly should the score represent: code quality, merge safety, or a clearly defined combination?
- Which categories should be included?
- How should unevaluated categories affect the score?
- How should severity and confidence influence findings?
- How should duplicate or related findings be handled?
- What findings should block approval regardless of score?
- What thresholds, if any, should map scores to recommendations?
- How should AI-generated findings be validated?

Do not invent final weights, score thresholds, or approval rules.
