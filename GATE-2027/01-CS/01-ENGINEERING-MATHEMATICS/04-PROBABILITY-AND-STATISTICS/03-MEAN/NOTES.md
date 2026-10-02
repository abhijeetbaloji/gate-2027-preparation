# Mean — Learning Notes

These notes are written for **first-time learning** or relearning. For a compressed sheet, use `REVISION.md` after you have studied this file.

---

## 1. What is the mean in GATE?

The **mean** (average) is the primary measure of **central tendency** — the "balance point" of data or a distribution.

Two contexts in GATE:

1. **Sample / population mean** of observed data: x̄ or μ.
2. **Expectation E[X]** — mean of a random variable (theoretical).

**Prerequisite:** `01-RANDOM-VARIABLES/NOTES.md` (expectation).

**Links:** Compare with `04-MEDIAN/NOTES.md` and `05-MODE/NOTES.md`; spread measured by `06-STANDARD-DEVIATION/NOTES.md`; distribution means in `02-DISTRIBUTIONS/`.

---

## 2. Sample and population mean

### Formulas

**Arithmetic mean:** x̄ = (1/n) Σᵢ xᵢ = (x₁ + x₂ + … + xₙ) / n.

**Population mean** (if all N members): μ = (1/N) Σ xᵢ — same formula, different notation.

### Why divide by n

Mean = total / count. Each observation contributes equally.

### Worked Example 1 — Data mean

Scores: 4, 7, 7, 10. n = 4.

x̄ = (4+7+7+10)/4 = 28/4 = **7**.

---

## 3. Expectation E[X] — distribution mean

### Discrete

**E[X] = Σ x · p(x)** — probability-weighted average of values.

### Continuous

**E[X] = ∫ x · f(x) dx**.

### Why E[X] is "the" mean of a distribution

If you repeat the experiment infinitely, the sample average converges to E[X] (law of large numbers — intuition for GATE).

### Worked Example 2 — From PMF

X: P(X=1)=0.2, P(X=2)=0.5, P(X=3)=0.3.

E[X] = 1·0.2 + 2·0.5 + 3·0.3 = 0.2+1.0+0.9 = **2.1**.

---

## 4. Linearity of expectation

### Rule

**E[aX + b] = a·E[X] + b**.

**E[X + Y] = E[X] + E[Y]** — always, even if X,Y dependent.

### Why linearity holds

Expectation is a weighted sum; scaling and shifting scale/shift the sum; sum of expectations is expectation of sum (algebra).

### Worked Example 3

E[X] = 4. Y = 3X − 2.

E[Y] = 3(4) − 2 = **10**.

### GATE Connection

Linearity works **without independence** — unlike variance.

---

## 5. Weighted mean

### Formula

**x̄_w = Σ wᵢ xᵢ / Σ wᵢ**.

### Why

When observations have different importance (e.g., exam: homework 20%, final 80%).

### Worked Example 4

Homework 80 (weight 2), final 60 (weight 3).

Weighted mean = (2·80 + 3·60)/(2+3) = (160+180)/5 = **68**.

---

## 6. Mean of named distributions (quick reference)

| Distribution | E[X] |
|--------------|------|
| Uniform {a,…,b} | (a+b)/2 |
| Uniform [a,b] | (a+b)/2 |
| Binomial(n,p) | np |
| Poisson(λ) | λ |
| Exponential(λ) | 1/λ |
| Normal(μ,σ²) | μ |

See respective `02-DISTRIBUTIONS/*/NOTES.md` for derivations.

---

## 7. Mean vs median vs mode

| Measure | Sensitive to outliers? | Use when |
|---------|------------------------|----------|
| Mean | Yes | Symmetric data, need for variance |
| Median | No | Skewed data |
| Mode | N/A | Most frequent category |

### Worked Example 5 — Outlier effect

Data: 1, 2, 3, 4, 100.

Mean = 110/5 = **22** (pulled up by 100).  
Median = **3** (middle value). See `04-MEDIAN/NOTES.md`.

---

## 8. Mean of grouped data

If values xᵢ have frequencies fᵢ:

**x̄ = Σ fᵢ xᵢ / Σ fᵢ**.

Same as weighted mean with weights = frequencies.

---

## 9. Pitfall — mean of means

### Trap

Average of group means equals overall mean **only if group sizes are equal** (or use weighted average).

### Correct

Overall mean = (n₁x̄₁ + n₂x̄₂) / (n₁ + n₂).

### Worked Example 6

Class A: 10 students, mean 70. Class B: 30 students, mean 80.

Overall = (10·70 + 30·80)/40 = (700+2400)/40 = **77.5** — not (70+80)/2 = 75.

---

## 10. GATE Connection

- Distinguish x̄ (sample) from μ or E[X] (population/distribution).
- Linearity: E[aX+b], E[X+Y] without independence.
- Distribution-specific means (np, λ, 1/λ, μ).
- Weighted mean in applied word problems.
- Links to **variance**: need E[X] and E[X²] for Var(X).

---

## 11. Common traps

1. Forgetting to **order** data is not needed for mean (unlike median).
2. Using arithmetic mean of group means with unequal sizes.
3. Confusing E[X] with most likely value (mode).
4. E[g(X)] ≠ g(E[X]) — e.g., E[X²] ≠ (E[X])².

---

## 12. Summary checklist

- [ ] x̄ = Σxᵢ/n; E[X] = Σx·p(x) or ∫x·f(x)dx.
- [ ] E[aX+b] = aE[X]+b; E[X+Y] = E[X]+E[Y] always.
- [ ] Weighted mean = Σwᵢxᵢ/Σwᵢ.
- [ ] Mean sensitive to outliers.
- [ ] Know E[X] for standard distributions.
