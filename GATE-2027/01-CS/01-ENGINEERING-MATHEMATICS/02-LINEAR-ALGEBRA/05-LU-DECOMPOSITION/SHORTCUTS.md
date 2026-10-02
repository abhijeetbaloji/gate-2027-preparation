# LU Decomposition — Shortcuts

Use only **after** understanding `NOTES.md`.

---

### Shortcut: 2×2 LU by one elimination step

**Why it works:** Only one multiplier ℓ₂₁ = a₂₁/a₁₁.

**When to use:** Quick verify on exams.

**Example:** [[2,1],[4,3]] → L=[[1,0],[2,1]], U=[[2,1],[0,1]].

**Trap / limitation:** a₁₁=0 needs row swap (PA=LU).

---

### Shortcut: det from U diagonal only

**Why it works:** det(L)=1 for unit diagonal.

**When to use:** After LU without row swaps.

**Example:** U diag (2,−1,5) → det=−10.

**Trap / limitation:** Each row swap flips sign.

---

### Shortcut: Forward then back — never mix order

**Why it works:** L then U mirrors elimination direction.

**When to use:** Every LU solve.

**Example:** Ly=b gives y; plug into Ux=y.

**Trap / limitation:** Must use permuted b if PA=LU.

---

### Shortcut: L diagonal always 1 — don't solve for ℓ_{ii}

**Why it works:** Definition of standard LU.

**When to use:** Writing L from multipliers.

**Example:** Only store below-diagonal entries.

**Trap / limitation:** LDU variant differs — read problem statement.

---

### Shortcut: Reuse LU for multiple b

**Why it works:** A unchanged; only b changes.

**When to use:** Conceptual "k right-hand sides" questions.

**Example:** k solves cost O(kn²) after one O(n³) factor.

**Trap / limitation:** If A changes, refactor.
