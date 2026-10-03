# Sorting — Practice Questions

Original practice for GATE CS. These questions are not from any GATE paper. Attempt the questions before reading the solutions.

## Level 1 — Conceptual

## Q1 — MCQ

Selection sort is run on \(n\) distinct keys. It scans each unsorted suffix completely and swaps the minimum into the next prefix position. Which statement is correct?

A. It always makes \(n(n-1)/2\) comparisons, and at most \(n-1\) swaps.

B. It always makes \(n-1\) comparisons, and \(n(n-1)/2\) swaps.

C. Both comparisons and swaps are \(\Theta(n \log n)\) in the worst case.

D. The running time is \(\Theta(n)\) because only \(n-1\) swaps are performed.

---

## Q2 — MSQ

Select all that apply. The sort is the standard top-down merge sort that always splits in half and merges, taking the left half first on a tie.

A. \(T(n) = 2T(n/2) + \Theta(n)\) solves to \(\Theta(n \log n)\) by Master case 2.

B. On an already sorted array the same algorithm runs in \(\Theta(n)\) time.

C. The merge buffer uses \(\Theta(n)\) auxiliary memory.

D. The tie rule makes the sort stable.

---

## Q3 — NAT

Selection sort compares every pair of positions that the nested suffix scans examine. For \(n = 10\), how many comparisons does it perform?

---

## Q4 — MCQ

Bottom-up construction of a binary heap, sifting down from the last non-leaf, costs

A. \(\Theta(n \log n)\), the same bound as inserting \(n\) keys one by one into an empty heap

B. \(\Theta(n)\), because a node of height \(h\) costs \(O(h)\) and \(\sum_h h/2^h\) converges

C. \(\Theta(\log n)\)

D. \(\Theta(n^2)\)

---

## Q5 — MSQ

Select all that apply. Counting sort orders integer keys whose values lie in \(0, \ldots, k\). The output is filled from the right end of the input, and the cumulative count of a value is decreased after each placement.

A. The algorithm is a comparison sort, so it needs \(\Omega(n \log n)\) time.

B. Every input order costs \(\Theta(n + k)\) time.

C. The right-to-left fill makes equal keys keep their original order.

D. The same bound holds inside the comparison model and therefore contradicts the decision-tree lower bound.

---

## Level 2 — Standard GATE Style

## Q6 — NAT

Insertion sort shifts a key left while the preceding key is strictly greater. On 6 distinct keys in reverse sorted order, how many shifts does it perform?

---

## Q7 — MCQ

Lomuto partition uses the last element as the pivot and swaps a key left when it is strictly smaller than the pivot. The input is \([7, 2, 6, 1, 5]\). After the pivot has been swapped into its final place, the array is

A. \([2, 1, 5, 7, 6]\)

B. \([1, 2, 5, 6, 7]\)

C. \([2, 1, 6, 5, 7]\)

D. \([1, 2, 7, 6, 5]\)

---

## Q8 — MSQ

Select all that apply. Heap sort builds a max-heap in the input array and then extracts the maximum \(n-1\) times. Sift-down is written with loops, not recursion. Array indexes start at 0.

A. The worst-case time is \(\Theta(n \log n)\).

B. Equal keys keep their original relative order.

C. Auxiliary memory beyond the input array is \(\Theta(1)\).

D. The children of index \(i\) are \(2i+1\) and \(2i+2\).

---

## Q9 — NAT

Counting sort is run on \([2, 0, 2, 1]\) with values in \(0, \ldots, 2\), filling the output from right to left so that the sort is stable. At which 0-based output index is the leftmost input 2 written?

---

## Q10 — MCQ

Least-significant-digit radix sort sorts one digit at a time, starting from the ones digit. Each digit pass must be

A. unstable, so a later digit is free to reorder equal digits

B. stable, so the order produced by an earlier digit survives inside one digit group

C. a comparison sort whose cost is \(\Theta(n \log n)\) per digit

D. in-place quicksort, because the digit alphabet is small

---

## Q11 — MSQ

Select all that apply. Bucket sort throws numeric keys into \(n\) equal-width buckets and sorts each bucket by insertion sort.

