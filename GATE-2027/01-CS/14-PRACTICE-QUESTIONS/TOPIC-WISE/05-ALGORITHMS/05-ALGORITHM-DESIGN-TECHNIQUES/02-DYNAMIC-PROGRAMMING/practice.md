# Dynamic Programming — Practice Questions

Original practice for GATE CS. These questions are not from any GATE paper. Attempt the questions before reading the solutions.

## Level 1 — Conceptual

## Q1 — MCQ

Fibonacci is defined by \(F(0) = 0\), \(F(1) = 1\), and \(F(n) = F(n-1) + F(n-2)\). Which statement is correct?

A. The plain recursion is dynamic programming, and it runs in \(\Theta(n)\) time.

B. The plain recursion performs \(\Theta(\varphi^n)\) additions, with \(\varphi = (1+\sqrt{5})/2\). Storing each value \(F(0), \ldots, F(n)\) once reduces the time to \(\Theta(n)\).

C. Memoisation does not change the exponential tree, because the recurrence itself is exponential.

D. The table uses \(\Theta(n^2)\) cells.

---

## Q2 — MSQ

Select all that apply.

A. Optimal substructure means an optimal solution contains optimal solutions of the subproblems that the recurrence glues together.

B. Overlapping subproblems are the reason a table is faster than a recursion that recomputes the same state.

C. Merge sort should be memoised, because its two halves overlap.

D. A recurrence can be a correct description of the optimum and still be exponential if the answers are not stored.

---

## Q3 — MCQ

In the 0/1 knapsack table, \(dp[i][x]\) is the best value using only the first \(i\) items and capacity \(x\). Item \(i\) has weight \(w_i\) and value \(v_i\), and \(w_i \le x\). The correct transition is

A. \(dp[i][x] = \max\bigl(dp[i][x-w_i],\ dp[i][x-w_i] + v_i\bigr)\)

B. \(dp[i][x] = \max\bigl(dp[i-1][x],\ dp[i-1][x-w_i] + v_i\bigr)\)

C. \(dp[i][x] = dp[i-1][x] + v_i\)

D. \(dp[i][x] = \max\bigl(dp[i-1][x],\ dp[i][x-w_i] + v_i\bigr)\)

---

## Q4 — NAT

A 0/1 knapsack has capacity 7. The items, in order, are \((w, v) = (2, 3),\ (3, 4),\ (4, 5),\ (5, 7)\). Each item may be taken at most once. What is the maximum value?

---

## Q5 — MCQ

Longest common subsequence lengths \(L[i][j]\) are computed on prefixes. When the characters \(X[i]\) and \(Y[j]\) differ, the cell is filled by

A. \(L[i-1][j-1] + 1\)

B. \(\max(L[i-1][j],\ L[i][j-1])\)

C. \(0\), because a mismatch ends every common subsequence

D. \(L[i-1][j-1]\), with no other neighbour consulted

---

## Level 2 — Standard GATE Style

## Q6 — NAT

What is the length of a longest common subsequence of \(X = \texttt{BEAR}\) and \(Y = \texttt{BARE}\)? Characters need not be contiguous.

---

## Q7 — NAT

The array is \([6, 2, 5, 1, 7, 4, 8]\). A subsequence must be strictly increasing. Using \(L[i] = 1 + \max\{L[j] : j < i,\ A[j] < A[i]\}\), with the maximum over the empty set taken to be 0, what is \(\max_i L[i]\)?

---

## Q8 — NAT

Four dimension entries \(p = (4, 2, 5, 3)\) describe three matrices, of sizes \(4\times 2\), \(2\times 5\), and \(5\times 3\). The matrix-chain cost of a split is \(dp[i][k] + dp[k+1][j] + p_{i}\, p_{k+1}\, p_{j+1}\) when dimensions are indexed so that matrix \(i\) (counting from 1) has dimensions \(p_{i-1}\times p_i\). What is the minimum number of scalar multiplications for the full product?

---

## Q9 — NAT

Denominations \(1, 4, 6\) may be used any number of times. The minimum number of coins that sum to 8 is computed by \(C[0] = 0\) and \(C[a] = 1 + \min_{d \le a} C[a-d]\). What is \(C[8]\)?

---

## Q10 — NAT

Edit distance charges 0 for a match and 1 for an insertion, a deletion, or a substitution. What is the edit distance from \(\texttt{PLAN}\) to \(\texttt{PANE}\)?

