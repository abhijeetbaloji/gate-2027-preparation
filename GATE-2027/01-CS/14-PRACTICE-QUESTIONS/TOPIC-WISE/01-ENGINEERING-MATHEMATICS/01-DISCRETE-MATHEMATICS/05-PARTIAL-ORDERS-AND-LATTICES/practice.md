# Partial Orders and Lattices — Practice Questions

Original practice for GATE CS. These questions are not from any GATE paper. Attempt the questions before reading the solutions.

## Level 1 — Conceptual

## Q1 — MCQ

A binary relation ≤ on a set P is a partial order when it is

A. reflexive, symmetric, and transitive
B. reflexive, antisymmetric, and transitive
C. irreflexive, antisymmetric, and transitive
D. reflexive, asymmetric, and transitive

---

## Q2 — MCQ

In a Hasse diagram, an upward line is drawn from x to y exactly when

A. x ≤ y
B. x < y and no element z satisfies x < z < y
C. x and y are incomparable
D. x is a minimal element and y is a maximal element

---

## Q3 — MCQ

Consider the set {2, 3, 4, 6, 12} ordered by divisibility. Which one of the following is true?

A. 2 is the least element
B. The poset has no least element
C. 4 is a minimal element
D. 12 is not a maximal element

---

## Q4 — MSQ

Let P be the set of all subsets of {x, y}, ordered by inclusion. Select all that apply.

A. ∅ is the least element of P
B. {x} and {y} are incomparable
C. {x, y} is the greatest element of P
D. {x} is a maximal element of P

---

## Level 2 — Standard GATE Style

## Q5 — MCQ

Which one of the following sets, ordered by divisibility, is a lattice?

A. {2, 3, 6}
B. {1, 2, 3}
C. {1, 2, 4, 8}
D. {2, 3, 4, 6}

---

## Q6 — NAT

A chain has 7 elements. How many ordered pairs (x, y), including pairs with x = y, satisfy x ≤ y?

---

## Q7 — MCQ

Let L be the set of positive divisors of 36, ordered by divisibility. The join (least upper bound) of 4 and 6 in L is

A. 2
B. 6
C. 12
D. 36

---

## Q8 — MSQ

Let P = {a, b, c, d}. The covering relations are a ≺ b, a ≺ c, b ≺ d, and c ≺ d, and ≤ is the reflexive-transitive closure of these covers. Select all that apply.

A. a is the least element of P
B. b and c are incomparable
C. d is the greatest element of P
D. b and c have no least upper bound in P

---

## Level 3 — Multi-Step

## Q9 — MCQ

Let L be the set of positive divisors of 12, ordered by divisibility, with join equal to lcm and meet equal to gcd. Which one of the following subsets is a sublattice of L?

A. {2, 4, 6}
B. {1, 2, 3, 6}
C. {4, 6, 12}
D. {2, 3, 4, 12}

---

## Q10 — NAT

Let D be the set of positive divisors of 30, ordered by divisibility. How many covering relations does this poset have?

---

## Q11 — MSQ

Select all that apply.

A. Every chain with 4 elements is a lattice
B. Every antichain with 4 elements is a lattice
C. Every one-element poset is both a chain and an antichain
D. Every finite nonempty chain has a greatest element

---

## Level 4 — Tricky / Trap-Based

## Q12 — MCQ

Let (P, ≤) be a finite poset with exactly three maximal elements. Which one of the following is true?

A. P has three distinct maximum elements
B. P has no maximum element
C. Every element of P is less than or equal to all three maximal elements
D. ≤ cannot be a partial order

---

## Q13 — NAT

Let Q be the set of all nonempty subsets of {1, 2, 3, 4}, ordered by inclusion. How many minimal elements does Q have?

---

## Q14 — MSQ

Which of the following hold in every lattice? Select all that apply.

A. a ∧ (a ∨ b) = a
B. a ∨ b = b ∨ a
C. a ∧ (b ∨ c) = (a ∧ b) ∨ (a ∧ c)
D. If a ≤ b, then a ∨ b = b

---

## Level 5 — Challenge

## Q15 — NAT

Let B be the set of all subsets of {1, 2, 3, 4}, ordered by inclusion. How many elements of B are incomparable with {1, 2}?

---

## Q16 — MCQ

Let C be the chain 0 < 1. In the product poset C × C, declare (x1, y1) ≤ (x2, y2) if and only if x1 ≤ x2 and y1 ≤ y2. Which one of the following is true?

A. The poset has 4 elements, and every pair of elements has both a join and a meet
B. The poset has 4 elements, and no two distinct elements are comparable
C. The poset has 2 elements
D. The relation ≤ is not reflexive

## Answer Key

