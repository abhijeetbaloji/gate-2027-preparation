# Relations — Practice Questions

Original practice for GATE CS. These questions are not from any GATE paper. Attempt the questions before reading the solutions.

## Level 1 — Conceptual

## Q1 — MCQ

A relation \(R\) on a set \(A\) is reflexive when

A. \((a,a) \in R\) for every \(a \in A\)
B. \((a,b) \in R\) implies \((b,a) \in R\)
C. \((a,a) \notin R\) for every \(a \in A\)
D. \((a,b) \in R\) and \((b,a) \in R\) imply \(a = b\)

---

## Q2 — MSQ

Let \(A = \{1,2,3\}\) and
\[
R = \{(1,1),(2,2),(3,3),(1,2),(2,1)\}.
\]
Which properties does \(R\) have?

Select all that apply.

A. Reflexive
B. Symmetric
C. Antisymmetric
D. Transitive

---

## Q3 — NAT

Enter the number of binary relations on a set with \(3\) elements.

---

## Q4 — MCQ

An equivalence relation on a set is a relation that is

A. reflexive, symmetric, and transitive
B. reflexive, antisymmetric, and transitive
C. symmetric and transitive, with reflexivity left optional
D. reflexive and symmetric, with transitivity left optional

---

## Level 2 — Standard GATE Style

## Q5 — MCQ

The number of symmetric relations on a set with \(3\) elements is

A. \(8\)
B. \(64\)
C. \(512\)
D. \(27\)

---

## Q6 — NAT

Enter the number of reflexive relations on a set with \(4\) elements.

---

## Q7 — MSQ

Let \(A = \{1,2,3,4,5\}\) and define \(a\,R\,b\) if and only if \(|a-b| \le 1\). Which properties does \(R\) have?

Select all that apply.

A. Reflexive
B. Symmetric
C. Transitive
D. Antisymmetric

---

## Q8 — MCQ

Let \(R = \{(1,2),(2,3),(1,1)\}\) and \(S = \{(2,2),(3,1),(1,3)\}\) be relations on \(\{1,2,3\}\). Define
\[
S \circ R = \{(a,c) \mid \text{there exists } b \text{ with } (a,b) \in R \text{ and } (b,c) \in S\}.
\]
Then \(S \circ R\) equals

A. \(\{(1,2),(1,3),(2,1)\}\)
B. \(\{(2,3),(3,1),(3,2)\}\)
C. \(\{(1,1),(2,2),(3,3)\}\)
D. \(\{(1,2),(2,3),(1,1)\}\)

---

## Q9 — MCQ

The reflexive closure of \(T = \{(1,2),(2,3),(3,1)\}\) on \(\{1,2,3\}\) contains how many ordered pairs?

A. \(3\)
B. \(6\)
C. \(9\)
D. \(12\)

---

## Q10 — NAT

Enter the number of equivalence relations on a set with \(3\) elements.

---

## Level 3 — Multi-Step

## Q11 — MCQ

The empty relation on the nonempty set \(\{1,2,3\}\) is

A. reflexive and symmetric
B. symmetric and transitive, but not reflexive
C. transitive, but not symmetric
D. reflexive, symmetric, and transitive

---

## Q12 — NAT

Let \(R = \{(1,2),(2,4),(4,3),(3,3),(1,1)\}\) on \(\{1,2,3,4\}\). Enter the number of ordered pairs in the transitive closure of \(R\).

---

## Q13 — MSQ

Let \(T = \{(1,2),(2,3),(3,1)\}\) on \(\{1,2,3\}\). Which statements are true?

Select all that apply.

A. The symmetric closure of \(T\) has \(6\) ordered pairs.
B. The reflexive closure of \(T\) has \(6\) ordered pairs.
C. The transitive closure of \(T\) has \(6\) ordered pairs.
D. The transitive closure of \(T\) has \(9\) ordered pairs.

---

## Q14 — MCQ

Let \(A = \{1,2,\ldots,10\}\) and define \(a\,R\,b\) if and only if \(a \equiv b \pmod{4}\). The number of equivalence classes of \(R\) is

A. \(2\)
B. \(4\)
C. \(5\)
D. \(10\)

---

## Level 4 — Tricky / Trap-Based

## Q15 — MCQ

The number of antisymmetric relations on a set with \(2\) elements is

A. \(4\)
B. \(8\)
C. \(12\)
D. \(16\)

---

## Q16 — MSQ

Which statements are true for every set \(A\) that has at least one element?

Select all that apply.

A. The empty relation on \(A\) is reflexive.
B. The empty relation on \(A\) is symmetric.
C. The empty relation on \(A\) is transitive.
D. Every symmetric and transitive relation on \(A\) is reflexive.

