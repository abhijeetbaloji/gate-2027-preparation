# Exponential Distribution — Learning Notes

These notes are written for **first-time learning** or relearning. For a compressed sheet, use `REVISION.md` after you have studied this file.

---

## 1. What models the exponential distribution?

The **exponential** distribution models **waiting time until the next event** when events occur randomly at a constant rate — e.g., time until next packet arrival, next failure, next customer.

Notation: **X ~ Exp(λ)** with rate λ > 0 (events per unit time).

**Prerequisite:** `01-RANDOM-VARIABLES/NOTES.md`, `04-POISSON/NOTES.md` (dual of Poisson counting).

**Links:** Poisson counts events; Exponential times between events. Memoryless property is unique to Exponential (among continuous distributions on [0,∞)).

---

## 2. PDF and CDF

### Formulas

**PDF:** f(x) = λe^{−λx} for x ≥ 0, else 0.

**CDF:** F(x) = P(X ≤ x) = 1 − e^{−λx} for x ≥ 0.

### Why f(x) = λe^{−λx}

- f(0) = λ (most likely to happen "soon" if rate is high).
- Decreasing density: longer waits become less likely.
- ∫₀^∞ λe^{−λx} dx = 1 ✓

### Why CDF = 1 − e^{−λx}

P(X > x) = e^{−λx} — survival function. CDF is complement.

### Worked Example 1 — Basic probability

X ~ Exp(λ = 0.5 per hour). P(X > 2 hours)?

P(X > 2) = e^{−0.5×2} = e^{−1} ≈ **0.368**.

P(X ≤ 2) = 1 − e^{−1} ≈ **0.632**.

---

## 3. Mean and variance — why E[X] = 1/λ

### Formulas

**E[X] = 1/λ**  
**Var(X) = 1/λ²**  
SD = 1/λ = E[X]

### Why mean is reciprocal of rate

If λ = 2 events/hour on average, average wait = 1/2 hour between events.

Integration: E[X] = ∫₀^∞ x·λe^{−λx} dx = 1/λ (integration by parts).

### Parameter confusion

Some texts use **β = 1/λ** as the **mean** directly. Read the question:

- "Rate λ = 3" → mean = 1/3.
- "Mean β = 5" → λ = 1/5, f(x) = (1/5)e^{−x/5}.

### Worked Example 2 — Identify parameter

"The mean time to failure is 10 hours."

λ = 1/10 = 0.1/hr. P(fail within 5 hr) = 1 − e^{−0.5} ≈ **0.393**.

---

## 4. Memoryless property — deep treatment

### Statement

**P(X > s + t | X > s) = P(X > t)** for all s, t ≥ 0.

"If you've already waited s units, the additional wait has the same distribution as starting fresh."

### Why it holds for exponential

P(X > s+t | X > s) = P(X > s+t) / P(X > s) = e^{−λ(s+t)} / e^{−λs} = e^{−λt} = P(X > t).

### Intuition

Constant hazard rate: at every instant, the "chance of event in next instant" doesn't depend on how long you've waited.

### GATE Connection

"If machine has run 3 hours without failure, P(run 2 more hours)?" → same as P(X > 2) for fresh machine — **memoryless**.

### Common Trap

Normal and Uniform are **not** memoryless. Only Exponential (on [0,∞)) has this property among continuous distributions tested in GATE.

---

## 5. Relation to Poisson process

### Dual relationship

| Poisson | Exponential |
|---------|-------------|
| Count events in time t | Time until next event |
| X ~ Poisson(λt) | Inter-arrival ~ Exp(λ) |
| E[count] = λt | E[wait] = 1/λ |

### Why they pair

In a Poisson process with rate λ:

- Number of events in interval [0, t] ~ Poisson(λt).
- Time until first event ~ Exp(λ).
- Times between consecutive events are i.i.d. Exp(λ).

### Worked Example 3 — Poisson ↔ Exponential

Calls arrive at rate 6/hour (λ = 6). P(no call in next 10 min)?

10 min = 1/6 hr. P(X > 1/6) = e^{−6×(1/6)} = e^{−1} ≈ **0.368**.

Equivalently: count in 1/6 hr ~ Poisson(1); P(0) = e^{−1} — same answer.

---

## 6. Minimum of independent exponentials

If X₁, X₂ independent Exp(λ₁), Exp(λ₂), then min(X₁, X₂) ~ Exp(λ₁ + λ₂).

**Why:** First event from either stream; combined rate adds.

GATE occasional twist: "Two servers, each Exp(λ); time until first completion."

---

## 7. Support and modeling constraints

- Support: **x ≥ 0 only**. Negative waiting times impossible.
- λ > 0. If question gives negative λ, re-read — likely mean β was given.

---

## 8. GATE Connection

- Identify Exp from "constant rate," "memoryless," "time until."
- Convert between λ and mean β = 1/λ.
- Pair with Poisson for count-vs-time problems.
- CDF form 1 − e^{−λx} for "within t" questions.

---

## 9. Comparison table

| Property | Exponential | Normal | Uniform |
|----------|-------------|--------|---------|
| Support | [0, ∞) | (−∞, ∞) | [a, b] |
| Skew | Right-skewed | Symmetric | Flat |
| Memoryless | Yes | No | No |
| Parameters | λ (rate) | μ, σ² | a, b |

---

## 10. Common traps

1. Using λ when problem gives **mean** (or vice versa).
2. Applying memoryless to non-exponential distributions.
3. Integrating PDF over wrong bounds (starts at 0).
4. Forgetting time unit scaling (minutes vs hours changes λ).

---

## 11. Summary checklist

- [ ] f(x) = λe^{−λx}, x ≥ 0; F(x) = 1 − e^{−λx}.
- [ ] E[X] = 1/λ; Var(X) = 1/λ².
- [ ] Memoryless: P(X>s+t | X>s) = P(X>t).
- [ ] Poisson(λt) counts ↔ Exp(λ) waits.
- [ ] P(X > t) = e^{−λt}.
