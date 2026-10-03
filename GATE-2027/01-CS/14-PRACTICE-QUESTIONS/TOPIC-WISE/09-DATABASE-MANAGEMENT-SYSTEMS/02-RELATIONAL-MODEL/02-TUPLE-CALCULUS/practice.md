# Tuple Calculus — Practice Questions

Original practice for GATE CS. These questions are not from any GATE paper. Attempt the questions before reading the solutions.

Tuple relational calculus is interpreted with set semantics. A query is safe when every value in its result is taken from the active domain of the database instance: each free tuple variable that contributes to the result is range-restricted by a positive membership test.

Questions that mention Device use this instance.

Device(Did, Lab, Power)

| Did | Lab | Power |
|-----|-----|-------|
| D1 | North | 30 |
| D2 | North | 45 |
| D3 | South | 45 |
| D4 | South | 10 |
| D5 | East | 30 |

## Level 1 — Conceptual

## Q1 — MCQ

In tuple relational calculus, a tuple variable

A. ranges over tuples of a relation named in the formula, once it is bound by a membership atom
B. ranges over single attribute values, never over whole tuples
C. must appear in the result even when it is bound by a quantifier
D. is legal only if the formula contains no quantifier

---

## Q2 — MCQ

Which formula is unsafe?

A. {d | d ∈ Device ∧ d.Power > 20}
B. {d | ¬(d ∈ Device)}
C. {d.Did | d ∈ Device ∧ d.Lab = 'East'}
D. {d.Lab | d ∈ Device ∧ d.Power = 10}

---

## Q3 — MCQ

"The Did of every device that shares its lab with at least one different device" is expressed with

A. an existential quantifier and an inequality on Did
B. a universal quantifier and no inequality
C. a negation wrapped around the whole of Device, with no positive membership atom on the result variable
D. division written inside the calculus formula as the symbol ÷

---

## Level 2 — Standard GATE Style

## Q4 — NAT

How many tuples are in {d.Did | d ∈ Device ∧ d.Power ≥ 45}? ______

---

## Q5 — MCQ

Which formula returns exactly {D1, D2, D3, D4}?

A. {d.Did | d ∈ Device ∧ ∃e (e ∈ Device ∧ e.Lab = d.Lab ∧ e.Did ≠ d.Did)}
B. {d.Did | d ∈ Device ∧ ∃e (e ∈ Device ∧ e.Lab = d.Lab)}
C. {d.Did | d ∈ Device ∧ ∀e (e ∈ Device → e.Lab = d.Lab)}
D. {d.Did | ∃e (e ∈ Device ∧ e.Lab = d.Lab ∧ e.Did ≠ d.Did)}

---

## Q6 — MSQ

Which formulas are safe? Select all that apply.

A. {d | d ∈ Device ∧ d.Power > 20}
B. {d | ¬(d ∈ Device)}
C. {d | ∀e (e ∈ Device → d.Power ≥ e.Power)}
D. {d.Lab | d ∈ Device ∧ d.Power = 10}

---

## Level 3 — Multi-Step

## Q7 — NAT

How many distinct labs are returned by

{d.Lab | d ∈ Device ∧ ∀e ((e ∈ Device ∧ e.Lab = d.Lab) → e.Power ≥ 30)}?

______

---

## Q8 — MCQ

Which tuple-calculus formula is equivalent to π_{Did}(σ_{Power ≥ 45}(Device))?

A. {d.Did | d ∈ Device ∧ d.Power ≥ 45}
B. {d.Did | d ∈ Device ∨ d.Power ≥ 45}
C. {e.Power | e ∈ Device ∧ e.Power ≥ 45}
D. {d.Did | ∀e (e ∈ Device ∧ e.Power ≥ 45)}

---

## Level 4 — Tricky / Trap-Based

## Q9 — MCQ

What is true of {d.Did | ∃e (e ∈ Device ∧ e.Power > 40)}?

