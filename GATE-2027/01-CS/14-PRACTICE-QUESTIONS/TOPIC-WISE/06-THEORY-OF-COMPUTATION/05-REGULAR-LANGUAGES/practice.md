# Regular Languages — Practice Questions

Original practice for GATE CS. These questions are not from any GATE paper. Attempt the questions before reading the solutions.

Two strings `x` and `y` are distinguishable with respect to `L` when some continuation `z` satisfies `xz ∈ L` and `yz ∉ L`, or the other way around. A language is regular exactly when only finitely many strings are pairwise distinguishable. The empty string is `ε`.

## Level 1 — Conceptual

## Q1 — MCQ

Which language is regular?

A. `{a^n b^{n+1} | n ≥ 0}`  
B. `{w ∈ {0, 1}* | |w| ≤ 3}`  
C. `{a^n b^n c^n | n ≥ 0}`  
D. `{ww | w ∈ {a, b}*}`

---

## Q2 — MCQ

If `L` is a regular language over `{0, 1}`, which language is always regular?

A. `{0, 1}* − L`  
B. `{0^n 1^n | 0^n 1^n ∈ L}`  
C. `{ww | w ∈ L}`  
D. every subset of `L`

---

## Q3 — MCQ

Which language is **not** regular?

A. `(01)*`  
B. `{a^n b^m | n, m ≥ 0}`  
C. `{a^n b^n | n ≥ 0}`  
D. `{w ∈ {0, 1}* | |w| is even}`

---

## Q4 — NAT

The number of length-5 strings in the regular language of binary strings with exactly two `1`s is ____.

---

## Level 2 — Standard GATE Style

## Q5 — MSQ

Which statements are true? Select all that apply.

A. If `L1` and `L2` are regular, then so is `L1 ∪ L2`  
B. If `L1` and `L2` are regular, then so is `L1 ∩ L2`  
C. If `L1` and `L2` are regular, then so is `L1 − L2`  
D. If `L` is regular, then so is `{ww | w ∈ L}`

---

## Q6 — MCQ

The reverse of a regular language is regular. The reverse of `a*b*` is

A. `a*b*`  
B. `b*a*`  
C. `(ab)*`  
D. `{a^n b^n | n ≥ 0}`

---

## Q7 — NAT

The number of states in the minimal complete DFA for

`{ w ∈ {a, b}* | w starts with b and contains an even number of a's }`

is ____.

---

## Q8 — MCQ

Which statement is true?

A. Regular languages are closed under reversal  
B. The union of a regular language and a non-regular language is never regular  
C. Every subset of a regular language is regular  
D. If `L*` is regular, then `L` is regular

---

## Level 3 — Multi-Step

## Q9 — MCQ

Let `L = {a^n b^{n+1} | n ≥ 0}`. The strings `a^i` and `a^j`, for `i ≠ j`, are distinguishable with respect to `L` because

A. `a^i b^{i+1} ∈ L` and `a^j b^{i+1} ∉ L`  
B. both `a^i` and `a^j` belong to `L`  
C. `L` is finite  
D. the continuation `b` puts every `a^i` into `L`

---

## Q10 — NAT

The number of strings of length 6 over `{a, b}` that do **not** contain the substring `ab` is ____.

---

## Q11 — MSQ

Which statements are true? Select all that apply.

A. If `L` has infinitely many pairwise distinguishable strings, then `L` is not regular  
B. If `L` is regular, then `L` has only finitely many pairwise distinguishable strings  
C. If only finitely many strings are pairwise distinguishable with respect to `L`, then `L` is regular  
D. Every DFA for `L`, minimal or not, has exactly one state per distinguishable class of `L`

---

## Level 4 — Tricky / Trap-Based

## Q12 — NAT

The number of states in the minimal complete DFA for the binary language of strings that do not contain the substring `11` is ____.

---

## Q13 — MCQ

Which example shows that `L ∪ M` and `L` can both be regular while `M` is not regular?