| Q | Type | Answer |
|---|------|--------|
| 1 | MCQ | B |
| 2 | MCQ | B |
| 3 | MCQ | B |
| 4 | MSQ | A, B, C |
| 5 | MCQ | C |
| 6 | NAT | 28 |
| 7 | MCQ | C |
| 8 | MSQ | A, B, C |
| 9 | MCQ | B |
| 10 | NAT | 12 |
| 11 | MSQ | A, C, D |
| 12 | MCQ | B |
| 13 | NAT | 4 |
| 14 | MSQ | A, B, D |
| 15 | NAT | 9 |
| 16 | MCQ | A |

## Detailed Solutions

### Q1

Answer: B

A partial order is reflexive, antisymmetric, and transitive. Reflexivity puts every pair (a, a) in the relation, which antisymmetric relations are allowed to contain. Symmetric plus reflexive and transitive is an equivalence relation, so A describes equivalence, not order. An irreflexive transitive relation is a strict order, so C drops reflexivity. Asymmetric relations forbid (a, a), so D cannot be a partial order.

### Q2

Answer: B

A cover x ≺ y means x < y and nothing lies strictly between them. The Hasse diagram draws only those covers, upward from the smaller element. All other comparabilities are recovered by going upward along a path, so drawing every pair with x ≤ y would repeat transitive edges and the reflexive loops. Incomparable pairs have no edge, and an edge need not join a global minimal element to a global maximal element.

### Q3

Answer: B

The divisibility relations among distinct elements are 2 | 4, 2 | 6, 2 | 12, 3 | 6, 3 | 12, 4 | 12, and 6 | 12. The elements with nothing strictly below them are 2 and 3. A least element would have to divide every element. But 2 does not divide 3, and 3 does not divide 2, so neither minimal element is least.

Option A fails because 2 does not divide 3. Option C fails because 2 | 4, so 4 is not minimal. Option D fails because every element divides 12, so 12 is the greatest element and therefore maximal.

### Q4

Answer: A, B, C

The four elements are ∅, {x}, {y}, and {x, y}. Every set contains ∅, so ∅ is least. Neither {x} ⊆ {y} nor {y} ⊆ {x}, so those two sets are incomparable. Every set is contained in {x, y}, so {x, y} is greatest. {x} is not maximal, because {x} is strictly below {x, y}.

### Q5

Answer: C

Under divisibility, 1 | 2 | 4 | 8 is a chain. In a chain the larger of any two elements is their join and the smaller is their meet, so {1, 2, 4, 8} is a lattice.

In {2, 3, 6}, the only common lower bound of 2 and 3 would be a common divisor, and gcd(2, 3) = 1 is not in the set. There is no lower bound in the set, so there is no meet. In {1, 2, 3}, lcm(2, 3) = 6 is not in the set, so 2 and 3 have no join. In {2, 3, 4, 6}, lcm(3, 4) = 12 is not in the set, so 3 and 4 have no join.

### Q6

Answer: 28

Label the chain x1 < x2 < … < x7. The pairs with xi ≤ xj are exactly the pairs i ≤ j. For i = 1 there are 7 choices of j, for i = 2 there are 6, and so on, down to 1:

7 + 6 + 5 + 4 + 3 + 2 + 1 = 28.

The same count is n(n + 1) / 2 with n = 7: 7 × 8 / 2 = 28. This includes the 7 reflexive pairs. Counting only strict pairs gives 7 × 6 / 2 = 21, which omits the diagonal required by reflexivity.

### Q7

Answer: C

The positive divisors of 36 are {1, 2, 3, 4, 6, 9, 12, 18, 36}. An upper bound of 4 and 6 must be a multiple of both, hence a multiple of lcm(4, 6). Since 4 = 2^2 and 6 = 2 × 3,

lcm(4, 6) = 2^2 × 3 = 12.

The multiples of 12 that still lie in the set are 12 and 36. Among those, 12 divides 36, so 12 is the least upper bound.

Option A is gcd(4, 6) = 2, which is the meet, not the join. Option B is not an upper bound: 4 does not divide 6. Option D is an upper bound, but it is larger than 12.

### Q8

Answer: A, B, C

The order is a ≤ a, b ≤ b, c ≤ c, d ≤ d, together with a < b, a < c, b < d, c < d, and a < d. Thus a is below every element, and every element is below d. There is no cover or chain between b and c, so b and c are incomparable.

The upper bounds of {b, c} are the elements above both. That set is exactly {d}, so the least upper bound exists and equals d. Option D is the trap of seeing two different covers into d and concluding that the join fails. A unique common upper bound is the join.

### Q9

Answer: B

In the divisor lattice of 12, the join of two divisors is their lcm and the meet is their gcd. Both operations return a divisor of 12. A subset is a sublattice when it contains the lcm and the gcd of each of its pairs.

For {1, 2, 3, 6} the pairs of distinct elements give:

- gcd(2, 3) = 1 and lcm(2, 3) = 6
- gcd(2, 6) = 2 and lcm(2, 6) = 6
- gcd(3, 6) = 3 and lcm(3, 6) = 6

Pairs involving 1 give gcd 1 and lcm equal to the other element. All of these results lie in {1, 2, 3, 6}.

The other subsets each miss one result:

