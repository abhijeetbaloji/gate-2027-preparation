# Continuity and Differentiability — Learning Notes

These notes are written for **first-time learning** or relearning. For a compressed sheet, use `REVISION.md` after you have studied this file.

---

## 1. Where this fits in GATE

**Limits** (`01-LIMITS/NOTES.md`) define continuity. **Differentiability** is a stronger property — a function can be continuous but not differentiable (|x| at 0).

GATE tests:
- Continuity at a point and on intervals
- Differentiability vs continuity
- Derivative rules (chain, product, quotient)
- Log differentiation, piecewise parameters
- Links to **MVT** and **maxima/minima**

---

## 2. Continuity at a point

f is **continuous at a** iff all three hold:

1. f(a) is defined
2. lim_{x→a} f(x) exists
3. lim_{x→a} f(x) = f(a)

### Types of discontinuity

| Type | Description | Example |
|------|-------------|---------|
| Removable | Limit exists ≠ f(a) or f(a) undefined | (x²−1)/(x−1) at 1 |
| Jump | Left ≠ right limit | Step function |
| Infinite | Limit → ±∞ | 1/x at 0 |

### Worked Example 1 — Removable hole

f(x) = (x² − 1)/(x − 1) for x ≠ 1, f(1) = 3.

lim_{x→1} f(x) = lim (x+1) = **2** ≠ f(1) = 3 ⇒ **not continuous** at 1.

If we set f(1) = 2, discontinuity becomes removable (hole filled).

### Worked Example 2 — Jump

f(x) = {1 if x ≥ 0, −1 if x < 0} at x = 0.

Left limit −1, right limit +1 ⇒ **not continuous** at 0.

---

## 3. Continuity on an interval

- **Continuous on [a,b]:** continuous at every point in (a,b), right-continuous at a, left-continuous at b.
- **MVT hypothesis** requires continuity on **[a,b]** (closed).

---

## 4. Differentiability

**f'(a) = lim_{h→0} [f(a+h) − f(a)] / h**

Geometric meaning: slope of tangent at a.

### Key theorem (proof sketch)

**Differentiable at a ⇒ continuous at a.**

*Proof:* f(a+h) − f(a) = h · [(f(a+h)−f(a))/h]. As h → 0, if derivative exists, RHS → 0·f'(a) = 0, so f(a+h) → f(a).

**Converse is false:** |x| is continuous at 0 but not differentiable (left slope −1, right slope +1).

### Worked Example 3 — |x| at 0

Continuous: lim |x| = 0 = f(0). ✓

Derivative: left derivative −1, right +1 ⇒ **not differentiable** at 0.

### Worked Example 4 — x|x| at 0

f(x) = x² for x ≥ 0, −x² for x < 0.

Both one-sided derivatives at 0 equal 0 ⇒ **differentiable** with f'(0) = 0.

---

## 5. Derivative rules

| Rule | Formula |
|------|---------|
| Constant | (c)' = 0 |
| Power | (x^n)' = n x^{n−1} |
| Sum | (f+g)' = f' + g' |
| Product | (fg)' = f'g + fg' |
| Quotient | (f/g)' = (f'g − fg')/g² |
| Chain | (f∘g)'(x) = f'(g(x))·g'(x) |

### Worked Example 5 — Chain rule

d/dx sin(2x) = cos(2x)·2 = **2 cos(2x)**.

### Worked Example 6 — Product rule

d/dx [x² e^x] = 2x e^x + x² e^x = x e^x(2 + x).

---

## 6. Logarithmic differentiation

For y = f(x)^{g(x)} or products/quotients with variable exponents:

1. Take ln: ln y = g(x) ln f(x)
2. Differentiate implicitly: y'/y = ...
3. Solve for y'

### Worked Example 7 — x^x (x > 0)

ln y = x ln x ⇒ y'/y = ln x + 1 ⇒ **y' = x^x(1 + ln x)**.

---

## 7. Piecewise functions — GATE favourite

At junction x = c:

1. **Continuity:** f(c⁻) = f(c⁺) = f(c)
2. **Differentiability:** left derivative = right derivative

### Worked Example 8 — Find parameters

f(x) = ax² + 1 for x ≤ 1, bx + 2 for x > 1.

Continuity at 1: a + 1 = b + 2.

Left derivative: 2a; right derivative: b.

Differentiability: 2a = b.

Solve: **a = 1, b = 2**.

---

## 8. Non-differentiable points of |x − a|

|x − a| has corner at x = a.

**|x − 1| + |x − 2|** non-differentiable at **x = 1** and **x = 2**.

---

## 9. GATE Connection

- "|x| at 0" — classic trap (continuous, not differentiable).
- Piecewise: find k for continuity and/or differentiability.
- Chain rule on nested trig/exp/log.
- x^x via log differentiation.
- MVT requires continuity on [a,b], differentiability on (a,b).

---

## 10. Common traps

1. Assuming continuous ⇒ differentiable.
2. Checking value match only, not derivative match at junctions.
3. Domain restrictions: ln x (x > 0), 1/x (x ≠ 0).
4. Confusing continuity on open vs closed interval for MVT.

---

## 11. Summary checklist

- [ ] Continuity: limit exists and equals f(a).
- [ ] Differentiable ⇒ continuous (not converse).
- [ ] Piecewise: match value AND derivative at junction.
- [ ] |x − a| corners at x = a.
- [ ] Log diff for x^x and variable powers.
