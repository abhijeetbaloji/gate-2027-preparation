# Binomial Distribution — Practice Questions

Original practice for GATE CS. These questions are not from any GATE paper. Attempt the questions before reading the solutions.

Notation: $X\sim\mathrm{Bin}(n,p)$ means $X$ counts successes in $n$ independent trials with success probability $p$ on each trial,

$$
P(X=k)=\binom{n}{k}p^k(1-p)^{n-k},\qquad k=0,1,\ldots,n.
$$

## Level 1 — Conceptual

## Q1 — MCQ

A fair coin is tossed $4$ times, independently. Let $X$ be the number of heads. Then $P(X=1)$ equals

A. $1/16$

B. $1/4$

C. $3/8$

D. $1/2$

---

## Q2 — MCQ

$X\sim\mathrm{Bin}(25,0.2)$. Then $E[X]$ equals

A. $5$

B. $4$

C. $20$

D. $25$

---

## Q3 — NAT

$X\sim\mathrm{Bin}(12,1/3)$. Enter the integer $E[X]$.

---

## Q4 — MCQ

Which one of the following is a binomial experiment?

A. The number of aces in $5$ cards dealt at once from a standard deck.

B. The number of heads in $8$ independent fair coin tosses.

C. The waiting time until the first head in a sequence of coin tosses.

D. The number of emails arriving in an hour, with no fixed number of trials.

---

## Level 2 — Standard GATE Style

## Q5 — MCQ

$X\sim\mathrm{Bin}(3,1/4)$. Then $P(X\ge 1)$ equals

A. $27/64$

B. $37/64$

C. $9/64$

D. $1/4$

---

## Q6 — MCQ

$X\sim\mathrm{Bin}(20,1/5)$. Then $\mathrm{Var}(X)$ equals

A. $4$

B. $16/5$

C. $16$

D. $4/5$

---

## Q7 — NAT

$X\sim\mathrm{Bin}(9,2/3)$. Enter the integer $\mathrm{Var}(X)$.

---

## Q8 — MSQ

Select all settings that are binomial.

A. Fifteen independent sensor readings; each fails with probability $0.02$; count the failures.

B. Four balls drawn at once, without replacement, from an urn with $3$ red balls and $7$ blue balls; count the red balls.

C. Six independent rolls of a fair die; count how many of them show a $6$.

D. The time until a server fails, when the lifetime is exponential.

---

## Level 3 — Multi-Step

## Q9 — MCQ

$X\sim\mathrm{Bin}(7,1/2)$. Which one of the following is correct?

A. $X$ has a unique mode at $3.5$.

B. $P(X=3)=P(X=4)$, and both values are modes.

C. $X$ has a unique mode at $7$.

D. The only mode is $\lfloor np\rfloor=3$.

---

## Q10 — NAT

$X\sim\mathrm{Bin}(5,1/2)$. If $P(X\ge 4)=p/q$ in lowest terms, enter $p+q$.

---

## Q11 — MCQ

Which one of the following is an appropriate Poisson approximation for a rare-event binomial (large $n$, small $p$, and moderate $np$)?

A. $\mathrm{Bin}(12,1/2)\approx\mathrm{Poisson}(6)$

B. $\mathrm{Bin}(400,0.005)\approx\mathrm{Poisson}(2)$

C. $\mathrm{Bin}(30,0.4)\approx\mathrm{Poisson}(12)$

D. $\mathrm{Bin}(8,0.25)\approx\mathrm{Poisson}(2)$

---

## Level 4 — Tricky / Trap-Based

## Q12 — MCQ

$X\sim\mathrm{Bin}(18,1/3)$. Which one of the following is correct?

A. The mean is $6$ and the variance is $6$.

B. The mean is $6$ and the variance is $4$.

C. The mean is $6$ and the variance is $12$.

D. The mean is $18$ and the variance is $4$.

---

## Q13 — NAT

