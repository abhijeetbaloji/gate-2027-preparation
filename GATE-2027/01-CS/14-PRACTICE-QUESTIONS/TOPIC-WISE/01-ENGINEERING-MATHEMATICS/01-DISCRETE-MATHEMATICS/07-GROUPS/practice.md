# Groups — Practice Questions

Original practice for GATE CS. These questions are not from any GATE paper. Attempt the questions before reading the solutions.

## Level 1 — Conceptual

## Q1 — MCQ

Consider the set of all rational numbers under multiplication. Which group axiom fails?

A. Closure
B. Associativity
C. Existence of an identity
D. Existence of inverses

---

## Q2 — MCQ

Which one of the following is true in every group?

A. There may be two distinct identity elements
B. The identity element is unique
C. Every element is an identity element
D. An identity element need only act on the left

---

## Q3 — NAT

The symmetric group S_4 is the group of all permutations of 4 distinct objects, under composition. How many elements does S_4 have?

---

## Q4 — MSQ

Select all that apply.

A. The integers under addition form a group
B. The non-negative integers under addition form a group
C. The integers modulo 5 under addition modulo 5 form a group
D. The rational numbers under multiplication form a group

---

## Level 2 — Standard GATE Style

## Q5 — MCQ

In the additive group of integers modulo 6, the order of the element 2 is

A. 1
B. 2
C. 3
D. 6

---

## Q6 — MCQ

Let G be a finite group with |G| = 12. Which one of the following cannot be the order of a subgroup of G?

A. 1
B. 4
C. 5
D. 6

---

## Q7 — NAT

How many generators does the cyclic group of integers modulo 8, under addition modulo 8, have?

---

## Q8 — MCQ

Which one of the following is true of the symmetric group S_3?

A. S_3 is abelian because every group of order 6 is abelian
B. Composition of permutations in S_3 need not commute
C. S_3 is abelian because |S_3| is even
D. S_3 has order 8

---

## Q9 — MSQ

Let G be the cyclic group of integers modulo 12 under addition. Select all that apply.

A. G has a subgroup of order 4
B. G has a subgroup of order 5
C. G has a subgroup of order 6
D. G is a subgroup of G

---

## Level 3 — Multi-Step

## Q10 — MCQ

In every group, the inverse of a product ab is

A. a^(−1) b^(−1)
B. b^(−1) a^(−1)
C. ab
D. ba

---

## Q11 — MSQ

Let U = {1, 3, 5, 7} with multiplication modulo 8. Select all that apply.

A. U is closed under this operation
B. 3 · 3 ≡ 1 (mod 8), so 3 is its own inverse in U
C. 2 is an element of U
D. 1 is the identity element for this operation on U

---

## Q12 — MCQ

Let G be a group of order 11. Which one of the following is true?

A. G is cyclic, and every non-identity element generates G
B. G has a subgroup of order 2
C. G is non-abelian
D. G has exactly 11 subgroups

---

## Q13 — MSQ

Let G be the integers modulo 7 under addition modulo 7. Select all that apply.

A. G is cyclic
B. The order of 1 is 7
C. The order of 0 is 7
D. G is abelian

---

## Level 4 — Tricky / Trap-Based

## Q14 — MCQ

Which one of the following is true?

A. If d divides |G|, then every finite group G has a subgroup of order d
B. If H is a subgroup of a finite group G, then |H| divides |G|
C. Every monoid is a group
D. The integers under multiplication form a group

---

## Q15 — NAT

In the additive group of integers modulo 8, how many elements have order exactly 2?

---

## Q16 — MSQ

Select all that apply.

A. In every group, (ab)^(−1) = a^(−1) b^(−1)
B. In every group, (a^(−1))^(−1) = a
C. In every group, the inverse of an element is unique
D. In every abelian group, (ab)^(−1) = a^(−1) b^(−1)

---

## Level 5 — Challenge

## Q17 — NAT

How many subgroups does the cyclic group of integers modulo 18, under addition, have?

---

## Q18 — MCQ

Let U = {k : 1 ≤ k ≤ 8 and gcd(k, 9) = 1}, with multiplication modulo 9. Which one of the following is true?

A. (U, ×) is a group of order 6
B. (U, ×) is a group of order 8
C. 3 belongs to U, and 3 has a multiplicative inverse modulo 9
D. Multiplication modulo 9 is not associative on U

## Answer Key

| Q | Type | Answer |
|---|------|--------|
| 1 | MCQ | D |
| 2 | MCQ | B |
| 3 | NAT | 24 |
| 4 | MSQ | A, C |
| 5 | MCQ | C |
| 6 | MCQ | C |
| 7 | NAT | 4 |
| 8 | MCQ | B |
| 9 | MSQ | A, C, D |
| 10 | MCQ | B |
| 11 | MSQ | A, B, D |
| 12 | MCQ | A |
| 13 | MSQ | A, B, D |
| 14 | MCQ | B |
| 15 | NAT | 1 |
| 16 | MSQ | B, C, D |
| 17 | NAT | 6 |
| 18 | MCQ | A |

