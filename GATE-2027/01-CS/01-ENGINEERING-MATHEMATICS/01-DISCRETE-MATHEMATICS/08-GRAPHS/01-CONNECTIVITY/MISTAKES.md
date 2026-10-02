# Graphs: Connectivity — Mistakes

## Common Mistakes

| Trap | Wrong reasoning | Correct rule |
|------|-----------------|--------------|
| Tree from edge count alone | \|E\| = n − 1 ⇒ tree | Also need **connected** (or acyclic) |
| Path vs walk | Allow repeated vertices in "path" | Path: no repeated vertices |
| Euler circuit | All degrees even ⇒ Euler circuit | Need **connected** graph too |
| Odd degrees | Sum even ⇒ sequence realisable | Need **even number** of odd-degree vertices |
| Forest edges | Use n − 1 always | Forest: \|E\| = n − k for k components |
| Bipartite | Has even cycles ⇒ bipartite | Need **no odd cycle**; C_4 is bipartite |
| Bridge on cycle | Edge in cycle can be bridge | Bridges are **not** on any cycle |
| Tree leaves | Star has 1 leaf | Star K_{1,n−1} has **n − 1 leaves** (only centre degree > 1) |
| Complete graph edges | n² edges | Simple: **n(n−1)/2** |
| Directed connectivity | Weak = strong | Weakly connected ≠ strongly connected |

## My Mistakes

Record mistakes here after solving PYQs and practice questions. Do not pre-fill entries.

| Date | Source | Question | Mistake | Root cause | Fix / Rule |
|------|--------|----------|---------|------------|------------|
| | | | | | |

## Pre-exam checklist

- [ ] Re-read entries marked "recurring"
- [ ] Re-solve one question from each row before the exam
