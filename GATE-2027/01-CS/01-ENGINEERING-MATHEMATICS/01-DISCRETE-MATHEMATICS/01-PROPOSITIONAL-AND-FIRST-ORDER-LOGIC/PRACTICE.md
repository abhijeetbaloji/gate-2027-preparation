# Propositional and First-Order Logic — GATE-STYLE PRACTICE

## Level 1 — Concept Check

**Q1.** How many rows in a truth table for a formula with 4 distinct propositional variables?

**Q2.** When is P→Q false?

**Q3.** What is the contrapositive of "If it rains, the match is cancelled"?

**Q4.** Is ¬(P∨Q) equivalent to ¬P∨¬Q?

**Q5.** Translate to FOL: "Every dog has a tail." (Dog(x), HasTail(x))

---

## Level 2 — Standard GATE

**Q6.** Which is logically equivalent to P→Q?
(a) Q→P  (b) ¬Q→¬P  (c) ¬P→¬Q  (d) Q∨¬P

**Q7.** Convert (P∨Q)→(P∧R) to CNF.

**Q8.** Which is a tautology?
(a) (P→Q)∨(Q→P)  (b) P∧¬P  (c) (P→Q)∧(P→¬Q)  (d) P→¬P

**Q9.** ¬∃x (Student(x) → Passed(x)) is equivalent to:
(a) ∀x (Student(x) ∧ ¬Passed(x))  (b) ∀x (¬Student(x) ∨ Passed(x))

**Q10.** Using modus tollens on premises P→Q and ¬Q, what follows?

---

## Level 3 — Multi-Step

**Q11.** Simplify: ¬(P→(Q→R)) to a formula using only ∧, ∨, ¬.

**Q12.** Apply resolution to {P∨Q∨R, ¬P∨Q, ¬Q, ¬R}. Does it derive □?

**Q13.** How many satisfying assignments does (P∨Q)∧(¬P∨Q) have?

**Q14.** Negate: ∀x ∃y (x+y=0) over reals. Write equivalent without ∀,∃ on same side.

**Q15.** Premises: P→(Q→R), P, Q. Derive R using only MP.

---

## Level 4 — Trap Questions

**Q16.** "P→Q is false" is equivalent to:
(a) ¬P∨¬Q  (b) P∧¬Q  (c) ¬P∧Q  (d) P∨¬Q

**Q17.** Which is equivalent to ∀x∃y Loves(x,y)?
(a) ∃y∀x Loves(x,y)  (b) Neither — order matters

**Q18.** (P→Q)∧(Q→P) is:
(a) tautology  (b) contradiction  (c) contingency  (d) equivalent to P↔Q

**Q19.** Valid argument P, P→Q ⊢ Q. Is P∧(P→Q)→Q a tautology?
(a) Yes  (b) No

**Q20.** CNF of ¬(P∧Q)∨R?

---

## Level 5 — Challenge

**Q21.** How many clauses in CNF of (P→Q)∧(R→S)∧(P∨R)?

**Q22.** Is ((P→Q)→P)→P (Peirce's law) a tautology? Prove or give counterexample.

**Q23.** FOL: Domain = integers. Which means "There is no largest integer"?
(a) ∀x∃y(y>x)  (b) ∃y∀x(y>x)  (c) ¬∃y∀x(y≥x)

**Q24.** Set {P∨Q, ¬P∨R, ¬Q∨R, ¬R} — satisfiable?

**Q25.** Count minimal DNF terms for P↔Q.

---

## Answers (Full Reasoning)

**A1.** 2⁴ = **16** rows.

**A2.** Only when **P=T and Q=F**.

**A3.** "If the match is not cancelled, it did not rain" (¬Q→¬P).

**A4.** **No.** ¬(P∨Q) ≡ ¬P∧¬Q (De Morgan).

**A5.** **∀x (Dog(x) → HasTail(x))**

**A6.** **(b) ¬Q→¬P** — contrapositive. (d) Q∨¬P ≡ ¬P∨Q ≡ P→Q also works — both (b) and (d). In single-answer GATE, **(b)** is the standard "contrapositive" answer; **(d)** is material equivalence form.

**A7.** ¬(P∨Q)∨(P∧R) → (¬P∧¬Q)∨(P∧R) → distribute: **(¬P∨P∧R)∧(¬Q∨P∧R)**. Further: (¬P∨R)∧(¬Q∨P)∧(¬Q∨R) after simplification — verify by case analysis.

**A8.** **(a)** — only (T,F) and (F,T) need checking; both give T. (b) contradiction; (c) forces Q and ¬Q when P; (d) false at P=T.

**A9.** ¬∃x(¬Student(x)∨Passed(x)) ≡ ∀x¬(¬Student(x)∨Passed(x)) ≡ **∀x(Student(x)∧¬Passed(x))** — answer **(a)**.

**A10.** **¬P** (modus tollens).

**A11.** ¬(P→(¬Q∨R)) ≡ P∧(Q∧¬R) = **P∧Q∧¬R**.

**A12.** ¬Q + P∨Q∨R → P∨R. ¬P∨Q + P∨R → Q∨R. ¬R + P∨R → P. ¬P∨Q + P → Q. ¬Q + Q → **□**. Yes, unsatisfiable.

**A13.** (P∨Q)∧(¬P∨Q): Q must be T. P free → **2** assignments (P=T or P=F, Q=T).

**A14.** ∃x∀y ¬(x+y=0) ≡ **∃x∀y (x+y≠0)**. Over reals this is false (take y=−x), but the negated form is correct syntactically.

**A15.** P + P→(Q→R) ⊢ Q→R (MP). Q + Q→R ⊢ **R** (MP).

**A16.** **(b) P∧¬Q** — negation of implication.

**A17.** **(b)** — ∀x∃y allows different y per x; ∃y∀x needs one y for all.

**A18.** **(d)** — equivalent to P↔Q; contingency (not always T).

**A19.** **(a) Yes** — when P∧(P→Q) is T, P and Q are T, so implication is T; when premise F, implication T vacuously.

**A20.** **(¬P∨¬Q∨R)** — single clause CNF.

**A21.** Each implication gives one clause: (¬P∨Q), (¬R∨S), (P∨R) → **3 clauses**.

**A22.** **Yes, tautology.** If P=T, conclusion T. If P=F, then P→Q=T, so (T)→F = F... wait: P=F → (P→Q)=T, (T→P)=(T→F)=F, F→F=T. If P=T,Q=F: (F→T)=T, T→T=T. If P=T,Q=T: T→T=T. **Tautology** ✓

**A23.** **(a) ∀x∃y(y>x)** — for each x, some y is larger. (c) also works: ¬∃y∀x(y≥x). Best: **(a)**.

**A24.** ¬R forces R=F. P∨Q and ¬P∨R → need P (since R=F). ¬P∨Q with P → Q. ¬Q∨R → ¬Q. Q and ¬Q — **unsatisfiable**.

**A25.** P↔Q ≡ (P∧Q)∨(¬P∧¬Q) → **2** minterms.
