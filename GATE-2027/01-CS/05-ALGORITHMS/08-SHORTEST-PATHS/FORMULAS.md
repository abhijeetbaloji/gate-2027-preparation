# Shortest Paths — Formulas

| Result | When it applies |
|--------|-----------------|
| Relaxation `dist[v] ≤ dist[u] + w(u, v)` | Any shortest-path algorithm. Equality holds for edges on a shortest path |
| BFS | Every weight is 1, or the question counts edges. Time `Θ(V + E)` on lists |
| Dijkstra, non-negative weights only | Array `Θ(V²)`; binary heap `Θ((V + E) log V)`; Fibonacci heap `Θ(E + V log V)` |
| Bellman–Ford | `V − 1` full relaxations, then one detection pass. Time `Θ(V E)`. Negative edges allowed |
| Negative cycle from `s` | Some distance still decreases on pass `V` of Bellman–Ford |
| DAG one-source | Topological order, one relaxation pass. Time `Θ(V + E)`. Negative edges allowed; no cycle exists |
| Longest path in a DAG | Negate weights and use the DAG algorithm, or take `max` instead of `min`. Do not use Dijkstra on the negated graph |
| Floyd–Warshall `D[i][j] = min(D[i][j], D[i][k] + D[k][j])` | `k` outermost. Time `Θ(V³)`, space `Θ(V²)` |
| Negative cycle, all pairs | Some `D[i][i] < 0` after Floyd |
| Johnson | Potentials from Bellman–Ford, reweight `w'(u, v) = w(u, v) + h(u) − h(v) ≥ 0`, Dijkstra from each vertex. Time `Θ(VE + V E log V)` with binary heaps |
| Dijkstra from every vertex, non-negative, array | `Θ(V³)`, same class as Floyd, but weights must be non-negative |
| No shortest path | A negative cycle is reachable from `s` and can reach the target |
| Unreachable | Distance `∞`, not 0 |
