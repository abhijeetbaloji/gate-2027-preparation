# Standard Deviation — Practice Questions

Original practice for GATE CS. These questions are not from any GATE paper. Attempt the questions before reading the solutions.

## Level 1 — Conceptual

## Q1 — MCQ

The numbers \(1, 5, 5, 9\) are an entire population. Their population standard deviation is

A. \(2\)

B. \(2\sqrt{2}\)

C. \(8\)

D. \(4\)

---

## Q2 — NAT

A random variable has variance \(36\). Enter its standard deviation.

---

## Q3 — MCQ

For a sample of \(n=5\) observations, the sum of squared deviations from the sample mean is \(20\). The unbiased sample variance is

A. \(4\)

B. \(5\)

C. \(20\)

D. \(\sqrt{5}\)

---

## Level 2 — Standard GATE Style

## Q4 — MCQ

If the standard deviation of \(X\) is \(5\), then the standard deviation of \(2X+7\) is

A. \(10\)

B. \(17\)

C. \(12\)

D. \(5\)

---

## Q5 — NAT

The random variables \(X\) and \(Y\) are independent, with standard deviations \(5\) and \(12\). Enter the standard deviation of \(X+Y\).

---

## Q6 — MSQ

Select all that apply.

A. The variance of a random variable is the square of its standard deviation.

B. For constants \(a\) and \(b\), the standard deviation of \(aX+b\) is \(|a|\) times the standard deviation of \(X\).

C. If \(X\) and \(Y\) are independent, then the standard deviation of \(X+Y\) equals the sum of the two standard deviations.

D. If \(X\) and \(Y\) are independent, then \(\mathrm{Var}(X+Y)=\mathrm{Var}(X)+\mathrm{Var}(Y)\).

---

## Level 3 — Multi-Step

## Q7 — MCQ

Suppose \(P(X=0)=\dfrac{1}{4}\), \(P(X=2)=\dfrac{1}{2}\), and \(P(X=4)=\dfrac{1}{4}\). The standard deviation of \(X\) is

A. \(\sqrt{2}\)

B. \(2\)

C. \(6\)

D. \(4\)

---

## Q8 — NAT

Treat \(4, 6, 8, 10\) as an entire population. Enter the population variance.

---

## Level 4 — Tricky / Trap-Based

## Q9 — MCQ

The random variables \(X\) and \(Y\) are independent, with standard deviations \(6\) and \(8\). The standard deviation of \(X+Y\) is

A. \(10\)

B. \(14\)

C. \(48\)

D. \(100\)

---

## Q10 — MSQ

A population has variance \(9\), so its standard deviation is \(3\). Select all that apply.

A. Multiplying every observation by \(-2\) changes the standard deviation from \(3\) to \(6\).

B. Adding \(4\) to every observation changes the variance from \(9\) to \(13\).

C. The unbiased sample variance divides the sum of squared deviations from the sample mean by \(n-1\).

D. Variances of independent random variables add.

---

## Level 5 — Challenge

## Q11 — NAT

Suppose \(P(X=0)=\dfrac{1}{2}\), \(P(X=1)=\dfrac{1}{3}\), and \(P(X=3)=\dfrac{1}{6}\). Enter the integer \(36\cdot\mathrm{Var}(X)\).

---

## Q12 — MCQ

The random variables \(X\) and \(Y\) are independent, with \(\mathrm{Var}(X)=4\) and \(\mathrm{Var}(Y)=9\). The standard deviation of \(2X-Y\) is

A. \(5\)

B. \(7\)

C. \(1\)

D. \(25\)

## Answer Key

| Q | Type | Answer |
|---|------|--------|
| 1 | MCQ | B |
| 2 | NAT | 6 |
| 3 | MCQ | B |
| 4 | MCQ | A |
| 5 | NAT | 13 |
| 6 | MSQ | A, B, D |
| 7 | MCQ | A |
| 8 | NAT | 5 |
| 9 | MCQ | A |
| 10 | MSQ | A, C, D |
| 11 | NAT | 41 |
| 12 | MCQ | A |

## Detailed Solutions

### Q1

The population mean is \((1+5+5+9)/4=5\). The squared deviations are \(16, 0, 0, 16\), and their sum is \(32\). The population variance divides by \(N=4\):

\[
\sigma^2=\frac{32}{4}=8,\qquad \sigma=\sqrt{8}=2\sqrt{2}.
\]

Option (A) is \(\sqrt{4}\), as if the variance had been \(4\). Option (C) is the variance, not the standard deviation. Option (D) is half the variance. The unbiased sample variance would divide by \(3\), giving \(32/3\), whose square root is not listed. The question asks for the population standard deviation. Answer: **B**.

### Q2

By definition, the standard deviation is the non-negative square root of the variance:

\[
\sigma=\sqrt{36}=6.
\]

Leaving the answer as \(36\) confuses variance with standard deviation. Using \(36^2=1296\) squares when the definition takes a square root. Answer: **6**.

### Q3

The unbiased sample variance is

\[
s^2=\frac{1}{n-1}\sum_{i=1}^{n}(x_i-\bar x)^2=\frac{20}{4}=5.
\]

Option (A) divides by \(n=5\), which is the population-style divisor, not the unbiased sample divisor. Option (C) stops before dividing. Option (D) is the sample standard deviation corresponding to variance \(5\), not the variance itself. Answer: **B**.

### Q4

A shift does not change spread, and a scale factor \(a\) multiplies the standard deviation by \(|a|\):

