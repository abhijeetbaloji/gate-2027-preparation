# Random Variables — Practice Questions

Original practice for GATE CS. These questions are not from any GATE paper. Attempt the questions before reading the solutions.

## Level 1 — Conceptual

## Q1 — MCQ

A discrete random variable $X$ satisfies

$$
P(X=0)=\frac{1}{5},\quad P(X=1)=\frac{2}{5},\quad P(X=2)=\frac{2}{5}.
$$

Which one of the following is correct?

A. This is not a PMF, because the three probabilities are not equal.

B. This is a valid PMF.

C. This is not a PMF, because the probabilities sum to $4/5$.

D. This is a valid PDF of a continuous random variable, but not a PMF.

---

## Q2 — MCQ

A function $f$ is defined by $f(x)=5$ for $0\le x\le 1/5$, and $f(x)=0$ otherwise. Which one of the following is correct?

A. $f$ is not a PDF, because $f(x)>1$ on its support.

B. $f$ is not a PDF, because the length of the support is less than $1$.

C. $f$ is a valid PDF.

D. $f$ is a valid PMF of a discrete random variable.

---

## Q3 — NAT

A discrete random variable $X$ satisfies

$$
P(X=0)=\frac{1}{8},\quad P(X=2)=\frac{1}{2},\quad P(X=4)=\frac{3}{8}.
$$

If $E[X]=p/q$ in lowest terms, enter $p+q$.

---

## Level 2 — Standard GATE Style

## Q4 — MCQ

The CDF of a continuous random variable $X$ is $F(x)=0$ for $x<1$, $F(x)=(x-1)/6$ for $1\le x\le 7$, and $F(x)=1$ for $x>7$. Then $P(2\le X\le 5)$ equals

A. $1/6$

B. $1/3$

C. $1/2$

D. $2/3$

---

## Q5 — MCQ

For a random variable $X$, $E[X]=5$ and $E[X^2]=29$. Then $\mathrm{Var}(X)$ equals

A. $4$

B. $24$

C. $29$

D. $54$

---

## Q6 — NAT

A discrete random variable $X$ takes the value $-1$ with probability $3/4$ and the value $3$ with probability $1/4$. Enter the integer equal to $E[X^2]$.

---

## Q7 — MSQ

Select all that apply.

A. If $X$ is a continuous random variable, then $P(X=2)=0$.

B. A PDF may take a value strictly larger than $1$.

C. $E[X^2]=(E[X])^2$ for every random variable $X$.

D. Every CDF is a non-decreasing function.

---

## Level 3 — Multi-Step

## Q8 — MCQ

$\mathrm{Var}(X)=6$. Let $Y=-4X+9$. Then $\mathrm{Var}(Y)$ equals

A. $-24$

B. $24$

C. $96$

D. $105$

---

## Q9 — NAT

The function $f(x)=kx^2$ for $0\le x\le 3$, and $f(x)=0$ otherwise, is a PDF. If the constant $k$ equals $p/q$ in lowest terms, enter $p+q$.

---

## Q10 — MSQ

$X$ and $Y$ are independent, with $E[X]=4$, $E[Y]=-1$, $\mathrm{Var}(X)=3$, and $\mathrm{Var}(Y)=5$. Select all that apply.

A. $E[3X-2Y]=14$

B. $\mathrm{Var}(X+Y)=8$

C. $E[XY]=-4$

D. $\mathrm{Var}(X-Y)=-2$

---

## Level 4 — Tricky / Trap-Based

## Q11 — MCQ

$\mathrm{Var}(X)=3$, $\mathrm{Var}(Y)=5$, and $\mathrm{Cov}(X,Y)=-1$. Then $\mathrm{Var}(X+Y)$ equals

A. $8$

B. $6$

C. $7$

D. $4$

---

## Q12 — NAT

$E[X]=2$ and $\mathrm{Var}(X)=7$. Let $Y=3X-4$. Enter the integer $\mathrm{Var}(Y)$.

---

## Level 5 — Challenge

## Q13 — MCQ

The joint PMF of discrete random variables $X$ and $Y$ is

|  | $Y=0$ | $Y=1$ |
|---|------:|------:|
| $X=0$ | $1/8$ | $1/8$ |
| $X=1$ | $1/4$ | $1/2$ |

Which one of the following is correct?

A. $X$ and $Y$ are independent, and $E[X]=3/4$.

B. $X$ and $Y$ are not independent, and $E[X]=3/4$.

C. $X$ and $Y$ are not independent, and $E[X]=1/2$.

D. $X$ and $Y$ are independent, and $E[XY]=15/32$.

---

## Q14 — NAT

A continuous random variable $X$ has PDF $f(x)=3x^2$ for $0\le x\le 1$, and $f(x)=0$ otherwise. If $\mathrm{Var}(X)=p/q$ in lowest terms, enter $p+q$.

## Answer Key

| Q | Type | Answer |
|---|------|--------|
| 1 | MCQ | B |
| 2 | MCQ | C |
| 3 | NAT | 7 |
| 4 | MCQ | C |
| 5 | MCQ | A |
| 6 | NAT | 3 |
| 7 | MSQ | A, B, D |
| 8 | MCQ | C |
| 9 | NAT | 10 |
| 10 | MSQ | A, B, C |
| 11 | MCQ | B |
| 12 | NAT | 63 |
| 13 | MCQ | B |
| 14 | NAT | 83 |

## Detailed Solutions

### Q1

Add the point masses: $1/5+2/5+2/5=1$, and each term is nonnegative. A discrete PMF does not have to be uniform. So this is a valid PMF. Answer: **B**.

