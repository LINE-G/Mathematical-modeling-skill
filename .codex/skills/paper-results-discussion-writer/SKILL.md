---
name: paper-results-discussion-writer
description: Draft evidence-grounded results, discussion, applicability, and limitation sections for a mathematical-modeling contest paper after final results and robustness evidence are available.
---

# Purpose

Turn frozen experiment evidence into an argument readers can audit: result, comparison, interpretation, uncertainty, and boundary. This is not a generic experiment log or a method-writing skill.

Read `../_references/huawei-cup-writing-and-layout-patterns.md` before drafting.

# Preconditions

- Final result analysis, robustness report, solution package, and current frozen numbers exist.
- The modeler has recorded claim scope and physical/domain interpretation.
- Planned paper figures and tables passed render verification.

# Workflow

1. Build or refresh `paper/claim_evidence_map.json`. Each claim records its Qx, frozen value/source, comparison, figure/table, robustness support, limitation, and decision ID.
2. For each Qx write a compact sequence:
   - report the required output;
   - compare with the usable baseline or a declared reference when relevant;
   - explain the human-confirmed domain meaning;
   - state uncertainty, sensitivity, or error evidence;
   - delimit the tested scenario, applicable range, and failure boundary.
3. Add cross-question synthesis only when outputs genuinely interact.
4. Place exact values in tables and trends/structure in figures. Introduce every visual from the claim it proves.
5. Save `paper/sections/results_discussion.tex` or the requested section paths; return it to `paper-section-writer` for document integration, then hand the integrated draft to `paper-polisher`.

# Rules

- Every conclusion sentence must resolve to a claim-map entry.
- A baseline is evidence only when inputs, output definition, and evaluation setting are comparable.
- Distinguish observed results from explanations and extrapolations.
- Do not treat a sensitivity result as proof of global robustness.
- Do not hide failed scenarios; report them as limitations, fallback conditions, or scope restrictions.

# Verification

- Each Qx is answered and each answer has evidence.
- Comparisons are metric-compatible and scoped.
- Figures/tables support a named claim rather than decorate the section.
- Limitation and applicability statements agree with robustness evidence.
