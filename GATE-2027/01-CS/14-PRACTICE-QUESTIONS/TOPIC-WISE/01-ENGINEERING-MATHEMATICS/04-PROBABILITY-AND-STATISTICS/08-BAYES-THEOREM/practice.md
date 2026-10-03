# Bayes' Theorem — Practice Questions

Original practice for GATE CS. These questions are not from any GATE paper. Attempt the questions before reading the solutions.

## Level 1 — Conceptual

## Q1 — MCQ

In the identity \(P(H\mid D)=P(D\mid H)\,P(H)/P(D)\), the factor \(P(H)\) is the

A. prior

B. likelihood

C. posterior

D. marginal probability of the evidence

---

## Q2 — MCQ

In Bayes' theorem, \(P(D\mid H)\) is the

A. prior of \(H\)

B. likelihood of \(H\) for evidence \(D\)

C. posterior of \(H\) given \(D\)

D. marginal probability of \(H\)

---

## Q3 — NAT

Suppose \(P(H)=\dfrac{1}{4}\), \(P(D\mid H)=\dfrac{2}{5}\), and \(P(D)=\dfrac{1}{2}\). Write \(P(H\mid D)=\dfrac{p}{q}\) in lowest terms. Enter \(p+q\).

---

## Level 2 — Standard GATE Style

## Q4 — MCQ

A condition has prior probability \(\dfrac{1}{4}\). A test detects the condition with probability \(\dfrac{4}{5}\) when it is present, and gives a positive result with probability \(\dfrac{1}{5}\) when it is absent. The probability that the condition is present, given a positive test, equals

A. \(\dfrac{4}{7}\)

B. \(\dfrac{4}{5}\)

C. \(\dfrac{1}{4}\)

D. \(\dfrac{7}{20}\)

---

## Q5 — NAT

Plant F1 makes \(\dfrac{3}{4}\) of the items and has defect probability \(\dfrac{1}{10}\). Plant F2 makes the rest and has defect probability \(\dfrac{1}{5}\). An item is defective. Enter \(100\) times the probability that it came from F1.

---

## Q6 — MCQ

A message is spam with prior probability \(\dfrac{1}{5}\). A keyword appears with probability \(\dfrac{3}{4}\) in spam and with probability \(\dfrac{1}{4}\) in non-spam. Given that the keyword appears, the probability that the message is spam equals

A. \(\dfrac{3}{7}\)

B. \(\dfrac{3}{4}\)

C. \(\dfrac{1}{5}\)

D. \(\dfrac{7}{20}\)

---

## Q7 — MSQ

Select all that apply.

A. The prior is the probability of a hypothesis before the evidence is observed.

B. The likelihood of a hypothesis is the probability of the evidence given that hypothesis.

C. For a partition into hypotheses, the posterior probabilities given the same evidence sum to \(1\).

D. If a test has sensitivity \(0.99\), then the probability of the condition given a positive test is \(0.99\).

---

## Level 3 — Multi-Step

## Q8 — NAT

Three suppliers produce \(\dfrac{1}{2}\), \(\dfrac{3}{10}\), and \(\dfrac{1}{5}\) of the stock. Their defect probabilities are \(\dfrac{1}{50}\), \(\dfrac{1}{25}\), and \(\dfrac{1}{20}\), respectively. A purchased item is defective. Write the probability that it came from the second supplier as \(\dfrac{p}{q}\) in lowest terms. Enter \(p+q\).

---

## Q9 — MCQ

In a group of \(100\) people, \(5\) have a condition. A test is positive for \(80\%\) of the people who have the condition and for \(20\%\) of the people who do not. Given that a person's test is positive, the probability that the person has the condition is

A. \(\dfrac{4}{23}\)

B. \(\dfrac{4}{5}\)

C. \(\dfrac{1}{20}\)

D. \(\dfrac{19}{23}\)

---

## Q10 — MCQ

Machines M1, M2, and M3 produce \(40\%\), \(35\%\), and \(25\%\) of the output. Their defect rates are \(1\%\), \(2\%\), and \(4\%\). Given that an item is defective, the probability that it came from M3 is

A. \(\dfrac{10}{21}\)

B. \(\dfrac{1}{25}\)

C. \(\dfrac{1}{4}\)

D. \(\dfrac{21}{1000}\)

---

## Level 4 — Tricky / Trap-Based

