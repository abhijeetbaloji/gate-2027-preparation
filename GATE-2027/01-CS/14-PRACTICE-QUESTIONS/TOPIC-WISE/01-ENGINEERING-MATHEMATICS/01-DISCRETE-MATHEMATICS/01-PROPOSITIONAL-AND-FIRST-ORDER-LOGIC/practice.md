# Propositional and First-Order Logic — Practice Questions

Original practice for GATE CS. These questions are not from any GATE paper. Attempt the questions before reading the solutions.

## Level 1 — Conceptual

## Q1 — MCQ

Which of the following is logically equivalent to \(P \rightarrow Q\)?

A. \(Q \rightarrow P\)
B. \(\neg P \lor Q\)
C. \(P \land \neg Q\)
D. \(\neg P \land Q\)

---

## Q2 — MSQ

Which of the following formulas are tautologies?

Select all that apply.

A. \((P \rightarrow Q) \lor (Q \rightarrow P)\)
B. \(P \land \neg P\)
C. \(P \rightarrow (Q \rightarrow P)\)
D. \((P \lor Q) \rightarrow (P \land Q)\)

---

## Q3 — NAT

The formula \((P \rightarrow Q) \land (\neg R \lor P)\) contains three distinct propositional variables. Enter the number of rows in its complete truth table.

---

## Q4 — MCQ

Which formula is logically equivalent to \(\neg(P \rightarrow Q)\)?

A. \(\neg P \rightarrow \neg Q\)
B. \(P \land \neg Q\)
C. \(\neg P \lor \neg Q\)
D. \(\neg P \land \neg Q\)

---

## Q5 — MCQ

Let the domain be the set of all people. \(\mathrm{Intern}(x)\) means \(x\) is an intern, and \(\mathrm{Badge}(x)\) means \(x\) receives a badge. Which formula expresses “Every intern receives a badge”?

A. \(\forall x\,(\mathrm{Intern}(x) \rightarrow \mathrm{Badge}(x))\)
B. \(\forall x\,(\mathrm{Intern}(x) \land \mathrm{Badge}(x))\)
C. \(\exists x\,(\mathrm{Intern}(x) \land \mathrm{Badge}(x))\)
D. \(\forall x\,(\mathrm{Badge}(x) \rightarrow \mathrm{Intern}(x))\)

---

## Level 2 — Standard GATE Style

## Q6 — MCQ

The contrapositive of \(\neg P \rightarrow Q\) is

A. \(Q \rightarrow \neg P\)
B. \(\neg Q \rightarrow P\)
C. \(P \rightarrow \neg Q\)
D. \(\neg Q \rightarrow \neg P\)

---

## Q7 — NAT

Enter the number of truth assignments to \((P, Q, R)\) that satisfy
\[
(P \lor \neg Q) \land (Q \lor \neg R) \land R.
\]

---

## Q8 — MSQ

Which of the following equivalences hold for every truth assignment?

Select all that apply.

A. \(\neg(P \land Q) \equiv \neg P \lor \neg Q\)
B. \(P \rightarrow Q \equiv \neg Q \rightarrow \neg P\)
C. \(\neg(P \rightarrow Q) \equiv \neg P \lor \neg Q\)
D. \(P \leftrightarrow Q \equiv (P \rightarrow Q) \land (Q \rightarrow P)\)

---

## Q9 — MCQ

Which of the following is a CNF formula logically equivalent to \(P \rightarrow (Q \land R)\)?

A. \((\neg P \lor Q) \land (\neg P \lor R)\)
B. \((\neg P \land \neg Q) \lor R\)
C. \((P \lor Q) \land (P \lor R)\)
D. \(\neg P \lor \neg Q \lor \neg R\)

---

## Q10 — NAT

Enter the number of truth assignments to \((P, Q, R)\) that satisfy \(P \leftrightarrow (Q \lor R)\).

---

## Q11 — MCQ

From the premises \(\neg R\) and \((P \land Q) \rightarrow R\), which conclusion follows by one application of modus tollens?

A. \(P \land Q\)
B. \(\neg(P \land Q)\)
C. \(R\)
D. \(P \rightarrow Q\)

---

## Q12 — MCQ

Which formula is logically equivalent to \(\neg \exists x\,\forall y\,\mathrm{Linked}(x,y)\)?

