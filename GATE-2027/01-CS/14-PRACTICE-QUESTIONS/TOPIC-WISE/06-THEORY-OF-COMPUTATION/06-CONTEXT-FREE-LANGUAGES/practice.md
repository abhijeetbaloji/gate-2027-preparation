# Context-Free Languages — Practice Questions

Original practice for GATE CS. These questions are not from any GATE paper. Attempt the questions before reading the solutions.

Context-free languages are exactly the languages of context-free grammars and exactly the languages of nondeterministic push-down automata. The empty string is `ε`.

## Level 1 — Conceptual

## Q1 — MCQ

Which language is context-free but not regular?

A. `a*b*`  
B. `{a^n b^n | n ≥ 0}`  
C. `{a^n b^n c^n | n ≥ 0}`  
D. `{ww | w ∈ {a, b}*}`

---

## Q2 — MCQ

If `L1` and `L2` are context-free, which construction shows that `L1 ∪ L2` is context-free?

A. A new start symbol `S` with productions `S → S1 | S2`, where `S1` and `S2` are the old start symbols  
B. The intersection of the two grammars  
C. The complement of a regular language  
D. A product of two minimal DFAs

---

## Q3 — MCQ

Which grammar generates `{a^n b^n c^m | n, m ≥ 0}`?

A. `S → T C`, `T → aTb | ε`, `C → cC | ε`  
B. `S → aSb | c`  
C. `S → aS | bS | cS | ε`  
D. `S → aSbSc | ε`

---

## Q4 — NAT

The number of strings of length 4 in `{a^i b^j | i ≠ j}` is ____.

---

## Level 2 — Standard GATE Style

## Q5 — MSQ

Context-free languages are closed under which operations? Select all that apply.

A. union  
B. concatenation  
C. Kleene star  
D. intersection

---

## Q6 — MCQ

Let `L` be context-free and let `R` be regular. Then `L ∩ R` is

A. always regular  
B. always context-free, and not always regular  
C. never context-free  
D. always finite

---

## Q7 — MCQ

The reverse of a context-free language is context-free. The reverse of `{a^n b^{2n} | n ≥ 0}` is

A. `{a^n b^{2n} | n ≥ 0}`  
B. `{b^{2n} a^n | n ≥ 0}`  
C. `{a^{2n} b^n | n ≥ 0}`  
D. `{a^n b^n a^n | n ≥ 0}`

---

## Q8 — NAT

The number of strings of length 5 in `{w c w^R | w ∈ {a, b}*}` is ____.

---

## Level 3 — Multi-Step

## Q9 — MCQ

Which statement is true?

A. If both `L` and its complement are context-free, then `L` is regular  
B. Over `{a, b}`, both `{a^n b^n | n ≥ 0}` and its complement are context-free, and `{a^n b^n | n ≥ 0}` is not regular  
C. The complement of a non-regular language is never context-free  
D. Context-free languages are closed under complement

---

## Q10 — MSQ

Let `L1 = {a^n b^n c^m | n, m ≥ 0}` and `L2 = {a^n b^m c^m | n, m ≥ 0}`. Which statements are true? Select all that apply.

A. `L1` is context-free  
B. `L2` is context-free  
C. `L1 ∩ L2` is context-free  
D. `L1 ∪ L2` is context-free

---

## Q11 — MCQ

Which language is context-free?

A. `{a^i b^j c^k | i = j and j = k}`  
B. `{a^i b^j c^k | i = j or j = k}`  
C. `{ww | w ∈ {a, b}*}`  
D. `{a^n b^n c^n d^n | n ≥ 0}`

---

## Level 4 — Tricky / Trap-Based

## Q12 — MCQ

Which statement is true?

A. The intersection of a context-free language with a regular language is always regular  
B. The intersection of a context-free language with a regular language is always context-free  
C. Context-free languages are closed under complement  
D. Context-free languages are closed under intersection

---

## Q13 — MSQ

Which statements are true? Select all that apply.

A. Context-free languages are closed under union  
B. Context-free languages are not closed under intersection  
C. Context-free languages are not closed under complement  
D. If `L` is context-free and `R` is regular, then `L ∩ R` is always regular

