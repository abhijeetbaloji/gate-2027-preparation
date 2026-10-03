# Integrity Constraints — Practice Questions

Original practice for GATE CS. These questions are not from any GATE paper. Attempt the questions before reading the solutions.

Unless a question says otherwise, foreign keys use the SQL default MATCH SIMPLE, checks are immediate, and a foreign key with no action named uses ON DELETE RESTRICT. Each insertion in Q4 is tested alone against the original instance.

Department(DeptId, Dname), primary key DeptId

| DeptId | Dname |
|--------|-------|
| 1 | Audit |
| 2 | Design |

Employee(EmpId, Ename, DeptId, MgrId)

- Primary key EmpId
- DeptId may be NULL and references Department(DeptId)
- MgrId may be NULL and references Employee(EmpId)

| EmpId | Ename | DeptId | MgrId |
|-------|-------|--------|-------|
| 10 | Rya | 1 | NULL |
| 11 | Vik | 1 | 10 |
| 12 | Sai | NULL | 10 |

Project(ProjId, Pname, LeadId)

- Primary key ProjId
- LeadId may be NULL and references Employee(EmpId)

| ProjId | Pname | LeadId |
|--------|-------|--------|
| P1 | Bridge | 10 |
| P2 | Kite | NULL |

Assignment(EmpId, ProjId, Role)

- Primary key (EmpId, ProjId)
- EmpId references Employee(EmpId) and is not null
- ProjId references Project(ProjId) and is not null
- Role may be NULL

| EmpId | ProjId | Role |
|-------|--------|------|
| 10 | P1 | lead |
| 11 | P1 | aide |
| 11 | P2 | aide |

## Level 1 — Conceptual

## Q1 — MCQ

Entity integrity requires which of the following?

A. No component of a primary key may be NULL
B. Every foreign key must be NULL when the referenced row is deleted
C. A relation may have two identical rows as long as the primary key is indexed
D. A candidate key may be a proper subset of another candidate key

---

## Q2 — MCQ

Which statement is true?

A. Every superkey is a candidate key
B. Every candidate key is a minimal superkey
C. A foreign key is always a candidate key of the referencing relation
D. Removing an attribute from a candidate key always leaves a superkey

---

## Q3 — MCQ

A foreign key in relation R references a key of relation S. Which requirement is part of referential integrity?

A. Every non-NULL foreign-key value in R must equal the referenced key of some row in S
B. S must contain a foreign key back to R
C. The foreign key must have the same attribute names as the referenced key
D. The foreign key of R must itself be a candidate key of R

---

## Level 2 — Standard GATE Style

## Q4 — MSQ

Which insertions are accepted on the original instance? Select all that apply.

A. Employee (13, Uma, 2, 11)
B. Employee (13, Uma, 9, 11)
C. Assignment (12, P1, NULL)
D. Assignment (10, P1, aide)

---

## Q5 — NAT

How many Assignment rows belong to employees whose DeptId is 1? ______

---

## Q6 — MCQ

What happens if Department row 1 is deleted and every foreign key uses ON DELETE RESTRICT?

A. The delete is rejected because at least one Employee row references department 1
B. The delete succeeds and sets DeptId to NULL on employees 10 and 11
C. The delete succeeds and removes employees 10 and 11 only
D. The delete succeeds and removes every Assignment row

---

## Q7 — NAT

How many Employee rows have a NULL DeptId? ______

---

## Level 3 — Multi-Step

## Q8 — MSQ

Suppose AB and AC are the only candidate keys of R(A, B, C). Which statements are true? Select all that apply.

A. A alone is a candidate key
B. AB is a superkey
C. B alone is a superkey
D. ABC is a superkey and is not a candidate key

---

## Q9 — NAT

Under ON DELETE RESTRICT on every foreign key, how many existing rows reference employee 10 and therefore block a deletion of that employee? Count Employee rows that name 10 as MgrId, Project rows that name 10 as LeadId, and Assignment rows whose EmpId is 10. ______

