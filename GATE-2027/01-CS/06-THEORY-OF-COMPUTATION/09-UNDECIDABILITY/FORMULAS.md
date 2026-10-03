# Undecidability — Rules

| Problem | Model | Status | Why / limitation |
|---|---|---|---|
| `w ∈ L` | DFA / RE | decidable | `\|w\|` steps |
| empty / finite / equal / `Σ*` | DFA | decidable | graph / minimize / complement |
| `w ∈ L(G)` | CFG | decidable | CYK |
| `L(G)=∅` / finite | CFG | decidable | generating variables / productive cycle |
| `L(G1)=L(G2)` / `L(G)=Σ*` / ambiguous | CFG | undecidable | do not copy onto DFAs |
| `w ∈ L(M)` | TM | RE, not decidable | `A_TM` |
| `L(M)=∅` | TM | not RE | complement is RE |
| `L(M)≠∅` | TM | RE, not decidable | `A_TM ≤` this |
| `L(M)` regular / finite / `Σ*` | TM | undecidable | Rice |
| `M` has ≤ 10 states | TM | decidable | syntax |
| `M` runs > `k` steps on every / some input | TM, `k` fixed | decidable | finite window of length `k` |
| exists DPDA for `L(N)` | NFA `N` | decidable | answer always yes |

Reduction: `A ≤ B` and `A` undecidable ⇒ `B` undecidable. Not the converse.
