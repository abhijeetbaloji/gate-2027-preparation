# Graphs: Matching — Shortcuts

### Complete bipartite K_{m,n}
- **Why:** Every edge crosses parts; greedy pick works.
- **When:** "Maximum matching in K_{3,5}?"
- **Example:** Answer = **min(3,5) = 3**.
- **Trap:** |E| = 15 but matching size is 3, not 15.

### Path graph P_n
- **Why:** Alternate edges along path.
- **When:** Line of n vertices.
- **Example:** P_6 → **3** edges in max matching.
- **Trap:** P_5 → ⌊5/2⌋ = **2**, not 3.

### Hall's theorem — check smallest failing S
- **Why:** One bad subset disproves saturating matching.
- **When:** "Does matching covering all of A exist?"
- **Example:** Two vertices in A share only one neighbour in B → fail.
- **Trap:** |A| ≤ |B| is necessary but **not sufficient**.

### Perfect matching on trees
- **Why:** Structure matters, not just |V| even.
- **When:** Tree with 6 vertices.
- **Example:** Star K_{1,5} → max matching **1** (not perfect).
- **Trap:** Path P_6 **does** have perfect matching.

### König for min vertex cover
- **Why:** Find max matching first on small bipartite graph.
- **When:** "Minimum vertices touching all edges."
- **Example:** Matching of size 3 → min cover size **3**.
- **Trap:** König fails on non-bipartite (e.g. triangle needs 2 cover, max matching 1).
