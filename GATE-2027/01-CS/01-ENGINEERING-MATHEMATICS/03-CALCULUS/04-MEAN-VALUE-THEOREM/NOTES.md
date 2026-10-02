# Mean Value Theorem — Learning Notes

These notes are written for **first-time learning** or relearning. For a compressed sheet, use `REVISION.md` after you have studied this file.

---

## 1. Why MVT matters in GATE

The **Mean Value Theorem (MVT)** guarantees a point where the instantaneous rate of change equals the average rate of change over an interval. It connects:

- **Continuity** and **differentiability** (`02-CONTINUITY-AND-DIFFERENTIABILITY/NOTES.md`)
- **Maxima/minima** (Rolle is a special case)
- Existence proofs ("there exists c such that f'(c) = k")

GATE asks: state hypotheses, find c, apply Rolle/MVT, estimate function values from derivative bounds.

---

## 2. Rolle's theorem (special case)

**Hypotheses:**
1. f continuous on **[a, b]**
2. f differentiable on **(a, b)**
3. **f(a) = f(b)**

**Conclusion:** ∃ c ∈ **(a, b)** such that **f'(c) = 0**.

### Geometric meaning

If start and end at same height, somewhere the tangent is horizontal (parallel to x-axis).

### Worked Example 1

f(x) = x² − 4x + 3 on [1, 3].

f(1) = 0, f(3) = 0. f' = 2x − 4.

Rolle ⇒ ∃ c: 2c − 4 = 0 ⇒ **c = 2** ∈ (1, 3). ✓

### Worked Example 2 — When Rolle fails

f(x) = |x| on [−1, 1]. f(−1) = f(1) but f not differentiable at 0 — Rolle **does not apply** (hypothesis fails).

---

## 3. Lagrange Mean Value Theorem

**Hypotheses:**
1. f continuous on **[a, b]**
2. f differentiable on **(a, b)**

**Conclusion:** ∃ c ∈ **(a, b)** such that

**f'(c) = (f(b) − f(a)) / (b − a)**

### Geometric meaning

Some tangent is **parallel to the secant** joining (a, f(a)) and (b, f(b)).

### Derivation idea (sketch)

Define auxiliary g(x) = f(x) − [(f(b)−f(a))/(b−a)]·(x−a).

Then g(a) = g(b). Apply Rolle to g ⇒ g'(c) = 0 ⇒ f'(c) = secant slope.

### Worked Example 3

f(x) = x² on [1, 3].

Secant slope = (9 − 1)/(3 − 1) = 4.

f'(c) = 2c = 4 ⇒ **c = 2** ∈ (1, 3).

### Worked Example 4 — Existence only

f continuous on [0, 5], f(0) = 2, f(5) = 12.

MVT ⇒ some c with f'(c) = (12−2)/5 = **2** (we don't need to find c).

---

## 4. Cauchy Mean Value Theorem (generalization)

If f, g continuous on [a,b], differentiable on (a,b), and g'(x) ≠ 0 on (a,b):

∃ c ∈ (a,b): **f'(c)/g'(c) = (f(b)−f(a))/(g(b)−g(a))**.

Rare in GATE but know the name if mentioned.

---

## 5. Applications in GATE

### 5.1 Prove f'(c) = k for some c

Use MVT directly on [a,b] if average slope equals k.

### 5.2 Bound function values

If |f'(x)| ≤ M on [a,b], then |f(b) − f(a)| ≤ M|b − a|.

### 5.3 Monotonicity

If f'(x) > 0 on (a,b), then f is strictly increasing (MVT: f(b) > f(a) for b > a).

### Worked Example 5 — Monotonicity

f'(x) = 3x² + 1 > 0 everywhere ⇒ f strictly increasing on ℝ.

---

## 6. Hypotheses — GATE trap zone

| Requirement | Interval type |
|-------------|---------------|
| Continuity | **Closed** [a, b] |
| Differentiability | **Open** (a, b) |
| c in conclusion | **Open** (a, b) — not necessarily endpoint |

Missing any hypothesis ⇒ theorem may fail.

### Counterexample — continuity

f(x) = {1 if x < 1, 2 if x ≥ 1} on [0, 2]. Not continuous at 1; MVT fails.

---

## 7. Relation to other topics

- **Rolle:** MVT when f(a) = f(b).
- **Maxima:** Rolle says if endpoints equal, an interior critical point exists.
- **Limits:** derivative defined via limit of difference quotient.

---

## 8. GATE Connection

- "Which theorem guarantees ∃c with f'(c) = ...?" → MVT/Rolle.
- Verify hypotheses before applying.
- Estimate |f(b) − f(a)| from |f'| bound.
- Classic: f(0)=f(1) ⇒ ∃c: f'(c)=0 (Rolle).

---

## 9. Common traps

1. c is in **(a,b)**, not {a,b}.
2. Continuity on closed, differentiability on open — don't swap.
3. Applying Rolle when f(a) ≠ f(b).
4. Assuming MVT gives unique c (may be many).

---

## 10. Summary checklist

- [ ] Rolle: f(a)=f(b) ⇒ ∃c: f'(c)=0.
- [ ] Lagrange: f'(c) = average slope (f(b)−f(a))/(b−a).
- [ ] Hypotheses: cont [a,b], diff (a,b).
- [ ] c ∈ (a,b) open interval.
- [ ] Use for existence and monotonicity arguments.
