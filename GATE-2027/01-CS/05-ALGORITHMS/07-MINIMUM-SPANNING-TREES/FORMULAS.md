# Minimum Spanning Trees — Formulas

| Result | When it applies |
|--------|-----------------|
| A tree on `V` vertices has `V − 1` edges | Connected and acyclic. `V` edges imply a cycle |
| Cut property | Lightest edge across a cut that the current MST subset does not touch is safe to add. Holds for negative weights |
| Cycle property | A heaviest edge on a cycle is excluded from some MST |
| Unique MST | All edge weights distinct. Repeated weights can give several MSTs of equal weight |
| Kruskal time `Θ(E log E) = Θ(E log V)` | Sort dominates Union-Find’s `Θ(E α(V))` |
| Prim, binary heap | `Θ(E log V)` |
| Prim, unsorted array or matrix | `Θ(V²)` |
| Prim, Fibonacci heap | `Θ(E + V log V)` |
| Union by rank + path compression | Amortised `α(V)` per operation, inverse Ackermann |
| Maximum spanning tree | Negate weights, or add heaviest non-cycle edge first |
| MST path vs shortest path | Not the same. A direct non-tree edge can be lighter than the tree path |
