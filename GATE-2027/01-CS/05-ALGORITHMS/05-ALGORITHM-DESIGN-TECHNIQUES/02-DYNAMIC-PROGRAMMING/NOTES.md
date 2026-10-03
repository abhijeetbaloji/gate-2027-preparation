# Dynamic Programming — Learning Notes

Dynamic programming solves a problem by solving smaller versions of the same problem and storing the answers. It applies when those smaller versions **overlap** and when an optimal solution is built from optimal solutions of the pieces. Greedy keeps only one piece. Divide-and-conquer also splits, but its subproblems are disjoint, so it does not bother with a table.

---

## 1. The two properties

**Optimal substructure.** An optimal solution contains optimal solutions of subproblems. If a shortest path from `s` to `t` goes through `u`, then the part from `s` to `u` is a shortest path. If it were not, you could splice in a better `s`-to-`u` path and improve the original. This is why shortest paths, knapsack, and matrix chain have DP formulations.

**Where it fails.** Longest *simple* path does not have this property in a graph with cycles: the longest simple path from `s` to `u` may use vertices you needed for the continuation, so you cannot splice freely. Unrestricted longest paths are NP-hard. Do not invent a DP on vertex subsets unless the subset is the state and you accept `2^V` time.

**Overlapping subproblems.** The recursion tree repeats the same pair `(i, w)` or the same index. Fibonacci is the picture: `F(n)` calls `F(n−1)` and `F(n−2)`, and those both call `F(n−3)`. A plain recursion does an exponential amount of repeated work. A table turns it into linear work.

Divide-and-conquer mergesort does not overlap: the left half and the right half are disjoint. Memoising mergesort does not change the `Θ(n log n)` bound. Memoising Fibonacci changes `Θ(φ^n)` calls into `Θ(n)` additions.

**Why both are required.** Optimal substructure says the recurrence is *correct*. Overlap says the table is *faster* than raw recursion. A problem can have one and not the other.

---

## 2. How a state is chosen

Write a sentence of the form: “`dp(state)` is the best value of *this* subproblem.” The state must be small enough to store, and rich enough that the transition does not need to look at the original decisions, only at smaller states.

A practical checklist:

1. What is the input prefix, suffix, or capacity still unused? That is the usual state.
2. What choice is made last (or first)? The transition tries each legal choice and calls a smaller state.
3. What is the base case, when no choice remains?
4. In which order can you fill the table so that every dependency is already known? That order is the iteration order. If you cannot find one, the recurrence has a cycle and this DP is wrong (or you need a different state).

**Memoisation** is the recursive form plus a cache. Compute `dp(s)` by looking up `s` first. **Tabulation** fills a table in dependency order and never recurses. Both compute the same recurrence. Memoisation skips states that the original input never asks for. Tabulation makes the order and the space obvious, which is what a complexity question wants.

**Reconstruction.** Store the argmax (the choice that won) beside the value, or recompute the choice by testing which transition matches the stored value. The value alone is not the solution if the question asks for the items or the alignment.

---

## 3. Fibonacci, as the pattern

**Definition.** `F(0) = 0`, `F(1) = 1`, `F(n) = F(n−1) + F(n−2)`.

**Why the naive recursion is exponential.** The recursion tree is a full binary tree of depth `n` in the worst branch, and the number of leaves is `F(n)` itself, which grows as `Θ(φ^n)` with `φ = (1+√5)/2 ≈ 1.618`.

**Why the DP is linear.** Each state `0..n` is computed once, from the previous two, in `Θ(1)` time. Time `Θ(n)`. If you keep only the last two numbers, auxiliary space is `Θ(1)`; the full table is `Θ(n)`.

| Version | Time | Auxiliary space |
|---------|------|-----------------|
| Naive recursion | `Θ(φ^n)` | `Θ(n)` stack |
| Memoised or table | `Θ(n)` | `Θ(n)`, or `Θ(1)` rolling |

