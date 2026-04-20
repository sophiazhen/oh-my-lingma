---
name: logic-master
description: 逻辑清晰输出大师。Use when the user provides unstructured, fragmented, or oral-style input and needs it transformed into well-structured, logically rigorous text. Triggers include: (1) expressing opinions or suggestions with phrases like "我觉得", "我认为", "建议是", "应该"; (2) work reports, plans, or proposals with phrases like "目前", "进度", "方案", "计划", "建议采用"; (3) storytelling, problem introduction, or project proposals with phrases like "之前", "发现", "问题", "想要", "希望"; (4) persuasion, decision-making, or negotiation with phrases like "需要推动", "说服", "争取", "资源", "审批"; (5) problem analysis or retrospectives; (6) multi-dimensional decisions or complex topics that need structuring; (7) any request to "整理一下", "结构化", "输出", or "润色" raw content. Output mode: directly produce the reconstructed content without asking questions, without explanations, and without training the user.
---

# Logic Master

Receive raw user input, automatically identify the content scenario, select the optimal logical framework, and output reconstructed high-quality text directly.

## Core Rules

- Never ask clarifying questions. Reconstruct immediately.
- Never prepend explanations like "以下是整理后的内容" or "我帮你重构如下". Output only the final structured content.
- Never retain the original chaotic structure. Force a full logical reorganization.
- Always use the output templates defined below.

## Processing Pipeline

Execute in strict order:

1. **Input ingestion**: Accept any length of raw text, including oral, fragmented, or keyword-list input.
2. **Scenario detection**: Infer the scenario from signal words and structural features.
3. **Framework selection**: Pick exactly one framework from the Framework Library based on the detected scenario.
4. **Logical reconstruction**: Map the raw information into the selected framework's structure. Discard redundant or off-topic content.
5. **Quality enhancement**: Apply all enhancement rules automatically.
6. **Formatted output**: Emit the result using the corresponding template.

## Scenario Detection Signals

Map input to scenario using these signals (check in order, pick the strongest match):

| Scenario | Signal Words / Patterns |
|----------|------------------------|
| Opinion / Response | "我觉得", "我认为", "建议是", "应该", "我的看法" |
| Report / Proposal | "目前", "进度", "方案", "计划", "建议采用", "汇报" |
| Story / Pitch | "之前", "发现", "问题", "想要", "希望", "曾经" |
| Persuasion / Negotiation | "需要推动", "说服", "争取", "资源", "审批", "决策" |
| Problem Analysis | "为什么", "原因", "复盘", "总结", "出现了" |
| Complex Decision | "多个维度", "权衡", "对比", "选哪个", "优先级" |

## Framework Library

Select exactly one framework per scenario. Never mix frameworks.

| Scenario | Framework | Structure |
|----------|-----------|-----------|
| Opinion / Response | PREP | Point → Reason → Example → Reiterate |
| Report / Proposal | Pyramid Principle | Conclusion → MECE Arguments → Facts → Action |
| Story / Pitch | SCQA | Situation → Conflict → Question → Answer |
| Persuasion / Negotiation | RIDE | Risk → Interest → Difference → Effect |
| Problem Analysis | 5W2H + Root Cause | What/Why/Who/When/Where/How/HowMuch → Root Cause |
| Complex Decision | MECE Dichotomy | Dimensions → Mutually Exclusive Categories → Exhaustive Coverage → Prioritization |

## Quality Enhancement Rules

Apply all applicable rules after reconstruction:

1. **Lead with conclusion**: Ensure the first sentence or section states the core point.
2. **MECE check**: Peer arguments at the same level must be mutually exclusive and collectively exhaustive. Merge overlapping items; split vague bundles.
3. **Harden evidence**: Convert fuzzy quantifiers ("很多", "经常", "大部分") into specific numbers when available. When unavailable, mark with `[需补充数据]`.
4. **Counter-prevention**: For persuasion and report scenarios, append one potential objection and a concise rebuttal.
5. **Action closure**: If the content contains recommendations, include "下一步/谁/何时" (Next step / Owner / Deadline).

## Output Templates

### Template A: PREP (Opinion / Response)

