# Sets — Practice Questions

Original practice for GATE CS. These questions are not from any GATE paper. Attempt the questions before reading the solutions.

## Level 1 — Conceptual

## Q1 — MCQ

Which of the following is true?

A. \(\{1\} \in \{1,2\}\)
B. \(\emptyset \in \{1,2\}\)
C. \(\{1\} \subseteq \{1,2\}\)
D. \(\{1,2\} \subseteq \{1\}\)

---

## Q2 — MSQ

Which of the following statements are true?

Select all that apply.

A. \(\emptyset \subseteq \{a,b\}\)
B. \(\emptyset \in \{\emptyset\}\)
C. \(\{\emptyset\} = \emptyset\)
D. \(\emptyset \in \emptyset\)

---

## Q3 — NAT

Let \(A = \{p, q, r, s, t, u\}\). Enter the number of subsets of \(A\).

---

## Q4 — MCQ

Let \(A\) and \(B\) be subsets of a universe \(U\). The difference \(A - B\) equals

A. \(B \cap A^{c}\)
B. \(A \cap B^{c}\)
C. \(A \cup B^{c}\)
D. \((A \cup B)^{c}\)

---

## Level 2 — Standard GATE Style

## Q5 — MCQ

If \(|A| = 28\), \(|B| = 17\), and \(|A \cap B| = 6\), then \(|A \cup B|\) equals

A. \(51\)
B. \(45\)
C. \(39\)
D. \(33\)

---

## Q6 — NAT

Let \(|A| = 5\) and \(|B| = 7\). Enter \(|A \times B|\).

---

## Q7 — MSQ

Which identities hold for all subsets \(A\), \(B\), and \(C\) of a universe \(U\)?

Select all that apply.

A. \(A \cup (B \cap C) = (A \cup B) \cap (A \cup C)\)
B. \(A - B = B - A\)
C. \(A \cap (B \cup C) = (A \cap B) \cup (A \cap C)\)
D. \((A \cap B)^{c} = A^{c} \cap B^{c}\)

---

## Q8 — MCQ

For subsets \(A\) and \(B\) of a universe \(U\), \((A \cup B)^{c}\) equals

A. \(A^{c} \cup B^{c}\)
B. \(A^{c} \cap B^{c}\)
C. \(A \cap B\)
D. \(A^{c} \cup B\)

---

## Level 3 — Multi-Step

## Q9 — NAT

A club has \(90\) members. Of these, \(38\) play chess, \(33\) play carrom, and \(27\) play bridge. Also, \(12\) play chess and carrom, \(10\) play chess and bridge, and \(9\) play carrom and bridge, where each of those three counts includes members who play all three games. Exactly \(4\) members play all three games. Enter the number of members who play none of the three games.

---

## Q10 — MCQ

If \(|A| = 16\), \(|B| = 13\), and \(|A \cap B| = 5\), then \(|A \triangle B|\) equals

A. \(24\)
B. \(19\)
C. \(14\)
D. \(29\)

---

## Q11 — MSQ

Which statements are true for all finite sets \(A\), \(B\), and \(C\)?

Select all that apply.

A. \(|A \times B| = |A| \cdot |B|\)
B. \(A \times \emptyset = \emptyset\)
C. \(A \times B = B \times A\) whenever \(A\) and \(B\) are nonempty
D. \(A \times (B \cup C) = (A \times B) \cup (A \times C)\)

---

## Level 4 — Tricky / Trap-Based

## Q12 — MCQ

The cardinality of the power set of \(\{\emptyset\}\) is

A. \(0\)
B. \(1\)
C. \(2\)
D. \(4\)

---

## Q13 — NAT

Enter the number of subsets of \(\{1,2,3,4,5,6,7,8,9\}\) that contain both \(2\) and \(5\), and do not contain \(8\).

---

## Q14 — MSQ

Which of the following statements are true?

Select all that apply.

A. \(\emptyset\) is an element of every set.
B. \(\emptyset\) is a subset of every set.
C. \(|\mathcal{P}(\emptyset)| = 1\)
D. \(\{\emptyset\}\) is the empty set.

---

## Level 5 — Challenge

## Q15 — MCQ

Which set equals \(A \cap (B \triangle C)\)?

A. \((A \cap B) \cup (A \cap C)\)
B. \((A \cap B \cap C^{c}) \cup (A \cap C \cap B^{c})\)
C. \(A \cap B \cap C\)
D. \((A \cup B) \triangle C\)

---

## Q16 — MCQ

