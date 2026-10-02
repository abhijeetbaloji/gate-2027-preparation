# System of Linear Equations — Shortcuts

Use only **after** understanding `NOTES.md`.

---

### Shortcut: Rank comparison only — no full solve

**Why it works:** Rouché–Capelli classifies solutions from ranks alone.

**When to use:** "How many solutions?" MCQs.

**Example:** 3×5 matrix, rank=3 → if consistent, 5−3=2 free vars → infinite.

**Trap / limitation:** Must compute rank([A|b]), not just rank(A).

---

### Shortcut: Homogeneous + square + det(A)≠0 → only x=0

**Why it works:** Invertible A ⇒ Ax=0 ⇒ x=A^{-1}0=0.

**When to use:** Quick check on homogeneous systems.

**Example:** det≠0 → unique trivial solution only.

**Trap / limitation:** det=0 does not always mean infinite — still need rank check for non-homogeneous.

---

### Shortcut: Dependent rows in A — same relation must hold in b

**Why it works:** Linear combination of equations must match on RHS.

**When to use:** Consistency check without elimination.

**Example:** R₁−2R₂=0 in A requires b₁−2b₂=0.

**Trap / limitation:** Hidden dependence needs elimination.

---

### Shortcut: Parameter λ — watch for zero pivot

**Why it works:** Row becomes dependent at specific λ.

**When to use:** "For which λ no solution / infinite?"

**Example:** Eliminate; denominator in pivot expression = 0 → special λ.

**Trap / limitation:** Also check rank([A|b]) at special λ.

---

### Shortcut: Free variable = assign t, express pivots

**Why it works:** RREF shows pivot vs free columns.

**When to use:** Writing general solution.

**Example:** x₃=t → back-substitute x₂, x₁ in terms of t.

**Trap / limitation:** Use RREF, not REF, for cleanest form.
