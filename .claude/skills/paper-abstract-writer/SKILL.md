---
name: paper-abstract-writer
description: Prepare an evidence-backed mathematical-modeling abstract from the final solution package and frozen results, with an optional pre-result outline that contains no invented findings.
---

# Purpose

Write the abstract last when numerical results are frozen. Before results exist, this skill may create only a structural outline. It does not summarize exploratory runs or claim a competition outcome.

# Modes

- `outline`: before freeze, create `paper/abstract_outline.md` with slots for problem, route, per-question output, validation, limitation, and keywords. Do not write metrics, comparative claims, or result wording.
- `final`: after all relevant Qx solution packages and freezes exist, create `paper/sections/abstract.tex` or the requested format.

Read `../_references/huawei-cup-writing-and-layout-patterns.md` for concise contest-paper style.

# Final Preconditions

- Every claimed subquestion has a solution package and current `frozen_numbers.json`.
- Claim scope, physical interpretation, and limitations are recorded in the decision ledger.
- The abstract format and word limit are known or treated as a visible constraint.

# Workflow

1. Build an abstract claim map from frozen numbers, final result analysis, robustness evidence, and decision IDs.
2. Draft in this order: problem context and objective; overall architecture; concise Q1/Q2/... method-output pairs; validation or comparative evidence; applicable range or limitation; keywords.
3. Prefer concrete frozen results to generic praise, but include only results material to the solution.
4. Check every number, method name, and conclusion against the package and body sections.
5. Save the claim map at `paper/claim_evidence_map.json` if it is not already current, then save the final abstract.

# Rules

- Do not write "first prize", "optimal", "significant", or "innovative" without a verified, contest-relevant basis; an abstract never guarantees an award.
- Do not introduce citations, equations, tables, unverified scope, or results absent from the body.
- Do not list procedural details unless they distinguish the mathematical route.
- Keep each Qx represented only when it has an answer in the paper.

# Verification

- Problem, route, outputs, evidence, and boundary are all present.
- Every numeric or comparative statement resolves to frozen evidence.
- Abstract, conclusion, and results section answer the same set of subquestions.
- The requested length and current contest template are respected.
