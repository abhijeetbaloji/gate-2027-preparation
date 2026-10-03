# Mode — Practice Questions

Original practice for GATE CS. These questions are not from any GATE paper. Attempt the questions before reading the solutions.

## Level 1 — Conceptual

## Q1 — MCQ

In the list \(4, 6, 6, 9, 6, 4, 6, 6\), the mode is

A. \(4\)

B. \(6\)

C. \(9\)

D. \(5\)

---

## Q2 — NAT

The observations are \(2, 2, 3, 3, 3, 5, 5, 8\). Enter the mode.

---

## Level 2 — Standard GATE Style

## Q3 — MCQ

In a frequency table, \(4\) occurs \(3\) times, \(7\) occurs \(6\) times, \(9\) occurs \(6\) times, and \(12\) occurs \(2\) times. The number of modes is

A. \(0\)

B. \(1\)

C. \(2\)

D. \(4\)

---

## Q4 — NAT

A discrete random variable satisfies \(P(X=0)=0.1\), \(P(X=1)=0.25\), \(P(X=2)=0.4\), and \(P(X=3)=0.25\). Enter the mode of \(X\).

---

## Q5 — MSQ

Select all that apply.

A. A mode of a data set is a value of highest frequency.

B. A data set may have two modes.

C. For a continuous random variable, the probability of equaling the mode is positive.

D. The discrete uniform distribution on \(\{1,2,3,4\}\) has a unique mode.

---

## Level 3 — Multi-Step

## Q6 — MCQ

Grouped data have class frequencies \(0\)–\(10\): \(4\), \(10\)–\(20\): \(9\), \(20\)–\(30\): \(6\), and \(30\)–\(40\): \(3\). The modal class is

A. \(0\)–\(10\)

B. \(10\)–\(20\)

C. \(20\)–\(30\)

D. \(30\)–\(40\)

---

## Q7 — NAT

A discrete distribution has

\[
P(X=1)=0.15,\; P(X=2)=0.35,\; P(X=3)=0.10,\; P(X=4)=0.05,\; P(X=5)=0.35.
\]

The distribution has two modes. Enter the sum of the modes.

---

## Level 4 — Tricky / Trap-Based

## Q8 — MCQ

The observations are \(1, 1, 1, 4, 4, 4, 7, 9\). Which one of the following is correct?

A. The unique mode is \(1\).

B. The unique mode is \(4\).

C. The data are bimodal, with modes \(1\) and \(4\).

D. The data have no mode, because the highest frequency is shared by two values.

---

## Q9 — MSQ

Select all that apply.

A. For \(\lambda>0\), the mode of the exponential density \(\lambda e^{-\lambda x}\) on \(x\ge 0\) is \(0\).

B. The continuous uniform density on \([2,8]\) has a unique mode at \(5\).

C. For a continuous random variable, the probability of the single point equal to a mode is \(0\).

D. The mode of a data set must lie between the mean and the median.

---

## Level 5 — Challenge

## Q10 — NAT

The density \(f(x)=6x(1-x)\) on \(0\le x\le 1\), and \(f(x)=0\) elsewhere, has a unique mode \(m\). Enter \(100m\).

## Answer Key

| Q | Type | Answer |
|---|------|--------|
| 1 | MCQ | B |
| 2 | NAT | 3 |
| 3 | MCQ | C |
| 4 | NAT | 2 |
| 5 | MSQ | A, B |
| 6 | MCQ | B |
| 7 | NAT | 7 |
| 8 | MCQ | C |
| 9 | MSQ | A, C |
| 10 | NAT | 50 |

## Detailed Solutions

### Q1

The value \(4\) occurs twice, \(6\) occurs five times, and \(9\) occurs once. The highest frequency is \(5\), so the mode is \(6\).

Option (A) is a value that occurs, but not most often. Option (C) occurs only once. Option (D) does not occur at all; it is the count of the \(6\)s, not a data value. Answer: **B**.

### Q2

The value \(2\) occurs twice, \(3\) occurs three times, \(5\) occurs twice, and \(8\) occurs once. The unique highest frequency is \(3\), so the mode is \(3\).

The mean is \((2+2+3+3+3+5+5+8)/8=31/8\), which is not an observation of highest frequency. The median of the eight ordered values is the average of \(3\) and \(3\), which happens to be \(3\) here, but the mode is identified by the frequency count. Answer: **3**.

