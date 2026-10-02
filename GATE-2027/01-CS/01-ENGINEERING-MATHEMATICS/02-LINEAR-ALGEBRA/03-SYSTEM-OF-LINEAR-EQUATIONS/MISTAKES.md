# System of Linear Equations — Mistakes

## Common Mistakes

These are **general/common traps** — not personal error logs.

### General/common trap: Underdetermined ⇒ infinite solutions

**What goes wrong:** Assuming m < n always gives infinitely many solutions.

**Correct rule:** Need rank(A) = rank([A|b]) < n; may be inconsistent.

**Prevention:** Always compare rank([A|b]) to rank(A).

---

### General/common trap: Ignoring augmented column in rank

**What goes wrong:** Using rank(A) alone to decide consistency.

**Correct rule:** If rank([A|b]) > rank(A) → **no solution**.

**Prevention:** Row-reduce [A|b] together.

---

### General/common trap: Losing solutions during row ops

**What goes wrong:** Multiplying a row by zero or swapping incorrectly.

**Correct rule:** Only swap, nonzero scale, add multiple — all reversible (except scale tracks for det).

**Prevention:** Never zero out a row and drop it without checking pivot structure.

---

### General/common trap: Free variable count = m − n

**What goes wrong:** Using equation count minus unknown count.

**Correct rule:** Free vars = **n − rank(A)**.

**Prevention:** Reduce first, count pivot columns.

---

### General/common trap: Applying Cramer's rule when det=0

**What goes wrong:** Dividing by zero or missing infinite/no solution cases.

**Correct rule:** Cramer's only when det(A)≠0 (unique solution).

**Prevention:** Check det or rank first.

---

## My Mistakes

Record your own errors after PYQs and practice. Do not pre-fill.

| Date | Source | Question | Mistake | Root Cause | Correct Rule | Prevention |
|------|--------|----------|---------|------------|--------------|------------|
| | | | | | | |
