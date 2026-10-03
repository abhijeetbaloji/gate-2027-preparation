# Divide and Conquer — Revision

## Pattern

Divide into smaller independent pieces, solve, combine. No table, because the pieces do not overlap. Time = the recurrence.

## Bounds

| Algorithm | Recurrence | Time | Worst extra space |
|-----------|------------|------|-------------------|
| Merge sort | `2T(n/2)+Θ(n)` | `Θ(n log n)` all cases | `Θ(n)` buffer |
| Quicksort balanced | same | `Θ(n log n)` | `Θ(log n)` stack |
| Quicksort degenerate | `T(n−1)+Θ(n)` | `Θ(n²)` | `Θ(n)` stack |
| Binary search | `T(n/2)+Θ(1)` | `Θ(log n)` | `Θ(1)` iterative |
| Inversions | merge sort | `Θ(n log n)` | `Θ(n)` |
| Max subarray D&C | `2T(n/2)+Θ(n)` | `Θ(n log n)` | `Θ(log n)` stack |
| Kadane | one pass | `Θ(n)` | `Θ(1)` |
| Closest pair, y merged | `2T(n/2)+Θ(n)` | `Θ(n log n)` | `Θ(n)` |
| Closest pair, re-sort y | `2T(n/2)+Θ(n log n)` | `Θ(n log² n)` | `Θ(n)` |
| Karatsuba | `3T(n/2)+Θ(n)` | `Θ(n^{log2 3})` | polynomial |
| Strassen | `7T(n/2)+Θ(n²)` | `Θ(n^{log2 7})` | polynomial |
| Quickselect | one side | expected `Θ(n)`, worst `Θ(n²)` | `Θ(n)` worst stack |
| Median of medians | `T(n/5)+T(7n/10)+O(n)` | worst `Θ(n)` | — |

## Why

- Case 2: every level costs `n`, `log n` levels.
- Bad quicksort: the level costs form `n + (n−1) + …`.
- Strassen/Karatsuba: fewer subproblems than the naive split, exponent `log_b a`.
- Strip: `O(1)` checks per point, not all pairs.

## Not this technique

- Matrix-chain order: DP, `Θ(n³)`, Catalan count of shapes.
- 0/1 knapsack, LCS: overlapping, so DP.
- Activity selection: greedy.

## Traps

- Merge sort answered `Θ(n)`.
- Master theorem on `T(n−1)` or on `n/3` with `2n/3`.
- Strassen confused with matrix chain.
- Quickselect worst case called linear.
- Both halves of binary search “solved”.
