# Pumping Lemma — MISTAKES

Typical mistakes for this topic (general error patterns, not records of any person's errors). Theory: [NOTES.md](NOTES.md).

## 1. Conceptual confusions

| Mistake | Correct idea |
|---|---|
| “If a language pumps, it is regular” | The lemma is necessary, not sufficient |
| “If a language pumps, it is CFL” | Same, one level up |
| “Regular pumping failed, so not CFL” | `{a^n b^n}` fails regular pumping and is CFL |
| Checking one split of `a^p b^p` | Every legal `y = a^t`, `1 ≤ t ≤ p`, must fail |
| Pumping a string with `|s| < p` | The lemma is silent on short strings |
| Taking `y` from the `b`-block of `a^p b^p` | `|xy| ≤ p` keeps `y` in the `a`s |
| `|y| = 0` allowed | Then pumping never changes the string |
| CFL condition `|uv| ≤ p` | The bound is `|vwx| ≤ p`, and `|vx| ≥ 1` |
| Unique pumping length = min-DFA size | Min-DFA size is *a* pumping length; `(aa+bb)*` has smallest `p = 2` and 4 DFA states |
| If `p` fails, every larger integer fails | The opposite: if `p` works, every larger integer works |
| `k = 0` illegal | Deletion is the usual contradiction for equal counts |
| Finite languages “have no pumping length” | Any `p` larger than every word works vacuously |

## 2. Proof-structure mistakes

- Choosing `p` yourself as a number, then taking `s = a^3 b^3` with `3 < p`.
- Writing “consider `y =` the first symbol” and stopping, without saying why every other legal `y` is of the same shape.
- Mixing the two lemmas: a regular split `xyz` on a CFL question, or `uvwxy` with `|xy| ≤ p`.
- Intersecting with `∅` and claiming a regular core.

## 3. Pumping-length mistakes

- Testing `a^2` against `p = 3` in `{ a^{2+3k} } ∪ { b^{10+12k} }` — that word is too short to constrain `p = 3`.
- Forgetting that `b^{10}` *does* constrain every `p ≤ 10`.
- Assuming exactly one option can be a pumping length.

## 4. PYQ-derived traps (mapped stems only)

| Year / Q# | Trap pattern |
|---|---|
| 2019 Q.15 | Treating 3, 5 or 9 as pumping lengths because they divide a cycle of `a`-words; ignoring the sparse `b`-words; thinking only the min-DFA size is legal; thinking a larger integer cannot be a pumping length if a smaller one fails. The extract is OCR-garbled — read the PDF. |

## 5. Examination-time mistakes

- Proving regularity by exhibiting one pumped string that stays in `L`.
- Using CFL pumping to answer a “not regular” question when Myhill–Nerode on `a^i` is one line.
- Forgetting to say `s ∈ L` and `|s| ≥ p` before splitting.

## 6. How to check yourself

1. Did I write the quantifiers in the order ∃ `p`, ∀ long `s`, ∃ split, ∀ `k`?
2. Is my `s` at least `p` long, and is `y` forced into a single block by `|xy| ≤ p`?
3. Did I kill every legal split, not one?
4. If the question asks “not CFL”, did I use `uvwxy` and `|vwx| ≤ p`?
5. If the question asks which `p` *can* be a pumping length, did I look for a long word that cannot be pumped at the small options, and for a DFA-sized safe option among the large ones?

---

## My Mistakes

| Date | Source | Question | Mistake | Root cause | Fix / Rule |
|------|--------|----------|---------|------------|------------|
|      |        |          |         |            |            |
