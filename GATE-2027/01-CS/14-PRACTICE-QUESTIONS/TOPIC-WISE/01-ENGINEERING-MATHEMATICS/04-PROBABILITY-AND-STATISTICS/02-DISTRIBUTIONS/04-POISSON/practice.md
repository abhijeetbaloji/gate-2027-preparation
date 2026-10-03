# Poisson Distribution — Practice Questions

Original practice for GATE CS. These questions are not from any GATE paper. Attempt the questions before reading the solutions.

Notation: $X\sim\mathrm{Poisson}(\lambda)$ means

$$
P(X=k)=e^{-\lambda}\frac{\lambda^k}{k!},\qquad k=0,1,2,\ldots,
$$

with $E[X]=\mathrm{Var}(X)=\lambda$.

## Level 1 — Conceptual

## Q1 — MCQ

$X\sim\mathrm{Poisson}(2)$. Then $P(X=0)$ equals

A. $e^{-2}$

B. $2e^{-2}$

C. $e^{-1}$

D. $1-e^{-2}$

---

## Q2 — MCQ

For $X\sim\mathrm{Poisson}(\lambda)$, which one of the following is correct?

A. $E[X]=\lambda$ and $\mathrm{Var}(X)=\lambda^2$

B. $E[X]=\lambda$ and $\mathrm{Var}(X)=\lambda$

C. $E[X]=1/\lambda$ and $\mathrm{Var}(X)=1/\lambda^2$

D. $E[X]=\lambda$ and $\mathrm{Var}(X)=\lambda(1-\lambda)$

---

## Q3 — NAT

$X\sim\mathrm{Poisson}(5)$. Enter the integer $E[X]+\mathrm{Var}(X)$.

---

## Level 2 — Standard GATE Style

## Q4 — MCQ

$X\sim\mathrm{Poisson}(4)$. Then $P(X\ge 1)$ equals

A. $e^{-4}$

B. $1-e^{-4}$

C. $4e^{-4}$

D. $1-4e^{-4}$

---

## Q5 — MCQ

Calls arrive as a Poisson process at a mean rate of $8$ per hour. The probability of exactly $0$ calls in a given $15$-minute period is

A. $e^{-8}$

B. $e^{-2}$

C. $e^{-15}$

D. $1-e^{-2}$

---

## Q6 — NAT

Typos occur as a Poisson process at a mean rate of $3$ per page. Enter the expected number of typos in a $4$-page section.

---

## Q7 — MSQ

$X\sim\mathrm{Poisson}(\lambda)$ and $Y\sim\mathrm{Poisson}(\mu)$ are independent, with $\lambda>0$ and $\mu>0$. Select all that apply.

A. $E[X]=\mathrm{Var}(X)$

B. $X+Y\sim\mathrm{Poisson}(\lambda+\mu)$

C. $X+Y\sim\mathrm{Poisson}(\lambda\mu)$

D. $P(X=0)=e^{-\lambda}$

---

## Level 3 — Multi-Step

## Q8 — MCQ

$X\sim\mathrm{Poisson}(3)$. Then $P(X\le 1)$ equals

A. $4e^{-3}$

B. $3e^{-3}$

C. $e^{-3}$

D. $1-e^{-3}$

---

## Q9 — NAT

Each of $2000$ independent trials has success probability $0.001$. The Poisson approximation uses $\lambda=np$. Enter that value of $\lambda$.

---

## Q10 — MCQ

In one hour, the number of customers at shop A is $\mathrm{Poisson}(2)$ and the number at shop B is $\mathrm{Poisson}(7)$. The two counts are independent. The probability that the two shops together have $0$ customers in that hour is

A. $e^{-9}$

B. $e^{-14}$

C. $e^{-2}+e^{-7}$

D. $e^{-5}$

---

## Level 4 — Tricky / Trap-Based

## Q11 — MCQ

Cracks along a road occur as a Poisson process with mean $0.4$ cracks per metre. The probability of no crack in a given $5$-metre stretch is

A. $e^{-0.4}$

B. $e^{-2}$

C. $e^{-5}$

D. $0.4\,e^{-5}$

---

## Q12 — NAT

$X\sim\mathrm{Poisson}(4)$. Enter the integer $E[(X+1)^2]$.

---

## Level 5 — Challenge

## Q13 — MCQ

$X\sim\mathrm{Poisson}(4)$. Which one of the following is correct?

A. $P(X=3)=P(X=4)$

B. $P(X=4)=P(X=5)$

C. $P(X=1)=P(X=2)$

D. $P(X=0)=P(X=1)$

---

## Q14 — NAT

$X\sim\mathrm{Poisson}(6)$. Enter the integer $E[X(X-1)]$.

## Answer Key

