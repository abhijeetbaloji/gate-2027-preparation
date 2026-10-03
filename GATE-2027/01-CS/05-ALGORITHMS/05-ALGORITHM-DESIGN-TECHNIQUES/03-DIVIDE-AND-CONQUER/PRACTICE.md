# Divide and Conquer — Practice

These are practice questions, not GATE questions.

### Level 1 — Concept

**1.** Why does a divide-and-conquer merge sort not use a DP table?

**2.** Solve `T(n) = 2T(n/2) + n`.

**3.** Why does endpoint-pivot quicksort on a sorted array become quadratic?

**4.** Binary search’s recurrence has `a = 1`, not `a = 2`. Why?

**5.** What does Strassen reduce from 8 to 7?

### Level 2 — Standard

**6.** Time and auxiliary buffer of merge sort.

**7.** Best, average, and worst time of quicksort with a fixed last-element pivot.

**8.** How many inversions are revealed when a merge emits a right-half key while 4 left-half keys remain?

**9.** Kadane versus divide-and-conquer maximum subarray: the two time bounds.

**10.** Solve `T(n) = 7T(n/2) + n²`.

### Level 3 — Multi-step

**11.** Array `[4, 1, 3, 2]`. How many inversions does the merge-sort counter report? List the pairs.

**12.** Maximum subarray of `[−2, 1, −3, 4, −1, 2, 1, −5, 4]` by Kadane. Give the sum.

**13.** Closest pair: if every recursive call sorts its points by y-coordinate, what recurrence and solution do you get?

**14.** Karatsuba uses `T(n) = 3T(n/2) + Θ(n)`. Which Master case, and why is the answer not `Θ(n log n)`?

**15.** Median of medians: why does `T(n) ≤ T(n/5) + T(7n/10) + O(n)` stay linear?

### Level 4 — Trap-based

**16.** “Merge sort is case 2, and `f(n) = n`, so `T(n) = Θ(n)`.” What was dropped?

**17.** `T(n) = T(n/3) + T(2n/3) + n` is fed to the Master theorem with `a = 2`, `b = 3`. Why is that illegal, and what is the real bound?

**18.** A solution quotes `O(n^{2.807})` for ordering a product of `n` different matrices. Which algorithm was confused with which?

**19.** Quickselect is given worst-case `Θ(n)`. Which algorithm was meant, if the bound is to be true?

**20.** The maximum-subarray recursion computes only the best crossing sum at the top level and returns it. Give an array where this misses the optimum.

### Level 5 — Challenge

**21.** Show the level costs of `T(n) = 2T(n/2) + n²` sum to at most `2n²`.

**22.** During a merge, why is each inversion counted at most once?

**23.** Explain the Karatsuba identity enough to see where the fourth product goes. You may use `x = x1 B + x0`, `y = y1 B + y0`.

**24.** In the closest-pair strip, why can a point be compared with only a constant number of later points rather than all of them?

**25.** A randomised quicksort has expected time `Θ(n log n)` on a sorted array. A deterministic last-pivot quicksort does not. What changed in the recurrence?

---

## Answers and explanations

**1.** The left and right halves are disjoint. Each subarray is sorted once. A table would not remove repeated work, because there is none.

**2.** Master case 2: `a = 2`, `b = 2`, `log_b a = 1`, `f(n) = Θ(n)`. Solution `Θ(n log n)`.

**3.** The pivot is the smallest or largest key, so one side has size `n − 1`. `T(n) = T(n − 1) + Θ(n) = Θ(n²)`.

**4.** The sorted-order test proves the key cannot lie in one half. Only one recursive call is made. Solving both halves would be `Θ(n)`.

**5.** The number of recursive block multiplications of `(n/2) × (n/2)` matrices. Additions stay `Θ(n²)`.

**6.** Time `Θ(n log n)` in every case. Buffer `Θ(n)`. Stack `Θ(log n)` on top of that if the implementation is recursive.

**7.** Best `Θ(n log n)`, average `Θ(n log n)`, worst `Θ(n²)`.

**8.** 4. Each of those left keys forms an inversion with the emitted key.

**9.** Kadane `Θ(n)`. Divide and conquer `Θ(n log n)`.

**10.** `log2 7 ≈ 2.807`. `n² = O(n^{log2 7 − ε})`, case 1. `Θ(n^{log2 7})`.

**11.** Pairs `(4,1), (4,3), (4,2), (3,2)`. Four inversions.

**12.** 6, from `[4, −1, 2, 1]`.

**13.** `T(n) = 2T(n/2) + Θ(n log n)`. `log_b a = 1`, and `f(n) = Θ(n log n) = Θ(n^{log_b a} log^1 n)`, so extended case 2 gives `Θ(n log² n)`.

**14.** Case 1, not case 2. The critical exponent is `log2 3 ≈ 1.585`, and `f(n) = n` is polynomially smaller. Case 2 would need `f` to match `n^{log2 3}`. The solution is `Θ(n^{log2 3})`, which is larger than `n log n` and smaller than `n²`.

**15.** The coefficients `0.2 + 0.7 = 0.9 < 1`. Subproblem sizes shrink by a constant factor in total, so the non-recursive `O(n)` costs form a geometric series bounded by `O(n)`.

**16.** The extra `log n` from `Θ(log n)` equal levels. The correct class is `Θ(n log n)`.

**17.** The two subproblems are not the same size, so there is no single `b` with `a` identical pieces. Depth is `Θ(log n)` along the `2/3` branch, and each level costs `Θ(n)`, so the bound is still `Θ(n log n)`.

**18.** Strassen’s exponent belongs to multiplying two `n × n` matrices. Ordering a chain of many matrices is the `Θ(n³)` DP. The `n` in those two bounds is not even the same kind of parameter (matrix dimension versus number of factors).

**19.** Median of medians (worst-case linear selection). Plain quickselect is expected linear and worst-case quadratic.

**20.** `[1, 5, −10, 1]`. Midpoint between `5` and `−10`. The best crossing segment has to include both middle elements or a bridge across them; the best sum that touches both sides is at most `5 + (−10) + 1 = −4`, or `−10 + 1 = −9`, while the left half alone contains `5` (and `1+5=6`). Returning only a crossing sum misses 6. (Any array whose maximum segment lies strictly on one side works.)

**21.** Level `i` costs `n² / 2^i`. Sum `n² (1 + 1/2 + 1/4 + …) < n² · 2`.

**22.** An inverting pair has a unique lowest merge that places the two elements in different halves: the first time their ranges are split apart. Only that merge sees them as a left key and a right key. Later merges see them already in one combined sorted run, or not as that pair. So the charge happens in one merge.

**23.** `xy = x1 y1 B² + (x1 y0 + x0 y1) B + x0 y0`. The middle coefficient equals `(x1+x0)(y1+y0) − x1 y1 − x0 y0`. That expression reuses the two products `x1 y1` and `x0 y0` and adds only one new product, the sum-pair. Four products would have been `x1 y1`, `x1 y0`, `x0 y1`, `x0 y0`.

**24.** Inside each half, every pair is at least `δ` apart. In the strip, points therefore cannot cluster: a later point more than `δ` away in y-coordinate is already too far, and within y-distance `δ` the packing of `δ`-separated points leaves only a constant number of candidates.

**25.** The pivot rank became uniform, because the pivot index is random, so the average-case split recurrence applies even though the values are sorted. The deterministic rule always selects the maximum of a sorted subarray, so every split is 0 and `n−1`.