A. If the keys are uniform, the expected running time is \(\Theta(n)\).

B. If every key falls into one bucket, the worst-case time is \(\Theta(n^2)\).

C. The worst-case time is \(\Theta(n \log n)\) for every distribution.

D. The linear expectation uses the uniformity assumption.

---

## Level 3 — Multi-Step

## Q12 — NAT

How many inversions does \([5, 1, 4, 2, 3]\) contain? An inversion is a pair of indexes \(i < j\) with \(A[i] > A[j]\).

---

## Q13 — MCQ

Distinct keys are sorted by quicksort. The pivot rank is always 1 or \(n\) inside the current subarray. The worst-case recurrence is

A. \(T(n) = 2T(n/2) + \Theta(n) = \Theta(n \log n)\)

B. \(T(n) = T(n-1) + \Theta(n) = \Theta(n^2)\)

C. \(T(n) = T(n/2) + \Theta(n) = \Theta(n)\)

D. \(T(n) = T(n-1) + \Theta(1) = \Theta(n)\)

---

## Q14 — MSQ

Select all that apply. The \(k\)-th smallest key is selected from \(n\) distinct keys.

A. Median-of-medians with groups of 5 satisfies \(T(n) \le T(n/5) + T(7n/10) + O(n)\).

B. Because \(1/5 + 7/10 < 1\), that recurrence is \(\Theta(n)\) in the worst case.

C. Plain quickselect, recursing into one side of a naive partition, is \(\Theta(n)\) in the worst case.

D. Plain quickselect with a uniformly random pivot has expected time \(\Theta(n)\).

---

## Q15 — NAT

An external merge sorts \(N = 10000\) records. Memory holds \(M = 100\) records, and each pass merges \(k = 10\) runs. How many merge passes are required after the initial runs have been formed? Use \(\lceil \log_k (N/M) \rceil\).

---

## Q16 — MSQ

Select all that apply. Quicksort partitions in place and recurses on both sides. The pivot can be an extreme key on every call.

A. The worst-case recursion depth is \(\Theta(n)\).

B. When pivot ranks stay near the middle, the stack depth is \(\Theta(\log n)\).

C. Auxiliary memory, including the recursion stack, is \(\Theta(1)\) on every input.

D. The \(\Theta(n^2)\) time case and the \(\Theta(n)\) stack case can occur on the same input.

---

## Level 4 — Tricky / Trap-Based

## Q17 — MCQ

The input is already sorted in increasing order. Quicksort always pivots on the first element of the current subarray. Insertion sort shifts only while the preceding key is strictly greater. Their running times on this input are

A. quicksort \(\Theta(n^2)\), insertion sort \(\Theta(n)\)

B. both \(\Theta(n)\)

C. quicksort \(\Theta(n \log n)\), insertion sort \(\Theta(n^2)\)

D. both \(\Theta(n^2)\)

---

## Q18 — MSQ

Select all that apply.

A. Bubble sort that stops when a pass makes no swap is \(\Theta(n)\) on a sorted array.

B. Bubble sort that always executes \(n-1\) passes is \(\Theta(n)\) on a sorted array.

C. Selection sort is \(\Theta(n)\) because it writes at most \(n-1\) swaps.

D. Insertion sort that moves a key left only while \(A[j] > \mathrm{key}\) is stable.

---

## Q19 — MCQ

A student charges \(\Theta(\log n)\) to every node and concludes that bottom-up heap construction is \(\Theta(n \log n)\). What is the correct account of the bottom-up algorithm?

A. The student’s bound is tight for bottom-up construction.

B. Leaves do not sift, a node of height \(h\) costs \(O(h)\), and \(\sum h \cdot n / 2^{h}\) is \(\Theta(n)\). Inserting \(n\) keys one by one is the algorithm that costs \(\Theta(n \log n)\).

C. Bottom-up construction is \(\Theta(\log n)\).

D. After a linear build, the \(n\) extracts of heap sort are also linear.

---

## Level 5 — Challenge

## Q20 — MCQ

