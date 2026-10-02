# Standard Deviation — Learning Notes

These notes are written for **first-time learning** or relearning. For a compressed sheet, use `REVISION.md` after you have studied this file.

---

## 1. What is spread in GATE?

**Mean** (`03-MEAN/NOTES.md`) locates the centre; **variance** and **standard deviation (SD)** measure how spread out data or a distribution is around that centre.

GATE tests:
- Computing variance/SD from data or distributions
- Properties: Var(aX+b), sum of independent RVs
- Linking to every distribution (Binomial, Poisson, Normal, etc.)

---

## 2. Population vs sample

### Population (theoretical / full data)

**Variance:** σ² = (1/N) Σ (x_i − μ)²

**SD:** σ = √σ²

### Sample (GATE: read the question)

**Sample variance (unbiased):** s² = Σ(x_i − x̄)² / **(n−1)**

**Population formula:** divide by **n** instead.

GATE often uses population formula unless "sample" or "unbiased" is stated.

---

## 3. Variance from expectation

For random variable X with mean μ = E[X]:

**Var(X) = E[(X − μ)²] = E[X²] − (E[X])²**

### Derivation of computational formula

E[(X−μ)²] = E[X² − 2μX + μ²] = E[X²] − 2μE[X] + μ² = E[X²] − μ².

### Worked Example 1 — From data

Values 2, 4, 6: μ = 4.

Var = ((−2)² + 0² + 2²)/3 = 8/3. SD = **√(8/3)**.

### Worked Example 2 — From PMF

X: P(0)=0.5, P(2)=0.5. E[X]=1, E[X²]=0·0.5+4·0.5=2.

Var = 2 − 1² = **1**. SD = **1**.

---

## 4. Standard deviation definition

**σ = √Var(X)** — same units as X (easier to interpret than variance).

Var(X)=9 ⇒ SD = **3**.

---

## 5. Properties (essential for GATE)

| Property | Formula |
|----------|---------|
| Var(aX + b) | a² Var(X) |
| SD(aX + b) | \|a\| · σ |
| Var(X + Y) | Var(X) + Var(Y) if **independent** |
| SD(X + Y) | √(Var(X)+Var(Y)) if independent — **not** σ_X + σ_Y |
| Var(constant) | 0 |

### Why Var(aX+b) = a²Var(X)

Spread scales by |a|; shifting by b does not change spread.

### Worked Example 3 — Scaling

SD(X) = 4. SD(3X + 2) = 3 · 4 = **12**.

### Worked Example 4 — Sum of independent

σ_X = 3, σ_Y = 4 ⇒ SD(X+Y) = √(9+16) = **5** (not 7).

---

## 6. Distribution variances (reference)

| Distribution | Var(X) | SD(X) |
|--------------|--------|-------|
| Bernoulli(p) | p(1−p) | √(p(1−p)) |
| Binomial(n,p) | np(1−p) | √(np(1−p)) |
| Poisson(λ) | λ | √λ |
| Exponential(λ) | 1/λ² | 1/λ |
| Uniform [a,b] | (b−a)²/12 | (b−a)/√12 |
| Normal(μ,σ²) | σ² | σ |

### Worked Example 5 — Binomial

X ~ Bin(16, 0.5). Var = 16·0.5·0.5 = **4**. SD = **2**.

### Worked Example 6 — Poisson

X ~ Poisson(9). SD = √9 = **3**.

---

## 7. Chebyshev's inequality (intuition)

P(|X − μ| ≥ kσ) ≤ 1/k² — at least rough spread bound; GATE rarely computes but good context.

---

## 8. Relation to other topics

- **Mean:** centre for deviation calculation.
- **Median/Mode:** spread usually measured from mean, not median.
- **Normal:** 68-95-99.7 rule uses σ.
- **Random Variables:** E[X²] trick is the workhorse.

---

## 9. GATE Connection

- Compute Var from data or PMF using E[X²] − (E[X])².
- SD(3X+2) scaling problems.
- Independent sum: √(σ_X² + σ_Y²).
- Distribution SD: Poisson √λ, Binomial √(np(1−p)).
- N(μ, σ²) notation: σ is SD, σ² is variance.

---

## 10. Common traps

1. SD(X+Y) ≠ SD(X) + SD(Y) in general.
2. Variance additive only for **independent** (or uncorrelated) variables.
3. Confusing σ with σ² in Normal notation.
4. Wrong divisor: n vs n−1 for sample variance.
5. SD of constant = 0.

---

## 11. Summary checklist

- [ ] Var = E[X²] − (E[X])².
- [ ] σ = √Var.
- [ ] Var(aX+b) = a²Var(X).
- [ ] Independent sum: variances add.
- [ ] Know Binomial, Poisson, Uniform, Normal variances.
