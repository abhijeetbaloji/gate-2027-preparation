# Greedy Algorithms — Learning Notes

A greedy algorithm builds a solution by a local rule and never takes a step back. That is safe only when a locally best choice can be extended to a globally best solution. Many famous graph algorithms are greedy; their full write-ups live under minimum spanning trees and shortest paths. This file is about the design rule, the proofs, and the standard problems GATE uses to test it.

---

## 1. The design rule

**What it is.** You have a solution built from pieces (jobs, edges, items, activities). At each step you add the piece that looks best according to a fixed rule, subject to feasibility, and you do not reconsider it.

**Intuition.** “Take the best available bite.” This works when the best bite never blocks a better overall meal. It fails when a modest bite now keeps two better bites available later.

**Two properties that make the proof work.**

1. **Greedy-choice property.** There exists an optimal solution that agrees with the greedy algorithm’s first choice. You prove this by exchange: start from any optimal solution, and if it differs from the greedy choice, rewrite it until it contains that choice, without losing optimality.
2. **Optimal substructure.** After that choice is fixed, an optimal solution of the remaining problem, plus the choice, is optimal for the original problem.

Divide-and-conquer and dynamic programming also use optimal substructure. Greedy adds the claim that you need not try the other first choices. Dynamic programming tries them and stores the winners. If you cannot prove the greedy-choice property, do not use the greedy rule.

**Why “it worked on my example” is not a proof.** A rule can succeed on ten arrays and fail on the eleventh. The exchange argument has to cover every input.

**Complexity pattern.** The greedy step itself is often `O(1)` or `O(log n)` with a heap. The dominant cost is sorting the candidates, `O(n log n)`, or maintaining a priority queue.

---

## 2. Activity selection (interval scheduling)

**What it is.** `n` activities with start times `s_i` and finish times `f_i`. Two activities are compatible if one finishes no later than the other starts. Select a maximum-size compatible subset. (The objective is the number of activities, not a weight. Weighted interval scheduling needs dynamic programming.)

**The rule.** Sort so that `f_1 ≤ f_2 ≤ … ≤ f_n`. Pick activity 1. Then pick the next activity that starts at or after the finish of the last picked activity. Repeat.

**Why sorting by finish time is the right local rule.** The activity that ends soonest leaves the largest possible remainder of the day. Sorting by start time, by duration, or by the number of conflicts does not have an exchange proof. Shortest duration is a common wrong rule: a short activity in the middle can block two activities that would have fit on either side.

**Why the exchange works.** Let greedy pick activity `g` first (an earliest finisher). Let `OPT` be any optimal set, and let `a` be the activity in `OPT` that finishes first. Then `f_g ≤ f_a`. Replacing `a` by `g` keeps feasibility: everything else in `OPT` starts at or after `f_a`, hence at or after `f_g`. The new set has the same size and contains the greedy choice. The same argument repeats on the activities that start after `f_g`.

**Example.**

| Activity | A | B | C | D |
|----------|---|---|---|---|
| Start | 1 | 2 | 4 | 6 |
| Finish | 3 | 5 | 6 | 8 |

Sorted by finish: A, B, C, D. Pick A (ends 3). B starts at 2, too early. C starts at 4, take it (ends 6). D starts at 6, take it. Set `{A, C, D}`, size 3. `{B, D}` has size 2.

**Complexity.**

| Case | Time | Why | Space |
|------|------|-----|-------|
| All cases, if you sort | `Θ(n log n)` | Sort dominates a later linear scan | `Θ(1)` extra beyond the sort, or `Θ(n)` if the sort needs it |
| Already sorted by finish | `Θ(n)` | One scan | `Θ(1)` |

There is no better or worse input for the scan: you look at each activity once. The worst case is the sorting bound.

**When not to use this rule.** Activities have values and you want maximum value. A low-value activity that finishes first can block a high-value one. Use dynamic programming on weighted intervals. Also do not use it when the objective is something other than “maximum number of compatible intervals”.

**GATE trap.** Sorting by start time or by length and still claiming optimality. The exchange proof uses the earliest finish.

---

## 3. Fractional knapsack

**What it is.** A knapsack of capacity `W`. Item `i` has weight `w_i` and value `v_i`. You may take any fraction `x_i ∈ [0, 1]` of an item. Weight `Σ x_i w_i ≤ W`. Maximise `Σ x_i v_i`.

