# Generating Functions — Practice Questions

Original practice for GATE CS. These questions are not from any GATE paper. Attempt the questions before reading the solutions.

## Level 1 — Conceptual

## Q1 — MCQ

The ordinary generating function of the sequence \(a_n = 1\), for every \(n \ge 0\), is

A. \(\dfrac{1}{1 - x}\)
B. \(\dfrac{1}{(1 - x)^2}\)
C. \(e^x\)
D. \(\dfrac{x}{1 - x}\)

---

## Q2 — MCQ

The coefficient of \(x^2\) in \((1 + x)^9\) is

A. 36
B. 18
C. 84
D. 9

---

## Q3 — NAT

The coefficient of \(x^4\) in \(\dfrac{1}{1 - 3x}\) is ____.

---

## Level 2 — Standard GATE Style

## Q4 — NAT

The coefficient of \(x^5\) in \(\dfrac{1}{(1 - x)^4}\) is ____.

---

## Q5 — MCQ

The ordinary generating function of the sequence \(a_n = n\), for \(n \ge 0\), is

A. \(\dfrac{x}{(1 - x)^2}\)
B. \(\dfrac{1}{(1 - x)^2}\)
C. \(\dfrac{1}{1 - x}\)
D. \(\dfrac{x}{1 - x}\)

---

## Q6 — MCQ

Let \(G(x) = \sum_{n \ge 0} a_n x^n\) and \(H(x) = \sum_{n \ge 0} b_n x^n\). The coefficient of \(x^3\) in the product \(G(x) H(x)\) is

A. \(\sum_{k = 0}^{3} a_k b_{3 - k}\)
B. \(a_3 b_3\)
C. \(a_0 b_0 + a_3 b_3\)
D. \(a_3 + b_3\)

---

## Q7 — NAT

The coefficient of \(x^9\) in \((1 + x + x^2 + \cdots)^3\) is ____.

---

## Level 3 — Multi-Step

## Q8 — MCQ

The ordinary generating function of the sequence \(a_n = 4^n\), for \(n \ge 0\), is

A. \(\dfrac{1}{1 - 4x}\)
B. \(\dfrac{1}{(1 - x)^4}\)
C. \(\dfrac{4}{1 - x}\)
D. \(\dfrac{1}{4 - x}\)

---

## Q9 — NAT

The coefficient of \(x^4\) in \(\dfrac{1}{(1 - x)(1 - 2x)}\) is ____.

---

## Q10 — MSQ

Let \(C_n = \dfrac{1}{n + 1} C(2n, n)\) denote the \(n\)th Catalan number, with \(C_0 = 1\), and let \(C(x) = \sum_{n \ge 0} C_n x^n\). Select all that apply.

A. The number of valid parenthesis strings with 3 pairs is 5
B. \(C_4 = 14\)
C. \(C(x) = \dfrac{1}{1 - x\, C(x)}\)
D. \(C_3 = C(6, 3)\)

---

## Level 4 — Tricky / Trap-Based

## Q11 — MCQ

The exponential generating function of the sequence \(a_n = 1\), for every \(n \ge 0\), is

A. \(e^x\)
B. \(\dfrac{1}{1 - x}\)
C. \(\dfrac{1}{(1 - x)^2}\)
D. \(x e^x\)

---

## Q12 — MCQ

The coefficient of \(x^8\) in \(\dfrac{x^3}{(1 - x)^2}\) is

A. 6
B. 9
C. 7
D. 5

---

## Level 5 — Challenge

## Q13 — NAT

The coefficient of \(x^{10}\) in \((x^2 + x^3 + x^4 + \cdots)^3\) is ____.

---

## Q14 — MSQ

Let \(G(x) = \sum_{n \ge 0} (3n + 2)\, x^n\). Select all that apply.

A. \(G(x) = \dfrac{2 + x}{(1 - x)^2}\)
B. \(G(x) = \dfrac{2 - x}{(1 - x)^2}\)
C. The coefficient of \(x^4\) in \(G(x)\) is 14
D. \(G(x) = \dfrac{2}{1 - x} + \dfrac{3x}{(1 - x)^2}\)

## Answer Key