---

## Q17 — MCQ

A student counts the relations on an \(n\)-element set as \(2^{n}\). For \(n = 3\), the correct count exceeds the student’s count by

A. \(5\)
B. \(504\)
C. \(8\)
D. \(256\)

---

## Level 5 — Challenge

## Q18 — MCQ

The number of relations on a \(4\)-element set that are both reflexive and symmetric is

A. \(64\)
B. \(256\)
C. \(4096\)
D. \(1024\)

---

## Q19 — NAT

Enter the number of equivalence relations on a set with \(4\) elements.

---

## Q20 — MSQ

On \(A = \{2,3,6,12\}\), define \(a\,R\,b\) if and only if \(a\) divides \(b\). Which properties does \(R\) have?

Select all that apply.

A. Reflexive
B. Symmetric
C. Antisymmetric
D. Transitive

---

## Answer Key

| Q | Type | Answer |
|---|------|--------|
| 1 | MCQ | A |
| 2 | MSQ | A, B, D |
| 3 | NAT | 512 |
| 4 | MCQ | A |
| 5 | MCQ | B |
| 6 | NAT | 4096 |
| 7 | MSQ | A, B |
| 8 | MCQ | A |
| 9 | MCQ | B |
| 10 | NAT | 5 |
| 11 | MCQ | B |
| 12 | NAT | 8 |
| 13 | MSQ | A, B, D |
| 14 | MCQ | B |
| 15 | MCQ | C |
| 16 | MSQ | B, C |
| 17 | MCQ | B |
| 18 | MCQ | A |
| 19 | NAT | 15 |
| 20 | MSQ | A, C, D |

## Detailed Solutions

### Q1

Answer: A

Reflexivity quantifies over every element of the underlying set: each element must be related to itself. On a matrix, that means every diagonal entry is \(1\).

B is symmetry. A reflexive relation need not be symmetric; the usual order on \(\{1,2\}\) contains \((1,2)\) and both loops, but not \((2,1)\).

C is irreflexivity. It forbids the pairs that reflexivity demands.

D is antisymmetry. It allows loops. It does not by itself force every loop to be present, so a relation can be antisymmetric and still miss some \((a,a)\).

### Q2

Answer: A, B, D

The pairs \((1,1)\), \((2,2)\), and \((3,3)\) are all present, so \(R\) is reflexive.

Every off-diagonal pair has its reverse: \((1,2)\) is present with \((2,1)\), and \((3,3)\) is its own reverse. So \(R\) is symmetric.

It is not antisymmetric. Both \((1,2)\) and \((2,1)\) belong to \(R\), but \(1 \neq 2\).

It is transitive. The nontrivial chains are \((1,2)\) followed by \((2,1)\), which requires \((1,1)\), and \((2,1)\) followed by \((1,2)\), which requires \((2,2)\). Both required pairs are present. Chains that pass through a loop, such as \((1,2)\) followed by \((2,2)\), demand a pair that is already in \(R\). Nothing in \(R\) leaves the block \(\{1,2\}\) toward \(3\) except the loop at \(3\). Thus \(R\) is an equivalence relation, with classes \(\{1,2\}\) and \(\{3\}\).

### Q3

Answer: 512

A binary relation on \(A\) is any subset of \(A \times A\). If \(|A| = 3\), then \(|A \times A| = 9\). Each of these \(9\) ordered pairs can be included or excluded, so the number of relations is
\[
2^{3^{2}} = 2^{9} = 512.
\]
The count \(2^{3} = 8\) would be right for subsets of \(A\), not for subsets of \(A \times A\). The count \(3^{2} = 9\) is only the number of possible ordered pairs.

### Q4

Answer: A

Equivalence means the three properties reflexive, symmetric, and transitive all hold. The equivalence classes then partition the underlying set: they are nonempty, pairwise disjoint, and their union is the whole set.

B replaces symmetry with antisymmetry. Those three properties define a partial order. Equality is both an equivalence and a partial order, but a general equivalence such as “same remainder modulo \(4\)” is symmetric and is not antisymmetric once a class has two distinct elements.

C omits reflexivity. The empty relation on a nonempty set is symmetric and transitive, and it is not reflexive, so it is not an equivalence. Symmetry and transitivity do not force the diagonal.

D omits transitivity. On \(\{1,2,3\}\), the relation of differing by at most \(1\), including loops, is reflexive and symmetric. It contains \((1,2)\) and \((2,3)\) but not \((1,3)\), so it is not transitive and not an equivalence.

### Q5

Answer: B

