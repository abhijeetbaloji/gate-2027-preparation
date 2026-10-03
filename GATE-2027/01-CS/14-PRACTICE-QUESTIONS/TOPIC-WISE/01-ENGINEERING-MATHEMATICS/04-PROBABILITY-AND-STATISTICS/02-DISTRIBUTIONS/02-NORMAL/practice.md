# Normal Distribution — Practice Questions

Original practice for GATE CS. These questions are not from any GATE paper. Attempt the questions before reading the solutions.

Notation: $X\sim N(\mu,\sigma^2)$ means $X$ is normal with mean $\mu$ and variance $\sigma^2$. The standard normal CDF is $\Phi(z)=P(Z\le z)$ for $Z\sim N(0,1)$. Use only the values of $\Phi$ stated in a question, together with $\Phi(-z)=1-\Phi(z)$.

## Level 1 — Conceptual

## Q1 — MCQ

$X\sim N(40,9)$. Which one of the following is correct?

A. The mean is $40$ and the standard deviation is $9$.

B. The mean is $40$ and the standard deviation is $3$.

C. The mean is $9$ and the standard deviation is $40$.

D. The mean is $40$ and the variance is $3$.

---

## Q2 — MCQ

$Z\sim N(0,1)$. Which one of the following is correct?

A. $P(Z>0)=1/2$

B. $P(Z=0)=1/2$

C. $P(Z>1)=P(Z>-1)$

D. $P(Z<0)=1$

---

## Q3 — NAT

$X\sim N(6,4)$. Enter the integer equal to $100\cdot P(X>6)$.

---

## Level 2 — Standard GATE Style

## Q4 — MCQ

Use $\Phi(1)=0.8413$. Let $X\sim N(20,25)$. Then $P(X\le 25)$ equals

A. $0.8413$

B. $0.1587$

C. $0.5000$

D. $0.6826$

---

## Q5 — MCQ

$X\sim N(4,9)$ and $Y=2X+1$. Then

A. $Y\sim N(9,18)$

B. $Y\sim N(9,36)$

C. $Y\sim N(8,36)$

D. $Y\sim N(9,12)$

---

## Q6 — NAT

$X\sim N(15,16)$. Enter the integer equal to the $z$-score $(23-\mu)/\sigma$.

---

## Level 3 — Multi-Step

## Q7 — MCQ

$X\sim N(2,4)$ and $Y\sim N(5,9)$ are independent. Then $X+Y$ follows

A. $N(7,13)$

B. $N(7,5)$

C. $N(7,25)$

D. $N(10,13)$

---

## Q8 — NAT

Use $\Phi(2)=0.9772$ exactly as given. Let $X\sim N(30,25)$. Enter the integer equal to $10000\cdot P(X\le 40)$.

---

## Level 4 — Tricky / Trap-Based

## Q9 — MSQ

$X\sim N(\mu,\sigma^2)$ with $\sigma>0$. Select all that apply.

A. $P(X>\mu)=1/2$

B. $P(X=\mu)=0$

C. The median of $X$ is $\mu$

D. If $Y$ is an independent copy of $X$, then the standard deviation of $X+Y$ is $2\sigma$

---

## Q10 — NAT

$X\sim N(0,4)$ and $Y\sim N(0,12)$ are independent. Enter the integer $\mathrm{Var}(X-Y)$.

---

## Level 5 — Challenge

## Q11 — MCQ

Use $\Phi(0.5)=0.6915$ and $\Phi(1)=0.8413$. Let $X\sim N(10,4)$. Then $P(9\le X\le 12)$ equals

A. $0.5328$

B. $0.1498$

C. $0.6915$

D. $0.8413$

---

## Q12 — NAT

$X\sim N(3,5)$ and $Y\sim N(-1,2)$ are independent. Let $W=-2X+3Y$. Enter the integer $\mathrm{Var}(W)$.

## Answer Key

| Q | Type | Answer |
|---|------|--------|
| 1 | MCQ | B |
| 2 | MCQ | A |
| 3 | NAT | 50 |
| 4 | MCQ | A |
| 5 | MCQ | B |
| 6 | NAT | 2 |
| 7 | MCQ | A |
| 8 | NAT | 9772 |
| 9 | MSQ | A, B, C |
| 10 | NAT | 16 |
| 11 | MCQ | A |
| 12 | NAT | 38 |

