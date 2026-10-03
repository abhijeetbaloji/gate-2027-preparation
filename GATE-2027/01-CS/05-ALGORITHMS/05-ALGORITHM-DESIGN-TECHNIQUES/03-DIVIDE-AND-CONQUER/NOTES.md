# Divide and Conquer — Learning Notes

Divide and conquer splits an instance into smaller instances of the same problem, solves them, and combines the answers. The subproblems are usually disjoint, so there is no DP table. The running time is a recurrence, almost always solved by the Master theorem or a recursion tree. Merge sort and quicksort are the models; their sort-specific properties are in the sorting notes. This file is about the technique and the other standard applications.

---

## 1. The three steps

**Divide.** Break the input into `a` smaller pieces, typically of size `n/b`. The split must be cheaper than the work you are trying to save, often `O(n)` or `O(1)`.

**Conquer.** Solve the pieces recursively. A piece of constant size is solved directly.

**Combine.** Turn the piece-solutions into a solution of the original instance. In merge sort the combine step is the merge, `Θ(n)`. In quicksort the combine step is empty and the divide step is the partition, `Θ(n)`. In binary search the combine step is `Θ(1)` and only one piece is solved, so `a = 1`.

**Why this is not DP.** The left half of an array and the right half do not share subproblems. Computing both is necessary, and neither is computed twice. If the same subproblem appeared many times, you would add a cache and the algorithm would become DP (matrix chain looks recursive but overlaps, so it is DP).

**Why this is not greedy.** You do not keep a single locally best piece and discard the rest, except in algorithms such as quickselect that *intentionally* discard a side after a partition. Binary search discards a side because of monotonicity, which is a proof, not a heuristic.

---

## 2. Merge sort, and why it is `Θ(n log n)`

**Recurrence.** `T(n) = 2 T(n/2) + Θ(n)`, `T(1) = Θ(1)`.

**Recursion tree.** The root merge costs `c n`. The next level has two merges of size `n/2`, total `c n`. Every level costs `c n`. A size halves each time, so the depth is `log2 n` until size 1. There are `Θ(log n)` levels. Total `Θ(n log n)`.

**Master theorem.** `a = 2`, `b = 2`, `log_b a = 1`, `f(n) = Θ(n^{log_b a})`. Case 2. An extra `log n` appears because every level costs the same amount. `T(n) = Θ(n log n)`.

**Why the input values do not matter.** The split is always in half, and the merge always walks every element. Best, average, and worst case are the same class. (Natural merge sort, which detects existing runs, is a different algorithm.)

**Space.** The merge buffer is `Θ(n)` auxiliary. The recursion stack is `Θ(log n)`.

A full treatment of stability and inversions is in the sorting notes. The point here: equal level costs are what produce the extra logarithm in case 2.

---

## 3. Quicksort, and why it can be `Θ(n²)`

**Divide.** Partition around a pivot in `Θ(n)`.

**Conquer.** Recurse on the two sides. Combine is nothing.

**Balanced case.** Pivot rank near `n/2`: `T(n) = 2 T(n/2) + Θ(n) = Θ(n log n)`, same tree as merge sort.

**Unbalanced case.** Pivot is always the minimum or the maximum: `T(n) = T(n − 1) + T(0) + Θ(n) = T(n − 1) + Θ(n)`. Unrolling gives `n + (n − 1) + … + 1 = Θ(n²)`.

**Why sorted input does this** when the pivot is a fixed endpoint. The endpoint of a sorted array is an extreme key, so one side is empty every time. The recursion degenerates into a chain of length `n`. Randomising the pivot makes the *expected* cost `Θ(n log n)` on every input, because the rank is then uniform. The worst-case shape still exists; it is just unlikely.

**Average.** With a uniform pivot rank,

```
T(n) = Θ(n) + (1/n) Σ_{q=0}^{n−1} (T(q) + T(n−1−q))
```

which solves to `Θ(n log n)`. The Master theorem does not apply directly, because the two sizes are random rather than `n/b`.

| Case | Time | Why | Stack space |
|------|------|-----|-------------|
| Best | `Θ(n log n)` | Even splits | `Θ(log n)` |
| Average | `Θ(n log n)` | Uniform rank | `Θ(log n)` expected |
| Worst | `Θ(n²)` | `T(n) = T(n−1) + Θ(n)` | `Θ(n)` |

---

## 4. Binary search as one-sided divide and conquer

`T(n) = T(n/2) + Θ(1)`. Here `a = 1`, `b = 2`, `log_b a = 0`, `f(n) = Θ(1) = Θ(n^{log_b a})`. Case 2 gives `Θ(log n)`.

You solve only one half because the other half is proved empty of the answer. That proof is the sorted-array invariant. Without it, you would have to solve both halves and the recurrence would be `T(n) = 2T(n/2) + Θ(1) = Θ(n)`, which is no better than a scan.

---

## 5. Counting inversions

