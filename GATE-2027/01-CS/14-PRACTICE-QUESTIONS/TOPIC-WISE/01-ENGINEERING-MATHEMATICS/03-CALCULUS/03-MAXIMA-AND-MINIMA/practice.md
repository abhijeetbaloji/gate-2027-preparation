# Maxima and Minima — Practice Questions

Original practice for GATE CS. These questions are not from any GATE paper. Attempt the questions before reading the solutions.

MSQ items may have more than one correct option. NAT items ask for an integer; enter only that integer.

## Level 1 — Conceptual

## Q1 — MCQ

Let \(f(x) = x^2 - 6x + 5\). Then

A. \(f\) has a local maximum at \(x = 3\)

B. \(f\) has a local minimum at \(x = 3\)

C. \(f\) has a local minimum at \(x = 6\)

D. \(f\) has no critical point

---

## Q2 — NAT

The local maximum value of \(f(x) = -x^2 + 4x + 1\) is an integer. Enter that integer.

---

## Q3 — MCQ

The absolute maximum value of \(f(x) = -x^2\) on the closed interval \([-1, 3]\) is

A. \(-9\)

B. \(-1\)

C. \(0\)

D. \(3\)

---

## Level 2 — Standard GATE Style

## Q4 — NAT

The number of critical points of \(f(x) = x^3 - 6x^2 + 9x\) is an integer. Enter that integer.

---

## Q5 — MCQ

The maximum value of \(f(x) = 6x - x^2\) is

A. \(3\)

B. \(6\)

C. \(9\)

D. \(18\)

---

## Q6 — MSQ

Let \(f(x) = x^4 - 2x^2\). Which of the following statements is/are true?

A. \(f\) has a local maximum at \(x = 0\), and \(f(0) = 0\)

B. \(f\) has a local minimum at \(x = 1\), and \(f(1) = -1\)

C. \(f\) has a local minimum at \(x = -1\), and \(f(-1) = -1\)

D. \(f\) has a local minimum at \(x = 0\)

---

## Level 3 — Multi-Step

## Q7 — NAT

The absolute minimum value of \(f(x) = x^2 - 4x + 1\) on \([0, 5]\) is an integer. A negative value is allowed. Enter that integer.

---

## Q8 — MCQ

A rectangle has perimeter \(28\). The maximum possible area of such a rectangle is

A. \(28\)

B. \(42\)

C. \(49\)

D. \(98\)

---

## Level 4 — Tricky / Trap-Based

## Q9 — MCQ

Let \(f(x) = x^3\). Which one of the following statements is true?

