# Context-Free Grammars — MISTAKES

Typical mistakes for this topic (general error patterns, not records of any person's errors). Theory: [NOTES.md](NOTES.md).

## 1. Conceptual confusions

| Mistake | Correct idea |
|---|---|
| Two derivations that rewrite independent variables in different orders are two parses | They are one parse tree; count leftmost derivations or trees |
| Ambiguous grammar ⇒ language not context-free | Ambiguity is a property of the grammar; the language is still CFL |
| Ambiguous grammar ⇒ inherently ambiguous language | The language may have another, unambiguous, grammar |
| `S → aSbS \| ε` generates every equal-count string | It generates Dyck words; `ba` is out |
| Right-linear grammars are the only CFGs | They are the regular special case |
| `S → aSb \| ε` is a regular grammar | Terminals on both sides of the variable; language not regular |
| Deleting useless productions shrinks `L(G)` | Those productions lie on no terminal derivation |
| CNF step count depends on `\|V\|` | For `\|w\| = n ≥ 1` it is `2n − 1` in every CNF derivation |
| `S → aB` is CNF | CNF needs `A → BC` or `A → a` |
| `S → aSb` is GNF | GNF forbids a trailing terminal |

## 2. Reading / invariant mistakes

- Swapping `and` with `or`, and `≥` with `>`, when two grammars differ only on whether `ε` or a pure-`a` string is generated.
- Treating a wrap `a^n _ b^n` as automatically non-regular when the hole already generates `a* … b*`.
- Claiming `n_a > n_b` for `S → aS | aSbS | c` after seeing that `aSbS` adds both; `u = 0` gives equality (`acbc`, and `c`).
- Checking an invariant only on the base production of `A` and not on the recursive production (ratio bounds).
- Counting distinct derivations that are not leftmost.

## 3. Construction mistakes

- Useless symbols: reachable first, generating second, stop. A variable reached only through a non-generating friend survives.
- Declaring a variable generating because it has a production, even if every sentential form still contains that variable (`A → AB`).
- Applying `2n − 1` to a non-CNF grammar or to `w = ε`.

## 4. PYQ-derived traps (mapped stems only)

| Year / Q# | Trap pattern |
|---|---|
| 2026 CS1 Q.52 | Forgetting that `B` is balanced; checking `#a` vs `#b` on `S`’s terminals alone |
| 2025 CS1 Q.19 | Linking the exponents (`a^n b^{2n}`) instead of taking a union of two families |
| 2024 CS1 Q.59 | Using `\|V\| = 10` in the arithmetic |
| 2024 CS2 Q.52 | Strict `n_a > n_b` or `n_c = 2 n_b`; not testing `w = c` |
| 2023 Q.39 | “Has `aSb` so not regular”; or `(a+b)*` which contains `ba` |
| 2016 CS1 Q.42 | `G1` as `m > 0`, or `G2` as `and` instead of `or` |
| 2007 Q.78–79 | Extract damaged; grammar is equal-count, not Dyck — `ba` is in |
| 2025 CS2 Q.40, 2024 CS2 Q.40, 2021 Q.31 | Spending TOC time on LL(1)/LALR tables |
| 2021 Q.13, 2015 Q.28 | Reading “CFG” as context-free grammar |

## 5. Examination-time mistakes

- Not testing `ε` and the shortest member against every closed form.
- Proving two grammars equivalent by checking three strings.
- Drawing a parse tree and then counting a non-leftmost derivation as a second leftmost derivation.

## 6. How to check yourself

1. Did I describe each variable before `S`?
2. Did I test a string that violates the claimed property?
3. For counts: did I use production-use equations **and** the shortest member?
4. For CNF steps: is the grammar in CNF and is `n ≥ 1`?
5. For useless symbols: generating, then reachable on what remains?
6. Is this stem actually compiler design?

---

## My Mistakes

| Date | Source | Question | Mistake | Root cause | Fix / Rule |
|------|--------|----------|---------|------------|------------|
|      |        |          |         |            |            |
