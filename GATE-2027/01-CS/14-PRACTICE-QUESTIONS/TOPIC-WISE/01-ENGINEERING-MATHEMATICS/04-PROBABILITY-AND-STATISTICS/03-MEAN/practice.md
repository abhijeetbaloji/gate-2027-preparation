# Mean — Practice Questions

Original practice for GATE CS. These questions are not from any GATE paper. Attempt the questions before reading the solutions.

## Level 1 — Conceptual

## Q1 — MCQ

The arithmetic mean of the observations \(5, 9, 11, 15\) is

A. \(10\)

B. \(11\)

C. \(9\)

D. \(40\)

---

## Q2 — NAT

The five numbers \(3, 6, 8, 10, 13\) are an entire population. Enter the population mean \(\mu\).

---

## Q3 — MCQ

A discrete random variable \(X\) satisfies \(P(X=0)=\dfrac{1}{5}\), \(P(X=2)=\dfrac{2}{5}\), and \(P(X=5)=\dfrac{2}{5}\). Then \(E[X]\) equals

A. \(\dfrac{7}{5}\)

B. \(\dfrac{14}{5}\)

C. \(2\)

D. \(7\)

---

## Level 2 — Standard GATE Style

## Q4 — MCQ

If \(E[X]=6\) and \(Y=4X-5\), then \(E[Y]\) equals

A. \(19\)

B. \(24\)

C. \(29\)

D. \(4\)

---

## Q5 — NAT

A course grade uses three components: a lab score of \(72\) with weight \(1\), a midterm score of \(84\) with weight \(2\), and a final score of \(90\) with weight \(3\). Enter the weighted mean.

---

## Q6 — MSQ

Select all that apply.

A. The arithmetic mean of \(n\) observations is their sum divided by \(n\).

B. \(E[X+Y]=E[X]+E[Y]\) holds only when \(X\) and \(Y\) are independent.

C. If a constant \(c\) is added to every observation, the mean increases by \(c\).

D. For every random variable \(X\), \(E[X^2]=(E[X])^2\).

---

## Level 3 — Multi-Step

## Q7 — MCQ

In a frequency table, the value \(2\) occurs \(4\) times, the value \(5\) occurs \(6\) times, and the value \(8\) occurs \(5\) times. The mean is

A. \(5\)

B. \(\dfrac{26}{5}\)

C. \(\dfrac{15}{2}\)

D. \(78\)

---

## Q8 — NAT

The observations are \(6, 8, 8, 11, 17\). One of the observations equal to \(8\) is replaced by \(18\). Enter the new mean.

---

## Level 4 — Tricky / Trap-Based

## Q9 — MCQ

Section A has \(12\) students and mean score \(64\). Section B has \(28\) students and mean score \(79\). The mean of all \(40\) students is

A. \(\dfrac{143}{2}\)

B. \(\dfrac{149}{2}\)

C. \(79\)

D. \(64\)

---

## Q10 — MSQ

The observations are \(2, 3, 4, 5, 86\). Select all that apply.

A. The mean is \(20\).

B. The median is \(20\).

C. Multiplying every observation by \(-1\) multiplies the mean by \(-1\).

D. The unweighted average of the means of the groups \(\{2,3\}\) and \(\{4,5,86\}\) equals the overall mean.

---

## Level 5 — Challenge

## Q11 — NAT

Eight observations have mean \(15\). One new observation equal to \(33\) is included. Every observation in the resulting list of nine numbers is then increased by \(4\). Enter the final mean.

---

## Q12 — NAT

The random variable \(X\) takes the values \(1, 4, 7\), each with probability \(\dfrac{1}{3}\). Enter the integer \(E[X^2]\).

## Answer Key

| Q | Type | Answer |
|---|------|--------|
| 1 | MCQ | A |
| 2 | NAT | 8 |
| 3 | MCQ | B |
| 4 | MCQ | A |
| 5 | NAT | 85 |
| 6 | MSQ | A, C |
| 7 | MCQ | B |
| 8 | NAT | 12 |
| 9 | MCQ | B |
| 10 | MSQ | A, C |
| 11 | NAT | 21 |
| 12 | NAT | 22 |

## Detailed Solutions

### Q1

\[
\frac{5+9+11+15}{4}=\frac{40}{4}=10.
\]

The mean does not require the data to be sorted. Option (B) is the larger of the two middle values after sorting, which is a median ingredient, not the mean. Option (C) is the smaller of those middle values. Option (D) is the total, before dividing by the count. Answer: **A**.

### Q2

For a population of \(N=5\) values,

\[
\mu=\frac{3+6+8+10+13}{5}=\frac{40}{5}=8.
\]

The population mean uses the same average as a sample mean. The divisor is \(N\), not \(N-1\); the \(N-1\) divisor belongs to an unbiased sample variance, not to the mean. Answer: **8**.

### Q3

\[
E[X]=0\cdot\frac{1}{5}+2\cdot\frac{2}{5}+5\cdot\frac{2}{5}=\frac{4}{5}+\frac{10}{5}=\frac{14}{5}.
\]

