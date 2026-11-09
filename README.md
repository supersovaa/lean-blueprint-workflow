# lean-blueprint-workflow

A lightweight Agent Skill for keeping **Lean 4 formalizations** and **human-readable LaTeX blueprints** aligned.

Lean の数学・物理の定義、定理、証明と、leanblueprint による解説を定理単位で対応付けて保守するための公開スキルです。

## When to use / 用途

Use this skill when **creating, revising, or reviewing a Lean formalization and its corresponding LaTeX blueprint**, including theorem links and consistency checks. The workflow uses the selected checkout's guidance and checks that readers can reach the paired sources from the project's entry points.

このスキルは Lean と Blueprint の対応関係を担当します。論文の構成・投稿原稿の執筆は、それぞれの論文リポジトリの方針で管理します。

The canonical executable guidance is [skills/lean-blueprint-workflow/SKILL.md](skills/lean-blueprint-workflow/SKILL.md). The upstream blueprint tool is [leanblueprint](https://github.com/PatrickMassot/leanblueprint).

## Repository contents

```text
skills/lean-blueprint-workflow/SKILL.md   # one canonical skill definition
examples/                                # optional Lean/TeX pairing
README.md                                 # purpose, activation and setup
LICENSE                                   # MIT
```

The workflow first establishes statement contracts, source structure, and paired deliverables; implementation and verification both follow that plan. It reads Lake to identify actual build requirements and configures the selected layout accordingly. Naming and documentation navigation are owned by [scope-aligned-naming](https://github.com/supersovaa/scope-aligned-naming/blob/490e4424c9b0c15f16e61d328054bf828a30f301/SKILL.md) and [index-driven-docs](https://github.com/supersovaa/index-driven-docs/blob/f64230344a72ceaee351d9a51c48397b74c5f0fa/SKILL.md), respectively. `examples/` contains optional reference material; ordinary skill use starts from `SKILL.md` and follows its referenced guidance.

## Install once / 共通インストール

In Codex, request the skill from the public GitHub directory:

```text
$skill-installer install https://github.com/supersovaa/lean-blueprint-workflow/tree/main/skills/lean-blueprint-workflow
```

Alternatively, install the `skills/lean-blueprint-workflow/` folder as `~/.agents/skills/lean-blueprint-workflow/` for a user-wide Codex skill, or under a project's `.agents/skills/` for that project.

Installation makes the skill available through the agent's skill discovery mechanism. Update the installed copy when you want to adopt newer instructions; use a pinned Git revision when reproducibility matters.

## Link it from each research repository / 研究リポジトリからの参照

Use the following work-type entry in the repository's `AGENTS.md` (or its established task-specific guidance):

```md
## Lean formalization and blueprint work

When creating, revising, or reviewing Lean 4 definitions, theorems,
or proofs together with their LaTeX blueprint, read and apply
[lean-blueprint-workflow](https://github.com/supersovaa/lean-blueprint-workflow/blob/main/skills/lean-blueprint-workflow/SKILL.md).
```

This direct link identifies the **single canonical rule source**. In an environment where the skill is installed, the agent can also activate it through skill discovery. When operating through a GitHub connection, the agent should open the linked `SKILL.md` at the start of this type of work. A link in `AGENTS.md` is a routing instruction; the agent needs access to the linked source.

For a paper in another repository, identify which Lean repository, commit, and fully qualified declarations the paper uses.

## Optional example

[examples/](examples/) shows a small Lean theorem and corresponding LaTeX theorem. Add the example to an initialized Lean/leanblueprint project before trying the compile and document commands.

## License

MIT — see [LICENSE](LICENSE).
