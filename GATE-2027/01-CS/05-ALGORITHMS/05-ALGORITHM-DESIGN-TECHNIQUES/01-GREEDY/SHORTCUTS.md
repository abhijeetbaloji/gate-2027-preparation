# Greedy — Shortcuts

### Name the objective before you trust the rule

**Shortcut.** Earliest-finish greedy is for the *number* of intervals. Highest-profit greedy is for one-unit job profit. Ratio greedy is for a *fractional* knapsack.

**Why it works.** Each rule has an exchange proof for one objective. A different objective breaks the exchange.

**When to use.** The stem says “maximum number”, “maximum profit”, or “fraction of an item”.

**Example.** Intervals with weights are a DP problem even though they are still intervals.

**Limitation.** If the objective is minimum lateness and every job must run, earliest deadline first is the greedy rule, not highest profit.

---

### One counterexample kills a greedy claim

**Shortcut.** To reject a proposed greedy rule, give one feasible instance where its value loses to another feasible solution.

**Why it works.** The greedy-choice property is a “for all inputs” statement. One failure falsifies it.

**When to use.** “Does this strategy always give an optimal answer?”

**Example.** Coins 1, 3, 4 and amount 6: greedy takes three coins, two 3s are better.

**Limitation.** A successful example does not prove the rule. After a counterexample you still need DP or another algorithm if the question asks for the optimum.

---

### Negative weights: MST yes, Dijkstra no

**Shortcut.** A negative edge does not by itself forbid a greedy algorithm. It forbids Dijkstra’s finalise-the-closest-vertex step. Kruskal and Prim remain correct.

**Why it works.** The cut property compares edges with each other and never adds path weights. Dijkstra assumes that extending a path cannot get cheaper later, which is false if a later edge is negative.

**When to use.** A graph question mentions a negative number and asks which algorithm still works.

**Example.** One edge of weight `−1` on an otherwise positive graph: compute an MST with Kruskal; do not run Dijkstra.

**Limitation.** A negative *cycle* makes shortest paths undefined. MST does not care about cycles’ signs beyond the cycle property (the heaviest edge of a cycle is excluded from some MST). An MST algorithm still returns a tree; it does not detect shortest-path issues.

---

### Huffman and file merge share a heap

**Shortcut.** Repeatedly combine the two smallest weights. The cost of a file-merge sequence is the sum of the combined sizes.

**Why it works.** The two lightest leaves belong together at the bottom of an optimal tree. Each merge creates a new weight that competes in later rounds.

**When to use.** Prefix codes, or “minimum cost to merge all files”.

**Example.** Files 2, 3, 4, 5. First cost 5, then 9, then 14, total 28.

**Limitation.** Merging the two *largest* is the wrong direction. Ties can produce different trees with the same cost; do not hunt for a unique parenthesisation.