---

## Q10 — MCQ

Inserting Assignment (12, P9, aide) is rejected because

A. (12, P9) duplicates an existing primary key
B. employee 12 does not exist
C. project P9 does not exist
D. Role is not allowed to be the string aide

---

## Level 4 — Tricky / Trap-Based

## Q11 — MCQ

Shipment(ShipId, Lot, Bin, Qty) has primary key ShipId. The foreign key (Lot, Bin) references Shelf(Lot, Bin). Bin may be NULL. Under MATCH SIMPLE, inserting (S9, L1, NULL, 4) when no Shelf row has Lot = L1

A. is rejected, because Lot is non-NULL and must match a shelf
B. is accepted, because a composite foreign key is not checked when any of its columns is NULL
C. is accepted only when some Shelf row has a NULL Bin
D. violates entity integrity on ShipId

---

## Q12 — MSQ

Which statements are true in SQL? Select all that apply.

A. A PRIMARY KEY column rejects NULL
B. A UNIQUE column and a PRIMARY KEY column treat NULL in exactly the same way
C. A foreign-key column may be NULL when it is not declared NOT NULL and is not part of a primary key
D. Referential integrity constrains the non-NULL foreign-key values

---

## Level 5 — Challenge

## Q13 — MCQ

Dept.MgrEmpId is NOT NULL and references Employee(EmpId). Employee.DeptId is NOT NULL and references Dept(DeptId). Both foreign keys are checked immediately. The tables are empty. Which statement is true?

A. One transaction can insert the first department and the first employee if both foreign keys are DEFERRABLE and the checks are deferred until commit
B. Inserting the department first always succeeds, even though MgrEmpId is NOT NULL and no employee exists
C. Writing NULL into both foreign keys satisfies the NOT NULL constraints
D. A schema in which foreign keys form a cycle is illegal, so it cannot be created

---

## Q14 — MSQ

On the original instance, which statements are true? Select all that apply.

A. (EmpId, ProjId) is a candidate key of Assignment
B. EmpId alone is a candidate key of Assignment
C. Deleting project P2 is rejected when Assignment's foreign key uses ON DELETE RESTRICT
D. Employee 12 violates referential integrity because DeptId is NULL

---

## Answer Key

| Q | Type | Answer |
|---|------|--------|
| 1 | MCQ | A |
| 2 | MCQ | B |
| 3 | MCQ | A |
| 4 | MSQ | A, C |
| 5 | NAT | 3 |
| 6 | MCQ | A |
| 7 | NAT | 1 |
| 8 | MSQ | B, D |
| 9 | NAT | 4 |
| 10 | MCQ | C |
| 11 | MCQ | B |
| 12 | MSQ | A, C, D |
| 13 | MCQ | A |
| 14 | MSQ | A, C |

## Detailed Solutions

### Q1

Answer: A

Entity integrity says that a primary key identifies every row, so none of its columns may be NULL. For a composite primary key, even one NULL component is forbidden.

B is one possible referential action, not the definition of entity integrity. C contradicts the definition of a key: a primary key forbids duplicate rows. D is false because candidate keys are minimal. If a proper subset were still a key, the larger set would only be a superkey.

### Q2

Answer: B

A candidate key is a superkey with no proper subset that is still a superkey. Every candidate key is therefore a minimal superkey.

A reverses the inclusion. A superkey may contain extra attributes. C is false: a foreign key points at a candidate key of the referenced relation, and it need not be unique in the referencing relation. Assignment.EmpId is a foreign key and is repeated. D is the opposite of minimality. Removing an attribute from a candidate key must destroy the superkey property.

### Q3

Answer: A

Referential integrity is a matching rule. Under MATCH SIMPLE, if the foreign key is fully non-NULL, that value must occur in the referenced candidate key. NULL handling is the subject of Q11; the core non-NULL rule is A.

B is not required. One direction is enough, though cycles are allowed. C is not required; correspondence is by declaration, not by spelling. D fails for the same reason as Q2.C: many rows may share a foreign-key value.

