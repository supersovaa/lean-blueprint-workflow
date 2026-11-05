---
name: lean-blueprint-workflow
description: Create and maintain Lean 4 formalizations alongside human-readable LaTeX blueprints, including theorem links, proof dependencies, consistency reviews, and build checks. Use for Lean/TeX theorem authoring or maintenance in any Lake project. Do not use for ordinary paper writing without an associated Lean blueprint.
---

# Lean Blueprint Workflow

Maintain a readable mathematical blueprint and a Lean 4 formalization **together**, while keeping their responsibilities distinct. Work with mathematics and physics in any project; do not assume a fixed repository, domain, namespace, language, folder layout, or publication venue.

## Discover the target project first

1. Identify the actual repository/worktree and its user-defined conventions before editing. Respect its permissions, branch, existing files, and CI.
2. Read `lakefile.toml` or `lakefile.lean`, `lean-toolchain`, project root imports, existing modules, and any `blueprint/src` files.
3. Locate matching Lean declarations and TeX theorem labels. Search existing dependencies (Mathlib or local modules) before creating new material.
4. If a paper is in a separate repository, resolve its explicitly declared Lean references or pinned revisions; avoid guessing which revision a paper uses.
5. Prefer the established structure. A **suggested** layout for a new project is:

```text
project/
├── lakefile.toml
├── lean-toolchain
├── Project.lean
├── Project/
│   └── Topic/
│       └── Result.lean
└── blueprint/
    └── src/
        ├── content.tex
        ├── web.tex
        ├── print.tex
        └── Topic/
            └── Result.tex
```

This is a convention, not a required schema. Files need not match one-to-one: bind **individual declarations and labels**, not filenames.

## Initialize when requested

- Use an existing blueprint as-is. For a new blueprint in an existing Lake project, prefer the upstream `leanblueprint new` generator to obtain a compatible TeX/CI layout.
- Check the generator's proposed edits and Git settings before accepting them. Preserve existing Lean modules, TeX content, workflows, and user customizations.
- Check availability of Lean/Lake, the Python `leanblueprint` CLI, TeX (for PDF), and Graphviz (for dependency diagrams). Report missing prerequisites rather than claiming a successful build.

## Author a theorem or definition

1. **Specify the statement.** Identify variable types, quantifiers, hypotheses, notation, conventions, and result. For physics, make units, boundary conditions, smoothness assumptions, sign conventions, approximations, and model assumptions explicit when relevant.
2. **Implement the Lean declaration.** Reuse available mathlib and local definitions; write an actual term/tactic proof. Keep statement names stable and use the fully qualified name in the blueprint.
3. **Explain the mathematics.** Write LaTeX with motivation, definitions, statement, detailed human proof, and interpretation. Match notation and hypotheses to the checked Lean statement. State what was modeled or approximated separately from what is proved.
4. **Connect both sides.** In the appropriate TeX statement environment, use a stable `\\label{...}` and `\\lean{Namespace.declaration}`. Use `\\uses{label1, label2}` for actual prerequisite TeX labels; distinguish statement dependencies from proof dependencies by placing each in its correct environment. Multiple Lean declarations can be listed if needed.
5. **Mark verified progress.** Use `\\leanok` on a statement/definition only once it is formalized. Mark a proof environment `\\leanok` only once its proof is formalized as well. These are documentation annotations, **not Lean proof checking**. Use `\\notready` where appropriate for statements that require further blueprint work.
6. **Keep changes synchronized.** When a Lean statement changes, revisit the TeX statement, proof, physical interpretation, and downstream dependencies. When TeX changes, re-check corresponding Lean hypotheses and conclusions. Preserve existing labels unless migration is intentional.

### Minimal pairing

The `examples/` directory in this skill's repository provides one Lean declaration and a matching blueprint snippet. The TeX snippet is intended to be included inside a blueprint initialized by `leanblueprint new`, not compiled as a standalone TeX document.

## Validate

Run these from the target **Lean project root**, as dependencies and available tools permit:

```sh
lake build
leanblueprint checkdecls
leanblueprint pdf
leanblueprint web
```

- `lake build` typechecks the formalization as part of the configured build target(s). Confirm that new files are reachable through project imports/build targets, and compile the changed modules explicitly when appropriate.
- `leanblueprint checkdecls` checks that declaration names referenced in the blueprint exist; it does **not** establish that the prose statement has the same mathematical meaning.
- `leanblueprint pdf` and `leanblueprint web` check document rendering. PDF requires a TeX installation. When bibliography is present, build PDF before Web as recommended by leanblueprint.
- Also inspect rendered formulae, Japanese or other non-ASCII text if present, internal references, Lean links, and dependency graph.
- Review proof assumptions and claims manually. `sorry`, `admit`, unsubstantiated `axiom` substitutions, and unverified external claims must be identified rather than reported as completed formal proofs.
- Record each command as **passed, failed, or not run**, with concrete reasons and excerpts of actionable errors. Never infer test success from source inspection alone.

## Multiple repositories and papers

- Keep the Lean formalization and its blueprint together when that improves theorem maintenance; author separate research papers in their own repositories when appropriate.
- When referencing a theory repository from a paper repository, use an explicit repository identity, revision/commit and named Lean declarations. Git submodules or a documented pinned checkout are options; Lake Git dependencies are for Lean-to-Lean imports.
- Check the paper's claims against the **pinned** Lean revision and its documented hypotheses. Treat the broader physical interpretation as a separate scholarly review.
- Avoid creating new repositories or splitting existing ones without a concrete requirement. Let actual reuse and dependency boundaries determine packaging.

## Finish with an auditable summary

Report: (1) Lean paths and fully qualified declarations, (2) blueprint paths and LaTeX labels, (3) hypotheses/conclusion alignment, (4) build/check status, and (5) unformalized material or follow-up work. Distinguish a draft blueprint from a verified formalization.

## References

- Leanblueprint upstream: https://github.com/PatrickMassot/leanblueprint
- Agent Skills: https://learn.chatgpt.com/docs/build-skills
