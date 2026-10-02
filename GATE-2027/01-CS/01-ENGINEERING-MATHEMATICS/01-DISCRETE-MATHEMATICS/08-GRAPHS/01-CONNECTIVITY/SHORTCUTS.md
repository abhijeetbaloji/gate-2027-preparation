# Graphs: Connectivity — Shortcuts

### Tree test in one step
- **Why:** Tree = connected + |E| = |V| − 1, OR acyclic + |E| = |V| − 1.
- **When:** MCQ gives n, m and asks "must be a tree?"
- **Example:** 10 vertices, 9 edges, acyclic → tree without drawing.
- **Trap:** 10 vertices, 9 edges, but disconnected (e.g. two components) → **not** a tree.

### Odd-degree vertex count
- **Why:** Sum of degrees is even.
- **When:** "Which degree sequence is impossible?"
- **Example:** 3, 3, 3, 2, 1 → three odd → **impossible**.
- **Trap:** Sequence summing to even but with odd count of odd terms still invalid.

### Disconnected edge lower bound
- **Why:** Each component on n_i vertices needs ≥ n_i − 1 edges to be connected internally.
- **When:** k components, find minimum edges.
- **Example:** 5 isolated vertices → 0 edges, 5 components.
- **Trap:** Using n − 1 when graph has k > 1 components (correct min is |V| − k for forest).

### Bipartite quick check
- **Why:** Odd cycle ⇔ not bipartite.
- **When:** Small graph drawn in question.
- **Example:** Triangle C_3 → not bipartite; any tree → bipartite.
- **Trap:** Graph with even cycle only (C_4) **is** bipartite.

### Euler shortcut
- **Why:** Degree parity decides trail type.
- **When:** "Does Euler circuit exist?"
- **Example:** K_5: all degree 4 → even; connected → **Euler circuit exists**.
- **Trap:** Two components each with all even degrees → **no** Euler circuit for whole graph.