**The rule.** Sort by decreasing value per unit weight `v_i / w_i`. Take items whole until the next one does not fit. Fill the remaining capacity with a fraction of that next item.

**Why it works.** Suppose an optimal solution leaves some amount of a higher-ratio item untaken while it carries a lower-ratio item. Swapping a little weight from the worse item to the better one increases value and stays within capacity. So there is an optimal solution that uses items in ratio order, with at most one fractional item.

**Example.** Capacity 50.

| Item | Weight | Value | Ratio |
|------|--------|-------|-------|
| A | 10 | 60 | 6 |
| B | 20 | 100 | 5 |
| C | 30 | 120 | 4 |

Take all of A and B (weight 30, value 160). Remaining capacity 20. Take `20/30` of C, value 80. Total value 240.

**Complexity.** `Θ(n log n)` to sort, then `Θ(n)` to fill. Auxiliary space `Θ(1)` besides the sort. Best, average, and worst time match because the values do not change the control flow except which item is fractional, and you still sort.

**The 0/1 version is not greedy.** If you must take an item entirely or not at all, the same ratio order can fail. On the table above, ratio order takes A and B and then cannot take C (weight 60 > 50). Value 160. Taking B and C weighs 50 and is worth 220. The fraction was exactly what made the swap argument possible. 0/1 knapsack has optimal substructure but not this greedy-choice property. It is solved by dynamic programming in `Θ(n W)` time.

**GATE trap.** Applying the ratio sort to a 0/1 statement, or refusing a fraction when the problem says “fractional”. Read whether `x_i` may lie strictly between 0 and 1.

---

## 4. Coin change, and a case where the obvious rule fails

**What it is.** Coins of denominations `d_1 > d_2 > … > d_k`, and an amount `A`. Make `A` with as few coins as possible. Unlimited supply.

**The greedy rule.** Take as many of the largest denomination as fit, then the next, and so on.

**When it works.** For canonical systems, including the usual powers and the standard currency sets that have been proved canonical (for example 1, 5, 10, 25). The proof is specific to the set. “Real money” is not a theorem by itself; the denomination list is.

**When it fails.** Denominations `1, 3, 4`, amount `6`.

- Greedy: one 4 and two 1s. Three coins.
- Optimal: two 3s. Two coins.

The first choice of a 4 cannot be part of any optimal solution. The greedy-choice property is false for this set.

**What to do instead.** Dynamic programming: let `C(a)` be the minimum number of coins for amount `a`. `C(0) = 0`, and `C(a) = 1 + min_i C(a − d_i)` over `d_i ≤ a`. Time `Θ(k A)`, pseudo-polynomial. That algorithm is correct for every positive integer denomination set. Greedy is only a fast special case.

**GATE trap.** “Greedy coin change is optimal” with no denomination hypothesis. Always test a small non-canonical set before you trust the rule.

---

## 5. Huffman coding

**What it is.** A set of symbols with frequencies. Build a binary prefix code of minimum expected codeword length. A prefix code means no codeword is a prefix of another, so a bitstream decodes without separators.

**Why a tree.** Each prefix code is a binary tree. Symbols are leaves. The codeword is the path, say 0 left and 1 right. The expected length is `Σ freq(leaf) · depth(leaf)`.

**The rule.** Put the symbols in a min-heap by frequency. While more than one node remains, extract the two smallest, make them children of a new node whose frequency is their sum, and insert the parent. The last node is the root.

**Why it works.** In an optimal tree, the two least frequent symbols are siblings at the deepest level. If they were not, you could swap a deeper, rarer symbol with a shallower one and not increase the cost, or strictly decrease it. Merging those two symbols reduces the problem to a smaller Huffman instance. That is the greedy-choice property plus optimal substructure.

**Example.** Frequencies `{A: 5, B: 9, C: 12, D: 13, E: 16, F: 45}`. The first merge joins A and B into a node of weight 14. The heap process continues until one tree remains. F, the most frequent symbol, ends up with a short code. A and B end up deep. You do not need the full tree to see the greedy step: the first internal node is always the two currently lightest nodes.

**Complexity.**

| Case | Time | Why | Space |
|------|------|-----|-------|
| All cases, binary heap | `Θ(n log n)` | `n − 1` extract-min pairs, each `O(log n)` | `Θ(n)` for the heap and the tree |

