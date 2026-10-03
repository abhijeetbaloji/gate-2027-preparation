# Divide and Conquer — Practice Questions

Original practice for GATE CS. These questions are not from any GATE paper. Attempt the questions before reading the solutions.

## Level 1 — Conceptual

## Q1 — MCQ

Standard top-down merge sort splits the array in half, sorts both halves, and merges them in linear time. Its recurrence and solution are

A. \(T(n) = 2T(n/2) + \Theta(n) = \Theta(n)\)

B. \(T(n) = 2T(n/2) + \Theta(n) = \Theta(n \log n)\)

C. \(T(n) = T(n-1) + \Theta(n) = \Theta(n^2)\)

D. \(T(n) = 2T(n/2) + \Theta(1) = \Theta(n \log n)\)

---

## Q2 — MSQ

Select all that apply.

A. In merge sort the combine step is the linear merge, and the split is into two disjoint halves.

B. In quicksort the linear work is the partition, and the combine step does no further merging.

C. Binary search solves both halves and therefore has recurrence \(T(n) = 2T(n/2) + \Theta(1)\).

D. Memoising merge sort does not improve its \(\Theta(n \log n)\) bound, because the halves do not overlap.

---

## Q3 — MCQ

Binary search on a sorted array solves one half and does \(\Theta(1)\) work besides the recursive call. Under the Master theorem, \(a = 1\), \(b = 2\), and \(f(n) = \Theta(1)\). The solution is

A. \(\Theta(n)\)

B. \(\Theta(\log n)\)

C. \(\Theta(n \log n)\)

D. \(\Theta(1)\)

---

## Level 2 — Standard GATE Style

## Q4 — MCQ

Quicksort’s pivot is always the smallest or the largest key in the current subarray. The recurrence is \(T(n) = T(n-1) + \Theta(n)\). Its solution is

A. \(\Theta(n \log n)\), by Master case 2 with \(b = 1\)

B. \(\Theta(n^2)\), by unrolling the arithmetic series

C. \(\Theta(n)\)

D. \(\Theta(n^{\log_2 3})\)

---

## Q5 — NAT

During merge sort, an inversion \(i < j\) with \(A[i] > A[j]\) is counted when the two values lie in different halves and the right-half value is emitted while \(r\) left-half values remain. How many inversions does \([4, 1, 3, 2]\) contain?

---

## Q6 — MSQ

Select all that apply. The contiguous maximum-subarray problem is solved in two ways on \([2, -4, 3, -1, 2, -1, 5, -6]\). The empty segment is not allowed.

A. The divide-and-conquer version, taking the better of the left half, the right half, and the best crossing sum, satisfies \(T(n) = 2T(n/2) + \Theta(n) = \Theta(n \log n)\).

B. Kadane’s scan, which extends the best sum ending at the previous index only when that sum is positive, runs in \(\Theta(n)\) time and \(\Theta(1)\) extra memory.

C. On this array the maximum sum is 8.

D. It is enough to compute the crossing sum at one fixed midpoint and skip both recursive calls.

---

## Q7 — MCQ

Karatsuba multiplies two \(n\)-bit integers by writing each as a high half and a low half. The recurrence used by the algorithm is

A. \(T(n) = 4T(n/2) + \Theta(n) = \Theta(n^2)\)

B. \(T(n) = 3T(n/2) + \Theta(n) = \Theta(n^{\log_2 3})\)

C. \(T(n) = 2T(n/2) + \Theta(n) = \Theta(n \log n)\)

D. \(T(n) = 7T(n/2) + \Theta(n^2)\)

---

## Level 3 — Multi-Step

## Q8 — MSQ

Select all that apply. Closest pair is computed for \(n\) points in the plane. The divide step splits on the median \(x\)-coordinate. Let \(\delta\) be the smaller of the two recursive distances.

A. A cross pair closer than \(\delta\) must lie in the vertical strip of width \(2\delta\) about the dividing line.

B. If \(y\)-order is maintained and passed down, each strip point is compared with \(O(1)\) later points in \(y\)-order, the combine is \(\Theta(n)\), and \(T(n) = \Theta(n \log n)\).

C. Sorting by \(y\) from scratch inside every call keeps the combine linear and the solution \(\Theta(n \log n)\).

D. Comparing every pair inside the strip is still linear, because the strip is a subset of the point set.

---

## Q9 — MCQ

Strassen multiplies two \(n \times n\) matrices with \(T(n) = 7T(n/2) + \Theta(n^2)\). Which statement is correct?

