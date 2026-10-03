# Turing Machines — Practice

Original questions. Not PYQs and not a copy of `14-PRACTICE-QUESTIONS`.

### Q1 · MCQ · Level 1

The unbounded resource of a TM is

- (A) the number of states  (B) the tape  (C) `Σ`  (D) the number of accept states

<details><summary>Answer</summary>

**Answer:** (B).
</details>

### Q2 · MCQ · Level 1

`M` decides `L` when

- (A) it accepts `L` and may loop outside `L`
- (B) it always halts, accepts `L`, and rejects `L̄`
- (C) it rejects every input
- (D) it has no reject state

<details><summary>Answer</summary>

**Answer:** (B).
</details>

### Q3 · MCQ · Level 2

Multi-tape TMs, as language acceptors,

- (A) accept a larger class  (B) accept exactly the RE languages  (C) accept only regular languages  (D) cannot be simulated

<details><summary>Answer</summary>

**Answer:** (B).
</details>

### Q4 · MCQ · Level 2

NTMs as language acceptors

- (A) accept some non-RE languages  (B) accept exactly the RE languages  (C) accept only decidable languages  (D) are illegal

<details><summary>Answer</summary>

**Answer:** (B).
</details>

### Q5 · MCQ · Level 2

`A_TM` is

- (A) decidable  (B) RE but not decidable  (C) not RE  (D) regular

<details><summary>Answer</summary>

**Answer:** (B).
</details>

### Q6 · NAT · Level 2

TM: `q0` start, `q_acc` accept. `δ(q0,a)=(q1,a,R)`, `δ(q1,a)=(q1,a,R)`, `δ(q1,⊔)=(q_acc,⊔,L)`, and `b` / `⊔` from `q0` reject. Moves to accept `aa`: ____.

<details><summary>Answer</summary>

**Answer:** 3 — `q0` on first `a`, `q1` on second `a`, `q1` on blank.
</details>

### Q7 · MCQ · Level 3

If `L` and `L̄` are both RE, then

- (A) `L` is decidable  (B) `L` is not RE  (C) `L̄` is not RE  (D) `L` is finite

<details><summary>Answer</summary>

**Answer:** (A).
</details>

### Q8 · MSQ · Level 3

True:

- (A) decidable languages closed under complement
- (B) RE closed under complement
- (C) RE closed under union
- (D) RE closed under intersection

<details><summary>Answer</summary>

**Answer:** (A), (C), (D).
</details>

### Q9 · MCQ · Level 4

`M` accepts exactly `L` and halts on every string in `L`. Then `L` is

- (A) necessarily decidable  (B) RE, not necessarily decidable  (C) not RE  (D) regular

<details><summary>Answer</summary>

**Answer:** (B). Halting on yes-instances is already part of acceptance.
</details>

### Q10 · MCQ · Level 4

False:

- (A) decidable ⇒ RE  (B) RE ⇒ decidable  (C) regular ⇒ decidable  (D) CFL ⇒ decidable

<details><summary>Answer</summary>

**Answer:** (B).
</details>

### Q11 · MSQ · Level 5

RE but not decidable:

- (A) `A_TM`  (B) DFA membership  (C) HALT  (D) TM emptiness

<details><summary>Answer</summary>

**Answer:** (A), (C). Emptiness is not RE. DFA membership is decidable.
</details>

### Q12 · MCQ · Level 5

`{a^n | n prime}` is

- (A) not TM-acceptable  (B) regular not CFL  (C) CFL not regular  (D) neither regular nor CFL, but decidable

<details><summary>Answer</summary>

**Answer:** (D).
</details>
