# Push-Down Automata — Practice

Original GATE-style questions written for this repository. They are not previous-year questions. They do not repeat the questions in `../../14-PRACTICE-QUESTIONS/TOPIC-WISE/06-THEORY-OF-COMPUTATION/04-PUSH-DOWN-AUTOMATA/practice.md`; do both sets.

Transition notation: `δ(q, a, X) = (p, γ)` pops `X` and pushes `γ` (leftmost = new top). The stack starts with bottom marker `Z`. Acceptance is existential. Traces below were checked ID by ID.

Open the answer block only after attempting the question.

---

## Level 1 — Conceptual

### Q1 · MCQ

Which language is accepted by some PDA but by no FA?

- (A) `{ ww^R | w ∈ {0,1}* }`
- (B) `{ 0^{2n} | n ≥ 0 }`
- (C) `(01)*`
- (D) all strings over `{0,1}` whose length is divisible by 3

<details><summary>Answer and solution</summary>

**Answer:** (A)

**Solution:** (A) has the grammar `S → 0S0 | 1S1 | ε` and an NPDA that guesses the middle. The strings `0^n` are pairwise distinguishable by the continuation `0^n`, so it is not regular. (B) is `(00)*`, regular. (C) and (D) are regular.

**Concept tested:** CFL − regular vs regular.
**Difficulty:** Level 1
**Common trap:** (B), thinking even length on a unary alphabet needs a stack.
</details>

### Q2 · MCQ

A PDA that accepts by empty stack accepts a string `w` when

- (A) some computation reads all of `w` and ends with an empty stack
- (B) every computation ends with an empty stack
- (C) the state is accepting, regardless of leftover stack symbols
- (D) the stack empties at least once during the computation, even if input remains

<details><summary>Answer and solution</summary>

**Answer:** (A)

**Solution:** Empty-stack acceptance is existential and is checked only after the input is consumed. Accept states are irrelevant. Emptying the stack in the middle of `w` is not acceptance of `w`.

**Concept tested:** empty-stack mode.
**Difficulty:** Level 1
**Common trap:** (C), which is final-state mode.
</details>

### Q3 · MCQ

Every language accepted by a DFA is accepted by

- (A) some DPDA, and some DFA languages are not DCFL
- (B) some DPDA (ignore the stack, run the DFA in the finite control)
- (C) some NPDA but not by any DPDA
- (D) no PDA, because a PDA must use its stack

<details><summary>Answer and solution</summary>

**Answer:** (B)

**Solution:** Regular ⊂ DCFL. A DPDA may leave `Z` untouched and copy the DFA’s transition table. (A)’s second clause is false. (C) and (D) contradict the inclusion.

**Concept tested:** regular ⊂ DCFL; 2025-family fact.
**Difficulty:** Level 1
**Common trap:** thinking a PDA is required to push.
</details>

---

## Level 2 — Standard GATE

### Q4 · MSQ

The PDA accepts by final state `qf` only. Start `q0`, stack `Z`.

```
δ(q0, a, Z) = (q0, AZ)
δ(q0, a, A) = (q0, AA)
δ(q0, b, A) = (q1, A)
δ(q1, b, A) = (q0, ε)
δ(q0, ε, Z) = (qf, Z)
```

(`q1` remembers that an odd number of `b`s have been read since the last pop.) Which strings are accepted? Select all that apply.

- (A) `ε`
- (B) `abb`
- (C) `ab`
- (D) `aabbbb`

<details><summary>Answer and solution</summary>

**Answer:** (A), (B), (D)

**Solution:** The ε-move on `(q0, Z)` competes with the `a`-move on `(q0, Z)`, so this particular table is an NPDA: the branch that takes ε too early dies if input remains; the branch that waits accepts `{ a^n b^{2n} | n ≥ 0 }`. A `b` in `q0` on `A` moves to `q1` without popping (odd `b`). A `b` in `q1` on `A` pops one `A` and returns to `q0`. The ε-move to `qf` exists only in `q0` on `Z`, so the machine accepts when `#b = 2 #a` and the input is finished in `q0`. Language `{ a^n b^{2n} | n ≥ 0 }`.

