# Mathematical Modeling Skills 使用说明

这套 skills 用于数学建模竞赛的题目解析、模型设计、代码实验、论文写作和提交前审查。它是一套有门禁的协作流程，不是一键代写器：AI 负责整理、实现、检查和排版，使用者负责问题取舍、模型含义、方法选择和最终授权。

优秀论文参考只用于校准模型架构、证据链、技术写作和版面检查，不会复制往届论文内容，也不保证一等奖或任何竞赛名次。

## 1. 安装

### 1.1 安装原生插件

需要先安装 Git，以及对应的 Claude Code 或 Codex/ChatGPT CLI。Windows 用户可在 Git Bash 或 WSL 中运行下面的命令：

```bash
git clone https://github.com/LINE-G/Mathematical-modeling-skill.git
cd Mathematical-modeling-skill
./install.sh
```

只安装一个平台：

```bash
./install.sh --target codex
./install.sh --target claude
```

先查看将要执行的操作：

```bash
./install.sh --dry-run
```

安装后重新打开 Claude Code 或 Codex 会话。后续更新：

```bash
cd Mathematical-modeling-skill
git pull
./install.sh
```

### 1.2 将项目文件部署到比赛工作区

原生插件模式适合日常使用；如果希望在比赛项目目录中直接看到 `.codex/skills`、`.claude/skills`、`AGENTS.md` 和 `CLAUDE.md`，使用项目模式：

```bash
./install.sh --mode project --target both --project-dir /path/to/contest
```

安装器发现目标文件已存在且内容不同时会停止。确认要替换时再加 `--force`；替换前会生成带时间戳的备份：

```bash
./install.sh --mode project --target both --project-dir /path/to/contest --force
```

## 2. 准备比赛工作区

技能仓库和比赛工作区建议分开。例如：

```text
Mathematical-modeling-skill/       # skill 仓库
my-contest-2026/                   # 当前赛题工作区
├── workspace/data_raw/            # 题目附件和原始数据，只读
├── workspace/data_clean/          # 清洗后的副本
└── scratch/                       # 临时探索
```

把题面和附件放进当前比赛工作区，原始数据放在 `workspace/data_raw/`。不要直接修改原始文件，也不要把没有来源的网上数据混入实验。

第一次对话发送仓库中的 [Initial Prompt-zh.md](../Initial%20Prompt-zh.md)，再补充以下信息：比赛名称、年份和当前官方格式要求；题面文件与附件位置；使用 Python 还是 MATLAB/北太天元；论文语言、页数或字数限制；团队更重视解释性、预测精度、可行性还是计算速度；哪些判断必须由队员确认。

推荐开场指令：

```text
这是本次数学建模竞赛工作区。请先读取 AGENTS.md 和相关 skills，运行 workflow-orchestrator，确认当前阶段和缺失材料。不要直接选模型或写代码。
```

## 3. 标准工作流

按下面顺序推进。每个 gate 未通过时，不要跳到后续产物。

| 阶段 | 主要 skill | 关键产物或门禁 |
|---|---|---|
| 状态检查 | `workflow-orchestrator` | 读取 `session_config.json`，判断当前 gate |
| 题目理解 | `problem-parser`、`problem-classifier`、`related-paper-analyzer` | G1：子问题、数据、约束、输出和成功标准明确 |
| 架构设计 | `model-architecture-designer`、`symbol-table-builder`、`model-assumptions-builder`、`data-auditor-cleaner` | 定义现实对象到数学对象的抽象、层间输入输出和证据路线 |
| 方法筛选 | `decision-prompt-builder`、`method-selector` | G2：主方法、可用 baseline、风险探针和备用触发条件 |
| 人工拍板 | `modeler-decision-logger` | G2.5：方法选择和理由写入 `methods/Qx/qx_decisions.jsonl` |
| 代码计划 | `model-code-analyzer` | 主方法、baseline、多阶段接口和验证矩阵 |
| 编码审查 | Python 或 MATLAB generator、`code-reviewer` | G3：代码运行成功，命名检查 JSON 通过 |
| 结果判断 | `result-report-generator`、`robustness-checker`、`final-method-explainer` | 结果、误差、敏感性、消融或边界证据 |
| 冻结材料 | `figure-table-planner`、`math-figure-generator`、`solution-package-builder` | G4：材料包和 `frozen_numbers.json` 完成 |
| 论文写作 | `paper-section-writer`、`paper-results-discussion-writer`、`paper-abstract-writer`、`paper-polisher`、`reference-manager` | G5：章节、结果讨论、摘要、引用和图表一致 |
| 最终审查 | `consistency-auditor`、`completeness-auditor`、`quality-assurance-auditor`、`award-readiness-auditor` | G6：所有必需审计通过后才组装终稿 |

多阶段模型必须说明每一层的数学职责。例如“机理模型 → 参数拟合 → 优化”，或“解析模型 → 独立仿真验证”。不能为了显得复杂而堆叠算法。

## 4. 你需要在关键节点做什么

这套流程会在以下节点要求使用者回答，而不是替你猜：

1. **方法筛选前**：输出形式、优先级、不可接受的失败、实验预算。
2. **风险探针后**：选择主方法和 baseline，并说明理由。
3. **实验后**：继续、调整方法，还是触发备用路线。
4. **最终冻结前**：保留、降级还是删除某项论文主张。
5. **终稿前**：确认物理含义、贡献边界和最终提交授权。

示例：

```text
Q1 的风险探针已经完成。请给我主方法、baseline、关键风险、可比指标和备用触发条件，我来确认方法选择；不要替我写决定理由。
```

```text
Q2 round1 已完成。请运行 result-report-generator 和 robustness-checker，只根据保存的结果给出继续、调整或启用备用的选择卡。
```