An inversion is a pair `i < j`, `A[i] > A[j]`. During the merge of two sorted halves, every time the next output comes from the right half while `r` keys remain on the left, those `r` pairs are inversions. Charge them in `Θ(1)` and otherwise merge as usual.

**Why the time stays `Θ(n log n)`.** The extra work per merge is still linear. The recurrence does not change. A double loop over all pairs is `Θ(n²)`. Divide and conquer wins because each pair is counted in the unique merge that first separates its two elements into different halves... actually each inversion is counted exactly once, in the merge where the two elements are in different halves and those halves are being merged. That uniqueness is why you do not double-count.

**Space.** `Θ(n)` merge buffer, like merge sort.

---

## 6. Maximum subarray

**The problem.** Contiguous segment of maximum sum. (An empty segment is sometimes allowed and has sum 0; GATE usually wants a non-empty segment. Read the stem.)

**Divide and conquer.** Split at the midpoint. The optimum lies entirely on the left, entirely on the right, or it crosses the midpoint. The two sides are recursive. The crossing sum is the best suffix of the left half plus the best prefix of the right half, computed in `Θ(n)` by two scans.

**Recurrence.** `T(n) = 2 T(n/2) + Θ(n) = Θ(n log n)`.

**Kadane’s algorithm is not this recurrence.** One left-to-right pass keeps the best segment that ends at the current index: extend the previous ending-here sum if it is positive, otherwise start over. Time `Θ(n)`, space `Θ(1)`. It is a DP (or a scan), and it dominates the divide-and-conquer version. Know both, and do not quote `Θ(n log n)` if a linear scan is what the question allows.

**Example.** `[2, −3, 4, −1, 2, 1, −5, 4]`. Kadane’s ending-here sums reach a best of `4 + (−1) + 2 + 1 = 6`. The crossing idea on a midpoint between `−1` and `2` also finds that segment. A segment that is only the last `4` sums to 4 and loses.

**GATE trap.** Using the divide-and-conquer crossing scan but forgetting one of the two recursive sides. The maximum might not cross the particular midpoint you chose; that is why both halves must be solved.

---

## 7. Closest pair of points

**The problem.** `n` points in the plane. Euclidean distance. Find the minimum distance between two distinct points. A double loop is `Θ(n²)`.

**Algorithm.**

1. Sort by x-coordinate once, `Θ(n log n)`, and keep a y-sorted copy.
2. Split the point set by x-coordinate into two halves of `n/2`.
3. Recursively find the closest distance `δL` on the left and `δR` on the right. Let `δ = min(δL, δR)`.
4. The closest pair is either inside a half or has one point in each half. Any cross pair closer than `δ` must lie in the vertical strip of width `2δ` around the dividing line.
5. Walk that strip in y-order. For each point, only the next few points in y-order can lie within `δ`. A standard packing argument says at most 7 later points need to be checked (the other half’s `δ × δ` squares cannot hold two points each, because `δ` is already a closest distance inside each half).

**Why the combine is linear.** Each point does `O(1)` distance computations against later strip points, not `O(n)`.

**Recurrence.** `T(n) = 2 T(n/2) + Θ(n) = Θ(n log n)` after the initial sort. If you re-sort by y inside every call, the combine becomes `Θ(n log n)` and the solution is `Θ(n log² n)`. The careful version passes y-sorted lists down and merges them like merge sort, keeping the combine linear.

| Version | Time | Space |
|---------|------|-------|
| Brute force | `Θ(n²)` | `Θ(1)` |
| Re-sort by y each time | `Θ(n log² n)` | `Θ(n)` |
| Y-order maintained | `Θ(n log n)` | `Θ(n)` |

**Why not a one-dimensional trick only.** On a line, sort and check neighbours, `Θ(n log n)` worst case, and the strip argument is unnecessary. The plane needs the strip because two points can be close in distance and far in x-index.

**GATE traps.**

- Claiming `Θ(n log n)` for the version that sorts by y inside every call.
- Checking every pair inside the strip and calling that `O(n)`. A full strip scan of all pairs is quadratic in the strip size; the constant-size window is the whole trick.
- Forgetting the initial sort in the recurrence. It is the same class, so the bound survives, but a question that asks for the recurrence of the recursive part wants `2T(n/2) + O(n)`.

---

## 8. Integer multiplication and Strassen

**Grade-school multiplication** of two `n`-bit integers (or `n`-digit) is `Θ(n²)` bit operations.

**Karatsuba.** Write `x = x1 · 2^{n/2} + x0`, similarly `y`. The product needs three multiplications of `n/2`-bit numbers, not four:

```
x y = x1 y1 · 2^n + ((x1+x0)(y1+y0) − x1 y1 − x0 y0) · 2^{n/2} + x0 y0
```

