# GATE PYQs

## 2026

### Q.30

**Paper:** GATE 2026 CS-1 (forenoon)

**Question:**

Let 𝑃, 𝑄, 𝑅 and 𝑆 be the attributes of a relation in a relational schema. Let 𝑋 ⟶𝑌
indicate functional dependency in the context of a relational database, where
𝑋, 𝑌 ⊆{𝑃, 𝑄, 𝑅, 𝑆}.
Which of the following options is/are always true?

**Options:**

A. If ( {𝑃, 𝑄} ⟶{𝑅} and {𝑃} ⟶{𝑅} ), then {𝑄} ⟶{𝑅}
B. If {𝑃, 𝑄} ⟶{𝑅}, then ( {𝑃} ⟶{𝑅} or {𝑄} ⟶{𝑅} )
C. If ( {𝑃} ⟶{𝑅} and {𝑄} ⟶{𝑆} ), then {𝑃, 𝑄} ⟶{𝑅, 𝑆}
D. If {𝑃} ⟶{𝑅}, then {𝑃, 𝑄} ⟶{𝑅}

**Type:** MCQ

**Answer:** VERIFICATION REQUIRED

**Source:** GATE 2026 CS-1 (forenoon), `12-PYQ/2026/set-01/question-paper.pdf`

---

### Q.31

**Paper:** GATE 2026 CS-1 (forenoon)

**Question:**

statements is/are true?
It is always possible to obtain a dependency-preserving 3NF decomposition of a

**Options:**

A. relation It is always possible to obtain a dependency-preserving 1NF decomposition of a
B. relation It is not always possible to obtain a dependency-preserving BCNF decomposition
C. of a relation It is not always possible to obtain a dependency-preserving 2NF decomposition of
D. a relation

**Type:** MCQ

**Answer:** VERIFICATION REQUIRED

**Source:** GATE 2026 CS-1 (forenoon), `12-PYQ/2026/set-01/question-paper.pdf`

---

### Q.42

**Paper:** GATE 2026 CS-2 (afternoon)

**Question:**

In the context of schema normalization in relational DBMS, consider a set F of
functional dependencies. The set of all functional dependencies implied by F is
called the closure of F. To compute the closure of F, Armstrong’s Axioms can be
applied. Consider 𝑋, 𝑌, and 𝑍 as sets of attributes over a relational schema. The three
rules of Armstrong’s Axioms are described as follows.
Reflexivity: If  𝑌⊆𝑋 , then 𝑋→𝑌
Augmentation: If  𝑋→𝑌, then 𝑋𝑍→𝑌𝑍 for any Z
Transitivity: If 𝑋→𝑌 and 𝑌→𝑍, then 𝑋→𝑍
The additional rule of Union is defined as follows.
Union: If 𝑋→𝑌 and 𝑋→𝑍, then 𝑋→𝑌𝑍
It can be proved that the additional rule of Union is also implied by the three rules
of Armstrong’s Axioms. Listed below are four combinations of these three rules.
Which one of these combinations is both necessary and sufficient for the proof ?

**Options:**

A. Reflexivity, Augmentation, and Transitivity
B. Reflexivity and Augmentation
C. Transitivity
D. Augmentation and Transitivity

**Type:** MCQ

**Answer:** VERIFICATION REQUIRED

**Source:** GATE 2026 CS-2 (afternoon), `12-PYQ/2026/set-02/question-paper.pdf`

---

## 2025

### Q.47

**Paper:** GATE 2025 CS-1

**Question:**

Consider a relational schema  𝑡𝑒𝑎𝑚(𝑛𝑎𝑚𝑒, 𝑐𝑖𝑡𝑦, 𝑜𝑤𝑛𝑒𝑟), with functional
dependencies {𝑛𝑎𝑚𝑒→𝑐𝑖𝑡𝑦, 𝑛𝑎𝑚𝑒→𝑜𝑤𝑛𝑒𝑟}.
The relation  𝑡𝑒𝑎𝑚 is decomposed into two relations,  𝑡1(𝑛𝑎𝑚𝑒, 𝑐𝑖𝑡𝑦) and
𝑡2(𝑛𝑎𝑚𝑒, 𝑜𝑤𝑛𝑒𝑟). Which of the following statement(s) is/are TRUE?

