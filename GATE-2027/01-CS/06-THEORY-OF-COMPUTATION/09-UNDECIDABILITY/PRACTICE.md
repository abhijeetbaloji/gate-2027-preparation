# Undecidability — Practice

Original questions. Not PYQs and not a copy of `14-PRACTICE-QUESTIONS`.

### Q1 · MCQ · Level 1

DFA membership is

- (A) decidable  (B) undecidable  (C) not RE  (D) meaningless

<details><summary>Answer</summary>

**Answer:** (A).
</details>

### Q2 · MCQ · Level 1

RE equivalence is

- (A) decidable  (B) undecidable  (C) RE-not-decidable  (D) not RE

<details><summary>Answer</summary>

**Answer:** (A) — convert, minimize.
</details>

### Q3 · MCQ · Level 2

CFG emptiness is

- (A) decidable (generating variables)  (B) undecidable  (C) decidable only for regular grammars  (D) the same as TM emptiness

<details><summary>Answer</summary>

**Answer:** (A).
</details>

### Q4 · MCQ · Level 2

CFG equivalence is

- (A) decidable by minimization  (B) undecidable  (C) decidable because membership is  (D) decidable because emptiness is

<details><summary>Answer</summary>

**Answer:** (B).
</details>

### Q5 · NAT · Level 2

Among: DFA empty, DFA finite, DFA equal, TM empty — how many are decidable? ____

<details><summary>Answer</summary>

**Answer:** 3.
</details>

### Q6 · MCQ · Level 3

`L(G) = Σ*` for a CFG `G` is

- (A) decidable (membership)  (B) undecidable  (C) decidable (finiteness)  (D) the same as emptiness

<details><summary>Answer</summary>

**Answer:** (B).
</details>

### Q7 · MCQ · Level 3

Decidable:

- (A) CFG finite?  (B) TM finite?  (C) `L(M)` regular?  (D) two CFGs equal?

<details><summary>Answer</summary>

**Answer:** (A).
</details>

### Q8 · MSQ · Level 3

Undecidable by Rice:

- (A) `L(M)=∅`  (B) `L(M)` finite  (C) `L(M)` regular  (D) `M` has exactly five states

<details><summary>Answer</summary>

**Answer:** (A), (B), (C).
</details>

### Q9 · MCQ · Level 3

CFG ambiguity is

- (A) decidable by checking strings up to a fixed length  (B) undecidable  (C) decidable because every CFL has an unambiguous grammar  (D) decidable in CNF

<details><summary>Answer</summary>

**Answer:** (B).
</details>

### Q10 · MCQ · Level 4

True:

- (A) every undecidable language is not RE
- (B) `A_TM` is RE but not decidable
- (C) `A_TM` is decidable but not RE
- (D) undecidable ⇒ no recognizer

<details><summary>Answer</summary>

**Answer:** (B).
</details>

### Q11 · MCQ · Level 4

TM emptiness is

- (A) decidable  (B) RE-not-decidable  (C) not RE (non-emptiness is RE-not-decidable)  (D) regular

<details><summary>Answer</summary>

**Answer:** (C).
</details>

### Q12 · MSQ · Level 4

RE but not decidable:

- (A) `A_TM`  (B) CFG non-equivalence  (C) TM emptiness  (D) TM non-emptiness

<details><summary>Answer</summary>

**Answer:** (A), (B), (D).
</details>

### Q13 · MCQ · Level 5

Universality of CFGs is undecidable. Therefore CFG equivalence is undecidable because

- (A) `L(G)=Σ*` iff `L(G)=L(G_all)` for a fixed grammar of `Σ*`
- (B) universality does not mention a second grammar, so equivalence is easier
- (C) membership is decidable
- (D) DFA universality is undecidable by the same proof

<details><summary>Answer</summary>

**Answer:** (A). (D) is false: DFA universality is emptiness of the complement.
</details>

### Q14 · MSQ · Level 5

Decidable:

- (A) `M` has ≤ 10 states
- (B) `L(M)` has ≤ 10 strings
- (C) `L(D)` has ≤ 10 strings (`D` a DFA)
- (D) `L(G)` has ≤ 10 strings (`G` a CFG)

<details><summary>Answer</summary>

**Answer:** (A), (C), (D). (B) is Rice.
</details>

### Q15 · MCQ · Level 5

`A ≤ B` means a computable `f` with `x ∈ A ⇔ f(x) ∈ B`. Valid:

- (A) `A` undecidable ⇒ `B` undecidable
- (B) `B` undecidable ⇒ `A` undecidable
- (C) `A` decidable ⇒ `B` decidable
- (D) `B` RE ⇒ `A` not RE

<details><summary>Answer</summary>

**Answer:** (A).
</details>

### Q16 · MCQ · Level 2

Accepted by a DPDA:

- (A) every regular language  (B) every CFL  (C) every NPDA language  (D) every decidable language

<details><summary>Answer</summary>

**Answer:** (A).
</details>