There is no better or worse input: `n` fixes the work. Best, average, and worst coincide.

**GATE trap.** Calling the recursive tree “DP” because it uses a recurrence. DP includes the storage. Without storage it is just a slow recursion.

---

## 4. 0/1 knapsack

**What it is.** Each item is taken once or not at all. Capacity `W`. Item `i` has weight `w_i` and value `v_i`. Maximise value without exceeding `W`.

**State.** `dp[i][x]` = maximum value using only the first `i` items, with capacity exactly the budget `x` (or at most `x`; both work if you are careful). The “at most `x`” version:

```
dp[0][x] = 0
dp[i][x] = dp[i−1][x]                         if w_i > x
dp[i][x] = max(dp[i−1][x], dp[i−1][x−w_i] + v_i)   otherwise
```

**Why this transition.** The optimal packing of the first `i` items either skips item `i`, in which case it equals the optimum on `i−1` items with the same capacity, or it takes item `i`, in which case the remaining capacity `x − w_i` is packed optimally with the first `i−1` items. Those are the only two legal choices. The `i−1` in the “take” branch is what makes the item 0/1: you cannot take it twice.

**Why greedy ratio fails.** See the greedy notes. Capacity 50, weights 10, 20, 30, values 60, 100, 120. DP finds 220. Ratio order without fractions finds 160.

**Example.** Capacity 5. Items `(w, v) = (2, 3), (3, 4), (4, 5)`.

Fill by increasing `i`. The optimum is 7, from the first two items (weight 5). The single item of value 5 is worse. A hand trace of the last row is enough in an exam if `W` is small; the recurrence is what you write if the question asks why.

**Complexity.**

| | Bound | Why |
|--|-------|-----|
| Time | `Θ(n W)` | One constant-time cell per item per capacity |
| Space | `Θ(n W)`, or `Θ(W)` | A row depends only on the previous row. Rolling two arrays, or one array filled *downward* in `x`, keeps `Θ(W)`. Filling one array upward reuses the same item twice and solves the unbounded problem by mistake |

Best, average, and worst are the same: every cell is filled. The bound is **pseudo-polynomial**. It is polynomial in the numeric value `W`, not in the bit length of `W`. If `W` is exponential in the input length, this DP is not a polynomial-time algorithm. 0/1 knapsack is NP-hard, so that limitation is expected. When `W` is small, the DP is the method to use.

**Unbounded knapsack** (unlimited copies) changes one index:

```
dp[x] = max over items with w_i ≤ x of  (dp[x − w_i] + v_i)
```

or, in the two-dimensional form, the “take” branch calls `dp[i][x − w_i]` with the *same* `i`. Rod cutting and coin-change value maximisation are this pattern.

---

## 5. Subset sum

**State.** `dp[i][s]` is true if a subset of the first `i` numbers sums to `s`.

```
dp[i][s] = dp[i−1][s]  or  dp[i−1][s − a_i]   (the second only if s ≥ a_i)
```

**Complexity.** `Θ(n · Σ)` time, where `Σ` is the target or the total sum. Space `Θ(Σ)` with a rolling boolean array, updated downward so each number is used once.

**Partition.** An array can be split into two subsets of equal sum if and only if the total is even and subset-sum hits `total/2`.

**GATE observation.** This is 0/1 knapsack with every value equal to its weight, and you only care whether value `Σ/2` is reachable. Do not build a numeric knapsack if a boolean row is enough.

---

## 6. Coin change (minimum number of coins)

**State.** `C[a]` = fewest coins that sum to `a`. `C[0] = 0`. `C[a] = ∞` if `a` is impossible so far.

```
C[a] = 1 + min over denominations d ≤ a of C[a − d]
```

**Why it is unbounded knapsack.** Each denomination may be used many times, so the transition stays on the same set of coins and only reduces the amount.

**Example.** Denominations 1, 3, 4. Amount 6.