A. \(\log_2 7 \approx 2.807\), \(n^2 = O(n^{\log_2 7 - \varepsilon})\) for a positive \(\varepsilon\), case 1 applies, and \(T(n) = \Theta(n^{\log_2 7})\).

B. Case 2 applies, because \(n^2\) matches \(n^{\log_2 7}\), so the solution is \(\Theta(n^2 \log n)\).

C. This recurrence parenthesises a chain of \(n\) rectangular matrices.

D. The classical triple loop is already \(o(n^{\log_2 7})\).

---

## Q10 — MSQ

Select all that apply. The rank-\(k\) key is selected without sorting the whole array.

A. Randomised quickselect recurses into one side and has expected time \(\Theta(n)\).

B. The worst case of that randomised procedure, over unlucky pivots, is \(\Theta(n^2)\).

C. Median of medians, groups of 5, satisfies \(T(n) \le T(n/5) + T(7n/10) + O(n) = \Theta(n)\) in the worst case, because \(1/5 + 7/10 < 1\).

D. The Master theorem applies directly to quickselect’s random subproblem sizes.

---

## Level 4 — Tricky / Trap-Based

## Q11 — MCQ

Sorted input is given to quicksort, and the pivot is always the last element of the current subarray. Which description is correct?

A. This is the best case, \(T(n) = 2T(n/2) + \Theta(n)\).

B. The last element is the maximum, one side is empty, and \(T(n) = T(n-1) + \Theta(n) = \Theta(n^2)\).

C. Sorted input forces every pivot rank to the middle.

D. The Master theorem’s case 2 applies with \(b = 1\).

---

## Q12 — MSQ

Select all that apply. \(T(n) = T(n/3) + T(2n/3) + \Theta(n)\).

A. There is no single \(a\) and \(b\) to substitute into the Master theorem.

B. The longer branch has depth \(\Theta(\log n)\), every level of the tree sums to \(\Theta(n)\), and \(T(n) = \Theta(n \log n)\).

C. Because \(1/3 + 2/3 = 1\), the solution is \(\Theta(n)\), as for \(T(n) = T(n/2) + \Theta(n)\).

D. The same class, \(\Theta(n \log n)\), is what case 2 gives for \(T(n) = 2T(n/2) + \Theta(n)\).

---

## Level 5 — Challenge

## Q13 — MCQ

Counting inversions by merge sort adds, in \(\Theta(1)\) time, the number \(r\) of still-unmerged left-half keys whenever a right-half key is emitted. Which statement is correct?

A. Each inversion is counted once, in the unique merge that first places its two keys in different halves, and the recurrence stays \(T(n) = 2T(n/2) + \Theta(n) = \Theta(n \log n)\).

B. The extra counter forces an additional \(\Theta(n^2)\) pair loop inside each merge.

C. Inversions between two keys in the same half are counted again at the parent merge.

D. The algorithm is correct only if the merge prefers the right half on a tie, so equal keys become inversions.

---

## Q14 — MSQ

Select all that apply.

A. Solving both halves of a search, with recurrence \(T(n) = 2T(n/2) + \Theta(1)\), is \(\Theta(n)\) by Master case 1, and it does not improve on a scan.

B. Binary search is allowed to use \(T(n) = T(n/2) + \Theta(1)\) only because sorted order proves that the discarded half contains no answer.

C. A fresh \(y\)-sort in every closest-pair call changes the combine to \(\Theta(n \log n)\) and the solution to \(\Theta(n \log^2 n)\).

D. Using Strassen’s exponent as the cost of matrix-chain parenthesisation confuses multiplication of two matrices with the cubic ordering DP.

## Answer Key

| Q | Type | Answer |
|---|------|--------|
| 1 | MCQ | B |
| 2 | MSQ | A, B, D |
| 3 | MCQ | B |
| 4 | MCQ | B |
| 5 | NAT | 4 |
| 6 | MSQ | A, B, C |
| 7 | MCQ | B |
| 8 | MSQ | A, B |
| 9 | MCQ | A |
| 10 | MSQ | A, B, C |
| 11 | MCQ | B |
| 12 | MSQ | A, B, D |
| 13 | MCQ | A |
| 14 | MSQ | A, B, C, D |

## Detailed Solutions

### Q1

Answer: B

The two subproblems are half the size, and the merge walks every key, so \(T(n) = 2T(n/2) + \Theta(n)\). Master’s theorem: \(a = 2\), \(b = 2\), \(\log_b a = 1\), and \(f(n) = \Theta(n^{\log_b a})\). Case 2 multiplies by an extra \(\log n\), because every level of the recursion tree costs \(\Theta(n)\) and there are \(\Theta(\log n)\) levels. Writing \(\Theta(n)\) keeps the cost of one level and drops the depth. The recurrence with \(\Theta(1)\) combine is a different algorithm: the leaves dominate and the solution is \(\Theta(n)\).