## Q11 — MCQ

A condition occurs in \(\dfrac{1}{200}\) of a population. A test always detects a person who has the condition, and its false-positive rate is \(\dfrac{1}{100}\). The probability that a person who tests positive has the condition is

A. \(\dfrac{100}{299}\)

B. \(1\)

C. \(\dfrac{199}{200}\)

D. \(\dfrac{1}{200}\)

---

## Q12 — NAT

A fire occurs with probability \(\dfrac{1}{50}\). An alarm sounds with probability \(\dfrac{9}{10}\) when there is a fire and with probability \(\dfrac{1}{20}\) when there is no fire. Write the probability that there is a fire, given that the alarm sounds, as \(\dfrac{p}{q}\) in lowest terms. Enter \(p+q\).

---

## Level 5 — Challenge

## Q13 — NAT

Hypotheses \(A\), \(B\), and \(C\) have priors \(\dfrac{1}{2}\), \(\dfrac{1}{3}\), and \(\dfrac{1}{6}\). A flag is raised with probabilities \(\dfrac{1}{4}\), \(\dfrac{1}{2}\), and \(1\) under those three hypotheses. Write the probability of \(C\) given that the flag is raised as \(\dfrac{p}{q}\) in lowest terms. Enter \(p+q\).

---

## Q14 — MCQ

The prior odds of \(H\) against \(H^c\) are \(1:4\). Evidence \(D\) has likelihood ratio

\[
\frac{P(D\mid H)}{P(D\mid H^c)}=\frac{3}{1},
\]

with \(P(D\mid H)=\dfrac{3}{4}\) and \(P(D\mid H^c)=\dfrac{1}{4}\). Then \(P(H\mid D)\) equals

A. \(\dfrac{3}{7}\)

B. \(\dfrac{3}{4}\)

C. \(\dfrac{1}{5}\)

D. \(\dfrac{3}{5}\)

## Answer Key

| Q | Type | Answer |
|---|------|--------|
| 1 | MCQ | A |
| 2 | MCQ | B |
| 3 | NAT | 6 |
| 4 | MCQ | A |
| 5 | NAT | 60 |
| 6 | MCQ | A |
| 7 | MSQ | A, B, C |
| 8 | NAT | 11 |
| 9 | MCQ | A |
| 10 | MCQ | A |
| 11 | MCQ | A |
| 12 | NAT | 85 |
| 13 | NAT | 15 |
| 14 | MCQ | A |

## Detailed Solutions

### Q1

Bayes' theorem multiplies the likelihood \(P(D\mid H)\) by the prior \(P(H)\), then divides by the marginal probability of the evidence. The factor \(P(H)\) is the belief in \(H\) before \(D\) is observed, so it is the prior.

Option (B) is \(P(D\mid H)\). Option (C) is the whole left-hand side \(P(H\mid D)\). Option (D) is the denominator \(P(D)\). Answer: **A**.

### Q2

The likelihood is the probability of the observed evidence when the hypothesis is assumed true. That is \(P(D\mid H)\), not \(P(H\mid D)\).

Option (A) is \(P(H)\). Option (C) is \(P(H\mid D)\), the updated probability after seeing \(D\). Option (D) is again a probability of \(H\), not of the evidence. Answer: **B**.

### Q3

\[
P(H\mid D)=\frac{P(D\mid H)\,P(H)}{P(D)}=\frac{(2/5)(1/4)}{1/2}=\frac{1/10}{1/2}=\frac{1}{5}.
\]

Thus \(p+q=1+5=6\). The given marginal \(P(D)=1/2\) is consistent, because it forces \(P(D\mid H^c)=8/15\), which lies between \(0\) and \(1\). The likelihood \(2/5\) gives \(2+5=7\). The prior \(1/4\) gives \(1+4=5\). The joint probability \(1/10\) gives \(1+10=11\). None of those is the posterior. Answer: **6**.

### Q4

Let \(H\) be the event that the condition is present and \(D\) a positive test.

\[
P(D)=\frac{4}{5}\cdot\frac{1}{4}+\frac{1}{5}\cdot\frac{3}{4}=\frac{4}{20}+\frac{3}{20}=\frac{7}{20}.
\]

\[
P(H\mid D)=\frac{4/20}{7/20}=\frac{4}{7}.
\]