**Options:**

A. The relation 𝑡𝑒𝑎𝑚 is NOT in BCNF.
B. The relations 𝑡1 and 𝑡2 are in BCNF.
C. The decomposition constitutes a lossless join.
D. The relation 𝑡𝑒𝑎𝑚 is NOT in 3NF.

**Type:** MCQ

**Answer:** VERIFICATION REQUIRED

**Source:** GATE 2025 CS-1, `12-PYQ/2025/set-01/question-paper.pdf`

---

### Q.46

**Paper:** GATE 2025 CS-2

**Question:**

Consider the following relational schema along with all the functional dependencies
that hold on them.
R1(A, B, C, D, E): { 𝐷→𝐸, 𝐸𝐴→𝐵, 𝐸𝐵→𝐶}
R2(A, B, C, D): { 𝐴→𝐷, 𝐴→𝐵, 𝐶→𝐴}
Which of the following statement(s) is/are TRUE?

**Options:**

A. R1 is in 3NF
B. R2 is in 3NF
C. R1 is NOT in 3NF
D. R2 is NOT in 3NF

**Type:** MCQ

**Answer:** VERIFICATION REQUIRED

**Source:** GATE 2025 CS-2, `12-PYQ/2025/set-02/question-paper.pdf`

---

## 2024

### Q.22

**Paper:** GATE 2024 CS1

**Question:**

Which of the following statements about a relation R in first normal form (1NF)
is/are TRUE ?

**Options:**

A. R can have a multi-attribute key
B. R cannot have a foreign key
C. R cannot have a composite attribute
D. R cannot have more than one candidate key

**Type:** MCQ

**Answer:** VERIFICATION REQUIRED

**Source:** GATE 2024 CS1, `12-PYQ/2024/set-01/question-paper.pdf`

---

### Q.44

**Paper:** GATE 2024 CS1

**Question:**

The symbol  → indicates functional dependency in the context of a relational
database. Which of the following options is/are TRUE?

**Options:**

A. (𝑋, 𝑌) →(𝑍, 𝑊) implies 𝑋→(𝑍, 𝑊)
B. (𝑋, 𝑌) →(𝑍, 𝑊) implies (𝑋, 𝑌) →𝑍
C. ((𝑋, 𝑌) →𝑍 and 𝑊→𝑌) implies (𝑋, 𝑊) →𝑍
D. (𝑋→𝑌 and 𝑌→𝑍) implies 𝑋→𝑍

**Type:** MCQ

**Answer:** VERIFICATION REQUIRED

**Source:** GATE 2024 CS1, `12-PYQ/2024/set-01/question-paper.pdf`

---

### Q.56

**Paper:** GATE 2024 CS2

**Question:**

A functional dependency 𝐹:⁡𝑋→𝑌 is termed as a useful functional dependency if
and only if it satisfies all the following three conditions:
•  𝑋 is not the empty set.
•  𝑌 is not the empty set.
•  Intersection of 𝑋 and 𝑌 is the empty set.
For a relation  𝑅 with 4 attributes, the total number of possible useful functional
dependencies is ________

**Options:**

The paper does not print options for this numerical-answer question.

**Type:** NAT

**Answer:** VERIFICATION REQUIRED

**Source:** GATE 2024 CS2, `12-PYQ/2024/set-02/question-paper.pdf`

---

## 2022

### Q.14

**Paper:** GATE 2022 CS

**Question:**

In a relational data model, which one of the following statements is TRUE?

**Options:**

A. A relation with only two attributes is always in BCNF.
B. If all attributes of a relation are prime attributes, then the relation is in BCNF.
C. Every relation has at least one non-prime attribute.
D. BCNF decompositions preserve functional dependencies.

**Type:** MCQ

**Answer:** VERIFICATION REQUIRED

**Source:** GATE 2022 CS, `12-PYQ/2022/question-paper.pdf`

---

## 2020

### Q.36

**Paper:** GATE 2020 CS

**Question:**

Consider a relational table R that is in 3NF, but not in BCNF. Which one of the
following statements is TRUE?

**Options:**

