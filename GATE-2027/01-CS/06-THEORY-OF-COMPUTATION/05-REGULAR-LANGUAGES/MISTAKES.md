# Regular Languages — MISTAKES

Typical mistakes for this topic (general error patterns, not records of any person's errors). Theory: [NOTES.md](NOTES.md).

## 1. Conceptual confusions

| Mistake | Correct idea |
|---|---|
| `{a^n}{b^n} = {a^n b^n}` | Concatenation picks two independent exponents; the product is `a*b*` |
| `a*b*` is not regular | Independent counts are regular; equal counts are not |
| `{a^n b^m \| n ≠ m}` is regular “because n and m are free” | Relative to `a*b*` this is the complement of `{a^n b^n}` |
| Every subset of a regular language is regular | `{a^n b^n} ⊂ {a, b}*` |
| Infinite union of regular languages is regular | `⋃_n {a^n b^n}` |
| `L ∪ M` regular ⇒ both regular | `{a^n b^n} ∪ {a, b}* = {a, b}*` |
| `L*` regular ⇒ `L` regular | A non-regular `L` containing `a` and `b` can satisfy `L* = Σ*` |
| `{ww \| w ∈ L}` is `L · L` | Concatenation does not force the two halves to be equal |
| Complement of a non-regular language can be regular | Regular languages are closed under complement both ways |
| `L1 ∩ L̄2 = ∅` means `L1 = L2` | It means `L1 ⊆ L2` |
| Unary `αβα` is a copy, hence not regular | Shortest unary `α` always works; the language is `a(a+b)+a` |
| `#a ≡ r (mod p)` and `#a = #b` is regular “because of the modulus” | The equality still requires unbounded memory |
| Left-linear grammars are not regular | Left-linear and right-linear generate the same family |
| Every regular grammar is LL(1) | Left recursion is allowed in a regular grammar and forbids LL(1) |
| Pumping a few strings proves regularity | Pumping never proves regularity; give a DFA / RE / finite MN index |

## 2. Closure / construction mistakes

- Flipping accept states of an NFA and calling it the complement.
- Reversing a DFA and expecting the result to stay deterministic.
- Treating “closed under union” as closed under infinite union.
- Using `L2 = Σ*` and concluding `L1 ∩ L2` regular implies `L1` regular — it does not; the hypothesis is too weak. (`L2 = Σ*` would make the intersection equal `L1`, but the stem does not give that `L2`.)
- Forgetting that `∅` is regular: it is a legal counter-example in “always true?” stems.

## 3. Myhill–Nerode mistakes

- Distinguishing `a^i` from `a^j` with a continuation that accepts *both* or *neither*.
- Counting unreachable DFA states as MN classes.
- Claiming two states are equivalent because they are both rejecting, without checking continuations.
- Using MN to argue CFL / not CFL.

## 4. PYQ-derived traps (mapped stems only)

| Year / Q# | Trap pattern |
|---|---|
| 2026 Q.51 | Concluding `L1` is regular or CFL from a regular intersection; forgetting that regular ⇒ CFL applies to `L2` |
| 2025 CS1 Q.44 | Treating `L2` as a copy language; or treating `L1` as “starts and ends with the same letter” |
| 2025 CS2 Q.52 | `{a, b}* ∩ {a^m b^n c^{m−n}}` still has the equal-count core; modular-and-equal is not modular-only |
| 2024 Q.23 | `L1 ∩ L̄2 = ∅` as equality; `L1 ∪ L3` always non-regular |
| 2020 Q.8 | Union regular ⇒ both regular; infinite-union closure |
| 2019 Q.7 | `{ww^R \| w ∈ L}` confused with `L · L^R`; prefix/suffix of regular need not be regular (they are) |
| 2014 Q.15 | Concatenation of `{a^n}` and `{b^n}` written as `{a^n b^n}` |
| 2008 Q.53 | `{n ≠ m}` marked regular; `{xcy}` marked non-regular because of the centre letter |
| 2007 Q.7 | Finite subset of a non-regular set marked non-regular; infinite union of finite sets marked regular |
| 2007 Q.53 | “Regular grammar” swapped with “regular language” in the LL(1) / LR(1) claims |

## 5. Examination-time mistakes

- Proving “always” by checking one example; disproving “always” requires one counter-example, proving it requires a construction.
- Stopping after “the language is infinite, hence not regular”.
- Using pumping on a language that is regular, then panicking when a split works.

## 6. How to check yourself

1. Independent counts or modular counts? If yes, name the DFA memory. If an equality of two unbounded counts, name the distinguishing prefixes.
2. Did I cancel a regular operand illegally?
3. For `αβα`, is `α` unary? If yes, does `|α| = 1` already generate the whole set?
4. For complement / equality, did I write `⊆` when the option said `=`?
5. Did I prove regularity with a machine / RE / finite index, not with pumping?

---

## My Mistakes

| Date | Source | Question | Mistake | Root cause | Fix / Rule |
|------|--------|----------|---------|------------|------------|
|      |        |          |         |            |            |
