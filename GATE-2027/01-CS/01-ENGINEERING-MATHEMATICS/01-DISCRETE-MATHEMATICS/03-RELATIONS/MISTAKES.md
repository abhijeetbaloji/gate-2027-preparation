# Relations — Mistakes

## Common Mistakes

### General/common trap: Empty relation not reflexive on nonempty set

**What goes wrong:** Claiming ∅ on {1,2,3} is reflexive.

**Correct rule:** Need (1,1),(2,2),(3,3) — all missing.

**Prevention:** Reflexive requires **every** diagonal pair.

---

### General/common trap: Symmetric + transitive implies reflexive (false)

**What goes wrong:** "R symmetric and transitive so reflexive."

**Correct rule:** Counterexample: R=∅ on {1,2} — symmetric and transitive vacuously, **not reflexive**.

**Prevention:** Test with empty or partial diagonal.

---

### General/common trap: Antisymmetric vs asymmetric

**What goes wrong:** Using "antisymmetric" when meaning "asymmetric."

**Correct rule:** Antisymmetric allows (a,a); asymmetric forbids (a,b) and (b,a) for a≠b.

**Prevention:** Read definition word-by-word.

---

### General/common trap: Wrong relation count

**What goes wrong:** 2^n relations instead of 2^(n²).

**Correct rule:** Choose any subset of n² ordered pairs.

**Prevention:** n=2 → should get 2⁴=16, not 4.

---

### General/common trap: Composition order reversed

**What goes wrong:** Computing R∘S when question defines S∘R.

**Correct rule:** Read "R followed by S" vs matrix convention carefully.

**Prevention:** Write one example pair manually.

---

## My Mistakes

| Date | Source | Question | Mistake | Root Cause | Correct Rule | Prevention |
|------|--------|----------|---------|------------|--------------|------------|
| | | | | | | |