| Q | Type | Answer |
|---|------|--------|
| 1 | MCQ | A |
| 2 | MCQ | A |
| 3 | NAT | 81 |
| 4 | NAT | 56 |
| 5 | MCQ | A |
| 6 | MCQ | A |
| 7 | NAT | 55 |
| 8 | MCQ | A |
| 9 | NAT | 31 |
| 10 | MSQ | A, B, C |
| 11 | MCQ | A |
| 12 | MCQ | A |
| 13 | NAT | 15 |
| 14 | MSQ | A, C, D |

## Detailed Solutions

### Q1

Answer: A

The geometric series is

\(\dfrac{1}{1 - x} = \sum_{n \ge 0} x^n\),

so every coefficient is 1. The series \(1/(1 - x)^2\) has coefficients \(n + 1\). The series \(e^x = \sum x^n / n!\) is the exponential generating function of the same sequence, not the ordinary one. The series \(x/(1 - x) = \sum_{n \ge 1} x^n\) has constant term 0.

### Q2

Answer: A

By the binomial theorem, the coefficient of \(x^2\) in \((1 + x)^9\) is

\(C(9, 2) = \dfrac{9 \times 8}{2} = 36\).

### Q3

Answer: 81

\(\dfrac{1}{1 - 3x} = \sum_{n \ge 0} (3x)^n = \sum_{n \ge 0} 3^n x^n\).

The coefficient of \(x^4\) is \(3^4 = 81\).

### Q4

Answer: 56

The series \(1/(1 - x)^k\) has coefficient \(C(n + k - 1,\, n)\) on \(x^n\). Here \(k = 4\) and \(n = 5\):

\(C(5 + 4 - 1,\, 5) = C(8, 5) = C(8, 3) = \dfrac{8 \times 7 \times 6}{6} = 56\).

### Q5

Answer: A

Start from \(\sum_{n \ge 0} x^n = 1/(1 - x)\). Differentiating and multiplying by \(x\) produces

\(\sum_{n \ge 1} n x^n = \dfrac{x}{(1 - x)^2}\).

The constant term is 0, which matches \(a_0 = 0\). The series \(1/(1 - x)^2\) generates \(a_n = n + 1\), one larger than \(n\) at every index.

### Q6

Answer: A

The product of ordinary generating functions is the Cauchy product. The coefficient of \(x^3\) is

\(a_0 b_3 + a_1 b_2 + a_2 b_1 + a_3 b_0 = \sum_{k = 0}^{3} a_k b_{3 - k}\).

The term \(a_3 b_3\) is one summand of the coefficient of \(x^6\). Addition of coefficients belongs to the sum of series, not to their product.

### Q7

Answer: 55

\(1 + x + x^2 + \cdots = 1/(1 - x)\), so

\((1 + x + x^2 + \cdots)^3 = \dfrac{1}{(1 - x)^3}\).

The coefficient of \(x^9\) is

\(C(9 + 3 - 1,\, 9) = C(11, 9) = C(11, 2) = \dfrac{11 \times 10}{2} = 55\).

This is also the number of non-negative integer solutions of \(u + v + w = 9\).

### Q8

Answer: A

\(\dfrac{1}{1 - 4x} = \sum_{n \ge 0} 4^n x^n\).

The series \(1/(1 - x)^4\) generates the binomial coefficients \(C(n + 3,\, 3)\). The series \(4/(1 - x)\) generates the constant sequence 4. Finally,

\(\dfrac{1}{4 - x} = \dfrac{1}{4} \cdot \dfrac{1}{1 - x/4} = \sum_{n \ge 0} \dfrac{1}{4^{n+1}} x^n\),

whose coefficients are powers of \(1/4\).

### Q9

Answer: 31

Decompose

\(\dfrac{1}{(1 - x)(1 - 2x)} = \dfrac{A}{1 - x} + \dfrac{B}{1 - 2x}\).

Then \(A(1 - 2x) + B(1 - x) = 1\). Setting \(x = 1\) gives \(A(1 - 2) = 1\), so \(A = -1\). Setting \(x = 1/2\) gives \(B(1 - 1/2) = 1\), so \(B = 2\). Therefore

\(\dfrac{1}{(1 - x)(1 - 2x)} = -\dfrac{1}{1 - x} + \dfrac{2}{1 - 2x}\),

