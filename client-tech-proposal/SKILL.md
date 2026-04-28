---
name: client-tech-proposal
description: Create, improve, or review Chinese client-facing technical proposals, project approval documents, bid technical proposals, and stakeholder-oriented design documents. Use this skill when the user asks for a "client proposal", "project approval material", "technical design for client", "bid proposal", "立项材料", "客户方案", "面向甲方的设计方案", "投标技术方案", or any technical document intended for customers, project sponsors, decision-makers, or non-engineering stakeholders. The output is a review-ready Chinese document that explains design rationale, key mechanisms, and implementation paths in language that stakeholders can understand and use for project approval.
---

# Client-Facing Technical Proposal Skill

Use this skill to produce a Chinese technical proposal for **clients, project sponsors, bid evaluators, decision-makers, or non-engineering stakeholders**. The document must help the reader answer: **why this capability should be built, how it works at a mechanism level, whether it is feasible, and how it will be delivered in phases**.

This skill produces a fundamentally different document from the `system-design-plan` skill. That skill produces internal engineering design documents (DDL, API contracts, deployment architecture). This skill produces **stakeholder-readable proposals** where the primary goal is comprehension and persuasion, not implementation specification.

## Scope

Use this skill for technical proposals in these scenarios:

- **Project approval (立项)**: Documents that go into project approval materials for customer organizations or internal investment committees.
- **Bid proposals (投标方案)**: Technical sections of competitive bid documents that must demonstrate capability understanding and solution quality.
- **Customer-facing design supplements**: Design chapters that accompany a broader proposal, explaining key mechanisms in readable language.
- **Stakeholder briefings**: Technical design summaries for leadership, product owners, or cross-functional reviewers who need to understand direction without reading engineering specifications.

If the user explicitly asks for an internal engineering design document with DDL, API contracts, error codes, cache keys, or deployment details, refer them to the `system-design-plan` skill instead.

## Core Writing Philosophy

### The Information Layering Principle

A good client-facing technical proposal organizes information in **five layers**. The reader can stop at any layer and still have received value:

**Layer 1 — Value (3 minutes)**: What problem exists, why this capability matters, what it will achieve. The reader can stop here and already decide "this direction is worth pursuing."

**Layer 2 — Design approach (10 minutes)**: The overall design thinking, the core approach, how the pieces fit together. The reader can stop here and understand "how this works conceptually."

**Layer 3 — Key mechanisms (15-30 minutes)**: Each critical mechanism explained in narrative form — what it is, what problem it solves, how it works step by step, what happens after it is in place. The reader can stop here and judge "this design is sound and feasible."

**Layer 4 — Views and experience**: What the system looks like to different user roles, what the interaction model is.

**Layer 5 — Phased delivery and references**: How the capability will be built in stages, timeline, and optional technical references for those who want to go deeper.

**Critical rule**: Layers 1-3 must be readable without any knowledge of specific technologies, frameworks, or internal architecture. Layer 5 may contain optional technical details, but they must be structured so the reader can skip them without losing the thread.

### The "Person-Readable" Standard

Every paragraph in the proposal must pass this test:

> If a technically literate person who is NOT on the engineering team reads this paragraph, can they understand what is being proposed and why?

This does not mean "dumb it down." It means:
- Explain mechanisms in terms of **what happens and why**, not **which component calls which**.
- Use **role-action narrative** ("when X happens, the system responds by doing Y") instead of **implementation narrative** ("the PolicyEngine generates a ConfigPlan which the Orchestrator executes via Adapter").
- Put the **business reasoning** before the **technical reasoning**.

### What This Document Is NOT

This document is NOT:
- A system design document with DDL, API contracts, error codes, cache keys, or deployment topology.
- An engineering handoff document that developers use to write code.
- A technical architecture review document for internal architecture board.

If the user needs any of the above, use the `system-design-plan` skill.

## Input Handling

Extract the following information from the user's prompt before writing:

- **Project or capability name**: What are we proposing?
- **Customer or stakeholder context**: Who will read this document? What decision are they making?
- **Business background**: What is the current situation? What pain points or opportunities exist?
- **Core capability or mechanism names**: Which specific mechanisms or capabilities need to be explained? (e.g., "observation template mechanism", "dynamic tag association", "event-driven observation adjustment")
- **Existing system context**: What systems or platforms does this capability integrate with? What is the current state?
- **Scale or scope indicators**: How big is the environment? How many users, devices, or experiments?
- **Delivery expectations**: Does the customer expect phased delivery? Are there known constraints?

