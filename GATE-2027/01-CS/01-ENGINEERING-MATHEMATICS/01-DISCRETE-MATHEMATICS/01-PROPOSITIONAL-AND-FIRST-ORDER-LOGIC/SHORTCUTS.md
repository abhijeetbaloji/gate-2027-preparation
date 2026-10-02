# Propositional and First-Order Logic — Shortcuts

### Shortcut
P→Q is automatically T when P=F or Q=T.

### Why it works
Implication is false only at (T,F); all other rows are T by definition.

### When to use
Quick truth-value checks without building full table.

### Example
P=F, Q=F: P→Q = T (vacuously true).

### Trap/limitation
Does not mean P causes Q — only truth-functional shortcut.

---

### Shortcut
To test tautology, try the all-F assignment first.

### Why it works
If formula is F when all vars are F, it cannot be a tautology — eliminates options fast.

### When to use
MCQ "which is a tautology?" with 4 options.

### Example
(P→Q)→P: at P=F,Q=F → (T)→F = F. Not a tautology.

### Trap/limitation
Passing all-F test doesn't prove tautology — need all rows or proof.

---

### Shortcut
Convert (A→B) to CNF directly as (¬A∨B).

### Why it works
A→B ≡ ¬A∨B is already a single clause.

### When to use
CNF conversion; avoid full distribution when possible.

### Example
(P∧Q)→R becomes ¬(P∧Q)∨R = (¬P∨¬Q∨R) — one clause.

### Trap/limitation
Nested implications need repeated application.

---

### Shortcut
¬(P→Q) = P∧¬Q in one step.

### Why it works
Derived from ¬(¬P∨Q) = P∧¬Q.

### When to use
Negating implications in equivalence problems.

### Example
¬(x>0 → x²>0) ≡ (x>0)∧¬(x²>0) — find counterexample x.

### Trap/limitation
Do not confuse with contrapositive.

---

### Shortcut
"All A are B" in FOL: ∀x(A(x)→B(x)), not ∀x(A(x)∧B(x)).

### Why it works
Universal claim is vacuously true for non-A objects with →; ∧ would require everything to be A.

### When to use
Every FOL translation question.

### Example
"All cats are mammals" = ∀x(Cat(x)→Mammal(x)).

### Trap/limitation
"Some A are B" needs ∃x(A(x)∧B(x)) — different connective inside.