A. It safely returns {D2, D3}
B. It is unsafe, because the result variable d is not range-restricted
C. It safely returns every Did in Device
D. It safely returns the empty set, because d and e are different variables

---

## Q10 — MSQ

Which formulas safely return the Did values of devices whose power is greater than or equal to the power of every device? On this instance those devices are D2 and D3. Select all that apply.

A. {d.Did | d ∈ Device ∧ ∀e (e ∈ Device → e.Power ≤ d.Power)}
B. {d.Did | ∀e (e ∈ Device → e.Power ≤ d.Power)}
C. {d.Did | d ∈ Device ∧ ¬∃e (e ∈ Device ∧ e.Power > d.Power)}
D. {d.Did | d ∈ Device ∧ ∀e (e ∈ Device ∧ e.Power ≤ d.Power)}

---

## Level 5 — Challenge

## Q11 — NAT

How many values are returned by

{d.Did | d ∈ Device ∧ d.Lab ≠ 'East' ∧ ∀e ((e ∈ Device ∧ e.Lab = 'East') → d.Power > e.Power)}?

______

---

## Q12 — MCQ

A formula is meant to say "every device in lab South has power below 40". Which writing is the safe and correct pattern?

A. ∀e ((e ∈ Device ∧ e.Lab = 'South') → e.Power < 40), with the result variable separately restricted by membership in Device
B. ∀e (e ∈ Device ∧ e.Lab = 'South' ∧ e.Power < 40), used as a restriction on an unrestricted result variable
C. ∀e (e ∈ Device → e.Lab = 'South' ∧ e.Power < 40)
D. ¬∃e (e ∈ Device), conjoined with a comparison of constants 10 < 40

---

## Answer Key

| Q | Type | Answer |
|---|------|--------|
| 1 | MCQ | A |
| 2 | MCQ | B |
| 3 | MCQ | A |
| 4 | NAT | 2 |
| 5 | MCQ | A |
| 6 | MSQ | A, D |
| 7 | NAT | 2 |
| 8 | MCQ | A |
| 9 | MCQ | B |
| 10 | MSQ | A, C |
| 11 | NAT | 2 |
| 12 | MCQ | A |

## Detailed Solutions

### Q1

Answer: A

A tuple variable stands for a whole tuple. The atom d ∈ Device restricts d to the tuples actually stored in Device. Attributes are then read with d.Did, d.Lab, and d.Power. B describes domain calculus more than tuple calculus. A quantified variable is not automatically part of the result; the result is the tuple, or the components, written before the vertical bar, so C fails. Quantifiers are the usual way to express join-like and "for all" conditions, so D fails.

### Q2

Answer: B

B says "every tuple that is not in Device". Nothing ties d to the active domain, and infinitely many tuples outside Device satisfy the formula. That query is unsafe.

A restricts d by d ∈ Device before using d.Power. C and D do the same, and their results are finite: C returns D5, and D returns the lab South.

### Q3

Answer: A

Sharing a lab means there exists another tuple in the same lab with a different Did. That is ∃ together with an inequality. A universal quantifier would say something about every device, which is a different claim, so B fails. C is the unsafe pattern of Q2. The division symbol is an algebra operator, not a tuple-calculus connective, so D fails.

### Q4

Answer: 2

The powers that are at least 45 are D2 (North, 45) and D3 (South, 45). D1 and D5 have power 30, and D4 has power 10. The result set is {D2, D3}.

### Q5

Answer: A

North contains D1 and D2, South contains D3 and D4, and East contains only D5. A device is kept when some other device has the same lab. That drops D5 and keeps D1, D2, D3, and D4.

B is true for every device, including D5, because each device is a witness for its own lab. The missing inequality is the trap. C keeps a device only if every device in the whole relation is in its lab. No lab contains all five devices, so C is empty. D never range-restricts d. The variable d appears in e.Lab = d.Lab and in the result, but d ∈ Device is absent, so D is unsafe and is not the finite set {D1, D2, D3, D4}.

### Q6

Answer: A, D

