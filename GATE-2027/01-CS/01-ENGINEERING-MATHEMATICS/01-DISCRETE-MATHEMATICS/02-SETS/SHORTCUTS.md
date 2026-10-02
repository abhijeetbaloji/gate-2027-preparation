# Sets — Shortcuts

### Shortcut 1: Union size without drawing Venn
Add sizes, subtract intersection once. For three sets, remember **+ singles, − pairs, + triple**.

### Why it works
Inclusion–exclusion removes double-counted elements systematically.

### When to use
Any "how many know at least one of …" or divisibility-by-{2,3,5} counting.

### Example
|Java|=60, |Python|=45, |both|=25 → |either|=60+45−25=80.

### Trap/limitation
Needs correct intersection sizes; for 4+ sets full I–E is error-prone — use complement if easier.

---

### Shortcut 2: Subsets containing a specific element
If A has n elements and must contain x, answer is **2^(n−1)** (not 2^n).

### Why it works
Include x always; each other element independently in/out.

### When to use
"Subsets of {1..n} containing 7" or "must include this item".

### Example
Subsets of 10-element set containing 3: 2^9 = 512.

### Trap/limitation
If multiple forced elements, subtract from n accordingly (e.g. must contain 3 and 7 → 2^8).

---

### Shortcut 3: De Morgan first on complements
When you see \((\bigcup A_i)^c\) or nested complements, flip **union↔intersection** and complement each set **before** shading Venn.

### Why it works
Logical equivalence ¬(P∨Q) ≡ ¬P∧¬Q applied to membership.

### When to use
MCQ "which expression equals …" with complements.

### Example
\((A∪B)^c = A^c ∩ B^c\) immediately — no case split.

### Trap/limitation
Universe U must stay fixed; complement is relative to U.

---

### Shortcut 4: Complement counting ("at least one" → 1 − "none")
Count hard case via complement: \|at least one\| = \|U\| − \|none\|.

### Why it works
Partition U into "has property" and "does not".

### When to use
"At least one of A,B,C" when "none" is simpler (e.g. not divisible by 2,3, or 5).

### Example
1..1000 divisible by 2 or 3 or 5: 734; not divisible by any: 1000−734=266.

### Trap/limitation
"At least one" ≠ "exactly one" — symmetric difference counts exactly one.

---

### Shortcut 5: Power set of small sets — list don't guess
For |A|≤3, list P(A): ∅, singletons, … — catches {∅} and nested subset traps.

### Why it works
Concrete listing avoids formula misapplication on edge cases.

### When to use
P({∅}), P({1,2}), "how many elements in P(A)" with unusual A.

### Example
P({∅}) = {∅, {∅}} → 2 elements.

### Trap/limitation
Does not scale; for |A|=10 use 2^10.

