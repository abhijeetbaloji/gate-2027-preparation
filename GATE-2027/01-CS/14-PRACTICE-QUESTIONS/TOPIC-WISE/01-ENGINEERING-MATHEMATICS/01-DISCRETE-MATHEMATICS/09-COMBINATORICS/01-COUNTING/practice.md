# Combinatorics: Counting — Practice Questions

Original practice for GATE CS. These questions are not from any GATE paper. Attempt the questions before reading the solutions.

## Level 1 — Conceptual

## Q1 — MCQ

A library code is formed by choosing one letter from {P, Q, R, S, T} and then one digit from {0, 1, 2, 3}. How many such codes are there?

A. 9
B. 20
C. 120
D. 5!

---

## Q2 — MCQ

In how many ways can a chairperson and a treasurer be chosen from 8 distinct club members if the two offices must be held by different people?

A. 28
B. 56
C. 64
D. 16

---

## Q3 — NAT

The number of ways to choose 3 projects from 11 distinct projects is ____.

---

## Q4 — MCQ

What is the smallest number of integers that must be chosen to guarantee that at least 3 of them leave the same remainder when divided by 7?

A. 14
B. 15
C. 21
D. 16

---

## Q5 — MCQ

The number of distinct strings obtained by rearranging the letters of BALLOON is

A. 1260
B. 5040
C. 2520
D. 630

---

## Level 2 — Standard GATE Style

## Q6 — NAT

The number of non-negative integer solutions of \(w + x + y + z = 6\) is ____.

---

## Q7 — MCQ

The number of ways to seat 7 distinct people around a round table, where two seatings that differ only by a rotation are regarded as the same and reflections are regarded as different, is

A. 5040
B. 720
C. 360
D. 7

---

## Q8 — NAT

In a group of 80 students, 46 play chess, 39 play carrom, and 18 play both. The number of students who play neither game is ____.

---

## Q9 — MCQ

The coefficient of \(y^3\) in the expansion of \((1 + 2y)^6\) is

A. 160
B. 80
C. 20
D. 64

---

## Q10 — MSQ

Select all that apply.

A. \(C(12, 3) = C(12, 9)\)
B. \(P(7, 3) = 210\)
C. The number of ways to place 6 identical balls into 2 distinct boxes, allowing empty boxes, is \(C(6, 2) = 15\)
D. The number of ways to seat 5 distinct people around a round table, where rotations are the same seating and reflections are different, is \(4! = 24\)

---

## Q11 — NAT

The number of derangements of 5 distinct objects (permutations in which no object stays in its original position) is ____.

---

## Level 3 — Multi-Step

## Q12 — NAT

The number of positive integer solutions of \(p + q + r + s = 13\) is ____.

---

## Q13 — MCQ

Finite sets \(A\), \(B\), and \(C\) satisfy

\(|A| = 26\), \(|B| = 21\), \(|C| = 17\),

\(|A \cap B| = 8\), \(|A \cap C| = 6\), \(|B \cap C| = 5\), \(|A \cap B \cap C| = 2\).

Then \(|A \cup B \cup C|\) equals

A. 47
B. 45
C. 64
D. 43

---

## Q14 — NAT

The number of surjective functions from a set of 4 elements to a set of 3 elements is ____.

---

## Q15 — MCQ

How many 4-letter strings can be formed from the alphabet {A, B, C, D, E, F, G} if all four letters in a string must be distinct?

A. 840
B. 35
C. 2401
D. 210

---

## Q16 — MSQ

Let \(S\) be a set with 8 elements. Select all that apply.

A. \(S\) has 256 subsets
B. The number of subsets of \(S\) of size 3 is \(C(8, 3) = 56\)
C. The number of ways to divide 8 distinct people into two unlabeled groups of 4 is \(C(8, 4)/2 = 35\)
D. The number of ways to arrange 8 distinct people in a circle, with rotations regarded as the same arrangement, is \(8!\)

---

## Level 4 — Tricky / Trap-Based

## Q17 — MCQ

The number of distinct strings obtained by rearranging the letters of ASSESS is

A. 30
B. 720
C. 360
D. 15

---

## Q18 — MCQ

The number of positive integer solutions of \(x + y + z = 11\) is

