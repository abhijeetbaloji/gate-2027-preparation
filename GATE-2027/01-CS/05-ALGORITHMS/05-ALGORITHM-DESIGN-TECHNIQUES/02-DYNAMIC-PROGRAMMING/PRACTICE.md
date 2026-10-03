# Dynamic Programming — Practice

These are practice questions, not GATE questions.

### Level 1 — Concept

**1.** Which two properties does a DP problem need, and which one does mergesort lack?

**2.** Why is naive Fibonacci exponential even though the closed recurrence mentions only `n`?

**3.** Write the 0/1 knapsack transition and point at the index that forbids a second copy.

**4.** LCS: what do you do when `X[i] ≠ Y[j]`?

**5.** Why is `Θ(n W)` called pseudo-polynomial?

### Level 2 — Standard

**6.** 0/1 knapsack, capacity 5, items `(2, 3), (3, 4), (4, 5)` as `(weight, value)`. Optimum?

**7.** Minimum coins for amount 6 with denominations 1, 3, 4.

**8.** LCS length of `ABCD` and `ACBD`?

**9.** Edit distance between `CAT` and `CAR`, with match 0 and insert, delete, substitute 1.

**10.** Matrix dimensions `p = (2, 3, 4, 2)`. Minimum multiplication cost?

### Level 3 — Multi-step

**11.** LIS lengths ending at each index of `[3, 1, 2, 1, 8]`, and the answer.

**12.** Run the tail method on `[3, 1, 2, 0]`. What is `T` at the end, and why is `T` not a subsequence you can read off in index order?

**13.** Subset-sum target 5 on `{2, 3, 4}`. Which sums are reachable?

**14.** A rod of length 4, prices `p[1]=1, p[2]=5, p[3]=8, p[4]=9`. Best revenue?

**15.** Count the parenthesisations of 4 matrices (3 multiplications). You do not need the costs. Then state the DP time as a function of the number of matrices `n`.

### Level 4 — Trap-based

**16.** A 1D knapsack array is updated from low capacity to high, and each item is considered once in that upward sweep. Which problem did you solve?

**17.** Someone computes LCS by adding 1 on a match and otherwise copying the diagonal. Give two strings of length 2 where this is wrong.

**18.** Edit distance of `A` and `A` is reported as 1. What cost was mis-assigned?

**19.** “Matrix chain is `O(n^{2.8})` by Strassen.” What are the two different problems?

**20.** Longest simple path in an undirected graph with positive weights is solved by “Dijkstra but maximising”. What fails?

### Level 5 — Challenge

**21.** Argue the LCS match case: if `X[i] = Y[j]`, then `L[i][j] = L[i−1][j−1] + 1`.

**22.** Why does filling a 0/1 knapsack row from `x = W` downward to `w_i` allow one array instead of two?

**23.** Derive the matrix-chain multiplication cost `p[i−1] · p[k] · p[j]` from the dimensions of the two partial products.

**24.** Bellman–Ford’s state is “at most `k` edges”. Why do `V − 1` rounds finish all simple shortest paths when there is no negative cycle?

**25.** Show a three-item 0/1 instance where sorting by `v/w` and taking the prefix that fits is not optimal. Use capacity 50 and items `(10, 60), (20, 100), (30, 120)`.

---

## Answers and explanations

**1.** Optimal substructure and overlapping subproblems. Mergesort has optimal substructure of a sort (sorted halves make a sorted merge) but the two halves are disjoint, so there is nothing to memoize for a speed-up.

**2.** Each call makes two smaller calls, and the subproblems overlap. The number of leaves is `Θ(φ^n)` unless results are stored.

**3.** `dp[i][x] = max(dp[i−1][x], dp[i−1][x−w_i] + v_i)` when the item fits. Both branches use `i−1`, so item `i` is not available again.

**4.** `L[i][j] = max(L[i−1][j], L[i][j−1])`. Do not add 1, and do not jump straight to the diagonal as the only option.

**5.** The table has `W + 1` columns. `W` may be exponential in the number of bits used to write it. The algorithm is polynomial in the numeric value of `W`, not necessarily in the input length.

**6.** 7, from weights 2 and 3. The weight-4 item alone is worth 5.

**7.** 2, via 3 + 3. Greedy 4 + 1 + 1 uses 3.

