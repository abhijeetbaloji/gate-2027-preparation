# Recurrence Relations — Practice Questions

Original practice for GATE CS. These questions are not from any GATE paper. Attempt the questions before reading the solutions.

## Level 1 — Conceptual

## Q1 — MCQ

The sequence defined by \(a_n = 3 a_{n-1}\) for \(n \ge 1\), with \(a_0 = 4\), satisfies \(a_3 =\)

A. 108
B. 36
C. 81
D. 12

---

## Q2 — MCQ

The order of the recurrence \(a_n + 2 a_{n-1} - a_{n-3} = 6\) is

A. 1
B. 2
C. 3
D. 6

---

## Q3 — NAT

Let \(b_0 = 2\), \(b_1 = 5\), and \(b_n = b_{n-1} + b_{n-2}\) for \(n \ge 2\). The value of \(b_6\) is ____.

---

## Q4 — MCQ

How many initial conditions are required to determine a unique solution of a linear homogeneous recurrence relation of order 3 with constant coefficients?

A. 1
B. 2
C. 3
D. 4

---

## Level 2 — Standard GATE Style

## Q5 — NAT

Let \(a_n = 5 a_{n-1} - 4 a_{n-2}\) for \(n \ge 2\), with \(a_0 = 3\) and \(a_1 = 6\). The value of \(a_4\) is ____.

---

## Q6 — MCQ

The general solution of \(a_n - 8 a_{n-1} + 16 a_{n-2} = 0\) is

A. \((A + Bn)\, 4^n\)
B. \(A \cdot 4^n + B \cdot 4^n\)
C. \(A \cdot 4^n + B \cdot (-4)^n\)
D. \((A + Bn)\, (-4)^n\)

---

## Q7 — MCQ

The sequence defined by \(a_n = 3 a_{n-1} + 4\) for \(n \ge 1\), with \(a_0 = 2\), has closed form

A. \(4 \cdot 3^n - 2\)
B. \(2 \cdot 3^n + 4\)
C. \(4 \cdot 3^n + 2\)
D. \(3^{n+1} - 2\)

---

## Q8 — NAT

Let \(c_0 = 1\), \(c_1 = 3\), and \(c_n = 2 c_{n-1} + c_{n-2}\) for \(n \ge 2\). The value of \(c_5\) is ____.

---

## Q9 — MSQ

Consider \(a_n - 10 a_{n-1} + 25 a_{n-2} = 0\). Select all that apply.

A. The number 5 is a repeated root of the characteristic equation
B. The general solution is \((A + Bn)\, 5^n\)
C. The general solution is \(A \cdot 5^n + B \cdot 25^n\)
D. The general solution contains exactly two arbitrary constants

---

## Level 3 — Multi-Step

## Q10 — NAT

Let \(a_n = 2 a_{n-1} + 3n\) for \(n \ge 1\), with \(a_0 = 0\). The value of \(a_4\) is ____.

---

## Q11 — MCQ

Let \(T(1)\) be a positive constant, and let \(T(n) = 8\, T(n/2) + n^2\) for \(n = 2^k\) with \(k \ge 1\). By the Master theorem, \(T(n)\) is

A. \(\Theta(n^3)\)
B. \(\Theta(n^3 \log n)\)
C. \(\Theta(n^2 \log n)\)
D. \(\Theta(n^2)\)

---

## Q12 — MCQ

Suppose \(a_n = 2 \cdot 4^n + 3 \cdot (-1)^n\) for every \(n \ge 0\). Which recurrence does this sequence satisfy for all \(n \ge 2\)?

A. \(a_n = 3 a_{n-1} + 4 a_{n-2}\)
B. \(a_n = 4 a_{n-1} + a_{n-2}\)
C. \(a_n = 3 a_{n-1} - 4 a_{n-2}\)
D. \(a_n = 4 a_{n-1} - a_{n-2}\)

---

## Q13 — NAT

Let \(a_n = 4 a_{n-1} - 3\) for \(n \ge 1\), with \(a_0 = 2\). The value of \(a_3\) is ____.

---

## Level 4 — Tricky / Trap-Based

## Q14 — MCQ

Let \(a_n = 6 a_{n-1} - 8 a_{n-2}\) for \(n \ge 2\), with \(a_0 = 3\) and \(a_1 = 10\). Then \(a_3\) equals

A. 136
B. 128
C. 36
D. 216

---

## Q15 — MCQ

Let \(a_n - 3 a_{n-1} = 2 \cdot 3^n\) for \(n \ge 1\), with \(a_0 = 1\). Then \(a_3\) equals

A. 189
B. 27
C. 54
D. 81

---

## Q16 — MSQ

