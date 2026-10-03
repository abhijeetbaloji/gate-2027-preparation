# Monoids — Practice Questions

Original practice for GATE CS. These questions are not from any GATE paper. Attempt the questions before reading the solutions.

## Level 1 — Conceptual

## Q1 — MCQ

Which one of the following is the correct list of requirements for a monoid (M, ·)?

A. · is associative, and M contains a two-sided identity for ·
B. · is commutative, and M contains an identity for ·
C. Every element of M has an inverse, and nothing else is required
D. · is commutative and every element has an inverse

---

## Q2 — MSQ

Let N = {0, 1, 2, …}. Select all that apply.

A. (N, +) is a monoid
B. ({1, 2, 3, …}, +) is a monoid
C. The power set of {a, b}, under union, is a monoid
D. (Z, −) is a monoid, where Z is the set of all integers

---

## Level 2 — Standard GATE Style

## Q3 — MCQ

Let S be a fixed set and let P(S) be its power set. In the monoid (P(S), ∩), the identity element is

A. ∅
B. S
C. an arbitrary singleton subset of S
D. nonexistent

---

## Q4 — NAT

Let Σ = {a, b, c}. In the free monoid Σ* of finite words under concatenation, how many words have length exactly 4?

---

## Q5 — MCQ

Which one of the following monoids is not commutative?

A. (N, +), where N = {0, 1, 2, …}
B. (N, ×), with the same set N
C. ({a, b}*, concatenation)
D. The power set of {a, b}, under union

---

## Level 3 — Multi-Step

## Q6 — MSQ

Let N = {0, 1, 2, …} and consider the monoid (N, +), whose identity is 0. Which of the following are submonoids? Select all that apply.

A. {0, 2, 4, 6, …}
B. {1, 3, 5, 7, …}
C. {0}
D. {1, 2, 3, …}

---

## Q7 — MCQ

Define f: N → N by f(n) = 2n, where N = {0, 1, 2, …} and both copies of N use addition. Which one of the following is true?

A. f preserves the operation and sends the identity to the identity
B. f preserves the operation but sends the identity to something other than the identity
C. f sends the identity to the identity but does not preserve the operation
D. f(n) is not always an element of N

---

## Level 4 — Tricky / Trap-Based

## Q8 — MSQ

Let N = {0, 1, 2, …} and let Z be the set of all integers. Select all that apply.

A. Every group is a monoid
B. Every monoid is a group
C. (N, +) is a monoid and is not a group
D. (Z, +) is a group

---

## Q9 — NAT

Let M = {1, 2, 3, 4} with the operation a ∗ b = max(a, b). How many elements of M do not have an inverse?

---

## Level 5 — Challenge

## Q10 — MCQ

Let D be the set of positive divisors of 18, with the binary operation gcd. The identity element of this monoid is

A. 1
B. 3
C. 9
D. 18

## Answer Key

| Q | Type | Answer |
|---|------|--------|
| 1 | MCQ | A |
| 2 | MSQ | A, C |
| 3 | MCQ | B |
| 4 | NAT | 81 |
| 5 | MCQ | C |
| 6 | MSQ | A, C |
| 7 | MCQ | A |
| 8 | MSQ | A, C, D |
| 9 | NAT | 3 |
| 10 | MCQ | D |

## Detailed Solutions

### Q1

Answer: A

A monoid is a set with an associative binary operation and a two-sided identity e, meaning e · a = a · e = a for every a. Closure is part of having a binary operation on M. Commutativity is optional: it produces a commutative monoid, but it is not required. Inverses are the extra axiom that turns a monoid into a group, so C and D demand too much and omit associativity or the identity.

### Q2

Answer: A, C

Addition on N is associative, and 0 + n = n + 0 = n, so (N, +) is a monoid. Union on a power set is associative, and X ∪ ∅ = ∅ ∪ X = X, so the identity is ∅ and the structure is a monoid.

The positive integers are closed under addition and addition is associative, but there is no positive integer e with e + n = n for every positive n. The identity 0 has been left out, so B is only a semigroup. Subtraction on Z is not associative:

