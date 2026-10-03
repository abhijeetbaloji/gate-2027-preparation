# Graph Traversals — Formulas

| Result | When it applies |
|--------|-----------------|
| List space `Θ(V + E)` | Adjacency lists. Sum of undirected degrees `2E` |
| Matrix space `Θ(V²)` | Adjacency matrix |
| BFS / DFS time, lists | `Θ(V + E)`. Each vertex started once, each edge scanned once |
| BFS / DFS time, matrix | `Θ(V²)`. Every row is scanned |
| Auxiliary space | `Θ(V)` colours; queue or recursion stack up to `Θ(V)` |
| Unweighted distance | BFS `dist[v]` equals the minimum number of edges from the source |
| Directed cycle | Equivalent to a back edge (to a grey vertex) in DFS |
| Undirected cycle | Back edge to a vertex other than the parent |
| Topological order | Decreasing DFS finish time, or Kahn (indegree 0). Needs a DAG |
| Parenthesis property | Descendant intervals lie inside `[disc[u], fin[u]]` |
| Kosaraju | Two DFS passes, the second on the transposed graph in decreasing finish order. Time `Θ(V + E)` |
| Bipartite | Equivalent to 2-colourable, equivalent to no odd cycle |
| BFS level gap | A non-tree edge in an undirected BFS joins the same level or adjacent levels |