\[
\mathrm{SD}(2X+7)=|2|\cdot 5=10.
\]

Option (B) is \(2\cdot 5+7\), which incorrectly adds the shift to the standard deviation. Option (C) uses \(2\cdot 5+2\). Option (D) ignores the factor \(2\). The variance would be multiplied by \(2^2=4\), becoming \(100\), and the standard deviation is the square root of that scaled variance. Answer: **A**.

### Q5

Independence lets the variances add. The variances are \(25\) and \(144\), so

\[
\mathrm{SD}(X+Y)=\sqrt{25+144}=\sqrt{169}=13.
\]

Adding the standard deviations gives \(5+12=17\), which is not the standard deviation of the sum. Answer: **13**.

### Q6

(A) is the relation \(\mathrm{Var}(X)=(\mathrm{SD}(X))^2\).

(B) is the scaling rule. The absolute value appears because a negative scale reverses direction but does not make spread negative.

(C) is false. For independent \(X\) and \(Y\), the variances add, so the standard deviation of the sum is \(\sqrt{\sigma_X^2+\sigma_Y^2}\), not \(\sigma_X+\sigma_Y\).

(D) is the independence rule for variances.

(E) is true: a constant has no spread, so its variance and its standard deviation are both \(0\).

Answer: **A, B, D**.

### Q7

\[
E[X]=0\cdot\frac{1}{4}+2\cdot\frac{1}{2}+4\cdot\frac{1}{4}=2,
\]

\[
E[X^2]=0\cdot\frac{1}{4}+4\cdot\frac{1}{2}+16\cdot\frac{1}{4}=2+4=6.
\]

Hence \(\mathrm{Var}(X)=6-2^2=2\), and the standard deviation is \(\sqrt{2}\).

Option (B) is the variance, or the mean. Option (C) is \(E[X^2]\). Option (D) is \((E[X])^2\). Forgetting to subtract \((E[X])^2\) from \(E[X^2]\) is the usual source of those three wrong values. Answer: **A**.

### Q8

The population mean is \((4+6+8+10)/4=7\). The deviations are \(-3,-1,1,3\), and the squared deviations sum to \(9+1+1+9=20\). Dividing by the population size \(N=4\) gives

\[
\sigma^2=\frac{20}{4}=5.
\]

The unbiased sample variance would be \(20/3\). The question states that the four numbers are the entire population, so the divisor is \(4\). The population standard deviation is \(\sqrt{5}\), which was not requested. Answer: **5**.

### Q9

Independence gives

\[
\mathrm{Var}(X+Y)=6^2+8^2=36+64=100,
\]

so \(\mathrm{SD}(X+Y)=\sqrt{100}=10\).

Option (B) adds the standard deviations. Option (C) is the product \(6\cdot 8\). Option (D) is the variance of the sum, not the standard deviation. Standard deviation is not linear. Answer: **A**.

### Q10

(A) is true because \(\mathrm{SD}(-2X)=|-2|\cdot 3=6\). The sign of the multiplier does not appear in the standard deviation.

(B) is false. Adding a constant does not change variance. The variance stays \(9\), rather than becoming \(9+4\).

(C) is the definition of the unbiased sample variance. It is distinct from the population formula, which divides by \(n\).

(D) is true when the variables are independent (uncorrelated is the precise covariance condition; independence is the sufficient condition used here).

(E) is false. The correct identity is \(\mathrm{Var}(3X)=3^2\mathrm{Var}(X)=9\,\mathrm{Var}(X)\). The factor \(3\) without a square belongs to the standard deviation, not to the variance.

Answer: **A, C, D**.

### Q11

The probabilities sum to \(1/2+1/3+1/6=1\). Then

\[
E[X]=1\cdot\frac{1}{3}+3\cdot\frac{1}{6}=\frac{1}{3}+\frac{1}{2}=\frac{5}{6},
\]

\[
E[X^2]=1\cdot\frac{1}{3}+9\cdot\frac{1}{6}=\frac{1}{3}+\frac{3}{2}=\frac{11}{6}.
\]

\[
\mathrm{Var}(X)=\frac{11}{6}-\left(\frac{5}{6}\right)^2=\frac{66}{36}-\frac{25}{36}=\frac{41}{36}.
\]

Therefore \(36\cdot\mathrm{Var}(X)=41\).

Using \((E[X])^2\) alone gives \(25\). Using \(E[X^2]\) without subtracting the squared mean, and then multiplying by \(6\), gives \(11\). Both omit part of the computational formula \(\mathrm{Var}(X)=E[X^2]-(E[X])^2\). Answer: **41**.

### Q12

Independence gives \(\mathrm{Var}(2X-Y)=\mathrm{Var}(2X)+\mathrm{Var}(-Y)\). A minus sign does not reduce variance, because \(\mathrm{Var}(-Y)=\mathrm{Var}(Y)\). Scaling by \(2\) multiplies variance by \(4\):

\[
\mathrm{Var}(2X-Y)=4\cdot 4+9=16+9=25,
\]

so the standard deviation is \(\sqrt{25}=5\).

Option (B) is \(\mathrm{SD}(2X)+\mathrm{SD}(Y)=4+3\), adding standard deviations. Option (C) is \(\mathrm{SD}(2X)-\mathrm{SD}(Y)=4-3\), which treats the minus sign as subtraction of spread. Option (D) is the variance of \(2X-Y\), not the standard deviation. Answer: **A**.