How many integers from \(1\) to \(120\), inclusive, are divisible by at least one of \(4\), \(6\), and \(10\)?

A. \(62\)
B. \(44\)
C. \(40\)
D. \(30\)

---

## Answer Key

| Q | Type | Answer |
|---|------|--------|
| 1 | MCQ | C |
| 2 | MSQ | A, B |
| 3 | NAT | 64 |
| 4 | MCQ | B |
| 5 | MCQ | C |
| 6 | NAT | 35 |
| 7 | MSQ | A, C |
| 8 | MCQ | B |
| 9 | NAT | 19 |
| 10 | MCQ | B |
| 11 | MSQ | A, B, D |
| 12 | MCQ | C |
| 13 | NAT | 64 |
| 14 | MSQ | B, C |
| 15 | MCQ | B |
| 16 | MCQ | B |

## Detailed Solutions

### Q1

Answer: C

A set \(X\) is a subset of \(Y\) when every element of \(X\) is an element of \(Y\). The only element of \(\{1\}\) is \(1\), and \(1 \in \{1,2\}\), so \(\{1\} \subseteq \{1,2\}\).

A uses element-hood for a set. The elements of \(\{1,2\}\) are the numbers \(1\) and \(2\), not the set \(\{1\}\). So \(\{1\} \notin \{1,2\}\).

B fails for the same reason: \(\emptyset\) is not one of the numbers \(1\) or \(2\).

D fails because \(2 \in \{1,2\}\) but \(2 \notin \{1\}\).

### Q2

Answer: A, B

A is true because the empty set has no element that could lie outside \(\{a,b\}\). Vacuously, \(\emptyset \subseteq S\) for every set \(S\).

B is true because the only element of \(\{\emptyset\}\) is \(\emptyset\). This set has one element. It is not empty.

C is false. The left side has one element, namely \(\emptyset\), and the right side has no elements.

D is false. The empty set has no elements at all, so it does not contain \(\emptyset\).

### Q3

Answer: 64

If a finite set has \(n\) elements, each element can be kept out of a subset or put into it. Those choices are independent, so the power set has \(2^{n}\) elements. Here \(n = 6\), and
\[
2^{6} = 64.
\]
The count \(|A| = 6\) is the number of elements, not the number of subsets. The count \(6! = 720\) counts orderings of \(A\), not subsets.

### Q4

Answer: B

By definition, \(x \in A - B\) exactly when \(x \in A\) and \(x \notin B\). Relative to the universe \(U\), \(x \notin B\) means \(x \in B^{c}\). Therefore
\[
A - B = A \cap B^{c}.
\]

A is \(B - A\), which swaps the two sets. Difference is not commutative: if \(A = \{1\}\) and \(B = \{1,2\}\) inside \(U = \{1,2\}\), then \(A - B = \emptyset\) while \(B - A = \{2\}\).

C adds the complement of \(B\) to all of \(A\), so it contains every element outside \(B\), including elements that were never in \(A\).

D is the complement of the union, which excludes every element of \(A\). An element of \(A - B\) lies in \(A\), so it does not lie in \((A \cup B)^{c}\).

### Q5

Answer: C

The two-set inclusion–exclusion formula is
\[
|A \cup B| = |A| + |B| - |A \cap B|.
\]
Substitute the given sizes:
\[
|A \cup B| = 28 + 17 - 6 = 39.
\]
The intersection is counted in both \(|A|\) and \(|B|\), so it must be subtracted once.

A is \(28 + 17 + 6 = 51\), which adds the overlap instead of removing it. B is \(28 + 17 = 45\), the sum with no correction for the six shared elements. D is \(28 + 17 - 12 = 33\), which subtracts the overlap twice.

### Q6

Answer: 35

The Cartesian product \(A \times B\) consists of the ordered pairs \((a,b)\) with \(a \in A\) and \(b \in B\). Each of the \(5\) choices for the first coordinate combines with each of the \(7\) choices for the second, so
\[
|A \times B| = 5 \cdot 7 = 35.
\]
Adding the sizes, \(5 + 7 = 12\), counts a union of disjoint sets of those sizes, not a product. The product of the power-set sizes, \(2^{5} \cdot 2^{7}\), counts pairs of subsets rather than pairs of elements.

### Q7

Answer: A, C

A is the distributive law of union over intersection. An element is in the left side when it is in \(A\), or in both \(B\) and \(C\). That is the same as being in \(A \cup B\) and in \(A \cup C\).

