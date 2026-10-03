# Context-Free Languages — MISTAKES

Typical mistakes for this topic (general error patterns, not records of any person's errors). Theory: [NOTES.md](NOTES.md).

## 1. Conceptual confusions

| Mistake | Correct idea |
|---|---|
| Three letters ⇒ not CFL | `{ a^n b^n c^m }` is CFL; the free index matters |
| `{ a^n b^m c^n d^m }` is CFL because each pair is CFL | Crossed pairs; not CFL. Nested `{ a^n b^m c^m d^n }` is CFL |
| `{ ww }` is CFL | Not, over a two-letter alphabet. `{ ww^R }` is |
| CFL closed under intersection / complement | Neither. Counter-example `{ a^n b^n c^n }` as an intersection |
| `CFL − regular` is not CFL | It **is** (`L ∩ complement(R)`) |
| `regular − CFL` is CFL | Not necessarily (`Σ* − C`) |
| `CFL ∩ regular` is regular | It is CFL, not always regular |
| `Q ⊆ P` with `P` regular ⇒ `Q` regular | `{ p^n q^n } ⊆ p* q*` |
| If `L` and `complement(L)` are CFL then `L` is regular | False; `{ a^n b^n }` over `{a,b}` |
| DCFL closed under union | No; closed under complement |
| Concatenating a non-CFL with a regular language yields a non-CFL | Not an automatic theorem |

## 2. Algebra mistakes

- Applying De Morgan with CFL complements as if they were CFL.
- Reading `L1 − L2` as `L2 − L1`.
- Treating “not closed” as “the result is never in the class”.

## 3. Identification mistakes

- `{ a^m b^m c^{m+n} }`: thinking leftover `c`’s are a regular tail after an empty stack (the bound `#c ≥ m+1` still mentions `m`).
- `{ a^m b^n c^{m+n} }`: thinking two matches are required (`m` and `n` are independent; only their **sum** is matched).
- Unary `{ a^n a^n } = a^{2n}` treated as `{ ww }` over `{a,b}`.

## 4. PYQ-derived traps (mapped stems only)

| Year / Q# | Trap pattern |
|---|---|
| 2025 CS1 Q.45 | Swapping which of `L1`, `L2` is CFL |
| 2021 Q.1 | Extract garbled; `L1 − L2` is the combination that need not be CFL, but solve from the PDF |
| 2021 Q.12 | Extract unreadable — do not invent options |
| 2017 Q.4 | Missing complement bar on statement II in the extract; intersection of two CFLs is the other false claim |
| 2011 Q.24 | Choosing `P ∩ Q` because “intersection with regular”, after forgetting `Q ⊆ P` makes it equal to `Q` |

## 5. Examination-time mistakes

- Writing “not CFL” without a grammar for the sibling that **is** CFL, then mixing the two.
- Using pumping in this folder when a one-stack / two-agreement picture already answers, or the reverse: claiming “not CFL” with no argument at all.

## 6. How to check yourself

1. How many independent unbounded equalities?
2. Nested/sequential vs crossed?
3. Did I rewrite `−` before applying closure?
4. Does “always” survive the standard counter-examples `{ a^n b^n }`, `{ a^n b^n c^n }`, `Σ*`?
5. Is the extract intact, or is the PDF mandatory?

---

## My Mistakes

| Date | Source | Question | Mistake | Root cause | Fix / Rule |
|------|--------|----------|---------|------------|------------|
|      |        |          |         |            |            |