---

## Q14 — MCQ

Which language is context-free?

A. the complement of `{a^n b^n | n ≥ 0}` over the alphabet `{a, b}`  
B. `{a^n b^n c^n | n ≥ 0}`  
C. `{ww | w ∈ {a, b}*}`  
D. `{a^n b^m c^n d^m | n, m ≥ 0}`

---

## Level 5 — Challenge

## Q15 — MSQ

Which languages are context-free? Select all that apply.

A. `{a^n b^n c^m d^m | n, m ≥ 0}`  
B. `{a^n b^m c^m d^n | n, m ≥ 0}`  
C. `{a^n b^m c^n d^m | n, m ≥ 0}`  
D. `{a^n b^n c^m | n, m ≥ 0}`

---

## Q16 — MCQ

Which statement is false?

A. `{a^n b^n c^m d^m | n, m ≥ 0}` is context-free  
B. `{a^n b^m c^m d^n | n, m ≥ 0}` is context-free  
C. `{a^n b^m c^n d^m | n, m ≥ 0}` is context-free  
D. `{a^n b^n c^m | n, m ≥ 0} ∩ {a^n b^m c^m | n, m ≥ 0} = {a^n b^n c^n | n ≥ 0}`, and the language on the right is not context-free

## Answer Key
| Q | Type | Answer |
|---|------|--------|
| 1 | MCQ | B |
| 2 | MCQ | A |
| 3 | MCQ | A |
| 4 | NAT | 4 |
| 5 | MSQ | A, B, C |
| 6 | MCQ | B |
| 7 | MCQ | B |
| 8 | NAT | 4 |
| 9 | MCQ | B |
| 10 | MSQ | A, B, D |
| 11 | MCQ | B |
| 12 | MCQ | B |
| 13 | MSQ | A, B, C |
| 14 | MCQ | A |
| 15 | MSQ | A, B, D |
| 16 | MCQ | C |

## Detailed Solutions

### Q1

Answer: B

(A) is regular, hence context-free, but the question asks for a language that is not regular.

(B) has the grammar `S → aSb | ε`, so it is context-free. It is not regular: if `i ≠ j`, then `a^i b^i` is in the language and `a^j b^i` is not.

(C) is not context-free. The pumping argument is in Q16 and, in more detail, in the pumping-lemma set: a window of length `p` inside `a^p b^p c^p` cannot repair all three equal exponents at once.

(D) is not context-free. If it were, its intersection with the regular language `a*b*a*b*` would be context-free. A square `xx` lies in `a*b*a*b*` only when `x ∈ a*b*`: an internal `ba` in `x` would appear twice in `xx`, but `a*b*a*b*` contains only one `ba` transition. Thus the intersection is exactly `{a^n b^m a^n b^m | n, m ≥ 0}`. The four blocks are the crossed equalities of Q15(C), and the same pumping case analysis, read with the second `a`-block in place of `c` and the second `b`-block in place of `d`, shows that this intersection is not context-free. Hence (D) is not context-free. The reverse language `{w w^R}` is context-free, because one stack matches a string against its reverse; the same-order copy does not have that shape.

### Q2

Answer: A

Take grammars for `L1` and `L2` with disjoint variables and start symbols `S1` and `S2`. The new productions `S → S1 | S2` generate a string exactly when one of the old grammars does. The result is context-free.

Intersection does not preserve the context-free languages, so (B) is not a closure construction. (C) and (D) are constructions for regular languages.

### Q3

Answer: A

In (A), `T` generates `{a^n b^n | n ≥ 0}` and `C` generates `c*`. Their concatenation is the required language, including the cases `n = 0` and `m = 0`.

(B) generates `{a^n c b^n | n ≥ 0}`. (C) generates every string over `{a, b, c}`. (D) ties three counts together and does not generate `c` alone or `abcc`.

### Q4

Answer: 4

Every string in the language has the form `a^i b^j`. For length 4 the candidates are

`aaaa` (`4, 0`), `aaab` (`3, 1`), `aabb` (`2, 2`), `abbb` (`1, 3`), `bbbb` (`0, 4`).

