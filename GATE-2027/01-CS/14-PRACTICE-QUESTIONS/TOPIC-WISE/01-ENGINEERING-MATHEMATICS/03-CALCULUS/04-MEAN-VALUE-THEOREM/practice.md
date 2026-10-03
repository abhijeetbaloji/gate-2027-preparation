# Mean Value Theorem — Practice Questions

Original practice for GATE CS. These questions are not from any GATE paper. Attempt the questions before reading the solutions.

MSQ items may have more than one correct option. NAT items ask for an integer; enter only that integer.

## Level 1 — Conceptual

## Q1 — MCQ

If the hypotheses of Rolle's theorem hold for \(f\) on \([a, b]\), then the theorem concludes that there exists \(c \in (a, b)\) such that

A. \(f'(c) = 0\)

B. \(f(c) = 0\)

C. \(f'(c) = f(a)\)

D. \(f''(c) = 0\)

---

## Q2 — NAT

Let \(f(x) = x^2\) on \([2, 6]\). The Mean Value Theorem guarantees a point \(c \in (2, 6)\) with \(f'(c) = \dfrac{f(6) - f(2)}{6 - 2}\). That \(c\) is an integer. Enter \(c\).

---

## Level 2 — Standard GATE Style

## Q3 — MCQ

Let \(f(x) = x^2 - 6x + 8\) on \([2, 4]\). Rolle's theorem gives a point \(c \in (2, 4)\) with \(f'(c) = 0\). The value of \(c\) is

A. \(2\)

B. \(3\)

C. \(4\)

D. \(6\)

---

## Q4 — NAT

Suppose \(f\) is continuous on \([0, 6]\) and differentiable on \((0, 6)\), with \(f(0) = 4\) and \(f(6) = 16\). The Mean Value Theorem guarantees a point \(c \in (0, 6)\) such that \(f'(c)\) equals an integer. Enter that integer.

---

## Q5 — MSQ

Which of the following is/are required in the hypotheses of Lagrange's Mean Value Theorem for a function \(f\) on a closed interval \([a, b]\)?

A. \(f\) is continuous on \([a, b]\)

B. \(f\) is differentiable on \((a, b)\)

C. \(f(a) = f(b)\)

D. \(f\) must be differentiable at the endpoints \(a\) and \(b\)

---

## Level 3 — Multi-Step

## Q6 — MCQ

Suppose \(f\) is continuous on \([0, 3]\), differentiable on \((0, 3)\), and \(|f'(x)| \le 4\) for every \(x \in (0, 3)\). If \(f(0) = 1\), then the largest possible value of \(f(3)\) is

A. \(4\)

B. \(12\)

C. \(13\)

D. \(16\)

---

## Q7 — NAT

Let \(f(x) = x^3 + x - 1\). The number of real roots of \(f(x) = 0\) is an integer. Enter that integer.

---

## Level 4 — Tricky / Trap-Based

## Q8 — MCQ

Let \(f(x) = |x|\) on \([-2, 2]\). Note that \(f(-2) = f(2)\). Which one of the following statements is true?

A. Rolle's theorem applies, and the only point it produces is \(c = 0\)

B. Rolle's theorem does not apply, because \(f\) is not differentiable on \((-2, 2)\)

C. Rolle's theorem does not apply, because \(f(-2) \neq f(2)\)

D. \(f\) is differentiable at \(0\) and \(f'(0) = 0\)

---

## Q9 — NAT

Let \(f(x) = x^3 - 3x\) on \([-\sqrt{3}, \sqrt{3}]\). The number of points \(c\) in the open interval \((-\sqrt{3}, \sqrt{3})\) at which \(f'(c) = 0\) is an integer. Enter that integer.

---

## Level 5 — Challenge

## Q10 — MSQ

Let \(f(x) = x^3 - 3x + 1\) on \([0, 2]\). Which of the following statements is/are true?

A. Rolle's theorem applies to \(f\) on \([0, 2]\)

B. There exists \(c \in (0, 2)\) such that \(f'(c) = 1\)

C. \(f'(1) = 0\)

D. \(f\) is discontinuous at \(x = 1\)

## Answer Key

| Q | Type | Answer |
|---|------|--------|
| 1 | MCQ | A |
| 2 | NAT | 4 |
| 3 | MCQ | B |
| 4 | NAT | 2 |
| 5 | MSQ | A, B |
| 6 | MCQ | C |
| 7 | NAT | 1 |
| 8 | MCQ | B |
| 9 | NAT | 2 |
| 10 | MSQ | B, C |

## Detailed Solutions

### Q1

Answer: A

Rolle's theorem assumes continuity on \([a, b]\), differentiability on \((a, b)\), and \(f(a) = f(b)\). The conclusion is a point \(c\) strictly between \(a\) and \(b\) with \(f'(c) = 0\).

(B) concludes something about the function value, not the derivative. (C) equates the derivative to an endpoint value; the theorem does not say that. (D) asks for a second derivative, which Rolle does not mention. Lagrange's theorem is the version that allows \(f(a) \neq f(b)\) and concludes that \(f'(c)\) equals the secant slope. When that slope happens to be \(0\), Lagrange reduces to Rolle.

### Q2

Answer: 4

\(f(6) = 36\) and \(f(2) = 4\), so the secant slope is \((36 - 4)/(6 - 2) = 8\). Also \(f'(x) = 2x\), so \(2c = 8\) and \(c = 4\). This lies in \((2, 6)\). The hypotheses hold because \(x^2\) is a polynomial.

Entering \(8\) reports the secant slope. Entering \(2\) or \(6\) reports an endpoint. The point \(c\) guaranteed by the theorem lies in the open interval.

### Q3

Answer: B

\(f(2) = 4 - 12 + 8 = 0\) and \(f(4) = 16 - 24 + 8 = 0\), so \(f(2) = f(4)\). The polynomial is continuous on \([2, 4]\) and differentiable on \((2, 4)\). Rolle applies.

\(f'(x) = 2x - 6 = 0\) gives \(c = 3\), which lies in \((2, 4)\).

(A) and (C) are the endpoints. The conclusion of Rolle places \(c\) in the open interval, even though \(f'\) may also be inspected at endpoints for other reasons. (D) is the coefficient of the linear term, not the root of \(f'\).

### Q4

Answer: 2

The hypotheses of Lagrange's theorem are exactly the ones stated. The conclusion is

\[
f'(c) = \dfrac{f(6) - f(0)}{6 - 0} = \dfrac{16 - 4}{6} = 2
\]

for some \(c \in (0, 6)\). The theorem does not identify \(c\); it identifies the derivative value. Entering \(12\) is the change in \(f\) without dividing by the length of the interval. Entering \(4\) or \(16\) reports an endpoint value of \(f\).

### Q5

Answer: A, B

Lagrange's Mean Value Theorem needs continuity on the closed interval and differentiability on the open interval. (A) and (B) are the hypotheses.

(C) is the extra hypothesis of Rolle's theorem. Lagrange does not need \(f(a) = f(b)\). If the endpoint values differ, the conclusion is \(f'(c) = (f(b) - f(a))/(b - a)\), which need not be \(0\).

(D) is stronger than the theorem requires. Differentiability at the endpoints is not part of the hypothesis. Continuity at the endpoints is required; a derivative there is not.

### Q6

Answer: C

By the Mean Value Theorem, there is some \(c \in (0, 3)\) with

\[
f(3) - f(0) = f'(c)(3 - 0).
\]

The bound \(|f'(c)| \le 4\) gives \(|f(3) - 1| \le 12\), so \(f(3) \le 1 + 12 = 13\). The bound is sharp in the sense that a function with slope \(4\) throughout, such as \(f(x) = 1 + 4x\), attains \(f(3) = 13\).

(A) is the derivative bound itself. (B) is \(4 \cdot 3\), the maximum increase, without adding \(f(0)\). (D) is \(4 \cdot 4\), using the wrong interval length or multiplying the bound by \(f(0)\).

### Q7

Answer: 1

\(f'(x) = 3x^2 + 1 \ge 1 > 0\) for every real \(x\). By the Mean Value Theorem, if \(b > a\) then \(f(b) - f(a) = f'(c)(b - a) > 0\). So \(f\) is strictly increasing on \(\mathbb{R}\) and has at most one real root.

Also \(f(0) = -1 < 0\) and \(f(1) = 1 > 0\). Continuity and the intermediate-value theorem give at least one root in \((0, 1)\). Therefore there is exactly one real root. Entering \(3\) counts the degree of the cubic. A cubic always has at least one real root, but it need not have three; here the positive derivative rules the other two out.

### Q8

Answer: B

\(f(-2) = f(2) = 2\), so the equal-endpoint condition holds and (C) is false. But \(f(x) = |x|\) is not differentiable at \(0\), and \(0\) lies in \((-2, 2)\). Differentiability on the whole open interval fails, so Rolle's theorem does not apply. (B) is true.

(A) applies the conclusion after a hypothesis has failed. The corner is exactly why there is no \(c\) with \(f'(c) = 0\): the slope is \(-1\) on \((-2, 0)\) and \(1\) on \((0, 2)\), and \(f'(0)\) does not exist. (D) claims that missing derivative. Lagrange's theorem fails on this interval for the same reason: differentiability on the open interval is required there too.

### Q9

Answer: 2

\(f(-\sqrt{3}) = -3\sqrt{3} + 3\sqrt{3} = 0\) and \(f(\sqrt{3}) = 3\sqrt{3} - 3\sqrt{3} = 0\). The polynomial is continuous on the closed interval and differentiable on the open interval, so Rolle guarantees at least one root of \(f'\) in \((-\sqrt{3}, \sqrt{3})\).

Directly, \(f'(x) = 3x^2 - 3 = 3(x - 1)(x + 1)\), so \(f'(c) = 0\) at \(c = -1\) and \(c = 1\). Both lie in \((-\sqrt{3}, \sqrt{3})\) because \(\sqrt{3} > 1\). There are two such points. Entering \(1\) counts only the positive root, or only the existence statement from Rolle. Rolle guarantees at least one; it does not say the point is unique.

### Q10

Answer: B, C

\(f(0) = 1\) and \(f(2) = 8 - 6 + 1 = 3\). The endpoint values differ, so Rolle's theorem does not apply. (A) is false. A polynomial is continuous everywhere, so (D) is false.

The secant slope is \((3 - 1)/(2 - 0) = 1\). Lagrange's theorem applies and gives some \(c \in (0, 2)\) with \(f'(c) = 1\). Explicitly, \(f'(x) = 3x^2 - 3\), so \(3c^2 - 3 = 1\), hence \(c^2 = 4/3\) and \(c = 2/\sqrt{3}\). This value is about \(1.15\), which lies in \((0, 2)\). The negative root \(-2/\sqrt{3}\) does not lie in the interval. (B) is true.

Also \(f'(1) = 3 - 3 = 0\), so (C) is true. That critical point is not the \(c\) from the secant condition, because the secant slope is \(1\), not \(0\). Using Rolle because a derivative happens to vanish somewhere, even though \(f(0) \neq f(2)\), is the mix-up between the two theorems.
