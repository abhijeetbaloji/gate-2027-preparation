# Context-Free Grammars — Rules

| Rule | When | Example | Limitation |
|---|---|---|---|
| CNF steps = `2n − 1` | CNF, `\|w\| = n ≥ 1` | `n = 90` → 179 | not for a general CFG; `ε` is the extra `S → ε` |
| GNF steps = `n` | GNF, `\|w\| = n ≥ 1` | | |
| `B → aBb \| ab` preserves `#a=#b` | that shape | 2026-style `B` | do not assume `A` preserves the same |
| `S → aS \| aSbS \| c` ⇒ `#c = #b + 1` | that grammar | 2024 | `#a > #b` is not forced |
| Ambiguity | two leftmost / two trees | `S → SS \| a` | language may still be unambiguous via another grammar |
| Useless-symbol order | generating, then reachable | | the other order can leave stranded variables |
