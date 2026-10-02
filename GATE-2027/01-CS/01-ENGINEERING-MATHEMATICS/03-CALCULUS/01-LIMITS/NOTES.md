# Limits — Learning Notes

These notes are written for **first-time learning** or relearning. For a compressed sheet, use `REVISION.md` after you have studied this file.

---

## 1. What is a limit in GATE?

A **limit** describes what value f(x) approaches as x gets close to a (x may or may not equal a). Limits are the foundation of:

- **Continuity** (`02-CONTINUITY-AND-DIFFERENTIABILITY/NOTES.md`)
- **Derivatives** (difference quotient limit)
- **Integrals** (Riemann sums → definite integral)
- **MVT** and optimization

GATE tests standard limits, indeterminate forms, one-sided limits, and squeeze/L'Hôpital techniques.

---

## 2. Formal definition (intuition)

**lim_{x→a} f(x) = L** means: for every sequence (or neighbourhood) of x values approaching a (with x ≠ a allowed), f(x) approaches L.

**One-sided limits:**
- **lim_{x→a⁺} f(x)** — approach from the right
- **lim_{x→a⁻} f(x)** — approach from the left

**Existence rule:** lim_{x→a} f(x) exists iff left limit = right limit.

### Worked Example 1 — One-sided mismatch

f(x) = |x|/x for x ≠ 0.

- x → 0⁺: |x|/x = x/x = **1**
- x → 0⁻: |x|/x = (−x)/x = **−1**

Limits differ ⇒ **limit does not exist** at 0.

### GATE Connection

Piecewise functions and absolute values are favourite GATE setups for one-sided limits.

---

## 3. Standard limits (memorize)

| Limit | Value |
|-------|-------|
| lim_{x→0} sin x / x | 1 |
| lim_{x→0} tan x / x | 1 |
| lim_{x→0} (eˣ − 1) / x | 1 |
| lim_{x→0} (aˣ − 1) / x | ln a |
| lim_{x→0} (1 + x)^{1/x} | e |
| lim_{x→∞} (1 + 1/x)ˣ | e |
| lim_{x→0} (1 − cos x) / x² | 1/2 |
| lim_{x→0} (ln(1+x)) / x | 1 |

### Derivation sketch — sin x / x = 1

**Geometric squeeze (x > 0 small):** In a unit circle, chord length sin x < arc x < tan x.

Divide by sin x > 0: 1 < x/sin x < 1/cos x.

Take reciprocals and apply squeeze as x → 0⁺: lim sin x / x = 1. By symmetry, holds for x → 0⁻.

### Derivation sketch — (eˣ − 1) / x = 1

Let t = eˣ − 1, so x = ln(1+t) and as x → 0, t → 0.

(eˣ − 1)/x = t / ln(1+t) → 1 (since ln(1+t) ~ t).

### Worked Example 2 — Scaling standard limit

lim_{x→0} sin(5x)/x = 5 · lim sin(5x)/(5x) = **5**.

### Worked Example 3 — e limit

lim_{x→0} (1 + 2x)^{1/x} = [lim (1+2x)^{1/(2x)}]² = **e²**.

---

## 4. Algebraic techniques

### 4.1 Direct substitution

If f is continuous at a, lim_{x→a} f(x) = f(a).

### 4.2 Factorization / rationalization (0/0 forms)

**Worked Example 4.**

lim_{x→2} (x² − 4)/(x − 2) = lim (x+2)(x−2)/(x−2) = lim (x+2) = **4**.

**Worked Example 5 — Rationalize.**

lim_{x→0} (√(1+x) − 1)/x · (√(1+x)+1)/(√(1+x)+1) = lim x/(x(√(1+x)+1)) = **1/2**.

### 4.3 Rational functions at infinity

Compare **leading terms** (highest degree in numerator and denominator).

lim_{x→∞} (3x² + 1)/(2x² − x) = 3/2 (coefficient ratio).

If degree(numerator) < degree(denominator) → 0; if greater → ±∞.

---

## 5. L'Hôpital's rule

### When it applies

For lim f(x)/g(x) as x → a (or ∞), if f and g → 0 or both → ±∞ (indeterminate **0/0** or **∞/∞**), and derivatives exist near a:

**lim f/g = lim f'/g'** (if the latter limit exists or is ±∞).

### Derivation idea (sketch)

For 0/0 near a: f(a)=g(a)=0. By MVT on [a, x], f(x) = f'(c)g(x)/g'(c) for some c between a and x; as x → a, ratio → f'(a)/g'(a).

### Worked Example 6 — Single application

lim_{x→0} (eˣ − 1 − x)/x² → 0/0.

Apply L'Hôpital: (eˣ − 1)/(2x) → still 0/0.

Again: eˣ/(2) → **1/2**.

### Worked Example 7 — When NOT to use

lim_{x→∞} (3x² + 1)/(2x² − x) — already determinate; answer **3/2** without L'Hôpital.

### Common traps

- Form must be 0/0 or ∞/∞ before applying.
- Differentiate numerator and denominator **separately** — not quotient rule on f/g.
- L'Hôpital may fail if f'/g' limit does not exist (try another method).

---

## 6. Squeeze (sandwich) theorem

If g(x) ≤ f(x) ≤ h(x) near a and lim g = lim h = L, then **lim f = L**.

**Worked Example 8.**

lim_{x→0} x² sin(1/x): |sin(1/x)| ≤ 1 ⇒ −x² ≤ x² sin(1/x) ≤ x².

Both bounds → 0 ⇒ limit = **0**.

---

## 7. Limits involving exponentials and logarithms

lim_{x→0⁺} x ln x = 0 (rewrite as ln x / (1/x), ∞/∞, L'Hôpital).

lim_{x→∞} ln x / x = 0.

---

## 8. Piecewise limits

At junction x = c: compute left and right limits separately; equal ⇒ limit exists.

---

## 9. GATE Connection

- MCQs on sin, e, log standard forms.
- 0/0 rational — **factor first**, L'Hôpital only if needed.
- One-sided limits for |x|, piecewise definitions.
- Degree comparison at ∞ — no calculus needed.
- Links to continuity: limit must equal f(a) for continuity.

---

## 10. Common traps

1. Substituting x = a directly in 0/0 form.
2. Ignoring one-sided mismatch.
3. Applying L'Hôpital without checking indeterminate form.
4. Forgetting that limit can exist when f(a) is undefined (removable discontinuity).

---

## 11. Summary checklist

- [ ] Memorize standard limits (sin, e, cos, ln).
- [ ] Check one-sided limits for |x| and piecewise.
- [ ] Factor/rationalize before L'Hôpital.
- [ ] At ∞: compare degrees for rationals.
- [ ] Squeeze for bounded oscillation (sin(1/x) type).