A. \(x = 0\) is a local maximum because \(f'(0) = 0\)

B. \(x = 0\) is a local minimum because \(f''(0) = 0\)

C. \(x = 0\) is a critical point but not a local extremum

D. \(f\) has a local maximum at \(x = 1\)

---

## Q10 — NAT

The absolute maximum value of \(f(x) = x^3 - 3x\) on \([-2, 3]\) is an integer. Enter that integer.

---

## Level 5 — Challenge

## Q11 — MSQ

Let \(f(x) = x^3 - 3x^2 - 9x + 2\). Which of the following statements is/are true?

A. \(f\) has a local maximum at \(x = -1\)

B. \(f\) has a local minimum at \(x = 3\)

C. \(f''(3) > 0\)

D. \(x = 0\) is a critical point of \(f\)

---

## Q12 — NAT

For \(x > 0\), let \(f(x) = x^2 + \dfrac{16}{x}\). The minimum value of \(f\) is an integer. Enter that integer.

## Answer Key

| Q | Type | Answer |
|---|------|--------|
| 1 | MCQ | B |
| 2 | NAT | 5 |
| 3 | MCQ | C |
| 4 | NAT | 2 |
| 5 | MCQ | C |
| 6 | MSQ | A, B, C |
| 7 | NAT | -3 |
| 8 | MCQ | C |
| 9 | MCQ | C |
| 10 | NAT | 18 |
| 11 | MSQ | A, B, C |
| 12 | NAT | 12 |

## Detailed Solutions

### Q1

Answer: B

\(f'(x) = 2x - 6 = 2(x - 3)\). The only critical point is \(x = 3\). Also \(f''(x) = 2 > 0\), so the second-derivative test gives a local minimum.

(A) uses the wrong sign of \(f''\). A positive second derivative means the graph is concave up, a local minimum. (C) sets the derivative equal to \(0\) as \(x = 6\) by reading \(f'(x) = 2x - 6\) as a root of the function rather than solving \(2x - 6 = 0\). (D) ignores the root of \(f'\).

### Q2

Answer: 5

\(f'(x) = -2x + 4 = 0\) gives \(x = 2\). Then \(f''(x) = -2 < 0\), so this critical point is a local maximum. The value is

\[
f(2) = -4 + 8 + 1 = 5.
\]

Entering \(2\) reports the location instead of the value. Entering \(4\) stops after \(4x\) at \(x = 2\) and drops \(-x^2 + 1\).

### Q3

Answer: C

\(f'(x) = -2x = 0\) only at \(x = 0\), which lies in \([-1, 3]\). Compare the critical value with the endpoints:

\[
f(-1) = -1, \quad f(0) = 0, \quad f(3) = -9.
\]

The largest is \(0\).

(A) is the endpoint \(x = 3\), which is the absolute minimum. (B) is the other endpoint. (D) is the right endpoint of the domain, not a function value of \(-x^2\). On a closed interval the absolute maximum can sit at an endpoint, but here the interior critical point wins. Both endpoints still have to be checked.

### Q4

Answer: 2

\(f'(x) = 3x^2 - 12x + 9 = 3(x^2 - 4x + 3) = 3(x - 1)(x - 3)\). The solutions are \(x = 1\) and \(x = 3\), two distinct critical points. The derivative exists everywhere, so there are no extra critical points where \(f'\) fails to exist. Entering \(3\) counts the degree of \(f\) instead of the roots of \(f'\).

### Q5

Answer: C

\(f'(x) = 6 - 2x = 0\) gives \(x = 3\). Then \(f''(x) = -2 < 0\), so \(x = 3\) is a maximum, and it is the global maximum because it is the only critical point and \(f(x) \to -\infty\) as \(|x| \to \infty\). The value is \(f(3) = 18 - 9 = 9\).

(A) is the critical point, not the value. (B) is the linear coefficient. (D) is \(6 \cdot 3\), which drops the \(-x^2\) term.

### Q6

Answer: A, B, C

\(f'(x) = 4x^3 - 4x = 4x(x^2 - 1) = 4x(x - 1)(x + 1)\). The critical points are \(x = -1, 0, 1\).

\(f''(x) = 12x^2 - 4\). Then \(f''(0) = -4 < 0\), so \(x = 0\) is a local maximum, and \(f(0) = 0\). (A) is true and (D) is false: the second derivative is negative, so the sign says maximum, not minimum.

\(f''(1) = 8 > 0\) and \(f''(-1) = 8 > 0\), so both are local minima. \(f(1) = 1 - 2 = -1\) and \(f(-1) = 1 - 2 = -1\). (B) and (C) are true.

A first-derivative check agrees. \(f'\) changes from negative to positive at \(x = -1\), from positive to negative at \(x = 0\), and from negative to positive at \(x = 1\).

### Q7

Answer: -3

\(f'(x) = 2x - 4 = 0\) gives \(x = 2\), which lies in \((0, 5)\). And \(f''(x) = 2 > 0\), so \(x = 2\) is a local minimum. Compare:

\[
f(0) = 1, \quad f(2) = 4 - 8 + 1 = -3, \quad f(5) = 25 - 20 + 1 = 6.
\]

The absolute minimum on \([0, 5]\) is \(-3\). The endpoint value \(1\) is larger. The other endpoint \(6\) is the absolute maximum. Entering \(1\) checks only the left endpoint. Entering \(2\) reports the critical point instead of \(f(2)\).

### Q8

Answer: C

Let the sides be \(x\) and \(y\). The perimeter condition is \(2(x + y) = 28\), so \(y = 14 - x\) with \(0 < x < 14\). The area is \(A(x) = x(14 - x) = 14x - x^2\).

\(A'(x) = 14 - 2x = 0\) gives \(x = 7\), so \(y = 7\) and \(A = 49\). Also \(A''(x) = -2 < 0\), confirming a maximum. The square has the largest area among rectangles of a fixed perimeter.

(A) is the perimeter. (B) is \(6 \cdot 7\), a non-critical rectangle. (D) is \(14 \cdot 7\), which uses the semi-perimeter as if it were the other side.

### Q9

Answer: C

\(f'(x) = 3x^2\) and \(f''(x) = 6x\). So \(f'(0) = 0\): \(x = 0\) is a critical point. But \(f''(0) = 0\), and the second-derivative test is inconclusive. The first-derivative test decides it: \(f'(x) = 3x^2 \ge 0\) on both sides of \(0\), and \(f'(x) = 0\) only at \(x = 0\). There is no sign change. Also \(f(-0.2) < 0 < f(0.2)\), so values immediately to the left are smaller and values immediately to the right are larger. The point is not a local maximum and not a local minimum.

(A) treats every zero of \(f'\) as a maximum. (B) treats \(f'' = 0\) as a minimum; that test gives no conclusion when the second derivative vanishes. (D) fails because \(f'(1) = 3 \neq 0\), and \(f\) is strictly increasing on \(\mathbb{R}\).

### Q10

Answer: 18

\(f'(x) = 3x^2 - 3 = 3(x - 1)(x + 1)\). The critical points in \([-2, 3]\) are \(x = -1\) and \(x = 1\).

\(f''(x) = 6x\). So \(f''(-1) = -6 < 0\) (local maximum) and \(f''(1) = 6 > 0\) (local minimum). The values to compare are

\[
\begin{align*}
f(-2) &= -8 + 6 = -2, \\
f(-1) &= -1 + 3 = 2, \\
f(1) &= 1 - 3 = -2, \\
f(3) &= 27 - 9 = 18.
\end{align*}
\]

The absolute maximum is \(18\), attained at the right endpoint. The local maximum value \(2\) is smaller. A zero derivative at an interior point is not automatically the absolute maximum on a closed interval. Entering \(2\) stops at the local maximum. Entering \(-2\) is the absolute minimum. The sign of \(f''\) identifies which critical point is a local maximum; it does not replace the endpoint comparison.

### Q11

Answer: A, B, C

\(f'(x) = 3x^2 - 6x - 9 = 3(x^2 - 2x - 3) = 3(x - 3)(x + 1)\). The critical points are \(x = -1\) and \(x = 3\). In particular \(f'(0) = -9 \neq 0\), so (D) is false.

\(f''(x) = 6x - 6\). Then \(f''(-1) = -12 < 0\), a local maximum, and \(f''(3) = 12 > 0\), a local minimum. So (A), (B), and (C) are true.

The first-derivative signs agree: \(f'\) changes from positive to negative at \(x = -1\), and from negative to positive at \(x = 3\). The corresponding values are \(f(-1) = 7\) and \(f(3) = -25\); the question asks for the type of each critical point, not those values. Reversing the second-derivative sign would swap (A) and (B).

### Q12

Answer: 12

For \(x > 0\),

\[
f'(x) = 2x - \dfrac{16}{x^2} = \dfrac{2(x^3 - 8)}{x^2}.
\]

The only positive root is \(x = 2\). Then

\[
f''(x) = 2 + \dfrac{32}{x^3}, \quad f''(2) = 2 + 4 = 6 > 0,
\]

so \(x = 2\) is a local minimum. It is the global minimum on \((0, \infty)\) because it is the only positive critical point, \(f(x) \to \infty\) as \(x \to 0^+\), and \(f(x) \to \infty\) as \(x \to \infty\). The minimum value is

\[
f(2) = 4 + \dfrac{16}{2} = 4 + 8 = 12.
\]

The negative root \(x = -2\) of \(f'(x) = 0\) is outside the stated domain. Entering \(4\) or \(8\) keeps only one term of \(f(2)\). Entering \(2\) reports the minimizer instead of the minimum value.