A and D both bind the result variable with d ∈ Device, and every output component is copied from that tuple. They are safe. D returns {South}.

B is the complement of Device and is unsafe. C compares d.Power with every device, but d itself is never required to be a tuple of Device. Any imaginary tuple with a huge Power component would qualify, so C is unsafe. The safe version of C adds d ∈ Device, which is the repair used in Q10.

### Q7

Answer: 2

The formula keeps a lab when every device in that lab has power at least 30.

- North: 30 and 45, both at least 30. Kept.
- South: 45 and 10. The device of power 10 fails the test. Rejected.
- East: 30, which is at least 30. Kept.

The distinct labs are North and East. The count is 2, not 3. South is the trap of checking only the maximum device in the lab.

The implication matters. For a device e in a different lab, e.Lab = d.Lab is false, so the implication is true and that e does not spoil the lab. The universal quantifier is therefore local to the lab.

### Q8

Answer: A

The algebra expression keeps Did of those Device tuples whose Power is at least 45. That is exactly A, and on this instance it returns {D2, D3}.

B uses disjunction. A tuple of Device would qualify even with a small power, because d ∈ Device would already be true. C returns powers, not Did values, so the result schema differs. D universally quantifies a conjunction. It demands that every tuple e, whether or not it is the result tuple, belong to Device and have power at least 45. That is not the selection, and it does not range-restrict a separate result variable in a useful way.

### Q9

Answer: B

The only membership atom binds e. The result component is d.Did, and d is free and never required to belong to Device. The formula does not define a finite set of Did values drawn from the database. It is unsafe.

A is what the formula would mean if the author had written d ∈ Device ∧ ∃e (...), or had used one variable for both the result and the test. That repaired query does return {D2, D3}, whose powers are 45. The formula as written does not say that. C and D treat an unrestricted variable as if it still ranged over Device.

### Q10

Answer: A, C

The maximum power in the instance is 45, shared by D2 and D3. A device qualifies when no device has a strictly larger power.

A restricts d to Device and then checks every device through an implication. Both D2 and D3 pass, and D1, D4, and D5 fail. A is safe because d ∈ Device supplies every output value.

C is the same test written with a negated existential quantifier. The inner variable e is restricted by e ∈ Device, and d is restricted by d ∈ Device. It returns the same two identifiers.

B drops d ∈ Device. The comparison no longer forces d to be one of the five stored tuples, so B is unsafe even though its intended meaning is the maximum. D uses conjunction instead of implication inside ∀. The claim ∀e (e ∈ Device ∧ e.Power ≤ d.Power) says that every tuple in the universe is a member of Device. Tuples outside Device falsify it, so the formula does not mean "every stored device has power at most d.Power".

### Q11

Answer: 2

East contains only D5, with power 30. A device outside East qualifies when its power is strictly greater than 30.

- D1 is North, power 30, which is not strictly greater. Rejected.
- D2 is North, power 45. Kept.
- D3 is South, power 45. Kept.
- D4 is South, power 10. Rejected.
- D5 is East, removed by d.Lab ≠ 'East'.

The result is {D2, D3}, so the count is 2. Using ≥ instead of > would also keep D1 and would answer a different question. Forgetting the lab test would also keep nobody extra here, because D5's power is not greater than 30, but the lab test is what makes the query "outside East".

### Q12

Answer: A

The safe pattern for "every tuple that is in the relation and meets a guard also meets a conclusion" is universal quantification of an implication. If a result tuple is being printed, that result variable still needs its own positive membership atom. A is that pattern. The pattern is the right encoding even though this particular claim is false on the instance: D3 is in South and has power 45, so D3 falsifies e.Power < 40.

B puts a conjunction under ∀ and leaves the result variable unrestricted. A conjunction under ∀ says every tuple in the universe is a South device of power below 40, which is neither the intended sentence nor safe. C says every device, in every lab, is a South device below 40. North and East falsify it, and it is a different sentence. D ignores the stored powers and deletes the content of the query.