- lcm(4, 6) = 12, which is not in {2, 4, 6}
- gcd(4, 6) = 2, which is not in {4, 6, 12}
- lcm(2, 3) = 6, which is not in {2, 3, 4, 12}

Being a subposet is not enough: the join or meet computed in the large lattice must land back inside the subset.

### Q10

Answer: 12

The positive divisors of 30 = 2 × 3 × 5 are

{1, 2, 3, 5, 6, 10, 15, 30}.

One divisor covers another when the larger is the smaller multiplied by exactly one prime. The covers are

1 ≺ 2, 1 ≺ 3, 1 ≺ 5,
2 ≺ 6, 2 ≺ 10,
3 ≺ 6, 3 ≺ 15,
5 ≺ 10, 5 ≺ 15,
6 ≺ 30, 10 ≺ 30, 15 ≺ 30.

That is 3 + 2 + 2 + 2 + 3 = 12 covering relations. Pairs such as 1 | 6 are comparable but are not covers, because 2 lies strictly between them. Counting every comparable pair of distinct elements would overcount the Hasse diagram.

### Q11

Answer: A, C, D

In a chain, any two elements are comparable, so the meet is the smaller one and the join is the larger one. A 4-element chain is therefore a lattice, and its largest element is the greatest element. The same holds for every finite nonempty chain.

A one-element poset is totally ordered, and it also contains no two distinct comparable elements, so it is both a chain and an antichain.

A 4-element antichain has no upper bound at all for a pair of distinct elements, because nothing is above either element except itself, and the two elements are incomparable. The pair has no join, so the antichain is not a lattice.

### Q12

Answer: B

A maximum element is an element m such that x ≤ m for every x in P. Such an m is comparable with every element and is above every element, so it is the only maximal element. Three distinct maximal elements therefore make a maximum element impossible.

Option A misuses the word maximum: a maximum element, when it exists, is unique, so there cannot be three of them. Option C is stronger than maximality. An element can sit under one maximal element and be incomparable with the other two; three incomparable elements already form a counterexample to C and a valid partial order, so D is false as well.

### Q13

Answer: 4

Q contains the 2^4 − 1 = 15 nonempty subsets. The singletons {1}, {2}, {3}, and {4} have no nonempty proper subset, so nothing in Q lies strictly below them. Every other nonempty set S has size at least 2, and any one-element subset of S is a strictly smaller element of Q. Thus the minimal elements are exactly those four singletons.

The usual bottom element ∅ has been removed, so the poset has several minimal elements and no least element. Counting all 15 nonempty sets, or counting 1 because a minimum is expected, answers a different question.

### Q14

Answer: A, B, D

Every lattice operation is commutative, and the absorption law a ∧ (a ∨ b) = a holds in every lattice. Also a ≤ b if and only if a ∨ b = b, so D is the order form of the join.

Distributivity is not a lattice axiom. In the lattice M3, with elements {0, a, b, c, 1}, bottom 0, top 1, and a, b, c pairwise incomparable between them,

b ∨ c = 1, so a ∧ (b ∨ c) = a ∧ 1 = a,

while a ∧ b = 0 and a ∧ c = 0, so (a ∧ b) ∨ (a ∧ c) = 0.

Thus a ∧ (b ∨ c) ≠ (a ∧ b) ∨ (a ∧ c). Option C does not hold in every lattice.

### Q15

Answer: 9

B has 2^4 = 16 subsets. A set S is comparable with {1, 2} when S ⊆ {1, 2} or {1, 2} ⊆ S.

The subsets of {1, 2} are ∅, {1}, {2}, and {1, 2}: 4 sets.
The supersets of {1, 2} are {1, 2}, {1, 2, 3}, {1, 2, 4}, and {1, 2, 3, 4}: 4 sets.

The set {1, 2} is in both lists, so the number of comparable sets, including {1, 2} itself, is 4 + 4 − 1 = 7. Therefore the number of incomparable sets is

16 − 7 = 9.

They are {3}, {4}, {1, 3}, {1, 4}, {2, 3}, {2, 4}, {3, 4}, {1, 3, 4}, and {2, 3, 4}. An element is comparable with itself, so {1, 2} is not part of the incomparable count. Omitting that correction produces 16 − 8 = 8.

### Q16

Answer: A

The underlying set is

{(0, 0), (0, 1), (1, 0), (1, 1)},

so there are 4 elements, not 2. The relation is reflexive because 0 ≤ 0 and 1 ≤ 1 in C. It is not an antichain: (0, 0) ≤ (0, 1), (0, 0) ≤ (1, 0), and both middle elements are ≤ (1, 1). The only incomparable pair of distinct elements is {(0, 1), (1, 0)}.

For any two pairs, the componentwise maximum is the join and the componentwise minimum is the meet. Both results are again elements of C × C. Explicitly,

(0, 1) ∨ (1, 0) = (1, 1), (0, 1) ∧ (1, 0) = (0, 0).

Every pair therefore has a join and a meet, and the product is a lattice.