| a | 0 | 1 | 2 | 3 | 4 | 5 | 6 |
|---|---|---|---|---|---|---|---|
| C | 0 | 1 | 2 | 1 | 1 | 2 | 2 |

`C[6] = 2` (3+3), not the greedy 3. The DP tries every last coin; greedy locks in 4.

**Complexity.** `Θ(k A)` time, `Θ(A)` space. Pseudo-polynomial in the amount. Same best, average, and worst: the loops do not depend on which answer wins.

**The counting version** (“how many ways”) replaces `min` and `+1` by a sum of the ways to make `a − d`. Order the loops carefully: iterating coins outside and amount inside counts combinations; iterating amount outside counts permutations. GATE distinguishes these.

---

## 7. Longest common subsequence

**What it is.** A subsequence need not be contiguous. Given strings `X[1..m]` and `Y[1..n]`, find the longest string that is a subsequence of both. (A substring is contiguous; that is a different DP, often on matching spans.)

**State.** `L[i][j]` = LCS length of the prefixes `X[1..i]` and `Y[1..j]`.

```
L[0][j] = L[i][0] = 0
L[i][j] = L[i−1][j−1] + 1                  if X[i] = Y[j]
L[i][j] = max(L[i−1][j], L[i][j−1])        otherwise
```

**Why the recurrence is correct.** If the last characters match, some LCS can end with that character: take an LCS of the prefixes before them and append the character. If they do not match, the last character of `X` is unused or the last character of `Y` is unused (or both). The better of the two shorter prefixes covers those cases. Using both shortenings when they *do* match would drop a useful character.

**Example.** `X = ABCD`, `Y = ACBD`.

Match A. Then B does not match C. Eventually the LCS length is 3, for example `ABD` or `ACD`. The table is 5 by 5 with a zero border; filling it is mechanical once the recurrence is fixed.

**Complexity.** `Θ(m n)` time. Space `Θ(m n)`, or `Θ(min(m, n))` if only the length is required, because a row depends only on the previous row. Reconstructing the actual string from a rolling row needs extra care; keep the full table or the parent pointers if the string is required.

**Related.** Edit distance (next) uses the same grid with three moves. Longest common substring resets to 0 on a mismatch instead of taking a max of the neighbours, because contiguity breaks.

---

## 8. Edit distance

**What it is.** Minimum insertions, deletions, and substitutions that turn `X` into `Y`. Each operation costs 1 unless the question says otherwise.

**State.** `E[i][j]` = distance between prefixes `X[1..i]` and `Y[1..j]`.

```
E[i][0] = i          delete i characters
E[0][j] = j          insert j characters
E[i][j] = E[i−1][j−1]                         if X[i] = Y[j]
E[i][j] = 1 + min(
            E[i−1][j],      delete X[i]
            E[i][j−1],      insert Y[j]
            E[i−1][j−1]     substitute
          )                                     if they differ
```

**Why three branches.** The last operation on an optimal alignment is one of those three, and the preceding alignment is optimal for the remaining prefixes. Substitution (or a free match) consumes one character from each side. Insert consumes only from `Y`. Delete consumes only from `X`.

**Complexity.** `Θ(m n)` time and `Θ(m n)` space, or `Θ(min(m, n))` space for the number alone. All cases are equal.

**GATE trap.** Charging a substitution as two operations (delete plus insert) when the problem allows a direct replace of cost 1. Read the cost list. Also, matching characters cost 0, not 1.

---

## 9. Longest increasing subsequence

**Quadratic DP.** `L[i]` = length of a longest increasing subsequence that **ends at index `i`**.

```
L[i] = 1 + max{ L[j] : j < i and A[j] < A[i] }    (or 1 if no such j)
```

Answer is `max_i L[i]`. Time `Θ(n²)`, space `Θ(n)`. The state is “ending at `i`” because the next append decision only needs the last value, and storing that last value as the index avoids an extra dimension.

**Example.** `A = [3, 1, 2, 1, 8]`.