Let \(a_n = 2 a_{n-1} - a_{n-2}\) for \(n \ge 2\), with \(a_0 = 3\) and \(a_1 = 5\). Select all that apply.

A. The characteristic root 1 is repeated
B. \(a_n = 3 + 2n\) for every \(n \ge 0\)
C. \(a_n = 3 \cdot 1^n + 5 \cdot 1^n\) for every \(n \ge 0\)
D. \(a_6 = 15\)

---

## Level 5 — Challenge

## Q17 — NAT

Let \(a_n = a_{n-1} + 6 a_{n-2}\) for \(n \ge 2\), with \(a_0 = 2\) and \(a_1 = 1\). The value of \(a_5\) is ____.

---

## Q18 — MSQ

Let \(a_n = 4 a_{n-1} - 4 a_{n-2} + 2\) for \(n \ge 2\), with \(a_0 = 1\) and \(a_1 = 4\). Select all that apply.

A. The constant sequence 2 is a particular solution
B. The homogeneous solution has the form \((A + Bn)\, 2^n\)
C. \(a_4 = 114\)
D. \(a_n = 2^n + 2\) for every \(n \ge 0\)

## Answer Key

| Q | Type | Answer |
|---|------|--------|
| 1 | MCQ | A |
| 2 | MCQ | C |
| 3 | NAT | 50 |
| 4 | MCQ | C |
| 5 | NAT | 258 |
| 6 | MCQ | A |
| 7 | MCQ | A |
| 8 | NAT | 99 |
| 9 | MSQ | A, B, D |
| 10 | NAT | 78 |
| 11 | MCQ | A |
| 12 | MCQ | A |
| 13 | NAT | 65 |
| 14 | MCQ | A |
| 15 | MCQ | A |
| 16 | MSQ | A, B, D |
| 17 | NAT | 211 |
| 18 | MSQ | A, B, C |

## Detailed Solutions

### Q1

Answer: A

Unfold the recurrence: \(a_n = 4 \cdot 3^n\). Therefore

\(a_3 = 4 \cdot 3^3 = 4 \cdot 27 = 108\).

The same value is obtained by iteration: \(a_1 = 12\), \(a_2 = 36\), \(a_3 = 108\).

### Q2

Answer: C

The order is the largest lag that appears. The relation expresses \(a_n\) using \(a_{n-1}\) and \(a_{n-3}\), so the order is 3. The constant 6 is a non-homogeneous term; it does not change the order.

### Q3

Answer: 50

Compute successive terms:

\(b_2 = 5 + 2 = 7\),

\(b_3 = 7 + 5 = 12\),

\(b_4 = 12 + 7 = 19\),

\(b_5 = 19 + 12 = 31\),

\(b_6 = 31 + 19 = 50\).

### Q4

Answer: C

A linear homogeneous relation of order \(k\) has a \(k\)-dimensional solution space. Exactly \(k\) independent initial values fix the \(k\) arbitrary constants. For order 3, three initial conditions are required.

### Q5

Answer: 258

The characteristic equation of \(a_n - 5 a_{n-1} + 4 a_{n-2} = 0\) is

\(r^2 - 5r + 4 = (r - 1)(r - 4) = 0\).

The roots 1 and 4 are distinct, so \(a_n = A + B \cdot 4^n\).

\(A + B = 3\),

\(A + 4B = 6\).

Subtraction gives \(3B = 3\), so \(B = 1\) and \(A = 2\). Thus \(a_n = 2 + 4^n\), and

\(a_4 = 2 + 4^4 = 2 + 256 = 258\).

Iteration agrees: \(a_2 = 5 \cdot 6 - 4 \cdot 3 = 18\), \(a_3 = 5 \cdot 18 - 4 \cdot 6 = 66\), \(a_4 = 5 \cdot 66 - 4 \cdot 18 = 330 - 72 = 258\).

### Q6

Answer: A

The characteristic equation is \(r^2 - 8r + 16 = (r - 4)^2 = 0\). The root 4 has multiplicity 2, so the general solution is

\((A + Bn)\, 4^n\).

Writing \(A \cdot 4^n + B \cdot 4^n\) uses only one independent solution. The root is \(+4\), so the base is not \(-4\).

### Q7

Answer: A

The homogeneous equation \(a_n = 3 a_{n-1}\) has solution \(A \cdot 3^n\). The forcing term is the constant 4, and constants are not homogeneous solutions, so try a constant particular solution \(c\):

\(c = 3c + 4 \Rightarrow -2c = 4 \Rightarrow c = -2\).

The general solution is \(A \cdot 3^n - 2\). The condition \(a_0 = 2\) gives \(A - 2 = 2\), so \(A = 4\) and

