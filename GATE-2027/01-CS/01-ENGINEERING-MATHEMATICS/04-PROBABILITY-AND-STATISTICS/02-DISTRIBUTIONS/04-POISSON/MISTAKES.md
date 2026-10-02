# Poisson Distribution — Mistakes

## Common Mistakes

These are **general/common traps** — not personal error logs.

### General/common trap: No time scaling

**What goes wrong:** Using λ without multiplying by t

**Correct rule:** Count in t: Poisson(λt)

**Prevention:** Match interval to rate

---

### General/common trap: P(X≥1) by summing

**What goes wrong:** Summing k=1 to ∞

**Correct rule:** Use 1−e^{−λ}

**Prevention:** Complement rule

---

### General/common trap: Mean≠Var assumption

**What goes wrong:** Missing Poisson when E=Var

**Correct rule:** E[X]=Var(X)→think Poisson

**Prevention:** Check moments

---

## My Mistakes

Record your own errors after PYQs and practice. Do not pre-fill.

| Date | Source | Question | Mistake | Root Cause | Correct Rule | Prevention |
|------|--------|----------|---------|------------|--------------|------------|
| | | | | | | |
