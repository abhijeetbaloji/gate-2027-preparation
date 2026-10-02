# Integration — Learning Notes

These notes are written for **first-time learning** or relearning. For a compressed sheet, use `REVISION.md` after you have studied this file.

---

## 1. What is integration in GATE?

**Integration** is the reverse of differentiation and computes accumulated quantities: area under curves, average values, total change. Built on **limits** (`01-LIMITS/NOTES.md`) via Riemann sums.

GATE tests:
- Indefinite integrals (+C)
- Definite integrals and **Fundamental Theorem of Calculus (FTC)**
- Substitution, parts, partial fractions
- Area and average value applications

---

## 2. Indefinite integral

**∫ f(x) dx = F(x) + C** where F'(x) = f(x).

C is arbitrary constant — **never omit +C** in indefinite integrals.

### Standard integrals

| ∫ | Result |
|---|--------|
| x^n dx (n≠−1) | x^{n+1}/(n+1) + C |
| 1/x dx | ln|x| + C |
| e^x dx | e^x + C |
| sin x dx | −cos x + C |
| cos x dx | sin x + C |
| sec²x dx | tan x + C |
| 1/(1+x²) dx | tan⁻¹x + C |
| 1/√(1−x²) dx | sin⁻¹x + C |

---

## 3. Definite integral

**∫_a^b f(x) dx** = signed area under f from a to b.

### Riemann sum (definition idea)

Partition [a,b], sum f(x_i)Δx, take limit as Δx → 0.

---

## 4. Fundamental Theorem of Calculus (FTC)

### Part 1

If f continuous on [a,b], F(x) = ∫_a^x f(t) dt, then **F'(x) = f(x)**.

### Part 2 (evaluation)

If F' = f on [a,b], then **∫_a^b f(x) dx = F(b) − F(a)**.

### Derivation sketch of Part 2

Let F be any antiderivative of f. By Part 1, G(x) = ∫_a^x f(t)dt has G' = f, so G differs from F by constant: G(x) = F(x) − F(a).

Thus ∫_a^b f = G(b) − G(a) = F(b) − F(a).

### Worked Example 1

∫_0^1 x² dx = [x³/3]_0^1 = **1/3**.

### Worked Example 2

∫_0^π sin x dx = [−cos x]_0^π = (−(−1)) − (−1) = **2**.

---

## 5. Substitution (u-substitution)

If ∫ f(g(x)) g'(x) dx, let u = g(x), du = g'(x) dx.

### Worked Example 3

∫ 2x cos(x²) dx. Let u = x², du = 2x dx ⇒ ∫ cos u du = **sin u + C = sin(x²) + C**.

### Definite integral — change limits

∫_0^1 2x cos(x²) dx: u(0)=0, u(1)=1 ⇒ ∫_0^1 cos u du = sin(1).

---

## 6. Integration by parts

**∫ u dv = uv − ∫ v du**

Choose u via LIATE: Log, Inverse trig, Algebraic, Trig, Exponential (u priority).

### Worked Example 4

∫ x e^x dx. u = x, dv = e^x dx ⇒ du = dx, v = e^x.

= x e^x − ∫ e^x dx = **e^x(x − 1) + C**.

### Worked Example 5

∫ ln x dx. u = ln x, dv = dx ⇒ **x ln x − x + C**.

---

## 7. Partial fractions (rational functions)

Decompose P(x)/Q(x) when deg(P) < deg(Q).

Linear factors: A/(x−a) + B/(x−b) + ...

### Worked Example 6

∫ 1/(x²−1) dx = ∫ [1/2(x−1) − 1/2(x+1)] dx = **(1/2)ln|(x−1)/(x+1)| + C**.

---

## 8. Applications

### Area under curve

Area = ∫_a^b f(x) dx when f(x) ≥ 0.

### Average value

**f_avg = (1/(b−a)) ∫_a^b f(x) dx**

### Worked Example 7

Average of x² on [0, 3] = (1/3)∫_0^3 x² dx = (1/3)(27/3) = **3**.

---

## 9. Properties of definite integrals

- ∫_a^b f + ∫_a^b g = ∫_a^b (f+g)
- ∫_a^b f = −∫_b^a f
- ∫_a^a f = 0
- Even f on [−a,a]: ∫ = 2∫_0^a f(x) dx

---

## 10. GATE Connection

- FTC evaluation of definite integrals.
- ∫ x e^x, ∫ ln x — integration by parts.
- Substitution with trig/exp.
- Area and average value word problems.
- Don't forget **+C** indefinite; **change limits** for definite substitution.

---

## 11. Common traps

1. Missing +C in indefinite integrals.
2. Forgetting to change limits after substitution in definite integrals.
3. Wrong LIATE choice in integration by parts.
4. Dividing by zero in partial fractions (repeated roots need extra terms).

---

## 12. Summary checklist

- [ ] FTC: ∫_a^b f = F(b) − F(a).
- [ ] Substitution: identify inner function and derivative.
- [ ] Parts: ∫ u dv = uv − ∫ v du.
- [ ] Average: (1/(b−a)) × integral.
- [ ] +C for indefinite only.
