# Limits — Practice Questions

Original practice for GATE CS. These questions are not from any GATE paper. Attempt the questions before reading the solutions.

MSQ items may have more than one correct option. NAT items ask for an integer; enter only that integer.

## Level 1 — Conceptual

## Q1 — MCQ

The value of \(\lim_{x \to 0} \dfrac{\sin(5x)}{5x}\) is

A. \(0\)

B. \(1\)

C. \(5\)

D. the limit does not exist

---

## Q2 — NAT

The value of \(\lim_{x \to 3} \dfrac{x^2 - 9}{x - 3}\) is an integer. Enter that integer.

---

## Q3 — MCQ

The value of \(\lim_{x \to \infty} \dfrac{6x^2 - x}{2x^2 + 3}\) is

A. \(0\)

B. \(2\)

C. \(3\)

D. \(\infty\)

---

## Level 2 — Standard GATE Style

## Q4 — NAT

The value of \(\lim_{x \to 0} \dfrac{1 - \cos(2x)}{x^2}\) is an integer. Enter that integer.

---

## Q5 — MCQ

The value of \(\lim_{x \to 0} \dfrac{e^{4x} - 1}{x}\) is

A. \(0\)

B. \(1\)

C. \(4\)

D. \(e^4\)

---

## Q6 — MSQ

Which of the following limits equal \(e^3\)?

A. \(\lim_{x \to 0} (1 + 3x)^{1/x}\)

B. \(\lim_{x \to \infty} \left(1 + \dfrac{3}{x}\right)^x\)

C. \(\lim_{x \to \infty} \left(1 + \dfrac{1}{x}\right)^{3x}\)

D. \(\lim_{x \to 0} (1 + 3x)^{3/x}\)

---

## Q7 — NAT

The value of \(\lim_{x \to 0} \dfrac{\sqrt{1 + 6x} - 1}{x}\) is an integer. Enter that integer.

---

## Level 3 — Multi-Step

## Q8 — MCQ

The value of \(\lim_{x \to 0} x \sin(1/x)\) is

A. \(0\)

B. \(1\)

C. the limit does not exist, because \(\sin(1/x)\) oscillates

D. \(\infty\)

---

## Q9 — NAT

\(\lim_{x \to 0} \dfrac{e^x - 1 - x}{x^2}\) equals \(p/2\), where \(p\) is an integer. Enter \(p\).

---

## Q10 — MSQ

For \(x \neq 0\), let \(f(x) = |2x|/x\). Which of the following statements is/are true?

A. \(\lim_{x \to 0^+} f(x) = 2\)

B. \(\lim_{x \to 0^-} f(x) = -2\)

C. \(\lim_{x \to 0} f(x) = 0\)

D. \(\lim_{x \to 0} f(x)\) does not exist

---

## Level 4 — Tricky / Trap-Based

## Q11 — MCQ

The value of \(\lim_{x \to 0} \dfrac{\sin x}{x^2}\) is

A. \(1\)

B. \(1/2\)

C. \(0\)

D. the two-sided limit does not exist as a real number

---

## Q12 — NAT

The value of \(\lim_{x \to \infty} \dfrac{x + \sin x}{x}\) is an integer. Enter that integer.

---

## Level 5 — Challenge

## Q13 — MSQ

Define \(f(x) = \dfrac{x^2 - 9}{x - 3}\) for \(x \neq 3\). Which of the following statements is/are true?

A. \(\lim_{x \to 3} f(x) = 6\)

B. The limit does not exist, because \(f(3)\) is undefined

C. If \(f(3)\) is defined to be \(6\), then \(f\) is continuous at \(x = 3\)

D. If \(f(3)\) is defined to be \(0\), then \(f\) is continuous at \(x = 3\)

---

## Q14 — NAT

The value of \(\lim_{x \to \infty} x\left(\sqrt{x^2 + 8} - x\right)\) is an integer. Enter that integer.

## Answer Key