### Q2

The integral over the support is $5\cdot(1/5)=1$, and $f(x)\ge 0$. A PDF is a density, so its height may exceed $1$; only the area must equal $1$. It is not a PMF, because a PMF assigns probability to discrete points and each value is at most $1$. Answer: **C**.

### Q3

The probabilities sum to $1/8+4/8+3/8=1$.

$$
E[X]=0\cdot\frac{1}{8}+2\cdot\frac{1}{2}+4\cdot\frac{3}{8}=1+\frac{3}{2}=\frac{5}{2}.
$$

Thus $p+q=5+2=7$.

### Q4

For a continuous random variable, $P(2\le X\le 5)=F(5)-F(2)$, since the endpoints have probability $0$.

$$
F(5)=\frac{5-1}{6}=\frac{2}{3},\qquad F(2)=\frac{2-1}{6}=\frac{1}{6}.
$$

$$
F(5)-F(2)=\frac{4}{6}-\frac{1}{6}=\frac{1}{2}.
$$

Answer: **C**.

### Q5

$$
\mathrm{Var}(X)=E[X^2]-(E[X])^2=29-25=4.
$$

The value $29$ is the second moment, not the variance, and $54=29+25$ adds the two moments. Answer: **A**.

### Q6

$$
E[X]=(-1)\cdot\frac{3}{4}+3\cdot\frac{1}{4}=0.
$$

$$
E[X^2]=(-1)^2\cdot\frac{3}{4}+3^2\cdot\frac{1}{4}=\frac{3}{4}+\frac{9}{4}=3.
$$

So $E[X^2]=3$, while $(E[X])^2=0$. These are different quantities. The integer to enter is $3$.

### Q7

(A) is true: a continuous distribution gives probability $0$ to every single point.

(B) is true: the PDF in Q2 is an example with height $5$.

(C) is false: Q6 has $E[X^2]=3$ and $(E[X])^2=0$.

(D) is true: if $a<b$, then $F(a)=P(X\le a)\le P(X\le b)=F(b)$.

Answer: **A, B, D**.

### Q8

A shift does not change spread, and the coefficient is squared:

$$
\mathrm{Var}(-4X+9)=(-4)^2\mathrm{Var}(X)=16\cdot 6=96.
$$

Using $|-4|$ instead of $(-4)^2$ gives $24$. Adding the shift $9$ gives $105$. Variance cannot be negative. Answer: **C**.

### Q9

Nonnegativity forces $k\ge 0$. The total area must be $1$:

$$
\int_0^3 kx^2\,dx=k\left[\frac{x^3}{3}\right]_0^3=k\cdot\frac{27}{3}=9k=1.
$$

Hence $k=1/9$, and $p+q=1+9=10$.

### Q10

Linearity does not need independence:

$$
E[3X-2Y]=3\cdot 4-2\cdot(-1)=12+2=14.
$$

Independence gives $E[XY]=E[X]E[Y]=4\cdot(-1)=-4$, and it also gives covariance $0$, so

$$
\mathrm{Var}(X+Y)=\mathrm{Var}(X)+\mathrm{Var}(Y)=8,
$$

$$
\mathrm{Var}(X-Y)=\mathrm{Var}(X)+\mathrm{Var}(-Y)=\mathrm{Var}(X)+\mathrm{Var}(Y)=8.
$$

Subtracting the variances would produce $-2$, which is impossible. That claim is the false option.

Answer: **A, B, C**.

### Q11

In general,

$$
\mathrm{Var}(X+Y)=\mathrm{Var}(X)+\mathrm{Var}(Y)+2\mathrm{Cov}(X,Y)=3+5+2(-1)=6.
$$

Dropping the covariance term gives $8$. Adding $\mathrm{Cov}(X,Y)$ only once gives $7$. Answer: **B**.

### Q12

$$
\mathrm{Var}(3X-4)=3^2\cdot\mathrm{Var}(X)=9\cdot 7=63.
$$

The constant $-4$ does not appear in the variance. Enter $63$.

### Q13

The four joint probabilities sum to $1/8+1/8+2/8+4/8=1$.

$$
P(X=1)=\frac{1}{4}+\frac{1}{2}=\frac{3}{4},\qquad E[X]=\frac{3}{4}.
$$

$$
P(Y=0)=\frac{1}{8}+\frac{1}{4}=\frac{3}{8},\qquad P(X=0)=\frac{1}{4}.
$$

$$
P(X=0)P(Y=0)=\frac{1}{4}\cdot\frac{3}{8}=\frac{3}{32}\ne\frac{1}{8}=P(X=0,Y=0).
$$

So $X$ and $Y$ are not independent. Also $E[XY]=P(X=1,Y=1)=1/2$, whereas $E[X]E[Y]=(3/4)\cdot(5/8)=15/32$. Answer: **B**.

### Q14

First, $\int_0^1 3x^2\,dx=[x^3]_0^1=1$, so $f$ is a PDF.

$$
E[X]=\int_0^1 x\cdot 3x^2\,dx=3\int_0^1 x^3\,dx=3\cdot\frac{1}{4}=\frac{3}{4}.
$$

$$
E[X^2]=\int_0^1 x^2\cdot 3x^2\,dx=3\int_0^1 x^4\,dx=3\cdot\frac{1}{5}=\frac{3}{5}.
$$

$$
\mathrm{Var}(X)=\frac{3}{5}-\left(\frac{3}{4}\right)^2=\frac{48}{80}-\frac{45}{80}=\frac{3}{80}.
$$

Thus $p+q=3+80=83$.
