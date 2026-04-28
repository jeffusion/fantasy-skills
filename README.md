# Fantasy Skills

一个用于沉淀、维护和分发自定义 Claude / OpenCode Skills 的多 skill 仓库。

**仓库根目录下每个 skill 一个独立目录**，根 `README.md` 作为总索引，`CONTRIBUTING.md` 说明新增与维护规范。

## Skills

### 产品与方案设计

- [product-design-plan](./product-design-plan) - 生成完整、可协作落地的中文产品设计方案 / PRD，覆盖背景目标、用户故事、流程、功能规格、UI/UX、验收标准、风险与迭代计划。
- [client-tech-proposal](./client-tech-proposal) - 生成面向客户/甲方/立项评审的中文技术设计方案，以设计思路和关键机制为核心，用业务语言讲清"为什么这样设计"和"怎么工作"，不含 DDL/API/错误码等研发实现细节。
- [system-design-plan](./system-design-plan) - 生成面向研发内部的中文系统设计方案 / 详细设计，覆盖业务背景、概要设计、详细设计、数据设计（DDL）、接口契约、非功能设计、高可用、分布式专项、实施运维、风险评审与版本管理。

### 协作与思维工具

- [grill-me](./grill-me) - 针对计划或设计方案对用户进行 relentless 采访，逐个分支遍历决策树，直到达成共识。适用于用户想压力测试方案、被追问设计细节、或提到 "grill me"。

## 仓库结构

```text
.
├── README.md
├── CONTRIBUTING.md
├── .gitignore
├── client-tech-proposal/
│   ├── SKILL.md
│   ├── evals/
│   │   └── evals.json
│   └── references/
│       └── writing-guide.md
├── grill-me/
│   ├── SKILL.md
│   └── evals/
│       └── evals.json
├── product-design-plan/
│   ├── SKILL.md
│   └── evals/
│       └── evals.json
└── system-design-plan/
    ├── SKILL.md
    └── evals/
        └── evals.json
```

## Skill 目录约定

每个 skill 使用独立目录：

```text
skill-name/
├── SKILL.md              # 必需：frontmatter + skill 指令
├── evals/                # 推荐：测试提示与预期结果
│   └── evals.json
├── references/           # 可选：长文档、模板、规范
├── scripts/              # 可选：可复用脚本
└── assets/               # 可选：模板、图片、示例文件
```

`SKILL.md` frontmatter 至少包含：

```yaml
---
name: skill-name
description: 清楚说明什么时候触发、这个 skill 能完成什么任务。
---
```

## 打包验证

使用本机已安装的 `skill-creator` 打包脚本验证某个 skill：

```bash
python -m scripts.package_skill /home/wangjie/github/jeffusion_skills/product-design-plan
```

如需在 OpenCode 中安装，可将 skill 目录复制或链接到：

```text
~/.config/opencode/skills/<skill-name>
```

或使用打包生成的 `.skill` 文件进行分发。