If information is missing, state reasonable assumptions under **"Assumptions"** and unknowns under **"To Be Confirmed"**, then continue. Do not stop unless the user's request is too vague to identify even the problem space.

## Standard Design Process

Use the following process to structure reasoning and writing:

1. **Clarify the reader and their decision**: Identify who will read this document and what decision they need to make after reading it. This determines emphasis and depth.

2. **Define the problem and value proposition**: State the current pain points clearly, then articulate what the proposed capability will solve. Use contrast: "before → after" or "current limitations → new capabilities."

3. **Articulate the design approach**: Explain the overall design thinking in plain language. What is the core idea? Why this approach over alternatives? How do the pieces connect?

4. **Explain each key mechanism**: For each mechanism the user specified (or that you identify as critical), write a self-contained explanation following the mechanism template (see below).

5. **Describe the user experience and views**: Explain what different user roles will see and do. Avoid UI framework terminology.

6. **Plan phased delivery**: Break the capability into buildable stages with clear milestones.

7. **Self-check against the quality checklist**: Verify every section passes the person-readable test.

## Default Output Structure

When the user does not specify a format, output a complete proposal using the following structure. When the user asks for a shorter version, keep all top-level sections but compress each into concise paragraphs.

```markdown
# 《[Project or Capability Name]》技术设计方案

## 0. 文档信息
- 版本：v0.1
- 作者：
- 日期：
- 目标读者：[客户/甲方/立项评审/方案负责人]
- 状态：草案 / 评审中 / 已确认

## 1. 建设背景
### 1.1 当前现状
### 1.2 核心痛点
### 1.3 建设必要性

## 2. 设计目标

## 3. 总体设计思路

## 4. [关键机制一名称]实现机制
### 4.1 机制定位
### 4.2 解决的问题
### 4.3 工作方式
### 4.4 运行过程
### 4.5 落地效果

## 5. [关键机制二名称]实现机制
（同上结构）

## 6. [关键机制三名称]实现机制
（同上结构）

## 7. [关键机制 N 名称]实现机制
（按实际需要增减）

## 8. 用户视图与体验设计

## 9. 分阶段建设路径

## 10. 假设与待确认事项
```

### Section-by-Section Requirements

#### 建设背景 (Background)

Write this section so that a decision-maker can read it in 2 minutes and understand why this capability is needed.

**MUST include**:
- What the current situation looks like (concrete, not abstract).
- What specific problems or limitations exist (use examples or scenarios).
- Why now is the right time to address this.

**MUST NOT include**:
- Technology stack or architecture choices.
- Internal team structure or process descriptions.
- Generic statements like "with the rapid development of..."

Use contrast when possible:

```markdown
当前试验平台的观测能力主要依赖人工配置和静态规则。当试验资源发生变化、
网络状态波动或异常事件出现时，观测策略无法自动跟随，导致观测遗漏、
定位滞后、过程不可追溯等问题。

本方案围绕"试验动态观测"能力建设，使平台能够根据试验状态和资源变化
自动调整观测范围与观测粒度。
```

#### 设计目标 (Design Goals)

Write 4-6 concrete goals. Each goal must describe a **capability**, not a **technology**.

Good goal: "支持资源变化后的观测自动跟随。当试验新增、删除或迁移资源时，系统能够自动调整对应观测任务。"

Bad goal: "采用 Kafka 消息队列实现事件的异步处理和解耦。"

#### 总体设计思路 (Overall Design Approach)

This is the most important section. It must explain the **design reasoning** in a way that a non-engineer can follow.

Write this as **connected narrative paragraphs**, not bullet lists. The narrative should cover:
1. What is the core design idea? (one sentence)
2. How does it work at a high level? (what happens first, then what, then what)
3. What are the key moving parts and how do they relate?
4. What guarantees does the design provide? (traceability, controllability, recoverability)

Example structure:

```markdown
动态观测能力采用"模板定义、标签关联、事件驱动、后台执行、过程记录"
的设计思路。

试验开始前，平台根据试验类型选择对应的观测模板。模板中定义该类试验
需要关注的观测对象、观测指标、触发条件和响应动作。

试验运行过程中，系统持续接收资源变化事件和观测异常事件。当资源发生
变化时，后台根据试验资源标签重新匹配观测模板，自动生成新增、调整或
回收观测任务。当异常事件发生时，系统根据模板中的事件规则临时提升
观测粒度。

所有自动动作均形成观测记录，包括事件来源、命中规则、执行动作、
执行结果和恢复状态。通过该机制，观测系统既能自动适配试验变化，
又能保证过程可追溯、动作可控制。
```