A. \(\forall x\,\exists y\,\neg\mathrm{Linked}(x,y)\)
B. \(\exists x\,\forall y\,\neg\mathrm{Linked}(x,y)\)
C. \(\forall x\,\forall y\,\neg\mathrm{Linked}(x,y)\)
D. \(\exists x\,\exists y\,\neg\mathrm{Linked}(x,y)\)

---

## Level 3 — Multi-Step

## Q13 — NAT

Enter the number of truth assignments to \((P, Q, R)\) that satisfy
\[
(P \rightarrow Q) \land (Q \rightarrow R) \land (R \rightarrow P).
\]

---

## Q14 — MCQ

Consider the clauses \(L \lor M\), \(\neg L \lor N\), and \(\neg N\). Resolving \(L \lor M\) with \(\neg L \lor N\) produces

A. \(M \lor N\)
B. \(L \lor N\)
C. \(\neg M\)
D. the empty clause

---

## Q15 — MSQ

Which of the following inferences are valid?

Select all that apply.

A. From \(P \rightarrow Q\) and \(Q \rightarrow R\), infer \(P \rightarrow R\).
B. From \(P \rightarrow Q\) and \(Q\), infer \(P\).
C. From \(P \lor Q\) and \(\neg P\), infer \(Q\).
D. From \(P \rightarrow Q\) and \(\neg P\), infer \(\neg Q\).

---

## Q16 — MCQ

Which formula is logically equivalent to \((\neg P \land Q) \lor (P \land \neg Q)\)?

A. \(P \leftrightarrow Q\)
B. \(\neg(P \leftrightarrow Q)\)
C. \(P \rightarrow Q\)
D. \(P \land Q\)

---

## Q17 — MSQ

Let the domain be the set of campus printers. \(\mathrm{Online}(x)\) means printer \(x\) is online, and \(\mathrm{Ready}(x)\) means printer \(x\) is ready. Which formulas correctly express “Every online printer is ready”?

Select all that apply.

A. \(\forall x\,(\mathrm{Online}(x) \rightarrow \mathrm{Ready}(x))\)
B. \(\neg \exists x\,(\mathrm{Online}(x) \land \neg\mathrm{Ready}(x))\)
C. \(\forall x\,(\mathrm{Online}(x) \land \mathrm{Ready}(x))\)
D. \(\exists x\,(\mathrm{Online}(x) \rightarrow \mathrm{Ready}(x))\)

---

## Level 4 — Tricky / Trap-Based

## Q18 — MCQ

Consider the assignment where \(P\) is false and \(Q\) is true. Which statement is correct?

A. Both \(\neg(P \rightarrow Q)\) and \(\neg P \lor \neg Q\) are true.
B. Both \(\neg(P \rightarrow Q)\) and \(\neg P \lor \neg Q\) are false.
C. \(\neg(P \rightarrow Q)\) is false, and \(\neg P \lor \neg Q\) is true.
D. \(\neg(P \rightarrow Q)\) is true, and \(\neg P \lor \neg Q\) is false.

---

## Q19 — MSQ

Which of the following statements are true?

Select all that apply.

A. Every tautology is satisfiable.
B. Every contradiction is satisfiable.
C. Every contingency is satisfiable, and no contingency is a tautology.
D. If the inference “from these premises, conclude \(\psi\)” is valid, then the conjunction of those premises is a tautology.

---

## Q20 — NAT

Operator precedence is \(\neg\), then \(\land\), then \(\lor\), then \(\rightarrow\), then \(\leftrightarrow\). Under that precedence, \(\neg P \lor Q \land R\) means \((\neg P) \lor (Q \land R)\). Enter the number of truth assignments to \((P, Q, R)\) that make this formula true.

---

## Q21 — MCQ

The domain is \(\{1,2\}\), and the only true atoms of \(\mathrm{Knows}\) are \(\mathrm{Knows}(1,1)\) and \(\mathrm{Knows}(2,2)\). Which statement is correct?

A. \(\forall x\,\exists y\,\mathrm{Knows}(x,y)\) is true, and \(\exists y\,\forall x\,\mathrm{Knows}(x,y)\) is false.
B. Both formulas are false.
C. Both formulas are true.
D. \(\forall x\,\exists y\,\mathrm{Knows}(x,y)\) is false, and \(\exists y\,\forall x\,\mathrm{Knows}(x,y)\) is true.

---

## Level 5 — Challenge

## Q22 — NAT