Records are ordered by the numeric key, and the letter is only a label. Selection sort repeatedly swaps the minimum of the suffix into the next position. The input, in order, is \((2,a),\ (3,x),\ (2,b),\ (1,y)\). After the sort, the two records of key 2 appear as

A. \(a\) before \(b\)

B. \(b\) before \(a\)

C. one of them deleted, because the keys are equal

D. \(a\) before \(b\), because selection sort is stable

---

## Q21 — NAT

Among arrays of \(n = 9\) distinct keys, what is the maximum number of inversions?

---

## Q22 — MSQ

Select all that apply.

A. Every comparison sort uses \(\Omega(n \log n)\) comparisons in the worst case.

B. Counting sort on keys in \(0, \ldots, n\) is a counterexample to (A).

C. The decision-tree bound does not apply to counting sort, because counting sort indexes by key value instead of comparing pairs of keys.

D. Least-significant-digit radix sort stays correct if a digit pass is unstable.

## Answer Key

| Q | Type | Answer |
|---|------|--------|
| 1 | MCQ | A |
| 2 | MSQ | A, C, D |
| 3 | NAT | 45 |
| 4 | MCQ | B |
| 5 | MSQ | B, C |
| 6 | NAT | 15 |
| 7 | MCQ | A |
| 8 | MSQ | A, C, D |
| 9 | NAT | 2 |
| 10 | MCQ | B |
| 11 | MSQ | A, B, D |
| 12 | NAT | 6 |
| 13 | MCQ | B |
| 14 | MSQ | A, B, D |
| 15 | NAT | 2 |
| 16 | MSQ | A, B, D |
| 17 | MCQ | A |
| 18 | MSQ | A, D |
| 19 | MCQ | B |
| 20 | MCQ | B |
| 21 | NAT | 36 |
| 22 | MSQ | A, C |

## Detailed Solutions

### Q1

Answer: A

The suffix lengths are \(n-1, n-2, \ldots, 1\), and each of those keys is compared no matter what the values are. The sum is \(n(n-1)/2\). Each of the \(n-1\) prefix positions receives at most one swap. The running time follows the comparisons, so it is \(\Theta(n^2)\) in the best, average, and worst cases. A linear swap count does not make the algorithm linear.

### Q2

Answer: A, C, D

Master’s theorem: \(a = 2\), \(b = 2\), \(\log_b a = 1\), and \(f(n) = \Theta(n) = \Theta(n^{\log_b a})\). Case 2 gives \(T(n) = \Theta(n \log n)\). The recursion tree says the same thing: every level merges \(\Theta(n)\) keys and there are \(\Theta(\log n)\) levels. The split does not look at the values, so a sorted input does not become a linear special case. The merge writes into a buffer of length \(n\). On a tie, emitting the left half first keeps the earlier equal key on the left, so the sort is stable.

### Q3

Answer: 45

The comparison count is \(10 \cdot 9 / 2 = 45\). It does not depend on the input order.

### Q4

Answer: B

In a heap, at most about \(n/2^{h+1}\) nodes have height \(h\), and a sift from such a node walks \(O(h)\) edges. The total is \(O(n) \sum_h h/2^h\). The series \(\sum_h h/2^h\) equals 2, so the build is \(\Theta(n)\). The different algorithm that inserts \(n\) keys into an empty heap pays \(\Theta(\log n)\) per insertion and is \(\Theta(n \log n)\). Heap sort’s later \(n\) extracts bring the whole sort back to \(\Theta(n \log n)\); the linear build is absorbed, not cancelled.

### Q5

Answer: B, C

Counting sort never asks whether one key is smaller than another. It uses the key as an index, so the \(\Omega(n \log n)\) comparison lower bound does not apply, and there is no contradiction. The loops scan the \(n\) keys and the \(k+1\) counters, which is \(\Theta(n+k)\) for every order. Processing the input from right to left places the rightmost copy of a value into the rightmost reserved slot, then the next copy further left. Equal keys therefore keep their original order.

### Q6

Answer: 15