C is the distributive law of intersection over union. An element is in \(A\) and in at least one of \(B\) or \(C\) exactly when it is in \(A \cap B\) or in \(A \cap C\).

B is false in general. Take \(A = \{1\}\) and \(B = \{2\}\). Then \(A - B = \{1\}\) and \(B - A = \{2\}\).

D has the wrong dual connective. De Morgan’s law says \((A \cap B)^{c} = A^{c} \cup B^{c}\). The intersection of the complements is \((A \cup B)^{c}\), not \((A \cap B)^{c}\).

### Q8

Answer: B

De Morgan’s law for sets is
\[
(A \cup B)^{c} = A^{c} \cap B^{c}.
\]
An element lies outside the union exactly when it lies outside \(A\) and outside \(B\).

A is the complement of the intersection, \((A \cap B)^{c}\), not of the union. An element in \(A - B\) lies in \(A^{c} \cup B^{c}\) because it lies in \(B^{c}\), but it does not lie in \((A \cup B)^{c}\).

C is the overlap. Elements of the overlap lie in the union, so they lie outside the complement of the union.

D still contains every element of \(B\) that is outside \(A\). Those elements are in the union, so they are not in the complement.

### Q9

Answer: 19

The phrase “play chess and carrom” gives the full intersection \(|\mathrm{Chess} \cap \mathrm{Carrom}|\), including the \(4\) members who also play bridge. Use three-set inclusion–exclusion:
\begin{align*}
|\mathrm{Chess} \cup \mathrm{Carrom} \cup \mathrm{Bridge}|
&= 38 + 33 + 27 - 12 - 10 - 9 + 4 \\
&= 98 - 31 + 4 \\
&= 71.
\end{align*}
The \(4\) members in all three games were added three times and then removed three times, once in each pairwise term, so they must be added back once. Members in none of the games are the rest of the club:
\[
90 - 71 = 19.
\]
Omitting the final \(+4\) produces \(98 - 31 = 67\) and then \(90 - 67 = 23\), which undercounts the triple overlap. Adding the three individual sizes and subtracting from \(90\) is impossible in the direct way \(90 - 98\), because \(98\) double-counts overlaps. Using only chess and carrom, \(38 + 33 - 12 = 59\), ignores bridge.

### Q10

Answer: B

The symmetric difference \(A \triangle B\) contains the elements that lie in exactly one of the two sets. Its size is
\[
|A \triangle B| = |A| + |B| - 2|A \cap B|.
\]
The intersection is excluded from both sides, so it is removed twice:
\[
16 + 13 - 2 \cdot 5 = 29 - 10 = 19.
\]
Equivalently, \(|A - B| + |B - A| = (16 - 5) + (13 - 5) = 11 + 8 = 19\).

A is the union size \(16 + 13 - 5 = 24\). The union still contains the five shared elements, which symmetric difference excludes. C is \(16 + 13 - 15 = 14\), which subtracts the overlap three times. D is the raw sum \(16 + 13 = 29\), with no overlap removed.

### Q11

Answer: A, B, D

A is the multiplication rule for a product of finite sets: each element of \(A\) pairs with each element of \(B\).

B is true because a pair \((a,b)\) would need a second coordinate \(b \in \emptyset\), and no such \(b\) exists. The product is empty.

D expands by cases on the second coordinate. If \(b \in B \cup C\), then \(b \in B\) or \(b \in C\), so \((a,b)\) lies in \(A \times B\) or in \(A \times C\), and the converse is the same argument read backwards.

C is false. Take \(A = \{1\}\) and \(B = \{2\}\). Then \(A \times B = \{(1,2)\}\) and \(B \times A = \{(2,1)\}\). These ordered pairs are different, so the products are unequal even though both sets are nonempty.

### Q12

Answer: C

The set \(\{\emptyset\}\) has one element, and that element is the empty set. A one-element set has \(2^{1} = 2\) subsets:
\[
\mathcal{P}(\{\emptyset\}) = \{\emptyset,\ \{\emptyset\}\}.
\]
The two members are the empty set and the original set itself.

A would say the power set is empty. Every power set contains at least \(\emptyset\). B counts only one of the two subsets, usually by treating \(\{\emptyset\}\) as if it were \(\emptyset\). D is \(2^{2}\), the power-set size of a two-element set. The set \(\{\emptyset\}\) does not have two elements; \(\emptyset\) and \(\{\emptyset\}\) are not both elements of \(\{\emptyset\}\).

### Q13

Answer: 64

