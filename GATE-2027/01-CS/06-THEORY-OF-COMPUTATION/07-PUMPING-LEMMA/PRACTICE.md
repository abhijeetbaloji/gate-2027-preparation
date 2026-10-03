# Pumping Lemma — Practice

Original GATE-style questions written for this repository. They are not previous-year questions. They do not repeat the questions in `../../14-PRACTICE-QUESTIONS/TOPIC-WISE/06-THEORY-OF-COMPUTATION/07-PUMPING-LEMMA/practice.md`; do both sets.

A pumping length of a regular language `L` is an integer `p ≥ 1` such that every `s ∈ L` with `|s| ≥ p` has some split `s = xyz` with `|xy| ≤ p`, `|y| ≥ 1`, and `xy^k z ∈ L` for every `k ≥ 0`. Open the answer block only after attempting the question.

---

## Level 1 — Conceptual

### Q1 · MCQ

In a proof that `L` is not regular, after you assume `L` is regular, **who chooses what**?

- (A) the lemma supplies a pumping length `p`; you pick one `s ∈ L` with `|s| ≥ p`; the lemma may then pick any split with `|xy| ≤ p` and `|y| ≥ 1`; you pick a `k` that leaves `L`
- (B) you pick `p` first, then the lemma must accept whatever split you like, including `|xy| > p`
- (C) you pick `k`, then `p`, then a string of length 1
- (D) the lemma supplies both `p` and a string shorter than `p`

<details><summary>Answer and solution</summary>

**Answer:** (A)

**Solution:** Quantifiers in order: ∃ `p` (lemma), ∀ long `s` (you choose one), ∃ legal split (adversary), ∀ `k` (you choose a bad `k`). Because the split is existential, your write-up must work for every legal `xyz`. (B) reverses the window. (C) and (D) ignore `|s| ≥ p`.

**Concept tested:** who owns each quantifier in a non-regularity proof.
**Difficulty:** Level 1
**Common trap:** picking the split yourself and ignoring the other legal `y`s.
</details>

### Q2 · MCQ

The regular pumping lemma requires `|xy| ≤ p` because

- (A) a DFA with `p` states, reading a prefix of length `p`, visits `p + 1` states, so a nonempty cycle already occurs inside that prefix
- (B) `y` must contain every alphabet symbol
- (C) otherwise `k = 0` would be forbidden
- (D) the lemma applies only to strings of length exactly `p`

<details><summary>Answer and solution</summary>

**Answer:** (A)

**Solution:** Pigeonhole on the first `p + 1` states of the run. The repeated state gives a cycle `y` with `|xy| ≤ p` and `|y| ≥ 1`. Pumping is walking that cycle. (B) and (D) are not in the lemma. (C) confuses the two bounds: `k = 0` is allowed; `|y| ≥ 1` is what makes deletion change the string.

**Concept tested:** why the window is a prefix of length `p`.
**Difficulty:** Level 1
**Common trap:** treating `|xy| ≤ p` as an arbitrary bound with no DFA meaning.
</details>

### Q3 · MCQ

Suppose `L` is **not** regular. Which statement is true?

- (A) `L` cannot be context-free
- (B) `L` might still be context-free
- (C) `L` has finitely many Myhill–Nerode classes
- (D) every infinite subset of `L` fails to be regular, and that is why pumping applies

<details><summary>Answer and solution</summary>

**Answer:** (B)

**Solution:** `{a^n b^n}` and `{a^n b^{2n}`} are the standard witnesses: regular pumping (or MN) kills regularity, while an obvious CFG remains. (A) is the promotion this question exists to block. (C) is the opposite of Myhill–Nerode. (D) is false: `{a^n b^n | n ≥ 0} ∪ a*` is not regular and still contains the infinite regular subset `a*`. Pumping is applied to `L` itself, not to its subsets.

**Concept tested:** not-regular versus not-CFL; pumping is only the weaker conclusion.
**Difficulty:** Level 1
**Common trap:** (A) — treating the regular lemma as a CFL test.
</details>

---

## Level 2 — Standard GATE

### Q4 · MCQ

Let `L = { a^n b a^n | n ≥ 0 }` and let `p` be a pumping length. For `s = a^p b a^p` and a legal split `s = xyz`, the string `xy^0 z` is

