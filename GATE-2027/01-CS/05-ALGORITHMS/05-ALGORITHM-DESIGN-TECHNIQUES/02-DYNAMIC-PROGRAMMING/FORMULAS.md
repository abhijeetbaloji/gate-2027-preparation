# Dynamic Programming — Formulas

| Result | When it applies |
|--------|-----------------|
| Fibonacci memo or table `Θ(n)` time | Each state `0..n` once. Naive recursion is `Θ(φ^n)` |
| 0/1 knapsack `dp[i][x] = max(dp[i−1][x], dp[i−1][x−w_i] + v_i)` | Item used at most once. Time `Θ(n W)`, space `Θ(W)` if the previous row is updated downward |
| Unbounded knapsack | “Take” branch uses the same item index, or a 1D recurrence on capacity. Rod cutting, unlimited coins |
| Subset sum `Θ(n · target)` | Boolean DP. Equal partition: target `total/2` when the total is even |
| Coin minimum `C[a] = 1 + min_d C[a−d]` | Unlimited coins. Time `Θ(k A)`. Not the same as greedy |
| LCS: match → diagonal `+ 1`; else max of up and left | Subsequence, not substring. Time `Θ(m n)` |
| Longest common substring | Reset length to 0 on a mismatch. Contiguous |
| Edit distance | Insert, delete, substitute cost 1; match cost 0. Time `Θ(m n)` |
| LIS ending at `i`: `Θ(n²)` | `L[i] = 1 + max L[j]` over `j < i`, `A[j] < A[i]` |
| LIS tails: `Θ(n log n)` | `T[len]` is the smallest tail of length `len`, updated by binary search. `T` is not the subsequence |
| Matrix chain `dp[i][j] = min_k dp[i][k] + dp[k+1][j] + p[i−1] p[k] p[j]` | `n` matrices, `n+1` dimensions. Time `Θ(n³)`, space `Θ(n²)`. Catalan number `C_{n−1}` counts parenthesisations, it is not the DP time |
| Rod cutting `Θ(n²)` | `R[x] = max_ℓ p[ℓ] + R[x−ℓ]` |
| Weighted intervals `Θ(n log n)` | Sort by finish; `dp[i] = max(dp[i−1], v_i + dp[pred[i]])` |
| Bellman–Ford `Θ(V E)` | DP by number of edges, `V − 1` rounds |
| Floyd–Warshall `Θ(V³)` | `D_k[i][j] = min(D_{k−1}[i][j], D_{k−1}[i][k] + D_{k−1}[k][j])` |
| Pseudo-polynomial | Time polynomial in the numeric value `W` or `A`, not necessarily in the number of input bits |