Recurrence `T(n) = 3 T(n/2) + Θ(n)`. `log2 3 ≈ 1.585`. Case 1 of the Master theorem: `f(n) = n = O(n^{log2 3 − ε})`. So `T(n) = Θ(n^{log2 3})`, about `Θ(n^{1.585})`, which beats `Θ(n²)`.

**Strassen’s matrix product.** Two `n × n` matrices. The naive product is `Θ(n³)` scalar multiplications: `n²` entries, each a dot product of length `n`. Block the matrices into four `n/2` blocks. Strassen forms the product from **7** block multiplications plus `Θ(n²)` additions, instead of 8.

```
T(n) = 7 T(n/2) + Θ(n²) = Θ(n^{log2 7})
```

`log2 7 ≈ 2.807`. Again case 1, because `n²` is polynomially smaller than `n^{log2 7}`.

**What Strassen is not.** It does not schedule a chain of different matrices. That is the cubic DP in the dynamic-programming notes. It also does not change the definition of matrix multiplication; it only reduces the arithmetic count. The constant factors are large, which matters in practice and does not matter for the Theta class.

**GATE trap.** Quoting `O(n³)` as the best possible matrix multiplication. It is the standard bound. Strassen is a legal better exponent when the question asks for a divide-and-conquer matrix product. Quoting Strassen for matrix-chain parenthesisation is a category error.

---

## 9. Select and quickselect

Quickselect partitions like quicksort and recurses into **one** side, the side that contains rank `k`.

**Expected time** with a random pivot is `Θ(n)`. Intuition: a good pivot (rank between 25% and 75%) happens often enough that the expected sizes form a geometric series `n + (3/4)n + (3/4)² n + … = Θ(n)`. The Master theorem does not apply to the random sizes; the expectation is proved by conditioning on the pivot rank.

**Worst case** of that version is `Θ(n²)`, the same bad pivots as quicksort.

**Median of medians** forces a good pivot. Groups of 5, median of each group, then the median of those medians. The pivot is guaranteed to discard at least about 30% of the elements. 

```
T(n) ≤ T(n/5) + T(7n/10) + O(n) = Θ(n)
```

because `1/5 + 7/10 = 0.9 < 1`. The work shrinks geometrically. This is worst-case linear selection, and it can be used as a pivot to make quicksort worst-case `Θ(n log n)`, with a large constant.

---

## 10. Reading a new recurrence

| Recurrence | Solution | Why |
|------------|----------|-----|
| `2T(n/2) + n` | `Θ(n log n)` | Equal level costs, `log n` levels |
| `2T(n/2) + 1` | `Θ(n)` | Leaves dominate |
| `2T(n/2) + n²` | `Θ(n²)` | Root dominates |
| `T(n/2) + 1` | `Θ(log n)` | One path of length `log n` |
| `3T(n/2) + n` | `Θ(n^{log2 3})` | Karatsuba, case 1 |
| `7T(n/2) + n²` | `Θ(n^{log2 7})` | Strassen, case 1 |
| `T(n−1) + n` | `Θ(n²)` | Not Master; unroll |
| `T(n/3) + T(2n/3) + n` | `Θ(n log n)` | Not Master; tree depth `log_{3/2} n`, each level `Θ(n)` |

---

## 11. How to choose

| Situation | Technique |
|-----------|-----------|
| Sort with a worst-case guarantee and stability | Merge sort |
| Sort in place, average speed | Quicksort |
| Search a sorted array | Binary search |
| Count inversions | Merge sort with a counter |
| Maximum subarray, linear time wanted | Kadane |
| Maximum subarray, illustrating divide and conquer | Crossing-midpoint recurrence, `Θ(n log n)` |
| Closest points in the plane | Strip method, `Θ(n log n)` if y-order is maintained |
| Large integer product | Karatsuba |
| Two square matrices, arithmetic count | Strassen if a sub-cubic bound is asked; classical triple loop otherwise |
| `k`-th smallest, expected linear | Quickselect |
| `k`-th smallest, worst-case linear | Median of medians |
| Overlapping subproblems (chain order, knapsack, LCS) | DP, not divide and conquer |
| One local choice proved safe | Greedy |

---

## 12. Common GATE traps

1. Merge sort’s case 2 written as `Θ(n)` because `f(n) = n`.
2. Quicksort’s worst case blamed on “random data”. The bad case is a pivot rule that keeps hitting an extreme key.
3. Master theorem applied to `T(n) = T(n−1) + n` or to two different fractions `n/3` and `2n/3`.
4. Closest-pair combine claimed linear while each call sorts by y from scratch.
5. Strassen used as the answer to matrix-chain ordering.
6. Karatsuba described as four half-size multiplications. The saving is that one of the four is replaced by additions.
7. Maximum subarray’s divide-and-conquer bound quoted when Kadane is the expected linear algorithm.
8. Quickselect’s expected `Θ(n)` stated as a worst-case bound.
9. Inversion count double-charged, or charged in `Θ(n²)` inside a merge.
10. Binary search written as `2T(n/2)` as if both halves were solved.
