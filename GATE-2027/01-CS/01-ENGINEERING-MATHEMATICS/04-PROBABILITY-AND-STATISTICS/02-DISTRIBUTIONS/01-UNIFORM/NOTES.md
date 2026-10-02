# Uniform Distribution — Learning Notes

These notes are written for **first-time learning** or relearning. For a compressed sheet, use `REVISION.md` after you have studied this file.

---

## 1. What is uniform distribution?

When every outcome in a range is **equally likely**, the random variable is **uniform**.

GATE tests:

- discrete uniform on {a, a+1, …, b},
- continuous uniform on [a, b],
- mean, variance, and interval probabilities.

**Prerequisite:** `01-RANDOM-VARIABLES/NOTES.md` (PMF, PDF, E[X], Var).

**Links forward:** Uniform is the simplest continuous model; Normal generalizes "bell-shaped" data; expectation formulas connect to `03-MEAN/NOTES.md`.

---

## 2. Discrete uniform

### Concept

X takes values a, a+1, …, b with **equal** probability.

n = b − a + 1 values → **P(X = k) = 1/n** for each k.

### Why E[X] = (a + b) / 2

By symmetry, the average of equally spaced integers from a to b is the midpoint. Algebraically:

E[X] = (1/n) Σ_{k=a}^{b} k = (a+b)/2.

Special case: die {1,…,6} → E[X] = 3.5.

### Why Var(X) = (n² − 1) / 12

Derived from E[X²] − E[X]² using sum of squares formula. For {1,…,n}: Var = (n²−1)/12.

### Worked Example 1 — Fair die

X ~ uniform on {1,2,3,4,5,6}. n = 6.

E[X] = (1+6)/2 = **3.5**.  
Var(X) = (36−1)/12 = **35/12 ≈ 2.92**.

P(X ≥ 5) = P(X=5) + P(X=6) = 2/6 = **1/3**.

### GATE Connection

"Pick a random integer from 1 to 100" → discrete uniform; P(even) = 50/100 = 1/2.

---

## 3. Continuous uniform on [a, b]

### Concept

X is equally likely anywhere on the interval [a, b].

**PDF:** f(x) = 1/(b−a) for x ∈ [a, b], else 0.

Height = 1/(length) so that total area = 1.

### Why E[X] = (a + b) / 2

Same symmetry argument: center of mass of a flat rectangle is the midpoint.

E[X] = ∫ₐᵇ x · (1/(b−a)) dx = (a+b)/2.

### Why Var(X) = (b − a)² / 12

Integrate (x − μ)² · f(x). Result: variance grows with **square** of interval length.

### CDF

F(x) = 0 for x < a; F(x) = (x−a)/(b−a) for a ≤ x ≤ b; F(x) = 1 for x > b.

**Linear** on [a, b] — characteristic of uniform.

### Worked Example 2 — Bus waiting time

Bus arrives uniformly between 0 and 20 minutes. X ~ Uniform(0, 20).

P(X ≤ 5) = 5/20 = **0.25**.  
P(8 ≤ X ≤ 12) = (12−8)/20 = **0.2**.  
E[X] = **10** minutes.

### Worked Example 3 — Find missing endpoint

X ~ Uniform(a, 10), E[X] = 7.

(a+10)/2 = 7 → a = **4**.

---

## 4. Why length is (b − a), not (b − a + 1)

### Concept

**Discrete:** n = b − a + 1 (count integers inclusively).  
**Continuous:** length = b − a (no +1).

### Common Trap

Using die formula (n²−1)/12 with n = b−a for continuous uniform. Continuous uses **(b−a)²/12**.

---

## 5. Probability = proportion of interval

For continuous uniform on [a, b]:

**P(c ≤ X ≤ d) = (d − c) / (b − a)** when [c,d] ⊆ [a,b].

### Why it works

Probability = area under flat PDF = height × width = (1/(b−a)) × (d−c).

### Worked Example 4

X ~ Uniform(2, 8). P(X > 6) = (8−6)/(8−2) = 2/6 = **1/3**.

---

## 6. Transformations

If X ~ Uniform(0, 1) and Y = a + (b−a)X, then Y ~ Uniform(a, b).

**Why:** Linear map of uniform is uniform on the image interval. Used in random number generation.

---

## 7. Relation to other distributions

| Distribution | Relation to Uniform |
|--------------|---------------------|
| Normal | Limit of sums; not flat |
| Exponential | Waiting time; decreasing PDF |
| Binomial | Discrete; not equal probs unless p=1/2 on 2 outcomes |

Uniform on [0,1] is the **building block** for simulating other distributions (inverse transform method — beyond GATE scope but good intuition).

---

## 8. GATE Connection

- Interval probability without integration: **ratio of lengths**.
- "Equally likely" keyword → uniform.
- Compare mean of discrete {1,…,n} vs continuous [0,n]: both have midpoint mean but different variance formulas.

---

## 9. Common traps

1. **P(X = x) = 0** for continuous X — only intervals matter.
2. Confusing **n** (count) with **b−a** (length).
3. PDF is 0 outside [a,b]; don't integrate over wrong bounds.
4. All values equally likely in discrete uniform → every value is a **mode** (see `05-MODE/NOTES.md`).

---

## 10. Summary checklist

- [ ] Discrete: P(X=k) = 1/n, E = (a+b)/2, Var = (n²−1)/12.
- [ ] Continuous: f(x) = 1/(b−a), E = (a+b)/2, Var = (b−a)²/12.
- [ ] P(c ≤ X ≤ d) = (d−c)/(b−a) for continuous uniform.
- [ ] CDF is linear on [a,b].