A. R has a nontrivial functional dependency X → A, where X is not a superkey and A is a prime attribute.
B. R has a nontrivial functional dependency X → A, where X is not a superkey and A is a non-prime attribute and X is not a proper subset of any key. () R has a nontrivial functional dependency X → A, where X is not a superkey and A is a non-prime attribute and X is a proper subset of some key.
D. A cell in R holds a set instead of an atomic value.

**Type:** MCQ

**Answer:** VERIFICATION REQUIRED

**Source:** GATE 2020 CS, `12-PYQ/2020/question-paper.pdf`

---

## 2019

### Q.32

**Paper:** GATE 2019 CS (printed header Set-2)

**Question:**

Let the set of fiuctional dependencies F = {QR → S, R → P, S → Q} hold on a relation
schema X = (PQRS). X is not in BCNF. Suppose X is decomposed into two schemas Y and
Z, where Y = (PR) and Z = (QRS).
Consider the two statements given below.
Both Y and Z are in BCNF
II. Decomposition of X into Y and Z is dependency preserving and lossless
Which of the above statements is/are correct?

**Options:**

A. Both I and II
B. Ionly
C. II only
D. Neither I nor II

**Type:** MCQ

**Answer:** VERIFICATION REQUIRED

**Source:** GATE 2019 CS (printed header Set-2), `12-PYQ/2019/question-paper.pdf`

---

## 2018

### Q.42

**Paper:** GATE 2018 CS

**Question:**

Consider the following four relational schemas. For each schema, all non-trivial functional
dependencies are listed. The underlined attributes are the respective primary keys.
Schema I: Registration (rollno, courses)
Field ‘courses’ is a set-valued attribute containing the set of courses a student has
registered for.
Non-trivial functional dependency:
rollno  →  courses
Schema II: Registration (rollno, courseid, email)
Non-trivial functional dependencies:
rollno, courseid  →  email
email  →  rollno
Schema III: Registration (rollno, courseid, marks, grade)
Non-trivial functional dependencies:
rollno, courseid  →  marks, grade
marks  →  grade
Schema IV: Registration (rollno, courseid, credit)
Non-trivial functional dependencies:
rollno, courseid  →  credit
courseid  →  credit
Which one of the relational schemas above is in 3NF but not in BCNF?

**Options:**

A. Schema I
B. Schema II
C. Schema III
D. Schema IV

**Type:** MCQ

**Answer:** VERIFICATION REQUIRED

**Source:** GATE 2018 CS, `12-PYQ/2018/question-paper.pdf`

---

## 2016

### Q.23

**Paper:** GATE 2016 CS-1

**Question:**

A database of research articles in a journal uses the following schema.
(VOLUME, NUMBER, STARTPAGE, ENDPAGE, TITLE, YEAR, PRICE)
The primary key is (VOLUME, NUMBER, STARTPAGE, ENDPAGE) and the following
functional dependencies exist in the schema.
(VOLUME, NUMBER, STARTPAGE, ENDPAGE) → TITLE
(VOLUME, NUMBER)  → YEAR
(VOLUME, NUMBER, STARTPAGE, ENDPAGE) → PRICE
The database is redesigned to use the following schemas.
(VOLUME, NUMBER, STARTPAGE, ENDPAGE, TITLE, PRICE)
(VOLUME, NUMBER, YEAR)
Which is the weakest normal form that the new database satisfies, but the old one does not?

**Options:**

A. 1NF
B. 2NF
C. 3NF
D. BCNF

**Type:** MCQ

**Answer:** VERIFICATION REQUIRED

**Source:** GATE 2016 CS-1, `12-PYQ/2016/set-01/question-paper.pdf`

---

## 2015

### Q.48

**Paper:** GATE 2015 CS, 7 February Shift 1

**Question:**

Consider an Entity-Relationship (ER) model in which entity sets E1 and E2 are connected by an
m: n relationship R12. E1 and E3 are connected by a 1 : n (1 on the side of E1 and n on the side of
E3) relationship R13.
Ey has two single-valued attributes a11 and a12 of which a11 is the key attribute. Ez has two single-
valued attributes a21 and a2 of which a21 is the key attribute. Ez has two single-valued attributes a31
and a32 of which a31 is the key attribute. The relationships do not have any attributes.
If a relational model is derived from the above ER model, then the minimum number of relations
that would be generated if all the relations are in 3NF 15
Correct Answer :

**Options:**

