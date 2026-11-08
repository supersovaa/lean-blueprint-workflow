# Minimal example

`BlueprintExample.lean` demonstrates a complete Lean 4 theorem.

`BlueprintExample.tex` is an **include-only snippet** for a blueprint initialized with `leanblueprint new`. It assumes the `theorem` environment and relevant macros are already configured by that project.

To try it in your own Lean project:

1. Copy the Lean declaration into an imported Lean module (adjust the namespace as appropriate).
2. Include the TeX snippet in the blueprint's `content.tex`; adjust its `\lean{...}` reference to the final fully qualified Lean name.
3. Run `lake build`, `leanblueprint pdf`, `leanblueprint web`, and then `leanblueprint checkdecls` where the corresponding tools are installed. Web generation creates the declaration list used by `checkdecls`.

The example illustrates declaration-to-text correspondence. It does not constitute a standalone Lake or TeX project.
