# Dynamic Programming — Shortcuts

### Write the last choice, then the state

**Shortcut.** Ask what the solution does last. The state is whatever that choice needs to know, and nothing else.

**Why it works.** Optimal substructure says the part before the last choice is itself optimal. If the state remembers exactly the constraint the choice uses (capacity left, prefixes matched, end index), the recurrence is forced.

**When to use.** A new problem that is clearly an optimisation over sequences or subsets with additive cost.

**Example.** 0/1 knapsack’s last choice is “item `i` in or out”, so the state is `(i, capacity left)`.

**Limitation.** If the last choice can invalidate earlier feasibility, the state is incomplete. Longest simple path is the usual warning.

---

### 0/1 looks at the previous row; unbounded looks at the current one

**Shortcut.** A 0/1 item’s “take” branch uses `dp[i−1][x − w]`. An unlimited item’s branch uses `dp[i][x − w]` or a 1D array scanned upward.

**Why it works.** `i−1` removes the item from the pool. The same `i` leaves it available for another copy.

**When to use.** Knapsack, rod cutting, coin count, subset sum.

**Example.** Updating a single knapsack array from `x = w` upward lets one item fill the whole row. That is unbounded, even if you meant 0/1.

**Limitation.** The direction rule assumes the usual left-to-right capacity loop. If you iterate capacities downward, a single array stays 0/1.

---

### LCS mismatch is not the diagonal

**Shortcut.** Equal characters: diagonal plus one. Unequal: max of the cell above and the cell to the left.

**Why it works.** A match consumes both prefixes. A mismatch drops one of the two last characters, not both (dropping both is available anyway through a later step, and taking it immediately can only be worse or equal).

**When to use.** Any subsequence alignment.

**Example.** `ABC` and `ADC` match `A`, mismatch `B`/`D`, match `C`. Length 2.

**Limitation.** Substring DP zeros the cell on a mismatch. Using the LCS rule there glues non-contiguous pieces.

---

### LIS in `n log n` stores tails, not the sequence

**Shortcut.** Replace the first tail that the new key can improve. The length of the tail array is the answer.

**Why it works.** A smaller tail of the same length is always at least as easy to extend. Binary search finds that length.

**When to use.** “Time complexity of LIS” when `Θ(n²)` and `Θ(n log n)` are both offered and the faster one is allowed.

**Example.** Array `3, 1, 2`. Tails evolve `[3] → [1] → [1, 2]`. Length 2. The array `[1, 2]` happens to be a subsequence here; on `3, 1, 2, 0` the tails become `[0, 2]`, which is not itself an increasing subsequence of the input in that order of indexes.

**Limitation.** Do not print `T` as the subsequence. Strict `<` versus non-decreasing `≤` changes the binary-search test.

---

### `Θ(n W)` is not “polynomial” just because it looks like a product

**Shortcut.** Call knapsack and coin DP pseudo-polynomial. They are polynomial in the integers `W` and `A` written in unary.

**Why it works.** The input can encode `W` in `O(log W)` bits. A table of width `W` is exponential in that bit length. NP-hardness of 0/1 knapsack is consistent with this.

**When to use.** A question asks whether knapsack DP is a polynomial-time algorithm.

**Example.** `n = 10`, `W = 2^{100}` cannot be tabulated.

**Limitation.** If the question promises `W = O(n)`, the same DP is polynomial in the input size. Read the promise.
