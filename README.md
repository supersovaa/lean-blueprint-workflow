# lean-blueprint-workflow

**Reusable Agent Skill for writing mathematical / physical explanations in LaTeX alongside Lean 4 formal proofs.**

Lean 4 による形式化と、leanblueprint による自然言語・LaTeX の定理や証明を対応付けて保守するための公開スキルです。数学・物理のさまざまなリポジトリで使えるよう、特定の研究テーマには依存しません。

> This repository contains an **agent skill**, not the upstream `leanblueprint` CLI itself. To build a blueprint, install and configure [Patrick Massot's leanblueprint](https://github.com/PatrickMassot/leanblueprint) in the target Lean project.

## What the skill does / 機能

- 新規または既存の Lean 4 / Lake プロジェクトの構成を確認
- 定義・補題・定理の Lean 宣言と LaTeX 本文を作成・更新
- `\lean{...}`、`\uses{...}`、`\leanok` を使って対応付け
- 物理学の仮定・数式の規約・数学的結論を照合
- `lake build`、`leanblueprint checkdecls`、`leanblueprint pdf`、`leanblueprint web` の検証結果を整理
- 論文リポジトリなどから別リポジトリの Lean 宣言を参照する際の、コミット固定と整合性確認

## Layout

```text
lean-blueprint-workflow/
├── LICENSE
├── README.md
├── skills/
│   └── lean-blueprint-workflow/
│       └── SKILL.md
└── examples/
    ├── README.md
    ├── BlueprintExample.lean
    └── BlueprintExample.tex
```

This repository **does not impose a directory layout on your research project**. The skill discovers the target project's conventions first.

## Installation / 導入

### Codex skill installer

In Codex, ask the skill installer to install the public GitHub skill directory:

```text
$skill-installer install https://github.com/supersovaa/lean-blueprint-workflow/tree/main/skills/lean-blueprint-workflow
```

### Manual installation for Codex

Place the `skills/lean-blueprint-workflow` directory at:

- `~/.agents/skills/lean-blueprint-workflow/` to use it across projects, or
- `<your-project>/.agents/skills/lean-blueprint-workflow/` to share it with one project.

Codex loads local skill directories with a `SKILL.md` file. Check [Build skills](https://learn.chatgpt.com/docs/build-skills) for current installation and distribution guidance. A public GitHub repository by itself does not automatically register the skill in ChatGPT or Codex.

## Example prompt / 使用例

```text
Use lean-blueprint-workflow. Add a theorem to my Lean project,
write its mathematical explanation in the blueprint,
connect them with the fully qualified Lean declaration name,
and report which checks actually passed.
```

日本語の例：

```text
lean-blueprint-workflow を使って、この定理の Lean 証明と
対応する LaTeX の解説を作り、両者の仮定と結論を照合してください。
実行した検証の結果も報告してください。
```

See [examples/](./examples/) for a minimal Lean/TeX pairing. The TeX example is an excerpt, not a standalone document.

## Validation in the target project

Once Lean, `leanblueprint` and the relevant document tools are configured:

```sh
lake build
leanblueprint checkdecls
leanblueprint pdf
leanblueprint web
```

The CLI's `checkdecls` checks declaration **existence**. Lean checks proofs; the correspondence between human prose and formal statement still requires review. `\leanok` is a status annotation rather than a compiler check.

## License

MIT — see [LICENSE](./LICENSE).