---

## Q11 — MSQ

Select all that apply.

A. Unlimited copies of an item, as in rod cutting or unbounded knapsack, take the transition that reads the same item set at the reduced capacity.

B. Filling a one-dimensional 0/1 knapsack array from low capacity toward high capacity lets the same item be used twice.

C. Subset-sum is 0/1 knapsack with every value equal to its weight, stored as a Boolean reachable array.

D. The 0/1 take-branch must read the previous item’s row, or a one-dimensional array that has not yet been overwritten at the residual capacity.

---

## Level 3 — Multi-Step

## Q12 — NAT

A rod of length 4 has piece prices \(p_1 = 1\), \(p_2 = 5\), \(p_3 = 8\), \(p_4 = 9\). Any length may be used more than once. The optimum is \(R[0] = 0\) and \(R[x] = \max_{1 \le \ell \le x}(p_\ell + R[x-\ell])\). What is \(R[4]\)?

---

## Q13 — NAT

The number of combinations, not permutations, of coins that sum to 4, using denominations \(1\) and \(2\), is computed by iterating coins on the outside and amounts on the inside, adding the ways to make \(a - d\). How many combinations are there?

---

## Q14 — NAT

The set is \(\{2, 3, 5, 6\}\). Subset-sum Boolean DP marks every sum that a subset can form. What is the largest integer \(s \le 8\) that cannot be formed?

---

## Q15 — MCQ

Which distinction is correct?

A. Strassen’s algorithm, with \(T(n) = 7T(n/2) + \Theta(n^2) = \Theta(n^{\log_2 7})\), chooses the parenthesisation of a chain of many matrices.

B. Matrix-chain ordering is the \(\Theta(n^3)\) dynamic program over splits. Strassen multiplies two square matrices.

C. The Catalan number \(C_{n-1}\) is the running time of matrix-chain DP.

D. Both problems are solved by the same triple loop with \(k\) outermost.

---

## Q16 — MSQ

Select all that apply.

A. 0/1 knapsack in \(\Theta(nW)\) time is polynomial in the numeric value \(W\) and need not be polynomial in the number of bits of \(W\).

B. That dependence on the numeric value is called pseudo-polynomial.

C. Because a table is used, every dynamic program is polynomial in the bit length of its numeric parameters.

D. If only the length of an LCS is required, two rows suffice and the auxiliary space is \(\Theta(\min(m, n))\). Reconstructing one subsequence from those two rows, without parent information, is not immediate.

---

## Level 4 — Tricky / Trap-Based

## Q17 — MCQ

A one-dimensional array implements 0/1 knapsack. Item weights are positive. The capacity index \(x\) must be scanned

A. from \(w_i\) upward to \(W\), so that \(dp[x-w_i]\) is the value after the same item has already been considered at the smaller capacity

B. from \(W\) downward to \(w_i\), so that \(dp[x-w_i]\) still holds the previous item’s answer

C. in either direction; 0/1 and unbounded knapsack coincide on one array

D. only at \(x = W\), because smaller capacities cannot affect the answer

---

## Q18 — MSQ

Select all that apply. The array is \([6, 2, 5, 1, 7, 4, 8]\), and the \(O(n \log n)\) tail method stores in \(T[\ell]\) the smallest tail of a strictly increasing subsequence of length \(\ell\).

A. After the whole array is processed, the length of \(T\) is 4.

B. The final contents of \(T\), read left to right, are a subsequence of the input.

C. Longest common substring resets the length to 0 on a mismatch. Longest common subsequence does not.

D. A matching pair in edit distance adds 1 to the distance.

---

## Q19 — MCQ

Denominations \(1, 4, 6\) and amount 8 are solved once by largest-coin greedy and once by the coin DP of Q9. Which statement is correct?

A. Both return 2 coins, so greedy is safe on every denomination set.

B. Greedy returns 3 coins, by taking \(6 + 1 + 1\). The DP returns 2, by taking \(4 + 4\). Largest-first is not optimal for this set.

C. The DP returns 3, because it is required to try the largest coin first.

D. No combination sums to 8.

---

## Level 5 — Challenge

## Q20 — MCQ

Each activity has a value, and the objective is the maximum total value of a compatible set, not the maximum number of activities. Which statement is correct?

A. Earliest-finish greedy is optimal, because values do not affect the exchange.