### Q2

Answer: A, B, D

Merge sort pays in the combine step. Quicksort pays in the divide step and then the pivot is already in its final place, so there is nothing to merge. Binary search throws one half away. Its recurrence has one recursive call, not two; option (C) is the cost of inspecting both halves and only gains a linear scan. The halves of an array in merge sort are disjoint intervals. A memo table would store each of them once and never be consulted again, so the bound stays \(\Theta(n \log n)\).

### Q3

Answer: B

\(\log_2 1 = 0\), and \(f(n) = \Theta(1) = \Theta(n^0)\). Case 2 gives \(T(n) = \Theta(n^0 \log n) = \Theta(\log n)\). Unrolling is a chain of \(\Theta(\log n)\) constant-time probes. The discard is safe only while the searched side is the only side that can hold the key.

### Q4

Answer: B

The Master theorem needs \(b > 1\). A subproblem of size \(n-1\) is not a constant-fraction split, so case 2 cannot be invoked with \(b = 1\). Unrolling produces

\[
T(n) = \Theta(n) + \Theta(n-1) + \cdots + \Theta(1) = \Theta(n^2).
\]

That is one partition per size, each linear in its size. The exponent \(\log_2 3\) is Karatsuba’s, from three half-size multiplications, not from a degenerate pivot.

### Q5

Answer: 4

The inverted pairs are \((4,1)\), \((4,3)\), \((4,2)\), and \((3,2)\). The pair \((1,3)\) and the pair \((1,2)\) are in order. The total is 4. In the merge of the sorted halves \([1, 4]\) and \([2, 3]\), emitting 2 while 4 remains on the left charges one inversion, and emitting 3 while 4 remains charges the other. The two inversions inside \([4, 1]\) were charged when that half was merged. Each pair is charged in exactly one merge, so the count is not doubled, and the extra arithmetic does not change the \(\Theta(n)\) combine.

### Q6

Answer: A, B, C

The maximum subarray is entirely left of the midpoint, entirely right of it, or it uses a suffix of the left half plus a prefix of the right half. The two scans that find that crossing piece are \(\Theta(n)\), and both recursive calls are required, so the recurrence is the merge-sort recurrence, \(\Theta(n \log n)\). Skipping a side can miss the optimum: the best segment might lie entirely in the skipped half. Kadane keeps the best sum that ends at the current index. If the previous ending sum is negative it is thrown away, because every extension of a negative prefix is worse than starting at the current key. One pass and a handful of scalars give \(\Theta(n)\) time and \(\Theta(1)\) extra memory.

On this array the ending-here sums are \(2\), then \(\max(-4, 2-4) = -2\), then \(3\), then \(2\), then \(4\), then \(3\), then \(8\), then \(2\). The best prefix of those values is 8, from the segment \(3, -1, 2, -1, 5\). The final \(-6\) is not included, and the opening \(2\) loses to 8.

### Q7

Answer: B

The product \(xy\) is assembled from the three half-size products \(x_1 y_1\), \(x_0 y_0\), and \((x_1+x_0)(y_1+y_0)\). The fourth product of the grade-school split is recovered by subtractions, which are \(\Theta(n)\) bit work together with the shifts. So \(a = 3\), \(b = 2\), and \(\log_2 3 \approx 1.585\). The linear combine is \(O(n^{\log_2 3 - \varepsilon})\) for a small positive \(\varepsilon\), which is Master case 1, and \(T(n) = \Theta(n^{\log_2 3})\). Four recursive products would be the grade-school \(\Theta(n^2)\) bound. Seven products are Strassen’s matrix recurrence, not integer multiplication.

### Q8

Answer: A, B

Any point farther than \(\delta\) from the dividing line is at least \(\delta\) away from every point on the other side, so a closer cross pair is confined to the strip. Inside one half, \(\delta\) is already a closest distance, and a packing of \(\delta \times \delta\) squares in the strip shows that only a constant number of later \(y\)-neighbours can lie within distance \(\delta\). Maintaining \(y\)-order by a merge, as in merge sort, makes that constant-size window cost \(\Theta(n)\) altogether, and the recurrence is again \(\Theta(n \log n)\). Re-sorting by \(y\) inside every call makes the combine \(\Theta(n \log n)\). The Master case then picks up another logarithm and the solution is \(\Theta(n \log^2 n)\), so (C) is false. Comparing all strip pairs is quadratic in the number of points that fall in the strip, which can be all \(n\) of them. The constant window is the entire reason the combine is linear.

