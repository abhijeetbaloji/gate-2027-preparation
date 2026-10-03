# Context-Free Grammars — Revision

- `A → α`, `α ∈ (V ∪ Σ)*`. Leftmost / rightmost / parse tree are equivalent views of one derivation.
- Ambiguous grammar: two leftmost derivations of one string. Not “not CFL”.
- Invariant method: track `#a − #b` (or similar) on each production.
- `S → aSb | ε` → `{a^n b^n}`. `S → aSbS | ε` → balanced (`#a=#b` and prefix property).
- `S → aSb | X`, `X → aX | Xb | a | b` → regular `a*(a+b)b*`.
- CNF: `A → BC | a`. Derivation of a string of length `n ≥ 1` has **`2n − 1`** steps. `|V|` is irrelevant.
- GNF: `A → aα`, `α` variables only. `|w|` steps.
- Useless symbols: generating first, then reachable.
- Inherent ambiguity: `{a^i b^j c^k | i=j or j=k}`.