$X\sim\mathrm{Bin}(3,1/6)$. If $P(X=0)=p/q$ in lowest terms, enter $p+q$.

---

## Q14 — MSQ

$X\sim\mathrm{Bin}(n,p)$ with $0<p<1$. Select all that apply.

A. $E[X]=np$

B. $\mathrm{Var}(X)=np(1-p)$

C. $X$ is the sum of $n$ i.i.d. Bernoulli$(p)$ random variables

D. $\mathrm{Var}(X)=np$ for every $p$ in $(0,1)$

---

## Level 5 — Challenge

## Q15 — MCQ

$X\sim\mathrm{Bin}(2,1/3)$ and $Y\sim\mathrm{Bin}(2,1/2)$ are independent. Then $P(X+Y=1)$ equals

A. $1/9$

B. $1/4$

C. $1/3$

D. $5/12$

---

## Q16 — NAT

$X\sim\mathrm{Bin}(5,1/3)$. If $P(X=2)=p/q$ in lowest terms, enter $p+q$.

## Answer Key

| Q | Type | Answer |
|---|------|--------|
| 1 | MCQ | B |
| 2 | MCQ | A |
| 3 | NAT | 4 |
| 4 | MCQ | B |
| 5 | MCQ | B |
| 6 | MCQ | B |
| 7 | NAT | 2 |
| 8 | MSQ | A, C |
| 9 | MCQ | B |
| 10 | NAT | 19 |
| 11 | MCQ | B |
| 12 | MCQ | B |
| 13 | NAT | 341 |
| 14 | MSQ | A, B, C |
| 15 | MCQ | C |
| 16 | NAT | 323 |

## Detailed Solutions

### Q1

Here $n=4$ and $p=1/2$, so

$$
P(X=1)=\binom{4}{1}\left(\frac{1}{2}\right)^4=\frac{4}{16}=\frac{1}{4}.
$$

Answer: **B**.

### Q2

$$
E[X]=np=25\cdot 0.2=5.
$$

Answer: **A**.

### Q3

$$
E[X]=12\cdot\frac{1}{3}=4.
$$

Enter $4$.

### Q4

A binomial experiment needs a fixed number of independent trials and the same success probability on every trial.

(B) has $8$ independent tosses and a constant heads probability.

(A) draws without replacement, so the trials are dependent and the conditional probability of an ace changes. (C) is a waiting time, not a count in a fixed number of trials. (D) has no fixed $n$. Answer: **B**.

### Q5

Use the complement of zero successes:

$$
P(X=0)=\left(\frac{3}{4}\right)^3=\frac{27}{64},
$$

$$
P(X\ge 1)=1-\frac{27}{64}=\frac{37}{64}.
$$

Option (A) is $P(X=0)$, not the event "at least one." Answer: **B**.

### Q6

$$
E[X]=20\cdot\frac{1}{5}=4,
$$

but the variance still carries the failure factor:

$$
\mathrm{Var}(X)=np(1-p)=20\cdot\frac{1}{5}\cdot\frac{4}{5}=\frac{16}{5}.
$$

Option (A) is the mean. Answer: **B**.

### Q7

$$
\mathrm{Var}(X)=9\cdot\frac{2}{3}\cdot\frac{1}{3}=2.
$$

The mean is $np=6$, which is not the variance. Enter $2$.

### Q8

(A) has a fixed number of independent trials with constant failure probability, so the failure count is $\mathrm{Bin}(15,0.02)$.

(C) has six independent rolls and success probability $1/6$ on each roll, so the count is $\mathrm{Bin}(6,1/6)$.

(B) is sampling without replacement, so the success probability is not constant across draws. (D) is an exponential waiting time, not a binomial count.

Answer: **A, C**.

### Q9

The mode location uses $(n+1)p$. Here

$$
(n+1)p=8\cdot\frac{1}{2}=4,
$$