Exactly one of them has `i = j`, namely `aabb`. The other four are in the language. Strings such as `baaa` are not of the form `a^i b^j`.

### Q5

Answer: A, B, C

Union is the new start symbol of Q2. Concatenation is `S → S1 S2` with the same disjoint-variable convention. Star is `S → S1 S | ε`.

Intersection does not preserve context-free languages. Q10 gives the standard counterexample: two context-free languages whose intersection is `{a^n b^n c^n | n ≥ 0}`.

### Q6

Answer: B

Run a PDA for `L` and a DFA for `R` together. The stack is the PDA's stack, and the finite control stores the pair of states. Accept when the PDA accepts and the DFA is in an accept state. The result is a PDA, so `L ∩ R` is context-free.

It is not always regular. Take `L = {a^n b^n | n ≥ 0}` and `R = a*b*`. Both the intersection and `L` are the same non-regular context-free language. The intersection is infinite, so (D) is false as well.

### Q7

Answer: B

The reverse of `a^n b^n b^n` is `b^n b^n a^n = b^{2n} a^n`. The grammar `S → b b S a | ε` generates that language, so the reverse is context-free.

In general, reversing every right-hand side of a context-free grammar reverses the generated language and leaves the grammar context-free. (A) would require the block of `b`s to stay on the right. (C) has the right letters in the wrong counts. (D) is a three-block language and is not the reverse of a two-block language.

### Q8

Answer: 4

A string `w c w^R` has length `2|w| + 1`. Length 5 forces `|w| = 2`. There are `2^2 = 4` choices of `w` over `{a, b}`:

`aacaa`, `abcab`, `bacba`, `bbcbb`.

### Q9

Answer: B

(B) is true, and it is a counterexample to (A), (C), and (D).

The language `L = {a^n b^n | n ≥ 0}` is context-free and not regular. Its complement over `{a, b}` is the union of two context-free languages:

- the regular, hence context-free, language of strings that are not in `a*b*`, namely `(a+b)*ba(a+b)*`
- the language `{a^i b^j | i ≠ j}`

The second language has the grammar

```
S → T | U
T → aTb | A
A → aA | a
U → aUb | B
B → bB | b
```

`T` generates the strings with more `a`s than `b`s, and `U` generates the strings with more `b`s than `a`s. Context-free languages are closed under union, so the complement is context-free.

Thus both a language and its complement can be context-free while the language is not regular. That is why (A) and (C) are false.

(D) is false for a different reason. If every context-free language had a context-free complement, De Morgan's identity

`L1 ∩ L2 = complement( complement(L1) ∪ complement(L2) )`

would make the context-free languages closed under intersection. Q10 shows they are not. The complement constructed above is not that counterexample: it is context-free. A concrete witness is the complement of `{a^n b^n c^n | n ≥ 0}`. That complement is context-free, because a string fails the three equal exponents when it is outside `a*b*c*`, or it is in `a*b*c*` and has either unequal `a` and `b` counts or unequal `b` and `c` counts. Each of those pieces is context-free. Its complement, `{a^n b^n c^n | n ≥ 0}`, is not context-free.

### Q10

Answer: A, B, D

(A) is the language of Q3(A). (B) has the symmetric grammar `S → A T`, `A → aA | ε`, `T → bTc | ε`.

(D) is true because context-free languages are closed under union.

(C) is false. A string in both languages satisfies `n = m` in the middle exponent from both descriptions, so

`L1 ∩ L2 = {a^n b^n c^n | n ≥ 0}`.

That language is not context-free. The pumping proof is the case analysis in the solution of Q16: no window of length `p` can raise or lower all three exponents together. Since the intersection is not context-free, context-free languages are not closed under intersection. Both `L1` and `L2` are nevertheless context-free, which is why (A), (B), and (D) survive.

### Q11

Answer: B

(B) is the union of `{a^i b^i c^k | i, k ≥ 0}` and `{a^i b^j c^j | i, j ≥ 0}`. Each piece is context-free by a one-stack grammar, as in Q10, and the union of context-free languages is context-free.