A. `L = {0, 1}*` and `M = {0^n 1^n | n ≥ 0}`  
B. `L = {0^n 1^n | n ≥ 0}` and `M = {0, 1}*`  
C. `L = ∅` and `M = {0, 1}*`  
D. `L = M = {0^n 1^n | n ≥ 0}`

---

## Q14 — MSQ

Which statements are true? Select all that apply.

A. If `L` is not regular, then the complement of `L` is not regular  
B. If `L` is regular and `L ∩ M` is not regular, then `M` is not regular  
C. If `L` is not regular, then `L*` is not regular  
D. Regular languages are closed under intersection

---

## Level 5 — Challenge

## Q15 — MCQ

Which language `L` is not regular, while `L*` is regular?

A. `L = {a^n b^n | n ≥ 1} ∪ {a, b}`  
B. `L = {a^n b^n | n ≥ 0}`  
C. `L = a*b*`  
D. `L = {a, b}`

---

## Q16 — NAT

The number of states in the minimal complete DFA for

`{ a^i b^j | i, j ≥ 0 and i + j is even }`

is ____.

## Answer Key
| Q | Type | Answer |
|---|------|--------|
| 1 | MCQ | B |
| 2 | MCQ | A |
| 3 | MCQ | C |
| 4 | NAT | 10 |
| 5 | MSQ | A, B, C |
| 6 | MCQ | B |
| 7 | NAT | 4 |
| 8 | MCQ | A |
| 9 | MCQ | A |
| 10 | NAT | 7 |
| 11 | MSQ | A, B, C |
| 12 | NAT | 3 |
| 13 | MCQ | A |
| 14 | MSQ | A, B, D |
| 15 | MCQ | A |
| 16 | NAT | 5 |

## Detailed Solutions

### Q1

Answer: B

(B) is finite: it contains the empty string, 2 strings of length 1, 4 of length 2, and 8 of length 3. Every finite language has a DFA that walks along a trie of the accepted strings and sends every wrong continuation into a rejecting sink.

(A) is not regular: the strings `a^n` are pairwise distinguishable by `b^{n+1}`. (C) is not even context-free. (D) is not regular: if it were, its intersection with the regular language `a*ba*b` would be regular. That intersection is `{a^n b a^n b | n ≥ 0}`, and `a^i b` is distinguished from `a^j b` by the continuation `a^i b` whenever `i ≠ j`.

### Q2

Answer: A

Regular languages are closed under complement, so `{0, 1}* − L` is regular.

(B) need not be regular. Take `L = 0*1*`, which is regular. The displayed set is then all of `{0^n 1^n | n ≥ 0}`, which is not regular. (C) need not be regular: if `L = a*b`, then `{ww | w ∈ L} = {a^n b a^n b | n ≥ 0}`, and the strings `a^i b` are distinguished by `a^i b`. (D) is false because `{0, 1}*` is regular and `{0^n 1^n | n ≥ 0}` is a non-regular subset.

### Q3

Answer: C

(A), (B), and (D) have small DFAs: a two-state cycle for `(01)*`, an `a`-loop that switches once into a `b`-loop for `a*b*`, and a two-state parity DFA for even length.

(C) is not regular. If `i ≠ j`, the continuation `b^i` accepts `a^i b^i` and rejects `a^j b^i`. Infinitely many distinguishable strings imply that the language is not regular.

### Q4

Answer: 10

Choose 2 positions among 5 for the `1`s. The rest are `0`s. The number of strings is `C(5, 2) = 10`.

The same count is the number of words of length 5 accepted by the 4-state DFA that counts `1`s up to “three or more” and accepts only the state “exactly two”.

### Q5

Answer: A, B, C

Union is the product automaton that accepts if either component accepts, or the union of two regular expressions. Intersection accepts if both components accept. Difference is `L1 ∩ (Σ* − L2)`, and both intersection and complement preserve regularity.

(D) is false by the example in Q2: `L = a*b` is regular, but `{ww | w ∈ L}` is not. This is not the concatenation `L · L`, which would be regular. The operation here repeats the same string.