**8.** 3. One LCS is `ABD`. `ACD` is another. `ABCD` is not a subsequence of `ACBD` because `B` would have to appear after `C` and also in an order `A,B,C,D`; `ACBD` cannot provide both `B` before `C` and `C` before `B`. Length is not 4.

**9.** 1. Substitute `T` → `R`.

**10.** 36. `(2×3)(3×4)` costs 24, times `(4×2)` costs 16, total 40. `(3×4)(4×2)` costs 24, times the leading `2×3` costs 12, total 36.

**11.** Lengths `1, 1, 2, 1, 3`. Answer 3.

**12.** `3` → tails `[3]`. `1` replaces 3 → `[1]`. `2` extends → `[1, 2]`. `0` replaces 1 → `[0, 2]`. Length 2. `[0, 2]` is not a subsequence in that left-to-right index order: 0 sits after 2 in the array.

**13.** `0, 2, 3, 4, 5` (2+3), and `2+3+4=9` which is above the target. Not 1. Reachable up to 5: 0, 2, 3, 4, 5. Yes 5 = 2+3.

**14.** Cut into two rods of length 2: revenue `5 + 5 = 10`. The whole rod sells for 9. A length-3 plus a length-1 sells for 9. Best is 10.

**15.** Four matrices have three ways? Catalan `C_3 = 5`. The number of ways to parenthesise `n` matrices is `C_{n−1}`. For `n = 4`, `C_3 = 5`. DP time is `Θ(n³)`, not proportional to the Catalan number.

**16.** Unbounded knapsack. After placing the item at capacity `w`, a later cell `2w` in the same sweep already sees that updated cell and can take the item again.

**17.** `AB` and `BA`. True LCS length is 1. Copying the diagonal on the mismatch of the second characters, after a failed first pair, stays 0 if you also fail to take max(up, left). Even the pair `AA` and `BA`: position of the second `A` matches. A clean counterexample for “always copy diagonal on mismatch”: strings `AB`, `BA`. Correct `L[2][2] = max(L[1][2], L[2][1])`. If those borders were built properly, `L[1][2]` (prefix `A` vs `BA`) is 1 and `L[2][1]` (`AB` vs `B`) is 1, so the answer is 1. The diagonal `L[1][1]` (`A` vs `B`) is 0. Copying the diagonal yields 0, which is wrong.

**18.** The matching `A` was charged as a substitution. A match costs 0, so the distance is 0.

**19.** Strassen multiplies two `n × n` matrices in `O(n^{log2 7})` arithmetic operations. Matrix chain chooses the parenthesisation of a product of many rectangular matrices and is `Θ(n³)` in the number of matrices.

**20.** The longest simple path does not stay optimal when you append an edge: the “longest so far” may have used the vertices you need next, and avoiding cycles breaks the splicing argument. With cycles the problem is NP-hard. Dijkstra’s proof also uses non-negative weights to *minimise*, and the finalise-closest step is false for a maximum.

**21.** Any common subsequence either does not use `X[i]`, or does not use `Y[j]`, or uses both. If it uses both, those characters can be placed at the end because they are equal and are the last characters of the prefixes, and the preceding part is a common subsequence of the shorter prefixes. So the length is at least `L[i−1][j−1] + 1`. It is at most that, because deleting the last matched character from an LCS of the two prefixes yields a common subsequence of the shorter prefixes. The mismatch cases are not needed for this direction.

**22.** When you consider capacity `x`, the cell `x − w_i` has not yet been updated by item `i` if you walk downward. It still holds the previous item’s value, which is exactly `dp[i−1][x − w_i]`. Walking upward would read a cell item `i` has already updated.

**23.** The product of matrices `i..k` has dimensions `p[i−1] × p[k]`, because matrix `i` has `p[i−1]` rows and matrix `k` has `p[k]` columns. The product of matrices `k+1..j` has dimensions `p[k] × p[j]`. Multiplying a `p[i−1] × p[k]` matrix by a `p[k] × p[j]` matrix costs `p[i−1] · p[k] · p[j]`.

**24.** A simple path has at most `V − 1` edges. If a shortest path repeated a vertex, the cycle between the visits would have negative weight (otherwise you could delete it). With no negative cycle, some shortest path is simple, so it is discovered by round `V − 1`.

**25.** Ratio order is 6, 5, 4. The feasible prefix is the first two items, value 160, weight 30. Items 2 and 3 weigh 50 and are worth 220.
