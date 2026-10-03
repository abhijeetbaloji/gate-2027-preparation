# Regular Languages — Practice

Original GATE-style questions written for this repository. They are not previous-year questions. They do not repeat the questions in `../../14-PRACTICE-QUESTIONS/TOPIC-WISE/06-THEORY-OF-COMPUTATION/05-REGULAR-LANGUAGES/practice.md`; do both sets.

Conventions: `+` is union in regular expressions; juxtaposition is concatenation; `*` is Kleene star. Min-DFA counts are for complete DFAs over the stated alphabet. Every numerical answer below was checked by listing classes or counting strings.

Open the answer block only after attempting the question.

---

## Level 1 — Conceptual

### Q1 · MCQ

Which language is regular?

- (A) `{ a^n b^n | n ≥ 0 }`
- (B) `{ a^n b^m c^k | n, m, k ≥ 0 }`
- (C) `{ ww^R | w ∈ {a, b}* }`
- (D) `{ a^n b^{2n} | n ≥ 0 }`

<details><summary>Answer and solution</summary>

**Answer:** (B)

**Solution:** (B) is `a*b*c*`: three independent exponents, a 4-state DFA (which block, plus a sink for a late `a` or `b`). (A) equates two unbounded counts. (D) equates `#b = 2 #a`; it is context-free (`S → aSbb | ε`) but not regular. (C) is the even-length palindromes.

**Concept tested:** independent exponents versus equal counts / copies.
**Difficulty:** Level 1
**Common trap:** marking (D) regular because the `2` is a constant.
</details>

### Q2 · MCQ

Let `L` be a finite language. Which statement is **false**?

- (A) `L` is regular
- (B) every subset of `L` is regular
- (C) `L*` is regular
- (D) `{ ww | w ∈ L }` is necessarily non-regular

<details><summary>Answer and solution</summary>

**Answer:** (D)

**Solution:** Finite ⇒ regular, so (A) holds, every subset of a finite set is finite hence regular, and the star of a regular language is regular. `{ ww | w ∈ L }` has at most `|L|` strings, so it is finite, hence regular. The usual non-regular `ww` example needs an infinite `L` with mixed letters.

**Concept tested:** finite ⇒ regular, including finite copies.
**Difficulty:** Level 1
**Common trap:** importing “`ww` is never regular” without checking finiteness.
</details>

### Q3 · NAT

Over `{0, 1}`, the number of strings of length exactly 4 with an odd number of `0`s is ____.

<details><summary>Answer and solution</summary>

**Answer:** 8

**Solution:** Odd number of `0`s in 4 bits: `C(4, 1) + C(4, 3) = 4 + 4 = 8`. Equivalently half of `2^4`, because the parity-of-`0` DFA splits `{0, 1}^4` evenly.

**Concept tested:** a modular count is regular; counting its slice.
**Difficulty:** Level 1
**Common trap:** `C(4, 1) = 4` only (exactly one `0`, missing three).
</details>

### Q4 · MCQ

Let `L` be regular over `Σ`. Which language is **always** regular?

- (A) `{ ww^R | w ∈ L }`
- (B) `{ w#w | w ∈ L }` over `Σ ∪ {#}`
- (C) `Suffix(L) = { y | ∃ x, xy ∈ L }`
- (D) `{ a^n b^n | n ≥ 0 and a^n b^n ∈ L }`

<details><summary>Answer and solution</summary>

**Answer:** (C)

**Solution:** Suffixes of a regular language are regular (reverse, take prefixes, reverse). (A) fails for `L = {a, b}*`. (B) is a marked copy; already for `L = a*` it is `{ a^n # a^n }`, not regular. (D) can be all of `{a^n b^n}` (take `L = a*b*`).

**Concept tested:** suffix closure versus copy operations.
**Difficulty:** Level 1
**Common trap:** treating (A) as `L · L^R`, which *is* regular.
</details>

---

## Level 2 — Standard GATE

### Q5 · MSQ

Which languages are regular?

