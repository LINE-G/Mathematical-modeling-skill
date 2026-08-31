---
name: model-architecture-designer
description: Design a role-based mathematical architecture and evidence plan for each contest subquestion before algorithm screening, especially when the solution may combine mechanism, estimation, optimization, simulation, prediction, or graph modules.
---

# Purpose

Turn a framed problem into a small mathematical route, not an algorithm shopping list. This skill identifies what each module must explain, estimate, decide, or validate and how the modules exchange quantities. It does not choose the final method, write code, or fabricate a novel contribution.

Read `../_references/huawei-cup-award-paper-principles.md` before designing an architecture.

# Preconditions

- Problem parsing and classification are available.
- Required outputs, constraints, data inventory, and success criteria are sufficiently known.
- Material ambiguity in output form or evaluation has been resolved by the modeler.

# Workflow

1. For each Qx, state the chain `real object -> mathematical abstraction -> variables/states -> constraints -> output -> validation target`.
2. Identify the minimum layers needed. Typical patterns include:
   - mechanism/dynamics -> parameter fitting -> optimization;
   - analytical model -> independent simulation;
   - data characterization -> prediction -> decision;
   - signal/image preprocessing -> feature extraction -> reconstruction or classification;
   - graph representation -> constrained scheduling or allocation.
3. For every layer record its role, input, output, governing relation or quantity, assumptions, failure mode, and downstream consumer.
4. Define an evidence plan before algorithms are chosen: baseline comparison, exact or theoretical check, independent simulator, ablation, perturbation, or scenario stress test as appropriate.
5. Reject decorative layers. A layer must close a stated modeling gap, contribute a required output, or provide independent validation.
6. Save `planning/model_architecture.json` and `planning/evidence_plan.json`; update each Qx manifest when it exists.
7. Hand the architecture to `method-selector`, which may choose only methods consistent with the recorded roles.

# Architecture Contract

```json
{
  "schema_version": 1,
  "subquestions": [{
    "id": "Q1",
    "abstraction": {
      "real_object": "",
      "mathematical_object": "",
      "states_or_variables": [],
      "constraints": [],
      "required_outputs": [],
      "validation_target": ""
    },
    "layers": [{
      "id": "L1",
      "role": "mechanism|estimation|prediction|decision|optimization|simulation|validation",
      "input": [],
      "output": [],
      "mathematical_responsibility": "",
      "assumptions": [],
      "failure_mode": "",
      "downstream_layer": null
    }],
    "architecture_rationale": "",
    "excluded_complexity": []
  }]
}
```

The companion `planning/evidence_plan.json` records, for each Qx and core claim, the evidence role (`calibration`, `validation`, `robustness`, `ablation`, or `boundary`), source artifact, metric, predeclared comparison or threshold, and the action if the check fails.

# Rules

- Do not claim an architecture is innovative solely because it has many named methods.
- Keep empirical calibration distinct from independent validation when possible.
- Do not invent equations, causal relations, data fields, or validation data.
- Preserve human ownership of physical meaning, trade-offs, and final method selection.
- One module may fill multiple roles only when its inputs, outputs, and checks remain clear.

# Verification

- Every Qx has a traceable abstraction and output.
- Every layer has a necessary role and explicit handoff.
- Every top-level claim has a planned evidence path or an explicit limitation.
- The evidence plan includes a comparable baseline and relevant independent check or boundary test.