The paper does not print options for this numerical-answer question.

**Type:** NAT

**Answer:** VERIFICATION REQUIRED

**Source:** GATE 2015 CS, 7 February Shift 1, `12-PYQ/2015/set-01/question-paper.pdf`

---

### Q.13

**Paper:** GATE 2015 CS, 8 February Shift 1

**Question:**

Consider the relation X (P, Q,R,S,T,U) with the following set of functional dependencies
F = {
(P,R} → {S,T),
(P,S, U} → {Q,R}
Which of the following is the trivial functional dependency in F+ , where Ft is closure of F ?

**Options:**

A. (P,R) → {S,T}
B. (P,R} → (R,T}
C. {P,S} → {S}
D. {P,S,U} → {Q}

**Type:** MCQ

**Answer:** VERIFICATION REQUIRED

**Source:** GATE 2015 CS, 8 February Shift 1, `12-PYQ/2015/set-03/question-paper.pdf`

---

## 2014

### Q.30

**Paper:** GATE 2014 CS SET-1

**Question:**

Given the following two statements:
S1: Every table with two single-valued attributes is in 1NF, 2NF, 3NF
and BCNF.
S2: AB→C, D→E, E→C is a minimal cover for the set of functional
dependencies AB→C, D→E, AB→E, E→C.
Which one of the following is CORRECT?

**Options:**

A. S1 is TRUE and S2 is FALSE.
B. Both S1 and S2 are TRUE.
C. S1 is FALSE and S2 is TRUE.
D. Both S1 and S2 are FALSE.

**Type:** MCQ

**Answer:** VERIFICATION REQUIRED

**Source:** GATE 2014 CS SET-1, `12-PYQ/2014/set-01/question-paper.pdf`

---

## 2013

### Q.55

**Paper:** GATE 2013 CS Booklet A

**Question:**

The relation R is

**Options:**

A. in 1NF, but not in 2NF.
B. in 2NF, but not in 3NF.
C. in 3NF, but not in BCNF.
D. in BCNF. CS-A 12/20 2013COMPUTER SCIENCE & INFORMATION TECH. - CS General Aptitude (GA) Questions

**Type:** MCQ

**Answer:** VERIFICATION REQUIRED

**Source:** GATE 2013 CS Booklet A, `12-PYQ/2013/set-01/question-paper.pdf`

---

### Q.53

**Paper:** GATE 2013 CS Booklet B

**Question:**

The relation R is

**Options:**

A. in 1NF, but not in 2NF.
B. in 2NF, but not in 3NF.
C. in 3NF, but not in BCNF.
D. in BCNF. Statement for Linked Answer Questions 54 and 55: A computer uses 46-bit virtual address, 32-bit physical address, and a three-level paged page table organization. The page table base register stores the base address of the first-level table (T_{1}), which occupies exactly one page. Each entry of T_{1}stores the base address of a page of the second-level table (T_{2}). Each entry of T_{2} stores the base address of a page of the third-level table (T_{3}). Each entry of T_{3} stores a page table entry (PTE). The PTE is 32 bits in size. The processor used in the computer has a 1 MB 16-way set associative virtually indexed physically tagged cache. The cache block size is 64 bytes.

**Type:** MCQ

**Answer:** VERIFICATION REQUIRED

**Source:** GATE 2013 CS Booklet B, `12-PYQ/2013/set-02/question-paper.pdf`

---

### Q.55

**Paper:** GATE 2013 CS Booklet C

**Question:**

The relation R is

**Options:**

A. in 1NF, but not in 2NF.
B. in 2NF, but not in 3NF.
C. in 3NF, but not in BCNF.
D. in BCNF. CS- C 12/20 2013COMPUTER SCIENCE & INFORMATION TECH. - CS General Aptitude (GA) Questions

**Type:** MCQ

**Answer:** VERIFICATION REQUIRED

**Source:** GATE 2013 CS Booklet C, `12-PYQ/2013/set-03/question-paper.pdf`

---

### Q.53

**Paper:** GATE 2013 CS Booklet D

**Question:**

The relation R is

**Options:**

A. in 1NF, but not in 2NF.
B. in 2NF, but not in 3NF.
C. in 3NF, but not in BCNF.
D. in BCNF. Statement for Linked Answer Questions 54 and 55: A computer uses 46-bit virtual address, 32-bit physical address, and a three-level paged page table organization. The page table base register stores the base address of the first-level table (T_{1}), which occupies exactly one page. Each entry of T_{1}stores the base address of a page of the second-level table (T_{2}). Each entry of T_{2} stores the base address of a page of the third-level table (T_{3}). Each entry of T_{3} stores a page table entry (PTE). The PTE is 32 bits in size. The processor used in the computer has a 1 MB 16-way set associative virtually indexed physically tagged cache. The cache block size is 64 bytes.

**Type:** MCQ

**Answer:** VERIFICATION REQUIRED

**Source:** GATE 2013 CS Booklet D, `12-PYQ/2013/set-04/question-paper.pdf`

---

## 2012

### Q.2

**Paper:** GATE 2012 CS Booklet A

**Question:**

Which of the following is TRUE?

**Options:**

A. Every relation in 3NF is also in BCNF
B. A relation R is in 3NF if every non-prime attribute of R is fully functionally dependent on every key of R
C. Every relation in BCNF is also in 3NF
D. No relation can be in both BCNF and 3NF

**Type:** MCQ

**Answer:** VERIFICATION REQUIRED

**Source:** GATE 2012 CS Booklet A, `12-PYQ/2012/question-paper.pdf`

---

## 2009

### Q.56

**Paper:** GATE 2009 CS

**Question:**

Assume that, in the suppliers relation above, each supplier and each street within a city has a unique
name, and (sname, city) forms a candidate key. No other functional dependencies are implied other than
those implied by primary and candidate keys. Which one of the following is TRUE about the above
schema ?

**Options:**

A. The schema is in BCNF.
B. The schema is in 3NF but not in BCNF.
C. The schema is in 2NF but not in 3NF.
D. The schema is not in 2NF. Linked Answer Questions Statement for Linked Answer Questions 57 and 58: Frames of 1000 bits are sent over a 10°bps duplex link between two hosts. The propagation time is 25ms. Frames are to be transmitted into this link to maximally pack them in transit (within the link).

**Type:** MCQ

**Answer:** VERIFICATION REQUIRED

**Source:** GATE 2009 CS, `12-PYQ/2009/question-paper.pdf`

---

## 2008

### Q.69

**Paper:** GATE 2008 CS

**Question:**

Consider the following relational schemes for a library database:
Book (Title, Author, Catalog_no, Publisher, Year, Price)
Collection (Title, Author, Catalog_no)
with the following functional dependencies:
I. Title Author → Catalog_no
II. Catalog_no → Title Author Publisher Year
IIl. Publisher Title Year → Price
Assume {Author,Title) is the key for both schemes. Which of the following statements is true?

**Options:**

A. Both Book and Collection are in BCNF
B. Both Book and Collection are in 3NF only
C. Book is in 2NF and Collection is in 3NF
D. Both Book and Collection are in 2NF only

**Type:** MCQ

**Answer:** VERIFICATION REQUIRED

**Source:** GATE 2008 CS, `12-PYQ/2008/question-paper.pdf`

---

## 2007

### Q.48

**Paper:** GATE 2007 CS

**Question:**

Which of the following is TRUE about formulae in Conjunctive Normal Form?

**Options:**

A. For any formula, there is a truth assignment for which at least half the clauses evaluate to true.
B. For any formula, there is a truth assignment for which all the clauses evaluate to true.
C. There is a formula such that for each truth assignment, at most one-fourth of the clauses evaluate to true.
D. None of the above. CS - 11/24

**Type:** MCQ

**Answer:** VERIFICATION REQUIRED

**Source:** GATE 2007 CS, `12-PYQ/2007/question-paper.pdf`

---

### Q.62

**Paper:** GATE 2007 CS

**Question:**

Which one of the following statements is FALSE?

**Options:**

A. Any relation with two attributes is in BCNF.
B. A relation in which every key has only one attribute is in 2NF.
C. A prime attribute can be transitively dependent on a key in a 3NF relation.
D. A prime attribute can be transitively dependent on a key in a BCNF relation. CS - 15/24

**Type:** MCQ

**Answer:** VERIFICATION REQUIRED

**Source:** GATE 2007 CS, `12-PYQ/2007/question-paper.pdf`

---