\(a_n = 4 \cdot 3^n - 2\).

Check: \(a_1 = 3 \cdot 2 + 4 = 10\), and \(4 \cdot 3 - 2 = 10\). The expression \(3^{n+1} - 2 = 3 \cdot 3^n - 2\) has the wrong coefficient of \(3^n\).

### Q8

Answer: 99

\(c_2 = 2 \cdot 3 + 1 = 7\),

\(c_3 = 2 \cdot 7 + 3 = 17\),

\(c_4 = 2 \cdot 17 + 7 = 41\),

\(c_5 = 2 \cdot 41 + 17 = 82 + 17 = 99\).

### Q9

Answer: A, B, D

The characteristic equation is \(r^2 - 10r + 25 = (r - 5)^2 = 0\). The root 5 has multiplicity 2, so

\(a_n = (A + Bn)\, 5^n\),

which contains the two constants \(A\) and \(B\). The form \(A \cdot 5^n + B \cdot 25^n\) would belong to the distinct roots 5 and 25.

### Q10

Answer: 78

The homogeneous solution is \(A \cdot 2^n\). The forcing term \(3n\) is linear, and neither constants nor linear polynomials solve the homogeneous equation, so try \(Bn + C\):

\(Bn + C = 2\bigl(B(n - 1) + C\bigr) + 3n = (2B + 3)n + (-2B + 2C)\).

Equating coefficients: \(B = 2B + 3\), so \(B = -3\), and \(C = -2B + 2C\), so \(C = 2B = -6\).

A particular solution is \(-3n - 6\). The general solution is

\(a_n = A \cdot 2^n - 3n - 6\).

From \(a_0 = 0\), \(A - 6 = 0\), hence \(A = 6\) and \(a_n = 6 \cdot 2^n - 3n - 6\). Therefore

\(a_4 = 6 \cdot 16 - 12 - 6 = 96 - 18 = 78\).

Iteration: \(a_1 = 3\), \(a_2 = 12\), \(a_3 = 33\), \(a_4 = 2 \cdot 33 + 12 = 78\).

### Q11

Answer: A

Here \(a = 8\), \(b = 2\), and \(\log_b a = \log_2 8 = 3\). Compare \(f(n) = n^2\) with \(n^{\log_b a} = n^3\). Since \(n^2 = O(n^{3 - \varepsilon})\) for \(\varepsilon = 1\), Master theorem case 1 applies:

\(T(n) = \Theta(n^3)\).

The factor \(\log n\) appears in case 2, when \(f(n)\) has the same order as \(n^{\log_b a}\).

### Q12

Answer: A

The closed form is a linear combination of \(4^n\) and \((-1)^n\), so the characteristic roots are 4 and \(-1\):

\((r - 4)(r + 1) = r^2 - 3r - 4 = 0\).

The recurrence is \(a_n - 3 a_{n-1} - 4 a_{n-2} = 0\), or

\(a_n = 3 a_{n-1} + 4 a_{n-2}\).

The first few terms are \(a_0 = 5\), \(a_1 = 5\), \(a_2 = 35\), \(a_3 = 125\). For example,

\(3 \cdot 5 + 4 \cdot 5 = 35\) and \(3 \cdot 35 + 4 \cdot 5 = 125\).

### Q13

Answer: 65

A constant particular solution satisfies \(c = 4c - 3\), so \(c = 1\). The homogeneous solution is \(A \cdot 4^n\), and

\(a_n = A \cdot 4^n + 1\).

From \(a_0 = 2\), \(A + 1 = 2\), so \(A = 1\) and \(a_n = 4^n + 1\). Hence

\(a_3 = 64 + 1 = 65\).

Iteration: \(a_1 = 8 - 3 = 5\), \(a_2 = 20 - 3 = 17\), \(a_3 = 68 - 3 = 65\).

### Q14

Answer: A

Rewrite the relation as \(a_n - 6 a_{n-1} + 8 a_{n-2} = 0\). The characteristic equation is

\(r^2 - 6r + 8 = (r - 2)(r - 4) = 0\).

Thus \(a_n = A \cdot 2^n + B \cdot 4^n\). The initial conditions give

\(A + B = 3\), \(2A + 4B = 10\).

The second equation simplifies to \(A + 2B = 5\). Subtraction yields \(B = 2\) and \(A = 1\), so

\(a_n = 2^n + 2 \cdot 4^n\).

\(a_3 = 2^3 + 2 \cdot 4^3 = 8 + 2 \cdot 64 = 136\).

Reversing both signs in the characteristic polynomial produces \(r^2 + 6r + 8 = 0\), whose roots are \(-2\) and \(-4\). Dropping the \(2^n\) term leaves \(2 \cdot 64 = 128\). The value \(a_2 = 6 \cdot 10 - 8 \cdot 3 = 36\) is one step too early, and \(6 \cdot 36 = 216\) keeps only the first term of the recurrence.