Option (A) uses only the middle term \(2\cdot(2/5)\). Option (C) is the ordinary average of the support \(\{0,2,5\}\), which ignores the unequal probabilities. Option (D) is the sum of the values that have positive probability, with no weighting and no division. Answer: **B**.

### Q4

Linearity gives \(E[aX+b]=aE[X]+b\), with no independence assumption required:

\[
E[Y]=4\cdot 6-5=19.
\]

Option (B) is \(4E[X]\), dropping the shift. Option (C) adds \(5\) instead of subtracting it. Option (D) subtracts \(5\) from \(E[X]\) and ignores the factor \(4\). Answer: **A**.

### Q5

\[
\frac{1\cdot 72+2\cdot 84+3\cdot 90}{1+2+3}=\frac{72+168+270}{6}=\frac{510}{6}=85.
\]

An unweighted average of the three scores is \((72+84+90)/3=82\), which treats the final as equal to the lab. The weights must appear both in the numerator and in the denominator. Answer: **85**.

### Q6

(A) is the definition of the arithmetic mean.

(B) is false. \(E[X+Y]=E[X]+E[Y]\) holds for every pair of random variables whose expectations exist, including dependent pairs. Independence is the extra condition used for adding variances, not means.

(C) is the shift rule: the mean of \(x_i+c\) is \(\bar x+c\).

(D) is false. \(E[X^2]=(E[X])^2\) only in special cases, such as a constant random variable. In general \(E[g(X)]\neq g(E[X])\).

(E) matches the definitions \(\bar x=(1/n)\sum x_i\) and \(\mu=(1/N)\sum x_i\): same averaging formula, different symbols.

Answer: **A, C**.

### Q7

The total frequency is \(4+6+5=15\), and

\[
\sum f_i x_i=2\cdot 4+5\cdot 6+8\cdot 5=8+30+40=78,
\]

so the mean is \(78/15=26/5\).

Option (A) is the unweighted average \((2+5+8)/3\), which ignores frequencies. Option (C) is half the total frequency. Option (D) is \(\sum f_i x_i\) before dividing by \(\sum f_i\). Answer: **B**.

### Q8

The original sum is \(6+8+8+11+17=50\), so the original mean is \(50/5=10\). Replacing \(8\) by \(18\) increases the sum by \(10\). The new sum is \(60\), and the new mean is \(60/5=12\).

A common slip is to add \(10\) to the mean itself, producing \(20\), instead of spreading the increase of \(10\) across five observations. Answer: **12**.

### Q9

Group sizes differ, so the overall mean is the size-weighted average:

\[
\frac{12\cdot 64+28\cdot 79}{40}=\frac{768+2212}{40}=\frac{2980}{40}=\frac{149}{2}.
\]

Option (A) is \((64+79)/2\), the unweighted average of the two section means. That equals the overall mean only when the sections have the same size. Option (C) uses only the larger section. Option (D) uses only the smaller section. Answer: **B**.

### Q10

The sum is \(2+3+4+5+86=100\), so the mean is \(100/5=20\). Thus (A) is true.

The ordered list is \(2,3,4,5,86\), so the median is \(4\), not \(20\). Thus (B) is false. The single large observation pulls the mean far above the median.

(C) is the scaling rule \(E[aX]=aE[X]\) with \(a=-1\), so it is true.

For (D), the group means are \((2+3)/2=5/2\) and \((4+5+86)/3=95/3\). Their unweighted average is

\[
\frac{1}{2}\left(\frac{5}{2}+\frac{95}{3}\right)=\frac{205}{12}\neq 20.
\]

The groups have sizes \(2\) and \(3\), so averaging the group means equally is not the overall mean. Thus (D) is false.

For (E), adding \(10\) to one observation adds \(10/5=2\) to the mean. Thus (E) is true.

Answer: **A, C**.

### Q11

After the new observation is included, the mean of the nine numbers is

\[
\frac{8\cdot 15+33}{9}=\frac{120+33}{9}=\frac{153}{9}=17.
\]

Adding \(4\) to every observation then adds \(4\) to the mean, so the final mean is \(17+4=21\).

Using \((15+33)/2=24\) ignores the original sample size. Adding \(4\) before combining the new observation, or adding \(4\) only to \(33\), changes the numerator and does not give \(21\). Answer: **21**.

### Q12

\[
E[X^2]=1^2\cdot\frac{1}{3}+4^2\cdot\frac{1}{3}+7^2\cdot\frac{1}{3}=\frac{1+16+49}{3}=\frac{66}{3}=22.
\]

The mean itself is \(E[X]=(1+4+7)/3=4\), and \((E[X])^2=16\). Squaring the mean is the wrong calculation: \(E[X^2]\neq (E[X])^2\) because \(X\) is not constant. The gap \(22-16=6\) is \(\mathrm{Var}(X)\), which is not what was asked. Answer: **22**.
