# Graph Traversals — Mistakes

### Common GATE Traps

| Trap | What goes wrong | Correct rule | Prevention |
|------|-----------------|--------------|------------|
| Weighted BFS | Hop count treated as weight | BFS minimises the number of edges. Unequal weights need Dijkstra or Bellman–Ford | Check whether weights are all 1 |
| DFS distance | Parent depth reported as distance | Only a BFS tree (unweighted) is a shortest-path tree | Ask which colour order was used |
| Topological key | Increasing discovery time | Decreasing finish time, or Kahn | Finish time is when the subtree is done |
| Cycle via parent | The edge back to the DFS parent in an undirected graph | That edge is the tree edge already used. A cycle needs a different visited vertex | Store the parent |
| Grey vs black | Every edge to a visited vertex called a back edge | Directed back edges go to grey vertices | Black means the vertex has finished |
| Bound `O(E)` | Isolated vertices dropped | Full traversal is `Θ(V + E)` | A graph may have `E = 0` |
| Matrix bound | `Θ(V + E)` quoted for a matrix scan | Scanning all rows is `Θ(V²)` | Name the representation |
| One component | DFS/BFS not restarted | Loop over all vertices and start on each white one | The graph may be disconnected |
| Kosaraju order | Second pass on the original graph, or increasing finish times | Transpose, then decreasing finish order | Two mistakes each break the SCC partition |
| Queue vs stack | BFS implemented with a stack | BFS is a queue. A stack is DFS | Level order is FIFO |

### My Mistakes

Record your own errors after practice and past papers. Do not pre-fill this table.

| Date | Source | Question | Mistake | Root Cause | Correct Rule | Prevention |
|------|--------|----------|---------|-----------|--------------|------------|
| | | | | | | |
