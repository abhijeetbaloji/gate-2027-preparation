# Binomial Distribution — Shortcuts

Only use shortcuts **after** you understand the underlying concepts in `NOTES.md`.

---

### Shortcut: At least one

**Why it works:** 1−(1−p)^n

**When to use:** Complement

**Example:** p=0.1,n=10→1−0.9^10

**Trap / limitation:** —

---

### Shortcut: Expected count

**Why it works:** np directly

**When to use:** No PMF sum

**Example:** n=20,p=0.05→E=1

**Trap / limitation:** —

---

### Shortcut: Poisson approx

**Why it works:** λ=np when n large p small

**When to use:** Rare events

**Example:** 1000×0.002→Poi(2)

**Trap / limitation:** p must be small

---