| Q | Type | Answer |
|---|------|--------|
| 1 | MCQ | B |
| 2 | NAT | 6 |
| 3 | MCQ | C |
| 4 | NAT | 2 |
| 5 | MCQ | C |
| 6 | MSQ | A, B, C |
| 7 | NAT | 3 |
| 8 | MCQ | A |
| 9 | NAT | 1 |
| 10 | MSQ | A, B, D |
| 11 | MCQ | D |
| 12 | NAT | 1 |
| 13 | MSQ | A, C |
| 14 | NAT | 4 |

## Detailed Solutions

### Q1

Answer: B

Write \(\dfrac{\sin(5x)}{5x} = \dfrac{\sin u}{u}\) with \(u = 5x\). As \(x \to 0\), \(u \to 0\), so the standard limit gives \(1\).

(A) is the value of \(\sin 0\), which ignores the indeterminate form \(0/0\). (C) is \(\lim_{x \to 0} \sin(5x)/x\), which has an extra factor of \(5\) in the denominator removed. (D) fails because the left- and right-hand limits both equal \(1\).

### Q2

Answer: 6

For \(x \neq 3\), \(x^2 - 9 = (x - 3)(x + 3)\), so the quotient equals \(x + 3\). The limit is \(3 + 3 = 6\). The function is undefined at \(x = 3\), but the limit does not need the function value. A common wrong entry is \(0\), from substituting \(x = 3\) into the original \(0/0\) expression.

### Q3

Answer: C

The numerator and denominator both have degree \(2\). Divide by \(x^2\):

\[
\dfrac{6 - 1/x}{2 + 3/x^2} \to \dfrac{6}{2} = 3.
\]

(A) would be correct only if the denominator had higher degree. (B) is the ratio of the constant terms, or a misread of the leading coefficients as \(6/3\). (D) would be correct if the numerator had higher degree. L'Hôpital is unnecessary: the form is \(\infty/\infty\), but the leading-coefficient comparison already settles it.

### Q4

Answer: 2

Use \(1 - \cos \theta = 2\sin^2(\theta/2)\) with \(\theta = 2x\):

\[
\dfrac{1 - \cos(2x)}{x^2} = \dfrac{2\sin^2 x}{x^2} = 2\left(\dfrac{\sin x}{x}\right)^2 \to 2 \cdot 1 = 2.
\]

The standard limit \((1 - \cos x)/x^2 \to 1/2\) is a different argument. Replacing \(x\) by \(2x\) without adjusting the denominator produces the wrong value \(1/2\).

### Q5

Answer: C

\[
\dfrac{e^{4x} - 1}{x} = 4 \cdot \dfrac{e^{4x} - 1}{4x} \to 4 \cdot 1 = 4,
\]

because \((e^u - 1)/u \to 1\) as \(u = 4x \to 0\).

(A) comes from substituting \(x = 0\) into a \(0/0\) form. (B) is the unscaled standard limit \((e^x - 1)/x\). (D) is \(e^{4x}\) at \(x = 1\), not this limit.

### Q6

Answer: A, B, C

(A) \((1 + 3x)^{1/x} = \big[(1 + 3x)^{1/(3x)}\big]^3 \to e^3\).

(B) \(\big(1 + 3/x\big)^x = \big[(1 + 3/x)^{x/3}\big]^3 \to e^3\).

(C) \(\big(1 + 1/x\big)^{3x} = \big[(1 + 1/x)^x\big]^3 \to e^3\).

(D) \((1 + 3x)^{3/x} = \big[(1 + 3x)^{1/(3x)}\big]^9 \to e^9\), not \(e^3\). The extra \(3\) in the exponent stacks with the \(3\) already inside the base.

### Q7

Answer: 3

Rationalize:

\[
\dfrac{\sqrt{1 + 6x} - 1}{x} \cdot \dfrac{\sqrt{1 + 6x} + 1}{\sqrt{1 + 6x} + 1} = \dfrac{6}{\sqrt{1 + 6x} + 1} \to \dfrac{6}{2} = 3.
\]

Entering \(6\) keeps the unsimplified numerator and forgets the conjugate in the denominator at \(x = 0\).

### Q8

Answer: A