### Q6

Answer: B

The reverse of `a^i b^j` is `b^j a^i`. As `i` and `j` range over all nonnegative integers, the reversed language is `b*a*`.

Reversal preserves regularity in general: reverse every transition of an NFA, swap the roles of the start state and the accept states (using a new start state with `ε`-moves into the old accept states if there are several), and convert back to a DFA if desired. Here the direct description is enough.

(A) still rejects `ba`. (C) is a different infinite set. (D) is not regular and is not the reverse of `a*b*`.

### Q7

Answer: 4

Four states are necessary and sufficient.

- `s`: nothing read (start, not accept)
- `bad`: the string began with `a` (reject sink)
- `e`: began with `b`, and the number of `a`s so far is even (accept)
- `o`: began with `b`, and the number of `a`s so far is odd (not accept)

Transitions: `s —b→ e`, `s —a→ bad`, `e —a→ o`, `e —b→ e`, `o —a→ e`, `o —b→ o`, and `bad` stays in `bad`.

Distinguishability:

- `e` is the only accept state among the four, so `ε` as a continuation separates it from `s`, `o`, and `bad`.
- From `s`, the continuation `b` is accepted. From `o`, `b` stays odd and is rejected. From `bad`, `b` is rejected.
- From `o`, the continuation `a` reaches `e` and is accepted. From `bad`, `a` is rejected.

So there are 4 classes. The rejecting sink is reachable by `a` and cannot be omitted from a complete DFA: `s` on `a` must go somewhere that can never accept.

### Q8

Answer: A

(A) is true; the NFA reversal in Q6 is the construction.

(B) is false. `{0, 1}* ∪ {0^n 1^n | n ≥ 0} = {0, 1}*`, which is regular, while the second language is not.

(C) is false by the same non-regular subset of `{0, 1}*`.

(D) is false. Q15 gives a non-regular language whose star is regular. A smaller illustration of the same idea is any non-regular language that contains both `a` and `b` and therefore satisfies `L* = {a, b}*`.

### Q9

Answer: A

For `i ≠ j`, `a^i b^{i+1}` has exactly one more `b` than `a`, so it is in `L`. The string `a^j b^{i+1}` has `j` `a`s and `i + 1` `b`s. These exponents match the language only if `j + 1 = i + 1`, that is, only if `j = i`. They do not, so the continuation `b^{i+1}` distinguishes `a^i` from `a^j`.

There are infinitely many such strings, one for each `i`. Hence `L` is not regular. (B) is false because `a^i` contains no `b`. (C) is false because `L` is infinite. (D) is false because `a^i b = a^i b^1` is in `L` only for `i = 0`.

### Q10

Answer: 7

A string contains `ab` exactly when some `a` occurs before a later `b`. The strings that avoid `ab` are the strings in `b*a*`: a block of `b`s followed by a block of `a`s.

For length 6 there is one such string for each number of `b`s from 0 through 6, hence 7 strings: `bbbbbb`, `bbbbba`, `bbbbaa`, `bbbaaa`, `bbaaaa`, `baaaaa`, and `aaaaaa`.

### Q11

Answer: A, B, C

(A), (B), and (C) are the Myhill–Nerode theorem. Infinitely many pairwise distinguishable strings forbid a DFA, because each class needs its own state. Conversely, the distinguishable classes can be used as the states of a DFA: from the class of `x`, the symbol `a` leads to the class of `xa`, and this transition is well defined precisely because strings in the same class have the same continuations.

(D) is false. The number of classes equals the number of states of the minimal complete DFA. A non-minimal DFA has extra states, either unreachable or equivalent to other states.

### Q12

Answer: 3

Three states are enough.

- `r0`: start, and also every accepted string that does not end with `1`. Accept.
- `r1`: the string so far is accepted and ends with a single `1`. Accept.
- `rd`: `11` has already occurred. Reject sink.