B. Sort by finish time, let \(\mathrm{pred}[i]\) be the rightmost activity that finishes before \(i\) starts, and set \(dp[i] = \max(dp[i-1],\ v_i + dp[\mathrm{pred}[i]])\). With binary search for the predecessor, the time is \(\Theta(n \log n)\).

C. The unweighted earliest-finish scan already maximises an arbitrary value array.

D. The problem is the fractional knapsack ratio rule applied to interval length.

---

## Q21 — MSQ

Select all that apply.

A. A shortest path that passes through \(u\) is a shortest path to \(u\) plus a shortest path onward from \(u\). That substructure is why edge relaxation is valid.

B. A longest simple path that passes through \(u\) is always a longest simple path to \(u\) plus a longest simple continuation, even when the graph has cycles.

C. Bellman–Ford is dynamic programming on the number of edges: after \(k\) full relaxation rounds, distances are shortest-path weights among paths of at most \(k\) edges, if no negative cycle is feeding them.

D. Floyd–Warshall’s state allows one new intermediate vertex \(k\), and the \(k\) loop is outermost.

---

## Q22 — MCQ

Naive recursion for \(F(n)\) uses a recursion tree whose number of leaves is \(F(n)\) itself. A bottom-up loop stores only the previous two numbers. The auxiliary space of that loop, and the time, are

A. space \(\Theta(n)\), time \(\Theta(\varphi^n)\)

B. space \(\Theta(1)\), time \(\Theta(n)\)

C. space \(\Theta(n)\), time \(\Theta(n)\) only if the full table is allocated; the two-variable loop is not correct

D. space \(\Theta(1)\), time \(\Theta(1)\), because each addition is \(O(1)\) and there is no loop

## Answer Key

| Q | Type | Answer |
|---|------|--------|
| 1 | MCQ | B |
| 2 | MSQ | A, B, D |
| 3 | MCQ | B |
| 4 | NAT | 10 |
| 5 | MCQ | B |
| 6 | NAT | 3 |
| 7 | NAT | 4 |
| 8 | NAT | 54 |
| 9 | NAT | 2 |
| 10 | NAT | 2 |
| 11 | MSQ | A, B, C, D |
| 12 | NAT | 10 |
| 13 | NAT | 3 |
| 14 | NAT | 4 |
| 15 | MCQ | B |
| 16 | MSQ | A, B, D |
| 17 | MCQ | B |
| 18 | MSQ | A, C |
| 19 | MCQ | B |
| 20 | MCQ | B |
| 21 | MSQ | A, C, D |
| 22 | MCQ | B |

## Detailed Solutions

### Q1

Answer: B

Without storage, the two recursive calls both expand \(F(n-3)\) and then the same pattern repeats. The number of leaves of that tree is \(F(n)\), which grows as \(\Theta(\varphi^n)\). Dynamic programming is the recurrence plus a cache or a table. Each of the \(n+1\) states is then computed from the previous two in constant time, so the cost falls to \(\Theta(n)\). The full table is a one-dimensional array of length \(n+1\), not an \(n \times n\) table. Calling the bare recursion “DP” omits the storage that changes the complexity.

### Q2

Answer: A, B, D

Optimal substructure is the reason the recurrence’s value equals the true optimum: a worse piece could be replaced by a better piece. Overlap is the reason the table helps. Merge sort’s left and right halves are disjoint, so a cache never hits and the \(\Theta(n \log n)\) bound is unchanged. Fibonacci has both properties only after the answers are stored. The recurrence alone, however correct, still walks the exponential tree.

### Q3

Answer: B

The optimum on the first \(i\) items either skips item \(i\), which is \(dp[i-1][x]\), or takes it once, which adds \(v_i\) to an optimum on the first \(i-1\) items with capacity \(x - w_i\). The index \(i-1\) on the take branch is what forbids a second copy. Option (A) never looks at a smaller item set. Option (D) is the unbounded transition: the take branch may use item \(i\) again. Option (C) forces the item to be taken.

### Q4

Answer: 10

Rows are items, columns are capacities \(0\) through \(7\). Each take reads the previous row.

| \(i \backslash x\) | 0 | 1 | 2 | 3 | 4 | 5 | 6 | 7 |
|-------------------:|--:|--:|--:|--:|--:|--:|--:|--:|
| 0 items | 0 | 0 | 0 | 0 | 0 | 0 | 0 | 0 |
| \((2,3)\) | 0 | 0 | 3 | 3 | 3 | 3 | 3 | 3 |
| \((3,4)\) | 0 | 0 | 3 | 4 | 4 | 7 | 7 | 7 |
| \((4,5)\) | 0 | 0 | 3 | 4 | 5 | 7 | 8 | 9 |
| \((5,7)\) | 0 | 0 | 3 | 4 | 5 | 7 | 8 | 10 |

