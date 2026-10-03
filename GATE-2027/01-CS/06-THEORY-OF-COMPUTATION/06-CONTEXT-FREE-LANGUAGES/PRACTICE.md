# Context-Free Languages — Practice

Original GATE-style questions written for this repository. They are not previous-year questions. They do not repeat the questions in `../../14-PRACTICE-QUESTIONS/TOPIC-WISE/06-THEORY-OF-COMPUTATION/06-CONTEXT-FREE-LANGUAGES/practice.md`; do both sets.

Every membership claim below has an explicit grammar or a one-stack strategy; every non-membership claim names the two independent agreements or the crossed shape. Pumping quantifiers live in `07-PUMPING-LEMMA`.

Open the answer block only after attempting the question.

---

## Level 1 — Conceptual

### Q1 · MCQ

Which language is context-free but not regular?

- (A) `{ 0^{2n} | n ≥ 0 }`
- (B) `{ 0^n 1^n | n ≥ 0 }`
- (C) `{ 0^n 1^n 2^n | n ≥ 0 }`
- (D) `{ ww | w ∈ {0,1}* }`

<details><summary>Answer and solution</summary>

**Answer:** (B)

**Solution:** (B) is `S → 0S1 | ε`, not regular (the strings `0^n` are pairwise distinguishable). (A) is regular (`(00)*`). (C) and (D) are not CFL.

**Concept tested:** CFL − regular vs not-CFL.
**Difficulty:** Level 1
**Common trap:** (A) as a “copy”. Unary even length is regular.
</details>

### Q2 · MCQ

If `C1` and `C2` are CFL, which construction shows that `C1 C2` is CFL?

- (A) A new start production `S → S1 S2` after renaming variables apart
- (B) The product of two PDAs’ stacks
- (C) Complement then union
- (D) Intersection of the two grammars

<details><summary>Answer and solution</summary>

**Answer:** (A)

**Solution:** Concatenation of CFLs is the juxtaposition of the two start symbols. Two stacks are not a PDA. Complement is not a CFL operation. Intersection of two CFLs need not be CFL.

**Concept tested:** concat closure vs the failed intersection construction.
**Difficulty:** Level 1
**Common trap:** (B).
</details>

### Q3 · MCQ

Which grammar generates `{ 0^n 1^m 2^n | n, m ≥ 0 }`?

- (A) `S → 0 S 2 | T`, `T → 1 T | ε`
- (B) `S → 0 S 1 | 2`
- (C) `S → 0 S 1 S 2 | ε`
- (D) `S → 0 1 2 S | ε`

<details><summary>Answer and solution</summary>

**Answer:** (A)

**Solution:** The wrap `0 S 2` matches the outer pair; `T` is `1*`. (B) puts a `1` in the wrap and a single `2` in the middle. (C) ties three counts to the number of wraps. (D) generates `(012)*`.

**Concept tested:** one matching pair plus a free regular block.
**Difficulty:** Level 1
**Common trap:** (B).
</details>

### Q4 · NAT

The number of strings of length 3 in `{ 0^i 1^j | i > j ≥ 0 }` is ____.

<details><summary>Answer and solution</summary>

**Answer:** 2

**Solution:** Candidates of the form `0* 1*` and length 3: `000` (`3 > 0`), `001` (`2 > 1`), `011` (`1 > 2` false), `111` (`0 > 3` false). Two strings. Strings with a `1` before a `0` are not in `0* 1*`.

**Concept tested:** listing `a^i b^j` by length.
**Difficulty:** Level 1
**Common trap:** counting all 8 binary strings, or including `011`.
</details>

---

## Level 2 — Standard GATE

### Q5 · MSQ

CFL are closed under which operations? Select all that apply.

- (A) union
- (B) reversal
- (C) complement
- (D) intersection with a regular language

<details><summary>Answer and solution</summary>

**Answer:** (A), (B), (D)

**Solution:** Union is `S → S1 | S2`. Reverse the right-hand sides. PDA × DFA gives (D). Complement fails: otherwise De Morgan plus union would give intersection, and `{ 0^n 1^n 2^m } ∩ { 0^n 1^m 2^m } = { 0^n 1^n 2^n }` is not CFL.

**Concept tested:** closure table.
**Difficulty:** Level 2
**Common trap:** (C), or omitting (D) because “intersection is not closed”.
</details>

### Q6 · MCQ

Let `C` be CFL and `R` regular. Then `C ∩ R` is

