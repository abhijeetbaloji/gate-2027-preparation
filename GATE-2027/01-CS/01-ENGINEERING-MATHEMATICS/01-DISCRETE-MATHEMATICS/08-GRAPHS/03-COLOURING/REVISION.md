# Graphs: Colouring — Quick Revision

- χ(G) = minimum colours for proper vertex colouring.
- Lower bound: χ ≥ ω (clique size); χ ≥ 1 always.
- K_n: χ = n; bipartite (with edges): χ = 2; odd cycle: χ = 3.
- Tree (≥ 2 vertices): χ = 2; single vertex: χ = 1.
- Bipartite ⇔ no odd cycle ⇔ χ = 2 (non-empty).
- Greedy: at most Δ + 1 colours.
- Brooks: χ ≤ Δ unless K_n or odd cycle (connected, simple).
- χ ≤ Δ **not** always (C_5 counterexample).
- Planar: χ ≤ 4 (Four Colour Theorem).
- Edge colouring: χ'(G) ∈ {Δ, Δ+1} (Vizing).
