# Minimum Spanning Trees — Mistakes

### Common GATE Traps

| Trap | What goes wrong | Correct rule | Prevention |
|------|-----------------|--------------|------------|
| Shortest-path algorithm | Dijkstra or BFS builds the tree | MST uses the cut property. Kruskal or Prim | Ask whether the output is a tree of minimum *sum*, or distances from a source |
| Cycle edge kept | Kruskal adds an edge inside a component | Same `Find` root means reject | The edge is the heaviest on its new cycle only after a lighter connection exists; either way it closes a cycle |
| Heap Prim timed as `V²` | Data structure ignored | Binary heap is `Θ(E log V)`. The `Θ(V²)` bound is the array scan | Name the priority-queue implementation |
| Negative weight | Kruskal abandoned | Cut property allows negative weights | Save the objection for Dijkstra |
| Uniqueness | One picture treated as the only tree | Distinct weights ⇒ unique. Equal weights ⇒ maybe not | Look for repeated numbers |
| Tree path | Distance in the MST reported as a shortest path | A non-tree edge can undercut the tree path | Triangle 3, 3, 4: unused edge 4 beats the path of weight 6 |
| Edge count | `V` edges in the tree | `V − 1` | One more edge creates a cycle |
| Disconnected input | A tree is still claimed | No spanning tree exists; the result is a forest | Check reachability |
| Dense Kruskal | Sort of a complete graph called optimal | Array Prim is `Θ(V²)`, better than `Θ(V² log V)` | Compare `E` with `V²` |
| Directed graph | Undirected Kruskal run on arcs | The syllabus MST is undirected. Directions need a different algorithm | Check the arrowheads |

### My Mistakes

Record your own errors after practice and past papers. Do not pre-fill this table.

| Date | Source | Question | Mistake | Root Cause | Correct Rule | Prevention |
|------|--------|----------|---------|-----------|--------------|------------|
| | | | | | | |