- (A) always regular
- (B) always CFL, and not always regular
- (C) always finite
- (D) not always CFL

<details><summary>Answer and solution</summary>

**Answer:** (B)

**Solution:** Product construction. Not always regular: `{ 0^n 1^n } ∩ 0* 1* = { 0^n 1^n }`. Infinite, so not (C).

**Concept tested:** CFL ∩ regular.
**Difficulty:** Level 2
**Common trap:** (A).
</details>

### Q7 · MCQ

The reverse of `{ 0^n 1^{3n} | n ≥ 0 }` is

- (A) `{ 0^n 1^{3n} | n ≥ 0 }`
- (B) `{ 1^{3n} 0^n | n ≥ 0 }`
- (C) `{ 0^{3n} 1^n | n ≥ 0 }`
- (D) `{ 1^n 0^n 1^n | n ≥ 0 }`

<details><summary>Answer and solution</summary>

**Answer:** (B)

**Solution:** Reverse `0^n 1^n 1^n 1^n` to `1^{3n} 0^n`. Grammar `S → 1 1 1 S 0 | ε`. (C) swaps the counts the wrong way. (D) is not even two-block.

**Concept tested:** reverse of a CFL; letter order.
**Difficulty:** Level 2
**Common trap:** (C).
</details>

### Q8 · NAT

The number of even-length palindromes of length 4 over `{0,1}` is ____.

<details><summary>Answer and solution</summary>

**Answer:** 4

**Solution:** `{ ww^R : |w| = 2 }`. There are `2^2 = 4` choices of `w`: `0000`, `0110`, `1001`, `1111`.

**Concept tested:** `{ ww^R }` counting.
**Difficulty:** Level 2
**Common trap:** counting odd palindromes, or all 16 strings of length 4.
</details>

---

## Level 3 — Multi-Step

### Q9 · MCQ

Which statement is true?

- (A) If `L` and `complement(L)` are both CFL, then `L` is regular
- (B) Over `{0,1}`, `{ 0^n 1^n | n ≥ 0 }` and its complement are both CFL, and `{ 0^n 1^n }` is not regular
- (C) The complement of a non-regular CFL is never CFL
- (D) DCFL is not closed under complement

<details><summary>Answer and solution</summary>

**Answer:** (B)

**Solution:** Complement of `{ 0^n 1^n }` over `{0,1}` is `(0+1)* 10 (0+1)*` (not in `0*1*`) union `{ 0^i 1^j | i ≠ j }` (CFG with a more-0s arm and a more-1s arm). That union is CFL. So (A) and (C) fail. (D) is false: DCFL **is** closed under complement.

**Concept tested:** both a CFL and its complement can be CFL; DCFL vs CFL complement.
**Difficulty:** Level 3
**Common trap:** (A), the slogan copied from regular languages (or from DCFL, wrongly applied to CFL).
</details>

### Q10 · MSQ

`C1 = { 0^n 1^n 2^m | n, m ≥ 0 }`, `C2 = { 0^n 1^m 2^m | n, m ≥ 0 }`. Which statements are true? Select all that apply.

- (A) `C1` is CFL
- (B) `C2` is CFL
- (C) `C1 ∩ C2` is CFL
- (D) `C1 ∪ C2` is CFL

<details><summary>Answer and solution</summary>

**Answer:** (A), (B), (D)

**Solution:** (A) `S → T U`, `T → 0 T 1 | ε`, `U → 2 U | ε`. (B) symmetric. (D) union of CFLs. (C) is `{ 0^n 1^n 2^n }`, not CFL.

**Concept tested:** the standard intersection counter-example; union still CFL.
**Difficulty:** Level 3
**Common trap:** (C).
</details>

### Q11 · MCQ

Which language is context-free?

- (A) `{ 0^i 1^j 2^k | i = j and j = k }`
- (B) `{ 0^i 1^j 2^k | i = j or j = k }`
- (C) `{ ww | w ∈ {0,1}* }`
- (D) `{ 0^n 1^n 2^n 3^n | n ≥ 0 }`

<details><summary>Answer and solution</summary>

**Answer:** (B)

**Solution:** (B) is the union of two one-stack languages, hence CFL (and inherently ambiguous). (A) is `{ 0^n 1^n 2^n }`. (C) and (D) are not CFL.

**Concept tested:** `and` vs `or` on equalities.
**Difficulty:** Level 3
**Common trap:** (A), or rejecting (B) because it is inherently ambiguous.
</details>

---

## Level 4 — Tricky / Trap-Based

### Q12 · MCQ