At capacity 7 the last row compares “skip the weight-5 item” (value 9, from the previous row) with “take it and use capacity 2” (value \(7 + 3 = 10\)). The maximum is 10, from the items of weights 2 and 5. Weights 3 and 4 also fill the knapsack and score only \(4+5 = 9\).

### Q5

Answer: B

If the last characters differ, no common subsequence uses both of them as its last character. The better of “drop the last character of \(X\)” and “drop the last character of \(Y\)” covers the three possibilities (drop \(X\), drop \(Y\), or drop both, which is included in either choice). The diagonal increment is legal only when the characters match. Resetting to 0 is the longest common *substring* rule, where contiguity has already been broken.

### Q6

Answer: 3

Prefixes of \(\texttt{BEAR}\) against prefixes of \(\texttt{BARE}\):

|  |  | B | A | R | E |
|--|--|--:|--:|--:|--:|
|  | 0 | 0 | 0 | 0 | 0 |
| B | 0 | 1 | 1 | 1 | 1 |
| E | 0 | 1 | 1 | 1 | 2 |
| A | 0 | 1 | 2 | 2 | 2 |
| R | 0 | 1 | 2 | 3 | 3 |

The length is 3. One common subsequence is \(\texttt{BAR}\): B, A, and R occur in that order in both strings. No common subsequence has length 4, because the table’s corner is 3. In particular \(\texttt{BEA}\) is not a subsequence of \(\texttt{BARE}\): after E, which is the last character of \(Y\), there is no A.

### Q7

Answer: 4

| Index \(i\) | 0 | 1 | 2 | 3 | 4 | 5 | 6 |
|-------------|--:|--:|--:|--:|--:|--:|--:|
| \(A[i]\) | 6 | 2 | 5 | 1 | 7 | 4 | 8 |
| \(L[i]\) | 1 | 1 | 2 | 1 | 3 | 2 | 4 |

The 5 extends the 2. The 7 extends the length-2 subsequence ending at 5. The 4 extends the 1, or the 2, but not the 5. The 8 extends the length-3 subsequence ending at 7. The answer is 4. One subsequence is \(2, 5, 7, 8\). The state “ending at \(i\)” is enough because an extension only needs the last value.

### Q8

Answer: 54

There are \(n = 3\) matrices and two full-product splits. Adjacent products first:

- \(M_1 M_2\) costs \(4 \cdot 2 \cdot 5 = 40\).
- \(M_2 M_3\) costs \(2 \cdot 5 \cdot 3 = 30\).

The full chain:

- \((M_1 M_2)M_3\) costs \(40 + 4 \cdot 5 \cdot 3 = 40 + 60 = 100\).
- \(M_1(M_2 M_3)\) costs \(30 + 4 \cdot 2 \cdot 3 = 30 + 24 = 54\).

The minimum is 54. The dimension factor is \(p_{i-1} \cdot p_k \cdot p_j\) in 0-based index language: the left result has row count \(p_{i-1}\) and the right result has column count \(p_j\), and they meet at \(p_k\). Using \(p_i\) in place of \(p_{i-1}\) would price a different pair of dimensions. Cells are filled by increasing chain length, because a chain depends only on strictly shorter chains. There are \(\Theta(n^2)\) cells and \(O(n)\) splits per cell, so the general algorithm is \(\Theta(n^3)\). Here \(n = 3\) is small enough to compare both splits directly.

### Q9

Answer: 2

| \(a\) | 0 | 1 | 2 | 3 | 4 | 5 | 6 | 7 | 8 |
|------:|--:|--:|--:|--:|--:|--:|--:|--:|--:|
| \(C[a]\) | 0 | 1 | 2 | 3 | 1 | 2 | 1 | 2 | 2 |

\(C[4] = 1\) by a single 4. \(C[6] = 1\) by a single 6. \(C[8]\) tries last coin 1 (\(1+C[7] = 3\)), last coin 4 (\(1+C[4] = 2\)), and last coin 6 (\(1+C[2] = 3\)). The minimum is 2, realised by \(4+4\). The same item set is reused, which is correct because the supply of each denomination is unlimited.

