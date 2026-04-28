# Client Tech Proposal Writing Guide

This reference provides concrete examples of good and bad writing patterns for client-facing technical proposals.

## 1. Opening: Value First, Not Technology First

### ❌ Bad Opening (Technology-Stack First)

> 本系统前端采用 Vue 3 + Element Plus，后端采用 Go 语言模块化单体架构，消息队列采用 Kafka，缓存采用 Redis，数据库采用 PostgreSQL。服务间通过 gRPC 通信，部署在 Kubernetes 集群上。

**Problem**: The reader cannot judge whether this system solves their problem. They see a list of tools, not a solution.

### ✅ Good Opening (Value First)

> 当前试验平台的观测能力主要依赖人工配置和静态规则。当试验资源发生变化、网络状态波动或异常事件出现时，观测策略无法自动跟随，导致观测遗漏、定位滞后、过程不可追溯等问题。
>
> 本方案围绕"试验动态观测"能力建设，设计观测模板、事件处理、动态标签关联和观测记录机制，使平台能够根据试验状态和资源变化自动调整观测范围与观测粒度。

**Why this works**: The reader immediately understands the problem and the proposed solution direction.

## 2. Mechanism Description: Narrative Over Terminology

### ❌ Bad Mechanism Description (Engineering Terminology)

> PolicyEngine 接收 ResourceChangeEvent，查询 TemplateStore 获取绑定模板，生成 ConfigPlan。ConfigPlan 由 ConfigOrchestrator 调用 Adapter 执行。执行完成后通过 desired_state 与 actual_state 对账保证最终收敛。

**Problem**: Only the engineering team can understand this. A client or decision-maker sees jargon, not a mechanism.

### ✅ Good Mechanism Description (Role-Action Narrative)

> 当试验资源发生变化时，试验服务会生成资源变更事件。观测系统收到事件后，不直接按照事件内容盲目下发配置，而是重新读取当前试验的资源状态、标签信息和已绑定的观测模板。系统根据模板中的匹配规则判断新增资源是否属于某个观测范围，如果匹配，则生成新的观测任务；如果资源被删除或迁移，则回收或更新原有任务。通过这种方式，观测配置不再依赖人工维护，而是能够随试验资源变化自动收敛。

**Why this works**: The reader can form a mental picture of what happens, without needing to know any class names or internal architecture.

## 3. Problem Statement: Contrast, Not Assertion

### ❌ Bad Problem Statement (Empty Assertion)

> 现有观测系统存在性能不足、可扩展性差、智能化程度低等问题，无法满足日益增长的业务需求。

**Problem**: This could apply to any system. It provides no concrete information.

### ✅ Good Problem Statement (Specific Contrast)

> 传统网络观测技术（如 Ping/Traceroute、SNMP、sFlow）在试验环境中存在明显局限：
>
> - Ping/Traceroute 只能测量连通性和路径，无法反映真实业务流量的丢包和时延。
> - SNMP 轮询间隔通常为 5 分钟，无法捕获秒级性能波动。
> - sFlow 基于采样，精度不足以支撑逐流分析。
>
> iFIT 解决了"如何精准、真实地测量端到端及逐跳的业务级丢包和时延"这一核心问题。

**Why this works**: The reader understands exactly what is wrong today and why the new approach is needed.

## 4. Flow Description: Role + Action + Reason

### ✅ Good Flow Pattern

> **（2）采集策略下发（中心 → 边缘）**
>
> 试验观测平台（中心）通过接口调用指控平台的观测配置接口，传递参数：采集设备列表、测量模式、测量周期、目标流信息等。
>
> 指控平台解析策略后，调用网络控制器中的观测配置模板将配置转换为各设备的具体指令，并分别下发至入节点、中间节点、出节点。
>
> 设备收到配置后本地生效：入节点负责为目标流的首个报文封装测量头；中间/出节点识别测量头并执行统计。

**Why this works**: Every step identifies WHO acts (中心, 指控平台, 设备), WHAT they do, and WHY. The reader can follow the chain of actions.

## 5. Length and Focus

### ❌ Bad Approach (Comprehensive Coverage)

Trying to cover every aspect of a system in one document: architecture, data design, API design, deployment, monitoring, security, HA, distributed systems, risks, versioning — producing 30+ pages.

### ✅ Good Approach (Focused Mechanism Chapters)

Writing 3-6 focused chapters, each explaining one key mechanism in 800-1500 words. Total 8-12 pages. The reader can understand each mechanism independently.

## 6. Phased Delivery: Capability Stages, Not Sprint Plans

### ❌ Bad Phased Delivery

> Sprint 1（2 周）：完成数据库表设计和 API 开发。
> Sprint 2（3 周）：完成消息队列集成和缓存层。
> Sprint 3（2 周）：完成前端页面和集成测试。

**Problem**: Clients do not think in sprints or engineering tasks.

### ✅ Good Phased Delivery

> 第一阶段建设基础闭环，完成观测模板、动态标签和后台策略处理能力，实现资源变化后的观测任务自动跟随。
>
> 第二阶段建设动态观测能力，支持异常事件触发后的临时采样调整和自动恢复。
>
> 第三阶段建设智能增强能力，在确定性闭环基础上引入智能分析。

**Why this works**: Each stage describes a **delivered capability**, not an engineering task. The client can understand what they get at each stage.
