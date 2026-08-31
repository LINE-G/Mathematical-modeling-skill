---
name: award-readiness-auditor
description: Run a high-standard, non-predictive final audit for mathematical-modeling contest papers, focusing on substantive modeling, evidence independence, complete subquestion answers, usable outputs, writing, and layout after ordinary submission audits pass.
---

# Purpose

Assess whether a submission has the qualities commonly expected of strong contest papers. This is a preparation audit, not a prediction or guarantee of a first-prize result; judges, rules, opponents, and year-specific criteria remain outside its control.

Read `../_references/huawei-cup-award-paper-principles.md` and `../_references/huawei-cup-writing-and-layout-patterns.md`.

# Preconditions

- Submission profile is active.
- Consistency, completeness, and quality-assurance audits have passed or their open findings are supplied.
- Final PDF/rendered paper, solution packages, freezes, robustness reports, and claim-evidence map are available.

# Audit Dimensions

1. **Question closure**: every Qx is explicitly answered in the body, conclusion, and abstract where appropriate.
2. **Mathematical substance**: abstraction, assumptions, objectives, constraints, derivation, and solver form a coherent route rather than an algorithm-name stack.
3. **Evidence independence**: claims have an appropriate baseline plus theory, simulation, ablation, perturbation, or scenario evidence when relevant; calibration is not mislabeled as validation.
4. **Decision usefulness**: outputs are legal, interpretable, actionable, and have stated applicable conditions.
5. **Narrative and presentation**: abstract-to-conclusion consistency, direct technical prose, figure/table argument quality, formula and symbol hygiene, and conformance with verified contest template requirements.

# Workflow

1. Sample canonical evidence directly; never certify based only on a summary or prose assertion.
2. For each dimension, record `PASS`, `CONDITIONAL`, or `FAIL` and findings classified as `BLOCKER`, `MAJOR`, or `MINOR`.
3. Distinguish an absent proof/experiment from a stated limitation. The latter may be acceptable only when the claim is appropriately narrowed.
4. Save `reports/AWARD_READINESS_REPORT.md` with traceable artifact paths, repair owner, and the final readiness verdict.
5. Return to the earliest producing skill for blockers. Do not edit the paper within this audit.

# Rules

- Never call a result "award-winning" or promise a ranking.
- Do not require every model to use all validation types; select tests that address its load-bearing risk.
- Do not accept cosmetic novelty, untested complexity, decorative figures, or generic claims as evidence of quality.
- Historical paper style informs clarity and structure but never overrides current official requirements.

# Verification

- Every Qx, central claim, and main visual was sampled against primary evidence.
- All blockers and majors identify a concrete repair target.
- Readiness verdict does not contradict prior audit results.
- Final assembly is recommended only when there are no blockers or majors.
