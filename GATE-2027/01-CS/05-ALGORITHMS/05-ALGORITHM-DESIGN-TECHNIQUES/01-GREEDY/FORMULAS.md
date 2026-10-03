# Greedy — Formulas and results

| Result | When it applies |
|--------|-----------------|
| Activity selection: sort by finishing time, then one linear scan | Maximum *number* of compatible intervals. Time `Θ(n log n)` including the sort, `Θ(n)` if already sorted |
| Fractional knapsack value | Take items in decreasing `v_i / w_i`; at most one item is fractional. Time `Θ(n log n)` |
| 0/1 knapsack is not solved by that ratio rule | A counterexample is in the notes (capacity 50, values 60, 100, 120). Use DP, `Θ(n W)` |
| Coin greedy | Optimal only for denomination sets where the greedy-choice property holds. Fails for `{1, 3, 4}` and amount 6 (3 coins vs 2) |
| Coin DP `C(a) = 1 + min_i C(a − d_i)` | Every positive denomination set. Time `Θ(k A)` |
| Huffman | Repeatedly merge the two lightest nodes. Time `Θ(n log n)`. Minimises `Σ freq · depth` among prefix codes |
| File-merge cost | Sum of the sizes of the files created at each merge. Same merge order as Huffman. Time `Θ(n log n)` |
| Job sequencing | Sort by decreasing profit. Place in the latest free slot `≤ deadline`. Naive `O(n²)`; with union-find `Θ(n log n)` after sorting |
| Cut property | Lightest edge across a cut is in some MST. Justifies Kruskal and Prim. Negative weights allowed |
| Dijkstra’s greedy step | Safe only if every edge weight is `≥ 0` |
| Weighted matroid | Maximum-weight independent set is found by the greedy “add the heaviest element that preserves independence” rule |