### Q10

Answer: 2

Rows are prefixes of \(\texttt{PLAN}\), columns are prefixes of \(\texttt{PANE}\). A match copies the diagonal. A mismatch adds 1 to the best of delete, insert, and substitute.

|  |  | P | A | N | E |
|--|--|--:|--:|--:|--:|
|  | 0 | 1 | 2 | 3 | 4 |
| P | 1 | 0 | 1 | 2 | 3 |
| L | 2 | 1 | 1 | 2 | 3 |
| A | 3 | 2 | 1 | 2 | 3 |
| N | 4 | 3 | 2 | 1 | 2 |

The distance is 2. One alignment deletes L and inserts E: \(\texttt{PLAN} \to \texttt{PAN} \to \texttt{PANE}\). A match contributes 0. Charging 1 for every column, including matches, would compute a different and larger number.

### Q11

Answer: A, B, C, D

All four statements match the transitions. Unlimited supply stays on the same set of items and only reduces the capacity, which is rod cutting, unbounded knapsack, and the coin recurrence. A left-to-right scan of one 0/1 array reads a residual capacity that this same item has already updated, so the item is taken again. Boolean subset-sum is the special knapsack in which a sum is either reachable or not; an equal partition exists when the total is even and the target \(\mathrm{total}/2\) is reachable. The downward scan, or an explicit previous row, preserves the “at most once” rule that the upward scan loses.

### Q12

Answer: 10

| \(x\) | 0 | 1 | 2 | 3 | 4 |
|------:|--:|--:|--:|--:|--:|
| \(R[x]\) | 0 | 1 | 5 | 8 | 10 |

\(R[2] = 5\) is one piece of length 2, better than two pieces of length 1. \(R[3] = 8\) is the length-3 price, better than \(5+1\). \(R[4]\) tries \(9 + R[0]\), \(8 + R[1] = 9\), \(5 + R[2] = 10\), and \(1 + R[3] = 9\). The maximum is 10, from two pieces of length 2. Best price per unit would cut a length-3 piece first (\(8/3\) beats \(5/2\)), leave a length-1 piece, and score 9. That greedy choice is not optimal. The DP tries every last cut.

### Q13

Answer: 3

Let the coins be considered in the order 1, then 2. The array of the number of combinations starts at \([1, 0, 0, 0, 0]\).

- Coin 1 updates it to \([1, 1, 1, 1, 1]\).
- Coin 2 adds, at amount 2, the one way to make 0; at amount 3, the one way to make 1; at amount 4, the two ways to make 2. The array becomes \([1, 1, 2, 2, 3]\).

The three combinations are \(1+1+1+1\), \(2+1+1\), and \(2+2\). Order inside a combination is not counted again, because each coin is finished before the next coin starts. Iterating amounts on the outside and coins on the inside counts permutations instead: \(1+1+2\), \(1+2+1\), and \(2+1+1\) would become three separate ways, and the total would be 5.

### Q14

Answer: 4

Process the numbers one at a time, scanning the Boolean array downward so each number is used once.

- After 2: sums \(0, 2\).
- After 3: sums \(0, 2, 3, 5\).
- After 5: sums \(0, 2, 3, 5, 7, 8\).
- After 6: sums \(0, 2, 3, 5, 6, 7, 8\), and larger sums past 8 that this question ignores.

Among \(0, 1, \ldots, 8\), the missing values are 1 and 4. The largest is 4. In particular 7 is \(2+5\) and 8 is \(3+5\) or \(2+6\), so a search that stops at the first failure would be wrong if it assumed a single initial segment of reachable sums.

### Q15

Answer: B

Matrix-chain DP has one state per subchain and tries every split of that subchain. With \(n\) matrices there are \(\Theta(n^2)\) subchains and \(O(n)\) splits, hence \(\Theta(n^3)\) arithmetic operations. The Catalan number \(C_{n-1}\) counts the parenthesisations; it is the size of the brute-force search, not the DP’s running time. Strassen is divide-and-conquer multiplication of two \(n \times n\) matrices: seven multiplications of \((n/2)\times(n/2)\) blocks, with solution \(\Theta(n^{\log_2 7})\). It does not receive a sequence of different dimensions, and Floyd–Warshall’s \(k\)-outermost loop is a third, unrelated triple loop.

### Q16

Answer: A, B, D

