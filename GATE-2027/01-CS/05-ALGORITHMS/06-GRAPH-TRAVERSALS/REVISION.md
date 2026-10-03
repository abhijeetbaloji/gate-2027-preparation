# Graph Traversals — Revision

## Time

| Representation | BFS or DFS |
|----------------|------------|
| Adjacency lists | `Θ(V + E)` |
| Adjacency matrix | `Θ(V²)` |

Extra space `Θ(V)` for colours, queue, or stack. Worst-case queue and worst-case DFS stack are both `Θ(V)`.

## Which one

- BFS, queue, levels: fewest edges. Not for unequal weights.
- DFS, stack, `disc`/`fin`: cycles, topological order, SCCs, articulation points.
- Topological order = decreasing finish time. Kahn = repeatedly remove indegree 0.
- Directed cycle = DFS back edge to a grey vertex.
- Undirected cycle = back edge to a non-parent.
- Bipartite = 2-colouring succeeds = no odd cycle.
- Kosaraju = finish times, transpose, DFS in decreasing finish order. `Θ(V + E)`.

## Properties

- BFS parent tree from `s`: shortest paths in hops.
- DFS parent tree: not a shortest-path tree.
- Descendant time intervals nest inside the ancestor’s `[disc, fin]`.
- Disconnected graphs: restart on every white vertex. Still `Θ(V + E)`.

## Traps

- Topological order from discovery times.
- Parent edge called a cycle.
- `O(E)` with isolated vertices ignored.
- `O(V + E)` on a matrix.
- Dijkstra’s job given to BFS.