- Index 0, value 3: length 1.
- Index 1, value 1: length 1.
- Index 2, value 2: extends the 1, length 2.
- Index 3, value 1: length 1.
- Index 4, value 8: extends the length-2 subsequence, length 3.

Answer 3. One such subsequence is `1, 2, 8`.

**`O(n log n)` method.** Maintain an array `T` where `T[len]` is the smallest possible tail of any increasing subsequence of length `len` seen so far. For each new key, binary-search the first tail that is `≥` the key (or `>` if duplicates are forbidden) and replace it. A smaller tail can only help future extensions, so the invariant holds. The length of `T` is the LIS length. This does **not** store the subsequence in `T` itself; `T` is a tail table, not the subsequence. Reconstruct with parent pointers if the sequence is required.

Time `Θ(n log n)` because each of the `n` keys does a binary search. Space `Θ(n)`. This beats the comparison-based feel of `Θ(n²)` and is the bound to quote when the question allows it. The quadratic DP is still the one to derive first.

**Strict versus non-decreasing.** `<` in the test gives strictly increasing. `≤` gives non-decreasing. The `O(n log n)` search direction must match.

---

## 10. Matrix chain multiplication

**What it is.** Matrices `M_i` has dimensions `p_{i−1} × p_i`. The product `M_1 M_2 … M_n` is associative. The parenthesisation does not change the product, but it changes the number of scalar multiplications. Choose the parenthesisation of minimum cost.

**Why a local greedy fails.** Multiplying the cheapest adjacent pair first can force an expensive product later. The optimal split of a chain is not always the cheapest split of a smaller pair chosen in isolation without looking at both sides. The number of parenthesisations is the Catalan number `C_{n−1}`, which is exponential, so brute force is not the exam method.

**State.** `dp[i][j]` = minimum cost to multiply the chain from matrix `i` through matrix `j`.

```
dp[i][i] = 0
dp[i][j] = min over i ≤ k < j of
           dp[i][k] + dp[k+1][j] + p[i−1] · p[k] · p[j]
```

**Why the last term.** The split after matrix `k` produces a matrix of size `p_{i−1} × p_k` and a matrix of size `p_k × p_j`. Multiplying those two costs `p_{i−1} · p_k · p_j` scalar multiplications, on top of the optimal costs of building each side.

**Order of filling.** By increasing chain length `j − i`. A cell of length `ℓ` depends only on shorter chains.

**Example.** Dimensions `(p) = (2, 3, 4, 2)`, so three matrices: `2×3`, `3×4`, `4×2`.

- Cost of `(M1 M2)` then times `M3`: `(2·3·4) + (2·4·2) = 24 + 16 = 40`.
- Cost of `M1` times `(M2 M3)`: `(3·4·2) + (2·3·2) = 24 + 12 = 36`.

Optimum 36. The DP tries both splits; here `n` is small enough to see both.

**Complexity.** `Θ(n²)` states, each tries `O(n)` splits, so time `Θ(n³)`. Space `Θ(n²)`. All cases are equal: every split is examined.

**GATE traps.**

- The dimension index: the cost uses `p[i−1]`, not `p[i]`, because matrix `i` starts at dimension `p_{i−1}`.
- Counting matrices versus counting dimension entries. `n` matrices means `n + 1` dimensions and `n − 1` possible split positions inside a full product.
- Confusing this cubic DP with Strassen’s `O(n^{log2 7})` matrix-multiply algorithm. Strassen multiplies two matrices. Matrix chain decides the order of many multiplications. They are different problems.

---

## 11. Rod cutting

A rod of length `n`, price `p[ℓ]` for a piece of length `ℓ`. Cut into pieces to maximise revenue. Unlimited use of each length.

```
R[0] = 0
R[x] = max over ℓ = 1..x of  (p[ℓ] + R[x − ℓ])
```

Time `Θ(n²)`, space `Θ(n)`. It is unbounded knapsack with weight = length and value = price. A greedy “cut the best price-per-length first” fails for the same reason coin greedy fails.

