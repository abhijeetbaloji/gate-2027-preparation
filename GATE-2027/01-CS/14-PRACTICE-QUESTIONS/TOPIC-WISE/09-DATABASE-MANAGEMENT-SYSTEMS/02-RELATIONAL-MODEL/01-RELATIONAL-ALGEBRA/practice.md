# Relational Algebra — Practice Questions

Original practice for GATE CS. These questions are not from any GATE paper. Attempt the questions before reading the solutions.

Relational algebra is used with set semantics: projection and union remove duplicate tuples. Natural join equates identically named attributes and keeps one copy of each shared name. If two relations have no attribute name in common, their natural join is their Cartesian product.

Questions 5 onward use this instance.

Borrower(Bid, Bname, City)

| Bid | Bname | City |
|-----|-------|------|
| B1 | Meera | Pune |
| B2 | Arun | Pune |
| B3 | Leela | Kochi |
| B4 | Omar | Jaipur |

Book(Isbn, Title, Genre)

| Isbn | Title | Genre |
|------|-------|-------|
| I1 | Atlas | Ref |
| I2 | Drift | Fiction |
| I3 | Moss | Fiction |
| I4 | Quartz | Ref |
| I5 | Nimbus | Poetry |

Loan(Bid, Isbn, Week)

| Bid | Isbn | Week |
|-----|------|------|
| B1 | I1 | 3 |
| B1 | I2 | 3 |
| B1 | I4 | 5 |
| B2 | I2 | 4 |
| B2 | I3 | 4 |
| B3 | I1 | 3 |
| B3 | I5 | 6 |
| B4 | I2 | 5 |

## Level 1 — Conceptual

## Q1 — MCQ

Which operator can return a relation with more tuples than its input relation?

A. Selection
B. Projection
C. Set difference
D. Cartesian product

---

## Q2 — MCQ

Natural join of R and S

A. equates every pair of attributes that happen to have the same domain, even if the names differ
B. equates attributes that have the same name and discards one copy of each equated attribute
C. always includes a tuple of R that matches no tuple of S, padded with nulls
D. is undefined whenever R and S have different numbers of attributes

---

## Q3 — MCQ

Under set semantics, which statement is true?

A. Projection can remove duplicate tuples that selection on the same relation would keep
B. Selection removes duplicate tuples and leaves the attribute list unchanged
C. Union keeps one copy of each tuple for every input in which it appears
D. If R has two identical tuples, both survive a projection

---

## Q4 — MCQ

The expression R(A, B) ÷ S(B) is

A. the set of A-values that occur in R together with every B-value in S
B. the set of A-values that occur in R together with at least one B-value in S
C. the set difference R − S
D. the natural join of R and S

---

## Level 2 — Standard GATE Style

## Q5 — MCQ

How many tuples are in σ_{City = 'Pune'}(Borrower)?

A. 1
B. 2
C. 3
D. 4

---

## Q6 — NAT

How many tuples are in π_{Genre}(Book)? ______

---

## Q7 — MCQ

Which expression returns the titles of books borrowed by borrowers who live in Kochi?

A. π_{Title}(σ_{City = 'Kochi'}(Borrower) ⋈ Loan ⋈ Book)
B. π_{Title}(σ_{City = 'Kochi'}(Book))
C. π_{Title}(Borrower ⋈ σ_{City = 'Kochi'}(Loan))
D. σ_{Title = 'Kochi'}(Borrower ⋈ Book)

---

## Q8 — MSQ

Which equalities hold in general under set semantics, assuming any union is applied only to union-compatible relations? Select all that apply.

A. σ_{c1}(σ_{c2}(R)) = σ_{c1 ∧ c2}(R)
B. π_X(R − S) = π_X(R) − π_X(S)
C. σ_c(R ∪ S) = σ_c(R) ∪ σ_c(S)
D. R ⋈ S = S ⋈ R

---

## Q9 — NAT

How many tuples are in Loan ⋈ Book? ______

---

## Level 3 — Multi-Step

## Q10 — NAT

How many tuples are in

π_{Bid, Isbn}(Loan) ÷ π_{Isbn}(σ_{Genre = 'Fiction'}(Book))?

______

---

## Q11 — MCQ

Which borrowers borrowed every reference book (Genre = 'Ref')? The result of the corresponding division, joined back to Borrower for the name, contains

A. only Meera
B. only Arun
C. Meera and Leela
D. nobody

---

## Q12 — NAT

How many tuples are in π_{Bname, Genre}(Borrower ⋈ Loan ⋈ Book)? ______

---

## Q13 — MSQ

Which expressions evaluate to exactly the one-tuple relation {(Meera)}? Select all that apply.