which is an integer. In that boundary case the PMF ties on the two adjacent values $4$ and $4-1=3$. Explicitly,

$$
P(X=3)=\frac{\binom{7}{3}}{2^7}=\frac{35}{128},\qquad P(X=4)=\frac{\binom{7}{4}}{128}=\frac{35}{128},
$$

and both exceed $P(X=2)=\binom{7}{2}/128=21/128$. A mode has to be an attainable value, so $3.5$ is not a mode. Using only $\lfloor np\rfloor=\lfloor 3.5\rfloor=3$ misses the tie at $4$. Answer: **B**.

### Q10

$$
P(X\ge 4)=P(X=4)+P(X=5)=\frac{\binom{5}{4}+\binom{5}{5}}{2^5}=\frac{5+1}{32}=\frac{6}{32}=\frac{3}{16}.
$$

The fraction $3/16$ is in lowest terms, so $p+q=3+16=19$.

### Q11

The rare-event guideline used here is: $n$ at least about $20$, $p$ at most about $0.05$, and $np$ moderate (below about $10$).

For (B), $n=400$, $p=0.005$, and $np=2$. All three parts of the guideline hold, and the approximating Poisson parameter is $np=2$.

(A) has $p=1/2$. (C) has $p=0.4$ and $np=12$. (D) has $n=8<20$ and $p=0.25$. Those three should be left as exact binomials. Answer: **B**.

### Q12

$$
E[X]=18\cdot\frac{1}{3}=6,
$$

$$
\mathrm{Var}(X)=18\cdot\frac{1}{3}\cdot\frac{2}{3}=4.
$$

Option (A) sets the variance equal to the mean, which is the Poisson relation, not the binomial one. Since $1-p=2/3<1$, the binomial variance $np(1-p)$ is strictly smaller than $np$. Answer: **B**.

### Q13

$$
P(X=0)=\left(\frac{5}{6}\right)^3=\frac{125}{216}.
$$

Here $125=5^3$ and $216=2^3\cdot 3^3$, so the fraction is in lowest terms. Thus $p+q=125+216=341$.

### Q14

(A) and (B) are the mean and variance formulas. (C) is the representation of a binomial count as a sum of indicator variables, one per trial.

(D) is false whenever $p\ne 0$: the factor $(1-p)$ is missing, and $\mathrm{Var}(X)=np$ would force $p\in\{0,1\}$.

Answer: **A, B, C**.

### Q15

The success probabilities differ, so $X+Y$ is not a single $\mathrm{Bin}(4,p)$ random variable. Condition on the two ways to get a sum of $1$:

$$
P(X=0)=\left(\frac{2}{3}\right)^2=\frac{4}{9},
$$

$$
P(X=1)=\binom{2}{1}\cdot\frac{1}{3}\cdot\frac{2}{3}=\frac{4}{9},
$$

$$
P(Y=0)=\frac{1}{4},\qquad P(Y=1)=\frac{1}{2}.
$$

Independence gives

$$
\begin{align*}
P(X+Y=1)
&= P(X=0)P(Y=1)+P(X=1)P(Y=0)\\
&= \frac{4}{9}\cdot\frac{1}{2}+\frac{4}{9}\cdot\frac{1}{4}\\
&= \frac{2}{9}+\frac{1}{9}\\
&= \frac{1}{3}.
\end{align*}
$$

The value $1/9$ is $P(X=0)P(Y=0)=P(X+Y=0)$. The value $1/4$ comes from replacing $P(X=1)$ by $P(X=2)$ in the second term. Answer: **C**.

### Q16

$$
P(X=2)=\binom{5}{2}\left(\frac{1}{3}\right)^2\left(\frac{2}{3}\right)^3=10\cdot\frac{1}{9}\cdot\frac{8}{27}=\frac{80}{243}.
$$

Since $80=2^4\cdot 5$ and $243=3^5$, the fraction is in lowest terms. Thus $p+q=80+243=323$.
