# Eigenvalues and Eigenvectors — Shortcuts

Use only **after** understanding `NOTES.md`.

---

### Shortcut: tr(A) and det(A) from eigenvalues without solving

**Why it works:** Vieta's formulas on characteristic polynomial.

**When to use:** Given eigenvalues or asked sum/product only.

**Example:** λ=2,2,5 → tr=9, det=20.

**Trap / limitation:** Need all eigenvalues (including multiplicities).

---

### Shortcut: det(A−cI) = Π(λᵢ−c)

**Why it works:** Shifted characteristic polynomial.

**When to use:** "Find det(A−3I)" when eigenvalues known.

**Example:** λ=1,4 → det(A−3I)=(−2)(1)=−2.

**Trap / limitation:** Count algebraic multiplicity.

---

### Shortcut: 2×2 eigenvalues — trace and det

**Why it works:** λ²−tr(A)λ+det(A)=0.

**When to use:** Quick 2×2 without full det expansion.

**Example:** tr=5, det=6 → λ=2,3.

**Trap / limitation:** Solve quadratic correctly.

---

### Shortcut: Symmetric 2×2 — orthogonal eigenvectors by inspection

**Why it works:** Spectral theorem guarantees perpendicular eigenvectors.

**When to use:** After finding λ, pick v perpendicular to first.

**Example:** A=[[2,1],[1,2]] → v₁=[1,1], v₂=[1,−1].

**Trap / limitation:** Only guaranteed for symmetric; normalize for Q.

---

### Shortcut: Triangular matrix — eigenvalues = diagonal

**Why it works:** A−λI upper triangular with diagonal a_{ii}−λ.

**When to use:** Triangular or diagonal A.

**Example:** diag(1,3,5) → λ=1,3,5.

**Trap / limitation:** Not true for all matrices — only triangular.