Enter the number of truth assignments to \((P, Q, R)\) that satisfy
\[
(P \lor Q \lor R) \land (\neg P \lor \neg Q) \land (\neg Q \lor \neg R) \land (\neg R \lor \neg P).
\]

---

## Q23 — MCQ

The inference “from \(P\) and \(P \rightarrow Q\), conclude \(Q\)” is valid. Which formula is a tautology that packages this inference?

A. \(P \land (P \rightarrow Q) \land Q\)
B. \((P \land (P \rightarrow Q)) \rightarrow Q\)
C. \(P \rightarrow (P \rightarrow Q)\)
D. \((P \rightarrow Q) \rightarrow Q\)

---

## Q24 — MSQ

Which formulas are logically equivalent to the negation of the following sentence?

\[
\forall x\,(\mathrm{Coder}(x) \rightarrow \exists y\,(\mathrm{Repo}(y) \land \mathrm{Owns}(x,y)))
\]

Select all that apply.

A. \(\exists x\,(\mathrm{Coder}(x) \land \forall y\,(\mathrm{Repo}(y) \rightarrow \neg\mathrm{Owns}(x,y)))\)
B. \(\exists x\,(\mathrm{Coder}(x) \land \neg\exists y\,(\mathrm{Repo}(y) \land \mathrm{Owns}(x,y)))\)
C. \(\forall x\,(\mathrm{Coder}(x) \land \neg\exists y\,(\mathrm{Repo}(y) \land \mathrm{Owns}(x,y)))\)
D. \(\exists x\,(\neg\mathrm{Coder}(x) \lor \forall y\,\neg\mathrm{Owns}(x,y))\)

---

## Answer Key

| Q | Type | Answer |
|---|------|--------|
| 1 | MCQ | B |
| 2 | MSQ | A, C |
| 3 | NAT | 8 |
| 4 | MCQ | B |
| 5 | MCQ | A |
| 6 | MCQ | B |
| 7 | NAT | 1 |
| 8 | MSQ | A, B, D |
| 9 | MCQ | A |
| 10 | NAT | 4 |
| 11 | MCQ | B |
| 12 | MCQ | A |
| 13 | NAT | 2 |
| 14 | MCQ | A |
| 15 | MSQ | A, C |
| 16 | MCQ | B |
| 17 | MSQ | A, B |
| 18 | MCQ | C |
| 19 | MSQ | A, C |
| 20 | NAT | 5 |
| 21 | MCQ | A |
| 22 | NAT | 3 |
| 23 | MCQ | B |
| 24 | MSQ | A, B |

## Detailed Solutions

### Q1

Answer: B

The defining rewrite of implication is \(P \rightarrow Q \equiv \neg P \lor Q\). The implication is false only in the row \(P\) true and \(Q\) false, and \(\neg P \lor Q\) fails in exactly that row.

A is the converse \(Q \rightarrow P\). The row \(P\) false and \(Q\) true makes the converse false while \(P \rightarrow Q\) stays true, so they are not equivalent.

C is \(P \land \neg Q\), which is the negation of \(P \rightarrow Q\), not the implication itself.

D is true only when \(P\) is false and \(Q\) is true. It fails on the row where both are true, while \(P \rightarrow Q\) holds there.

### Q2

Answer: A, C

A is a tautology. In every row at least one of \(P \rightarrow Q\) and \(Q \rightarrow P\) is true. The only row that looks risky is \(P\) true and \(Q\) false: the first implication is false, but \(Q \rightarrow P\) is true, so the disjunction is true. The other three rows make both implications true.

C rewrites as \(\neg P \lor \neg Q \lor P\). The complementary pair \(P\) and \(\neg P\) makes the disjunction true in every row, so \(P \rightarrow (Q \rightarrow P)\) is a tautology.

B is false in every row. It is a contradiction, not a tautology.

D fails when \(P\) is true and \(Q\) is false: the antecedent \(P \lor Q\) is true and the consequent \(P \land Q\) is false, so the implication is false. It is a contingency.

### Q3

Answer: 8

A complete truth table has one row for each assignment of the distinct variables. With three variables there are \(2^3 = 8\) rows. The connectives inside the formula do not remove rows; they only fill the output column. Using \(2^2 = 4\) would be right only for a formula in two variables, and \(3^2 = 9\) confuses binary truth values with a product of the variable count.

### Q4

Answer: B

