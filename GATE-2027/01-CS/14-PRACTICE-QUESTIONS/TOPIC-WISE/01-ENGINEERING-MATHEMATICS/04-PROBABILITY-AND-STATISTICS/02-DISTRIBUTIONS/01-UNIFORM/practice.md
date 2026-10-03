# Uniform Distribution — Practice Questions

Original practice for GATE CS. These questions are not from any GATE paper. Attempt the questions before reading the solutions.

Notation used below: a discrete uniform random variable on the integers $a,a+1,\ldots,b$ assigns equal probability to each of those integers. A continuous uniform random variable on $[a,b]$ has constant PDF $1/(b-a)$ on that interval.

## Level 1 — Conceptual

## Q1 — MCQ

A fair six-sided die is rolled once, and $X$ is the face shown. Then $P(X\le 2)$ equals

A. $1/6$

B. $1/3$

C. $1/2$

D. $2/3$

---

## Q2 — MCQ

$X$ is continuous uniform on $[0,12]$. Then $P(3\le X\le 9)$ equals

A. $1/4$

B. $1/3$

C. $1/2$

D. $3/4$

---

## Q3 — NAT

$X$ is continuous uniform on $[4,16]$. Enter the integer $E[X]$.

---

## Level 2 — Standard GATE Style

## Q4 — MCQ

An integer is chosen uniformly from $4$ through $11$, inclusive. The number of possible values is

A. $7$

B. $8$

C. $11$

D. $15$

---

## Q5 — MCQ

$X$ is continuous uniform on $[2,8]$. Then $\mathrm{Var}(X)$ equals

A. $3$

B. $35/12$

C. $49/12$

D. $6$

---

## Q6 — NAT

$X$ is continuous uniform on $[a,12]$, and $E[X]=9$. Enter the integer $a$.

---

## Q7 — MSQ

$X$ is continuous uniform on $[-1,5]$. Select all that apply.

A. The PDF equals $1/6$ on $[-1,5]$.

B. $E[X]=2$.

C. $P(X=2)=1/6$.

D. $\mathrm{Var}(X)=3$.

---

## Level 3 — Multi-Step

## Q8 — MCQ

$X$ is discrete uniform on $\{0,1,2,3,4,5,6,7\}$. Then $\mathrm{Var}(X)$ equals

A. $21/4$

B. $49/12$

C. $16/3$

D. $8$

---

## Q9 — NAT

$X$ is continuous uniform on $[0,1]$, and $Y=6X+2$. Enter the integer $\mathrm{Var}(Y)$.

---

## Q10 — MSQ

$X$ is discrete uniform on $\{1,2,3,4,5\}$. Select all that apply.

A. $X$ has $5$ possible values.

B. $E[X]=3$.

C. $\mathrm{Var}(X)=2$.

D. $\mathrm{Var}(X)=4/3$.

---

## Level 4 — Tricky / Trap-Based

## Q11 — MCQ

$X$ is discrete uniform on $\{0,1,2,3,4,5\}$, and $Y$ is continuous uniform on $[0,5]$. Which one of the following is correct?

A. $E[X]=E[Y]$ and $\mathrm{Var}(X)=\mathrm{Var}(Y)$.

B. $E[X]=E[Y]=5/2$, $\mathrm{Var}(X)=35/12$, and $\mathrm{Var}(Y)=25/12$.

C. $X$ has $5$ possible values, so $\mathrm{Var}(X)=(25-1)/12$.

D. $P(Y=0)=1/6$.

---

## Q12 — NAT

$X$ is continuous uniform on $[a,b]$, with $E[X]=5$ and $\mathrm{Var}(X)=12$. The right endpoint $b$ is a positive integer. Enter $b$.

---

## Level 5 — Challenge

## Q13 — MCQ

$X$ is continuous uniform on $[0,2]$. Then $E[X^2]$ equals

A. $1$

B. $4/3$

C. $2$

D. $1/3$

---

## Q14 — NAT

$X$ is continuous uniform on $[0,4]$, $Y$ is continuous uniform on $[2,8]$, and $X$ and $Y$ are independent. If $\mathrm{Var}(X+Y)=p/q$ in lowest terms, enter $p+q$.

## Answer Key

| Q | Type | Answer |
|---|------|--------|
| 1 | MCQ | B |
| 2 | MCQ | C |
| 3 | NAT | 10 |
| 4 | MCQ | B |
| 5 | MCQ | A |
| 6 | NAT | 6 |
| 7 | MSQ | A, B, D |
| 8 | MCQ | A |
| 9 | NAT | 3 |
| 10 | MSQ | A, B, C |
| 11 | MCQ | B |
| 12 | NAT | 11 |
| 13 | MCQ | B |
| 14 | NAT | 16 |

## Detailed Solutions

### Q1

The die is discrete uniform on $\{1,2,3,4,5,6\}$, so each face has probability $1/6$. Two faces are at most $2$:

$$
P(X\le 2)=\frac{2}{6}=\frac{1}{3}.
$$

Answer: **B**.

### Q2

For a continuous uniform random variable, probability is length of the target interval divided by length of the support:

$$
P(3\le X\le 9)=\frac{9-3}{12-0}=\frac{6}{12}=\frac{1}{2}.
$$