A. π_{Bname}(σ_{City = 'Pune' ∧ Genre = 'Ref'}(Borrower ⋈ Loan ⋈ Book))
B. π_{Bname}(σ_{City = 'Pune' ∧ Genre = 'Fiction'}(Borrower ⋈ Loan ⋈ Book))
C. π_{Bname}(Borrower ⋈ (π_{Bid, Isbn}(Loan) ÷ π_{Isbn}(σ_{Genre = 'Ref'}(Book))))
D. π_{Bname}(σ_{City = 'Kochi'}(Borrower))

---

## Level 4 — Tricky / Trap-Based

## Q14 — MCQ

How many tuples are in Borrower ⋈ Book?

A. 0
B. 4
C. 9
D. 20

---

## Q15 — MSQ

Which statements are true? Select all that apply.

A. σ_{Week = 3}(π_{Bid}(Loan)) is a legal expression and equals π_{Bid}(σ_{Week = 3}(Loan))
B. On this instance, Borrower ⋈ Book has one tuple for every pair of a borrower and a book
C. π_{Bid}(Loan) − π_{Bid}(σ_{Week = 3}(Loan)) excludes B1, even though B1 has a loan in week 5
D. Loan − Loan equals Loan, because every tuple of Loan matches a tuple of Loan

---

## Q16 — NAT

How many tuples are in π_{Bid}(Loan) − π_{Bid}(σ_{Week = 3}(Loan))? ______

---

## Level 5 — Challenge

## Q17 — NAT

How many titles are borrowed by every borrower who lives in Pune? In other words, how many tuples are in

π_{Title}( Book ⋈ ( π_{Isbn, Bid}(Loan) ÷ π_{Bid}(σ_{City = 'Pune'}(Borrower)) ) )?

______

---

## Q18 — MCQ

There is no book with Genre = 'Drama'. How many tuples are in

π_{Bid, Isbn}(Loan) ÷ π_{Isbn}(σ_{Genre = 'Drama'}(Book))?

A. 0
B. 1
C. 4
D. 8

---

## Answer Key

| Q | Type | Answer |
|---|------|--------|
| 1 | MCQ | D |
| 2 | MCQ | B |
| 3 | MCQ | A |
| 4 | MCQ | A |
| 5 | MCQ | B |
| 6 | NAT | 3 |
| 7 | MCQ | A |
| 8 | MSQ | A, C, D |
| 9 | NAT | 8 |
| 10 | NAT | 1 |
| 11 | MCQ | A |
| 12 | NAT | 6 |
| 13 | MSQ | A, C |
| 14 | MCQ | D |
| 15 | MSQ | B, C |
| 16 | NAT | 2 |
| 17 | NAT | 1 |
| 18 | MCQ | C |

## Detailed Solutions

### Q1

Answer: D

Cartesian product of relations of sizes m and n has m·n tuples, which can exceed both inputs. Selection keeps a subset of the tuples, so it cannot grow the relation. Projection keeps a subset of the columns and, under set semantics, can only reduce or preserve the number of tuples. Difference removes tuples of the second relation from the first, so it cannot grow either.

### Q2

Answer: B

Natural join matches on names, not on domains. A borrower city and a book genre are not joined merely because both are strings, so A is false. Unmatched tuples are dropped; padding with nulls is an outer join, so C is false. Different arities are allowed. The result arity is the number of distinct attribute names, so D is false.

### Q3

Answer: A

Two loans can share a Bid and differ in Week. Selection keeps both rows. Projection onto Bid keeps one. That is A. Selection filters rows; it is not the duplicate-removing operator, so B fails. Union is a set, so a tuple that appears in both inputs appears once, not once per input, and C fails. Relations are sets, so D's premise of two identical stored tuples is outside set semantics, and projection would still keep one copy.

### Q4

Answer: A

Division keeps those A-values for which the whole set S of B-values is present in R. "At least one" is a semijoin-style condition, not division, so B fails. Difference needs union-compatible inputs and does not express "for every", so C fails. Natural join requires matching tuples, which is existential, so D fails.

### Q5

Answer: B

The Pune rows are (B1, Meera, Pune) and (B2, Arun, Pune). Leela is in Kochi and Omar is in Jaipur, so the count is 2, not 3 or 4.

### Q6

Answer: 3

The genres on the five books are Ref, Fiction, Fiction, Ref, and Poetry. Projection removes the repeated Ref and Fiction values, leaving {Ref, Fiction, Poetry}.

### Q7

Answer: A

σ_{City = 'Kochi'}(Borrower) is the single tuple for Leela. She has loans of I1 and I5. Joining Book produces the titles Atlas and Nimbus.

B selects on Book, which has no City attribute, so it is illegal. C selects on Loan, which also has no City attribute. D equates a title with the string Kochi and would not read City at all; the join of Borrower and Book is not even a loan.