Start from \(P \rightarrow Q \equiv \neg P \lor Q\). Negate both sides and apply De Morgan:
\[
\neg(P \rightarrow Q) \equiv \neg(\neg P \lor Q) \equiv \neg(\neg P) \land \neg Q \equiv P \land \neg Q.
\]
The implication fails only when \(P\) is true and \(Q\) is false, which is exactly when \(P \land \neg Q\) is true.

A is the inverse of \(P \rightarrow Q\). It is equivalent to the converse, not to the negation. On the row both true, \(P \rightarrow Q\) is true so its negation is false, while \(\neg P \rightarrow \neg Q\) is true.

C is true on three of the four rows, including every row where \(P\) is false. On those rows \(P \rightarrow Q\) is already true, so its negation is false. C is the mistake of negating the two sides and joining them with \(\lor\).

D is true only when both are false. There \(P \rightarrow Q\) is true, so the negation is false.

### Q5

Answer: A

“Every intern receives a badge” restricts the claim to interns and then asserts the badge property. The universal quantifier with an implication does that: if \(x\) is an intern, then \(x\) receives a badge. Anyone who is not an intern makes the implication true and does not create a counterexample.

B says every person in the domain is an intern and also receives a badge. That is much stronger than the English sentence.

C says at least one intern receives a badge. That is an existential claim, not a universal one.

D reverses the direction. It says that badge holders are interns, which does not force every intern to receive a badge.

### Q6

Answer: B

The contrapositive of \(\alpha \rightarrow \beta\) is \(\neg\beta \rightarrow \neg\alpha\), and it is the conditional equivalent to the original. Here \(\alpha\) is \(\neg P\) and \(\beta\) is \(Q\), so
\[
\neg\beta \rightarrow \neg\alpha \equiv \neg Q \rightarrow \neg(\neg P) \equiv \neg Q \rightarrow P.
\]
Both sides equal \(P \lor Q\): the original is \(\neg(\neg P) \lor Q \equiv P \lor Q\), and \(\neg Q \rightarrow P\) is \(Q \lor P\).

A is the converse of the original formula. \(Q \rightarrow \neg P\) equals \(\neg Q \lor \neg P\), which fails when both \(P\) and \(Q\) are true, while \(\neg P \rightarrow Q\) holds in that row.

C is \(P \rightarrow \neg Q \equiv \neg P \lor \neg Q\). The same row, both true, separates it from \(\neg P \rightarrow Q\).

D is \(\neg Q \rightarrow \neg P \equiv Q \lor \neg P\). This is the contrapositive of \(P \rightarrow Q\), not of \(\neg P \rightarrow Q\). On the row where \(P\) and \(Q\) are both false, the original formula \(\neg P \rightarrow Q\) is false, while D is \(\neg\mathrm{false} \rightarrow \neg\mathrm{false}\), which is true.

### Q7

Answer: 1

The third conjunct forces \(R\) to be true. Substitute that into the second conjunct: \(Q \lor \neg R\) becomes \(Q \lor \mathrm{false}\), so \(Q\) is true. Substitute into the first conjunct: \(P \lor \neg Q\) becomes \(P \lor \mathrm{false}\), so \(P\) is true. The only surviving assignment is \((P,Q,R) = (\mathrm{true},\mathrm{true},\mathrm{true})\).

Checking that row: \(P \lor \neg Q\) is true, \(Q \lor \neg R\) is true, and \(R\) is true. Any other row kills at least one conjunct. In particular, leaving \(Q\) free after fixing \(R\) would count two rows, but the second conjunct does not leave \(Q\) free.

### Q8

Answer: A, B, D

A is De Morgan’s law for conjunction: an element fails to satisfy both atoms exactly when it fails the first or fails the second.

B is contraposition. Both sides rewrite to \(\neg P \lor Q\).

D is the definition of the biconditional: each direction of the implication must hold.

C is false. The correct negation is \(P \land \neg Q\). The assignment \(P\) false and \(Q\) true makes \(\neg(P \rightarrow Q)\) false, because the implication is true, while \(\neg P \lor \neg Q\) is true.

### Q9

Answer: A

Rewrite the implication and distribute:
\[
P \rightarrow (Q \land R) \equiv \neg P \lor (Q \land R) \equiv (\neg P \lor Q) \land (\neg P \lor R).
\]
The last formula is a conjunction of disjunctions of literals, so it is in CNF, and the algebra shows it is equivalent to the original.

