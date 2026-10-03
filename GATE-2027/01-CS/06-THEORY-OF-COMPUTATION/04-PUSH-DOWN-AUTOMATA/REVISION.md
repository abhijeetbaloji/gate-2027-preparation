# Push-Down Automata — Revision

- Move: read `a` or `ε`, pop `X`, push `γ` (left = top).
- Accept by **final state** (stack may be nonempty) or **empty stack** (ignore `F`). One machine: languages may differ. Family of NPDAs: both = CFL.
- NPDA ⇔ CFG.
- DPDA: at most one move, and no ε/letter conflict on the same stack top.
- Every regular language has a DPDA. Not every CFL does (`{ww^R}` needs a guess).
- `{wcw^R}` is DCFL. `{a^n b^n c^n}` and `{ww}` are not CFL.
- Empty-stack language of a **DPDA** is prefix-free.
- CFL ∩ regular is CFL (PDA × DFA). DCFL not closed under ∪ or ∩.