- (A) `a^{p−t} b a^p` for some `t` with `1 ≤ t ≤ p`, which is not in `L`
- (B) `a^p b a^{p−t}`, because `y` can sit in the second `a`-block
- (C) `a^p a^p`, because `y` must be the centre `b`
- (D) outside the reach of the lemma, because `|s| = 2p + 1` may be less than `p`

<details><summary>Answer and solution</summary>

**Answer:** (A)

**Solution:** `|s| = 2p + 1 ≥ p`. The prefix of length `p` is `a^p`, so `|xy| ≤ p` plants `y` entirely in the first `a`-block: `y = a^t`, `1 ≤ t ≤ p`. Deletion yields `a^{p−t} b a^p`, whose two `a`-blocks differ. (B) would require `|xy| ≥ p + 1`. (C): the centre `b` is at position `p + 1`, past the window. (D) is arithmetic nonsense.

**Concept tested:** `|xy| ≤ p` forces `y` into the first block of a marked copy.
**Difficulty:** Level 2
**Common trap:** (B) — treating the two `a`-blocks symmetrically.
</details>

### Q5 · NAT

The smallest pumping length of the regular language `(aba)*` is ____.

<details><summary>Answer and solution</summary>

**Answer:** 3

**Solution:** The nonempty members are concatenations of the block `aba`. For `p = 1` or `p = 2` the word `aba` is long enough. Every split with `|xy| ≤ 2` and `|y| ≥ 1` pumps to a string whose length is not a multiple of 3, or to `ba` / `aa` / `abba`, none of which is `(aba)*`. For `p = 3`, take `y` to be the first block `aba` of any nonempty member; pumping that block stays in the language, and `ε` is shorter than 3. So 1 and 2 fail, 3 works.

**Concept tested:** smallest pumping length of a block language.
**Difficulty:** Level 2
**Common trap:** answering 1 because “any nonempty string can pump one letter”.
</details>

### Q6 · MSQ

Which statements are true of pumping lengths?

- (A) if `p` is a pumping length of `L`, then so is `p + 2`
- (B) the number of states of the minimal DFA of `L` is always the smallest pumping length of `L`
- (C) the number of states of **some** DFA for `L` is a pumping length of `L`
- (D) `1` is a pumping length of every infinite regular language

<details><summary>Answer and solution</summary>

**Answer:** (A), (C)

**Solution:** (A): a string of length ≥ `p + 2` already has a split with `|xy| ≤ p`, which also satisfies `|xy| ≤ p + 2`. (C) is the pigeonhole proof. (B) fails for `(aa+bb)*`: smallest `p = 2`, min DFA has 4 states. (D) fails for the same language: `aa` cannot be pumped inside a window of size 1.

**Concept tested:** `q > p` fact; min DFA vs smallest `p`.
**Difficulty:** Level 2
**Common trap:** (B) as “the lemma says `p` equals the number of states”.
</details>

---

## Level 3 — Multi-step reasoning / construction

### Q7 · MCQ

Which statement is correct?

- (A) `{ a^n b^n | n ≥ 0 }` is not context-free
- (B) `{ a^n b^{2n} | n ≥ 0 }` is regular
- (C) `{ a^n b^n c^n | n ≥ 0 }` is context-free but not regular
- (D) `{ a^n b^n | n ≥ 0 }` is context-free but not regular

<details><summary>Answer and solution</summary>

**Answer:** (D)

**Solution:** `S → aSb | ε` generates `{a^n b^n}`. Regular pumping (or MN) shows it is not regular. (A) contradicts that grammar. (B): `{a^n b^{2n}}` is CFL (`S → aSbb | ε`) but not regular. (C): `{a^n b^n c^n}` fails CFL pumping (Section 7 of the notes), so it is not context-free.

**Concept tested:** two lemmas, two conclusions.
**Difficulty:** Level 3
**Common trap:** (C) — stopping after “not regular”.
</details>

### Q8 · MCQ

In the context-free pumping lemma the pieces `v` and `x`

- (A) are pumped independently, and the bound is `|uv| ≤ p`
- (B) are pumped together, at least one is nonempty, and the bound is `|vwx| ≤ p`
- (C) must both be nonempty
- (D) must each contain a single alphabet symbol

<details><summary>Answer and solution</summary>

**Answer:** (B)

