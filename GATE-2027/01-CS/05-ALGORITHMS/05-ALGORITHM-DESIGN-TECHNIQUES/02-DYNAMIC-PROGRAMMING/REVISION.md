# Dynamic Programming — Revision

## When

Optimal substructure and overlapping subproblems. Greedy skips the other choices. Divide-and-conquer has no overlap to store.

## Core recurrences

| Problem | Recurrence idea | Time | Space |
|---------|-----------------|------|-------|
| Fibonacci table | Sum of the previous two | Θ(n) | Θ(1) rolling |
| 0/1 knapsack | Skip, or take from the **previous** item row | Θ(nW) | Θ(W) rolling downward |
| Unbounded / rod / min coins | Same items, smaller capacity or amount | Θ(nW) or Θ(kA) | Θ(W) or Θ(A) |
| Subset sum | Boolean, previous row | Θ(n · target) | Θ(target) |
| LCS | Match: diagonal+1. Else max(up, left) | Θ(mn) | Θ(min(m,n)) for length |
| Edit distance | Match 0; insert, delete, substitute +1 | Θ(mn) | Θ(min(m,n)) for the number |
| LIS | Ends at i, or tail array + binary search | Θ(n²) or Θ(n log n) | Θ(n) |
| Matrix chain | Best split k, plus `p[i−1]·p[k]·p[j]` | Θ(n³) | Θ(n²) |
| Floyd–Warshall | Allow one new intermediate k | Θ(V³) | Θ(V²) |
| Bellman–Ford | At most k edges | Θ(VE) | Θ(V) |

## Facts

- Pseudo-polynomial: polynomial in the number `W`, not in `log W`.
- Catalan `C_{n−1}` counts matrix parenthesisations; the DP is cubic.
- Strassen multiplies two matrices. It does not choose a chain order.
- LIS tail array is not the subsequence.
- Longest simple path does not inherit shortest-path substructure.
- Coin DP and coin greedy disagree on denominations 1, 3, 4 and amount 6.

## Traps

- 1D knapsack updated upward → unbounded, not 0/1.
- LCS mismatch written on the diagonal.
- Edit cost 1 on a match.
- Matrix dimension off by one (`p[i]` versus `p[i−1]`).
- Naive Fibonacci called linear.