B is not in CNF: a conjunction still sits inside a disjunction. It is also not equivalent to the target. On the row \(P\) true, \(Q\) false, and \(R\) true, the target \(P \rightarrow (Q \land R)\) is false, and option A is \((\mathrm{false} \lor \mathrm{false}) \land (\mathrm{false} \lor \mathrm{true}) = \mathrm{false}\). Option B is \((\mathrm{false} \land \mathrm{true}) \lor \mathrm{true} = \mathrm{true}\).

C keeps \(P\) unnegated. On the row \(P\) false, \(Q\) false, \(R\) false, the target implication is true, but C is false.

D is one clause. On the row all three true, D is false, while \(P \rightarrow (Q \land R)\) is true.

### Q10

Answer: 4

\(P \leftrightarrow (Q \lor R)\) holds exactly when \(P\) equals the truth value of \(Q \lor R\).

- If \(Q\) and \(R\) are both false, then \(Q \lor R\) is false, so \(P\) must be false. One assignment.
- If \(Q\) is true and \(R\) is false, then \(Q \lor R\) is true, so \(P\) must be true. One assignment.
- If \(Q\) is false and \(R\) is true, then \(P\) must be true. One assignment.
- If \(Q\) and \(R\) are both true, then \(P\) must be true. One assignment.

That is \(1+1+1+1 = 4\). The three rows in which \(Q \lor R\) is true do not each split into two choices of \(P\); \(P\) is forced. Counting all \(2^3 = 8\) rows, or only the three rows where \(Q \lor R\) is true, misses the matching requirement on \(P\).

### Q11

Answer: B

Modus tollens says: from \(\neg\beta\) and \(\alpha \rightarrow \beta\), infer \(\neg\alpha\). Take \(\alpha\) to be \(P \land Q\) and \(\beta\) to be \(R\). The premises are exactly \(\neg\beta\) and \(\alpha \rightarrow \beta\), so the conclusion is \(\neg(P \land Q)\).

A affirms the antecedent that tollens is denying. C contradicts the premise \(\neg R\). D is not the negated antecedent; modus tollens returns the negation of the whole antecedent \(P \land Q\), which is \(\neg P \lor \neg Q\), not the new implication \(P \rightarrow Q\).

### Q12

Answer: A

Negation pushes inward by flipping each quantifier and negating the matrix at the end:
\[
\neg\exists x\,\forall y\,\mathrm{Linked}(x,y)
\equiv \forall x\,\neg\forall y\,\mathrm{Linked}(x,y)
\equiv \forall x\,\exists y\,\neg\mathrm{Linked}(x,y).
\]

B flips only the predicate and leaves the quantifier prefix in the original order. That is equivalent to \(\neg\forall x\,\exists y\,\mathrm{Linked}(x,y)\), a different sentence.

C negates the predicate but turns both quantifiers universal. That says every pair fails \(\mathrm{Linked}\), which is stronger than “there is no element related to every element.”

D flips both quantifiers to existential. That says some pair fails \(\mathrm{Linked}\), which is weaker than the negated sentence.

### Q13

Answer: 2

The three implications form a cycle, so \(P\), \(Q\), and \(R\) must share one truth value.

If \(P\) is true, then \(P \rightarrow Q\) forces \(Q\) true, and \(Q \rightarrow R\) forces \(R\) true. The remaining implication \(R \rightarrow P\) holds. This gives the assignment all true.

If \(P\) is false, then \(R \rightarrow P\) forces \(R\) false, and \(Q \rightarrow R\) forces \(Q\) false. The remaining implication \(P \rightarrow Q\) holds because its antecedent is false. This gives the assignment all false.

Every mixed assignment breaks the cycle. For example, true, true, false fails \(Q \rightarrow R\), and false, true, false fails \(Q \rightarrow R\) as well. So there are exactly two models. Stopping after \(P \rightarrow Q\) and \(Q \rightarrow R\), without \(R \rightarrow P\), would leave extra models such as false, false, true.

### Q14

Answer: A

Resolution needs complementary literals. \(L \lor M\) and \(\neg L \lor N\) contain \(L\) and \(\neg L\). Delete that complementary pair and disjoin the remaining literals:
\[
(L \lor M),\ (\neg L \lor N) \vdash M \lor N.
\]
The third clause \(\neg N\) is not used in this one step. Resolving \(M \lor N\) further with \(\neg N\) would give \(M\), and that is a later step, not the resolvent asked for.