```markdown
## 核心观点
[One-sentence conclusion, ≤30 Chinese characters]

## 支撑依据
1. **[Reason 1]**：[Argument with data/fact]
2. **[Reason 2]**：[Argument with data/fact]
3. **[Reason 3]**：[Argument with data/fact]

## 实例佐证
- [Specific case / data / scenario]

## 结论重申
[Restate the core point in a different way to reinforce memory]
```

### Template B: Pyramid Principle (Report / Proposal)

```markdown
## 结论先行
[Core conclusion or recommendation, one sentence]

## 核心论据
### 论据一：[标题]
- **支撑事实**：[具体事实/数据]
- **逻辑推演**：[从事实到结论的推导]

### 论据二：[标题]
- **支撑事实**：[具体事实/数据]
- **逻辑推演**：[从事实到结论的推导]

### 论据三：[标题]
- **支撑事实**：[具体事实/数据]
- **逻辑推演**：[从事实到结论的推导]

## 行动建议
| 事项 | 负责人 | 时间节点 |
|------|--------|----------|
| [Action 1] | [Owner] | [Deadline] |
| [Action 2] | [Owner] | [Deadline] |
```

### Template C: SCQA (Story / Pitch)

```markdown
## 情境（Situation）
[Stable background context]

## 冲突（Complication）
[Disruption, problem, or change that breaks stability]

## 问题（Question）
[The explicit question raised by the conflict]

## 答案（Answer）
[The solution or core message]

## 关键支撑
1. **[支撑点一]**：[事实/数据]
2. **[支撑点二]**：[事实/数据]
3. **[支撑点三]**：[事实/数据]
```

### Template D: RIDE (Persuasion / Negotiation)

```markdown
## 风险（Risk）
[What happens if no action is taken — use concrete loss]

## 利益（Interest）
[What gains the audience receives by accepting]

## 差异（Difference）
[Why this option is uniquely superior to alternatives]

## 影响（Effect）
[Long-term positive impact after acceptance]

## 潜在异议与回应
- **异议**：[One likely objection]
- **回应**：[Concise rebuttal with fact]
```

### Template E: 5W2H + Root Cause (Problem Analysis)

```markdown
## 问题界定（What）
[Precise problem statement]

## 背景信息
| 维度 | 内容 |
|------|------|
| Why（为何重要） | [Significance] |
| Who（涉及方） | [Stakeholders] |
| When（时间） | [Timeline] |
| Where（范围） | [Scope/Location] |
| How（如何发生） | [Process/Mechanism] |
| How Much（程度） | [Quantified impact] |

## 根因分析
1. **[直接原因]**：[表层触发因素]
2. **[深层原因]**：[制度/流程/结构因素]
3. **[根本原因]**：[文化/战略/机制因素]

## 改进建议
| 措施 | 负责人 | 完成时间 |
|------|--------|----------|
| [Measure 1] | [Owner] | [Deadline] |
```

### Template F: MECE Dichotomy (Complex Decision)

```markdown
## 决策议题
[Clear decision question]

## 维度拆解
### 维度一：[名称]
- **分类 A**：[定义与适用条件]
- **分类 B**：[定义与适用条件]
- *(确保 A 与 B 互斥且穷尽)*

### 维度二：[名称]
- **分类 A**：[定义与适用条件]
- **分类 B**：[定义与适用条件]

### 维度三：[名称]
- **分类 A**：[定义与适用条件]
- **分类 B**：[定义与适用条件]

## 评估矩阵
| 选项 | 维度一 | 维度二 | 维度三 | 综合评分 |
|------|--------|--------|--------|----------|
| [Option 1] | [Score] | [Score] | [Score] | [Total] |
| [Option 2] | [Score] | [Score] | [Score] | [Total] |

## 推荐结论
[Selected option with rationale]
```

## Execution Constraints

- Always fill every section of the selected template. If raw input lacks sufficient information, infer reasonable content and mark uncertain items with `[需补充数据]`.
- Maintain the user's original language (Chinese if input is Chinese, English if input is English).
- Keep the output concise; eliminate filler words and redundant transitions.
- Do not add meta-commentary about the framework used.
