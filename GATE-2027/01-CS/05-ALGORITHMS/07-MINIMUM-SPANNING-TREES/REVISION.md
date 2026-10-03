# Minimum Spanning Trees — Revision

## Facts

- Tree: `V − 1` edges, connected, acyclic.
- Cut property: lightest edge across an untouched cut is safe. Negatives allowed.
- Cycle property: heaviest edge on a cycle is out of some MST.
- Distinct weights → unique MST. Ties → same weight, possibly several trees.
- MST paths are not shortest paths.

## Algorithms

| Algorithm | Time | Notes |
|-----------|------|-------|
| Kruskal + Union-Find | `Θ(E log E) = Θ(E log V)` | Sort light to heavy; skip same component. `α(V)` is lower order |
| Prim, binary heap | `Θ(E log V)` | Grow one tree |
| Prim, array / matrix | `Θ(V²)` | Dense graphs |
| Prim, Fibonacci heap | `Θ(E + V log V)` | Theoretical |
| Maximum spanning tree | same | Heaviest feasible edge, or negate weights |

## Choose

- Edge list, sparse: Kruskal or heap Prim.
- Matrix, dense: array Prim.
- Shortest paths: not these algorithms.
- Directed arborescence: not undirected Kruskal.

## Traps

- Adding an edge whose ends are already connected.
- `Θ(V²)` Prim with a heap in the same sentence.
- Rejecting Kruskal over a negative weight.
- Claiming the tree is unique when weights repeat.
- Counting `V` edges.
