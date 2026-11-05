---
name: lean-blueprint-workflow
description: Maintain Lean 4 definitions, theorems, and proofs together with their corresponding LaTeX blueprint explanations. Use when creating, revising, or reviewing a Lean formalization and its blueprint, including their links and consistency checks.
---

# Lean Blueprint Workflow

Use this skill when creating, revising, or reviewing Lean 4 definitions, theorems, or proofs together with their LaTeX blueprint explanations. Keep the blueprint readable for humans and the matching Lean statements mechanically checkable.

## Understand the project

1. Identify the target repository and read its Lean/Lake setup, existing blueprint, local conventions, and relevant definitions. Follow its established module and chapter boundaries.
2. Find existing declarations and TeX labels before creating new ones. Prefer relevant definitions and theorems already available in the project or its dependencies.
3. For a new project, keep Lean modules and TeX chapters in their respective directories, such as `Project/Topic/Result.lean` and `blueprint/src/Topic/Result.tex`. Treat matching paths as a navigation aid; identify exact correspondence by declaration names and TeX labels.
4. If the project needs blueprint initialization, use the upstream `leanblueprint` setup for the installed version and inspect the generated files before integrating them with the existing project.

## Work on the formalization and explanation

1. **State the contract.** Record types, quantifiers, assumptions, conventions, notation, and the exact conclusion. In physics, specify relevant units, sign conventions, boundary conditions, smoothness, and approximations. Distinguish modeling assumptions from deductions.
2. **Formalize.** Create or update Lean definitions and proofs; use explicit imports and stable fully qualified names. Arrange new modules so project build targets reach them.
3. **Explain.** Write the corresponding mathematical statement, derivation/proof, and interpretation in LaTeX. Check every hypothesis and conclusion against the Lean type. Explain physical significance separately from the formal claim.
4. **Link.** Give each TeX statement a stable `\label{...}` and associate it with its Lean declaration using `\lean{Namespace.declaration}`. Record actual dependencies with `\uses{...}` in the relevant statement or proof environment. Prefer theorem-level correspondence over filename-level correspondence.
5. **Mark progress accurately.** Use `\leanok` for a statement or proof only when that portion has been formalized. Treat it as a documentation marker; Lean's type checker establishes formal proof acceptance. Keep unfinished formalizations clearly marked.
6. **Synchronize changes.** When either side changes, revisit the matched statement, assumptions, proof, interpretation, and dependent references. Preserve established labels and names when their meaning stays the same.

## Verify

Run applicable checks from the target project root:

```sh
lake build
leanblueprint checkdecls
leanblueprint pdf
leanblueprint web
```

- Ensure each changed Lean module is included in the relevant build or compile it directly.
- `checkdecls` checks referenced declaration names; compare the mathematical meaning of Lean and TeX separately.
- Inspect the PDF/HTML rendering, references, formulae, and character encoding when building documents.
- Audit proofs for `sorry`, `admit`, additional axioms, and unintended hypotheses. Report precisely which claims are formally established.
- Record each check as passed, failed, or not run, with its actual result or reason.

## Cross-repository use

When a separate paper or research repository refers to Lean results, resolve the named repository, specific revision/commit, and declaration names. Compare its claims with the pinned Lean statements. Paper manuscript structure and publication workflow belong to that paper's own guidance.

## Report the outcome

List the changed Lean and TeX paths, matched declaration names and labels, assumptions/conclusions checked, verification results, and any remaining formalization work.

## References

- Upstream leanblueprint: https://github.com/PatrickMassot/leanblueprint