A reverse-sorted array of 6 distinct keys has every pair inverted. The number of pairs is \(6 \cdot 5 / 2 = 15\). Each insertion-sort shift, under the strict test \(A[j] > \mathrm{key}\), removes exactly one inversion, so the shift count is 15. The best case, an already sorted array, shifts nothing and compares only \(n-1 = 5\) times.

### Q7

Answer: A

The pivot is 5. The boundary of keys known to be smaller starts at the left.

- 7 is not smaller.
- 2 is smaller, so it is swapped into the boundary: \([2, 7, 6, 1, 5]\).
- 6 is not smaller.
- 1 is smaller, so it is swapped with 7: \([2, 1, 6, 7, 5]\).
- The pivot is then swapped into the boundary: \([2, 1, 5, 7, 6]\).

Every key left of 5 is smaller than 5, and every key to the right is larger. The partition does not fully sort the two sides. That is why (B) is the finished sort, not the partition.

### Q8

Answer: A, C, D

After the linear build, each of \(n-1\) extracts sifts from the root down a heap of height \(\lfloor \log_2 n \rfloor\). The total is \(\Theta(n \log n)\) in every case, because the heap shape, not the key order, fixes the height. A sift can move a leaf past an equal key, so heap sort is not stable. An iterative sift stores only a few indexes. In a 0-based array the children of \(i\) are \(2i+1\) and \(2i+2\); the 1-based formulas \(2i\) and \(2i+1\) are a different layout.

### Q9

Answer: 2

Counts of 0, 1, and 2 are \(1, 1, 2\). The prefix sums, meaning “number of keys \(\le v\)”, are \([1, 2, 4]\).

- The rightmost key is 1. It is written at index \(2-1 = 1\), and the count of 1 falls to 1.
- The next key is the right-hand 2. It is written at index \(4-1 = 3\), and the count of 2 falls to 3.
- The next key is 0. It is written at index 0.
- The leftmost 2 is written at index \(3-1 = 2\).

The output is \([0, 1, 2, 2]\). The left-hand 2 stays left of the right-hand 2, which is the stability invariant. Its output index is 2.

### Q10

Answer: B

After the ones digit has been sorted, keys that share a tens digit must keep the ones order already computed. A stable digit sort does that: it groups by the current digit and does not reorder equal digits. An unstable pass can swap two keys that agreed on the current digit and differed on an earlier digit, and the earlier pass is lost. The usual digit pass is counting sort, costing \(\Theta(n+b)\) for a digit alphabet of size \(b\), not a comparison sort.

### Q11

Answer: A, B, D

Uniform keys give each bucket an expected constant size. Sorting a constant-size bucket by insertion sort is expected constant work, and \(n\) buckets give expected \(\Theta(n)\). The expectation is false without a distribution promise. If one bucket receives every key, insertion sort on that bucket is \(\Theta(n^2)\). Option (C) would be the right class for merge sort or heap sort, not for this bucket sort.

### Q12

Answer: 6

The inverted pairs are \((5,1),\ (5,4),\ (5,2),\ (5,3),\ (4,2),\ (4,3)\). That is 6. The pair \((1,2)\) and the pair \((2,3)\) are in order, so they are not inversions. Merge sort counts the same 6: whenever a key is emitted from the right half while \(r\) keys remain on the left, those \(r\) pairs are inversions, and each inversion is charged in exactly one merge.

### Q13

Answer: B

An extreme pivot leaves one side empty and the other side of size \(n-1\). Partition still looks at \(\Theta(n)\) keys. Unrolling \(T(n) = T(n-1) + \Theta(n)\) produces the sum \(n + (n-1) + \cdots + 1 = \Theta(n^2)\). The balanced recurrence in (A) is the best-case shape, not this one. The Master theorem does not apply, because the subproblem size is \(n-1\) rather than \(n/b\).

### Q14

Answer: A, B, D

