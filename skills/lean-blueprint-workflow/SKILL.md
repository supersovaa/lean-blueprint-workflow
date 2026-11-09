---
name: lean-blueprint-workflow
description: Maintain Lean 4 definitions, theorems, and proofs together with their corresponding LaTeX blueprint explanations. Use when creating, revising, or reviewing a Lean formalization and its blueprint, including their links and consistency checks.
---

# Lean Blueprint Workflow

Use this skill when creating, revising, or reviewing Lean 4 definitions, theorems, or proofs together with their LaTeX blueprint explanations. Keep the blueprint readable for humans and the matching Lean statements mechanically checkable.

## Understand the project

1. Select the repository and checkout, then read applicable repository and directory-local guidance, including `AGENTS.md` and linked skills. After a branch, worktree, or revision change, refresh affected guidance and references.
2. Read the Lean/Lake setup, mathematical manuscript, blueprint, and relevant definitions. Identify existing declarations and TeX labels to reuse, including suitable results in dependencies.
3. Locate the current source roots, module entry points, chapter navigation, and generated outputs. Read Lake configuration to distinguish the current arrangement from the build and public import requirements it must satisfy.

## Plan the paired work

Before implementation, establish the following decisions in the current task context or the project's existing plan/handoff. Reuse settled decisions and update the affected ones as the task or governing guidance changes.

1. **Statement contract.** Define the types, quantifiers, assumptions, conventions, notation, and exact conclusion of each affected result. In physics, include relevant units, signs, boundary conditions, smoothness, and approximations. Distinguish modeling assumptions from deductions.
2. **Source structure.** Assign responsibilities and dependency direction to modules, choose their source root, topic entry modules, paths, and namespaces, and apply [scope-aligned-naming](https://github.com/supersovaa/scope-aligned-naming/blob/490e4424c9b0c15f16e61d328054bf828a30f301/SKILL.md) to that choice from the repository root. Determine Lake configuration and imports from the chosen structure and actual compatibility requirements. For existing projects, include authorized structural changes and their migration effects in this decision.
3. **Paired deliverables and checks.** Identify the affected Lean declarations, mathematical statements, TeX labels, chapter inputs, source links, and verification commands. Include build targets, audit scripts, and packaging tools affected by the structure. Apply [index-driven-docs](https://github.com/supersovaa/index-driven-docs/blob/f64230344a72ceaee351d9a51c48397b74c5f0fa/SKILL.md) within its documentation scope, preserving tool-managed navigation. Declaration names and TeX labels establish exact correspondence across the chosen document and module layouts.

## Implement the paired work

1. **Set up the selected structure.** Configure source roots, module entry points, and build targets to match the plan. If blueprint initialization is needed, use upstream `leanblueprint` for the installed version, inspect its generated files, and integrate them into the selected layout.
2. **Formalize the contract.** Create or update Lean definitions and proofs in their assigned modules, using explicit imports and stable fully qualified names. Ensure the intended build targets reach them.
3. **Explain the result.** Write the mathematical statement, derivation/proof, and interpretation in LaTeX. Match every hypothesis and conclusion to the Lean type, and distinguish physical significance from the formal claim.
4. **Link the pair.** Give each TeX statement a stable `\label{...}` and associate it with its Lean declaration using `\lean{Namespace.declaration}`. Put prerequisites for stating a theorem in its statement environment's `\uses{...}`; put prerequisites used only in its proof in the proof environment. Prefer theorem-level correspondence over filename-level correspondence.
5. **Keep the pair synchronized.** When either side changes, revisit its matched statement, assumptions, proof, interpretation, and dependent references. Preserve labels and names while their meaning stays the same. Mark unfinished portions accurately; use `\leanok` only for a formalized statement or proof. This marker records documentation progress; Lean's type checker establishes proof acceptance.

## Verify against the plan

Run applicable checks from the target project root, generating the web blueprint before the declaration check:

```sh
lake build
leanblueprint pdf
leanblueprint web
leanblueprint checkdecls
```

- Compare the resulting files with the planned statement contracts, source structure, and deliverables. Verify build coverage for every changed Lean module or compile it directly; audit for `sorry`, `admit`, additional axioms, and unintended hypotheses.
- Compare Lean and TeX assumptions and conclusions mathematically. `checkdecls` verifies referenced declaration names; meaning requires this separate comparison.
- Follow the project's primary entry document through the topic entry modules, manuscript, and blueprint to the intended results and source declarations. Verify chapter navigation, source links, and affected audit and packaging paths against the selected structure.
- Inspect PDF/HTML rendering, references, formulae, and character encoding when building documents.
- Record each planned check as passed, failed, or not run, with its actual result or reason. Reconcile any mismatch with the plan before reporting completion.

## Cross-repository use

When a separate paper or research repository refers to Lean results, resolve the named repository, specific revision/commit, and declaration names. Compare its claims with the pinned Lean statements. Paper manuscript structure and publication workflow belong to that paper's own guidance.

## Report the outcome

Report completion against the requested scope and the plan. Identify changed Lean and TeX paths, matched declarations and labels, assumptions/conclusions checked, verification results, and remaining work. Distinguish a verified subset or progress checkpoint from completion of the requested work.

## References

- Upstream leanblueprint: https://github.com/PatrickMassot/leanblueprint