## Detailed Solutions

### Q1

Answer: D

The product of two rational numbers is rational, multiplication is associative, and 1 is an identity. The element 0 is rational, but there is no rational q with 0 · q = 1. Removing 0 would repair the inverse axiom; keeping every rational does not. Closure, associativity, and the identity are not the failing axiom.

### Q2

Answer: B

Suppose e and f are both identities. Then e = e · f because f is a right identity, and e · f = f because e is a left identity. Hence e = f. The identity is unique, it is two-sided, and only that one element acts as an identity. A group of order greater than 1 has non-identity elements, so C is false.

### Q3

Answer: 24

A permutation of 4 objects is a bijection from a 4-element set to itself. There are 4 choices for the image of the first object, then 3 remaining choices, then 2, then 1:

|S_4| = 4! = 4 × 3 × 2 × 1 = 24.

The count 2^4 = 16 is the number of subsets of a 4-element set, not the number of bijections.

### Q4

Answer: A, C

The integers under addition are closed and associative, the identity is 0, and the inverse of n is −n. Integers modulo 5 under addition are the cyclic group of order 5: the identity is 0, and the inverse of k is 5 − k when k ≠ 0.

The non-negative integers are closed under addition and have identity 0, but 1 has no non-negative additive inverse. They form a monoid, not a group. The rational numbers under multiplication include 0, which has no multiplicative inverse, so that structure is not a group.

### Q5

Answer: C

Work in Z_6. Adding 2 repeatedly:

2 ≡ 2, 2 + 2 ≡ 4, 2 + 2 + 2 ≡ 6 ≡ 0 (mod 6).

The first positive number of summands that produces the identity 0 is 3, so the order is 3. It is not 6: although 3 divides 6, the order is the smallest such positive integer, not the group order. The identity 0 is the only element of order 1.

### Q6

Answer: C

Lagrange’s theorem says that if H is a subgroup of a finite group G, then |H| divides |G|. Here the positive divisors of 12 are 1, 2, 3, 4, 6, and 12. Since 5 does not divide 12, no subgroup can have order 5. The orders 1, 4, and 6 all divide 12, so Lagrange does not forbid them. In particular the trivial subgroup has order 1.

### Q7

Answer: 4

The group is cyclic of order 8, generated by 1. An element k generates it precisely when gcd(k, 8) = 1, and the number of such residue classes is Euler’s totient φ(8). Since 8 = 2^3,

φ(8) = 8 × (1 − 1/2) = 4.

The generators are 1, 3, 5, and 7. For example, the multiples of 3 modulo 8 are 3, 6, 1, 4, 7, 2, 5, 0, which exhaust the group. The element 2 does not: its multiples are only 0, 2, 4, and 6.

### Q8

Answer: B

|S_3| = 3! = 6, so D is false. Let a = (1 2) and b = (1 3), with composition applying the right-hand permutation first. Then

b sends 1 to 3, and a fixes 3, so ab sends 1 to 3;
a sends 1 to 2, and b fixes 2, so ba sends 1 to 2.

Thus ab ≠ ba. The group is not abelian. Order 6 does not force commutativity, and neither does even order. There are non-abelian groups of order 6; S_3 is one of them.

### Q9

Answer: A, C, D

Z_12 is cyclic of order 12. For each positive divisor d of 12 there is exactly one subgroup of order d. The divisors are 1, 2, 3, 4, 6, and 12, so subgroups of orders 4 and 6 exist. Concretely, {0, 3, 6, 9} is a subgroup of order 4, and {0, 2, 4, 6, 8, 10} is a subgroup of order 6. Every group is a subgroup of itself, so D is true. Order 5 does not divide 12, so Lagrange’s theorem forbids a subgroup of order 5.

### Q10

Answer: B

Compute (ab)(b^(−1) a^(−1)) by associating in the middle:

(ab)(b^(−1) a^(−1)) = a (b b^(−1)) a^(−1) = a e a^(−1) = a a^(−1) = e.

The product in the other order is also e. Therefore the two-sided inverse of ab is b^(−1) a^(−1). The reversed product a^(−1) b^(−1) equals this only when the relevant elements commute. Option C would say ab has finite order dividing 2. Option D is the product in the other order, which need not be the inverse.

### Q11

Answer: A, B, D

The products modulo 8 are

1·1 ≡ 1, 1·3 ≡ 3, 1·5 ≡ 5, 1·7 ≡ 7,
3·3 ≡ 9 ≡ 1, 3·5 ≡ 15 ≡ 7, 3·7 ≡ 21 ≡ 5,
5·5 ≡ 25 ≡ 1, 5·7 ≡ 35 ≡ 3, 7·7 ≡ 49 ≡ 1.

