# Divide and Conquer — Formulas

| Result | When it applies |
|--------|-----------------|
| `T(n) = 2T(n/2) + Θ(n) = Θ(n log n)` | Merge sort, inversion count, closest pair with a linear combine, maximum-subarray D&C, balanced quicksort |
| `T(n) = T(n−1) + Θ(n) = Θ(n²)` | Quicksort with every pivot extreme |
| Average quicksort `Θ(n log n)` | Pivot rank uniform; not a direct Master application |
| `T(n) = T(n/2) + Θ(1) = Θ(log n)` | Binary search; only one half is solved |
| `T(n) = 2T(n/2) + Θ(1) = Θ(n)` | Both halves solved and combine is constant; also the lower bound shape of a full scan |
| Inversions during merge | Emitting a right-half key while `r` left keys remain adds `r` inversions. Total time stays `Θ(n log n)` |
| Maximum subarray D&C `Θ(n log n)` | Left, right, and crossing suffix+prefix |
| Kadane `Θ(n)` time, `Θ(1)` extra space | Best sum ending at `i`, then a global max. Prefer this when a linear algorithm is allowed |
| Closest pair `T(n) = 2T(n/2) + Θ(n) = Θ(n log n)` | Y-order maintained; each strip point checks `O(1)` later points |
| Closest pair with a fresh y-sort each call | `Θ(n log² n)` |
| Karatsuba `T(n) = 3T(n/2) + Θ(n) = Θ(n^{log2 3})` | `log2 3 ≈ 1.585`. Three half-size products, not four |
| Strassen `T(n) = 7T(n/2) + Θ(n²) = Θ(n^{log2 7})` | `log2 7 ≈ 2.807`. Two square matrices, not a matrix chain |
| Naive matrix product `Θ(n³)` | Triple loop |
| Median of medians `T(n) ≤ T(n/5) + T(7n/10) + O(n) = Θ(n)` | Groups of 5; `1/5 + 7/10 < 1` |
| Quickselect expected `Θ(n)`, worst `Θ(n²)` | Random pivot; one-sided recursion |
| Catalan number is not a D&C time | It counts parenthesisations; matrix-chain *ordering* is the cubic DP |
