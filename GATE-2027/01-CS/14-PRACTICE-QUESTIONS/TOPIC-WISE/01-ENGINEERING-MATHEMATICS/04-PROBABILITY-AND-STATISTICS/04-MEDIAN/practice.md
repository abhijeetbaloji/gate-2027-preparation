# Median — Practice Questions

Original practice for GATE CS. These questions are not from any GATE paper. Attempt the questions before reading the solutions.

## Level 1 — Conceptual

## Q1 — MCQ

The median of the list \(9, 2, 7, 4, 1\) is

A. \(7\)

B. \(4\)

C. \(\dfrac{23}{5}\)

D. \(9\)

---

## Q2 — NAT

The observations are \(12, 5, 8, 15\). Enter the median.

---

## Level 2 — Standard GATE Style

## Q3 — MCQ

The median of \(4, 10, 2, 8, 6, 14\) is

A. \(6\)

B. \(7\)

C. \(8\)

D. \(\dfrac{22}{3}\)

---

## Q4 — NAT

A value \(1\) occurs \(3\) times, a value \(2\) occurs \(5\) times, and a value \(4\) occurs \(4\) times. Enter the median of this collection of \(12\) numbers.

---

## Q5 — MSQ

Select all that apply.

A. After the observations are sorted in increasing order, if \(n\) is odd then the median is the entry in position \((n+1)/2\).

B. If \(n\) is even, the median is the larger of the two central values.

C. For two numbers \(a\le b\), the median is \((a+b)/2\).

D. In a list of five numbers, replacing the largest number by any larger number does not change the median.

---

## Level 3 — Multi-Step

## Q6 — MCQ

Let \(X\) be continuous uniform on the interval \([2,14]\). The median of \(X\) is

A. \(6\)

B. \(8\)

C. \(2\)

D. \(14\)

---

## Q7 — NAT

The observations are \(3, 5, 6, 9, 40\). The mean exceeds the median. Enter \(10\) times that difference.

---

## Level 4 — Tricky / Trap-Based

## Q8 — MCQ

The ordered observations are \(1, 3, 5, 7, 9, 11, 13\). The largest observation is removed. The median of the remaining observations is

A. \(5\)

B. \(6\)

C. \(7\)

D. \(8\)

---

## Q9 — MSQ

The observations are \(1, 2, 3, 4, 50\). Select all that apply.

A. The median is \(3\).

B. The mean is \(12\).

C. Replacing \(50\) by \(500\) changes the median.

D. The mean is greater than the median.

---

## Level 5 — Challenge

## Q10 — NAT

The density \(f(x)=\dfrac{2x}{9}\) on the interval \(0\le x\le 3\), and \(f(x)=0\) elsewhere, is a valid probability density. Let \(m\) be its median. Enter the integer \(2m^2\).

## Answer Key

| Q | Type | Answer |
|---|------|--------|
| 1 | MCQ | B |
| 2 | NAT | 10 |
| 3 | MCQ | B |
| 4 | NAT | 2 |
| 5 | MSQ | A, C, D |
| 6 | MCQ | B |
| 7 | NAT | 66 |
| 8 | MCQ | B |
| 9 | MSQ | A, B, D |
| 10 | NAT | 9 |

## Detailed Solutions

### Q1

Sort first: \(1, 2, 4, 7, 9\). Here \(n=5\) is odd, so the median is the entry in position \((5+1)/2=3\), which is \(4\).

Option (A) is the middle entry of the unsorted list. Option (C) is the mean, \((9+2+7+4+1)/5=23/5\). Option (D) is the first recorded value. Answer: **B**.

### Q2

Sort: \(5, 8, 12, 15\). Here \(n=4\) is even, so the median is the average of the entries in positions \(n/2=2\) and \(n/2+1=3\):

\[
\frac{8+12}{2}=10.
\]

Using only \(8\), or only \(12\), drops the even-count rule. The mean is \((5+8+12+15)/4=10\) as well in this particular list, but the median calculation uses the two central ordered values. Answer: **10**.

### Q3