The knapsack loops run once per item per capacity value. If \(W\) is encoded in binary, the input length is \(\Theta(n + \log W)\) and a factor \(W\) is exponential in that length. The algorithm is still the right exact method when \(W\) is small. “Uses a table” does not imply polynomial bit-complexity: the table can be exponential in a numeric parameter, or exponential in \(n\) when the state is a subset. For LCS length, row \(i\) depends only on row \(i-1\), so keeping two rows of length \(\min(m, n)+1\), after swapping which string is the column index, is enough. The actual string is recovered by walking parent pointers, which those two live rows do not retain.

### Q17

Answer: B

When the array is updated in place, \(dp[x - w_i]\) must still mean “without item \(i\)”. Scanning downward from \(W\) guarantees that the residual capacity, which is smaller than \(x\), has not been updated by item \(i\) yet. Scanning upward stores the just-taken item into the residual and then reads it again, which solves the unbounded problem. The two problems do not coincide. Cells below \(W\) matter because the take branch at \(W\) reads them.

### Q18

Answer: A, C

The tail updates are:

| Key considered | \(T\) afterwards |
|----------------|------------------|
| 6 | \([6]\) |
| 2 | \([2]\) |
| 5 | \([2, 5]\) |
| 1 | \([1, 5]\) |
| 7 | \([1, 5, 7]\) |
| 4 | \([1, 4, 7]\) |
| 8 | \([1, 4, 7, 8]\) |

The length is 4, in agreement with the quadratic DP. The final array is not a subsequence: 7 occurs in the input before 4, so \(1, 4, 7, 8\) is not a subsequence even though it is increasing. The tail array stores minimum endings, not a reconstruction. A real subsequence of length 4 is \(2, 5, 7, 8\). Substring length dies on a mismatch because the next character must continue the same block; subsequence length takes the better neighbour instead. An edit match costs 0.

### Q19

Answer: B

Greedy locks in one 6, then makes the residual 2 from two 1s, and reports 3. It never revisits that first choice. The table in Q9 tries every last coin and finds \(C[8] = 2\). The denomination set \(\{1, 4, 6\}\) does not have the greedy-choice property. A canonical system would need a separate proof; this instance is a counterexample, and the DP is the algorithm that is correct for every positive integer denomination set.

### Q20

Answer: B

The unweighted exchange replaces an activity by an earlier finisher without changing the objective, because every activity contributes 1. A value can make that replacement strictly worse, so earliest finish is not safe. The DP considers the activities in finish order. Activity \(i\) is skipped, contributing \(dp[i-1]\), or taken, contributing its value plus the best solution that ends at or before \(\mathrm{pred}[i]\). Those are the only feasible choices, and the predecessor is found by binary search in the finish-sorted list. Sorting plus \(n\) binary searches is \(\Theta(n \log n)\). When every value is 1 this DP agrees with earliest-finish greedy, which is why the unweighted problem does not need the table.

### Q21

Answer: A, C, D

If the \(s\)-to-\(u\) portion of a shortest \(s\)-to-\(t\) path were not itself shortest, splicing in a better \(s\)-to-\(u\) path would improve the whole path, and the splice stays a valid walk. Bellman–Ford computes exactly those best walks of increasing length: round \(k\) relaxes every edge from the round-\((k-1)\) distances. A simple path has at most \(V-1\) edges, which is why \(V-1\) rounds finish the computation when no negative cycle exists. Floyd–Warshall adds intermediates one vertex at a time. Putting \(k\) inside the \(i\) or \(j\) loop uses intermediates that the state has not yet been allowed to use, or uses them inconsistently. Longest simple paths do not survive the same splice. The longest simple route to \(u\) may already have consumed a vertex that the continuation needed, and with cycles the unrestricted problem is NP-hard. A Bellman-style maximisation does not repair that.

### Q22

Answer: B

The two-variable loop initialises \(a = 0\) and \(b = 1\), then replaces the pair by \((b,\ a+b)\) exactly \(n-1\) times for \(n \ge 1\). Each addition is \(\Theta(1)\) and there are \(\Theta(n)\) of them, so the time is \(\Theta(n)\). Only two numbers are stored, so the auxiliary space is \(\Theta(1)\). The full table is also \(\Theta(n)\) time but \(\Theta(n)\) space; it is not required. The exponential cost belongs to the recursion that does not store anything. A constant number of additions would compute only a constant index, not \(F(n)\).
