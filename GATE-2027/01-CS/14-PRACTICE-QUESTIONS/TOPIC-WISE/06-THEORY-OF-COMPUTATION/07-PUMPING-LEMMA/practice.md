# Pumping Lemma — Practice Questions

Original practice for GATE CS. These questions are not from any GATE paper. Attempt the questions before reading the solutions.

The pumping lemma is a necessary condition. It can prove that a language is not regular, or not context-free. It cannot prove that a language is regular or context-free. The empty string is `ε`.

## Level 1 — Conceptual

## Q1 — MCQ

Which statement is the pumping lemma for regular languages?

A. If `L` is regular, then there exists `p` such that every `s ∈ L` with `|s| ≥ p` has some split `s = xyz` with `|xy| ≤ p`, `|y| ≥ 1`, and `xy^k z ∈ L` for every `k ≥ 0`  
B. If `L` is regular, then for every `p` and every split of every string, the pumped strings stay in `L`  
C. If some string in `L` can be pumped, then `L` is regular  
D. If `L` is regular, then every string in `L` has a split with `|y| = 0` that can be pumped

---

## Q2 — MCQ

The regular pumping lemma requires `|y| ≥ 1` because

A. otherwise `y` could be empty, pumping would not change the string, and no contradiction could ever be reached  
B. `y` must contain every symbol of the alphabet  
C. `|y| ≥ 1` forces `|xy| > p`  
D. the lemma applies only to strings of length 1

---

## Q3 — MCQ

For a context-free language, the pumping lemma supplies a split `s = uvwxy` satisfying

A. `|vwx| ≤ p` and `|vx| ≥ 1`  
B. `|vw| ≤ p` and `|v| ≥ 1`, with no condition on `x`  
C. `|uv| ≤ p` and `|v| ≥ 1`  
D. `|vwx| ≥ p` and `|vx| = 0`

---

## Level 2 — Standard GATE Style

## Q4 — MCQ

A correct proof that a language is not regular must

A. take an arbitrary split that obeys `|xy| ≤ p` and `|y| ≥ 1`, and show that every such split fails for some `k`  
B. choose one favourite split, show that this one split fails, and ignore the other legal splits  
C. pump a string whose length is smaller than `p`  
D. conclude that the language is regular if one pumped string happens to stay in the language

---

## Q5 — MCQ

Let `L = {a^n b^{n+1} | n ≥ 0}`, and let `p` be a pumping length. For `s = a^p b^{p+1}` and a legal split `s = xyz`, the string `xy^0 z` is

A. `a^{p-k} b^{p+1}` for some `k` with `1 ≤ k ≤ p`, and this string is not in `L`  
B. `a^p b^p`, which is in `L`  
C. `a^{p+k} b^{p+1}` for some `k ≥ 1`, which is in `L`  
D. `b^{p+1}`, and the lemma does not allow this string to be examined

---

## Q6 — NAT

The smallest pumping length of the regular language `(aa+bb)*` is ____.  
A positive integer `p` is a pumping length when every string of the language of length at least `p` has some split meeting the regular pumping conditions.

---

## Level 3 — Multi-Step

## Q7 — MCQ

The language `{a^n b^{2n} | n ≥ 0}` is

A. neither regular nor context-free  
B. not regular, but context-free  
C. regular  
D. finite

---

## Q8 — MSQ

Which of the following integers are pumping lengths for `(aa+bb)*`? Select all that apply.

A. `1`  
B. `2`  
C. `3`  
D. `4`

---

## Level 4 — Tricky / Trap-Based

## Q9 — MSQ

Which of the following arguments are invalid? Select all that apply.

A. “For `{a^n b^n | n ≥ 0}`, the single split that takes `y` to be the first symbol of `a^p b^p` fails. A proof need not look at any other split, so the language is not regular.”  
B. “There is a `p` such that every sufficiently long string of `L` has a working split. Therefore `L` is regular.”  
C. “Using pumping length `p`, pump the string `a^3 b^3` even when `3 < p`.”  
D. “For `{a^n b^{2n} | n ≥ 0}`, every legal split of `a^p b^{2p}` has `y` inside the `a`s, and deleting `y` destroys the relation ‘twice as many `b`s as `a`s’. Therefore the language is not regular.”

---

## Q10 — MCQ

Which statement is true?

A. If a language satisfies the conclusion of the regular pumping lemma, then it is regular  
B. If a language is regular, then it satisfies the conclusion of the regular pumping lemma  
C. If a language fails the regular pumping lemma, then it is context-free  
D. If a language fails the regular pumping lemma, then it is not context-free

---

## Level 5 — Challenge

## Q11 — MCQ

Let `s = a^p b^p c^p`, and suppose `s = uvwxy` with `|vwx| ≤ p`. The window `vwx` cannot contain both an `a` and a `c` because

A. the `a`-block and the `c`-block are separated by `p` `b`s, and a window of length at most `p` cannot cover that separation  
B. the pumping lemma allows only one alphabet symbol in `vwx`  
C. `p` must be even  
D. `v` and `x` are required to be empty

