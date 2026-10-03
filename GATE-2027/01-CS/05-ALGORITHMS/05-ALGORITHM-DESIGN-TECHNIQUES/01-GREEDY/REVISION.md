# Greedy — Revision

## Proof shape

Greedy choice (exchange) + optimal substructure. An example is not a proof. One counterexample kills a rule.

## Rules

| Problem | Rule | Time | Fails when |
|---------|------|------|------------|
| Max number of intervals | Earliest finish | `Θ(n log n)` | Objective is weighted |
| Fractional knapsack | Best `v/w`, one fraction | `Θ(n log n)` | Items are 0/1 |
| Coins | Largest first | `O(k)` after the set is fixed, or sort | Non-canonical sets, e.g. 1, 3, 4 amount 6 |
| Huffman / file merge | Two lightest | `Θ(n log n)` | You merge the two heaviest |
| Unit jobs, max profit | Highest profit, latest feasible slot | `O(n²)` or `Θ(n log n)` | Processing times are not 1 |
| MST | Lightest safe edge | Kruskal / Prim bounds in that folder | — (negative edges are allowed) |
| Shortest path | Dijkstra’s closest unsettled vertex | See shortest paths | Any negative edge |

## 0/1 counterexample

Capacity 50. Weights 10, 20, 30. Values 60, 100, 120. Ratio greedy takes 10 and 20, value 160. Optimal 0/1 is 20+30, value 220. Fractional optimum is 240.

## Do not confuse

- Earliest deadline first: lateness, not profit.
- Coin DP: `Θ(k A)`, works for every denomination set.
- Matroid greedy: maximum-weight independent set when the feasible family is a matroid (Kruskal). Not a licence to be greedy on knapsack.