- `ε`: `n = 0`, ε-move on `Z`. Accepted.
- `abb`: push `A`, dummy-stay on first `b`, pop on second `b`, ε-move. Accepted.
- `ab`: finishes in `q1` with `AZ`. No ε-move. Rejected.
- `aabbbb`: two pushes, three pairs of `b`s would be needed for `n = 2` wait: `n = 2` needs 4 `b`s. `aabbbb` is `a^2 b^4`. Trace: two pushes (`AAZ`); `b` → `q1` stack `AAZ`; `b` pop → `q0` stack `AZ`; `b` → `q1` `AZ`; `b` pop → `q0` `Z`; ε-move. Accepted.

**Concept tested:** two input letters per stack symbol; parity state.
**Difficulty:** Level 2
**Common trap:** accepting `ab` as if the language were `{ a^n b^n }`.
</details>

### Q5 · NAT

On an accepting computation of the PDA in Q4 on `aaabbbbbb`, the maximum number of stack symbols, counting `Z`, is ____.

<details><summary>Answer and solution</summary>

**Answer:** 4

**Solution:** Three `a`s push three `A`s onto `Z`: stack `AAAZ`, height 4. Each pair of `b`s then pops one `A`. Height never increases after the `a`s. `n = 3` needs 6 `b`s; the input is `a^3 b^6`.

**Concept tested:** stack-height trace including `Z`.
**Difficulty:** Level 2
**Common trap:** answering 3 (forgetting `Z`) or 6 (counting `b`s).
</details>

### Q6 · MCQ

Which language is accepted by some DPDA?

- (A) `{ ww | w ∈ {a,b}* }`
- (B) `{ a^n b^n c^n | n ≥ 0 }`
- (C) `{ w # w^R | w ∈ {a,b}* }` (`#` a marker not in `{a,b}`)
- (D) `{ ww^R | w ∈ {a,b}* }`

<details><summary>Answer and solution</summary>

**Answer:** (C)

**Solution:** `#` is a unique switch from push to pop-match. Deterministic. (D) needs a guessed middle (NPDA, not DPDA). (A) and (B) are not CFL, so no PDA at all.

**Concept tested:** centre marker vs guessed middle vs non-CFL.
**Difficulty:** Level 2
**Common trap:** (D).
</details>

### Q7 · MCQ

For a single PDA `M`, let `L_f(M)` be its final-state language and `L_e(M)` its empty-stack language. Which statement is true?

- (A) `L_f(M) = L_e(M)` for every `M`
- (B) `L_f(M)` and `L_e(M)` may differ, but the families `{ L_f(N) | N an NPDA }` and `{ L_e(N) | N an NPDA }` are equal (both = CFL)
- (C) `L_e(M) ⊆ L_f(M)` always
- (D) `L_f` and `L_e` coincide exactly when `M` is deterministic

<details><summary>Answer and solution</summary>

**Answer:** (B)

**Solution:** The Q4 machine, read by empty stack, rejects `abb`: after the input `Z` is still there. So the modes of one machine differ. NPDAs can convert either way. Determinism is not the criterion for the modes of one machine to agree, and the conversions need not preserve determinism.

**Concept tested:** mode vs family.
**Difficulty:** Level 2
**Common trap:** (A) or (D).
</details>

---

## Level 3 — Multi-Step

### Q8 · MCQ

PDA, accept by final state. Accept states `{q0, qZ}`. Start `q0`.

```
δ(q0, a, Z) = (qp, AZ)
δ(qp, a, A)  = (qp, AA)
δ(qp, b, A)  = (qpop, ε)
δ(qpop, b, A) = (qpop, ε)
δ(qpop, ε, Z) = (qZ, Z)
δ(q0, b, Z)  = (qZ, Z)
δ(qZ, b, Z)  = (qZ, Z)
```

The language is

- (A) `{ a^n b^n | n ≥ 0 }`
- (B) `{ a^n b^m | n ≥ m ≥ 0 }`
- (C) `{ a^n b^m | m ≥ n ≥ 0 }`
- (D) `a* b*`

<details><summary>Answer and solution</summary>