#### 关键机制 (Key Mechanism Sections)

Each key mechanism is a **self-contained chapter**. A reader should be able to read only this chapter and fully understand one mechanism.

Use the following template for each mechanism:

**4.1 机制定位**: What is this mechanism? One paragraph that defines it in plain language.

**4.2 解决的问题**: What specific problem does this mechanism address? Why can't the system work well without it? Use before/after contrast.

**4.3 工作方式**: How does this mechanism work? Describe the core logic in narrative form. Use role-action language: "when X happens, the system does Y." Do NOT describe which component, class, or service performs the action.

**4.4 运行过程**: Walk through the mechanism step by step in a realistic scenario. Number the steps. Each step should explain **what happens** and **why it happens this way**.

**4.5 落地效果**: After this mechanism is in place, what changes? What can users do that they couldn't before? What improves?

Each mechanism chapter should be **800-1500 words** of narrative text. Use tables only for supplementary information, not as the primary explanation.

**Critical writing rules for mechanism sections**:

1. **Narrative over tables**: A paragraph that explains how a mechanism works is worth more than three tables listing its attributes.

2. **Explain the "why" before the "how"**: Before describing what the mechanism does, explain why it needs to exist. "Traditional approaches rely on X, which causes Y problem. This mechanism solves it by Z."

3. **Use role-action narrative**:
   - ✅ "当试验资源发生变化时，系统根据当前资源状态和已绑定的观测模板重新计算观测范围。"
   - ❌ "PolicyEngine 接收 ResourceChangeEvent，查询 TemplateStore 并生成 ConfigPlan。"

4. **One chapter, one mechanism**: Do not combine multiple mechanisms in one chapter. Do not mix mechanism description with data design or interface design.

5. **Self-contained**: Each mechanism chapter should make sense even if the reader skips other chapters.

#### 用户视图与体验设计 (User Views and Experience)

Describe what the system looks like to different user roles, using **product language**, not UI framework language.

**MUST include**:
- Who are the primary user roles?
- What does each role see and do?
- How do users navigate from overview to detail?

**MUST NOT include**:
- UI framework names (Vue, React, Element Plus, Ant Design).
- Component-level implementation details.
- CSS, layout, or styling specifications.

#### 分阶段建设路径 (Phased Delivery Plan)

Describe how the capability will be built in stages. Each stage must be understandable to a non-engineer.

Write in terms of **capabilities delivered**, not **engineering tasks**:

```markdown
第一阶段建设基础闭环，完成观测模板、动态标签、资源变化事件、后台策略处理
和观测记录能力，实现资源变化后的观测任务自动跟随。

第二阶段建设动态观测能力，支持异常事件触发后的临时采样调整、逐跳观测、
流量镜像和自动恢复。

第三阶段建设智能增强能力，在已有确定性闭环基础上，引入智能分析。
```

**MUST NOT include**: Sprint plans, story points, developer assignments, CI/CD pipelines, or internal team processes.

## Diagram Requirements

Use Mermaid diagrams sparingly. Maximum **3-4 diagrams** for the entire proposal.

Only include diagrams that help explain **mechanism flows**:

```mermaid
flowchart LR
  A[资源变化事件] --> B[后台策略匹配]
  B --> C[生成观测动作计划]
  C --> D[执行观测调整]
  D --> E[写入观测记录]
```

Do NOT include:
- ER diagrams or database schema diagrams.
- Deployment topology diagrams.
- System architecture diagrams showing specific technologies (Kafka, Redis, PostgreSQL).
- State machine diagrams with implementation-level states.

## Writing Rules

### Rule 1: Do Not Start with Technology Stack

**Wrong**:
> 本系统前端采用 Vue 3 + Element Plus，后端采用 Go，消息队列采用 Kafka……

**Right**:
> 本方案围绕试验动态观测能力进行设计，重点解决观测策略无法随资源变化自动调整、异常过程缺少细粒度观测和观测动作不可追溯等问题。

### Rule 2: Translate Engineering Concepts into Business Language

**Wrong**:
> PolicyEngine 生成 ConfigPlan，由 ConfigOrchestrator 调用 Adapter 执行，通过 desired_state 与 actual_state 对账保证收敛。