Let `C` be CFL and `R` regular. Which is **always** CFL?

- (A) `R − C`
- (B) `C − R`
- (C) `complement(C)`
- (D) intersection of `C` with another CFL

<details><summary>Answer and solution</summary>

**Answer:** (B)

**Solution:** `C − R = C ∩ complement(R)` and `complement(R)` is regular, so the product applies. `R − C` includes `Σ* − C`. Complement of a CFL need not be CFL. Intersection of two CFLs need not be CFL.

**Concept tested:** CFL − regular vs regular − CFL.
**Difficulty:** Level 4
**Common trap:** (A), swapping the operands of `−`.
</details>

### Q13 · MSQ

`P` is regular, `Q` is CFL, and `Q ⊆ P`. Which are **always regular**? Select all that apply.

- (A) `P ∩ Q`
- (B) `P − Q`
- (C) `Σ* − P`
- (D) `Σ* − Q`

<details><summary>Answer and solution</summary>

**Answer:** (C)

**Solution:** `P ∩ Q = Q`, which need not be regular (`{ 0^n 1^n } ⊆ 0* 1*`). `P − Q` need not be regular (same pair). `Σ* − P` is the complement of a regular language. `Σ* − Q` is the complement of a CFL, not always regular.

**Concept tested:** 2011-shape subset trap; only the complement of `P`.
**Difficulty:** Level 4
**Common trap:** (A), “intersection with regular”.
</details>

### Q14 · MCQ

Which language is **not** context-free?

- (A) `{ 0^n 1^n 2^m 3^m | n, m ≥ 0 }`
- (B) `{ 0^n 1^m 2^m 3^n | n, m ≥ 0 }`
- (C) `{ 0^n 1^m 2^n 3^m | n, m ≥ 0 }`
- (D) `{ 0^n 1^m 2^n | n, m ≥ 0 }`

<details><summary>Answer and solution</summary>

**Answer:** (C)

**Solution:** (A) sequential pairs: concat of `{ 0^n 1^n }` and `{ 2^m 3^m }`. (B) nested: `S → 0 S 3 | T`, `T → 1 T 2 | ε`. (D) one pair plus free `1`s: `S → 0 S 2 | T`, `T → 1 T | ε`. (C) crossed: `0` with `2` and `1` with `3`. One stack cannot store both pairs in the required order. Pumping of `0^p 1^p 2^p 3^p` is in `07-PUMPING-LEMMA`.

**Concept tested:** sequential vs nested vs crossed, with a different letter order from the 14-PRACTICE four-block question (here the non-CFL is the only crossed one, and (D) is a three-block CFL).
**Difficulty:** Level 4
**Common trap:** (B) or (D).
</details>

---

## Level 5 — Challenge

### Q15 · MSQ

Over `{0,1,2}`, with `i, j ≥ 1`:

`L_A = { 0^i 1^{i+j} 2^j }`  
`L_B = { 0^i 1^i 2^{i+j} }`

Which statements are true? Select all that apply.

- (A) `L_A` is CFL
- (B) `L_B` is CFL
- (C) `L_A ∩ 0^+ 1^+ 2^+` is CFL
- (D) `L_A · 2*` is CFL

<details><summary>Answer and solution</summary>

**Answer:** (A), (C), (D)

**Solution:** `L_A = { 0^i 1^i 1^j 2^j | i, j ≥ 1 }`, sequential pairs. Grammar:

```
S → X Y
X → 0 X 1 | 01
Y → 1 Y 2 | 12
```

PDA: push on `0`, pop on the first block of `1`s, push on the remaining `1`s, pop on `2`s. One stack, two phases. So (A) holds.

`L_B` asks `#0 = #1` **and** `#2 ≥ #0 + 1`. After matching `0`s against `1`s the stack is empty, so the lower bound on `#2` still depends on the same `i`. That is two agreements on one count, not CFL. (Same shape as `{ a^m b^m c^{m+n} }`, different alphabet.) So (B) fails.

(C): `L_A` already lies in `0^+ 1^+ 2^+`, so the intersection is `L_A`, which is CFL.

(D): concatenation of a CFL with a regular language is CFL (`S → S_A T`, `T → 2 T | ε`).

**Concept tested:** 2025-shape pair with the **sum on the middle block** vs the sum on the last block; concat with regular.
**Difficulty:** Level 5
**Common trap:** swapping which of `L_A`, `L_B` is CFL; thinking leftover `2`s make `L_B` a regular tail.
</details>