Option (B) is the sensitivity \(P(D\mid H)\). Option (C) is the prior. Option (D) is \(P(D)\), the marginal probability of a positive test. Most positive tests in this mixture do not come from the smaller group that has the condition, so the posterior \(4/7\) is below the sensitivity \(4/5\). Answer: **A**.

### Q5

\[
P(\text{defect})=\frac{3}{4}\cdot\frac{1}{10}+\frac{1}{4}\cdot\frac{1}{5}=\frac{3}{40}+\frac{2}{40}=\frac{5}{40}=\frac{1}{8}.
\]

The joint probability of F1 and a defect is \(3/40\), so

\[
P(\text{F1}\mid\text{defect})=\frac{3/40}{1/8}=\frac{3}{5}.
\]

Then \(100\cdot(3/5)=60\). The complementary posterior for F2 is \(2/5\), and \(100\) times that value is \(40\). One hundred times F1's defect rate is \(10\), and one hundred times F1's production share is \(75\). Those are a likelihood and a prior, not the posterior. Answer: **60**.

### Q6

Let \(S\) be spam and \(W\) the appearance of the keyword.

\[
P(W)=\frac{1}{5}\cdot\frac{3}{4}+\frac{4}{5}\cdot\frac{1}{4}=\frac{3}{20}+\frac{1}{5}=\frac{3}{20}+\frac{4}{20}=\frac{7}{20}.
\]

\[
P(S\mid W)=\frac{3/20}{7/20}=\frac{3}{7}.
\]

Option (B) is the likelihood \(P(W\mid S)\). Option (C) is the prior. Option (D) is \(P(W)\). The posterior equals the likelihood only in special cases; here the marginal probability of the keyword is \(7/20\), not \(1/5\), so the posterior \(3/7\) is not the likelihood \(3/4\). Answer: **A**.

### Q7

(A) and (B) are the definitions of prior and likelihood.

(C) is true. If the hypotheses partition the sample space, exactly one of them occurs. Conditioning on the same evidence of positive probability preserves that partition, so the posteriors sum to \(1\).

(D) is false. Sensitivity is \(P(\text{positive}\mid\text{condition})\). The posterior \(P(\text{condition}\mid\text{positive})\) also depends on the prior and on the false-positive rate. A rare condition can have a small posterior even when the sensitivity is \(0.99\).

(E) is true because \(H\) and \(H^c\) still partition the outcomes inside the evidence \(D\).

Answer: **A, B, C**.

### Q8

The three joint probabilities of supplier and defect are

\[
\frac{1}{2}\cdot\frac{1}{50}=\frac{1}{100},\qquad
\frac{3}{10}\cdot\frac{1}{25}=\frac{3}{250},\qquad
\frac{1}{5}\cdot\frac{1}{20}=\frac{1}{100}.
\]

Their sum is

\[
\frac{1}{100}+\frac{3}{250}+\frac{1}{100}=\frac{1}{50}+\frac{3}{250}=\frac{5}{250}+\frac{3}{250}=\frac{8}{250}=\frac{4}{125}.
\]

The second supplier contributes \(3/250\), so its posterior is

\[
\frac{3/250}{4/125}=\frac{3}{250}\cdot\frac{125}{4}=\frac{3}{8}.
\]

Thus \(p+q=3+8=11\). The first and third suppliers each have joint probability \(1/100\), so each has posterior \(5/16\), and \(5+16=21\). That answer uses the wrong supplier. Answer: **11**.

### Q9

There are \(4\) true positives, because \(80\%\) of \(5\) is \(4\). There are \(19\) false positives, because \(20\%\) of the other \(95\) people is \(19\). A positive test therefore occurs for \(23\) people, of whom \(4\) have the condition:

\[
P(\text{condition}\mid\text{positive})=\frac{4}{23}.
\]

Option (B) is the sensitivity \(4/5\). Option (C) is the prior \(5/100\). Option (D) is the proportion of positive tests that are false positives. The low prior makes false positives outnumber true positives, so the posterior is \(4/23\), far below the sensitivity. Answer: **A**.

### Q10

The contributions to the defect probability are

\[
0.40\cdot 0.01=0.004,\qquad 0.35\cdot 0.02=0.007,\qquad 0.25\cdot 0.04=0.010.
\]

The total is \(0.021=21/1000\). M3 contributes \(0.010=10/1000\), so

