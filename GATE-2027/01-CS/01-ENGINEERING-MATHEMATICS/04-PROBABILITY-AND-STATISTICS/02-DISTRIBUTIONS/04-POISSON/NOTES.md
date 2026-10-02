# Poisson Distribution — Learning Notes

These notes are written for **first-time learning** or relearning. For a compressed sheet, use `REVISION.md` after you have studied this file.

---

## 1. What models the Poisson distribution?

The **Poisson** distribution models **counts of rare, independent events** in a fixed interval of time or space — e.g., number of typos per page, packets per second, customers per hour.

Notation: **X ~ Poisson(λ)** where λ > 0 is the **average count** in the stated interval.

**Prerequisite:** `01-RANDOM-VARIABLES/NOTES.md`, `05-BINOMIAL/NOTES.md` (Poisson as limit).

**Links:** Dual of `03-EXPONENTIAL/NOTES.md` (count vs wait). Mean connects to `03-MEAN/NOTES.md`.

---

## 2. PMF — why e^{−λ} λ^k / k!?

### Formula

**P(X = k) = e^{−λ} · λ^k / k!** for k = 0, 1, 2, …

### Why this form (intuition)

Poisson arises as limit of Binomial(n, p) when n → ∞, p → 0, np = λ fixed:

- (1−p)^n ≈ e^{−np} = e^{−λ} (since p = λ/n).
- C(n,k) p^k (1−p)^{n−k} → e^{−λ} λ^k / k!.

So Poisson models **many trials, tiny success probability, fixed expected count λ**.

### Why e^{−λ} appears

Normalizing constant: Σ_{k=0}^∞ e^{−λ} λ^k/k! = e^{−λ} · e^λ = 1.

### Worked Example 1 — Basic PMF

X ~ Poisson(λ = 3). P(X = 0) = e^{−3} ≈ **0.050**.

P(X = 2) = e^{−3} · 9/2 ≈ **0.224**.

---

## 3. Mean = variance — the hallmark

### Formulas

**E[X] = λ**  
**Var(X) = λ**

### Why mean equals variance

Derived from PMF: E[X] = Σ k·P(X=k) = λ and E[X²] − E[X]² = λ.

**If a GATE question says E[X] = Var(X), think Poisson first.**

### Worked Example 2 — Identification

"Discrete RV with E[X] = 4 and Var(X) = 4." → likely **Poisson(4)**.

---

## 4. Poisson process and time scaling

### Rule

If events occur at rate λ per unit time, then count in interval of length **t** is:

**Poisson(λt)**.

### Why λ multiplies by t

Doubling the window doubles the expected number of events.

### Worked Example 3 — Time scaling

Emails arrive at 4/hour. P(0 emails in 15 minutes)?

t = 0.25 hr, λt = 1. P(X=0) = e^{−1} ≈ **0.368**.

### Common Trap

Forgetting to scale λ when the interval changes (minutes vs hours).

---

## 5. Binomial approximation to Poisson

### Rule

**Binomial(n, p) ≈ Poisson(λ)** when n large, p small, **λ = np** held moderate.

Typical rule of thumb: n ≥ 20, p ≤ 0.05, np < 10 (guideline, not rigid).

### Why it works

Rare events in many trials → Poisson limit (see §2 derivation).

### Worked Example 4 — Approximation

1000 trials, p = 0.002. Exact: Bin(1000, 0.002). Approximate: **Poisson(2)**.

P(X = 0) ≈ e^{−2} ≈ 0.135 (exact binomial very close).

### When NOT to approximate

n small or p not small — use exact binomial.

---

## 6. Useful derived formulas

| Event | Formula | Why |
|-------|---------|-----|
| P(X = 0) | e^{−λ} | Plug k=0 into PMF |
| P(X ≥ 1) | 1 − e^{−λ} | Complement of zero |
| P(X ≤ 1) | e^{−λ}(1 + λ) | Sum k=0,1 |

### Worked Example 5 — At least one

λ = 2. P(X ≥ 1) = 1 − e^{−2} ≈ **0.865**.

Don't sum infinite series when complement is faster.

---

## 7. Sum of independent Poissons

If X ~ Poisson(λ₁), Y ~ Poisson(λ₂) independent, then:

**X + Y ~ Poisson(λ₁ + λ₂)**.

### Why

Counts in non-overlapping intervals of a Poisson process add; combined rate is sum of rates.

### Worked Example 6

Accidents on road A: Poisson(3); road B: Poisson(5); independent.

Total accidents ~ **Poisson(8)**. P(total = 0) = e^{−8}.

---

## 8. Poisson vs Binomial vs Exponential

| Question type | Distribution |
|---------------|--------------|
| # successes in n fixed trials, prob p | Binomial |
| # events in interval, rare events | Poisson |
| Time until next event | Exponential |

---

## 9. GATE Connection

- **Mean = variance** identification.
- Scale λ by interval length.
- P(X=0) = e^{−λ} — fastest single probability.
- Bin(n,p) → Poisson(np) approximation.
- Sum of Poissons → Poisson(sum of λs).

---

## 10. Common traps

1. λ must be **positive**; k is non-negative **integer**.
2. Confusing **rate per hour** with count in **given** interval — multiply by t.
3. Using Poisson when trials are not independent or p is not small.
4. Summing PMF for P(X≥1) instead of 1 − e^{−λ}.

---

## 11. Summary checklist

- [ ] PMF: e^{−λ}λ^k/k!, k = 0,1,2,…
- [ ] E[X] = Var(X) = λ.
- [ ] Interval length t → Poisson(λt).
- [ ] Bin(n,p) ≈ Poisson(np) for large n, small p.
- [ ] P(X≥1) = 1 − e^{−λ}.
- [ ] Independent sums → Poisson(λ₁+λ₂).
