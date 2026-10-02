# Relations — Shortcuts

---

### Shortcut: Reflexive check — scan diagonal first

**Why it works:** Reflexive iff every (a,a) present.

**When to use:** Any property question on small finite set.

**Example:** Missing (3,3) → **not reflexive** immediately.

**Trap / limitation:** Don't stop there — may need other properties too.

---

### Shortcut: Transitive failure — hunt a→b→c without a→c

**Why it works:** Transitivity only fails on length-2 paths.

**When to use:** Verify transitive on 3–5 element sets.

**Example:** (1,2),(2,3)∈R but (1,3)∉R → **not transitive**.

**Trap / limitation:** Longer paths reduce to checking transitive closure edges.

---

### Shortcut: Reflexive relation count = 2^(n²−n)

**Why it works:** n diagonal pairs forced; remaining n²−n free.

**When to use:** "How many reflexive relations on n elements?"

**Example:** n=3 → 2⁶ = **64**.

**Trap / limitation:** "Reflexive and symmetric" uses 2^(n(n−1)/2) instead.

---

### Shortcut: Equivalence classes from digraph

**Why it works:** E.R. components are strongly connected with bidirectional edges.

**When to use:** Find partition from given relation.

**Example:** {1,2} mutually related, {3} alone → classes {1,2}, {3}.

**Trap / limitation:** Must verify E.R. first — invalid partition if not.

---

### Shortcut: Matrix — reflexive iff diagonal all 1

**Why it works:** Direct definition.

**When to use:** Quick MCQ elimination on matrix options.

**Trap / limitation:** Symmetric needs M = M^T; antisymmetric needs M∧M^T ⊆ I.