(1 − 1) − 1 = 0 − 1 = −1, while 1 − (1 − 1) = 1 − 0 = 1.

Since the operation is not associative, (Z, −) is not a monoid.

### Q3

Answer: B

The identity e must satisfy X ∩ e = e ∩ X = X for every X ⊆ S. Intersection only gets larger when the other set gets larger, and X ∩ S = X for every X. The empty set is the identity for union, not for intersection: X ∩ ∅ = ∅, which equals X only when X is already empty. A singleton fails as soon as S has some other element that must be retained. The identity exists and is the whole set S.

### Q4

Answer: 81

A word of length 4 is a sequence of 4 symbols, and each symbol has 3 independent choices. The number of such words is

3 × 3 × 3 × 3 = 3^4 = 81.

The empty word ε is the identity of Σ*, but it has length 0, so it is not one of these 81 words. Counting length at most 4 would add the shorter words 1 + 3 + 9 + 27 + 81 = 121 and would answer a different question.

### Q5

Answer: C

Addition and multiplication of non-negative integers are commutative, and X ∪ Y = Y ∪ X, so A, B, and D are commutative monoids. Their identities are 0, 1, and ∅ respectively.

In {a, b}*, concatenation is associative and the empty word is a two-sided identity, so it is a monoid. It is not commutative: the word ab is different from the word ba.

### Q6

Answer: A, C

A submonoid must be closed under the operation and must contain the identity of the original monoid.

The even set contains 0. The sum of two even non-negative integers is even, so it is closed. The set {0} contains the identity, and 0 + 0 = 0, so it is closed.

The odd set does not contain 0. It also fails closure because 1 + 1 = 2 is even. The positive integers are closed under addition, but they do not contain the identity 0 of (N, +). Closure alone does not make a submonoid.

### Q7

Answer: A

The identity of (N, +) is 0, and f(0) = 2 × 0 = 0. For the operation,

f(m + n) = 2(m + n) = 2m + 2n = f(m) + f(n).

Both monoid-homomorphism requirements hold. The value 2n is a non-negative integer whenever n is, so the codomain is correct. The map is not surjective, but a homomorphism is not required to be surjective.

### Q8

Answer: A, C, D

A group has an associative operation, an identity, and inverses. Forgetting the inverses leaves a monoid, so every group is a monoid. The converse is false: a monoid need not have inverses.

In (N, +) the identity is 0 and addition is associative, but a positive integer n has no n' in N with n + n' = 0. Thus (N, +) is a monoid and not a group. In Z every integer n has additive inverse −n, addition is associative, and the identity is 0, so (Z, +) is a group. It is also a monoid, which does not conflict with D.

### Q9

Answer: 3

The operation stays inside M because the maximum of two elements of M is one of those two elements. It is associative:

max(max(a, b), c) = max(a, b, c) = max(a, max(b, c)).

The identity is 1, because max(1, a) = a for every a in M. An inverse of a would be an element b with max(a, b) = 1. That forces a = 1 and b = 1. For a = 2, 3, or 4, max(a, b) ≥ a > 1 for every b. Exactly those three elements have no inverse.

This is a monoid in which most elements are not invertible. Having an identity does not provide inverses.

### Q10

Answer: D

The positive divisors of 18 are {1, 2, 3, 6, 9, 18}. The gcd of two divisors of 18 is again a divisor of 18, so the operation is closed. The gcd operation is associative and commutative. The identity must be an element e such that gcd(e, d) = d for every divisor d. That says e is a multiple of every divisor of 18, and e itself must be a divisor of 18. The only such element is 18:

gcd(18, 1) = 1, gcd(18, 2) = 2, gcd(18, 3) = 3,
gcd(18, 6) = 6, gcd(18, 9) = 9, gcd(18, 18) = 18.

Option A is the identity for lcm, not for gcd: gcd(1, 6) = 1, which is not 6. The elements 3 and 9 fail in the same way, since gcd(3, 2) = 1 ≠ 2 and gcd(9, 2) = 1 ≠ 2.
