# Eigenvalues and Eigenvectors — Mistakes

## Common Mistakes

These are **general/common traps** — not personal error logs.

### General/common trap: Confusing algebraic and geometric multiplicity

**What goes wrong:** Assuming one eigenvector per eigenvalue always.

**Correct rule:** Geometric ≤ algebraic; Jordan block [[2,1],[0,2]] has alg=2, geom=1.

**Prevention:** Solve (A−λI)v=0 and count independent solutions.

---

### General/common trap: Forgetting λ=0 as eigenvalue when det=0

**What goes wrong:** Only looking for nonzero λ from polynomial.

**Correct rule:** det(A)=0 ⟺ λ=0 is eigenvalue.

**Prevention:** Check constant term of char poly = det(A).

---

### General/common trap: Using A^k = PΛ^k P^{-1} when not diagonalizable

**What goes wrong:** Applying formula to Jordan blocks.

**Correct rule:** Need full set of linearly independent eigenvectors.

**Prevention:** Verify geometric = algebraic for each λ.

---

### General/common trap: Non-orthogonal eigenvectors for symmetric matrix

**What goes wrong:** Picking any eigenvector without orthogonalizing.

**Correct rule:** Distinct eigenvalues of symmetric A → orthogonal eigenvectors automatically if chosen from eigenspaces.

**Prevention:** Use dot product check for symmetric matrices.

---

### General/common trap: trace = product confusion

**What goes wrong:** Using tr(A) when question needs det(A).

**Correct rule:** **Sum** = tr; **product** = det.

**Prevention:** Write both Vieta relations on paper.

---

## My Mistakes

Record your own errors after PYQs and practice. Do not pre-fill.

| Date | Source | Question | Mistake | Root Cause | Correct Rule | Prevention |
|------|--------|----------|---------|------------|--------------|------------|
| | | | | | | |