---

## Q12 — MCQ

Let `L = {a^{n^2} | n ≥ 0}`. Take a pumping length `p`, the string `a^{p^2}`, and a legal regular split whose `y` has length `k` with `1 ≤ k ≤ p`. The pumped string `xy^2 z` has length `p^2 + k`. This shows that

A. `L` is not regular, because `p^2 < p^2 + k < (p+1)^2`  
B. `L` is not context-free  
C. `L` is finite  
D. every pumping length of a unary language is a perfect square

## Answer Key
| Q | Type | Answer |
|---|------|--------|
| 1 | MCQ | A |
| 2 | MCQ | A |
| 3 | MCQ | A |
| 4 | MCQ | A |
| 5 | MCQ | A |
| 6 | NAT | 2 |
| 7 | MCQ | B |
| 8 | MSQ | B, C, D |
| 9 | MSQ | A, B, C |
| 10 | MCQ | B |
| 11 | MCQ | A |
| 12 | MCQ | A |

## Detailed Solutions

### Q1

Answer: A

The quantifiers are part of the lemma. For a regular language there exists a pumping length `p`. After that length is fixed, every sufficiently long accepted string must have at least one good split. The split is not chosen by the prover while proving non-regularity: the prover must defeat every split that obeys `|xy| ≤ p` and `|y| ≥ 1`. For a good split, every pump power `k ≥ 0`, including `k = 0`, stays in the language.

(B) reverses the quantifiers on `p` and on the split. (C) is the converse, which is false. (D) uses an empty `y`, which the lemma excludes.

### Q2

Answer: A

If `y` were allowed to be empty, then `xy^k z` would equal `s` for every `k`. The condition would be true of every string and could never produce a string outside `L`. The requirement `|y| ≥ 1` makes the pumped string actually change. It does not force the window `xy` to be longer than `p`; the lemma says the opposite, `|xy| ≤ p`.

### Q3

Answer: A

The context-free pumping lemma says: if `L` is context-free, then there exists `p` such that every `s ∈ L` with `|s| ≥ p` has a split `s = uvwxy` with

- `|vwx| ≤ p`,
- `|vx| ≥ 1`,
- `u v^k w x^k y ∈ L` for every `k ≥ 0`.

The two copies `v` and `x` are pumped together. Either one may be empty, but not both. Option (C) is the regular lemma, mistakenly copied onto a context-free split. Option (B) forgets that `x` may carry the pumped symbols and that the bounded window is `vwx`, not `vw`.

### Q4

Answer: A

Because the lemma only promises that some split exists, a non-regularity proof must show that no legal split works. Fix `L` and assume it is regular. Let `p` be given by the lemma. Choose one string `s ∈ L` with `|s| ≥ p`. Then let `s = xyz` be an arbitrary split with `|xy| ≤ p` and `|y| ≥ 1`, and for every such split produce a `k` with `xy^k z ∉ L`.

Checking one split leaves open the possibility that another split pumps successfully. Pumping a string shorter than `p` is outside the hypothesis. Finding one string that does pump is what the lemma predicts for a regular language; it is not a test that proves regularity.

### Q5

Answer: A

The string `s = a^p b^{p+1}` is in `L` and has length greater than `p`. Any legal split has `|xy| ≤ p`, so `xy` lies entirely inside the `a`s. Thus `y = a^k` for some `k` with `1 ≤ k ≤ p`, since `|y| ≥ 1` and `|xy| ≤ p`.

Deleting `y` leaves `a^{p-k} b^{p+1}`. For this string to be in `L` one would need `p + 1 = (p − k) + 1`, hence `k = 0`. But `k ≥ 1`. The pumped-down string is outside `L`, for every legal split.

(B) deletes a `b`, which a legal split cannot do: the window `xy` never reaches the `b`s. (C) is pumping up, and `a^{p+k} b^{p+1}` is also outside `L`, but it is not `xy^0 z`.

### Q6

Answer: 2

The language `(aa+bb)*` is regular. Its strings are concatenations of the blocks `aa` and `bb`.

The integer `1` is not a pumping length. The string `aa` has length at least 1 and is in the language. The only split with `|xy| ≤ 1` and `|y| ≥ 1` is `x = ε`, `y = a`, `z = a`. Then `xy^0 z = a`, which is not in the language.

The integer `2` is a pumping length. Any nonempty string of the language begins with `aa` or with `bb`. Take `x = ε`, let `y` be that first block, and let `z` be the rest. Then `|xy| = 2`, `|y| = 2`, and `xy^k z` is `k` copies of a legal block followed by another string of the language. The result is in `(aa+bb)*` for every `k ≥ 0`, including `k = 0`.

Since `1` fails and `2` works, the smallest pumping length is 2. It is smaller than the number of states of the minimal DFA, which has 4 states: aligned at a block boundary (accept), having just read one `a`, having just read one `b`, and a rejecting sink for a broken pair. The lemma guarantees that the number of states of some DFA is a pumping length; it does not say that this number is the smallest one.

