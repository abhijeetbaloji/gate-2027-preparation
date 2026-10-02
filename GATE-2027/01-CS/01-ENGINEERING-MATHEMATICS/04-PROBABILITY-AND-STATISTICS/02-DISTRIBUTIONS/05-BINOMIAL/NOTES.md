# Binomial Distribution — Learning Notes

These notes are written for **first-time learning** or relearning. For a compressed sheet, use `REVISION.md` after you have studied this file.

---

## 1. What models the binomial distribution?

The **binomial** distribution counts **successes in n independent trials**, each with the same success probability p.

Notation: **X ~ Bin(n, p)**.

**Prerequisite:** `01-RANDOM-VARIABLES/NOTES.md`.

**Links:** Sum of n Bernoulli(p) trials; approximates to `04-POISSON/NOTES.md` when n large, p small; contrasts with Normal for large n (not always required at GATE).

---

## 2. Setup — four conditions (Bernoulli trials)

1. Fixed number of trials **n**.
2. Each trial: **success** (prob p) or **failure** (prob 1−p).
3. Trials are **independent**.
4. **p is constant** across trials.

If any condition fails, binomial may not apply (e.g., sampling without replacement → hypergeometric — rare at GATE).

---

## 3. PMF — why C(n,k) p^k (1−p)^{n−k}?

### Formula

**P(X = k) = C(n,k) · p^k · (1−p)^{n−k}** for k = 0, 1, …, n.

### Why it works

- Choose which k of n trials succeed: **C(n,k)** ways.
- Probability of one specific sequence with k successes: **p^k (1−p)^{n−k}**.
- Multiply: count × probability per sequence.

### Worked Example 1 — Fair coin

10 flips, p = 1/2. P(X = 5) = C(10,5) · (1/2)^10 = 252/1024 ≈ **0.246**.

---

## 4. Mean and variance

### Formulas

**E[X] = np**  
**Var(X) = np(1−p)**

### Why E[X] = np

X = I₁ + I₂ + … + Iₙ where each Iᵢ ~ Bernoulli(p), E[Iᵢ] = p.

By linearity: E[X] = np.

### Why Var(X) = np(1−p)

Var of Bernoulli is p(1−p); independent sum → variances add → n·p(1−p).

### Worked Example 2

20 items, each defective with p = 0.05.

E[X] = **1**; Var(X) = 20·0.05·0.95 = **0.95**.

---

## 5. "At least one success"

### Formula

**P(X ≥ 1) = 1 − P(X = 0) = 1 − (1−p)^n**.

### Why complement is faster

Avoid summing k = 1 to n terms.

### Worked Example 3

10 trials, p = 0.1. P(at least one success) = 1 − 0.9^10 ≈ **0.651**.

---

## 6. Mode of binomial

### Rule (approximate)

Mode ≈ **⌊(n+1)p⌋** (floor of (n+1)p).

At boundaries (e.g., (n+1)p integer), two adjacent values may tie for maximum probability.

### Why

PMF increases while (n−k+1)p > k(1−p), then decreases — peak near np.

### Worked Example 4

n = 10, p = 0.3. (n+1)p = 3.3 → mode ≈ **3**.

---

## 7. Binomial vs Poisson approximation

### When to approximate

**Bin(n, p) ≈ Poisson(λ = np)** when n is large, p is small, λ = np is moderate.

### Why

Rare events in many trials → Poisson limit (see `04-POISSON/NOTES.md` §5).

### Worked Example 5

n = 500, p = 0.004, λ = 2.

P(X = 0) ≈ e^{−2} ≈ 0.135 (Poisson); exact binomial ≈ 0.134 — close.

### When to keep binomial

n small, or p not near 0 — e.g., n = 10, p = 0.5.

---

## 8. Relation to Bernoulli

**Bernoulli(p)** is Bin(1, p): one trial, X ∈ {0, 1}.

**Bin(n, p) = sum of n i.i.d. Bernoulli(p)**.

---

## 9. GATE Connection

- Identify from "n trials," "independent," "probability p each."
- E[X] = np for expected count of successes.
- Complement for "at least one."
- Approximate with Poisson when n large, p small.
- Links to **mean** (np) and **variance** / **SD** (√(np(1−p))).

---

## 10. Common traps

1. Trials must be **independent** — "without replacement" changes model.
2. p is success probability, not failure — read carefully.
3. k must be integer 0 ≤ k ≤ n.
4. Using Poisson when p is not small (e.g., p = 0.5, n = 10).

---

## 11. Comparison table

| | Binomial | Poisson | Exponential |
|---|----------|---------|-------------|
| Variable | Count (0..n) | Count (0,1,2,…) | Time (≥0) |
| Parameters | n, p | λ | λ (rate) |
| E[X] | np | λ | 1/λ |
| Var(X) | np(1−p) | λ | 1/λ² |

---

## 12. Summary checklist

- [ ] P(X=k) = C(n,k)p^k(1−p)^{n−k}.
- [ ] E[X]=np, Var(X)=np(1−p).
- [ ] P(X≥1) = 1−(1−p)^n.
- [ ] Mode ≈ ⌊(n+1)p⌋.
- [ ] Large n, small p → Poisson(np).
- [ ] Sum of n Bernoulli(p).