Frequencies do not create an early exit. Best, average, and worst time are the same.

**Decoding.** Walk from the root according to the next bit until you hit a leaf. Prefix-freeness means you never wonder whether to stop early.

**When not to use.** The symbols do not have known independent frequencies, or you need a code with extra constraints (error correction). Huffman is optimal among prefix codes for a known distribution; it is not optimal among all possible encodings if you allow arithmetic coding’s fractional bits, which is outside this syllabus.

**GATE traps.**

- Merging the two *largest* frequencies. That builds a pessimal shape, not a Huffman tree.
- Forgetting that the parent’s weight re-enters the heap. Later merges compare parents with original symbols.
- Using Huffman when the question is 0/1 knapsack. Both use heaps or sorting sometimes; the objectives differ.

---

## 6. Optimal merging of files

**What it is.** Files of sizes `s_1, …, s_n`. Merging two files of sizes `a` and `b` costs `a + b` and produces a file of that size, which may be merged again. Find a sequence of merges of minimum total cost. This is the same tree shape as Huffman: internal-node weight is the sum of the two children, and the total cost is the sum of the internal-node weights.

**The rule.** Always merge the two current files of smallest size.

**Example.** Sizes `2, 3, 4, 5`.

- Merge 2 and 3, cost 5. Now `4, 5, 5`.
- Merge 4 and 5, cost 9. Now `5, 9`.
- Merge 5 and 9, cost 14.
- Total `5 + 9 + 14 = 28`.

Merging 5 and 4 first (cost 9), then 2 and 3 (cost 5), then 9 and 5 (cost 14) totals 28 as well — another optimal tree. Merging the two largest first is worse: 5 with 4 (9), then 9 with 3 (12), then 12 with 2 (14), total `9+12+14 = 35`.

**Complexity.** `Θ(n log n)` with a min-heap. Same bound in every case.

**GATE observation.** If the question only asks the cost, simulate the heap. If two pairs tie, different legal choices can give the same optimal cost; do not assume the tree is unique.

---

## 7. Job sequencing with deadlines

**What it is.** Each job takes one unit of time, earns profit `p_i` only if it finishes by deadline `d_i`, and you have one machine. Time slots are `1, 2, …, t` where `t` is the largest deadline. Maximise total profit. A job scheduled in slot `s` finishes at time `s` and needs `s ≤ d_i`.

**The rule.** Consider jobs in decreasing order of profit. Place each job in the latest slot that is still free and is at most its deadline. If no such slot exists, reject the job.

**Why latest slot, not earliest.** Leaving earlier slots open preserves room for a later job whose deadline is tighter. The exchange argument: in an optimal schedule, the highest-profit job can be moved to the latest feasible slot without decreasing profit, because that slot was either empty or held a job you can shift earlier or drop only if you are comparing profits correctly. The standard proof shows that the greedy set of accepted jobs is an optimal set, and the latest-slot placement realises it.

**Example.**

| Job | Profit | Deadline |
|-----|--------|----------|
| A | 100 | 2 |
| B | 19 | 1 |
| C | 27 | 2 |
| D | 25 | 1 |

Order by profit: A, C, D, B.

- A, deadline 2: put in slot 2.
- C, deadline 2: slot 2 is full, slot 1 is free and `≤ 2`. Put C in slot 1.
- D, deadline 1: slot 1 is full. Reject.
- B, deadline 1: reject.

Profit `100 + 27 = 127`. Sequence: C then A.

**Complexity.**

| Implementation | Time | Why |
|----------------|------|-----|
| Array of slots, scan backward for each job | `Θ(n · t)` with `t ≤ n` often written `O(n²)` | For each job, scan its deadline range |
| Disjoint-set “next free slot” | `Θ(n log n)` after sorting | Almost-constant finds |

Sorting by profit is `Θ(n log n)`. Best and worst stay in that class if you use the union-find version; the naive scan is quadratic regardless of profits, up to how large the deadlines are.

**When not to use.** Jobs have different processing times. One-unit jobs are essential to the slot argument. Variable lengths are a scheduling problem, and many versions are NP-hard. Also, if every job must run and the objective is minimum lateness, the right greedy rule is earliest deadline first, which is a different theorem.