- (A) `{ w ∈ {a, b}* | #_a(w) ≡ 1 (mod 4) }`
- (B) `{ w ∈ {a, b}* | #_a(w) = 2 · #_b(w) }`
- (C) `{ a^n b^m | n, m ≥ 0 and n + m ≥ 3 }`
- (D) `{ a^n b^n a^n | n ≥ 0 }`

<details><summary>Answer and solution</summary>

**Answer:** (A), (C)

**Solution:** (A) is a 4-state cycle on `a`, with `b` as a self-loop. (C) is `a*b*` minus the finite set `{ ε, a, b, aa, ab, bb }`, hence regular. (B) equates two counts (intersect with `a*b*` to get `{ a^{2k} b^k }`). (D) has two equalities; it is not even context-free.

**Concept tested:** modular vs equal counts; finite difference from `a*b*`.
**Difficulty:** Level 2
**Common trap:** rejecting (C) because of the `≥ 3` constraint.
</details>

### Q6 · MCQ

Let `L = { a^n b^m | n, m ≥ 0 and n is even }`. The reverse `L^R` is

- (A) `a* b*`
- (B) `b* (aa)*`
- (C) `(aa)* b*`
- (D) `{ b^n a^n | n even }`

<details><summary>Answer and solution</summary>

**Answer:** (B)

**Solution:** A typical member `a^{2k} b^m` reverses to `b^m a^{2k}`. As `m` and `k` vary independently this is `b* (aa)*`. Reverse preserves regularity; it does not introduce an equality of exponents. (C) is `L` itself. (A) includes `ba` reversed from a string with an odd number of `a`s. (D) is not regular and is not the reverse.

**Concept tested:** reverse of `a*b*`-like languages.
**Difficulty:** Level 2
**Common trap:** (D) — reversing as if it equated the counts.
</details>

### Q7 · NAT

The number of states in the minimal complete DFA over `{a, b}` for `{ w | w ends with aba }` is ____.

<details><summary>Answer and solution</summary>

**Answer:** 4

**Solution:** States are the longest prefix of `aba` that is a suffix of the string so far: `ε`, `a`, `ab`, `aba` (accept). Transitions: `ε -a→ a -b→ ab -a→ aba`; `ε -b→ ε`; `a -a→ a`; `ab -b→ ε`; `aba -a→ a` (string `abaa` ends with `a`); `aba -b→ ab` (`abab` ends with `ab`). All four are reachable. Only `aba` accepts. Continuation `a` separates `ab` from `ε` and from `a`; continuation `ba` separates `a` from `ε`.

**Concept tested:** min DFA for “ends with `w`”; overlap of `aba`.
**Difficulty:** Level 2
**Common trap:** 3 states (dropping the overlap `aba -a→ a`) or 5 (splitting “ends with `ba`” from `ab`).
</details>

### Q8 · MCQ

Let `L1` and `L2` be regular over `Σ`, and let `#` be a fresh symbol. Which language is **not** necessarily regular?

- (A) the right quotient `{ x | ∃ y ∈ L2, xy ∈ L1 }`
- (B) `h(L1)` for a homomorphism `h`
- (C) `{ x # x | x ∈ L1 }` over `Σ ∪ {#}`
- (D) `L1 ∩ L2`

<details><summary>Answer and solution</summary>

**Answer:** (C)

**Solution:** Regular languages are closed under quotient by a regular language, homomorphism, and intersection. (C) is a marked copy. For `L1 = a*` it is `{ a^n # a^n }`, not regular.

**Concept tested:** operations that stay inside the family versus copy.
**Difficulty:** Level 2
**Common trap:** (A) looks exotic; quotient by a regular language *is* regular.
</details>

---

## Level 3 — Multi-step reasoning / construction

### Q9 · MSQ

Let `L` be regular over `{a, b}`. Which languages are always regular?

- (A) `Suffix(L)`
- (B) `{ ww^R | w ∈ L }`
- (C) `L · L^R`
- (D) `Prefix(L)`

<details><summary>Answer and solution</summary>

