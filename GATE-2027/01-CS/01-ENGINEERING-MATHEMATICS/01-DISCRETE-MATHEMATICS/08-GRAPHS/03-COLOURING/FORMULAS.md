# Graphs: Colouring — Formulas

| Formula / result | Meaning | Conditions | GATE use | Common mistake |
|------------------|---------|------------|----------|----------------|
| χ(K_n) = n | Complete graph | n ≥ 1 | Direct MCQ | Using n−1 |
| χ(bipartite) = 2 | Two colours suffice | Connected bipartite, \|E\| > 0 | Quick from structure | Empty graph χ = 1 |
| χ(C_{2k+1}) = 3 | Odd cycle | k ≥ 1 | Classic trap vs Δ = 2 | Saying χ = 2 |
| χ(C_{2k}) = 2 | Even cycle | k ≥ 2 | Bipartite check | — |
| χ(tree) = 2 | Tree colouring | n ≥ 2 vertices | Tree questions | n = 1 → χ = 1 |
| χ ≥ ω | Clique lower bound | ω = max clique size | Bound χ from below | Confusing ω with Δ |
| Greedy ≤ Δ + 1 | Upper bound | Any ordering | Estimate | Thinking always optimal |
| Brooks: χ ≤ Δ | Upper bound | Connected, not K_n, not odd cycle | Δ given MCQ | Applying to K_4 (χ = 4 = Δ+1) |
| Planar χ ≤ 4 | Four colours | Planar graph | Statement MCQ | Proving theorem |
| Vizing χ' ∈ {Δ, Δ+1} | Edge colours | Simple graph | Edge colouring | χ' = Δ always (false) |