### Q9

Answer: A

\(\log_2 7\) is about \(2.807\), strictly larger than 2. Choose \(\varepsilon = \log_2 7 - 2 > 0\). Then \(n^2 = O(n^{\log_2 7 - \varepsilon})\), which is case 1, and the leaves dominate: \(T(n) = \Theta(n^{\log_2 7})\). Case 2 would require \(f(n)\) to match \(n^{\log_2 7}\) up to a polylogarithm, and \(n^2\) is polynomially smaller. The classical product uses \(\Theta(n^3)\) scalar multiplications, and \(n^{\log_2 7} = o(n^3)\), so the triple loop is the slower of the two. Parenthesising a chain of different matrices is the cubic dynamic program. Strassen receives two square matrices.

### Q10

Answer: A, B, C

A pivot whose rank falls between the 25th and 75th percentiles discards at least a quarter of the keys, and such a pivot occurs often enough under a uniform random rank that the expected sizes form a geometric series of linear cost. The expectation is \(\Theta(n)\). The same procedure still has a chain of extreme pivots, which is \(\Theta(n^2)\) time; randomness makes that chain unlikely, not impossible. Median of medians removes the randomness. Groups of 5 produce a pivot that discards at least about \(3n/10\) keys, leaving a subproblem of size at most \(7n/10\), plus the \(n/5\) call that computes the pivot. The coefficients \(0.2 + 0.7 = 0.9 < 1\) make the linear work shrink geometrically, so the worst case is \(\Theta(n)\). Random sizes are not a fixed \(n/b\), so the Master theorem does not apply to quickselect directly. The median-of-medians bound is a recursion-tree or substitution argument, not a single Master case.

### Q11

Answer: B

In an increasing subarray the last element is the maximum. Lomuto’s final swap, or any partition that uses that pivot, places it at the right end and leaves \(n-1\) keys on its left. The recurrence is \(T(n) = T(n-1) + \Theta(n) = \Theta(n^2)\). This input is the worst case of the endpoint pivot, not the best case. The best case is a pivot near the middle on every call, which sorted data does not provide to this rule. As in Q4, \(b = 1\) is outside the Master theorem.

### Q12

Answer: A, B, D

The children have different sizes, so the hypothesis \(T(n) = aT(n/b) + f(n)\) does not hold. Along the branch that always takes the \(2n/3\) child, the size falls below a constant after \(\Theta(\log n)\) steps, because \(\log_{3/2} n = \Theta(\log n)\). On any level, the subproblem sizes partition the original \(n\), so the non-recursive costs add to \(\Theta(n)\). The product is \(\Theta(n \log n)\). The identity \(1/3 + 2/3 = 1\) does not make the root dominate. That happens for a single chain \(T(n) = T(n/2) + \Theta(n)\), whose level costs form a geometric series \(n + n/2 + n/4 + \cdots\). The even split \(2T(n/2) + \Theta(n)\) is genuine case 2 and has the same \(\Theta\) class.

### Q13

Answer: A

Two keys form an inversion together in exactly one merge: the merge of the smallest interval that contains both, which is the first moment they lie in different halves. Charging \(r\) when the right key is emitted counts each of those \(r\) left keys once, in constant time, with no extra pair loop. Keys that share a half are counted deeper in the recursion, not again at the parent. The combine remains \(\Theta(n)\), Master case 2 still applies, and the time stays \(\Theta(n \log n)\). Equal keys are not inversions. The merge test is \(A[i] > A[j]\), or, if the merge is written with \(\le\) and the left half is preferred, an equal pair emits the left key and adds nothing. Preferring the right half on a tie would treat equals as inversions and would also make the sort unstable.

### Q14

Answer: A, B, C, D

For \(T(n) = 2T(n/2) + \Theta(1)\), one has \(a = 2\), \(b = 2\), \(\log_b a = 1\), and \(f(n) = \Theta(1) = O(n^{1-\varepsilon})\) with \(\varepsilon = 1\). Case 1 gives \(\Theta(n)\). The algorithm looks at a linear number of constant-size leaves and is no faster than scanning. Binary search’s one-sided recurrence is earned by the sorted-array invariant, not by the act of halving alone. A closest-pair implementation that sorts by \(y\) inside each call pays \(\Theta(n \log n)\) to combine two halves. The tree then has \(\Theta(\log n)\) levels of \(\Theta(n \log n)\) work, which is \(\Theta(n \log^2 n)\). Strassen’s exponent prices one product of two square matrices. Ordering a product of many differently shaped matrices is the \(\Theta(n^3)\) chain DP. Using either bound for the other problem answers a different question.