**Solution:** The pumped string is `u v^k w x^k y`. The condition is `|vx| ≥ 1`, so one of `v, x` may be `ε`. The local window is `vwx`. (A) copies the regular lemma onto the wrong split. (C) and (D) add constraints the lemma does not have.

**Concept tested:** CFL split conditions.
**Difficulty:** Level 3
**Common trap:** (A) — `|xy| ≤ p` reused as `|uv| ≤ p`.
</details>

### Q9 · MSQ

Which arguments are **invalid** as proofs that `{ a^n b^n | n ≥ 0 }` is not regular? Select all that apply.

- (A) “Take `s = a^3 b^3` and pump, even if the unknown `p` is larger than 3.”
- (B) “The split that sets `y` to the first `b` of `a^p b^p` fails, therefore the language is not regular.”
- (C) “`a*` is infinite, and every infinite language fails the pumping lemma.”
- (D) “For `s = a^p b^p`, every legal `y` is `a^t` with `1 ≤ t ≤ p`, and `xy^0 z ∉ L` for every such `t`.”

<details><summary>Answer and solution</summary>

**Answer:** (A), (B), (C)

**Solution:** (A) uses a string that may be shorter than `p`. (B) uses a split the lemma need not give (`|xy|` can exceed `p`). (C) is false (`a*` is regular and infinite). (D) is the valid proof: the length bound forces the shape of `y`, and every such `y` is killed.

**Concept tested:** illegal splits, short strings, infiniteness.
**Difficulty:** Level 3
**Common trap:** thinking (B) is valid because that split does fail — it is not a *legal* split the adversary must provide.
</details>

---

## Level 4 — Tricky / trap-based

### Q10 · MCQ

Let `L = { w # w | w ∈ {a, b}* }` with `#` a fresh symbol. A correct first step in proving that `L` is not regular is

- (A) intersecting `L` with the regular language `a* # a*`, obtaining `{ a^n # a^n | n ≥ 0 }`, then pumping (or using Myhill–Nerode)
- (B) pumping the string `#`, which has length 1
- (C) concluding that `L` is regular because it is the concatenation `Σ* # Σ*`
- (D) applying the CFL pumping lemma and stopping as soon as one split of `a^p # a^p` fails

<details><summary>Answer and solution</summary>

**Answer:** (A)

**Solution:** Regular ∩ regular = regular, so a non-regular slice infects `L`. The slice `{a^n # a^n}` is the marked copy of a unary string; `a^i` is distinguished from `a^j` by `# a^i`. (B) does not meet `|s| ≥ p` for unknown `p`. (C) is the unmarked concatenation, a different (regular) language. (D) mixes lemmas and checks one split.

**Concept tested:** intersect with regular before pumping a copy language.
**Difficulty:** Level 4
**Common trap:** (C) — dropping the requirement that the two sides be equal.
</details>

### Q11 · NAT

The smallest pumping length of `{ a^{2k+1} | k ≥ 0 }` is ____.

<details><summary>Answer and solution</summary>

**Answer:** 2

**Solution:** The language is the odd-length unary strings. For `p = 1` the word `a` must be pumped: the only legal split has `y = a`, and both `k = 0` (`ε`) and `k = 2` (`aa`) leave the language. For `p = 2` the word `a` is exempt. The next member `aaa` has the split `x = ε`, `y = aa`, `z = a`; pumping by 2 keeps the length odd. Every longer odd word has the same split inside the first two letters. So 1 fails and 2 works.

**Concept tested:** smallest pumping length of a unary parity language.
**Difficulty:** Level 4
**Common trap:** answering 1 because the min DFA has 2 states and “odd starts at length 1”.
</details>

### Q12 · MCQ

Let `L = { a^{n!} | n ≥ 0 }`. Assume a pumping length `p`, choose `n ≥ max(2, p)`, and take `s = a^{n!}`. A legal `y` has length `t` with `1 ≤ t ≤ p`. The string `xy^2 z` has length `n! + t`. This shows `L` is not regular because

- (A) `n! < n! + t < (n+1)!`
- (B) `n! + t` is always even
- (C) `L` is finite
- (D) the same argument proves that `L` is not context-free

<details><summary>Answer and solution</summary>

**Answer:** (A)