## Detailed Solutions

### Q1

In $N(\mu,\sigma^2)$, the second parameter is the variance. Here $\sigma^2=9$, so $\sigma=3$, and the mean is $40$. Using $9$ itself as the standard deviation is the parameter swap. Answer: **B**.

### Q2

The standard normal density is symmetric about $0$, so the upper half has probability $1/2$: $P(Z>0)=1/2$.

(B) is false because a normal random variable is continuous, so $P(Z=0)=0$.

(C) is false: $P(Z>-1)=\Phi(1)>1/2$, while $P(Z>1)=1-\Phi(1)<1/2$.

(D) would put the entire distribution on the negative side. Answer: **A**.

### Q3

The mean is $6$, and a normal distribution is symmetric about its mean, so $P(X>6)=1/2$. Therefore

$$
100\cdot P(X>6)=50.
$$

The variance $4$ is not needed. Enter $50$.

### Q4

The variance is $25$, so $\sigma=5$. Standardize the endpoint:

$$
P(X\le 25)=P\left(Z\le\frac{25-20}{5}\right)=P(Z\le 1)=\Phi(1)=0.8413.
$$

The value $0.1587$ is the upper tail $1-\Phi(1)$. The value $0.5000$ is $P(X\le 20)$. Answer: **A**.

### Q5

$$
E[Y]=2\cdot 4+1=9,\qquad \mathrm{Var}(Y)=2^2\cdot 9=36.
$$

A linear function of a normal random variable is normal, so $Y\sim N(9,36)$.

Option (A) multiplies the variance by $2$ instead of by $2^2$. Option (C) forgets the shift $+1$. Option (D) scales the standard deviation by $2$ and then treats that result as a variance, or otherwise fails to square the coefficient against $\sigma^2$. Answer: **B**.

### Q6

$\sigma^2=16$, so $\sigma=4$. The $z$-score is

$$
\frac{23-15}{4}=2.
$$

Enter $2$.

### Q7

Independence lets the variances add. The means always add:

$$
E[X+Y]=2+5=7,\qquad \mathrm{Var}(X+Y)=4+9=13.
$$

The sum of independent normals is normal, so $X+Y\sim N(7,13)$.

Option (C) adds the standard deviations first: $\sigma_X+\sigma_Y=2+3=5$, then squares that sum to get variance $25$. Standard deviations do not add. Answer: **A**.

### Q8

$\sigma=\sqrt{25}=5$, and

$$
P(X\le 40)=P\left(Z\le\frac{40-30}{5}\right)=\Phi(2)=0.9772.
$$

Using the given value exactly,

$$
10000\cdot 0.9772=9772.
$$

Enter $9772$.

### Q9

(A) is symmetry about the mean. (B) is the continuous point-mass fact $P(X=\mu)=0$. (C) holds because the normal distribution is symmetric, so mean and median coincide.

(D) is false. Independence gives $\mathrm{Var}(X+Y)=2\sigma^2$, so the standard deviation is $\sigma\sqrt{2}$, not $2\sigma$.

Answer: **A, B, C**.

### Q10

$$
\mathrm{Var}(X-Y)=\mathrm{Var}(X)+\mathrm{Var}(-Y)=\mathrm{Var}(X)+\mathrm{Var}(Y)=4+12=16,
$$

where the second step uses independence. Subtracting the variances would give $8$, which is not the variance of a difference. Enter $16$.

### Q11

$\sigma=\sqrt{4}=2$. The endpoints standardize as

$$
\frac{9-10}{2}=-0.5,\qquad \frac{12-10}{2}=1.
$$

$$
\begin{align*}
P(9\le X\le 12)
&= \Phi(1)-\Phi(-0.5)\\
&= 0.8413-\bigl(1-0.6915\bigr)\\
&= 0.8413-0.3085\\
&= 0.5328.
\end{align*}
$$

Option (B) is $\Phi(1)-\Phi(0.5)=0.1498$, which forgets to convert the negative $z$-score. Answer: **A**.

### Q12

The coefficients are squared, and independence lets the two contributions add:

$$
\mathrm{Var}(W)=(-2)^2\mathrm{Var}(X)+3^2\mathrm{Var}(Y)=4\cdot 5+9\cdot 2=20+18=38.
$$

The means are not needed for the variance. Enter $38$.
