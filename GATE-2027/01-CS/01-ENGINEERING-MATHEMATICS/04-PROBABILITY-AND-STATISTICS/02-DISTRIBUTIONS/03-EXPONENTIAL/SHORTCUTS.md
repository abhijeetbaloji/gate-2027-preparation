# Exponential Distribution — Shortcuts

Only use shortcuts **after** you understand the underlying concepts in `NOTES.md`.

---

### Shortcut: Survival

**Why it works:** P(X>t)=e^{−λt}

**When to use:** Faster than 1−F(t)

**Example:** λ=0.5,t=2→e^{−1}

**Trap / limitation:** —

---

### Shortcut: Memoryless

**Why it works:** Restart clock after s waited

**When to use:** P(2 more|waited 3)=P(X>2)

**Example:** —

**Trap / limitation:** Only exponential

---

### Shortcut: Poisson link

**Why it works:** P(0 events in t)=e^{−λt}

**When to use:** Dual of Exp wait

**Example:** 6/hr, 10min→e^{−1}

**Trap / limitation:** Scale λ by t

---
