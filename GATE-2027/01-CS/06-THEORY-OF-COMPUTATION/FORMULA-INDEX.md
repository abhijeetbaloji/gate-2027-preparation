# Theory of Computation — Formula / Rule Index

TOC has few numerical formulas. This index points at the equivalences, closure tables, construction rules and theorem conditions in each topic `FORMULAS.md`. The reason for each rule is in that topic’s `NOTES.md`.

## Regular expressions

[Regular expressions](01-REGULAR-EXPRESSIONS/FORMULAS.md)

- `∅L = ∅`, `{ε}L = L`, `∅* = {ε}`
- Star identities: `(r*)* = r*`, `(ε+r)* = r*`, `(r+s)* = (r*s*)*`
- Non-identities: `(r+s)* ≠ r*+s*`, `(rs)* ≠ r*s*`
- Arden: `X = Q + XP ⇒ QP*` and `X = Q + PX ⇒ P*Q`, needing `ε ∉ L(P)`
- State-elimination step: `R1 S* R2`
- Length counts: `k^n`; complement of a short forbidden pattern; inclusion–exclusion per length

## Finite automata

[Finite automata](02-FINITE-AUTOMATA/FORMULAS.md)

- Subset construction: at most `2^n` DFA states from an `n`-state NFA
- Reachable subset DFA may have far fewer than `2^n`; 1 state is possible
- Product: intersection / union uses `|Q1| · |Q2|` states before minimization
- Myhill–Nerode: number of pairwise distinguishable classes = size of the min complete DFA
- Standard sizes: ends with `w` (progress + possible sink); no `k` consecutive `1`s (`k+1` live states plus a dead state); third-symbol-from-end (`2^3 = 8`); two independent mods (`m·n`)

## Regular languages

[Regular languages](05-REGULAR-LANGUAGES/FORMULAS.md)

- Closed under union, intersection, complement, concatenation, star, reverse, prefix, suffix, quotient, homomorphism
- Not closed under infinite union, and not under “subset of”
- Finite ⇒ regular; regular ⇏ every subset regular
- `L · L^R` stays regular when `L` is; `{ww^R | w ∈ L}` need not
- Right-linear / left-linear grammars = regular languages

## Pumping lemma

[Pumping lemma](07-PUMPING-LEMMA/FORMULAS.md)

- Regular: exists `p`; every `s ∈ L`, `|s| ≥ p`, has a split `xyz` with `|xy| ≤ p`, `|y| ≥ 1`, and `xy^k z ∈ L` for all `k ≥ 0`
- CFL: exists `p`; split `uvwxy` with `|vwx| ≤ p`, `|vx| ≥ 1`, and `uv^k wx^k y ∈ L` for all `k ≥ 0`
- If `p` is a pumping length, every `q ≥ p` is one
- The lemma is necessary, not sufficient

## Context-free grammars

[Context-free grammars](03-CONTEXT-FREE-GRAMMARS/FORMULAS.md)

- Ambiguity: two leftmost derivations (equivalently two parse trees) of one string
- Useless-symbol order: generating first, then reachable
- CNF: `A → BC` or `A → a` (and `S → ε` only if `ε ∈ L` and `S` is not on a right-hand side)
- A CNF derivation of a string of length `n ≥ 1` has exactly `2n − 1` steps
- GNF: `A → aα` with `α` a string of variables

## Push-down automata

[Push-down automata](04-PUSH-DOWN-AUTOMATA/FORMULAS.md)

- Transition `δ(q, a, X) ∋ (p, γ)`: read `a` or `ε`, pop `X`, push `γ`
- NPDA + final state = NPDA + empty stack = CFL
- The two acceptance modes need not give the same language of *one* machine
- DPDA languages sit strictly between regular and CFL
- Empty-stack language of a DPDA is prefix-free
- CFL ∩ regular is CFL (PDA × DFA)

## Context-free languages

[Context-free languages](06-CONTEXT-FREE-LANGUAGES/FORMULAS.md)

- Closed under union, concatenation, star, reverse, homomorphism, intersection with regular
- Not closed under intersection, complement, or difference of two CFLs
- `L − R = L ∩ complement(R)` is CFL when `L` is CFL and `R` is regular
- Nested pairs CFL; crossed pairs and `{a^n b^n c^n}` not CFL
- `{ww^R}` CFL; `{ww}` not CFL

## Turing machines

[Turing machines](08-TURING-MACHINES/FORMULAS.md)

- Decides `L`: halt on every input, accept exactly `L`, reject the rest
- Recognizes `L`: accept exactly `L`; may loop outside `L`
- `L` decidable ⇔ `L` and `complement(L)` both RE
- Multi-tape and NTM do not change the RE languages
- Decidable closed under complement, union, intersection
- RE closed under union, intersection; not under complement
- Every regular language and every CFL is decidable

## Undecidability

[Undecidability](09-UNDECIDABILITY/FORMULAS.md)

- Many-one reduction: `A ≤ B` and `A` undecidable ⇒ `B` undecidable (direction matters)
- Rice: a nontrivial property of `L(M)` is undecidable; “`M` has five states” is not a language property
- DFA / NFA / RE: membership, emptiness, finiteness, equivalence, universality — decidable
- CFG: membership, emptiness, finiteness — decidable; equivalence, universality, ambiguity, “is `L(G)` regular?” — undecidable
- TM: membership RE-not-decidable; emptiness not RE; non-emptiness RE-not-decidable; regularity / universality / equivalence — undecidable
- “Runs more than a fixed `k` steps on every input / on some input” — decidable

## Chomsky hierarchy (quick inclusion)

```
regular  ⊂  CFL  ⊂  decidable  ⊂  RE  ⊂  all languages
              ⊂  DCFL ⊂ CFL
```

Regular ⊊ CFL (`{a^n b^n}`). CFL ⊊ decidable (`{a^n b^n c^n}` is decidable, not CFL). Decidable ⊊ RE (`A_TM`). RE ⊊ all languages (`complement(A_TM)`).