```text
所有 Qx 的最终结果已冻结。请按 problem-framing、assumptions-symbols、data-method、model-solution、results-discussion、evaluation-limitations、conclusion、abstract 的顺序准备论文。
```

## 5. `lean` 与 `submission` 模式

新项目默认使用：

```json
{
  "interaction_mode": "learning",
  "rigor_profile": "lean",
  "award_readiness_audit": true
}
```

- `lean`：适合探索和迭代，只保留 manifest、方法卡、决策、风险探针和运行摘要，不强制每轮长报告或冻结数字。
- `submission`：适合论文手交接和终稿，要求最终方法详解、结果分析、稳健性报告、材料包、冻结数字、论文和审计。
- `award_readiness_audit`：`submission` 默认启用，检查子题闭环、数学实质、证据独立性、输出可用性、写作和渲染版面。它是高标准准备审查，不是奖项预测。

切换到终稿模式时，使用明确指令：

```text
探索已完成。请将 planning/session_config.json 的 rigor_profile 切换为 submission，并重新判断各 Qx 是否满足论文交接条件。
```

## 6. 重要文件在哪里

```text
planning/
├── parse/problem_parse.json
├── classification/
├── manifests/Qx.json
├── model_architecture.json
├── evidence_plan.json
├── symbol_table.md
└── model_assumptions.md

methods/Qx/
├── qx_method_card.md
├── qx_decisions.jsonl
└── probes/risk_probe_summary.json

code/Qx/                         # Python；MATLAB 在 code/matlab/Qx/
├── qx_code_plan.md
└── reviews/qx_<lang>_review.json

results/Qx/
├── experiments/roundN/
│   ├── figures/ tables/ metrics/
│   └── run_summary.json
└── reports/
    ├── qx_final_result_analysis.md
    ├── qx_solution_package_for_writer.md
    └── frozen_numbers.json

robustness/Qx/qx_robustness_report.md

paper/
├── sections/
├── claim_evidence_map.json
├── figures/
├── refs.bib
└── audits/

reports/AWARD_READINESS_REPORT.md
```

论文中出现的数字必须来自当前的 `frozen_numbers.json`。如果代码修复导致数字变化，先记录解冻原因、重跑实验、重新冻结，再更新论文。

## 7. 论文写作顺序

不要从摘要开始写。推荐顺序是：问题重述与问题分析；假设、符号和数据处理；各子题的模型构建与模型求解；结果与讨论（结果、比较、解释、不确定性、适用边界）；稳健性、优点与局限；逐题结论；数字冻结后的最终摘要；图表、引用、排版和 PDF 审查。

每段只推进一个数学或证据点。公式定义变量和单位，图表支撑明确主张，题注写清条件和读者应看到的结论。历史优秀论文的版式只能作为可读性参考，字体、页边距、封面、页数和 AI 披露以当年官方模板为准。

## 8. 常用后续指令

```text
请运行 workflow-orchestrator，只报告每个 Qx 的当前 gate、阻塞项和一个下一动作。
```

```text
请检查 Q1 的数据审计和方法风险探针。不要生成代码，也不要选择方法。
```

```text
请审查 Q1 的 Python 代码是否通过 syntax、input_contract、method_alignment、reproducibility、output_contract 五项检查。
```

```text
请只检查论文里的数字、公式符号、图表引用和 frozen_numbers.json 的一致性，不修改模型。
```

```text
三个常规终审已通过。请运行 award-readiness-auditor，输出 BLOCKER、MAJOR、MINOR 和对应修复 skill。
```

## 9. 常见问题

### 找不到 skill

确认已经重新打开会话；Codex 用户检查 `C:\Users\<用户名>\.codex\skills` 或重新运行安装器，Claude 用户检查插件 marketplace 是否更新。

### 安装器提示目标文件冲突

先运行 `--dry-run` 查看冲突；确认要替换时使用 `--force`。不要直接删除未知目录。

### 方法还没选，AI 就开始写代码

停止当前操作，确认 G2 风险探针和 G2.5 人工决策是否存在。没有 `methods/Qx/qx_decisions.jsonl` 中的人工 `DECIDED` 记录，不应生成正式代码。

### 论文里的数字对不上

回到 `solution-package-builder` 和 `consistency-auditor`。不要手工编辑冻结数字；按照“解冻 → 修改 canonical source → 重跑 → 重冻结”处理。

### 论文看起来像模板拼接

让 `paper-results-discussion-writer` 重新按主张—证据映射组织结果，再让 `paper-polisher` 删除空泛连接语和实验流水账。不要用更多算法名称或装饰图掩盖论证缺口。

## 10. 提交前快速清单

- [ ] 每道子题都有明确输出、数学抽象、约束和验证目标。
- [ ] 主方法、可用 baseline 和复杂度理由已由使用者确认。
- [ ] 代码有固定随机种子、可复现输入和保存的输出文件。
- [ ] 结果包含可比指标，并完成与风险匹配的稳健性、消融、独立检查或边界测试。
- [ ] 所有核心数字已冻结，论文主张都能回溯到证据。
- [ ] 结果讨论写清结果、比较、解释、不确定性和适用范围。
- [ ] 摘要、正文、结论、图表和参考文献互相一致。
- [ ] PDF 已按当年官方模板渲染检查。
- [ ] consistency、completeness、QA 和默认启用的 award-readiness 审查均无 blocker/major。

## 11. 边界与责任

本项目不会编造数据、实验、引用、图表或奖项结果，也不会替使用者决定模型的物理意义。参赛者仍需遵守竞赛规则、独立完成研究并自行确认最终提交内容。