### Q7

Answer: B

The grammar `S → aSbb | ε` generates exactly `{a^n b^{2n} | n ≥ 0}`. Every derivation wraps one `a` and two `b`s, and the inductive converse is the same count. The language is context-free and infinite.

It is not regular. Let `p` be a pumping length and take `s = a^p b^{2p}`. Every legal split puts `y = a^k` inside the `a`s, with `1 ≤ k ≤ p`. Then `xy^0 z = a^{p-k} b^{2p}`. The `b`-count is twice the old `a`-count, not twice `p − k`. That string is outside the language. Failure of regular pumping does not affect the grammar, so the language remains context-free.

### Q8

Answer: B, C, D

Q6 shows that `2` is a pumping length and `1` is not.

If `p` is a pumping length, then every larger integer `q` is one too. A string of length at least `q` also has length at least `p`, so it has a split with `|xy| ≤ p`. That same split satisfies the weaker demand `|xy| ≤ q`, and it already pumps inside the language. Therefore `3` and `4` are pumping lengths.

The trap is to think that a pumping length must equal the number of DFA states, or that only one integer qualifies.

### Q9

Answer: A, B, C

(A) is invalid because of the quantifier on the split. For this particular language every legal `y` does fail, but an argument that inspects only “the first symbol” has not said so. Another split, such as `y = a^2` when `p ≥ 2`, is still allowed by the lemma until it is checked. The repair is one line: every legal `y` is `a^k` for some `k ≥ 1`, and every such `k` breaks the equality. That repaired argument is valid; the argument written in (A) is not.

(B) is invalid because it treats a necessary condition as a sufficient one. The pumping conclusion can hold, or appear to hold for the strings one tried, without a DFA existing. Regularity is proved by giving a DFA, an NFA, or a regular expression.

(C) is invalid because the lemma says nothing about strings shorter than `p`. A short string may leave the language when pumped even if the language is regular. The string used against the lemma must be at least `p` long, and `p` is chosen by the lemma, not by the prover. One cannot first choose `a^3 b^3` and then allow an unknown `p` larger than 3.

(D) is valid. It is the proof in Q7: the length bound forces every `y` into the `a`s, and the numerical relation fails for every positive `k = |y|`.

### Q10

Answer: B

(B) is the lemma itself: regularity implies the pumping property.

(A) is the converse, and it is false. The lemma is not a test one passes in order to become regular.

(C) and (D) confuse the two lemmas. Failure of regular pumping proves that the language is not regular. It can still be context-free, as `{a^n b^n | n ≥ 0}` and `{a^n b^{2n} | n ≥ 0}` are. It can also fail to be context-free, but the regular lemma does not prove that stronger claim. The context-free pumping lemma is a separate necessary condition, with a different split.

### Q11

Answer: A

In `a^p b^p c^p`, the last `a` and the first `c` have `p` `b`s between them. Any substring that contains at least one `a` and one `c` therefore has length at least `p + 2`. The pumping window `vwx` has length at most `p`, so it lies inside `a*b*`, or inside `b*c*`, or inside a single block. It never contains both an `a` and a `c`.

This is why the context-free pumping proof for `{a^n b^n c^n | n ≥ 0}` can be a short case analysis. Let `L` be that language, assume a pumping length `p`, and take `s = a^p b^p c^p`. For an arbitrary legal split, `vx` contains at least one symbol and only symbols from one block or from two adjacent blocks.

- Only `a`s are pumped: the `b` and `c` counts stay `p`, and the `a` count changes.
- Only `b`s, or only `c`s: the same one-count mismatch.
- Both `a`s and `b`s: the `c` count stays `p`. At least one of the `a` and `b` counts changes, so it is no longer `p`.
- Both `b`s and `c`s: the `a` count stays `p`, and at least one of the other counts changes.

The string `u v^2 w x^2 y` is outside `L`. Every legal split fails, so `L` is not context-free. The same separation fact is what (B), (C), and (D) try to replace with conditions the lemma does not have.

### Q12

Answer: A

Assume `L` is regular and let `p` be a pumping length. The string `a^{p^2}` is in `L` and is long enough. A legal regular split has `y = a^k` with `1 ≤ k ≤ p`, because `|xy| ≤ p` and the alphabet is unary.

The string `xy^2 z` has length `p^2 + k`. The next square after `p^2` is

`(p+1)^2 = p^2 + 2p + 1`.

Since `1 ≤ k ≤ p`, one has `p^2 < p^2 + k ≤ p^2 + p < p^2 + 2p + 1`. The length `p^2 + k` sits strictly between two consecutive squares, so it is not a square. The pumped string is outside `L`.

That contradiction proves (A): the language is not regular. It does not prove (B). The regular pumping lemma has nothing to say about context-free languages beyond the fact that a non-regular language might or might not be context-free. The set of squares is infinite, and a pumping length is not required to be a square.
