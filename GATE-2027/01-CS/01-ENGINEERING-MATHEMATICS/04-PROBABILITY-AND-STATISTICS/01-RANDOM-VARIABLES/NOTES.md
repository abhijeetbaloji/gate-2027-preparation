# Random Variables — Learning Notes

These notes are written for **first-time learning** or relearning. For a compressed sheet, use `REVISION.md` after you have studied this file.

---

## 1. What is a random variable in GATE?

A **random variable (RV)** X assigns a real number to each outcome of a random experiment. Instead of tracking abstract outcomes ("HH", "3 on die"), we work with numbers (number of heads, die value).

GATE CS tests whether you can:

- distinguish discrete vs continuous RVs,
- read and use PMF, PDF, and CDF correctly,
- compute expectation and variance,
- apply linearity and independence rules,
- connect RVs to named distributions (Uniform, Normal, Poisson, …).

**Connection to later topics:** RVs are the foundation for **distributions** (specific PMF/PDF families), **mean/variance/SD** (summaries of X), and **conditional probability / Bayes** (updating beliefs about X given events).

---

## 2. Discrete vs continuous

### Concept

- **Discrete X:** takes countable values (0, 1, 2, … or finite set). Described by **PMF** p(x) = P(X = x).
- **Continuous X:** takes values on an interval. Described by **PDF** f(x) where P(a ≤ X ≤ b) = ∫ₐᵇ f(x) dx.

### Why the formulas differ

For discrete X, probability is assigned to **points**: P(X = 3) can be positive.

For continuous X, P(X = exact value) = 0 (infinitely many points, each with zero width). Only **intervals** have positive probability. The PDF f(x) is a **density**: probability = area under the curve, not height.

### Formal rules

| Rule | Discrete (PMF) | Continuous (PDF) |
|------|----------------|------------------|
| Non-negativity | p(x) ≥ 0 | f(x) ≥ 0 |
| Total probability | Σ p(x) = 1 | ∫_{−∞}^{∞} f(x) dx = 1 |
| Interval probability | Σ_{x∈[a,b]} p(x) | ∫ₐᵇ f(x) dx |

### Worked Example 1 — Valid PMF?

X takes values 1, 2, 3 with p(1) = 0.3, p(2) = 0.3, p(3) = 0.3.

Sum = 0.9 ≠ 1 → **not a valid PMF**.

### Worked Example 2 — Valid PDF?

f(x) = 2x on [0, 1], else 0.

∫₀¹ 2x dx = [x²]₀¹ = 1 → **valid PDF**. Note f(1) = 2 > 1 — PDF **can exceed 1**; only the integral must equal 1.

### GATE Connection

GATE often asks: "Which is a valid PDF?" or "Find k so that f(x) = kx is a PDF on [0,2]." Set the integral to 1 and solve for k.

### Common Trap

**PDF values can exceed 1.** Students reject f(x) = 3 on [0, 1/3] because "probability can't be more than 1." But ∫₀^{1/3} 3 dx = 1 — it is valid.

---

## 3. Cumulative distribution function (CDF)

### Concept

**F(x) = P(X ≤ x)** for all real x.

### Properties (both types)

1. Non-decreasing: if a < b then F(a) ≤ F(b).
2. lim_{x→−∞} F(x) = 0; lim_{x→+∞} F(x) = 1.
3. Right-continuous.

### Why CDF is useful

- P(a < X ≤ b) = F(b) − F(a).
- For continuous X: differentiate F to get f (where derivative exists).
- For discrete X: F jumps at each value; jump size = p(x).

### Worked Example 3 — From PDF to CDF

f(x) = 1/4 on [0, 4], else 0.

F(x) = 0 for x < 0; F(x) = x/4 for 0 ≤ x ≤ 4; F(x) = 1 for x > 4.

P(1 ≤ X ≤ 3) = F(3) − F(1) = 3/4 − 1/4 = **1/2**.

### GATE Connection

"F(5) = 0.7" means P(X ≤ 5) = 0.7 — not P(X = 5).

---

## 4. Expectation E[X] — why Σ x·p(x)?

### Concept

**E[X]** is the **long-run average** if the experiment is repeated many times.

### Why the formula works (discrete)

If outcome x occurs with probability p(x), its contribution to the average over N trials ≈ N·x·p(x). Divide by N → x·p(x). Sum over all x.

