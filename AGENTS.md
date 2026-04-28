# PROJECT KNOWLEDGE BASE

**Generated:** 2026-04-28
**Commit:** no-git
**Branch:** no-branch

## OVERVIEW

Multi-skill repository for custom Claude / OpenCode Skills. It is documentation-first: each root-level skill directory contains a `SKILL.md` plus optional evals/resources; there is no application runtime.

## STRUCTURE

```text
jeffusion_skills/
├── README.md                 # public index and install/packaging notes
├── CONTRIBUTING.md           # required conventions for adding skills
├── product-design-plan/      # English-instruction skill for Chinese PRD/product-design output
│   ├── SKILL.md              # skill frontmatter + instructions
│   └── evals/evals.json      # prompt-based eval cases
└── AGENTS.md                 # this knowledge base
```

## WHERE TO LOOK

| Task | Location | Notes |
|------|----------|-------|
| Add a new skill | `CONTRIBUTING.md` | Follow kebab-case directory + `SKILL.md` + README index update. |
| Find available skills | `README.md` | Root index groups skills by domain. |
| Edit product design behavior | `product-design-plan/SKILL.md` | English instructions for Chinese PRD output, structure, quality checklist. |
| Add product-design test prompts | `product-design-plan/evals/evals.json` | Prompt-based evals; no code runner. |
| Package/validate a skill | external `skill-creator` env | Run from `/home/wangjie/.cc-switch/skills/skill-creator`. |

## CODE MAP

No code symbols. This repository currently has Markdown/JSON only.

## CONVENTIONS

- Multi-skill layout: each skill is a root-level directory, not nested under `skills/`.
- Skill directory names use kebab-case.
- Every skill requires `SKILL.md` with YAML frontmatter: `name` and `description`.
- `name` must match the directory name.
- `description` must include trigger contexts, common user phrasings, and output capability.
- Optional per-skill directories: `evals/`, `references/`, `scripts/`, `assets/`.
- If `SKILL.md` grows beyond roughly 500 lines, move long templates/specs/scripts into resource directories.
- Add every new skill to the root `README.md` index.
- Evals live per skill at `<skill-name>/evals/evals.json` with `skill_name`, `evals[]`, `id`, `prompt`, `expected_output`, `files`.
- Current evals are qualitative prompt expectations, not machine assertions.

## ANTI-PATTERNS (THIS PROJECT)

- Do not create a single-skill repo layout here.
- Do not put future skills under a top-level `skills/` folder unless the repository convention is explicitly changed.
- Do not commit generated `*.skill`, `*-workspace/`, `iteration-*`, `benchmark.*`, or `feedback.json` outputs.
- Do not include secrets, private data, malicious code, or hidden behavior in any skill.
- Do not let `SKILL.md` become an unbounded reference dump; use `references/` for long material.
- Do not fabricate external facts in writing skills; mark assumptions as `假设` or `待确认`.

## UNIQUE STYLES

- Skill instructions are written in precise English; product-design outputs are Chinese by default unless the user asks otherwise.
- Skills should explain why a workflow matters, not only list rigid commands.
- Product/PRD skills favor structured Markdown, tables, Mermaid flows, Given/When/Then acceptance criteria, and explicit risk/open-question sections.
- Keep repository docs practical and index-like; detailed behavior belongs inside each skill directory.

## COMMANDS

```bash
# Validate eval JSON
python -m json.tool /home/wangjie/github/jeffusion_skills/product-design-plan/evals/evals.json >/dev/null

# Package/validate a skill using the external skill-creator checkout
cd /home/wangjie/.cc-switch/skills/skill-creator
python -m scripts.package_skill /home/wangjie/github/jeffusion_skills/product-design-plan
```

## NOTES

- This directory is currently not a git repository; metadata above records `no-git`.
- README references `python -m scripts.package_skill`, but the script is not stored in this repo. It comes from the local `skill-creator` environment.
- Current scale: 5 project files, max depth 3, one skill. Root `AGENTS.md` is sufficient; child `AGENTS.md` files would duplicate parent rules.