A. 45
B. 78
C. 55
D. 36

---

## Q19 — MSQ

A code uses 3 symbols, each chosen from an alphabet of 8 distinct symbols. Select all that apply.

A. If repetition is allowed and order matters, there are \(8^3 = 512\) codes
B. If repetition is not allowed and order matters, there are \(P(8, 3) = 336\) codes
C. If repetition is not allowed and order does not matter, there are \(C(8, 3) = 56\) codes
D. If repetition is allowed and order does not matter, there are \(C(8, 3) = 56\) codes

---

## Level 5 — Challenge

## Q20 — NAT

The number of ways to seat 4 distinct men and 3 distinct women around a round table so that no two women sit next to each other is ____. Rotations of the same seating are identical, and reflections are different.

---

## Q21 — MCQ

How many integers in \(\{1, 2, \ldots, 84\}\) are divisible by 3, by 4, or by 7?

A. 48
B. 47
C. 61
D. 50

---

## Q22 — NAT

The number of non-negative integer solutions of \(x + y + z = 12\) in which \(x \le 7\), \(y \le 7\), and \(z \le 7\) is ____.

## Answer Key

| Q | Type | Answer |
|---|------|--------|
| 1 | MCQ | B |
| 2 | MCQ | B |
| 3 | NAT | 165 |
| 4 | MCQ | B |
| 5 | MCQ | A |
| 6 | NAT | 84 |
| 7 | MCQ | B |
| 8 | NAT | 13 |
| 9 | MCQ | A |
| 10 | MSQ | A, B, D |
| 11 | NAT | 44 |
| 12 | NAT | 220 |
| 13 | MCQ | A |
| 14 | NAT | 36 |
| 15 | MCQ | A |
| 16 | MSQ | A, B, C |
| 17 | MCQ | A |
| 18 | MCQ | A |
| 19 | MSQ | A, B, C |
| 20 | NAT | 144 |
| 21 | MCQ | A |
| 22 | NAT | 46 |

## Detailed Solutions

### Q1

Answer: B

The letter and the digit are chosen independently, so the product rule applies. There are 5 letters and 4 digits:

\(5 \times 4 = 20\).

Adding 5 and 4 gives 9, which would be correct only if the code were a letter or a digit, not both.

### Q2

Answer: B

The two offices are different, so order matters. The chairperson can be any of 8 members, and the treasurer any of the remaining 7:

\(P(8, 2) = 8 \times 7 = 56\).

The combination \(C(8, 2) = 28\) counts unordered pairs and does not assign the two offices.

### Q3

Answer: 165

A committee is an unordered selection:

\(C(11, 3) = \dfrac{11 \times 10 \times 9}{3 \times 2 \times 1} = \dfrac{990}{6} = 165\).

### Q4

Answer: B

The remainders modulo 7 are 0, 1, 2, 3, 4, 5, and 6, so there are 7 pigeonholes. If at most 2 chosen integers fall into each remainder class, then at most \(7 \times 2 = 14\) integers have been chosen, and it is still possible that no remainder occurs 3 times. One more integer forces some remainder to occur at least 3 times:

\(7 \times 2 + 1 = 15\).

### Q5

Answer: A

BALLOON has 7 letters: B, A, N once each, and L and O twice each. Identical letters do not create new strings when swapped:

\(\dfrac{7!}{2! \, 2!} = \dfrac{5040}{4} = 1260\).

Using \(7! = 5040\) treats every letter as distinct. Dividing by only one \(2!\) leaves 2520. Dividing by an extra \(2!\) leaves 630.

### Q6

Answer: 84

The variables are non-negative and the objects counted by the equation are identical units distributed to 4 distinct variables. Stars and bars gives

\(C(6 + 4 - 1,\, 6) = C(9, 6) = C(9, 3) = \dfrac{9 \times 8 \times 7}{6} = 84\).

### Q7

Answer: B

For \(n\) distinct people around a table, rotations are the same arrangement, so the count is \((n - 1)!\):

\((7 - 1)! = 6! = 720\).

The linear count \(7! = 5040\) treats rotated seatings as different. Dividing by 2 as well, which gives 360, is appropriate only when reflections are also identified.