B still contains \(L\) and drops \(M\), so it is not the resolvent of this pair. C would require resolving on \(M\), but the second clause has no \(\neg M\). D, the empty clause, is the result of resolving a literal with its complement when nothing else remains, as in \(N\) with \(\neg N\). These two clauses leave \(M\) and \(N\).

### Q15

Answer: A, C

A is hypothetical syllogism. From \(P \rightarrow Q \equiv \neg P \lor Q\) and \(Q \rightarrow R \equiv \neg Q \lor R\), the chain yields \(\neg P \lor R\), that is \(P \rightarrow R\). Whenever both premises are true, the conclusion is true.

C is disjunctive syllogism. If \(P \lor Q\) is true and \(P\) is false, the truth of the disjunction must come from \(Q\).

B affirms the consequent. The assignment \(P\) false and \(Q\) true makes \(P \rightarrow Q\) true and \(Q\) true, while \(P\) is false. The premises hold and the claimed conclusion does not.

D denies the antecedent. The same assignment \(P\) false and \(Q\) true makes \(P \rightarrow Q\) and \(\neg P\) true, while \(\neg Q\) is false.

### Q16

Answer: B

Build the four rows of \((\neg P \land Q) \lor (P \land \neg Q)\):

| \(P\) | \(Q\) | formula |
|---|---|---|
| T | T | false |
| T | F | true |
| F | T | true |
| F | F | false |

\(P \leftrightarrow Q\) is true precisely on the first and last rows, so its negation matches the table. The displayed formula is the exclusive-or of \(P\) and \(Q\).

A has the opposite column: true, false, false, true. C, namely \(P \rightarrow Q\), is true, false, true, true. It matches the displayed formula only on some rows. D is true only on the first row, where the displayed formula is false.

### Q17

Answer: A, B

A is the direct translation: for every printer, being online implies being ready.

B rewrites A by quantifier negation and the negation of an implication. The negation of A is \(\exists x\,(\mathrm{Online}(x) \land \neg\mathrm{Ready}(x))\), so the negation of that existential sentence is A again. Thus B is equivalent to A and matches the English sentence.

C says every printer is online and ready. A printer that is offline is a counterexample to C even when every online printer is ready.

D only asserts that some printer satisfies an implication. An offline printer makes \(\mathrm{Online}(x) \rightarrow \mathrm{Ready}(x)\) true, so D can hold when some other online printer is not ready. Existence and a bare implication do not express “every.”

### Q18

Answer: C

On \(P\) false and \(Q\) true, the implication \(P \rightarrow Q\) has a false antecedent, so it is true. Therefore \(\neg(P \rightarrow Q)\) is false. The other formula is \(\neg P \lor \neg Q = \mathrm{true} \lor \mathrm{false} = \mathrm{true}\).

This is the row that exposes the mistake of writing \(\neg(P \rightarrow Q)\) as \(\neg P \lor \neg Q\). The correct negation \(P \land \neg Q\) is false here, in agreement with \(\neg(P \rightarrow Q)\).

A says both are true, but the negated implication is false. B says both are false, but \(\neg P \lor \neg Q\) is true. D swaps the two truth values.

### Q19

Answer: A, C

A tautology is true on every row, so it is true on at least one row. Every tautology is satisfiable, and A is true.

A contingency is true on at least one row and false on at least one row. It is satisfiable, and it is not a tautology. C is true.

B is false. A contradiction, such as \(P \land \neg P\), is false on every row, so it is not satisfiable.

D confuses a valid inference with a tautology. The inference “from \(P\), conclude \(P\)” is valid, but the single premise \(P\) is not a tautology. The tautology associated with a valid inference is the implication whose antecedent is the conjunction of the premises and whose consequent is the conclusion. That implication can be a tautology while the premises themselves are not.

### Q20

Answer: 5

Precedence makes the formula \((\neg P) \lor (Q \land R)\).

If \(P\) is false, \(\neg P\) is true, so the disjunction is true for all four combinations of \(Q\) and \(R\).

If \(P\) is true, \(\neg P\) is false, so \(Q \land R\) must be true. That forces \(Q\) true and \(R\) true: one further assignment.

The total is \(4 + 1 = 5\).

Reading the formula as \((\neg P \lor Q) \land R\) is a different formula. It requires \(R\) true, and then \(\neg P \lor Q\): three assignments, namely \((P,Q,R)\) equal to (false, false, true), (false, true, true), and (true, true, true). That parse treats \(\lor\) as tighter than \(\land\), which contradicts the stated precedence.

