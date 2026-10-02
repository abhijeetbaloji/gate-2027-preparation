# Normal Distribution — Learning Notes

These notes are written for **first-time learning** or relearning. For a compressed sheet, use `REVISION.md` after you have studied this file.

---

## 1. What is the normal distribution?

The **normal (Gaussian)** distribution models quantities that cluster around a central value with symmetric tails: heights, measurement errors, aggregated scores.

Notation: **X ~ N(μ, σ²)** where μ = mean, σ² = variance, σ = standard deviation.

**Prerequisite:** `01-RANDOM-VARIABLES/NOTES.md`, `06-STANDARD-DEVIATION/NOTES.md`.

**Links:** Standardization connects to Z-tables; sums of normals stay normal; contrasts with Exponential (skewed) and Uniform (flat).

---

## 2. PDF and shape

### Concept

**f(x) = (1/(σ√(2π))) · exp(−(x−μ)²/(2σ²))**

Bell-shaped, symmetric about μ, tails extend to ±∞.

### Why σ matters

Larger σ → wider, flatter bell (more spread). Smaller σ → tall, narrow peak.

### Why PDF involves e^{−x²}

Arises from central limit theorem and maximum entropy among distributions with fixed variance. GATE does not require deriving the formula — know shape and parameters.

---

## 3. Standard normal Z ~ N(0, 1)

### Concept

**Z = (X − μ) / σ** transforms any N(μ, σ²) to N(0, 1).

### Why standardization works

Subtracting μ centers at 0; dividing by σ sets variance to 1. If X ~ N(μ, σ²), then E[Z] = 0, Var(Z) = 1.

### CDF Φ(z) = P(Z ≤ z)

GATE provides tables or Φ values. **P(Z > z) = 1 − Φ(z).**

### Symmetry

**P(Z > z) = P(Z < −z)** because distribution is symmetric about 0.

### Worked Example 1 — Standardization

X ~ N(100, 25) so μ = 100, σ = 5.

P(X ≤ 110) = P(Z ≤ (110−100)/5) = P(Z ≤ 2) = **Φ(2) ≈ 0.9772**.

P(X > 100) = P(Z > 0) = **0.5** (symmetry).

---

## 4. The 68–95–99.7 rule

### Concept

For X ~ N(μ, σ²):

| Interval | Approximate probability |
|----------|-------------------------|
| μ ± 1σ | ~68% |
| μ ± 2σ | ~95% |
| μ ± 3σ | ~99.7% |

### Why it helps

Quick estimates without tables when σ is known.

### Worked Example 2

Scores ~ N(70, 100), σ = 10.

"Within one SD" → P(60 ≤ X ≤ 80) ≈ **68%**.  
P(X > 90) = P(Z > 2) ≈ **2.5%** (half of 5% outside 2σ).

---

## 5. Linear transformations

### Rule

If X ~ N(μ, σ²), then **aX + b ~ N(aμ + b, a²σ²)**.

### Why variance scales with a²

Var(aX + b) = a²·Var(X) = a²σ².

### Worked Example 3

X ~ N(10, 4). Y = 3X − 5.

E[Y] = 3(10) − 5 = **25**.  
Var(Y) = 9(4) = **36** → Y ~ **N(25, 36)**.

---

## 6. Sum of independent normals

### Rule

If X ~ N(μ₁, σ₁²) and Y ~ N(μ₂, σ₂²) independent, then:

**X + Y ~ N(μ₁ + μ₂, σ₁² + σ₂²)**.

### Why GATE cares

Total error = sum of independent measurement errors → normal with added variances.

### Worked Example 4

X ~ N(0, 1), Y ~ N(0, 1) independent.

X + Y ~ N(0, **2**) — not N(0, 1).

---

## 7. σ vs σ² — critical distinction

| Symbol | Name | Units |
|--------|------|-------|
| σ² | Variance | squared units |
| σ | Standard deviation | same as X |

### Common Trap

"Variance is 9" → σ = 3, not 9. Always identify which parameter is given.

---

## 8. Tail probabilities

### Strategy

1. Standardize: z = (x − μ)/σ.
2. Use Φ table or symmetry.
3. For "between": Φ(z₂) − Φ(z₁).

### Worked Example 5

X ~ N(50, 16), σ = 4. P(46 ≤ X ≤ 54)?

z₁ = −1, z₂ = 1 → P = Φ(1) − Φ(−1) = 2Φ(1) − 1 ≈ **0.6827**.

---

## 9. Normal vs other distributions

| Situation | Better model |
|-----------|--------------|
| Symmetric, continuous, many factors | Normal |
| Waiting time until event | Exponential |
| Count of rare events | Poisson |
| Fixed n trials, success/fail | Binomial |
| Equally likely in range | Uniform |

Normal approximates Binomial when n large (not always on GATE syllabus, but useful intuition).

---

## 10. GATE Connection

- Standardize first — almost every normal question.
- Symmetry for negative z: Φ(−z) = 1 − Φ(z).
- MSQs on properties of N(μ,σ²): mean μ, mode μ, median μ (all equal for symmetric normal).
- Links to **mean** (μ), **SD** (σ), **median** (equals μ for symmetric distributions).

---

## 11. Common traps

1. Using σ² as σ in standardization.
2. Forgetting **independence** for sum of normals (variances add only when independent).
3. P(Z = z) = 0 — use intervals or P(Z ≤ z).
4. Confusing P(X > a) with P(X < a) — draw sketch or standardize.

---

## 12. Summary checklist

- [ ] X ~ N(μ, σ²): bell-shaped, symmetric about μ.
- [ ] Z = (X−μ)/σ ~ N(0,1).
- [ ] aX+b ~ N(aμ+b, a²σ²).
- [ ] Independent sum: means add, variances add.
- [ ] 68–95–99.7 rule for quick estimates.
- [ ] Tail symmetry: P(Z > z) = P(Z < −z).
