# Integration — Practice Questions

Original practice for GATE CS. These questions are not from any GATE paper. Attempt the questions before reading the solutions.

MSQ items may have more than one correct option. NAT items ask for an integer; enter only that integer.

## Level 1 — Conceptual

## Q1 — MCQ

The value of \(\displaystyle\int_0^2 4x\, dx\) is

A. \(2\)

B. \(4\)

C. \(8\)

D. \(16\)

---

## Q2 — NAT

The value of \(\displaystyle\int_1^4 2\, dx\) is an integer. Enter that integer.

---

## Q3 — MCQ

An antiderivative of \(\sin x\) is

A. \(-\cos x + C\)

B. \(\cos x + C\)

C. \(-\sin x + C\)

D. \(\sin x + C\)

---

## Q4 — NAT

The value of \(\displaystyle\int_0^{\pi/2} \sin x\, dx\) is an integer. Enter that integer.

---

## Level 2 — Standard GATE Style

## Q5 — MCQ

\(\displaystyle\int x e^x\, dx\) equals

A. \(e^x(x - 1) + C\)

B. \(e^x(x + 1) + C\)

C. \(x e^x + C\)

D. \(e^x + C\)

---

## Q6 — NAT

The value of \(\displaystyle\int_0^2 x^2\, dx\) equals \(p/3\), where \(p\) is an integer. Enter \(p\).

---

## Q7 — MSQ

Which of the following statements is/are true?

A. \(\displaystyle\int_2^2 (x^2 + 1)\, dx = 0\)

B. \(\displaystyle\int_0^1 x\, dx = -\int_1^0 x\, dx\)

C. \(\displaystyle\int_0^1 x\, dx = \int_1^0 x\, dx\)

D. If \(f\) is even and continuous on \([-2, 2]\), then \(\displaystyle\int_{-2}^{2} f(x)\, dx = 2\int_0^2 f(x)\, dx\)

---

## Q8 — NAT

The average value of \(f(x) = 3x\) on \([0, 2]\) is an integer. Enter that integer.

---

## Q9 — MCQ

\(\displaystyle\int 3x^2 \cos(x^3)\, dx\) equals

A. \(\sin(x^3) + C\)

B. \(\cos(x^3) + C\)

C. \(3\sin(x^3) + C\)

D. \(-\sin(x^3) + C\)

---

## Level 3 — Multi-Step

## Q10 — NAT

The value of \(\displaystyle\int_0^1 (6x^2 + 2)\, dx\) is an integer. Enter that integer.

---

## Q11 — MCQ

For \(x > 0\), \(\displaystyle\int \ln x\, dx\) equals

A. \(\dfrac{1}{x} + C\)

B. \(x \ln x - x + C\)

C. \(x \ln x + x + C\)

D. \(\dfrac{(\ln x)^2}{2} + C\)

---

## Q12 — NAT

The value of \(\displaystyle\int_0^1 (x + 1)^2\, dx\) equals \(p/3\), where \(p\) is an integer. Enter \(p\).

---

## Q13 — MSQ

Let \(y = 2x\) on the interval \([0, 3]\), and let \(F(x) = x^2\). Which of the following statements is/are true?

A. The area under \(y = 2x\) from \(0\) to \(3\) is \(9\)

B. The average value of \(2x\) on \([0, 3]\) is \(3\)

C. \(\displaystyle\int_0^3 2x\, dx = \int_3^0 2x\, dx\)

D. \(F(3) - F(0) = 9\), and this equals \(\displaystyle\int_0^3 2x\, dx\)

---

## Level 4 — Tricky / Trap-Based

## Q14 — MCQ

Both \(\sin x\) and \(\sin x + 7\) are proposed as antiderivatives of \(\cos x\). Which one of the following statements is true?

A. They differ by a constant, and each is an antiderivative of \(\cos x\)

B. Only \(\sin x\) is an antiderivative, because the constant of integration must be \(0\)

C. The derivative of \(\sin x + 7\) is \(\cos x + 7\)

D. The value of \(\displaystyle\int_0^{\pi/2} \cos x\, dx\) changes if the constant \(7\) is kept in the antiderivative

---

## Q15 — NAT

The value of \(\displaystyle\int_0^{\pi/4} \sin(2x)\, dx\) equals \(p/2\), where \(p\) is an integer. Enter \(p\).

---

## Q16 — MCQ

On any open interval that does not contain \(3\) or \(-3\),

\[
\int \dfrac{1}{x^2 - 9}\, dx
\]

equals

A. \(\dfrac{1}{6}\ln\left|\dfrac{x - 3}{x + 3}\right| + C\)