and the coefficient of \(x^n\) is

\(-1 + 2 \cdot 2^n = 2^{n+1} - 1\).

For \(n = 4\),

\(2^5 - 1 = 32 - 1 = 31\).

The same coefficient is the convolution \(\sum_{k = 0}^{4} 2^k = 1 + 2 + 4 + 8 + 16 = 31\).

### Q10

Answer: A, B, C

A: valid parenthesis strings with \(n\) pairs are counted by \(C_n\). For 3 pairs,

\(C_3 = \dfrac{1}{4} C(6, 3) = \dfrac{20}{4} = 5\).

B: \(C_4 = \dfrac{1}{5} C(8, 4) = \dfrac{70}{5} = 14\).

C: the Catalan generating function satisfies \(C(x) = 1 + x\, C(x)^2\). Rearrangement gives \(C(x) - x\, C(x)^2 = 1\), hence

\(C(x) \bigl(1 - x\, C(x)\bigr) = 1\), so \(C(x) = \dfrac{1}{1 - x\, C(x)}\).

D omits the factor \(1/(n + 1)\). The value \(C(6, 3) = 20\) is four times \(C_3\).

### Q11

Answer: A

The exponential generating function of \(\{a_n\}\) is \(\sum_{n \ge 0} a_n x^n / n!\). When \(a_n = 1\),

\(\sum_{n \ge 0} \dfrac{x^n}{n!} = e^x\).

The series \(1/(1 - x)\) is the ordinary generating function of the same sequence. The series \(x e^x = \sum_{n \ge 1} x^n / (n - 1)!\) is the exponential generating function of \(a_n = n\).

### Q12

Answer: A

The expansion \(1/(1 - x)^2 = \sum_{n \ge 0} (n + 1) x^n\) implies

\(\dfrac{x^3}{(1 - x)^2} = \sum_{n \ge 0} (n + 1) x^{n + 3}\).

The power \(x^8\) arises when \(n + 3 = 8\), so \(n = 5\), and the coefficient is \(5 + 1 = 6\).

Equivalently, multiplying by \(x^3\) shifts indices by 3, and the coefficient of \(x^5\) in \(1/(1 - x)^2\) is 6.

The coefficient of \(x^8\) in \(1/(1 - x)^2\) itself is 9; that count forgets the factor \(x^3\). Shifting by 4 instead of 3 reads the coefficient of \(x^4\), which is 5. The neighbouring integer 7 is one away from the correct shift.

### Q13

Answer: 15

Factor the smallest power out of each series:

\(x^2 + x^3 + x^4 + \cdots = \dfrac{x^2}{1 - x}\).

Cubing gives

\(\left(\dfrac{x^2}{1 - x}\right)^3 = \dfrac{x^6}{(1 - x)^3}\).

The coefficient of \(x^{10}\) in this series is the coefficient of \(x^4\) in \(1/(1 - x)^3\):

\(C(4 + 3 - 1,\, 4) = C(6, 4) = C(6, 2) = \dfrac{6 \times 5}{2} = 15\).

In stars-and-bars language, each of the three factors contributes at least 2, leaving 4 unrestricted non-negative exponents to distribute among 3 factors.

### Q14

Answer: A, C, D

Use \(\sum_{n \ge 0} x^n = 1/(1 - x)\) and \(\sum_{n \ge 1} n x^n = x/(1 - x)^2\):

\(G(x) = 3 \sum_{n \ge 0} n x^n + 2 \sum_{n \ge 0} x^n = \dfrac{3x}{(1 - x)^2} + \dfrac{2}{1 - x}\).

The second expression is D. The common denominator \((1 - x)^2\) gives

\(G(x) = \dfrac{3x + 2(1 - x)}{(1 - x)^2} = \dfrac{3x + 2 - 2x}{(1 - x)^2} = \dfrac{2 + x}{(1 - x)^2}\),

which is A. The sign in the numerator of B is the opposite of this calculation. The coefficient of \(x^4\) is the sequence term itself:

\(3 \cdot 4 + 2 = 14\).

Expanding B instead produces coefficients \(n + 2\), and the coefficient of \(x^4\) would be 6.
