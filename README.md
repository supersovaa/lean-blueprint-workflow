# lean-blueprint-workflow

Agent Skills for keeping **Lean 4 formalizations** and **human-readable LaTeX blueprints** aligned, and for writing **self-contained TeX explanations**.

Lean と TeX の対応管理、および TeX 文書内で説明を完結させる書き方を、研究リポジトリ間で共通利用するための公開スキルです。

## When to use / 用途

Use `lean-blueprint-workflow` when **creating, revising, or reviewing a Lean formalization and its corresponding LaTeX blueprint**, including theorem links and consistency checks. The workflow uses the selected checkout's guidance and checks that readers can reach the paired sources from the project's entry points.

`lean-blueprint-workflow` は Lean と Blueprint の対応関係を担当します。`self-contained-tex-writing` は、TeX 本文・Blueprint の作成・修正・レビューで、定義・仮定・導出・結論を文書内にそろえる書き方を担当します。TeX 執筆のスキルは単独でも利用できます。論文の構成・投稿形式は、それぞれの論文リポジトリの方針で管理します。

The canonical guidance is [skills/lean-blueprint-workflow/SKILL.md](skills/lean-blueprint-workflow/SKILL.md) for paired work and [skills/self-contained-tex-writing/SKILL.md](skills/self-contained-tex-writing/SKILL.md) for TeX exposition. The upstream blueprint tool is [leanblueprint](https://github.com/PatrickMassot/leanblueprint).

## Repository contents

```text
skills/lean-blueprint-workflow/SKILL.md     # Lean/TeX correspondence
skills/self-contained-tex-writing/SKILL.md  # self-contained TeX exposition
skills/*/LICENSE                          # license for each installable skill
examples/                                 # optional Lean/TeX pairing
README.md                                 # purpose, activation and setup
LICENSE                                   # MIT
```

The workflow first establishes statement contracts, source structure, and paired deliverables; implementation and verification both follow that plan. It reads Lake to identify actual build requirements and configures the selected layout accordingly. Naming and documentation navigation are owned by [scope-aligned-naming](https://github.com/supersovaa/scope-aligned-naming/blob/5d6099f7dd773781ab66d83a5d916b476a047602/SKILL.md) and [index-driven-docs](https://github.com/supersovaa/index-driven-docs/blob/f64230344a72ceaee351d9a51c48397b74c5f0fa/SKILL.md), respectively. `examples/` contains optional reference material; ordinary skill use starts from `SKILL.md` and follows its referenced guidance.

## Install once / 共通インストール

For Lean/Blueprint work, install both sibling skill directories from the same revision. In Codex, request them from the public GitHub directories:

```text
$skill-installer install https://github.com/supersovaa/lean-blueprint-workflow/tree/main/skills/lean-blueprint-workflow
$skill-installer install https://github.com/supersovaa/lean-blueprint-workflow/tree/main/skills/self-contained-tex-writing
```

Alternatively, copy both skill folders, including their licenses, under `~/.agents/skills/` for user-wide Codex use, or under a project's `.agents/skills/` for that project. Keep their directory names and sibling placement so the workflow's relative link resolves. For TeX-only work, install `self-contained-tex-writing/` on its own.

Installation makes the skill available through the agent's skill discovery mechanism. Update the paired installed copies together when adopting newer instructions; use a pinned Git revision when reproducibility matters.

## Link it from each research repository / 研究リポジトリからの参照

Use the following work-type entries in the repository's `AGENTS.md` (or its established task-specific guidance):

```md
## Lean formalization and blueprint work

When creating, revising, or reviewing Lean 4 definitions, theorems,
or proofs together with their LaTeX blueprint, read and apply
[lean-blueprint-workflow](https://github.com/supersovaa/lean-blueprint-workflow/blob/main/skills/lean-blueprint-workflow/SKILL.md)
and, for the TeX explanations,
[self-contained-tex-writing](https://github.com/supersovaa/lean-blueprint-workflow/blob/main/skills/self-contained-tex-writing/SKILL.md).

## TeX writing

When creating, revising, or reviewing TeX manuscripts or blueprint explanations,
read and apply
[self-contained-tex-writing](https://github.com/supersovaa/lean-blueprint-workflow/blob/main/skills/self-contained-tex-writing/SKILL.md).
```

Each direct link identifies that skill's **single canonical rule source**. In an environment where the skill is installed, the agent can also activate it through skill discovery. When operating through a GitHub connection, the agent should open the linked `SKILL.md` at the start of this type of work. A link in `AGENTS.md` is a routing instruction; the agent needs access to the linked source.

For a paper in another repository, identify which Lean repository, commit, and fully qualified declarations the paper uses.

## Optional example

[examples/](examples/) shows a small Lean theorem and corresponding LaTeX theorem. Add the example to an initialized Lean/leanblueprint project before trying the compile and document commands.

## License

MIT — see [LICENSE](LICENSE).