Transitions: `r0 —0→ r0`, `r0 —1→ r1`, `r1 —0→ r0`, `r1 —1→ rd`, and `rd` stays in `rd` on both symbols.

They are distinguishable.

- `ε` separates both accept states from `rd`.
- The continuation `1` is accepted from `r0` (`1` itself has no `11`) and rejected from `r1` (`11` contains `11`).

A fourth state is the usual off-by-one mistake: splitting “empty” from “ends with `0`”. Those two situations have the same continuations. Both accept `ε` as a continuation, both stay in the same kind of state on `0`, and both enter `r1` on `1`. The minimal complete DFA has 3 states, not 2 and not 4. Two states cannot both keep `1` alive and permanently kill `11`.

### Q13

Answer: A

In (A), `L` is regular and `L ∪ M = L` because `M ⊆ {0, 1}*`. The language `M` is not regular. This is the required separation.

(B) uses a non-regular `L`, so it does not illustrate the claim. (C) has a regular `M`. (D) has a non-regular union.

Closure under union does not let one cancel a regular summand and conclude that the other summand is regular.

### Q14

Answer: A, B, D

(A) is true. If the complement were regular, one more complement would make `L` regular.

(B) is true. It is the contrapositive of closure under intersection: if `M` were regular, then `L ∩ M` would be regular.

(C) is false. The language in Q15(A) is not regular, but its star is `{a, b}*`.

(D) is true. It is the operation whose contrapositive was used in (B). Regular languages are closed under intersection even though context-free languages are not. Confusing the two families is the trap.

### Q15

Answer: A

For (A), both `a` and `b` belong to `L`, so every string over `{a, b}` is a concatenation of elements of `L`. Thus `L* = {a, b}*`, which is regular.

`L` itself is not regular. Intersect with the regular language `a*b*`:

`L ∩ a*b* = {a^n b^n | n ≥ 1} ∪ {a, b}`.

If `L` were regular, this intersection would be regular, and deleting the finite set `{a, b}` would leave the regular language `{a^n b^n | n ≥ 1}`. That language is not regular: `a^i` and `a^j` are distinguished by `b^i` whenever `i ≠ j` and `i, j ≥ 1`. This contradiction shows that `L` is not regular.

(B) fails the second half of the question. The star of `{a^n b^n | n ≥ 0}` is still non-regular; its intersection with `a*b*` is the original language. (C) and (D) are regular already, so they are not examples of a non-regular `L`.

### Q16

Answer: 5

The language is the set of strings `a*b*` whose length is even. A complete DFA also needs a sink for a `b` followed later by an `a`.

- `ae`: even number of `a`s, still in the `a`-block. Accept, because `j = 0` and `i` is even. This is the start state.
- `ao`: odd number of `a`s, still in the `a`-block.
- `be`: a `b` has been read and the total length is even. Accept.
- `bo`: a `b` has been read and the total length is odd.
- `d`: a `b` was followed later by an `a`. Reject sink.

Transitions:

- `ae —a→ ao`, `ae —b→ bo`
- `ao —a→ ae`, `ao —b→ be`
- `be —b→ bo`, `be —a→ d`
- `bo —b→ be`, `bo —a→ d`
- `d` stays in `d`

The accept states are `ae` and `be`. Every string that stays inside `a*b*` flips parity on every symbol, and a late `a` dies in `d`.

All five states are distinguishable.

- `ε` separates the two accept states from `ao`, `bo`, and `d`.
- From `ae`, the continuation `aa` returns to `ae` and is accepted. From `be`, `aa` enters `d` and is rejected.
- From `ao`, the continuation `a` reaches `ae` and is accepted. From `bo` and from `d`, `a` is rejected.
- From `bo`, the continuation `b` reaches `be` and is accepted. From `d`, `b` is rejected.

So the minimal complete DFA has 5 states. Forgetting the sink `d` leaves the transition on `a` from `be` and `bo` undefined. Merging `ae` with `be` identifies a state that can still read `a` with a state that cannot.