**Answer:** (A), (C), (D)

**Solution:** Prefix: make accepting every DFA state that can reach an original accept. Suffix: reverse, prefix, reverse. `L^R` is regular, concatenation preserves regularity, so `L · L^R` is regular. (B) requires the two halves to be the reverse of *the same* `w`. For `L = {a, b}*` this is not regular.

**Concept tested:** prefix/suffix/`L L^R` versus `{ww^R}`.
**Difficulty:** Level 3
**Common trap:** marking (C) false because it looks like (B).
</details>

### Q10 · NAT

The number of Myhill–Nerode classes of `{ w ∈ {a, b}* | w contains at least two a's }` is ____.

<details><summary>Answer and solution</summary>

**Answer:** 3

**Solution:** A complete DFA counts `a`s up to 2, with `b` as a self-loop: `0`, `1`, `≥ 2` (accept). They are pairwise distinguishable: `ε` separates `≥ 2` from the others; `a` separates `1` from `0` (`a` from `1` is accepted, `a` from `0` is not). So the index is 3.

**Concept tested:** MN index = min-DFA size for a threshold count.
**Difficulty:** Level 3
**Common trap:** 4, by splitting “exactly two” from “three or more” — both accept every continuation.
</details>

### Q11 · MSQ

Which statements hold for **every** non-regular language `L` over `Σ`?

- (A) `Σ* − L` is non-regular
- (B) `L ∪ Σ*` is regular
- (C) some finite subset of `L` is non-regular
- (D) `L` has infinitely many Myhill–Nerode classes

<details><summary>Answer and solution</summary>

**Answer:** (A), (B), (D)

**Solution:** (A) is complement-closure in both directions. (B): `L ∪ Σ* = Σ*`. (D) is Myhill–Nerode. (C) is false: every finite set is regular.

**Concept tested:** complement, swallowing union, MN, finite ⇒ regular.
**Difficulty:** Level 3
**Common trap:** rejecting (B) because “union with a non-regular language stays non-regular”.
</details>

### Q12 · NAT

The number of states in the minimal complete DFA over `{a, b}` for `a*b*` is ____.

<details><summary>Answer and solution</summary>

**Answer:** 3

**Solution:** States: still in the `a`-block (start, accept); moved to the `b`-block (accept); saw a late `a` (reject sink). `ε` separates the two accepts from the sink. Continuation `a` is accepted from the `a`-block and rejected from the `b`-block. No fourth class: after a `b` has been seen, all such strings share continuations.

**Concept tested:** `a*b*` DFA, including the reachable sink.
**Difficulty:** Level 3
**Common trap:** 2, by leaving the sink incomplete; 4, by splitting “empty” from “some `a`s”.
</details>

---

## Level 4 — Tricky / trap-based

### Q13 · MCQ

Which language is regular?

- (A) `{ αβα | α ∈ {a, b}+, β ∈ {a, b}+ }`
- (B) `{ αβα | α ∈ {b}+, β ∈ {a, b}+ }`
- (C) `{ αα | α ∈ {a, b}+ }`
- (D) `{ a^n b a^n | n ≥ 1 }`

<details><summary>Answer and solution</summary>

**Answer:** (B)

**Solution:** In (B) the shortest legal `α` is `b`. Every string that starts and ends with `b` and has length at least 3 is `b x b` with `|x| ≥ 1`, hence in the language. So (B) equals `b(a+b)+b`, which is regular. (A) is a mixed copy: its intersection with `ab*ab*` is `{ ab^i ab^j | i > j }`, not regular. (C) is `{ ww | |w| ≥ 1 }`. (D) is distinguished by the prefixes `a^i`.

**Concept tested:** unary-`α` collapse versus mixed copy.
**Difficulty:** Level 4
**Common trap:** marking (B) non-regular because it is written as `αβα`.
</details>

### Q14 · MSQ

Which statements are true?

- (A) an infinite union of regular languages need not be regular
- (B) if `L1 ∪ L2` is regular, then both `L1` and `L2` are regular
- (C) every finite language is regular
- (D) regular languages are closed under complement