**GATE trap.** Sorting by deadline instead of profit when the objective is profit. Earliest-deadline-first optimises a lateness objective, not this profit objective.

---

## 8. Greedy graph algorithms (the idea only)

Full procedures, proofs, and complexities are in `07-MINIMUM-SPANNING-TREES` and `08-SHORTEST-PATHS`. The greedy content is:

**Minimum spanning tree, cut property.** For any cut with no tree edge across it yet, the lightest edge that crosses the cut is safe to add. Kruskal applies this by considering edges from lightest to heaviest and adding an edge when it joins two components (it is lightest across the cut between those components). Prim applies it by always extending the single growing component with the lightest edge that leaves it. Both are correct because of the cut property, not because “light edges feel small”. A negative edge is allowed: MST correctness does not need positive weights.

**Dijkstra.** Grow a set `S` of vertices whose distances are final. The next vertex is the unfinished vertex with the smallest tentative distance. That choice is safe only when every edge weight is non-negative. A negative edge behind you can make a “final” distance too large, and greedy will not revisit it. Bellman–Ford, which is dynamic programming by the number of edges, handles negative weights. If the question has a negative edge, Dijkstra is the wrong greedy algorithm.

**GATE trap.** Using Dijkstra on a graph that contains a negative weight, or using a “heaviest edge first” rule for an MST.

---

## 9. Matroids, in one precise statement

A **matroid** is a finite set `S` and a family `I` of subsets called independent sets, such that:

- the empty set is independent,
- a subset of an independent set is independent (hereditary),
- if `A` and `B` are independent and `|A| < |B|`, then some element of `B − A` can be added to `A` and the result stays independent (exchange).

On a **weighted matroid**, the greedy algorithm that repeatedly adds the maximum-weight element that preserves independence produces a maximum-weight independent set. Kruskal’s algorithm is this statement on the graphic matroid, whose independent sets are the acyclic edge sets.

This does **not** mean “a greedy rule works on a problem if and only if the problem mentions the word matroid”. It means: for the specific task “maximum-weight independent set in a hereditary family”, the greedy algorithm is optimal for every weight function exactly when that family is a matroid. Fractional knapsack is greedy-optimal for a different reason. 0/1 knapsack is not a matroid problem in this sense and greedy fails.

---

## 10. How to decide

| Problem shape | Use greedy? | Why |
|---------------|-------------|-----|
| Unweighted interval scheduling | Yes, earliest finish | Exchange on the first finisher |
| Weighted interval scheduling | No | A cheap early finish can block a valuable interval; use DP |
| Fractional knapsack | Yes, best ratio | Swapping weight toward a better ratio improves the objective |
| 0/1 knapsack | No | The fraction was necessary for the swap; use DP |
| Canonical coin systems | Yes, largest first | Depends on the denomination set |
| Arbitrary coin systems | No | `1, 3, 4` and amount 6 is a counterexample; use DP |
| Prefix code for known frequencies | Yes, Huffman | Two rarest symbols are deepest siblings |
| Merge files, cost = sum of sizes | Yes, two smallest | Same tree argument as Huffman |
| One-unit jobs, profit, deadlines | Yes, highest profit into the latest feasible slot | Slot exchange |
| MST | Yes, lightest safe edge | Cut property; negative weights allowed |
| Shortest paths, non-negative weights | Yes, Dijkstra | Finalise the closest unsettled vertex |
| Shortest paths, negative weights | No | Use Bellman–Ford or, for all pairs, Floyd–Warshall |
| Longest simple path | No | Greedy and straightforward DP both fail; the problem is NP-hard |

---

## 11. Common GATE traps

1. A worked example offered as a proof.
2. Earliest start, or shortest duration, for unweighted activity selection.
3. Ratio greedy on a 0/1 knapsack.
4. Largest-coin greedy on a non-canonical set.
5. Huffman merges of the two heaviest symbols.
6. Job sequencing sorted by deadline when profits differ and the objective is profit.
7. Dijkstra in the presence of a negative edge.
8. “Greedy never works with negative numbers.” MST algorithms allow them. Dijkstra does not.
9. Claiming the greedy solution is the unique optimum. Huffman trees and MSTs need not be unique; the optimal *value* is what the proof protects.
10. Forgetting the sort in the time bound and answering `Θ(n)` for activity selection that starts unordered.