---

## 12. Weighted interval scheduling, in outline

Sort intervals by finish time. Let `dp[i]` be the best value using the first `i` intervals in that order. Let `pred[i]` be the rightmost interval that finishes before `i` starts (binary search).

```
dp[i] = max(dp[i−1],  value[i] + dp[pred[i]])
```

Time `Θ(n log n)` because of the sort and the binary searches. This is the weighted version that earliest-finish greedy does not solve. Unweighted activity selection is the special case where every value is 1 and the greedy rule already matches the DP.

---

## 13. Shortest paths as DP

**Bellman–Ford.** `D[k][v]` = shortest-path weight from the source to `v` using at most `k` edges.

```
D[0][s] = 0,  D[0][v] = ∞ for v ≠ s
D[k][v] = min( D[k−1][v],  min over edges u→v of D[k−1][u] + w(u,v) )
```

After `V − 1` rounds, a simple path would have been found if no negative cycle exists. One more round that still improves a distance proves a negative cycle is reachable. Time `Θ(V E)`. The algorithm is DP on the number of edges, not a greedy finalisation. Details and the comparison with Dijkstra are in the shortest-path notes.

**Floyd–Warshall.** `D_k[i][j]` = shortest path from `i` to `j` that may use intermediate vertices from `{1, …, k}` only.

```
D_k[i][j] = min(D_{k−1}[i][j], D_{k−1}[i][k] + D_{k−1}[k][j])
```

Time `Θ(V³)`, space `Θ(V²)`. The state is “which intermediate vertices are allowed”, which is why adding vertex `k` is the only new choice.

---

## 14. Designing the state on a new problem

Ask these in order.

1. **Is the objective a combination of optimal pieces?** If splicing an optimal piece can destroy feasibility (simple paths, arbitrary subsets with side constraints), enlarge the state until feasibility is encoded, or stop and say the problem is not this kind of DP.
2. **What does the last decision look like?** Take or skip an item, match or edit a character, split a chain at `k`, place a coin, use one more edge.
3. **What must the state remember so that the last decision is legal?** Remaining capacity, prefix lengths, last index of an increasing subsequence, set of allowed intermediate vertices.
4. **Count the states times the work per state.** That product is the time. If it is exponential in a numeric parameter that is given in binary, say pseudo-polynomial.
5. **Do subproblems repeat?** If the recursion tree is already disjoint, you have divide-and-conquer, and a table will not improve the bound.

---

## 15. Comparison

| Method | Tries all local choices? | Stores subproblems? | Typical reason |
|--------|--------------------------|---------------------|----------------|
| Greedy | No, one rule | No | A proof says the other choices are unnecessary |
| Divide-and-conquer | Yes, inside each piece | No, pieces do not overlap | Merge sort, closest pair |
| DP | Yes | Yes | Overlap plus optimal substructure |
| Brute force | Yes | No | Subproblems do not repeat, or `n` is tiny |

---

## 16. Common GATE traps

1. Unbounded transition (`dp[i][x − w]`) used for a 0/1 item, so the item is taken many times.
2. Rolling knapsack array updated in the wrong direction.
3. LCS mismatch branch written as `L[i−1][j−1]` instead of the max of the two neighbours.
4. Edit distance charging 1 for a matching character.
5. LIS tail array read as if it were the subsequence.
6. Matrix-chain cost `p[i] · p[k] · p[j]` with the wrong dimension index.
7. Matrix chain confused with Strassen.
8. Coin DP and coin greedy given the same answer on a non-canonical set.
9. “DP is always polynomial.” Knapsack is pseudo-polynomial. Some DPs are `Θ(2^n n)` over subsets and are still exponential.
10. Longest simple path forced into a shortest-path recurrence.
11. Fibonacci recursion called `O(n)` with no memo.
12. Space of the full table quoted when only two rows are live, or the reverse, when parent pointers are required and were not stored.