\(|\sin(1/x)| \le 1\), so \(-|x| \le x\sin(1/x) \le |x|\). Both \(-|x|\) and \(|x|\) tend to \(0\). The squeeze theorem gives the limit \(0\).

(B) is the bound on \(\sin\), not the product. (C) would be right for \(\sin(1/x)\) alone: oscillation prevents that limit. Multiplication by \(x\) damps the oscillation. (D) fails because the expression is trapped between two quantities that go to \(0\).

### Q9

Answer: 1

The form is \(0/0\). Differentiate numerator and denominator separately (L'Hôpital):

\[
\lim_{x \to 0} \dfrac{e^x - 1}{2x}.
\]

This is still \(0/0\). One more application gives

\[
\lim_{x \to 0} \dfrac{e^x}{2} = \dfrac{1}{2}.
\]

So \(p/2 = 1/2\) and \(p = 1\). Stopping after one differentiation and substituting \(x = 0\) still leaves \(0/0\). Using the quotient rule on the original fraction is not L'Hôpital.

### Q10

Answer: A, B, D

For \(x > 0\), \(|2x|/x = 2x/x = 2\). For \(x < 0\), \(|2x|/x = (-2x)/x = -2\). So (A) and (B) are true. The one-sided limits differ, so the two-sided limit does not exist and (D) is true. (C) is the average of the one-sided limits; a two-sided limit exists only when the one-sided limits are equal, and that common value is not \(0\).

### Q11

Answer: D

\[
\dfrac{\sin x}{x^2} = \dfrac{\sin x}{x} \cdot \dfrac{1}{x}.
\]

The first factor tends to \(1\), while \(1/x\) tends to \(+\infty\) from the right and to \(-\infty\) from the left. The two-sided limit is not a real number. The same split appears after one L'Hôpital step: \(\cos x/(2x)\) tends to \(+\infty\) from the right and \(-\infty\) from the left.

(A) is \(\lim \sin x/x\), which drops a factor of \(x\) from the denominator. (B) is \(\lim (1 - \cos x)/x^2\). (C) treats the \(0/0\) form as if it were the number \(0\). This is a \(0/0\) form, not an \(\infty/\infty\) form, and simplifying it does not produce a finite limit.

### Q12

Answer: 1

\[
\dfrac{x + \sin x}{x} = 1 + \dfrac{\sin x}{x}.
\]

Since \(|\sin x| \le 1\), \(\sin x/x \to 0\) as \(x \to \infty\). The limit is \(1\).

The form is \(\infty/\infty\), so L'Hôpital looks available: the derivative ratio is \(1 + \cos x\), which oscillates and has no limit. L'Hôpital applies only when that new limit exists (or is infinite). Here it does not, so the rule gives no conclusion. The algebraic rewrite still shows the original limit is \(1\). Entering \(0\) comes from thinking the oscillating derivative ratio means the original limit fails.

### Q13

Answer: A, C

For \(x \neq 3\), \(f(x) = x + 3\), so \(\lim_{x \to 3} f(x) = 6\). (A) is true. A limit does not require \(f(3)\) to be defined, so (B) is false. Continuity at \(3\) needs the function value to equal the limit. Setting \(f(3) = 6\) does that, so (C) is true. Setting \(f(3) = 0\) leaves a removable mismatch, so (D) is false.

### Q14

Answer: 4

The expression is an \(\infty \cdot 0\) form, because \(\sqrt{x^2 + 8} - x \to 0\) while \(x \to \infty\). Rationalize:

\[
x\big(\sqrt{x^2 + 8} - x\big) \cdot \dfrac{\sqrt{x^2 + 8} + x}{\sqrt{x^2 + 8} + x} = \dfrac{8x}{\sqrt{x^2 + 8} + x}.
\]

Divide numerator and denominator by \(x\) (with \(x > 0\)):

\[
\dfrac{8}{\sqrt{1 + 8/x^2} + 1} \to \dfrac{8}{1 + 1} = 4.
\]

Leaving the answer as \(8\), or as \(0\) because the second factor tends to \(0\), skips the rationalization. This is not a plain \(\infty/\infty\) polynomial comparison until after the conjugate is used.