**Right**:
> 系统不会在事件发生后直接修改观测配置，而是先生成一份观测动作计划。这份计划记录本次需要新增哪些采集任务、调整哪些采样周期、是否需要临时开启细粒度观测。执行完成后，系统会比对期望状态与实际状态，确保观测配置最终收敛到正确状态。

### Rule 3: Prefer Narrative Over Tables

Tables are for supplementary information, comparisons, and data references. The primary explanation of any mechanism must be in paragraph form.

A good pattern: write 2-3 paragraphs explaining how a mechanism works, then optionally add a table summarizing key points for reference.

### Rule 4: No Engineering Implementation Details in Main Body

The following content MUST NOT appear in the main body of the proposal:

- Database DDL, table schemas, or field definitions.
- API endpoint paths, request/response formats, or error codes.
- Cache key naming conventions, TTL values, or invalidation strategies.
- Specific middleware deployment or configuration (Kafka topics, Redis instances).
- Code-level class names, module names, or package structures.
- Internal service communication protocols (gRPC, REST, message queue specifics).

If the user explicitly asks for some of these, place them in an **Appendix** section, clearly marked as supplementary technical reference.

### Rule 5: Control Length

Aim for **8-12 pages** total for the main body. Each key mechanism chapter should be **800-1500 words**.

Do not generate a 30+ page "comprehensive" proposal. If the user asks for comprehensive coverage, explain that a client proposal should be focused and suggest breaking it into focused chapters instead.

### Rule 6: Write for Decision-Making

Every section should help the reader make a decision:
- Background → "Is this problem real?"
- Design goals → "Are these the right goals?"
- Design approach → "Does this direction make sense?"
- Key mechanisms → "Will this actually work?"
- Phased delivery → "Can we actually build this?"

If a section does not help the reader make a decision, remove it or move it to an appendix.

### Rule 7: Avoid AI-Generated Padding

Do NOT include:
- Generic slogans: "本系统具备智能化、自动化、平台化能力。"
- Empty adjective lists: "高性能、高可靠、高可用、高扩展。"
- Template filler: "随着 XX 的快速发展……"
- Excessive sub-sectioning that creates the appearance of structure without adding information.

Replace empty claims with concrete capability descriptions:

**Wrong**: "系统具备智能化、自动化观测能力。"

**Right**: "当试验新增虚拟机时，系统根据虚拟机所属试验、站点和标签，自动判断其是否需要纳入当前观测模板。如果匹配，后台自动生成对应采集任务。"

## Quality Checklist

Before finalizing, verify the proposal against these checks:

1. **3-minute test**: Can a decision-maker understand the problem and proposed solution by reading only sections 1-3?
2. **Person-readable test**: Can a technically literate non-engineer understand every key mechanism chapter?
3. **Value-first test**: Does the document explain "why" before "how" in every section?
4. **No implementation leak test**: Is the main body free of DDL, API paths, error codes, cache keys, and middleware configuration?
5. **Mechanism completeness test**: Does each mechanism chapter explain what it is, what problem it solves, how it works, and what changes after it is in place?
6. **Narrative dominance test**: Are the primary explanations in paragraph form, not tables or bullet lists?
7. **Decision-ready test**: Could a reader use this document to approve or reject a project?
8. **Appendix separation test**: Are all implementation-level details (if any) in a clearly marked appendix?
9. **Length control test**: Is the main body within 8-12 pages, with each mechanism chapter 800-1500 words?
10. **No AI padding test**: Is the document free of generic slogans, empty adjectives, and template filler?

## Output Language

Write the final proposal in Chinese by default. Keep English technical terms only when they are standard and widely understood (e.g., SLA, QPS, API, SDK, MVP, gRPC, Telemetry).

If the user explicitly requests another output language, follow the user's request while preserving the same structure and quality requirements.

## Relationship to Other Skills

| Skill | Purpose | Audience | Key Content |
|---|---|---|---|
| `product-design-plan` | Product requirements and feature design | Product, design, engineering | User stories, flows, acceptance criteria |
| **`client-tech-proposal`** (this skill) | Technical proposal for stakeholders | Clients, sponsors, decision-makers | Design rationale, key mechanisms, phased delivery |
| `system-design-plan` | Internal engineering design | Engineering, architecture, QA, ops | DDL, API, architecture, deployment, HA |

When the user's request spans multiple skills, ask which perspective they need. If they say "for the client" or "for project approval," use this skill. If they say "for engineering handoff" or "for implementation," use `system-design-plan`.
