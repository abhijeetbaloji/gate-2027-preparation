# Continuity and Differentiability — Practice Questions

Original practice for GATE CS. These questions are not from any GATE paper. Attempt the questions before reading the solutions.

MSQ items may have more than one correct option. NAT items ask for an integer; enter only that integer.

## Level 1 — Conceptual

## Q1 — MCQ

The function \(f(x) = |x|\) at \(x = 0\) is

A. discontinuous

B. continuous but not differentiable

C. differentiable, and \(f'(0) = 0\)

D. differentiable, and \(f'(0) = 1\)

---

## Q2 — NAT

Let \(f(x) = x^3\). The value of \(f'(2)\) is an integer. Enter that integer.

---

## Q3 — MCQ

The value of \(\dfrac{d}{dx}\big[\sin(3x)\big]\) at \(x = 0\) is

A. \(0\)

B. \(1\)

C. \(3\)

D. \(-3\)

---

## Q4 — NAT

Let \(f(x) = x e^{2x}\). The value of \(f'(0)\) is an integer. Enter that integer.

---

## Level 2 — Standard GATE Style

## Q5 — MCQ

Define

\[
f(x) =
\begin{cases}
x + 2, & x < 1, \\
3x, & x \ge 1.
\end{cases}
\]

At \(x = 1\), \(f\) is

A. discontinuous

B. continuous and differentiable

C. continuous but not differentiable

D. differentiable but not continuous

---

## Q6 — NAT

Define

\[
f(x) =
\begin{cases}
2x + a, & x \le 1, \\
5x + 1, & x > 1.
\end{cases}
\]

If \(f\) is continuous at \(x = 1\), then \(a\) is an integer. Enter \(a\).

---

## Q7 — MSQ

Which of the following functions are differentiable at \(x = 0\)?

A. \(f(x) = |x|\)

B. \(f(x) = x|x|\)

C. \(f(x) = x^2\)

D. \(f(x) = |x| + x^2\)

---

## Q8 — NAT

For \(x > 0\), let \(y = x^x\). The value of \(y'/y\) at \(x = e^2\) is an integer. Enter that integer.

---

## Level 3 — Multi-Step

## Q9 — MCQ

Define

\[
f(x) =
\begin{cases}
ax^2, & x \le 1, \\
6x + b, & x > 1,
\end{cases}
\]

with \(a, b \in \mathbb{R}\). If \(f\) is differentiable at \(x = 1\), then \(a\) equals

A. \(1\)

B. \(2\)

C. \(3\)

D. \(6\)

---

## Q10 — NAT

The number of points at which \(f(x) = |x + 2| + |x - 3|\) is not differentiable is an integer. Enter that integer.

---

## Q11 — MSQ

Define \(f(x) = \dfrac{x^2 - 1}{x - 1}\) for \(x \neq 1\), and \(f(1) = 4\). Which of the following statements is/are true?

A. \(\lim_{x \to 1} f(x) = 2\)

B. \(f\) is continuous at \(x = 1\)

C. \(f\) has a removable discontinuity at \(x = 1\)

D. \(f\) is differentiable at \(x = 1\)

---

## Level 4 — Tricky / Trap-Based

## Q12 — MCQ

Which one of the following functions is continuous at \(x = 0\) but not differentiable at \(x = 0\)?

A. \(f(x) = x^3\)

B. \(f(x) = x|x|\)

C. \(f(x) = |x|\)

D. \(f(x) = x^2\)

---

## Q13 — NAT

Define

\[
f(x) =
\begin{cases}
x^2 + ax + b, & x \le 2, \\
6x - 4, & x > 2.
\end{cases}
\]

If \(f\) is differentiable at \(x = 2\), then \(a + b\) is an integer. Enter \(a + b\).

---

## Q14 — MSQ

Let \(f(x) = |x - 3|\). Which of the following statements is/are true?

A. \(f\) is continuous at \(x = 3\)

B. \(f'(3)\) exists and equals \(0\)

C. The left-hand derivative of \(f\) at \(x = 3\) equals \(-1\)

D. The right-hand derivative of \(f\) at \(x = 3\) equals \(1\)

---

## Level 5 — Challenge

## Q15 — MSQ

Define

\[
f(x) =
\begin{cases}
x^2 \sin(1/x), & x \neq 0, \\
0, & x = 0.
\end{cases}
\]

Which of the following statements is/are true?

A. \(f\) is continuous at \(x = 0\)

B. \(f'(0) = 0\)

C. \(f'\) is continuous at \(x = 0\)

D. \(\lim_{x \to 0} f(x) = 0\)

---

## Q16 — NAT

Let \(f(x) = x|x|\). Then \(f\) is differentiable at \(0\), and \(f'(0) = 0\). The right-hand derivative of \(f'\) at \(0\),

\[
\lim_{h \to 0^+} \dfrac{f'(h) - f'(0)}{h},
\]

is an integer. Enter that integer.

## Answer Key

| Q | Type | Answer |
|---|------|--------|
| 1 | MCQ | B |
| 2 | NAT | 12 |
| 3 | MCQ | C |
| 4 | NAT | 1 |
| 5 | MCQ | C |
| 6 | NAT | 4 |
| 7 | MSQ | B, C |
| 8 | NAT | 3 |
| 9 | MCQ | C |
| 10 | NAT | 2 |
| 11 | MSQ | A, C |
| 12 | MCQ | C |
| 13 | NAT | 2 |
| 14 | MSQ | A, C, D |
| 15 | MSQ | A, B, D |
| 16 | NAT | 2 |

## Detailed Solutions

### Q1

Answer: B

\(\lim_{x \to 0} |x| = 0 = f(0)\), so \(f\) is continuous at \(0\). The right-hand derivative is \(\lim_{h \to 0^+} h/h = 1\). The left-hand derivative is \(\lim_{h \to 0^-} (-h)/h = -1\). The one-sided derivatives differ, so \(f'(0)\) does not exist.

(A) confuses the corner with a jump. (C) and (D) claim a derivative that the one-sided slopes do not share. Continuity at a point does not imply differentiability there.

### Q2

Answer: 12

\(f'(x) = 3x^2\), so \(f'(2) = 3 \cdot 4 = 12\). The value \(6\) is \(f'(2)\) for \(x^2\), and \(8\) is \(f(2)\).

### Q3

Answer: C

The chain rule gives \(\dfrac{d}{dx}\sin(3x) = 3\cos(3x)\). At \(x = 0\) this is \(3\cos 0 = 3\).

(A) is \(\sin 0\). (B) drops the inner derivative \(3\). (D) is the derivative of \(\cos(3x)\) at \(0\), with a sign error relative to sine.

### Q4

Answer: 1

The product rule: \(f'(x) = e^{2x} + x \cdot 2e^{2x} = e^{2x}(1 + 2x)\). At \(x = 0\), \(f'(0) = 1\). Entering \(0\) uses only the factor \(x\) and ignores the derivative of \(e^{2x}\) multiplied by the first factor. Entering \(2\) is the inner derivative of the exponential alone.

### Q5

Answer: C

\(f(1) = 3\). The left-hand limit is \(1 + 2 = 3\), and the right-hand limit is \(3 \cdot 1 = 3\). So \(f\) is continuous at \(1\).

The left-hand derivative is the slope of \(x + 2\), which is \(1\). The right-hand derivative is the slope of \(3x\), which is \(3\). These differ, so \(f\) is not differentiable at \(1\).

(A) matches the function values incorrectly. (B) matches values and then assumes the derivatives match. (D) is impossible: differentiability at a point implies continuity at that point.

### Q6

Answer: 4

Continuity at \(x = 1\) uses the left piece as the function value: \(f(1) = 2 + a\). The right-hand limit is \(5 + 1 = 6\). So \(2 + a = 6\) and \(a = 4\). Differentiability was not asked; the slopes \(2\) and \(5\) do not match, but that does not change \(a\).

### Q7

Answer: B, C

(A) \(|x|\) has left slope \(-1\) and right slope \(1\) at \(0\), so it is not differentiable there.

(B) \(x|x|\) equals \(x^2\) for \(x \ge 0\) and \(-x^2\) for \(x < 0\). The difference quotient at \(0\) is \(|h|\), which tends to \(0\). So \(f'(0) = 0\).

(C) \(x^2\) is a polynomial, and \(f'(0) = 0\).

(D) \(|x| + x^2\) differs from \(|x|\) by a differentiable function. The corner of \(|x|\) remains, so the one-sided derivatives at \(0\) are \(-1\) and \(1\).

Thus only (B) and (C) are differentiable at \(0\). Continuity of (A) and (D) is not enough.

### Q8

Answer: 3

For \(x > 0\), \(\ln y = x \ln x\). Differentiate both sides:

\[
\dfrac{y'}{y} = \ln x + x \cdot \dfrac{1}{x} = 1 + \ln x.
\]

At \(x = e^2\), \(1 + \ln(e^2) = 1 + 2 = 3\). The value \(2\) is only \(\ln(e^2)\). The value \(e^2\) is \(y\) itself, not \(y'/y\).

### Q9

Answer: C

Differentiability at \(1\) requires continuity at \(1\) and equal one-sided derivatives.

Left value: \(f(1) = a\). Right-hand limit: \(6 + b\). So \(a = 6 + b\).

Left derivative: \(\dfrac{d}{dx}(ax^2) = 2ax\), which equals \(2a\) at \(x = 1\). Right derivative: \(6\). So \(2a = 6\), hence \(a = 3\), and then \(b = -3\).

(A) and (B) match neither the derivative condition nor the continuity condition. (D) sets \(a\) equal to the right-hand slope and skips the factor \(2\) from differentiating \(ax^2\).

### Q10

Answer: 2

\(|x - c|\) fails to be differentiable only at \(x = c\). The sum \(|x + 2| + |x - 3|\) therefore has candidate corners at \(x = -2\) and \(x = 3\).

Away from those points the expression is linear on each of \((-\infty, -2)\), \((-2, 3)\), and \((3, \infty)\), with slopes \(-2\), \(0\), and \(2\) respectively. At \(x = -2\) the slopes on the two sides are \(-2\) and \(0\). At \(x = 3\) they are \(0\) and \(2\). Both are genuine corners. There are exactly two such points. Counting the flat middle as an extra corner, or counting only one absolute value, produces \(1\) or \(3\).

### Q11

Answer: A, C

For \(x \neq 1\), \(x^2 - 1 = (x - 1)(x + 1)\), so \(f(x) = x + 1\) and \(\lim_{x \to 1} f(x) = 2\). (A) is true. The given value \(f(1) = 4\) is not \(2\), so \(f\) is not continuous at \(1\) and therefore not differentiable there. (B) and (D) fail. The limit exists and is finite, so the mismatch is a removable discontinuity: defining \(f(1) = 2\) would remove it. (C) is true. Differentiability was never reached, because continuity already fails.

### Q12

Answer: C

(A) \(x^3\) and (D) \(x^2\) are polynomials, hence differentiable at \(0\).

(B) As in Q7, \(x|x|\) has difference quotient \(|h| \to 0\), so it is differentiable at \(0\) even though an absolute value is present. The absolute value does not automatically create a corner after multiplication by \(x\).

(C) \(|x|\) is continuous at \(0\), but the left derivative is \(-1\) and the right derivative is \(1\).

### Q13

Answer: 2

Continuity at \(2\): the left value is \(4 + 2a + b\), and the right-hand limit is \(12 - 4 = 8\). So

\[
2a + b = 4. \tag{1}
\]

Left derivative: \(2x + a\), which equals \(4 + a\) at \(x = 2\). Right derivative: \(6\). So \(4 + a = 6\), hence \(a = 2\). Equation (1) then gives \(b = 0\), and \(a + b = 2\).

Matching only the function values and guessing \(a = 0\) leaves the slopes \(4\) and \(6\) unequal. Matching only the derivatives and forgetting continuity can produce a different pair \((a, b)\).

### Q14

Answer: A, C, D

\(f(3) = 0\), and \(\lim_{x \to 3} |x - 3| = 0\), so (A) is true.

For \(h > 0\), \(\big(f(3 + h) - f(3)\big)/h = h/h = 1\). For \(h < 0\), \(\big(f(3 + h) - f(3)\big)/h = (-h)/h = -1\). So (C) and (D) are true. The one-sided derivatives differ, so \(f'(3)\) does not exist. (B) treats the corner as a horizontal tangent. Continuity at the kink does not produce a derivative.

### Q15

Answer: A, B, D

\(|f(x)| \le x^2\) for every \(x\), and \(x^2 \to 0\). The squeeze theorem gives \(\lim_{x \to 0} f(x) = 0 = f(0)\). So (A) and (D) are true.

The difference quotient at \(0\) is \(h\sin(1/h)\). Its absolute value is at most \(|h|\), so \(f'(0) = 0\). (B) is true.

For \(x \neq 0\),

\[
f'(x) = 2x\sin(1/x) - \cos(1/x).
\]

Along \(x_n = 1/(2\pi n)\), \(\cos(1/x_n) = 1\) and \(f'(x_n) = -1\). Along \(y_n = 1/(\pi + 2\pi n)\), \(\cos(1/y_n) = -1\) and \(f'(y_n) = 1\). Both sequences tend to \(0\), but \(f'\) tends to two different values. So \(f'\) has no limit at \(0\) and is not continuous there. (C) fails. Differentiability of \(f\) does not imply continuity of \(f'\).

### Q16

Answer: 2

For \(h > 0\), \(f(h) = h^2\), so \(f'(h) = 2h\). With \(f'(0) = 0\),

\[
\dfrac{f'(h) - f'(0)}{h} = \dfrac{2h}{h} = 2.
\]

The right-hand limit is \(2\).

For a check of the other side: if \(h < 0\), then \(f(h) = -h^2\) and \(f'(h) = -2h\), so \(\big(f'(h) - 0\big)/h = -2\). The two second-order one-sided derivatives differ, so \(f''(0)\) does not exist, but the question asks only for the right-hand value. Entering \(0\) repeats \(f'(0)\). Entering \(-2\) is the left-hand value.