Every product is again in {1, 3, 5, 7}, so U is closed. In particular 3 · 3 ≡ 1, so 3 is its own inverse. Multiplying by 1 changes nothing, so 1 is the identity. The residue 2 shares a factor with 8, and 2 is not in the listed set. This set is the multiplicative group of units modulo 8.

### Q12

Answer: A

The order of any element divides 11 by Lagrange’s theorem. The positive divisors of 11 are 1 and 11. The only element of order 1 is the identity, so every other element has order 11 and therefore generates G. A group generated by one element is cyclic. Cyclic groups are abelian, so C is false.

A subgroup of order 2 would require 2 to divide 11, which it does not. The only subgroups are {e} and G, so there are 2 subgroups, not 11. The number 11 is the number of elements, and also one more than the number of generators: φ(11) = 10 generators.

### Q13

Answer: A, B, D

Z_7 is cyclic, generated by 1, because the multiples of 1 produce every residue. Addition is commutative, so the group is abelian. The sums of 1 are 1, 2, 3, 4, 5, 6, 0, and the first time the identity appears is at the seventh sum, so 1 has order 7.

The identity 0 satisfies 1 · 0 = 0 already, so its order is 1, not 7. Only a generator has order equal to the group order. Since 7 is prime, the non-identity elements are exactly the generators, but 0 is not one of them.

### Q14

Answer: B

Lagrange’s theorem is exactly B: the left cosets of H partition G into blocks of size |H|, so |G| = |H| · [G : H] and |H| divides |G|.

The converse is false: a divisor of |G| need not be the order of any subgroup. The alternating group A_4 has order 12, so 6 divides |A_4|, but A_4 has no subgroup of order 6. Indeed A_4 contains 8 three-cycles. A subgroup H of order 6 would have index 2, hence would be normal, and every square of an element of A_4 would lie in H. Every three-cycle g satisfies g = (g^(−1))^2, so all 8 three-cycles would lie in H, which cannot fit in a set of 6 elements. Option A states that false converse. A monoid need not have inverses, so C is false. Under multiplication the integer 0 has no inverse, and 2 has no integer inverse either, so D is false.

### Q15

Answer: 1

The identity is 0. For k in {0, 1, …, 7}, the order is the smallest positive m with m k ≡ 0 (mod 8).

- 0 has order 1.
- 1 has order 8, since the first return to 0 is after eight steps. The same holds for 3, 5, and 7, each of which is coprime to 8.
- 2 + 2 + 2 + 2 = 8 ≡ 0, and no smaller positive count works, so 2 has order 4. Likewise 6 ≡ −2 has order 4.
- 4 + 4 = 8 ≡ 0, while 4 itself is not 0, so 4 has order 2.

Exactly one element, namely 4, has order 2. The two solutions of 2x ≡ 0 (mod 8) are 0 and 4, but 0 has order 1. Counting every self-inverse element includes the identity and gives 2, which is not the number of elements of order exactly 2.

### Q16

Answer: B, C, D

If b is an inverse of a, then a is an inverse of b, because the same two products equal the identity. Uniqueness of inverses therefore gives (a^(−1))^(−1) = a. Uniqueness itself is the usual argument: if b and c both invert a, then b = b e = b (a c) = (b a) c = e c = c.

The general inverse formula is (ab)^(−1) = b^(−1) a^(−1), not a^(−1) b^(−1). In S_3, let a = (1 2) and b = (1 3), each equal to its own inverse, and compose by applying the right factor first. Then ab = (1 3 2) and (ab)^(−1) = (1 2 3). But a^(−1) b^(−1) = ab = (1 3 2), which is different. So A is false in a non-abelian group.

If the group is abelian, a^(−1) b^(−1) = b^(−1) a^(−1), so the two formulas agree and D holds.

### Q17

Answer: 6

Z_18 is cyclic of order 18. Cyclic groups have exactly one subgroup for each positive divisor of the group order. Factor 18 = 2 × 3^2. The positive divisors are

1, 2, 3, 6, 9, 18,

and there are 6 of them. The subgroup count is therefore 6. It is smaller than 18: most elements do not each generate a different subgroup. For example 1 and 5 lie in the same subgroup, namely the whole group, because both are generators.

### Q18

Answer: A

The integers from 1 to 8 that are coprime to 9 are the integers not divisible by 3:

U = {1, 2, 4, 5, 7, 8}.

There are 6 such residues, which is also φ(9) = 9 × (1 − 1/3) = 6. This is the multiplicative group of units modulo 9: it is closed because a product of units is a unit, multiplication modulo 9 is associative, the identity is 1, and every unit has an inverse modulo 9. Thus (U, ×) is a group of order 6.

Order 8 would count every nonzero residue modulo 9. That set is not closed in the sense of units: 3 · 3 = 9 ≡ 0, and 3 is not even in U. Also gcd(3, 9) = 3 ≠ 1, so 3 has no inverse modulo 9. Associativity does hold, because multiplication of integers is associative and reduction modulo 9 preserves it.
