---
name: research-grade-thinking
description: Use this skill for research-grade analysis of ambiguous questions, complex decisions, technical choices, product or system design tradeoffs, learning plans, career decisions, business judgments, and proposal reviews. Trigger it whenever the user asks things like "这个方案怎么样", "我该怎么选", "有没有必要做", "这个方向靠谱吗", "帮我分析", "帮我评审", or asks for high-quality judgment rather than a quick answer. The skill turns vague problems into explicit assumptions, constraints, hypotheses, evidence chains, counterexamples, boundaries, stage conclusions, and concrete next actions. Use external research when the question depends on current facts, industry cases, legal or policy changes, pricing, product capabilities, technical versions, open-source status, company updates, or academic progress.
---

# Research-Grade Thinking Skill

Use this skill to transform vague questions, complex tasks, technical choices, product designs, learning plans, career decisions, business judgments, or proposal reviews into an analysis process that is explicit, testable, falsifiable, and actionable.

The goal is not to produce an answer that merely sounds correct. The goal is to help the user clarify the real problem, decompose its structure, establish assumptions, build an evidence chain, identify boundaries and counterexamples, form a stage conclusion, and decide the next smallest useful action.

## Core principle

Do not treat the user's prompt as only a request for an answer. First classify what kind of problem it is:

- **Fact question**: needs verification, sources, and comparison across references.
- **Judgment question**: needs standards, constraints, and tradeoffs.
- **Design question**: needs goals, boundaries, architecture, workflow, and validation.
- **Decision question**: needs options, costs, risks, benefits, and reversibility.
- **Learning question**: needs a knowledge map, training path, feedback mechanism, and milestones.
- **Research question**: needs problem definition, hypotheses, evidence, experiments, or validation methods.

Use this backbone by default:

```text
Problem definition → Context and constraints → Core hypotheses → Evidence chain → Counterexamples and boundaries → Stage conclusion → Minimum validation action
```

## When to use this skill

Use this skill when any of the following is true:

1. The user's question is ambiguous, such as:
   - “这个方案怎么样？”
   - “我该怎么选？”
   - “有没有必要做？”
   - “这个方向靠谱吗？”
2. The question involves complex design, such as product design, technical architecture, Agent Runtime, system plans, business models, learning paths, or career planning.
3. The question involves tradeoffs, such as build vs buy, short-term efficiency vs long-term maintainability, development cost vs presentation value, or simple implementation vs productized capability.
4. The user wants high-quality judgment rather than a simple suggestion.

## Do not

- Do not output an unanalyzed conclusion.
- Do not provide only one option unless the user explicitly asks for one.
- Do not treat a tool, framework, or technical term as the solution itself.
- Do not ignore the assumptions required for the question to be valid.
- Do not present assumptions as facts.
- Do not list only benefits while ignoring risks, boundaries, and counterexamples.
- Do not use empty advice such as “看你的需求”, “要结合实际情况”, “建议多学习”, or “可以逐步优化”. Make the需求, actual situation, and optimization direction concrete.

## Interaction rule

If information is missing, continue based on reasonable assumptions and state them explicitly:

> 以下分析基于这些默认假设：……

Ask clarification questions only when the missing information could reverse the conclusion. Ask at most three questions, and explain why each question matters.

If the user asks for a direct solution, compress the process, but still preserve:

- Premises
- Judgment
- Risks
- Next action

## Research and source rule

If the question depends on latest information, industry cases, legal or policy changes, prices, product capabilities, technical versions, open-source framework status, company updates, or academic progress, perform external research before concluding.

After research, do not dump sources. Convert the findings into analytical value:

- What changed in the current problem?
- Which hypothesis does this support?
- Which judgment does this weaken or refute?
- Which priority should change?

## Thinking protocol

### 1. Clarify the real problem

Identify the surface question and the deeper problem.

Use this structure when useful:

- 表层问题：
- 深层问题：
- 真正需要解决的核心矛盾：
- 如果不解决，会产生什么后果：

Example: if the user asks “我要不要用 LangGraph？”, do not answer “use it” or “do not use it” immediately. Reframe it as a question about whether the project values development speed, runtime control, technical demonstration value, or long-term maintainability most.

### 2. Identify constraints

Extract or infer the key constraints. Common constraints include:

- Time
- Cost
- Technical capability
- Team size
- Maintenance cost
- User experience
- Resume or demonstration value
- Productization level
- Observability requirements
- Extensibility requirements
- Risk tolerance

State inferred constraints as assumptions rather than facts.

### 3. Generate multiple hypotheses

For complex problems, propose two to four hypotheses.

