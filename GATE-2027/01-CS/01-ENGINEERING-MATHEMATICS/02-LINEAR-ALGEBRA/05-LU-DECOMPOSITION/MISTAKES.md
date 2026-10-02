# LU Decomposition — Mistakes

## Common Mistakes

These are **general/common traps** — not personal error logs.

### General/common trap: Putting multipliers in U instead of L

**What goes wrong:** Storing ℓ_{ij} above diagonal or in wrong matrix.

**Correct rule:** Multipliers for eliminating below pivot in column k go to **L** at position (i,k).

**Prevention:** Follow Gaussian elimination bookkeeping: L encodes row ops.

---

### General/common trap: Non-unit diagonal on L

**What goes wrong:** Writing pivot values on L's diagonal.

**Correct rule:** Standard LU has **1s on L's diagonal**; pivots live on **U**.

**Prevention:** Check L_{ii}=1 always.

---

### General/common trap: Solving Ux=b before Ly=b

**What goes wrong:** Wrong triangular order.

**Correct rule:** **Forward** on L first (since A=LU).

**Prevention:** Remember L is applied first to x: L(Ux)=b.

---

### General/common trap: Ignoring P when PA=LU

**What goes wrong:** Solving Ly=b instead of Ly=Pb.

**Correct rule:** Apply same row permutation to b as to A.

**Prevention:** Track swaps when building P.

---

### General/common trap: Assuming LU always exists without pivoting

**What goes wrong:** Failing on [[0,1],[1,0]].

**Correct rule:** Zero pivot requires **row interchange** (PA=LU).

**Prevention:** Check leading pivot before elimination.

---

## My Mistakes

Record your own errors after PYQs and practice. Do not pre-fill.

| Date | Source | Question | Mistake | Root Cause | Correct Rule | Prevention |
|------|--------|----------|---------|------------|--------------|------------|
| | | | | | | |