### Q15

Answer: A

The homogeneous solution is \(A \cdot 3^n\). The forcing term \(2 \cdot 3^n\) is itself a homogeneous solution, so a constant multiple of \(3^n\) cannot be a particular solution. Try \(Bn \cdot 3^n\):

\(Bn \cdot 3^n - 3 \cdot B(n - 1) \cdot 3^{n-1} = \bigl(Bn - B(n - 1)\bigr) 3^n = B \cdot 3^n\).

This equals \(2 \cdot 3^n\) when \(B = 2\). The general solution is \((A + 2n)\, 3^n\). From \(a_0 = 1\), \(A = 1\), so

\(a_n = (1 + 2n)\, 3^n\).

\(a_3 = (1 + 6) \cdot 27 = 189\).

Check: \(a_1 = 3 \cdot 1 + 2 \cdot 3 = 9\), and \((1 + 2) \cdot 3 = 9\); \(a_2 = 3 \cdot 9 + 2 \cdot 9 = 45\); \(a_3 = 3 \cdot 45 + 2 \cdot 27 = 135 + 54 = 189\).

Using a particular solution of the form \(B \cdot 3^n\) leaves the left side equal to 0 and cannot match the forcing term. The pure powers \(3^3 = 27\) and \(3^4 = 81\) are the homogeneous shapes that miss the factor \(n\).

### Q16

Answer: A, B, D

The characteristic equation is \(r^2 - 2r + 1 = (r - 1)^2 = 0\). The root 1 is repeated, so

\(a_n = (A + Bn) \cdot 1^n = A + Bn\).

Then \(A = 3\) and \(A + B = 5\), so \(B = 2\) and \(a_n = 3 + 2n\). In particular

\(a_6 = 3 + 12 = 15\).

The expression \(3 \cdot 1^n + 5 \cdot 1^n = 8\) is a constant sequence and does not satisfy \(a_1 = 5\). It also omits the factor \(n\) required by the repeated root.

### Q17

Answer: 211

The characteristic equation of \(a_n - a_{n-1} - 6 a_{n-2} = 0\) is

\(r^2 - r - 6 = (r - 3)(r + 2) = 0\).

Hence \(a_n = A \cdot 3^n + B \cdot (-2)^n\). The initial conditions give

\(A + B = 2\), \(3A - 2B = 1\).

Doubling the first equation produces \(2A + 2B = 4\). Adding that to the second equation gives \(5A = 5\), so \(A = 1\) and \(B = 1\). Therefore

\(a_n = 3^n + (-2)^n\), \(a_5 = 243 + (-32) = 211\).

Iteration: \(a_2 = 1 + 6 \cdot 2 = 13\), \(a_3 = 13 + 6 \cdot 1 = 19\), \(a_4 = 19 + 6 \cdot 13 = 97\), \(a_5 = 97 + 6 \cdot 19 = 211\).

### Q18

Answer: A, B, C

The homogeneous equation is \(a_n - 4 a_{n-1} + 4 a_{n-2} = 0\), with characteristic equation

\(r^2 - 4r + 4 = (r - 2)^2 = 0\).

The repeated root 2 gives the homogeneous solution \((A + Bn)\, 2^n\).

For a constant particular solution, substitute \(a_n = c\):

\(c = 4c - 4c + 2 \Rightarrow c = 2\).

The constant 2 works because a constant sequence is not a homogeneous solution: the left side of the homogeneous relation applied to the constant \(c\) equals \(c\), not 0. The general solution is

\(a_n = (A + Bn)\, 2^n + 2\).

From \(a_0 = 1\), \(A + 2 = 1\), so \(A = -1\). From \(a_1 = 4\),

\((A + B) \cdot 2 + 2 = 4 \Rightarrow 2(-1) + 2B + 2 = 4 \Rightarrow 2B = 4 \Rightarrow B = 2\).

Thus \(a_n = (-1 + 2n)\, 2^n + 2\), and

\(a_4 = (-1 + 8) \cdot 16 + 2 = 112 + 2 = 114\).

Iteration confirms the same value: \(a_2 = 4 \cdot 4 - 4 \cdot 1 + 2 = 14\), \(a_3 = 4 \cdot 14 - 4 \cdot 4 + 2 = 42\), \(a_4 = 4 \cdot 42 - 4 \cdot 14 + 2 = 168 - 56 + 2 = 114\).

The formula \(2^n + 2\) gives \(a_0 = 3\), which disagrees with the given initial value \(a_0 = 1\).