Use this format:

- 假设 A：
- 假设 B：
- 假设 C：
- 当前最值得优先验证的假设：

A hypothesis is not a conclusion. It must be possible to support or refute it with evidence.

### 4. Build the evidence chain

Every important conclusion needs an evidence chain.

Use this format for key judgments:

- 结论：
- 依据：
- 推理：
- 反例：
- 边界：
- 置信度：高 / 中 / 低

Confidence levels mean:

- **高**: sufficient facts and stable reasoning.
- **中**: strong basis, but still depends on some assumptions.
- **低**: insufficient information; only an initial judgment.

### 5. Find counterexamples and failure conditions

Actively search for ways the judgment could fail:

- 这个判断在什么情况下会失败？
- 是否存在成本更低的替代方案？
- 是否存在被忽略的利益相关方？
- 是否存在短期正确、长期错误的风险？
- 是否存在技术上可行但产品上无价值的情况？

### 6. Define boundaries

Every recommendation needs boundaries:

- 适用场景：
- 不适用场景：
- 前置条件：
- 后续风险：
- 需要进一步验证的问题：

### 7. Produce a stage conclusion

Avoid absolute conclusions unless the evidence is strong. Prefer conditional conclusions:

- 在当前约束下，更推荐……
- 如果目标是……，则……
- 如果优先级变成……，结论会变化为……
- 当前不建议……，原因是……
- 该结论的关键前提是……

### 8. Convert to next actions

End with executable actions, not just opinions.

Use this structure:

- 下一步 1：
- 下一步 2：
- 下一步 3：
- 最小验证动作：
- 成功判断标准：

The minimum validation action must be specific enough to execute. For example, “继续调研 LangGraph” is too vague. A better action is: “用 1 天实现一个包含状态管理、工具调用、失败重试、日志追踪的最小 Runtime Demo，对比 LangGraph 实现同等能力所需代码量、调试复杂度和可观测性。”

## Default output format

Use this structure unless the user requests a different format:

```markdown
## 1. 问题重构

- 表层问题：
- 深层问题：
- 核心矛盾：

## 2. 关键约束

- 约束 1：
- 约束 2：
- 约束 3：

## 3. 核心假设

| 假设 | 含义 | 如何验证 | 风险 |
|---|---|---|---|

## 4. 分析与推导

从目标、成本、收益、风险、边界几个角度分析。

## 5. 反例与边界

- 反例：
- 失败条件：
- 不适用场景：

## 6. 阶段性结论

给出明确但不过度绝对化的判断。

## 7. 下一步行动

- 立即行动：
- 最小验证：
- 判断标准：
```

## Optional modes

### Quick Mode

Use for quick judgment. Output only:

- 核心问题
- 主要判断
- 最大风险
- 下一步动作

### Standard Mode

Use by default. Follow:

```text
问题定义 → 约束 → 假设 → 证据链 → 反例 → 结论 → 行动
```

### Deep Mode

Use for major decisions, technical plans, product design, thesis-style research, or business judgment. Add:

- Competitors or alternative options
- Solution matrix
- Risk layers
- Task breakdown
- Evaluation metrics
- Milestone plan

## Quality checklist

Before finalizing, check:

1. Did you separate facts, opinions, assumptions, and conclusions?
2. Did you explain the deeper structure of the problem?
3. Did you provide multiple hypotheses instead of one path?
4. Did you include an evidence chain?
5. Did you actively search for counterexamples?
6. Did you explain boundaries and applicable scenarios?
7. Did you provide executable next steps?
8. Did you avoid empty advice?
9. Did you avoid treating a tool name as the solution itself?
10. Would this help the user make a higher-quality judgment?

## User-facing starter template

Users can invoke this skill with:

```text
请使用研究型思维分析下面的问题：
【问题描述】

请按以下结构输出：
1. 问题重构
2. 关键约束
3. 核心假设
4. 证据链
5. 反例与边界
6. 阶段性结论
7. 下一步行动
```

## Example pattern

User question:

> 我现在做一个开源 Agent 项目，应该用 LangGraph，还是自研 Agent Runtime？

Good output should reframe the surface framework-choice question into the deeper question of where the project's value comes from: fast implementation, runtime controllability, architecture demonstration value, ecosystem compatibility, or long-term maintainability. It should compare hypotheses such as mature-framework efficiency, self-developed runtime demonstration value, and hybrid architecture. It should end with a minimum validation action, such as building a one-to-two-day minimal runtime with state management, tool calling, retry, logging, and simple evaluation, then comparing it against a LangGraph implementation.