### Q4

Answer: A, C

A uses a new EmpId, department 2 exists, and manager 11 exists. It is accepted.

B names department 9, which is not in Department. The DeptId foreign key rejects it.

C uses employee 12 and project P1, both present, and (12, P1) is not already an Assignment key. Role may be NULL. It is accepted.

D repeats the primary key (10, P1). It is rejected even though both foreign keys would have matched and the role string is harmless.

### Q5

Answer: 3

Employees in department 1 are Rya (10) and Vik (11). Sai's DeptId is NULL. Their assignment rows are (10, P1), (11, P1), and (11, P2). The count is 3.

### Q6

Answer: A

Employees 10 and 11 store DeptId 1. RESTRICT rejects a delete of a referenced department. Nothing is set to NULL, and no employee or assignment row is removed.

B would be ON DELETE SET NULL. C and D describe cascades that were not declared. Even a cascade from Department to Employee would still need a separate action for Assignment and for MgrId; RESTRICT does none of that.

### Q7

Answer: 1

Only Sai, employee 12, has a NULL department. A NULL foreign key is allowed here because DeptId is not part of Employee's primary key and was not declared NOT NULL. That row is legal; see Q14.

### Q8

Answer: B, D

AB is a candidate key, so it is a superkey. ABC contains AB, so ABC is a superkey, but it is not minimal: AB already determines the row. A candidate key cannot properly contain another candidate key, so ABC is not a candidate key.

A is false. If A alone were a key, AB and AC would not be minimal. C is false. B is a proper subset of the candidate key AB, so B is not a superkey.

### Q9

Answer: 4

The referencing rows are:

- Employee 11, with MgrId 10
- Employee 12, with MgrId 10
- Project P1, with LeadId 10
- Assignment (10, P1), with EmpId 10

Assignment rows of other employees do not reference EmpId 10. Project P2 has a NULL lead and does not reference 10. The count is 4, so RESTRICT rejects the deletion.

### Q10

Answer: C

Employee 12 exists, and (12, P9) is not an existing assignment key, so A and B are not the reason. The role value is permitted. Project P9 is absent, so the ProjId foreign key fails.

### Q11

Answer: B

MATCH SIMPLE, the SQL default, skips the foreign-key check when any column of a composite foreign key is NULL. Bin is NULL, so the DBMS does not require a Shelf row for L1. The row is accepted.

A is the behaviour people expect from MATCH FULL, or from checking each column separately. C invents a match against NULL, which ordinary equality does not provide. D fails because ShipId is S9, a non-NULL primary-key value, and the question does not say that S9 already exists.

### Q12

Answer: A, C, D

A primary key rejects NULL in every component. That is A and also entity integrity. A foreign key that is allowed to be NULL does not have to point at a row while it is NULL, and every fully specified foreign-key value must match. C and D are that rule.

B is false. In SQL, UNIQUE allows more than one NULL (the comparison NULL = NULL is not TRUE, so the uniqueness check does not see a duplicate), whereas PRIMARY KEY rejects NULL entirely.

### Q13

Answer: A

Each row needs the other row already to be visible if the foreign keys are checked immediately, and NOT NULL forbids inserting a temporary NULL. Deferring both checks until commit lets the transaction insert the two rows in either order and validate the cycle at the end.

B fails because an immediate NOT NULL foreign key cannot point at a missing employee. C contradicts NOT NULL. D is false: cyclic foreign keys are legal. What is difficult is the first insertion under immediate checking, not the schema itself.

### Q14

Answer: A, C

(EmpId, ProjId) is the declared primary key, so it is a candidate key. A holds. Project P2 is referenced by Assignment (11, P2). RESTRICT blocks the delete of P2. C holds.

B is false because EmpId 11 appears on two assignment rows, so EmpId does not uniquely identify an assignment. D is false because a NULL DeptId is a permitted foreign key on Employee. Referential integrity is not violated by that NULL.
