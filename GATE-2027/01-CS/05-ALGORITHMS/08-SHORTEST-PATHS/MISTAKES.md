# Shortest Paths — Mistakes

### Common GATE Traps

| Trap | What goes wrong | Correct rule | Prevention |
|------|-----------------|--------------|------------|
| Dijkstra and a negative edge | Finalised distance left unrepaired | Non-negative weights only. Otherwise Bellman–Ford | Scan the weights before choosing |
| “No negative cycle, so Dijkstra” | The proof still needs non-negative tails | No negative cycle is the condition for existence, not for Dijkstra | Separate existence from the algorithm |
| Negative edge means undefined | A shortest path is said not to exist | Undefined only if a negative cycle is reachable and useful | Look for a cycle, not a sign |
| BFS on weights | Hop count minimised | BFS is for equal weights. Dijkstra or Bellman–Ford otherwise | Read the weight column |
| MST used as distance | Tree-path weight reported | MST minimises a different sum. A rejected edge can be a shorter path | Triangle 3, 3, 4 |
| Floyd loop order | `k` written inside | `k` is outermost | The state adds one intermediate at a time |
| Sparse Bellman–Ford | Time `Θ(V³)` given as tight | Tight bound is `Θ(VE)`. `Θ(V³)` is only when `E = Θ(V²)` | Keep `E` in the answer |
| Distances start at 0 | Every vertex looks like a source | Only the source is 0; others start at `∞` | Check the initialisation |
| Longest path via Dijkstra | Weights negated, then Dijkstra | Negation creates negative edges. On a DAG, use the topological pass | Dijkstra’s hypothesis just failed |
| Detection pass skipped | `V − 1` rounds and stop, when the question asks about a cycle | Pass `V` still relaxing means a negative cycle from `s` | One extra pass |
| Undirected negative edge | Treated like a directed one | Both directions form a 2-cycle of weight `2w < 0` | Check the picture for arrowheads |
| Prim’s key | Edge weight used in Dijkstra’s queue | Dijkstra’s key is a path distance from the source | Say the key in words |

### My Mistakes

Record your own errors after practice and past papers. Do not pre-fill this table.

| Date | Source | Question | Mistake | Root Cause | Correct Rule | Prevention |
|------|--------|----------|---------|-----------|--------------|------------|
| | | | | | | |