The universe of the count is the nine-element set \(\{1,2,3,4,5,6,7,8,9\}\). A subset of the required kind must contain \(2\), must contain \(5\), and must exclude \(8\). That fixes three elements. The other six elements, namely \(1,3,4,6,7,9\), may each be included or excluded freely. The number of subsets is
\[
2^{6} = 64.
\]
Using \(2^{9-2} = 2^{7} = 128\) forces \(2\) and \(5\) in but still allows \(8\) to vary. Using \(2^{9} = 512\) ignores all three constraints. Using \(9 - 3 = 6\) as the answer counts free elements rather than subsets of those elements.

### Q14

Answer: B, C

B is the subset law for the empty set: there is no element of \(\emptyset\) that fails to belong to a given set.

C follows from the power-set formula. The empty set has \(0\) elements, and \(2^{0} = 1\). Explicitly, \(\mathcal{P}(\emptyset) = \{\emptyset\}\), a one-element set whose only element is \(\emptyset\).

A confuses subset with element. The claim \(\emptyset \in S\) is false for \(S = \{1\}\), since the only element of \(S\) is \(1\).

D is the same confusion as treating a singleton of the empty set as empty. \(\{\emptyset\}\) contains one element, so it is not equal to \(\emptyset\).

### Q15

Answer: B

By definition, \(B \triangle C = (B - C) \cup (C - B) = (B \cap C^{c}) \cup (C \cap B^{c})\). Intersect both sides with \(A\) and distribute:
\begin{align*}
A \cap (B \triangle C)
&= A \cap ((B \cap C^{c}) \cup (C \cap B^{c})) \\
&= (A \cap B \cap C^{c}) \cup (A \cap C \cap B^{c}).
\end{align*}
That is option B: the elements that lie in \(A\) and in exactly one of \(B\) or \(C\).

The other options fail on \(A = \{1,2,3\}\), \(B = \{1,3\}\), and \(C = \{2,3\}\), with universe large enough to contain these sets. Then \(B \triangle C = \{1,2\}\) and \(A \cap (B \triangle C) = \{1,2\}\).

A equals \((A \cap B) \cup (A \cap C) = \{1,3\} \cup \{2,3\} = \{1,2,3\}\), which still contains \(3\). The element \(3\) lies in both \(B\) and \(C\), so it is outside the symmetric difference.

C equals \(A \cap B \cap C = \{3\}\), the triple overlap, which is exactly the part symmetric difference removes.

D equals \((A \cup B) \triangle C\). Here \(A \cup B = \{1,2,3\}\) and \(\{1,2,3\} \triangle \{2,3\} = \{1\}\), which drops the element \(2\).

### Q16

Answer: B

Let \(A_{4}\), \(A_{6}\), and \(A_{10}\) be the sets of integers from \(1\) to \(120\) divisible by \(4\), \(6\), and \(10\). Their sizes are the corresponding floors:
\begin{align*}
|A_{4}| &= \lfloor 120/4 \rfloor = 30, \\
|A_{6}| &= \lfloor 120/6 \rfloor = 20, \\
|A_{10}| &= \lfloor 120/10 \rfloor = 12.
\end{align*}
Pairwise least common multiples are \(\operatorname{lcm}(4,6) = 12\), \(\operatorname{lcm}(4,10) = 20\), and \(\operatorname{lcm}(6,10) = 30\). The triple least common multiple is \(\operatorname{lcm}(4,6,10) = 2^{2} \cdot 3 \cdot 5 = 60\). Hence
\begin{align*}
|A_{4} \cap A_{6}| &= \lfloor 120/12 \rfloor = 10, \\
|A_{4} \cap A_{10}| &= \lfloor 120/20 \rfloor = 6, \\
|A_{6} \cap A_{10}| &= \lfloor 120/30 \rfloor = 4, \\
|A_{4} \cap A_{6} \cap A_{10}| &= \lfloor 120/60 \rfloor = 2.
\end{align*}
Inclusion–exclusion gives
\begin{align*}
|A_{4} \cup A_{6} \cup A_{10}|
&= 30 + 20 + 12 - 10 - 6 - 4 + 2 \\
&= 62 - 20 + 2 \\
&= 44.
\end{align*}

A is \(30 + 20 + 12 = 62\), the sum before any overlap is removed. C is \(30 + 20 - 10 = 40\), the two-set count for \(4\) and \(6\) only. D is \(|A_{4}| = 30\), which ignores multiples of \(6\) or \(10\) that are not multiples of \(4\), such as \(6\) and \(10\).