B. \(\dfrac{1}{6}\ln\left|\dfrac{x + 3}{x - 3}\right| + C\)

C. \(\ln|x^2 - 9| + C\)

D. \(\dfrac{1}{3}\arctan(x/3) + C\)

---

## Level 5 — Challenge

## Q17 — NAT

The value of \(\displaystyle\int_0^1 x e^x\, dx\) is an integer. Enter that integer.

---

## Q18 — MSQ

Let \(F(x) = \displaystyle\int_0^x (2t + 1)\, dt\). Which of the following statements is/are true?

A. \(F'(x) = 2x + 1\)

B. \(F(1) = 2\)

C. \(F'(x) = 2\)

D. \(F(0) = 0\)

## Answer Key

| Q | Type | Answer |
|---|------|--------|
| 1 | MCQ | C |
| 2 | NAT | 6 |
| 3 | MCQ | A |
| 4 | NAT | 1 |
| 5 | MCQ | A |
| 6 | NAT | 8 |
| 7 | MSQ | A, B, D |
| 8 | NAT | 3 |
| 9 | MCQ | A |
| 10 | NAT | 4 |
| 11 | MCQ | B |
| 12 | NAT | 7 |
| 13 | MSQ | A, B, D |
| 14 | MCQ | A |
| 15 | NAT | 1 |
| 16 | MCQ | A |
| 17 | NAT | 1 |
| 18 | MSQ | A, B, D |

## Detailed Solutions

### Q1

Answer: C

An antiderivative of \(4x\) is \(2x^2\). Then

\[
\big[2x^2\big]_0^2 = 8 - 0 = 8.
\]

(A) is the upper limit. (B) is the coefficient in the integrand. (D) is \(4 \cdot 2^2\), which uses \(4x^2\) as the antiderivative and forgets to divide by the new power, or equivalently forgets that \(\int 4x\, dx = 2x^2 + C\).

### Q2

Answer: 6

An antiderivative of the constant \(2\) is \(2x\). Then \(\big[2x\big]_1^4 = 8 - 2 = 6\). The same value is the height \(2\) times the width \(3\). Entering \(2\) reports the integrand. Entering \(8\) evaluates only the upper limit. Entering \(3\) is the length of the interval without the factor \(2\).

### Q3

Answer: A

\(\dfrac{d}{dx}(-\cos x) = \sin x\), so \(-\cos x + C\) is an antiderivative. The constant \(C\) belongs on an indefinite integral.

(B) differentiates to \(-\sin x\). (C) differentiates to \(-\cos x\). (D) differentiates to \(\cos x\). Each of those is the antiderivative of a different function. Omitting \(+C\) would also be incomplete for an indefinite integral; every option here that is otherwise right includes it, and the sign is what separates (A) from the others.

### Q4

Answer: 1

\[
\int_0^{\pi/2} \sin x\, dx = \big[-\cos x\big]_0^{\pi/2} = -\cos(\pi/2) - \big(-\cos 0\big) = 0 - (-1) = 1.
\]

The two minus signs at the lower limit are the usual slip. Dropping one of them produces \(0\) or \(-1\). The constant of integration does not appear: this is a definite integral.

### Q5

Answer: A

Integration by parts with \(u = x\) and \(dv = e^x\, dx\) gives \(du = dx\) and \(v = e^x\):

\[
\int x e^x\, dx = x e^x - \int e^x\, dx = x e^x - e^x + C = e^x(x - 1) + C.
\]

Differentiation checks it: \(\dfrac{d}{dx}\big[e^x(x - 1)\big] = e^x(x - 1) + e^x = x e^x\).

(B) has the wrong sign in the subtraction and differentiates to \(e^x(x + 1) + e^x = e^x(x + 2)\). (C) forgets to subtract \(\int v\, du\). (D) integrates only the exponential factor. The constant \(C\) is required because the integral is indefinite.

### Q6

Answer: 8

\[
\int_0^2 x^2\, dx = \left[\dfrac{x^3}{3}\right]_0^2 = \dfrac{8}{3}.
\]

So \(p/3 = 8/3\) and \(p = 8\). Entering \(2\) is the upper limit. Entering \(4\) uses \(x^2\) at \(x = 2\) without integrating. The denominator \(3\) is already fixed by the stem; the numerator is \(2^3\).

### Q7

Answer: A, B, D

(A) The limits are equal, so the integral is \(0\) for a continuous integrand.

(B) Reversing the limits changes the sign: \(\int_1^0 x\, dx = -1/2\) and \(\int_0^1 x\, dx = 1/2\), so the two sides match.

(C) is the same comparison without the minus sign. The two integrals are \(1/2\) and \(-1/2\), so they are not equal.

(D) is the even-function identity on a symmetric interval. For a check, \(x^2\) is even and \(\int_{-2}^{2} x^2\, dx = 16/3 = 2\int_0^2 x^2\, dx\).

### Q8

Answer: 3

The average value on \([0, 2]\) is

\[
\dfrac{1}{2 - 0}\int_0^2 3x\, dx = \dfrac{1}{2}\left[\dfrac{3}{2}x^2\right]_0^2 = \dfrac{1}{2} \cdot 6 = 3.
\]

Entering \(6\) reports the definite integral and forgets to divide by the length \(2\). Entering \(2\) reports the length of the interval.

### Q9

Answer: A

Let \(u = x^3\). Then \(du = 3x^2\, dx\), and the integral is \(\int \cos u\, du = \sin u + C = \sin(x^3) + C\).

Differentiation checks it: \(\dfrac{d}{dx}\sin(x^3) = 3x^2\cos(x^3)\).

(B) and (D) are the sine-versus-cosine sign pattern for \(\int \sin\), not \(\int \cos\). (C) differentiates to \(9x^2\cos(x^3)\), because the chain-rule factor \(3x^2\) is applied twice. The factor \(3x^2\) in the integrand is exactly \(du\); it should not be copied into the answer a second time.

### Q10

Answer: 4

\[
\int_0^1 (6x^2 + 2)\, dx = \big[2x^3 + 2x\big]_0^1 = 2 + 2 = 4.
\]

Entering \(8\) adds the coefficients of the integrand. Entering \(2\) keeps only one of the two evaluated terms.

### Q11

Answer: B

Integration by parts with \(u = \ln x\) and \(dv = dx\) gives \(du = dx/x\) and \(v = x\):

\[
\int \ln x\, dx = x \ln x - \int x \cdot \dfrac{1}{x}\, dx = x \ln x - \int 1\, dx = x \ln x - x + C.
\]

Differentiation checks it: \(\dfrac{d}{dx}(x \ln x - x) = \ln x + x \cdot (1/x) - 1 = \ln x\).

(A) is the derivative of \(\ln x\), not an antiderivative. (C) has the wrong sign on the second term; its derivative is \(\ln x + 2\). (D) is the antiderivative of \((\ln x)/x\), from the substitution \(u = \ln x\). The constant \(C\) is required on this indefinite integral.

### Q12

Answer: 7

Substitute \(u = x + 1\). Then \(du = dx\), and the limits change from \(x = 0\) to \(x = 1\) into \(u = 1\) to \(u = 2\):

\[
\int_1^2 u^2\, du = \left[\dfrac{u^3}{3}\right]_1^2 = \dfrac{8}{3} - \dfrac{1}{3} = \dfrac{7}{3}.
\]

So \(p = 7\). Expanding the original integrand gives the same value: \(\int_0^1 (x^2 + 2x + 1)\, dx = \big[x^3/3 + x^2 + x\big]_0^1 = 1/3 + 1 + 1 = 7/3\).

Entering \(8\) uses only the upper substituted limit. Entering \(1\) forgets to change the lower limit and then subtracts nothing useful. Keeping the old limits \(0\) and \(1\) after the substitution computes \(\int_0^1 u^2\, du = 1/3\), which is a different integral.

### Q13

Answer: A, B, D

On \([0, 3]\) the line \(y = 2x\) is nonnegative, so the area is the definite integral:

\[
\int_0^3 2x\, dx = \big[x^2\big]_0^3 = 9.
\]

(A) is true. Since \(F'(x) = 2x\), the Fundamental Theorem says the same evaluation is \(F(3) - F(0)\). (D) is true.

The average value is \(\dfrac{1}{3 - 0} \cdot 9 = 3\). (B) is true.

Reversing the limits changes the sign: \(\int_3^0 2x\, dx = -9\). (C) is false.

### Q14

Answer: A

\(\dfrac{d}{dx}(\sin x + 7) = \cos x\), and \(\dfrac{d}{dx}(\sin x) = \cos x\). Two antiderivatives of the same continuous function differ by a constant. (A) is true.

(B) forces the constant to be \(0\). Any constant is allowed in an indefinite integral; dropping \(+C\) is the mistake, not the presence of a nonzero constant. (C) treats the constant as if it survived differentiation. The derivative of a constant is \(0\).

(D) fails for a definite integral. If \(G(x) = \sin x + 7\), then

\[
G(\pi/2) - G(0) = (1 + 7) - (0 + 7) = 1,
\]

the same value as \(\sin(\pi/2) - \sin(0)\). The constant cancels. It matters for the indefinite integral, and it does not change the definite integral.

### Q15

Answer: 1

An antiderivative of \(\sin(2x)\) is \(-\cos(2x)/2\), because the chain rule brings down a factor \(2\). Then

\[
\left[-\dfrac{\cos(2x)}{2}\right]_0^{\pi/4} = -\dfrac{\cos(\pi/2)}{2} - \left(-\dfrac{\cos 0}{2}\right) = 0 + \dfrac{1}{2} = \dfrac{1}{2}.
\]

So \(p/2 = 1/2\) and \(p = 1\).

With the substitution \(u = 2x\), \(du = 2\, dx\), the limits change from \(x = 0\) and \(x = \pi/4\) to \(u = 0\) and \(u = \pi/2\):

\[
\int_0^{\pi/2} \dfrac{1}{2}\sin u\, du = \dfrac{1}{2}\big[-\cos u\big]_0^{\pi/2} = \dfrac{1}{2}.
\]

Forgetting the factor \(1/2\) and evaluating \(-\cos(2x)\) from \(0\) to \(\pi/4\) produces \(1\), which would be entered as if \(p = 2\). Forgetting to change the limits after the substitution, and integrating \(\sin u\) from \(0\) to \(\pi/4\), produces a different number. Both errors miss the chain-rule factor that the derivative of the inside function contributes.

### Q16

Answer: A

Factor \(x^2 - 9 = (x - 3)(x + 3)\) and decompose

\[
\dfrac{1}{(x - 3)(x + 3)} = \dfrac{A}{x - 3} + \dfrac{B}{x + 3}.
\]

Then \(A(x + 3) + B(x - 3) = 1\). At \(x = 3\), \(6A = 1\), so \(A = 1/6\). At \(x = -3\), \(-6B = 1\), so \(B = -1/6\). Therefore

\[
\int \dfrac{1}{x^2 - 9}\, dx = \dfrac{1}{6}\int\left(\dfrac{1}{x - 3} - \dfrac{1}{x + 3}\right) dx = \dfrac{1}{6}\ln\left|\dfrac{x - 3}{x + 3}\right| + C.
\]

Differentiating the answer recovers the integrand:

\[
\dfrac{1}{6}\left(\dfrac{1}{x - 3} - \dfrac{1}{x + 3}\right) = \dfrac{1}{6} \cdot \dfrac{6}{x^2 - 9} = \dfrac{1}{x^2 - 9}.
\]

(B) is the negative of (A). Its derivative is \(-1/(x^2 - 9)\), the partial-fraction sign error from swapping \(A\) and \(B\). (C) differentiates to \(2x/(x^2 - 9)\), which still has the factor \(2x\) from the chain rule. (D) is built for a sum of squares: \(\dfrac{d}{dx}\big[\tfrac{1}{3}\arctan(x/3)\big] = 1/(x^2 + 9)\), not \(1/(x^2 - 9)\). The constant \(C\) stays because the integral is indefinite. The formula is stated only on intervals that avoid the poles at \(x = \pm 3\).

### Q17

Answer: 1

From Q5, an antiderivative is \(e^x(x - 1)\). The constant of integration cancels in a definite integral:

\[
\big[e^x(x - 1)\big]_0^1 = e^1(1 - 1) - e^0(0 - 1) = 0 - (1)(-1) = 1.
\]

Entering \(0\) stops at the upper limit, where the factor \(x - 1\) vanishes, and drops the lower limit. Entering \(-1\) is only the lower-limit term before subtraction. The parts formula still needs both limits.

### Q18

Answer: A, B, D

The integrand \(2t + 1\) is continuous, so the Fundamental Theorem gives \(F'(x) = 2x + 1\). (A) is true. (C) differentiates the integrand as if the upper limit were not the variable, or drops the \(2x\) term; the derivative of the integral is the integrand evaluated at the upper limit, not the derivative of the integrand.

Explicitly, \(F(x) = \big[t^2 + t\big]_0^x = x^2 + x\). Then \(F(1) = 2\) and \(F(0) = 0\), so (B) and (D) are true. Also \(F'(x) = 2x + 1\), which matches (A) and rules out (C).

An integral from a constant lower limit up to that same limit is \(0\), which is (D). Forgetting the lower limit of \(0\) in the evaluation of \(F(1)\) is harmless here only because the antiderivative vanishes at \(0\); the theorem still requires \(F(b) - F(a)\).
