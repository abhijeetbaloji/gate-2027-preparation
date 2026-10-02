# Graphs: Colouring — Shortcuts

### Triangle present ⇒ χ ≥ 3
- **Why:** K_3 is clique of size 3.
- **When:** Small graph diagram with triangle.
- **Example:** Any graph containing K_3 → need ≥ 3 colours.
- **Trap:** χ = 3 does not mean graph is C_5; could be K_4 (χ = 4).

### Bipartite instant win
- **Why:** No odd cycle detected → χ = 2.
- **When:** Trees, even cycles, complete bipartite.
- **Example:** K_{3,4} → **χ = 2**.
- **Trap:** Empty graph on n vertices → **χ = 1**, not 2.

### Brooks quick upper bound
- **Why:** χ ≤ Δ for most "nice" graphs.
- **When:** Δ = 3, graph not K_4 and not odd cycle.
- **Example:** Cube graph Δ = 3, bipartite → χ = 2 ≤ 3.
- **Trap:** K_4 has Δ = 3, χ = 4 — Brooks exception.

### Greedy on high-degree-first order
- **Why:** Hard vertices coloured early; often fewer colours.
- **When:** Need upper bound only, not exact χ.
- **Example:** Gives ≤ Δ + 1 always.
- **Trap:** Greedy count may exceed χ.

### Odd cycle test for χ = 2
- **Why:** χ = 2 iff bipartite iff no odd cycle.
- **When:** "Is 2-colouring possible?"
- **Example:** C_6 → yes; C_7 → no (χ = 3).
- **Trap:** Graph with only even cycles but disconnected — still χ = 2 per component with edges.
