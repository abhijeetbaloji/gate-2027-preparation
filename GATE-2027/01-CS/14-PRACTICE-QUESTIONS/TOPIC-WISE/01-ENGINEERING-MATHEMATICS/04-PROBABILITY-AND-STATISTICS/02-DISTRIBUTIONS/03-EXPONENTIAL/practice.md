# Exponential Distribution — Practice Questions

Original practice for GATE CS. These questions are not from any GATE paper. Attempt the questions before reading the solutions.

Notation: $X\sim\mathrm{Exp}(\lambda)$ means $X$ has rate $\lambda>0$, PDF $f(x)=\lambda e^{-\lambda x}$ for $x\ge 0$, mean $1/\lambda$, and variance $1/\lambda^2$.

## Level 1 — Conceptual

## Q1 — MCQ

$X\sim\mathrm{Exp}(\lambda)$ with rate $\lambda=4$. Which one of the following is correct?

A. $E[X]=4$ and $\mathrm{Var}(X)=16$

B. $E[X]=1/4$ and $\mathrm{Var}(X)=1/16$

C. $E[X]=1/4$ and $\mathrm{Var}(X)=1/4$

D. $E[X]=4$ and $\mathrm{Var}(X)=4$

---

## Q2 — MCQ

$X\sim\mathrm{Exp}(1)$. Then $P(X>3)$ equals

A. $1-e^{-3}$

B. $e^{-3}$

C. $3e^{-3}$

D. $e^{-1}$

---

## Q3 — NAT

Jobs arrive at a constant rate of $3$ per hour. The waiting time until the next job is exponential with that rate. Enter the mean waiting time in minutes.

---

## Level 2 — Standard GATE Style

## Q4 — MCQ

The lifetime $X$, in hours, satisfies $X\sim\mathrm{Exp}(2)$. A device has already run for $5$ hours. The probability that it runs at least $3$ more hours is

A. $e^{-6}$

B. $e^{-10}$

C. $e^{-16}$

D. $1-e^{-6}$

---

## Q5 — MCQ

$X\sim\mathrm{Exp}(\lambda)$ with rate $\lambda=1/5$. Then $P(X\le 10)$ equals

A. $e^{-2}$

B. $1-e^{-2}$

C. $1-e^{-10}$

D. $1-e^{-1/2}$

---

## Q6 — NAT

An exponential random variable has mean $6$. Enter the integer equal to its variance.

---

## Level 3 — Multi-Step

## Q7 — MCQ

Packets arrive in a Poisson process at rate $5$ per minute. The probability that no packet arrives in the next $12$ seconds is

A. $e^{-1}$

B. $e^{-5}$

C. $e^{-12}$

D. $1-e^{-1}$

---

## Q8 — NAT

$X\sim\mathrm{Exp}(2)$ and $Y\sim\mathrm{Exp}(5)$ are independent. Let $M=\min(X,Y)$. If $E[M]=p/q$ in lowest terms, enter $p+q$.

---

## Level 4 — Tricky / Trap-Based

## Q9 — MSQ

Select all that apply.

A. The exponential distribution on $[0,\infty)$ is memoryless.

B. The continuous uniform distribution on $[0,10]$ is memoryless.

C. If an exponential random variable has mean $\beta$, then its rate is $1/\beta$.

D. If the PDF is $\lambda e^{-\lambda x}$ for $x\ge 0$, then the variance is $1/\lambda^2$.

---

## Q10 — NAT

The lifetime of a device, in hours, is exponential with mean $8$. The device has already survived $3$ hours. Enter the conditional expected remaining lifetime, in hours.

---

## Level 5 — Challenge

## Q11 — MCQ

Three components have independent lifetimes, each distributed as $\mathrm{Exp}(2)$. The system fails when the first component fails. If $T$ is the time to system failure, then

A. $T\sim\mathrm{Exp}(2)$ and $E[T]=1/2$

B. $T\sim\mathrm{Exp}(6)$ and $E[T]=1/6$

C. $T\sim\mathrm{Exp}(8)$ and $E[T]=1/8$

D. $T\sim\mathrm{Exp}(6)$ and $E[T]=6$

---

## Q12 — NAT

Three independent exponential random variables have means $3$, $4$, and $6$. Let $M$ be their minimum. If $E[M]=p/q$ in lowest terms, enter $p+q$.

## Answer Key

| Q | Type | Answer |
|---|------|--------|
| 1 | MCQ | B |
| 2 | MCQ | B |
| 3 | NAT | 20 |
| 4 | MCQ | A |
| 5 | MCQ | B |
| 6 | NAT | 36 |
| 7 | MCQ | A |
| 8 | NAT | 8 |
| 9 | MSQ | A, C, D |
| 10 | NAT | 8 |
| 11 | MCQ | B |
| 12 | NAT | 7 |