### Q8

Answer: 13

Inclusion–exclusion for two sets:

\(|\text{chess} \cup \text{carrom}| = 46 + 39 - 18 = 67\).

Students who play neither game:

\(80 - 67 = 13\).

### Q9

Answer: A

The binomial theorem gives

\((1 + 2y)^6 = \sum_{k=0}^{6} C(6, k) \, 1^{6-k} (2y)^k\).

The coefficient of \(y^3\) is

\(C(6, 3) \times 2^3 = 20 \times 8 = 160\).

Using \(2^2\) instead of \(2^3\) produces 80. Using the bare binomial coefficient produces 20. The term \(2^6 = 64\) is the coefficient of \(y^6\) only after the binomial coefficient \(C(6, 6) = 1\) is included, and it is not the coefficient of \(y^3\).

### Q10

Answer: A, B, D

A is the symmetry identity \(C(n, r) = C(n, n - r)\):

\(C(12, 3) = \dfrac{12 \times 11 \times 10}{6} = 220 = C(12, 9)\).

B is the definition of a permutation:

\(P(7, 3) = 7 \times 6 \times 5 = 210\).

C uses the combination formula for distinct objects. Six identical balls in 2 distinct boxes, empty boxes allowed, is a non-negative solution count:

\(C(6 + 2 - 1,\, 6) = C(7, 6) = 7\),

so C is false.

D is the circular-permutation formula \((5 - 1)! = 24\).

### Q11

Answer: 44

The derangement count is

\(!5 = 5! \sum_{i=0}^{5} \dfrac{(-1)^i}{i!} = \sum_{i=0}^{5} (-1)^i \dfrac{5!}{i!}\).

Term by term:

\(120 - 120 + \dfrac{120}{2} - \dfrac{120}{6} + \dfrac{120}{24} - \dfrac{120}{120}\)

\(= 120 - 120 + 60 - 20 + 5 - 1 = 44\).

### Q12

Answer: 220