### Q21

Answer: A

Check \(\forall x\,\exists y\,\mathrm{Knows}(x,y)\). For \(x = 1\), the witness \(y = 1\) works. For \(x = 2\), the witness \(y = 2\) works. The universal-existential sentence is true. The witness is allowed to depend on \(x\).

Check \(\exists y\,\forall x\,\mathrm{Knows}(x,y)\). This asks for one \(y\) known by every element. If \(y = 1\), then \(\mathrm{Knows}(2,1)\) is false. If \(y = 2\), then \(\mathrm{Knows}(1,2)\) is false. The existential-universal sentence is false.

B says the first sentence is false. C says the second sentence is true. D reverses both truth values. The two sentences are not equivalent: the order of the quantifiers changes whether the witness may depend on \(x\).

### Q22

Answer: 3

The clause \(\neg P \lor \neg Q\) forbids \(P\) and \(Q\) from being true together. \(\neg Q \lor \neg R\) forbids \(Q\) and \(R\) together. \(\neg R \lor \neg P\) forbids \(R\) and \(P\) together. Therefore at most one of \(P\), \(Q\), and \(R\) is true.

The clause \(P \lor Q \lor R\) forbids the assignment where all three are false. Therefore at least one is true.

The assignments with exactly one variable true satisfy every clause:

- \((true, false, false)\): the big disjunction holds, and each binary clause contains a false literal’s negation, hence a true literal.
- \((false, true, false)\) and \((false, false, true)\) work the same way.

There are 3 such assignments. All false fails \(P \lor Q \lor R\). Any assignment with two or more variables true fails the clause that covers that pair. Counting \(2^3 - 1 = 7\) only removes the all-false row and leaves the illegal double-true rows.

### Q23

Answer: B

An inference is valid when every assignment that makes all the premises true also makes the conclusion true. Packaging that statement as a single formula gives
\[
(P \land (P \rightarrow Q)) \rightarrow Q.
\]
This formula is a tautology: if the antecedent is true, then \(P\) is true and \(P \rightarrow Q\) is true, so modus ponens yields \(Q\), and the implication holds. If the antecedent is false, the implication holds outright.

A is the conjunction of the premises with the conclusion. It is false whenever \(P\) is false, so it is not a tautology. Validity does not claim that the premises are always true.

C is \(P \rightarrow (P \rightarrow Q) \equiv \neg P \lor \neg P \lor Q \equiv \neg P \lor Q\), which is just \(P \rightarrow Q\). The row \(P\) true and \(Q\) false makes it false.

D fails when \(Q\) is false and \(P\) is false: \(P \rightarrow Q\) is true, and a true antecedent with false consequent makes D false.

### Q24

Answer: A, B

Let \(\varphi\) be \(\forall x\,(\mathrm{Coder}(x) \rightarrow \exists y\,(\mathrm{Repo}(y) \land \mathrm{Owns}(x,y)))\). Negate the universal quantifier, then negate the implication:
\begin{align*}
\neg\varphi
&\equiv \exists x\,\neg(\mathrm{Coder}(x) \rightarrow \exists y\,(\mathrm{Repo}(y) \land \mathrm{Owns}(x,y))) \\
&\equiv \exists x\,(\mathrm{Coder}(x) \land \neg\exists y\,(\mathrm{Repo}(y) \land \mathrm{Owns}(x,y))).
\end{align*}
That is B. Push the remaining negation inward:
\[
\neg\exists y\,(\mathrm{Repo}(y) \land \mathrm{Owns}(x,y))
\equiv \forall y\,(\neg\mathrm{Repo}(y) \lor \neg\mathrm{Owns}(x,y))
\equiv \forall y\,(\mathrm{Repo}(y) \rightarrow \neg\mathrm{Owns}(x,y)).
\]
Substituting this into B produces A. So A and B are the same sentence, and both are \(\neg\varphi\). In words: some coder owns no repository.

C changes the outer quantifier to \(\forall\). It says every domain element is a coder who owns no repository. One coder who does own a repository makes C false while B can still be true because of a different coder.

D drops \(\mathrm{Repo}\) and uses a disjunction with \(\neg\mathrm{Coder}(x)\). A domain element who is not a coder satisfies D even when every coder owns a repository, so D can be true while \(\varphi\) is true. D is not the negation.