<details><summary>Answer and solution</summary>

**Answer:** (A), (C), (D)

**Solution:** (A): `⋃_n {a^n b^n}`. (B) fails for `{a^n b^n} ∪ {a, b}*`. (C) and (D) are the two closure facts that make “finite subset of a non-regular set” and “complement of a non-regular set” immediate.

**Concept tested:** finite vs infinite union; cancelling a union operand.
**Difficulty:** Level 4
**Common trap:** (B) as the converse of closure under union.
</details>

### Q15 · NAT

The number of Myhill–Nerode classes of the even-length language `{ w ∈ {a, b}* | |w| is even }` is ____.

<details><summary>Answer and solution</summary>

**Answer:** 2

**Solution:** All even-length strings are equivalent (one more symbol makes them odd, two make them even). All odd-length strings are equivalent. `ε` separates the two classes. The min DFA is the 2-state parity machine; both states are reachable.

**Concept tested:** MN for a length-parity language.
**Difficulty:** Level 4
**Common trap:** `2^n` or “infinitely many, one per length”.
</details>

### Q16 · MCQ

Which argument correctly shows that `{ a^n b^m | n ≠ m }` is **not** regular?

- (A) the language is infinite
- (B) `a*b*` is regular, and `a*b* − { a^n b^m | n ≠ m } = { a^n b^n | n ≥ 0 }`, which is not regular
- (C) `aabb` belongs to the language
- (D) regular languages are closed under complement, and this language is the complement of `a*b*`

<details><summary>Answer and solution</summary>

**Answer:** (B)

**Solution:** Difference of regular languages is regular, so if the unequal-count language were regular, `{a^n b^n}` would be too. (A) does not obstruct regularity (`a*` is infinite). (C) is one membership fact. (D) is false: the complement of `a*b*` also contains every string with a `ba` substring.

**Concept tested:** `n ≠ m` via difference from `a*b*`.
**Difficulty:** Level 4
**Common trap:** (D) — complement taken relative to `Σ*` instead of `a*b*`.
</details>

---

## Level 5 — Challenge

### Q17 · MCQ

Which statement is true?

- (A) every left-linear grammar is LL(1)
- (B) some regular language has no context-free grammar
- (C) every regular language is generated by some LR(1) grammar
- (D) a grammar that uses both a left-linear production and a right-linear production always generates a regular language

<details><summary>Answer and solution</summary>

**Answer:** (C)

**Solution:** Every regular language is a deterministic CFL (run the DFA and ignore the stack), and every DCFL has an LR(1) grammar. (A) fails because a left-linear grammar is typically left-recursive (`S → S0 | 1`), and left recursion forbids LL(1). (B) fails because regular ⊂ CFL. (D) fails: `S → aB`, `B → Sb | b` generates `{a^n b^n}`.

**Concept tested:** regular grammars vs LL(1) / LR(1); mixed linearity.
**Difficulty:** Level 5
**Common trap:** swapping “regular grammar” with “regular language” in (A) versus (C).
</details>

### Q18 · NAT

The number of states in the minimal complete DFA over `{a, b}` for

`{ w | #_a(w) is even and #_b(w) ≡ 0 (mod 3) }`

is ____.

<details><summary>Answer and solution</summary>

**Answer:** 6

**Solution:** Product of a 2-cycle on `a` and a 3-cycle on `b`: states `(p, q)` with `p ∈ {0, 1}`, `q ∈ {0, 1, 2}`. All six are reachable: `ε, a, b, bb, ab, abb`. Only `(0, 0)` accepts, so `ε` separates it from the other five. The five rejecting states are pairwise distinguished by a short continuation that lands in `(0, 0)` from one and not the other (`a` or `b` or `bb` as needed). So the index is 6.

**Concept tested:** product DFA for two independent modular counts.
**Difficulty:** Level 5
**Common trap:** 5, by merging two rejecting residues that still have different continuations; 12, by tracking length as well.
</details>