**Solution:** `(n+1)! = (n+1) n!`. For `n ≥ 2` one has `n! + t ≤ n! + n! = 2 n! < (n+1) n!`. The pumped length sits strictly between two consecutive factorials, so it is not a factorial. (B) is irrelevant. (C) is false. (D): regular pumping has no CFL conclusion.

**Concept tested:** length-gap pumping for `{a^{n!}}`.
**Difficulty:** Level 4
**Common trap:** (D) — using a regular lemma to kill CFL-ness.
</details>

### Q13 · MSQ

Which of the following integers are pumping lengths for `(aba)*`? Select all that apply.

- (A) `1`
- (B) `2`
- (C) `3`
- (D) `5`

<details><summary>Answer and solution</summary>

**Answer:** (C), (D)

**Solution:** Q5 shows that 3 is a pumping length and that 1 and 2 are not. Q6(A) then gives 5. Directly: every nonempty member begins with `aba`, and pumping that block is legal as soon as `|xy|` is allowed to be 3, hence as soon as `p ≥ 3`.

**Concept tested:** smallest `p` plus the `q > p` closure.
**Difficulty:** Level 4
**Common trap:** rejecting 5 because it is not a multiple of 3.
</details>

---

## Level 5 — Challenge

### Q14 · MCQ

After a legal regular split of `s = a^p b^p ∈ { a^n b^n | n ≥ 0 }`, the reason `k = 0` is the cheapest contradiction is

- (A) `xy^0 z` has fewer `a`s than `b`s, and the lemma allows deletion
- (B) the lemma forbids `k ≥ 2`
- (C) `y` must contain the letter `b`
- (D) `xy^0 z` has length less than `p`, so it is exempt from the lemma and therefore outside `L`

<details><summary>Answer and solution</summary>

**Answer:** (A)

**Solution:** `y = a^t` with `t ≥ 1`, so deletion yields `a^{p−t} b^p`. The lemma explicitly includes `k = 0`. (B) is backwards. (C) contradicts `|xy| ≤ p`. (D) confuses “the lemma does not *force* short strings to pump” with “short strings cannot belong to `L`”. Membership of `xy^0 z` is decided by the count, not by the lemma’s hypothesis.

**Concept tested:** deletion as a legal pump; what “short” does and does not mean.
**Difficulty:** Level 5
**Common trap:** (D) — declaring every string shorter than `p` to be outside `L`.
</details>

### Q15 · MCQ

Let `s = 0^p 1^p 0^p` and `s = uvwxy` with `|vwx| ≤ p`. The window `vwx` cannot contain a `0` from **both** `0`-blocks because

- (A) the two `0`-blocks are separated by `p` letters `1`, and a window of length at most `p` cannot cover that separation
- (B) the CFL lemma allows only one alphabet symbol in `vwx`
- (C) `v` and `x` are required to be equal
- (D) `p` must be even

<details><summary>Answer and solution</summary>

**Answer:** (A)

**Solution:** Any substring that contains a `0` from the first block and a `0` from the third block includes the entire `1^p` in between, hence has length at least `p + 2`. This is the same geometry as `a^p b^p c^p`. Pumping therefore cannot restore all three block lengths at once, so `{ 0^n 1^n 0^n | n ≥ 0 }` is not context-free. (B)–(D) are not conditions of the lemma.

**Concept tested:** CFL window on two copies of the same letter separated by a `p`-block.
**Difficulty:** Level 5
**Common trap:** thinking the argument needs three *distinct* letters.
</details>

### Q16 · MCQ

Which of the following **can** prove that a language `L` is regular?

- (A) exhibiting a pumping length of `L`
- (B) showing that `L` has finitely many Myhill–Nerode classes
- (C) showing that `L` fails the context-free pumping lemma
- (D) showing that `L` is infinite

<details><summary>Answer and solution</summary>

**Answer:** (B)

**Solution:** Myhill–Nerode is an if and only if: finite index ⇔ regular, and the classes are the min-DFA states. (A) is a necessary condition. (C) proves `L` is not even context-free. (D) is compatible with `a*`. To prove regularity you may also give a DFA, an NFA, an RE, or a right-linear grammar; pumping is not among those proofs.

**Concept tested:** MN versus pumping as regularity tests.
**Difficulty:** Level 5
**Common trap:** (A) — the 2019-style question asks which `p` *can* be a pumping length of a language already known to be regular; that is not a proof of regularity.
</details>