In a symmetric relation the diagonal entries are free, and each unordered pair \(\{i,j\}\) with \(i < j\) contributes one binary choice: include both \((i,j)\) and \((j,i)\), or include neither. For \(n = 3\) there are \(3\) diagonal choices and \(\binom{3}{2} = 3\) off-diagonal choices, so the number of independent bits is
\[
\frac{n(n+1)}{2} = \frac{3 \cdot 4}{2} = 6.
\]
The number of symmetric relations is \(2^{6} = 64\).

A is \(2^{3} = 8\). That is the number of reflexive symmetric relations on three elements: the diagonal is then fixed as present, and only the three upper pairs remain free. C is \(2^{9} = 512\), the number of all relations. D is \(3^{3} = 27\), which counts a different constraint pattern and is not the symmetric-relation count.

### Q6

Answer: 4096

A reflexive relation on an \(n\)-element set must contain all \(n\) diagonal pairs. The remaining \(n^{2} - n\) ordered pairs are free. For \(n = 4\),
\[
n^{2} - n = 16 - 4 = 12, \qquad 2^{12} = 4096.
\]
Forcing the diagonal out, rather than in, counts irreflexive relations and gives the same power of two, but that is a different family. Forgetting to reserve the diagonal and computing \(2^{16}\) counts every relation on a four-element set.

### Q7

Answer: A, B

For every \(a\), \(|a-a| = 0 \le 1\), so every loop is present and \(R\) is reflexive.

If \(|a-b| \le 1\), then \(|b-a| \le 1\), so \(R\) is symmetric.

It is not transitive. Both \((1,2)\) and \((2,3)\) are in \(R\), but \(|1-3| = 2 > 1\), so \((1,3) \notin R\).

It is not antisymmetric. Both \((1,2)\) and \((2,1)\) are in \(R\), and \(1 \neq 2\). Symmetry of a relation that contains at least one pair of distinct elements always destroys antisymmetry.

### Q8

Answer: A

The definition applies \(R\) first and \(S\) second. Check each pair of \(R\):

- \((1,2) \in R\) and \((2,2) \in S\) give \((1,2)\).
- \((2,3) \in R\) and \((3,1) \in S\) give \((2,1)\).
- \((1,1) \in R\) and \((1,3) \in S\) give \((1,3)\).

No other pair of \(S\) starts at the second coordinate of a pair from \(R\). Therefore
\[
S \circ R = \{(1,2),(1,3),(2,1)\}.
\]

B is \(R \circ S\), the composition in the opposite order. From \(S\) then \(R\): \((2,2)\) followed by \((2,3)\) gives \((2,3)\); \((3,1)\) followed by \((1,2)\) gives \((3,2)\) and \((3,1)\) followed by \((1,1)\) gives \((3,1)\). The pair \((1,3) \in S\) has no continuation in \(R\) from \(3\). So \(R \circ S = \{(2,3),(3,1),(3,2)\}\), which is not \(S \circ R\).

C is the identity, and none of its three loops was produced above. D is \(R\) itself. Composition does not return the first relation unless the second relation acts as an identity on the relevant intermediate elements.

### Q9

Answer: B

The reflexive closure is the smallest reflexive relation containing \(T\). Add the missing loops and keep the pairs already present:
\[
T \cup \{(1,1),(2,2),(3,3)\} = \{(1,2),(2,3),(3,1),(1,1),(2,2),(3,3)\}.
\]
That set has \(3 + 3 = 6\) ordered pairs.

A counts \(T\) before the loops are added, so it is not yet reflexive: \((1,1)\) is missing. C is the size of the transitive closure of this cycle. Closing the cycle produces every ordered pair on \(\{1,2,3\}\), which is \(9\) pairs, not \(6\). The reflexive closure does not add shortcut edges such as \((1,3)\). D exceeds \(|A \times A| = 9\), so it cannot be the size of any relation on this set.

### Q10

Answer: 5

Equivalence relations on a finite set are in one-to-one correspondence with partitions of that set. For \(\{1,2,3\}\) the partitions are:

- \(\{\{1\},\{2\},\{3\}\}\)
- \(\{\{1,2\},\{3\}\}\)
- \(\{\{1,3\},\{2\}\}\)
- \(\{\{2,3\},\{1\}\}\)
- \(\{\{1,2,3\}\}\)

There are \(5\) partitions, hence \(5\) equivalence relations. Counting only the partition into singletons and the one-block partition misses the three partitions of type \(2+1\). The number of all relations, \(512\), and the number of reflexive symmetric relations, \(8\), both ignore transitivity.

### Q11

Answer: B