## Detailed Solutions

### Q1

With rate $\lambda$, the mean is $1/\lambda$ and the variance is $1/\lambda^2$:

$$
E[X]=\frac{1}{4},\qquad \mathrm{Var}(X)=\frac{1}{16}.
$$

Treating $\lambda$ as the mean gives the other options. In particular, the variance equals the square of the mean, not the mean itself. Answer: **B**.

### Q2

The survival function is $P(X>t)=e^{-\lambda t}$. Here $\lambda=1$, so

$$
P(X>3)=e^{-3}.
$$

Option (A) is the CDF $P(X\le 3)$. Answer: **B**.

### Q3

The rate is $3$ jobs per hour, so the mean wait is $1/3$ hour. In minutes,

$$
\frac{1}{3}\cdot 60=20.
$$

Enter $20$.

### Q4

Memorylessness says that the remaining lifetime is a fresh $\mathrm{Exp}(2)$ random variable:

$$
P(X>5+3\mid X>5)=P(X>3)=e^{-2\cdot 3}=e^{-6}.
$$

Option (C) uses the total time in the exponent, $e^{-\lambda(5+3)}=e^{-16}$, which is the unconditional probability $P(X>8)$, not the conditional one. Option (D) is a CDF value. Answer: **A**.

### Q5

The rate is $1/5$, so $\lambda\cdot 10=2$. The CDF is

$$
P(X\le 10)=1-e^{-\lambda\cdot 10}=1-e^{-2}.
$$

Option (C) treats the time $10$ as if the rate were $1$. Option (D) uses the mean $5$ in place of the rate inside a mismatched exponent. Answer: **B**.

### Q6

If the mean is $\beta=6$, then $\lambda=1/6$ and

$$
\mathrm{Var}(X)=\frac{1}{\lambda^2}=\beta^2=36.
$$

Entering $6$ would confuse variance with the mean. Enter $36$.

### Q7

Convert $12$ seconds to $12/60=1/5$ minute. In a Poisson process of rate $5$ per minute, the count in $1/5$ minute is $\mathrm{Poisson}(1)$, so

$$
P(0\text{ packets})=e^{-1}.
$$

Equivalently, the waiting time is $\mathrm{Exp}(5)$ and

$$
P(X>1/5)=e^{-5\cdot(1/5)}=e^{-1}.
$$

Option (B) forgets the time conversion and uses one full minute. Answer: **A**.

### Q8

The minimum of independent exponential random variables is exponential with rate equal to the sum of the rates. Thus $M\sim\mathrm{Exp}(2+5)=\mathrm{Exp}(7)$, and

$$
E[M]=\frac{1}{7}.
$$

Hence $p+q=1+7=8$.

The same conclusion follows from the survival function:

$$
P(M>t)=P(X>t)P(Y>t)=e^{-2t}e^{-5t}=e^{-7t}.
$$

### Q9

(A) is the memoryless property, and it is the continuous memoryless law on $[0,\infty)$ in this syllabus.

(B) is false. On a bounded interval the remaining time cannot have the same distribution as the original waiting time: after waiting $9$ units on $[0,10]$, at most $1$ unit remains.

(C) and (D) are the rate-mean conversion and the variance formula.

Answer: **A, C, D**.

### Q10

Memorylessness says the remaining lifetime has the same distribution as the original lifetime, so its expectation is still the original mean, $8$ hours. Subtracting the time already survived would give $5$, which is not the conditional expectation for an exponential lifetime. Enter $8$.

### Q11

Independent exponential rates add for the first event. Three copies of rate $2$ give

$$
T\sim\mathrm{Exp}(2+2+2)=\mathrm{Exp}(6),\qquad E[T]=\frac{1}{6}.
$$

Option (A) keeps a single component's rate. Option (D) uses the combined rate as if it were the mean. Answer: **B**.

### Q12

Convert means to rates and add them:

$$
\lambda_1=\frac{1}{3},\quad \lambda_2=\frac{1}{4},\quad \lambda_3=\frac{1}{6}.
$$

$$
\lambda_1+\lambda_2+\lambda_3=\frac{4}{12}+\frac{3}{12}+\frac{2}{12}=\frac{9}{12}=\frac{3}{4}.
$$

The minimum is $\mathrm{Exp}(3/4)$, so

$$
E[M]=\frac{1}{3/4}=\frac{4}{3}.
$$

Thus $p+q=4+3=7$. The three means are different, so this is not "the smallest mean" and not the average of the three means.