### Q3

The frequencies are \(3, 6, 6, 2\). The maximum frequency is \(6\), and it is attained by both \(7\) and \(9\). Two modes means the data are bimodal, so the number of modes is \(2\).

Option (A) would describe a flat distribution in which every value ties, or the convention “no unique mode” applied too broadly. Here two values are strictly more frequent than the others, so those two are modes. Option (B) drops one of the tied values. Option (D) counts every distinct value, including those with lower frequency. Answer: **C**.

### Q4

Compare the point masses: \(0.1, 0.25, 0.4, 0.25\). The maximum is \(0.4\), attained only at \(x=2\). The mode of a discrete distribution is a value that maximizes the pmf.

The mean is \(0\cdot 0.1+1\cdot 0.25+2\cdot 0.4+3\cdot 0.25=1.9\), which is not a mode. The two values with probability \(0.25\) are tied with each other but are below the maximum. Answer: **2**.

### Q5

(A) is the definition for raw or frequency data.

(B) is true: a tie for the strictly highest frequency produces more than one mode.

(C) is false. A continuous distribution assigns probability \(0\) to every single point. The mode is a peak of the density, not a point of positive probability.

(D) is false. On \(\{1,2,3,4\}\) each value has probability \(1/4\), so every value ties. There is no unique mode.

(E) is true. A normal density peaks at its mean, so the mode, the median, and the mean agree.

Answer: **A, B**.

### Q6

The class frequencies are \(4, 9, 6, 3\). The modal class is the class of highest frequency, which is \(10\)–\(20\).

No interpolation inside the class is required to name the modal class. Option (A) is the first class. Option (C) is the class with the second-highest frequency. Option (D) is the class with the lowest frequency. Answer: **B**.

### Q7

The probabilities sum to \(0.15+0.35+0.10+0.05+0.35=1\). The maximum probability is \(0.35\), attained at both \(2\) and \(5\). Those are the two modes, and their sum is \(2+5=7\).

The mean is \(1\cdot 0.15+2\cdot 0.35+3\cdot 0.10+4\cdot 0.05+5\cdot 0.35=3.1\), which lies between the two modes and is not itself a mode. Reporting only one of \(2\) or \(5\) misses the tie. Answer: **7**.

### Q8

The value \(1\) occurs three times, \(4\) occurs three times, and \(7\) and \(9\) occur once each. The highest frequency is \(3\), shared by \(1\) and \(4\). The data are bimodal.

Options (A) and (B) each discard one of the tied modes. Option (D) uses the “no mode” description that fits a completely flat distribution, in which every value has the same frequency. Here \(7\) and \(9\) are less frequent, so the two peaks are genuine modes. Answer: **C**.

### Q9

(A) is true. For \(x\ge 0\), \(\lambda e^{-\lambda x}\) is strictly decreasing, so its maximum is at \(x=0\). The mean \(1/\lambda\) is positive, so the mode and the mean differ.

(B) is false. A continuous uniform density is constant on \([2,8]\). Every point has the same density, so there is no unique mode at the midpoint \(5\).

(C) is true. Continuity of the distribution forces \(P(X=m)=0\) even when \(m\) maximizes the density.

(D) is false. For an exponential density with parameter \(\lambda>0\), the mode is \(0\), the median is \((\ln 2)/\lambda\), and the mean is \(1/\lambda\). The mode lies outside the interval with endpoints at the mean and the median.

(E) is the definition of the modal class.

Answer: **A, C**.

### Q10

On \([0,1]\),

\[
\int_0^1 6x(1-x)\,dx=6\left[\frac{x^2}{2}-\frac{x^3}{3}\right]_0^1=6\left(\frac{1}{2}-\frac{1}{3}\right)=1,
\]

so \(f\) is a density. Then \(f(x)=6x-6x^2\) and \(f'(x)=6-12x\). The unique critical point in \([0,1]\) is \(x=1/2\). Since \(f(0)=f(1)=0\) and \(f(1/2)=3/2>0\), this critical point is the mode. Thus \(m=1/2\) and \(100m=50\).

The endpoints maximize nothing. Reporting \(100\) times the maximum density \(3/2\), which is \(150\), answers a different question. Answer: **50**.