Sort: \(2, 4, 6, 8, 10, 14\). The two central positions are \(3\) and \(4\), with values \(6\) and \(8\). The median is

\[
\frac{6+8}{2}=7.
\]

Option (A) keeps only the lower central value. Option (C) keeps only the upper central value. Option (D) is the mean, \(44/6=22/3\). Answer: **B**.

### Q4

There are \(12\) numbers, so the median is the average of positions \(6\) and \(7\) in the ordered list. The ordered blocks are three \(1\)s (positions \(1\)–\(3\)), five \(2\)s (positions \(4\)–\(8\)), and four \(4\)s (positions \(9\)–\(12\)). Both position \(6\) and position \(7\) are \(2\), so the median is \((2+2)/2=2\).

The cumulative frequency first reaches \(n/2=6\) inside the block of \(2\)s, and the next central position is still inside that same block. Averaging \(2\) with \(4\) would be appropriate only if the two central positions fell in different values. Answer: **2**.

### Q5

(A) is the odd-count rule, after sorting.

(B) is false. For even \(n\), the median is the average of the two central ordered values, not the larger one alone.

(C) is the even-count rule for \(n=2\).

(D) is true for five observations. The median is the third ordered value. The largest observation occupies position \(5\), so increasing it does not move the third position.

(E) is false. The median is defined from the ordered list. The middle entry of the raw recording order is not the median in general.

Answer: **A, C, D**.

### Q6

On \([2,14]\) the cdf is \(F(x)=(x-2)/12\). The median solves \(F(m)=1/2\):

\[
\frac{m-2}{12}=\frac{1}{2}\implies m-2=6\implies m=8.
\]

The same value is the midpoint \((2+14)/2\), because this uniform distribution is symmetric. Option (A) is the half-width \(6\), not a location on the original scale. Options (C) and (D) are the endpoints, each of which has cdf \(0\) or \(1\), not \(1/2\). Answer: **B**.

### Q7

Sort: \(3, 5, 6, 9, 40\). The median is the third value, \(6\). The mean is

\[
\frac{3+5+6+9+40}{5}=\frac{63}{5}=12.6.
\]

The difference is \(12.6-6=6.6\), and \(10\) times that difference is \(66\). The observation \(40\) moves the mean and leaves the median at \(6\). Reporting \(10\) times the mean, which is \(126\), or \(10\) times the median, which is \(60\), answers a different question. Answer: **66**.

### Q8

The original median of seven ordered values is \(7\). After \(13\) is removed, the ordered list is \(1, 3, 5, 7, 9, 11\). Now \(n=6\) is even, so the median is the average of positions \(3\) and \(4\):

\[
\frac{5+7}{2}=6.
\]

Option (A) is only the lower central value. Option (C) is the old median, or only the upper central value of the new list. Option (D) is the average of \(7\) and \(9\), which are positions \(4\) and \(5\) rather than \(3\) and \(4\). Answer: **B**.

### Q9

Sort: \(1, 2, 3, 4, 50\). The median is \(3\), so (A) is true. The mean is \(60/5=12\), so (B) is true. Replacing \(50\) by \(500\) changes the mean to \(510/5=102\) and leaves the middle ordered value equal to \(3\), so (C) is false and (D) is true. For a distribution that is perfectly symmetric about its mean, the median equals the mean, so (E) is true.

Answer: **A, B, D**.

### Q10

For \(0\le x\le 3\),

\[
F(x)=\int_0^x \frac{2t}{9}\,dt=\frac{x^2}{9}.
\]

Check that \(F(3)=1\), so \(f\) is a density. The median solves \(F(m)=1/2\):

\[
\frac{m^2}{9}=\frac{1}{2}\implies m^2=\frac{9}{2}\implies 2m^2=9.
\]

The mean of this density is \(2\), and \(2\cdot 2^2=8\), which is what one gets by using the mean in place of the median. The density is largest at the right endpoint \(x=3\), so the mode is \(3\) and \(2\cdot 3^2=18\). Neither substitute is the median. Answer: **9**.