Let \(E = \emptyset\) on \(A = \{1,2,3\}\).

Reflexivity fails because \((1,1) \notin E\). One missing loop is enough, so A and D are false.

Symmetry holds vacuously. The implication “if \((a,b) \in E\), then \((b,a) \in E\)” has a false antecedent for every pair, because \(E\) has no pairs. C is therefore false: the empty relation is symmetric.

Transitivity holds vacuously for the same reason. There are no pairs \((a,b)\) and \((b,c)\) in \(E\) that could demand \((a,c)\). So \(E\) is symmetric and transitive, and it is not reflexive.

### Q12

Answer: 8

The transitive closure is the set of pairs \((a,c)\) for which \(R\) has a directed path from \(a\) to \(c\) of length at least \(1\). The pairs already in \(R\) are
\[
(1,2),\ (2,4),\ (4,3),\ (3,3),\ (1,1).
\]
New pairs come from composing these edges:

- \((1,2)\) then \((2,4)\) gives \((1,4)\).
- \((2,4)\) then \((4,3)\) gives \((2,3)\).
- \((1,4)\) then \((4,3)\) gives \((1,3)\).
- \((4,3)\) then \((3,3)\) gives \((4,3)\), already present.
- \((2,3)\) then \((3,3)\) gives \((2,3)\), already present.

There is no edge into \(2\) except from \(1\), and \(1\) already has its loop. There is no edge out of \(3\) except the loop, so nothing reaches a new target from \(3\). The closure is
\[
\{(1,1),(1,2),(1,3),(1,4),(2,3),(2,4),(3,3),(4,3)\},
\]
which has \(8\) ordered pairs. Adding every missing loop would produce the reflexive-transitive closure, a larger set: \((2,2)\) and \((4,4)\) are still absent from the transitive closure.

### Q13

Answer: A, B, D

The symmetric closure adds the reverse of every pair. The reverses \((2,1)\), \((3,2)\), and \((1,3)\) are all new, and \(T\) had no loops to copy. The closure has the original \(3\) pairs plus these \(3\) reverses, so A is true and the size is \(6\).

The reflexive closure adds \((1,1)\), \((2,2)\), and \((3,3)\). None of these is in \(T\), so the size is \(3 + 3 = 6\) and B is true.

The transitive closure follows the cycle. From \((1,2)\) and \((2,3)\) add \((1,3)\); from \((2,3)\) and \((3,1)\) add \((2,1)\); from \((3,1)\) and \((1,2)\) add \((3,2)\). Continuing closes the loops: \((1,3)\) with \((3,1)\) gives \((1,1)\), \((2,1)\) with \((1,2)\) gives \((2,2)\), and \((3,2)\) with \((2,3)\) gives \((3,3)\). Every ordered pair on \(\{1,2,3\}\) appears, so the closure has \(3^{2} = 9\) pairs. D is true and C is false. A three-cycle is not already transitive, and its transitive closure is the full relation, not a six-pair set.

### Q14

Answer: B

Congruence modulo \(4\) is an equivalence relation on any set of integers: it is reflexive, symmetric, and transitive because equality of remainders has those properties. The classes inside \(A\) are the nonempty sets of elements with a fixed remainder.

The remainders of \(1\) through \(10\) are \(1,2,3,0,1,2,3,0,1,2\). All four possible remainders occur:

- remainder \(0\): \(\{4,8\}\)
- remainder \(1\): \(\{1,5,9\}\)
- remainder \(2\): \(\{2,6,10\}\)
- remainder \(3\): \(\{3,7\}\)

There are \(4\) classes. A counts only even and odd residue patterns, which is modulus \(2\). C might come from listing five representative numbers rather than four remainders. D is \(|A|\), the number of classes of the identity relation, not of congruence modulo \(4\).

### Q15

Answer: C

Let the ground set be \(\{1,2\}\). Antisymmetry forbids exactly one configuration of the off-diagonal pair: \((1,2)\) and \((2,1)\) cannot both be present. The legal off-diagonal choices are therefore “only \((1,2)\)”, “only \((2,1)\)”, or “neither”, which is \(3\) choices. Each diagonal entry may be present or absent, giving \(2^{2} = 4\) choices. The choices are independent, so the number of antisymmetric relations is
\[
2^{2} \cdot 3^{1} = 12.
\]
In general, on an \(n\)-element set the count is \(2^{n} \cdot 3^{n(n-1)/2}\), because each diagonal entry is free and each unordered off-diagonal pair has three legal orientations.