### Q8

Answer: A, C, D

Selection predicates on one relation can be stacked in either order and combined with conjunction, so A holds. Selection distributes over union, so C holds. Natural join is commutative under set semantics: matching is symmetric and the result schema does not depend on which input is written first, so D holds.

B does not hold. Let R(X, Y) = {(1, a), (2, a)} and S(X, Y) = {(1, b)}. Then R − S = R, so π_X(R − S) = {1, 2}. But π_X(R) − π_X(S) = {1, 2} − {1} = {2}. Projection does not distribute over difference.

### Q9

Answer: 8

Loan and Book share only Isbn. Every loan's Isbn is one of I1 through I5, and each of those appears in Book. Each of the 8 loan tuples matches exactly one book, so the natural join has 8 tuples. Week, Title, and Genre do not affect the match.

### Q10

Answer: 1

The fiction books are I2 (Drift) and I3 (Moss). A borrower id survives the division only if both isbns appear in Loan for that id.

- B1 has I1, I2, I4, and is missing I3.
- B2 has I2 and I3.
- B3 has I1 and I5.
- B4 has I2 only.

Only B2 survives, so the result has 1 tuple.

### Q11

Answer: A

The reference books are I1 (Atlas) and I4 (Quartz).

- B1 has both I1 and I4.
- B2 has neither reference isbn.
- B3 has I1 but not I4.
- B4 has neither.

The division returns {B1}, whose name is Meera. Leela borrowed Atlas but not Quartz, so C is the partial-match trap. Arun borrowed no reference book.

### Q12

Answer: 6

Borrower ⋈ Loan ⋈ Book has the same 8 loan rows, now with name, city, title, and genre. Projection onto (Bname, Genre) removes duplicate pairs:

- Meera: Ref (Atlas and Quartz collapse), Fiction
- Arun: Fiction (Drift and Moss collapse)
- Leela: Ref, Poetry
- Omar: Fiction

That is 6 tuples. The unprojected join has 8 rows; the two extra rows are repeated pairs, not new pairs.

### Q13

Answer: A, C

A keeps Pune borrowers who borrowed a reference book. Meera borrowed Atlas and Quartz. Arun's loans are both fiction. The name set is {Meera}.

C is the division from Q11, which returns Bid B1, then the join to Borrower returns Meera.

B also keeps Arun, because he lives in Pune and borrowed fiction. D returns Leela.

### Q14

Answer: D

Borrower has attributes (Bid, Bname, City) and Book has (Isbn, Title, Genre). There is no shared name, so the natural join is the Cartesian product: 4 · 5 = 20.

A is the trap of treating "no common attribute" as "no matching tuple". B is the size of the larger input. C is the sum 4 + 5, which is not a join size.

### Q15

Answer: B, C

B restates Q14: with no common attribute, every borrower is paired with every book.

C is true because set difference of the projections removes every Bid that appears in any week-3 loan. B1 appears in week 3, so B1 is removed, even though B1 also appears in week 5. The expression does not mean "has a loan outside week 3".

A is false because π_{Bid}(Loan) has no Week column, so a later selection on Week is illegal. D is false because R − R is empty, not R.

### Q16

Answer: 2

π_{Bid}(Loan) = {B1, B2, B3, B4}. The week-3 loans belong to B1 and B3, so the difference is {B2, B4}. The size is 2. B1 is not in the result; see Q15.

### Q17

Answer: 1

The Pune borrowers are B1 and B2. An isbn survives the division only if both have borrowed it.

- I1 is borrowed by B1 and B3, not by B2.
- I2 is borrowed by B1, B2, and B4.
- I3 is borrowed by B2 only.
- I4 is borrowed by B1 only.
- I5 is borrowed by B3 only.

Only I2 survives. Its title is Drift, so the outer projection has 1 tuple. Counting Pune borrowers, or counting every book either of them borrowed, answers a different query.

### Q18

Answer: C

Let R(Bid, Isbn) = π_{Bid, Isbn}(Loan) and let S be the empty set of drama isbns. By the algebraic definition

R ÷ S = π_{Bid}(R) − π_{Bid}((π_{Bid}(R) × S) − R).

A Cartesian product with the empty relation is empty, and subtracting the empty projection removes nothing. The result is π_{Bid}(R) = {B1, B2, B3, B4}, which has 4 tuples.

The same reading follows from the logical definition: an A-value qualifies when every B-value in S occurs with it. A universal claim over an empty set is true, and the A-values available from R are exactly the four borrower ids that appear in Loan.

A is the trap of deciding that division by nothing yields nothing. B is the fiction-division answer from Q10. D is the number of loan rows, not the number of distinct bids.
