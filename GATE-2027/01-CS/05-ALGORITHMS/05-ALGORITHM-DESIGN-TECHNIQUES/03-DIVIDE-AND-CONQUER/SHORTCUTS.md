# Divide and Conquer — Shortcuts

### Equal levels plus `log n` depth means `n log n`

**Shortcut.** If the recursion tree has `Θ(log n)` levels and each level does `Θ(n)` work, the solution is `Θ(n log n)`.

**Why it works.** That is Master case 2 for `T(n) = 2T(n/2) + Θ(n)`, and the same arithmetic for a tree whose longer branch is a constant-fraction shrink (`n/3` and `2n/3`).

**When to use.** Merge sort, inversions, a linear-combine closest pair, a crossing-midpoint subarray.

**Example.** Two subproblems of size `2n/3` and `n/3` still give `Θ(n)` per level and `Θ(log n)` depth.

**Limitation.** If the non-recursive work is `n²`, the root level dominates and there is no extra log. If only one subproblem is solved, the cost is a single path, not a full level of `n`.

---

### One empty side means a quadratic chain

**Shortcut.** `T(n) = T(n−1) + Θ(n)` is `Θ(n²)`. Fixed-endpoint quicksort on sorted data is this recurrence.

**Why it works.** The costs are `n + (n−1) + … + 1`.

**When to use.** The pivot rule is named and the input is sorted or reverse-sorted.

**Example.** Pivot = last element, array increasing. Each partition peels one key.

**Limitation.** A random pivot changes the recurrence to an expectation of `Θ(n log n)`. Do not quote `n²` for randomised quicksort except as a worst-case ceiling.

---

### Three multiplications, not four; seven blocks, not eight

**Shortcut.** Karatsuba replaces 4 half products by 3. Strassen replaces 8 block products by 7. Both beat the naive exponent because `log2 3 < 2` and `log2 7 < 3`.

**Why it works.** Master case 1: the leaf count `n^{log_b a}` dominates the polynomial combine cost.

**When to use.** “Better than `Θ(n²)` integer multiplication” or “better than `Θ(n³)` for one product of two square matrices”.

**Example.** `T(n) = 7T(n/2) + Θ(n²) = Θ(n^{log2 7})`.

**Limitation.** Matrix-chain parenthesisation is a different problem and stays `Θ(n³)` DP in the number of matrices. Strassen does not answer it.

---

### The strip is linear only with a constant window

**Shortcut.** After `δ` is known, each point in the closest-pair strip is compared with `O(1)` later points in y-order, not with the whole strip.

**Why it works.** Points inside one half are already at least `δ` apart, so they pack sparsely in the `δ`-by-`δ` squares of the strip.

**When to use.** Time of the combine step.

**Example.** A correct combine is `Θ(n)` and the recurrence is merge-sort’s.

**Limitation.** Sorting by y from scratch inside the combine makes that step `Θ(n log n)` and the total `Θ(n log² n)`. Checking all strip pairs is not the algorithm.

---

### Selection is linear only in the version you named

**Shortcut.** Randomised quickselect: expected `Θ(n)`, worst `Θ(n²)`. Median of medians: worst-case `Θ(n)`.

**Why it works.** A random good pivot shrinks the expected size geometrically. Groups of 5 force a 30% discard, and `1/5 + 7/10 < 1` sums to linear.

**When to use.** “`k`-th smallest” complexity options.

**Example.** Worst-case linear selection is the median-of-medians sentence, not the word “quickselect” alone.

**Limitation.** Using median-of-medians as every quicksort pivot gives worst-case `Θ(n log n)` sort, but the constant is large. The existence of the bound is the exam point, not a claim that library sort does this.