B is the number of symmetric relations on a two-element set, \(2^{2(2+1)/2} = 2^{3} = 8\). Symmetry ties the two off-diagonal entries together, whereas antisymmetry forbids them from being \(1\) at the same time; the counts are not equal. D is \(2^{4} = 16\), every relation on a two-element set, including the four relations that contain both \((1,2)\) and \((2,1)\). A is \(2^{2} = 4\), only the subsets of the diagonal.

### Q16

Answer: B, C

Let \(A\) be nonempty and let \(E\) be the empty relation on \(A\).

A is false. Pick \(a \in A\). Reflexivity requires \((a,a) \in E\), and the empty relation does not contain it.

B is true. The symmetry implication has no antecedent pair to check.

C is true. The transitivity implication has no two-step chain to check.

D is false. The same empty relation is symmetric and transitive, and Q11 already recorded that it is not reflexive when \(A\) is nonempty. Symmetry and transitivity do not produce the missing loops unless some pair \((a,b)\) is actually present and can be reversed and composed. With no pairs, that derivation never starts.

### Q17

Answer: B

The correct count uses the \(n^{2}\) possible ordered pairs. For \(n = 3\),
\[
2^{3^{2}} = 2^{9} = 512.
\]
The student’s count is \(2^{3} = 8\). The excess is
\[
512 - 8 = 504.
\]
A is \(5\), which is neither count and is not their difference. C is the student’s count \(8\), not the excess of the correct count over that count. D is \(2^{8} = 256\), half of \(512\), and \(512 - 8\) is not \(256\).

### Q18

Answer: A

Reflexivity fixes all \(4\) diagonal pairs as present. Symmetry then leaves one free bit for each unordered pair \(\{i,j\}\) with \(i < j\): include both directions, or include neither. The number of such pairs is
\[
\binom{4}{2} = 6,
\]
so the number of reflexive symmetric relations is \(2^{6} = 64\).

B is \(2^{8}\). It does not match either the six upper pairs or the twelve off-diagonal entries of a \(4 \times 4\) matrix. C is \(2^{16-4} = 2^{12} = 4096\), the reflexive relations with no symmetry restriction. D is \(2^{4 \cdot 5 / 2} = 2^{10} = 1024\), the symmetric relations with a free diagonal. Those relations need not be reflexive.

### Q19

Answer: 15

Count the partitions of a \(4\)-element set by block type. Let the set be \(\{1,2,3,4\}\).

- One block, type \(4\): \(\{\{1,2,3,4\}\}\). There is \(1\) such partition.
- Type \(3+1\): the singleton can be any of the \(4\) elements, and the other three form one block. There are \(4\) partitions.
- Type \(2+2\): the three partitions are \(\{\{1,2\},\{3,4\}\}\), \(\{\{1,3\},\{2,4\}\}\), and \(\{\{1,4\},\{2,3\}\}\). Choosing an ordered sequence of two pairs would double-count each partition, so the count is \(\binom{4}{2}/2 = 3\), not \(6\).
- Type \(2+1+1\): choose the unique doubleton in \(\binom{4}{2} = 6\) ways. The other two elements are singletons, and there is nothing further to choose. There are \(6\) partitions.
- Type \(1+1+1+1\): only the partition into four singletons. There is \(1\).

Add these disjoint cases:
\[
1 + 4 + 3 + 6 + 1 = 15.
\]
Each partition determines one equivalence relation, namely “lie in the same block,” and every equivalence relation arises once this way. The reflexive symmetric count \(2^{6} = 64\) from Q18 includes relations that are not transitive, so it is larger than \(15\).

### Q20

Answer: A, C, D

The relation contains a pair \((a,b)\) when \(b\) is a multiple of \(a\). The full set of pairs is
\[
\begin{align*}
&\{(2,2),(2,6),(2,12),(3,3),(3,6),(3,12),\\
&\quad(6,6),(6,12),(12,12)\}.
\end{align*}
\]

A holds because every positive integer divides itself, and each of \(2,3,6,12\) appears on the diagonal.

B fails because \((2,6) \in R\) while \((6,2) \notin R\): \(6\) does not divide \(2\).

C holds on this set. Suppose \(a\) divides \(b\) and \(b\) divides \(a\). For positive integers this forces \(a = b\). Directly from the list, the only time both \((a,b)\) and \((b,a)\) appear is when \(a = b\).

D holds because divisibility is transitive: if \(a\) divides \(b\) and \(b\) divides \(c\), then \(a\) divides \(c\). The composite pairs on this set are already present. For instance, \(2\) divides \(6\) and \(6\) divides \(12\), and \((2,12)\) is in \(R\); \(3\) divides \(6\) and \(6\) divides \(12\), and \((3,12)\) is in \(R\).