Groups of 5 are sorted in linear time. The median of the \(n/5\) group medians is a pivot that is guaranteed to be larger than at least about \(3n/10\) keys and smaller than at least about \(3n/10\) keys, so the recursive selection is on at most \(7n/10\) keys, plus a recursive call of size \(n/5\) to find the pivot. The coefficients sum to \(0.9 < 1\), and the \(O(n)\) work per level forms a shrinking geometric series, so \(T(n) = \Theta(n)\) in the worst case. Plain quickselect has the same bad pivots as quicksort, so its worst case is \(\Theta(n^2)\). With a random pivot the expected discarded fraction is large enough that the expectation is \(\Theta(n)\). “Selection is linear” is therefore true for median-of-medians in the worst case, and for randomised quickselect only in expectation.

### Q15

Answer: 2

The initial runs number \(N/M = 100\). Each pass reduces the number of runs by a factor of 10, so the number of passes is \(\lceil \log_{10} 100 \rceil = 2\). The first pass produces 10 runs, and the second pass produces one sorted run.

### Q16

Answer: A, B, D

A chain of extreme pivots makes \(n\) nested calls, so the stack is \(\Theta(n)\) at the same time as the running time is \(\Theta(n^2)\). Balanced pivots give \(\Theta(\log n)\) depth and \(\Theta(n \log n)\) time. Calling the extra memory \(\Theta(1)\) forgets those frames. Time and stack are different resources, but on the degenerate input both are large.

### Q17

Answer: A

The first element of a sorted subarray is its minimum. The left side of the partition is empty and the right side has \(n-1\) keys, which is the recurrence of Q13, so quicksort takes \(\Theta(n^2)\) time. Insertion sort walks the array once, the inner test \(A[j] > \mathrm{key}\) fails immediately, and it makes \(n-1\) comparisons, which is \(\Theta(n)\). Sorted input is the worst case of this pivot rule and the best case of insertion sort.

### Q18

Answer: A, D

(A) is true: the flag version makes one pass of \(n-1\) comparisons, swaps nothing, and stops. (B) is false: \(n-1\) full passes are \(\Theta(n^2)\) even when no swap occurs. The linear best case requires the flag. (C) is false for the reason in Q1: the quadratic comparisons dominate the linear writes. (D) is true: an equal key fails the test \(A[j] > \mathrm{key}\), so the new key stops to the right of the older equal key. Replacing \(>\) by \(\ge\) would slide the new key past the older one and destroy stability.

### Q19

Answer: B

The student’s charge gives every node the cost of the root. In the bottom-up build, a leaf is never sifted, and the number of nodes of height \(h\) falls geometrically. The resulting sum is \(\Theta(n)\), as in Q4. The \(\Theta(n \log n)\) bound is the cost of \(n\) separate insertions, and it is also the cost of the extract phase of heap sort, not of the build alone. The extracts are not linear: each can walk \(\Theta(\log n)\) edges.

### Q20

Answer: B

- Suffix minimum is \((1,y)\), swapped with \((2,a)\): \([(1,y),\ (3,x),\ (2,b),\ (2,a)]\).
- Next suffix minimum is \((2,b)\), swapped with \((3,x)\): \([(1,y),\ (2,b),\ (3,x),\ (2,a)]\).
- Next suffix minimum is \((2,a)\), swapped with \((3,x)\): \([(1,y),\ (2,b),\ (2,a),\ (3,x)]\).

The later record \(b\) has moved ahead of the earlier record \(a\). Selection sort is not stable: the swap that places a minimum can leap over an equal key. The stable order would have been \(a\) before \(b\).

### Q21

Answer: 36

Every pair is an inversion exactly when the array is reversed. The number of pairs among 9 keys is \(9 \cdot 8 / 2 = 36\). Insertion sort performs that many shifts on the reversed array, and bubble sort performs that many adjacent swaps.

### Q22

Answer: A, C

A comparison sort’s decision tree has at least \(n!\) leaves, one per permutation of distinct keys. A binary tree of height \(h\) has at most \(2^h\) leaves, so \(h \ge \log_2(n!)\). Stirling’s approximation gives \(\log_2(n!) = \Theta(n \log n)\). Counting sort does not build that tree. It is not a counterexample to a theorem whose hypothesis it does not satisfy. Unstable digit passes break least-significant-digit radix sort, because an earlier digit’s order is exactly what stability was preserving.