**E[X] = Σ x · p(x)** (discrete)  
**E[X] = ∫ x · f(x) dx** (continuous)

### Linearity — why it holds

E[aX + b] = a·E[X] + b. Scaling multiplies the average; shifting adds b to every outcome.

### Worked Example 4 — Expectation

X: values 0, 1, 2 with probs 1/4, 1/2, 1/4.

E[X] = 0·(1/4) + 1·(1/2) + 2·(1/4) = 0 + 1/2 + 1/2 = **1**.

### GATE Connection

Indicator trick: I = 1 if event occurs, 0 otherwise. Then **E[I] = P(event)**. Used in counting problems.

### Common Trap

**E[g(X)] ≠ g(E[X])** in general (Jensen's inequality). E[X²] is not (E[X])².

---

## 5. Variance — why E[X²] − (E[X])²?

### Concept

**Var(X) = E[(X − μ)²]** where μ = E[X]. Measures spread around the mean.

### Why the shortcut formula works

Expand (X − μ)² = X² − 2μX + μ². Take expectation:

E[(X−μ)²] = E[X²] − 2μ·E[X] + μ² = E[X²] − μ².

So **Var(X) = E[X²] − (E[X])²**.

### Properties

- Var(aX + b) = a²·Var(X) — shift b does not affect spread; scale a squares.
- Var(X) ≥ 0; equals 0 only if X is constant.

### Worked Example 5 — Variance from moments

E[X] = 3, E[X²] = 13.

Var(X) = 13 − 9 = **4**; SD = 2.

### GATE Connection

Given E[X] and E[X²], never recompute from definition — use the one-line subtraction.

---

## 6. Independence

### Concept

X and Y are **independent** if knowing one tells you nothing about the other:

P(X = x, Y = y) = P(X = x)·P(Y = y) (discrete; analogous for continuous).

### Why E[XY] = E[X]·E[Y]

When independent, the joint distribution factors; the double sum ∫∫ xy·f(x)f(y) dx dy splits into product of marginals.

### Why Var(X + Y) = Var(X) + Var(Y)

Covariance Cov(X,Y) = 0 when independent. General rule: Var(X+Y) = Var(X) + Var(Y) + 2·Cov(X,Y).

### Worked Example 6 — Independent sum

Var(X) = 4, Var(Y) = 9, X,Y independent.

Var(X + Y) = 4 + 9 = **13**.

### Common Trap

Var(X + Y) = Var(X) + Var(Y) requires **independence** (or at least zero covariance). Without independence, the cross term matters.

---

## 7. Functions of random variables (brief)

If Y = g(X), then:

- Discrete: P(Y = y) = Σ_{x: g(x)=y} P(X = x).
- E[g(X)] = Σ g(x)p(x) or ∫ g(x)f(x) dx — **not** g(E[X]) in general.

### GATE Connection

"If X ~ Uniform(0,1), find distribution of Y = 2X + 3" — use transformation or CDF method. Links to Uniform distribution notes.

---

## 8. Joint distributions (GATE-level)

For two RVs, **joint PMF/PDF** describes pairs (X, Y). Marginals:

p_X(x) = Σ_y p(x,y); f_X(x) = ∫ f(x,y) dy.

**Conditional PMF:** p_{X|Y}(x|y) = p(x,y) / P(Y = y) — foundation for `07-CONDITIONAL-PROBABILITY/NOTES.md`.

---

## 9. Topic links (study order)

1. **Random Variables** (this file) — PMF, PDF, CDF, E, Var.
2. **Distributions** — Uniform, Normal, Exponential, Poisson, Binomial (each gives a specific PMF/PDF).
3. **Mean** — E[X] as population/sample mean; **Median**, **Mode** as alternative centers.
4. **Standard Deviation** — √Var(X); spread in same units as data.
5. **Conditional Probability** — P(A|B); restricts sample space.
6. **Bayes Theorem** — update priors using evidence; denominator = total probability.

---

## 10. Summary checklist

- [ ] PMF sums to 1; PDF integrates to 1.
- [ ] CDF: P(X ≤ x); interval prob = F(b) − F(a).
- [ ] E[X] and Var(X) = E[X²] − E[X]².
- [ ] Linearity of expectation; variance scales with a².
- [ ] Independence → E[XY] = E[X]E[Y], Var(X+Y) = Var(X)+Var(Y).
- [ ] PDF can exceed 1; point probability is 0 for continuous X.