Each variable is at least 1. Substitute \(p' = p - 1\), and likewise for \(q, r, s\). Then \(p', q', r', s' \ge 0\) and

\(p' + q' + r' + s' = 13 - 4 = 9\).

The number of non-negative solutions is

\(C(9 + 4 - 1,\, 9) = C(12, 9) = C(12, 3) = \dfrac{12 \times 11 \times 10}{6} = 220\).

The same count is \(C(13 - 1,\, 4 - 1) = C(12, 3)\).

### Q13

Answer: A

For three sets, add the single sizes, subtract the three pairwise intersections, and add the triple intersection back:

\(|A \cup B \cup C| = 26 + 21 + 17 - 8 - 6 - 5 + 2\).

\(26 + 21 + 17 = 64\), and \(8 + 6 + 5 = 19\), so

\(64 - 19 + 2 = 47\).

Leaving the triple intersection out produces 45. Subtracting it instead of adding it produces 43. Stopping after the three single sizes produces 64.

### Q14

Answer: 36

By inclusion–exclusion, the number of surjections from a set of 4 elements onto a set of 3 elements is

\(\sum_{i=0}^{3} (-1)^i C(3, i) (3 - i)^4\)

\(= C(3, 0)\, 3^4 - C(3, 1)\, 2^4 + C(3, 2)\, 1^4 - C(3, 3)\, 0^4\)

\(= 81 - 3 \times 16 + 3 \times 1 - 0 = 81 - 48 + 3 = 36\).

Equivalently, the Stirling number of the second kind \(S(4, 3) = C(4, 2) = 6\) counts partitions of 4 elements into one doubleton and two singletons, and assigning those blocks to 3 distinct images multiplies by \(3!\):

\(3! \times 6 = 36\).

### Q15

Answer: A

Order matters and repetition is forbidden, so the count is a permutation:

\(P(7, 4) = 7 \times 6 \times 5 \times 4 = 840\).

\(C(7, 4) = 35\) ignores order. Allowing repetition gives \(7^4 = 2401\). Stopping after three factors gives \(7 \times 6 \times 5 = 210\).

### Q16

Answer: A, B, C

A: every element is either in a subset or not, so there are \(2^8 = 256\) subsets.

B: \(C(8, 3) = \dfrac{8 \times 7 \times 6}{6} = 56\).

C: first choose 4 people out of 8 for one group, which can be done in \(C(8, 4) = 70\) ways. The two groups are unlabeled and have equal size, so \(\{G, S \setminus G\}\) has been counted twice:

\(\dfrac{C(8, 4)}{2} = \dfrac{70}{2} = 35\).

D counts linear arrangements. Circular arrangements of 8 distinct people, up to rotation, number \((8 - 1)! = 7! = 5040\).

### Q17

Answer: A

ASSESS has 6 letters, of which S is repeated 4 times and A and E appear once:

\(\dfrac{6!}{4!} = \dfrac{720}{24} = 30\).

Treating the letters as distinct gives 720. Dividing only by \(2!\), as if S appeared twice, gives 360. An extra division by \(2!\) gives 15.

### Q18

Answer: A

Positive solutions require the change of variables \(x' = x - 1\), \(y' = y - 1\), \(z' = z - 1\). Then

\(x' + y' + z' = 11 - 3 = 8\), \(x', y', z' \ge 0\),

so the number is

\(C(8 + 3 - 1,\, 8) = C(10, 8) = C(10, 2) = \dfrac{10 \times 9}{2} = 45\).

The non-negative count for the original equation is \(C(11 + 3 - 1,\, 11) = C(13, 2) = 78\), which allows zeros. The neighbouring binomial values \(C(11, 2) = 55\) and \(C(9, 2) = 36\) come from shifting the sum by the wrong amount.

### Q19

Answer: A, B, C

A: each of 3 positions has 8 choices, so \(8^3 = 512\).

B: \(P(8, 3) = 8 \times 7 \times 6 = 336\).

C: an unordered selection of 3 distinct symbols is \(C(8, 3) = \dfrac{8 \times 7 \times 6}{6} = 56\).

D allows repetition while ignoring order, which is a multiset count:

\(C(8 + 3 - 1,\, 3) = C(10, 3) = \dfrac{10 \times 9 \times 8}{6} = 120\),

so \(C(8, 3)\) is the wrong formula there.

### Q20

Answer: 144

Seat the 4 men first. Around a table, rotations are identified, so they can be seated in

\((4 - 1)! = 3! = 6\)

ways. Four seated men create 4 gaps. To keep the women apart, place at most one woman in each gap, and arrange 3 distinct women in 3 of those 4 gaps:

\(P(4, 3) = 4 \times 3 \times 2 = 24\).

The product rule gives

\(6 \times 24 = 144\).

### Q21

Answer: A

Let \(A_3\), \(A_4\), and \(A_7\) be the integers in \(\{1, \ldots, 84\}\) divisible by 3, 4, and 7. Then

\(|A_3| = \lfloor 84/3 \rfloor = 28\), \(|A_4| = 21\), \(|A_7| = 12\),

\(|A_3 \cap A_4| = \lfloor 84/12 \rfloor = 7\), \(|A_3 \cap A_7| = \lfloor 84/21 \rfloor = 4\), \(|A_4 \cap A_7| = \lfloor 84/28 \rfloor = 3\),

\(|A_3 \cap A_4 \cap A_7| = \lfloor 84/84 \rfloor = 1\).

Inclusion–exclusion:

\(28 + 21 + 12 - 7 - 4 - 3 + 1 = 61 - 14 + 1 = 48\).

Omitting the triple intersection leaves 47. Using only the three single counts leaves 61.

### Q22

Answer: 46

Ignore the upper bounds first. The number of non-negative solutions of \(x + y + z = 12\) is

\(C(12 + 3 - 1,\, 12) = C(14, 2) = \dfrac{14 \times 13}{2} = 91\).

Subtract the solutions in which some variable is at least 8. If \(x \ge 8\), set \(x'' = x - 8\). Then \(x'' + y + z = 4\) with all variables non-negative:

\(C(4 + 3 - 1,\, 4) = C(6, 4) = 15\).

The same count applies to \(y \ge 8\) and to \(z \ge 8\), so 45 solutions are removed. Two variables cannot both be at least 8, because that would force the sum to be at least 16. Therefore

\(91 - 45 = 46\).
