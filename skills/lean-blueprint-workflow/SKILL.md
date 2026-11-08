---
name: lean-blueprint-workflow
description: Maintain Lean 4 definitions, theorems, and proofs together with their corresponding LaTeX blueprint explanations. Use when creating, revising, or reviewing a Lean formalization and its blueprint, including their links and consistency checks.
---

# Lean Blueprint Workflow

Use this skill when creating, revising, or reviewing Lean 4 definitions, theorems, or proofs together with their LaTeX blueprint explanations. Keep the blueprint readable for humans and the matching Lean statements mechanically checkable.

## Understand the project

1. Select the target repository and checkout, then read applicable repository and directory-local guidance (including `AGENTS.md` and linked skills) from that revision. After a branch, worktree, or revision change, recheck those entry points and refresh affected guidance and skill references. Read the Lean/Lake setup, existing blueprint, and relevant definitions from the selected checkout.
2. Find existing declarations and TeX labels before creating new ones. Prefer relevant definitions and theorems already available in the project or its dependencies.
3. Identify the roles and entry points for Lean sources, the mathematical manuscript, the blueprint, and generated outputs. Follow established module and chapter boundaries, applying [scope-aligned-naming](https://github.com/supersovaa/scope-aligned-naming/blob/2224434948e064209097b549945b658fd07ab948/SKILL.md) to changed names and paths. Resolve physical source roots through Lake configuration. For a new project, paths such as `Project/Topic/Result.lean` and `blueprint/src/Topic/Result.tex` can aid navigation; declaration names and TeX labels establish exact correspondence. Apply [index-driven-docs](https://github.com/supersovaa/index-driven-docs/blob/f64230344a72ceaee351d9a51c48397b74c5f0fa/SKILL.md) within its documentation scope, preserving tool-managed chapter navigation.
4. If the project needs blueprint initialization, use the upstream `leanblueprint` setup for the installed version and inspect the generated files before integrating them with the existing project.

## Establish the task obligations

Before editing, translate the applicable guidance and requested scope into concrete changes and checks: affected Lean modules and TeX statements, placement and navigation updates, and required verification. Reuse the current task context or established plan/handoff for these obligations. Reconcile them when the task or governing guidance changes.

## Work on the formalization and explanation

1. **State the contract.** Record types, quantifiers, assumptions, conventions, notation, and the exact conclusion. In physics, specify relevant units, sign conventions, boundary conditions, smoothness, and approximations. Distinguish modeling assumptions from deductions.
2. **Formalize.** Create or update Lean definitions and proofs; use explicit imports and stable fully qualified names. Arrange new modules so project build targets reach them.
3. **Explain.** Write the corresponding mathematical statement, derivation/proof, and interpretation in LaTeX. Check every hypothesis and conclusion against the Lean type. Explain physical significance separately from the formal claim.
4. **Link.** Give each TeX statement a stable `\label{...}` and associate it with its Lean declaration using `\lean{Namespace.declaration}`. Record prerequisites for stating a theorem with `\uses{...}` in its statement environment, and prerequisites used only to prove it in its proof environment. Prefer theorem-level correspondence over filename-level correspondence.
5. **Mark progress accurately.** Use `\leanok` for a statement or proof only when that portion has been formalized. Treat it as a documentation marker; Lean's type checker establishes formal proof acceptance. Keep unfinished formalizations clearly marked.
6. **Synchronize changes.** When either side changes, revisit the matched statement, assumptions, proof, interpretation, and dependent references. Preserve established labels and names when their meaning stays the same.

## Verify

Run applicable checks from the target project root:

```sh
lake build
leanblueprint pdf
leanblueprint web
leanblueprint checkdecls
```

- Build the web blueprint before `checkdecls`; web generation creates the declaration list that `checkdecls` reads.
- Check the task obligations against the resulting files and actual verification evidence.
- Ensure each changed Lean module is included in the relevant build or compile it directly.
- Check that the repository's primary entry document links to the Lean source entry, manuscript, and blueprint. Check document indexes or tool-managed chapter inputs, plus links from rendered statements to the corresponding source declarations. Update these paths with file moves.
- `checkdecls` checks referenced declaration names; compare the mathematical meaning of Lean and TeX separately.
- Inspect the PDF/HTML rendering, references, formulae, and character encoding when building documents.
- Audit proofs for `sorry`, `admit`, additional axioms, and unintended hypotheses. Report precisely which claims are formally established.
- Record each check as passed, failed, or not run, with its actual result or reason.

## Cross-repository use

When a separate paper or research repository refers to Lean results, resolve the named repository, specific revision/commit, and declaration names. Compare its claims with the pinned Lean statements. Paper manuscript structure and publication workflow belong to that paper's own guidance.

## Report the outcome

Report completion against the requested scope and task obligations. Identify the changed Lean and TeX paths, matched declaration names and labels, assumptions/conclusions checked, verification results, and remaining work. Distinguish a verified subset or progress checkpoint from completion of the requested work.

## References

- Upstream leanblueprint: https://github.com/PatrickMassot/leanblueprint