\[
P(\text{M3}\mid\text{defect})=\frac{10/1000}{21/1000}=\frac{10}{21}.
\]

Option (B) is M3's defect rate, \(4\%=1/25\). Option (C) is M3's share of production, \(25\%=1/4\). Option (D) is the marginal defect probability \(21/1000\). The posterior divides M3's joint contribution by the sum of all three contributions. Answer: **A**.

### Q11

Let \(H\) be the condition and \(D\) a positive test. Then \(P(D\mid H)=1\) and \(P(D\mid H^c)=1/100\).

\[
P(D)=\frac{1}{200}\cdot 1+\frac{199}{200}\cdot\frac{1}{100}
=\frac{100}{20000}+\frac{199}{20000}
=\frac{299}{20000}.
\]

\[
P(H\mid D)=\frac{1/200}{299/20000}=\frac{100}{299}.
\]

Option (B) is the sensitivity. A perfect detection rate does not make a positive test certain to mean the condition, because the false-positive branch still produces \(199\) expected positives per \(20000\) people, against \(100\) true positives. Option (C) is \(1\) minus the prior. Option (D) is the prior itself. Ignoring the base rate is what turns the answer into \(1\). Answer: **A**.

### Q12

\[
P(\text{alarm})=\frac{9}{10}\cdot\frac{1}{50}+\frac{1}{20}\cdot\frac{49}{50}
=\frac{9}{500}+\frac{49}{1000}
=\frac{18}{1000}+\frac{49}{1000}
=\frac{67}{1000}.
\]

The joint probability of fire and alarm is \(9/500=18/1000\), so

\[
P(\text{fire}\mid\text{alarm})=\frac{18/1000}{67/1000}=\frac{18}{67}.
\]

Since \(67\) is prime and does not divide \(18\), the fraction is in lowest terms, and \(p+q=18+67=85\). The likelihood \(9/10\) gives \(9+10=19\). The prior \(1/50\) gives \(1+50=51\). The marginal \(67/1000\) gives \(67+1000=1067\). The posterior is smaller than the likelihood because fires are rare relative to false alarms. Answer: **85**.

### Q13

The joint probabilities of a flag with each hypothesis are

\[
\frac{1}{4}\cdot\frac{1}{2}=\frac{1}{8},\qquad
\frac{1}{2}\cdot\frac{1}{3}=\frac{1}{6},\qquad
1\cdot\frac{1}{6}=\frac{1}{6}.
\]

The marginal probability of the flag is

\[
\frac{1}{8}+\frac{1}{6}+\frac{1}{6}=\frac{1}{8}+\frac{1}{3}=\frac{3}{24}+\frac{8}{24}=\frac{11}{24}.
\]

Hence

\[
P(C\mid\text{flag})=\frac{1/6}{11/24}=\frac{1}{6}\cdot\frac{24}{11}=\frac{4}{11},
\]

and \(p+q=4+11=15\). The posterior of \(A\) is \((1/8)/(11/24)=3/11\), so \(3+11=14\). The posterior of \(B\) is also \(4/11\). The three posteriors \(3/11\), \(4/11\), and \(4/11\) sum to \(1\), which checks the denominator. Using only the prior of \(C\) gives \(1+6=7\). Answer: **15**.

### Q14

Prior odds \(1:4\) mean \(P(H)=1/5\) and \(P(H^c)=4/5\). Posterior odds equal prior odds times the likelihood ratio:

\[
\frac{P(H\mid D)}{P(H^c\mid D)}=\frac{1}{4}\cdot\frac{3}{1}=\frac{3}{4}.
\]

If \(p=P(H\mid D)\), then \(p/(1-p)=3/4\), so \(4p=3-3p\) and \(p=3/7\).

The direct computation agrees:

\[
P(D)=\frac{3}{4}\cdot\frac{1}{5}+\frac{1}{4}\cdot\frac{4}{5}=\frac{3}{20}+\frac{4}{20}=\frac{7}{20},
\]

\[
P(H\mid D)=\frac{3/20}{7/20}=\frac{3}{7}.
\]

Option (B) is the likelihood \(P(D\mid H)\), and it is also the numerical value of the posterior odds. Odds of \(3/4\) are not a probability of \(3/4\). Option (C) is the prior. Option (D) adds the prior to the likelihood ratio without normalizing. Answer: **A**.