**Answer:** (C)

**Solution:** `a`s push in a non-accepting state `qp`. `b`s pop. The ε-move into accepting `qZ` fires only on `Z`, so at least as many `b`s as `a`s are required to uncover `Z`. Extra `b`s stay in `qZ`. Pure `b*` is accepted from `q0` on `Z`. Leftover `A`s (too few `b`s) finish in `qp` or `qpop`, neither accepting.

- `ε`: `q0` accept. `n = m = 0`.
- `abb`: `m = 2 ≥ n = 1`. Accepted.
- `aab`: leftover `A`, rejected.
- `aaa`: leftover `A`s in `qp`, rejected.

Not all of `a* b*` because of `aab`. Not `n ≥ m` because `abb` is in and `aab` is out.

**Concept tested:** leftover stack vs extra input; opposite inequality of the usual `{ n ≥ m }` machine.
**Difficulty:** Level 3
**Common trap:** (B), the leftover-`A` language.
</details>

### Q9 · MSQ

Which statements are true? Select all that apply.

- (A) NPDA languages = CFL
- (B) Every DCFL is regular
- (C) `{ 0^n 1^n | n ≥ 0 }` is a DCFL
- (D) `{ 0^n 1^n 2^n | n ≥ 0 }` is accepted by some NPDA

<details><summary>Answer and solution</summary>

**Answer:** (A), (C)

**Solution:** (A) is the equivalence. (B) is false: (C) is the witness that DCFL properly contains regular. (D) is not CFL, so no NPDA.

**Concept tested:** hierarchy.
**Difficulty:** Level 3
**Common trap:** (D) “three letters, use three states”.
</details>

### Q10 · NAT

The number of strings of length 3 in the language of Q8 is ____.

<details><summary>Answer and solution</summary>

**Answer:** 2

**Solution:** Strings `a^n b^m` with `n + m = 3` and `m ≥ n`: `(n,m) = (0,3)` and `(1,2)`. The strings are `bbb` and `abb`. `aab` and `aaa` have `m < n`.

**Concept tested:** counting in a leftover-input language.
**Difficulty:** Level 3
**Common trap:** counting 4 (all of `a*b*` of length 3) or 3 (including `aab`).
</details>

---

## Level 4 — Tricky / Trap-Based

### Q11 · MCQ

An NPDA for `{ ww^R | w ∈ {0,1}* }` has a rejecting computation on `0110` (it tries to switch after the first `0`). The string `0110` is

- (A) rejected, because a rejecting computation exists
- (B) accepted, because a computation that switches after `01` matches `10` and can accept
- (C) not context-free
- (D) accepted only by a DPDA

<details><summary>Answer and solution</summary>

**Answer:** (B)

**Solution:** Existential acceptance. `0110 = (01)(10) = w w^R` with `w = 01`. The language is CFL and the natural machine is nondeterministic; a DPDA cannot guess that middle.

**Concept tested:** NPDA acceptance; palindromes.
**Difficulty:** Level 4
**Common trap:** (A).
</details>

### Q12 · MSQ

Which statements are true? Select all that apply.

- (A) CFL ∩ regular is CFL
- (B) DCFL is closed under union
- (C) If a DPDA accepts `x` by empty stack, it accepts no proper extension `xy` by empty stack
- (D) `{ a^n b^n | n ≥ 0 }` is prefix-free, hence it is an empty-stack DPDA language

<details><summary>Answer and solution</summary>

**Answer:** (A), (C)

**Solution:** (A) is PDA × DFA. (B) is false: `{ a^n b^n c^* } ∪ { a^* b^n c^n }` is CFL and not DCFL (or, `{ a^n b^n } ∪ { a^n b^{2n} }`). (C) is prefix-freeness of empty-stack DPDA languages: after `x` the stack is empty, so no next move exists. (D) is false in both clauses: `ε` is a proper prefix of `ab`, so the language is not prefix-free, and therefore no empty-stack DPDA accepts it (a **final-state** DPDA does).

**Concept tested:** product; DCFL union; prefix-free empty stack.
**Difficulty:** Level 4
**Common trap:** (D), confusing the two acceptance modes for `{ a^n b^n }`.
</details>