The endpoints do not matter, because $P(X=3)=P(X=9)=0$. Answer: **C**.

### Q3

The mean of a continuous uniform random variable on $[a,b]$ is the midpoint:

$$
E[X]=\frac{4+16}{2}=10.
$$

Enter $10$.

### Q4

The integers from $4$ through $11$ inclusive are $4,5,6,7,8,9,10,11$. Their count is

$$
n=b-a+1=11-4+1=8.
$$

Using $b-a=7$ drops the left endpoint. Answer: **B**.

### Q5

The continuous-uniform variance uses the length $b-a=6$:

$$
\mathrm{Var}(X)=\frac{(8-2)^2}{12}=\frac{36}{12}=3.
$$

The value $35/12$ is the discrete-uniform variance for six points, $(n^2-1)/12$ with $n=6$. The value $49/12$ incorrectly uses $n=b-a+1=7$ inside the continuous formula. Answer: **A**.

### Q6

$$
\frac{a+12}{2}=9\implies a+12=18\implies a=6.
$$

Enter $6$.

### Q7

The length is $5-(-1)=6$, so the PDF is $1/6$ on $[-1,5]$ and $0$ outside. The mean is $(-1+5)/2=2$. The variance is $6^2/12=3$.

(C) is false: $X$ is continuous, so $P(X=2)=0$. The PDF value $1/6$ is not a point probability.

Answer: **A, B, D**.

### Q8

There are $n=8$ integers. The discrete-uniform variance is

$$
\mathrm{Var}(X)=\frac{n^2-1}{12}=\frac{64-1}{12}=\frac{63}{12}=\frac{21}{4}.
$$

Check with moments. $E[X]=(0+7)/2=7/2$ and

$$
E[X^2]=\frac{0^2+1^2+\cdots+7^2}{8}=\frac{140}{8}=\frac{35}{2},
$$

$$
\mathrm{Var}(X)=\frac{35}{2}-\left(\frac{7}{2}\right)^2=\frac{70}{4}-\frac{49}{4}=\frac{21}{4}.
$$

Option (B) is the continuous formula on $[0,7]$. Option (C) is $n^2/12$, which omits the $-1$. Answer: **A**.

### Q9

$Y=6X+2$ maps $[0,1]$ linearly onto $[2,8]$, so $Y$ is continuous uniform on $[2,8]$.

$$
\mathrm{Var}(Y)=\frac{(8-2)^2}{12}=\frac{36}{12}=3.
$$

The same result comes from scaling: $\mathrm{Var}(X)=1/12$ and $\mathrm{Var}(6X+2)=36\cdot(1/12)=3$. The added $2$ does not affect the variance. Enter $3$.

### Q10

Here $n=5$, so $E[X]=(1+5)/2=3$ and

$$
\mathrm{Var}(X)=\frac{5^2-1}{12}=\frac{24}{12}=2.
$$

(D) is the continuous formula $(5-1)^2/12=4/3$, which does not apply to this discrete uniform law.

Answer: **A, B, C**.

### Q11

For the discrete variable, $n=5-0+1=6$, so

$$
E[X]=\frac{0+5}{2}=\frac{5}{2},\qquad \mathrm{Var}(X)=\frac{36-1}{12}=\frac{35}{12}.
$$

For the continuous variable,

$$
E[Y]=\frac{0+5}{2}=\frac{5}{2},\qquad \mathrm{Var}(Y)=\frac{5^2}{12}=\frac{25}{12}.
$$

The means agree and the variances do not. Also $P(Y=0)=0$, because $Y$ is continuous. Answer: **B**.

### Q12

The midpoint and length conditions are

$$
\frac{a+b}{2}=5,\qquad \frac{(b-a)^2}{12}=12.
$$

So $a+b=10$ and $(b-a)^2=144$. Since $b>a$, $b-a=12$. Solving,

$$
b=\frac{(a+b)+(b-a)}{2}=\frac{10+12}{2}=11,\qquad a=\frac{10-12}{2}=-1.
$$

Check: length $12$, variance $144/12=12$, mean $(-1+11)/2=5$. Enter $11$.

### Q13

The PDF is $1/2$ on $[0,2]$.

$$
E[X^2]=\int_0^2 x^2\cdot\frac{1}{2}\,dx=\frac{1}{2}\left[\frac{x^3}{3}\right]_0^2=\frac{1}{2}\cdot\frac{8}{3}=\frac{4}{3}.
$$

Alternatively, $E[X]=1$ and $\mathrm{Var}(X)=2^2/12=1/3$, so

$$
E[X^2]=\mathrm{Var}(X)+(E[X])^2=\frac{1}{3}+1=\frac{4}{3}.
$$

Option (D) is the variance, not the second moment. Answer: **B**.

### Q14

$$
\mathrm{Var}(X)=\frac{4^2}{12}=\frac{4}{3},\qquad \mathrm{Var}(Y)=\frac{6^2}{12}=3.
$$

Independence gives

$$
\mathrm{Var}(X+Y)=\frac{4}{3}+3=\frac{4}{3}+\frac{9}{3}=\frac{13}{3}.
$$

Thus $p+q=13+3=16$.