(A) is `{a^n b^n c^n | n ≥ 0}`, which is not context-free. (C) is the copy language from Q1. (D) imposes four equal exponents. Intersecting (D) with `a*b*c*d*` leaves it unchanged, and pumping `a^p b^p c^p d^p` changes at most two adjacent blocks inside a window of length `p`, so some equality breaks.

### Q12

Answer: B

(B) is the closure fact from Q6. The product of a PDA and a DFA is a PDA.

(A) adds the false claim that the intersection is regular. The counterexample is `{a^n b^n} ∩ a*b*`. (C) and (D) are the two closure failures: Q10 for intersection, and Q9 for complement. Those failures are linked by De Morgan, but each can be shown on its own example.

### Q13

Answer: A, B, C

(A), (B), and (C) are the closure facts already used above. Union preserves context-free languages. Intersection does not, by `L1 ∩ L2 = {a^n b^n c^n}` in Q10. Complement does not: the complement of `{a^n b^n}` is context-free, but if every complement of a context-free language were context-free, intersection could be rebuilt by De Morgan from union and complement, contradicting Q10.

(D) is the trap. `L ∩ R` is context-free, not necessarily regular. The word “always regular” is what makes (D) false.

### Q14

Answer: A

(A) is context-free by the explicit union in Q9: strings that contain `ba`, together with strings `a^i b^j` whose exponents differ.

(B) is not context-free. (C) is not context-free, as recorded in Q1. (D) is not context-free; it is option (C) of Q15, proved there by pumping. The correct choice is the complement, which is easy to underestimate because `{a^n b^n}` itself is not regular. Non-regularity of `L` does not decide whether the complement is context-free.

### Q15

Answer: A, B, D

(A) is context-free: `S → X Y`, `X → aXb | ε`, `Y → cYd | ε`. The stack matches `a`s with `b`s and then, independently, `c`s with `d`s.

(B) is context-free: `S → aSd | T`, `T → bTc | ε`. The outer pair is `a` with `d`, and the inner pair is `b` with `c`. One stack handles the nested pairs.

(D) is context-free by Q3.

(C) is not context-free. Suppose it is, and let `p` be a pumping length. The string

`s = a^p b^p c^p d^p`

belongs to the language. Write `s = uvwxy` with `|vwx| ≤ p` and `|vx| ≥ 1`, as the pumping lemma requires. The window `vwx` lies inside one block or across one boundary between adjacent blocks. It cannot meet both an `a` and a `c`, nor both a `b` and a `d`, nor both an `a` and a `d`.

Pump to `k = 2`.

- If `vx` contains only `a`s, the `a`-count changes and the `c`-count does not, so `n` is no longer equal for `a` and `c`.
- The same one-letter failure applies to a window of only `b`s, only `c`s, or only `d`s.
- If the window meets `a` and `b`, the `c` and `d` counts stay fixed. Changing the `a`s breaks `a` against `c`, unless `vx` contains no `a`. If it contains no `a`, it changes the `b`s and breaks `b` against `d`. It cannot change neither, because `|vx| ≥ 1`.
- If the window meets `b` and `c`, either the `b`-count changes and no longer equals the unchanged `d`-count, or the `c`-count changes and no longer equals the unchanged `a`-count, or both happen.
- If the window meets `c` and `d`, the `a` and `b` counts stay fixed, and the same case split used for `a` and `b` breaks one of the two required equalities.

Every legal window fails. The language is not context-free. The same proof is why a PDA cannot accept (C): the dependencies `a` with `c` and `b` with `d` are crossed, and one stack cannot store both pairs in the required order.

### Q16

Answer: C

(A), (B), and the equality in (D) are true. The two grammars are those of Q15(A) and Q15(B). A string lies in both `{a^n b^n c^m}` and `{a^n b^m c^m}` exactly when all three exponents agree, and `{a^n b^n c^n}` is not context-free by the three-block case of the same pumping argument: in `a^p b^p c^p` a window of length at most `p` misses at least one of the three letters, so pumping changes a count that another letter does not follow.

(C) is the false statement. Q15 shows that `{a^n b^m c^n d^m | n, m ≥ 0}` is not context-free.