---

## Level 5 — Challenge

### Q13 · MCQ

A PDA pushes `X` on each `0`, switches state on the first `1` without changing the stack, pops one `X` on each later `1`, then on each `2` pops nothing but requires the stack to be already `Z` and stays in an accept state. It has no move on `0` after a `1`, or on `1` after a `2`. Its language is

- (A) `{ 0^i 1^j 2^k | i = j }`
- (B) `{ 0^i 1^j 2^k | i = j + k }`
- (C) `{ 0^i 1^{i+1} 2^k | k ≥ 0 }`
- (D) `{ 0^i 1^i 2^i }`

<details><summary>Answer and solution</summary>

**Answer:** (C)

**Solution:** `i` symbols are pushed. The first `1` does not pop, so it is a **centre marker** that must occur. Each later `1` pops one `X`. Accepting with stack `Z` after those `1`s requires exactly `i` popping `1`s, hence `#1 = i + 1`. Then any number of `2`s are a regular tail on empty stack (final-state). So `{ 0^i 1^{i+1} 2^k | i, k ≥ 0 }`. For `i = 0` the first `1` must still be read on `Z`; that is allowed if a `1`-on-`Z` switch exists, giving `1 2^k`. If `i = 0` is excluded by the machine needing an `X` for the switch, the `i ≥ 1` slice remains of the same form. In any case it is not (A) (that would pop on every `1` with no dummy first `1`), not three equal counts, and not `i = j + k` (the `2`s are unconstrained).

Check: `00111` is `0^2 1^3`, in (C) with `k = 0`. `0011` has four letters `0^2 1^2`, `#1 ≠ i+1`, rejected. `0011122` accepted.

**Concept tested:** a dummy first letter as a marker plus a regular tail.
**Difficulty:** Level 5
**Common trap:** (A), ignoring the non-popping first `1`.
</details>

### Q14 · MCQ

Which language is context-free?

- (A) `{ 0^i 1^j 2^j 3^i | i, j ≥ 0 }`
- (B) `{ 0^i 1^j 2^i 3^j | i, j ≥ 0 }`
- (C) `{ ww | w ∈ {0,1}* }`
- (D) `{ 0^n 1^n 2^n | n ≥ 0 }`

<details><summary>Answer and solution</summary>

**Answer:** (A)

**Solution:** (A) is nested pairs: `S → 0 S 3 | T`, `T → 1 T 2 | ε`. A PDA pushes on `0` and `1`, pops on `2` against `1`s then on `3` against `0`s. (B) is crossed (`0` with `2`, `1` with `3`) and is not CFL. (C) and (D) are the standard non-CFLs.

**Concept tested:** nested vs crossed; copy language.
**Difficulty:** Level 5
**Common trap:** (B), swapping the inner pair.
</details>

### Q15 · MSQ

Which languages are accepted by some DPDA? Select all that apply.

- (A) `{ 0^n 1^n | n ≥ 0 }`
- (B) `{ 0^n 1^{2n} | n ≥ 0 }`
- (C) `{ ww^R | w ∈ {0,1}* }`
- (D) every regular language over `{0,1}`

<details><summary>Answer and solution</summary>

**Answer:** (A), (B), (D)

**Solution:** (A) unique switch at the first `1`. (B) a DPDA uses a parity state (dummy stay on the odd `1`, pop on the even `1`) and, after a pop, an ε-peek that is defined only on the new top: `ε` on `Z` enters an accept state, `ε` on `A` returns to the even-with-`A`s state. Those two ε-moves have different tops and no competing letter-move, so the machine is deterministic. (The Q4 machine is **not** a DPDA: its `ε`-move on `(q0, Z)` competes with the `a`-move on `(q0, Z)`. It is an NPDA for the same language.) (C) is CFL not DCFL. (D) is regular ⊂ DCFL.

**Concept tested:** DPDA examples vs palindromes; regular ⊂ DCFL.
**Difficulty:** Level 5
**Common trap:** rejecting (B) because “two `1`s per `0` needs nondeterminism”; the parity state is deterministic.
</details>
