# Contributing Skills

本仓库用于长期维护多个自定义 skill。新增或修改 skill 时，请遵循以下约定，保证结构一致、可测试、可分发。

## 新增 skill 流程

1. 在仓库根目录新建 kebab-case 目录，例如 `system-design-plan/`。
2. 创建必需文件 `SKILL.md`。
3. 在 `SKILL.md` frontmatter 中写清：
   - `name`：必须与目录名一致。
   - `description`：必须说明触发场景、用户常见表达和输出能力。
4. 如 skill 有典型使用场景，添加 `evals/evals.json`。
5. 如正文超过约 500 行，把长模板、参考规范或脚本放入 `references/`、`scripts/` 或 `assets/`。
6. 在根 `README.md` 的 Skills 索引中添加入口。
7. 使用 `skill-creator` 的 `package_skill` 脚本做结构验证。

## SKILL.md 编写规范

- 用指令式语言描述模型应该怎么做。
- 解释“为什么这样做”，不要只堆叠僵硬规则。
- 保持渐进披露：核心流程写在 `SKILL.md`，长材料放到资源目录。
- 对输出格式给出清晰模板。
- 对质量标准给出检查清单。
- 不要包含密钥、隐私数据、恶意代码或与 skill 描述不一致的隐藏行为。

## evals/evals.json 格式

```json
{
  "skill_name": "skill-name",
  "evals": [
    {
      "id": 1,
      "prompt": "用户真实会提出的任务",
      "expected_output": "期望结果说明",
      "files": []
    }
  ]
}
```

## 推荐验证项

- `SKILL.md` frontmatter 可解析。
- `description` 能覆盖真实触发表达。
- 测试 prompt 能体现 skill 的核心价值。
- 输出结构、质量检查和边界条件足够明确。
- 打包脚本通过。