| Q | Type | Answer |
|---|------|--------|
| 1 | MCQ | A |
| 2 | MCQ | B |
| 3 | NAT | 10 |
| 4 | MCQ | B |
| 5 | MCQ | B |
| 6 | NAT | 12 |
| 7 | MSQ | A, B, D |
| 8 | MCQ | A |
| 9 | NAT | 2 |
| 10 | MCQ | A |
| 11 | MCQ | B |
| 12 | NAT | 29 |
| 13 | MCQ | A |
| 14 | NAT | 36 |

## Detailed Solutions

### Q1

Substitute $k=0$:

$$
P(X=0)=e^{-2}\frac{2^0}{0!}=e^{-2}.
$$

Option (B) is $P(X=1)$. Option (D) is $P(X\ge 1)$. Answer: **A**.

### Q2

For a Poisson random variable, the mean and the variance are both the parameter $\lambda$. Option (C) is the exponential mean and variance. Option (D) copies the binomial factor $(1-p)$ onto $\lambda$. Answer: **B**.

### Q3

$$
E[X]+\mathrm{Var}(X)=5+5=10.
$$

Enter $10$.

### Q4

The complement of the empty count is the fast form:

$$
P(X\ge 1)=1-P(X=0)=1-e^{-4}.
$$

Summing $k=1,2,3,\ldots$ is unnecessary. Answer: **B**.

### Q5

Fifteen minutes is $1/4$ hour. The count in that interval is $\mathrm{Poisson}(8\cdot 1/4)=\mathrm{Poisson}(2)$, so

$$
P(X=0)=e^{-2}.
$$

Option (A) uses the hourly mean without scaling by the interval length. Answer: **B**.

### Q6

Four pages scale the per-page mean:

$$
E[\text{typos}]=3\cdot 4=12.
$$

Enter $12$.

### Q7

(A) is the Poisson identity $E[X]=\mathrm{Var}(X)=\lambda$.

(B) is the sum rule for independent Poisson random variables: the parameters add.

(C) is false: the parameters are not multiplied.

(D) is the $k=0$ case of the PMF.

Answer: **A, B, D**.

### Q8

$$
P(X\le 1)=P(X=0)+P(X=1)=e^{-3}+e^{-3}\cdot\frac{3}{1}=e^{-3}(1+3)=4e^{-3}.
$$

Option (B) is only the $k=1$ term. Answer: **A**.

### Q9

The Poisson limit uses the fixed mean of the binomial:

$$
\lambda=np=2000\cdot 0.001=2.
$$

The conditions fit the usual rare-event guideline: $n$ is large, $p$ is small, and $np=2$ is moderate. Enter $2$.

### Q10

The sum of independent Poisson counts is Poisson with the summed means:

$$
A+B\sim\mathrm{Poisson}(2+7)=\mathrm{Poisson}(9),
$$

$$
P(A+B=0)=e^{-9}.
$$

Option (B) multiplies the means. Option (C) adds the two zero-probabilities instead of using the combined parameter. Answer: **A**.

### Q11

The interval is $5$ metres, so the mean count is

$$
\lambda t=0.4\cdot 5=2.
$$

$$
P(\text{no crack})=e^{-2}.
$$

Option (A) forgets to multiply the rate by the length. Answer: **B**.

### Q12

For $\lambda=4$,

$$
E[X^2]=\mathrm{Var}(X)+(E[X])^2=4+16=20.
$$

Expand the square and use linearity:

$$
E[(X+1)^2]=E[X^2+2X+1]=20+2\cdot 4+1=29.
$$

Enter $29$.

### Q13

The successive ratio of the PMF is

$$
\frac{P(X=k)}{P(X=k-1)}=\frac{\lambda}{k}.
$$

With $\lambda=4$,

$$
\frac{P(X=4)}{P(X=3)}=\frac{4}{4}=1,
$$

so $P(X=3)=P(X=4)$. Directly,

$$
P(X=3)=e^{-4}\frac{4^3}{3!}=e^{-4}\frac{64}{6}=e^{-4}\cdot\frac{32}{3},
$$

$$
P(X=4)=e^{-4}\frac{4^4}{4!}=e^{-4}\frac{256}{24}=e^{-4}\cdot\frac{32}{3}.
$$

The other ratios are not $1$:

$$
\frac{P(X=5)}{P(X=4)}=\frac{4}{5},\quad
\frac{P(X=2)}{P(X=1)}=\frac{4}{2}=2,\quad
\frac{P(X=1)}{P(X=0)}=4.
$$

Answer: **A**.

### Q14

Start from the two moments $E[X]=\lambda$ and $E[X^2]=\mathrm{Var}(X)+(E[X])^2=\lambda+\lambda^2$:

$$
E[X(X-1)]=E[X^2]-E[X]=\lambda+\lambda^2-\lambda=\lambda^2.
$$

For $\lambda=6$, this equals $36$. Enter $36$.
