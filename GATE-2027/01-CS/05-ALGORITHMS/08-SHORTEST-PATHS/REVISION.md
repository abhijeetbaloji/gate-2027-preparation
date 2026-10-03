# Shortest Paths — Revision

## Pick one

| Situation | Algorithm | Time |
|-----------|-----------|------|
| Unit weights | BFS | `Θ(V+E)` |
| Non-negative, sparse, one source | Dijkstra, binary heap | `Θ(E log V)` |
| Non-negative, dense, one source | Dijkstra, array | `Θ(V²)` |
| Negative edges, one source | Bellman–Ford | `Θ(VE)` |
| DAG, any signs | Topo order + relax | `Θ(V+E)` |
| All pairs, dense | Floyd–Warshall, `k` outer | `Θ(V³)` |
| All pairs, negative, sparse | Johnson | `Θ(VE log V)` with binary heaps |

## Why Dijkstra fails on a negative edge

It finalises the unsettled vertex of smallest tentative distance. A later negative edge can undercut that distance. Non-negative tails cannot.

## Detection

- Bellman–Ford: a decrease on pass `V` means a negative cycle is reachable from `s`.
- Floyd: some `D[i][i] < 0`.
- A lone negative edge is not a cycle.

## Not the same problem

- MST: minimum sum of a tree, not a path weight. Kruskal/Prim allow negative edges.
- Longest path in a DAG: negate, then the DAG shortest-path algorithm. Not Dijkstra.
- Unreachable distance is `∞`.

## Traps

- Dijkstra “because there is no negative cycle”.
- BFS on unequal weights.
- Floyd with `k` inside.
- `Θ(V³)` as the tight cost of sparse Bellman–Ford.
- Initialising every distance to 0.
