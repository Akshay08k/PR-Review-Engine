# Product Principles

These principles capture the direction agreed or strongly established during product discussions. They should guide future proposals unless explicitly revised.

## 1. Review the PR with the context that exists

A PR may have a detailed description, linked work item, tests, and documentation—or very little beyond the diff. The engine must still perform useful analysis with the available information.

## 2. Context is discovered, not only supplied

Developers should not have to manually identify every related file or attach every relevant document. The engine should begin with the PR and discover relevant context where supported.

## 3. Missing context is not automatically a defect

If no business requirement is available, business compliance should be reported as not independently verifiable—not assigned a failing score by default.

## 4. Separate facts, inferences, and unknowns

The system should make clear whether a conclusion comes from explicit requirements, source code, tests, repository patterns, or an inference. Uncertain observations must not be presented as confirmed defects.

## 5. Findings need evidence

A finding should explain what is wrong or potentially wrong, why it matters, and what evidence supports it. Where possible, evidence should point to relevant files, lines, tests, requirements, schemas, or history.

## 6. Use deterministic evidence where appropriate

Compilation, test execution, static analysis, and other machine-verifiable checks should use suitable tools rather than asking an LLM to guess their results. The exact toolchain is undecided.

## 7. Distinguish actual defects from potential concerns

When expected behavior cannot be established, report a concern or an unanswered question rather than claiming a definite business defect.

## 8. Do not collect everything indiscriminately

Context discovery should be relevant to the changed code and review question. The engine should not assume that the entire repository or every connected source must be ingested for every PR.

## 9. The score must not hide critical findings

A high aggregate score should not neutralize a critical defect. The final decision model must account for blockers independently or otherwise ensure they cannot be averaged away. The exact mechanism is open.

## 10. The product must be more than an LLM API wrapper

The product value should come from context discovery, evidence gathering, evaluation orchestration, validation, explainability, and decision support—not merely sending a prompt to a model.
