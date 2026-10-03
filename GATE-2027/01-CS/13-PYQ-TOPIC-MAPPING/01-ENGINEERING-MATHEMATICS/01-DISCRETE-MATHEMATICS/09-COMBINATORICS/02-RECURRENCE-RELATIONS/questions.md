# GATE PYQs

## 2026

### Q.17

**Paper:** CS-1, forenoon

**Question:**

Consider the following recurrence relations:
For all 𝑛> 1,
𝑛
𝑇_{1}(𝑛) = 4𝑇_{1} (2) + 𝑇_{2}(𝑛)
𝑛
𝑇_{2}(𝑛) = 5𝑇_{2} (4) + Θ(log_{2} 𝑛)
Assume that for all 𝑛≤1, 𝑇_{1}(𝑛) = 1 and 𝑇_{2}(𝑛) = 1.
Which one of the following options is correct?

**Options:**

A. 𝑇_{1}(𝑛) = Θ(𝑛^{2})
B. 𝑇_{1}(𝑛) = Θ(𝑛^{2} log_{2} 𝑛)
C. 𝑇 (𝑛) = Θ(𝑛^{log}4 5) 1
D. 𝑇 (𝑛) = Θ(𝑛^{log}4 5 log 𝑛) 1 2

**Type:** MCQ

**Answer:** VERIFICATION REQUIRED

**Source:** GATE 2026 CS-1 (forenoon), `12-PYQ/2026/set-01/question-paper.pdf`

---

## 2025

### Q.20

**Paper:** CS-1

**Question:**

𝑇(𝑛) = 2𝑇(𝑛−1) + 𝑛2^{𝑛} for 𝑛 > 0, 𝑇(0) = 1.
Which ONE of the following options is CORRECT?

**Options:**

A. 𝑇(𝑛) = Θ(𝑛^{2}2^{𝑛})
B. 𝑇(𝑛) = Θ(𝑛2^{𝑛})
C. 𝑇(𝑛) = Θ((log 𝑛)^{2} 2^{𝑛})
D. 𝑇(𝑛) = Θ(4^{𝑛})

**Type:** MCQ

**Answer:** VERIFICATION REQUIRED

**Source:** GATE 2025 CS-1, `12-PYQ/2025/set-01/question-paper.pdf`

---

## 2024

### Q.42

**Paper:** CS1

**Question:**

Consider the following recurrence relation:
𝑇(𝑛) = {√𝑛𝑇(√𝑛) + 𝑛 for 𝑛≥1,
1 for 𝑛= 1.
Which one of the following options is CORRECT?

**Options:**

A. 𝑇(𝑛) = Θ(𝑛 log log 𝑛)
B. 𝑇(𝑛) = Θ(𝑛 log 𝑛)
C. 𝑇(𝑛) = Θ(𝑛^{2} log 𝑛)
D. 𝑇(𝑛) = Θ(𝑛^{2} log log 𝑛)

**Type:** MCQ

**Answer:** VERIFICATION REQUIRED

**Source:** GATE 2024 CS1, `12-PYQ/2024/set-01/question-paper.pdf`

---

### Q.15

**Paper:** CS2

**Question:**

Let 𝑇(𝑛) be the recurrence relation defined as follows:
𝑇(0) = 1,
𝑇(1) = 2, and
𝑇(𝑛) = 5𝑇(𝑛−1) −6𝑇(𝑛−2) for 𝑛≥2
Which one of the following statements is TRUE?

**Options:**

A. 𝑇(𝑛) = ⁡Θ(2^{𝑛})⁡
B. 𝑇(𝑛) = ⁡Θ(𝑛2^{𝑛})
C. 𝑇(𝑛) = ⁡Θ(3^{𝑛})
D. 𝑇(𝑛) = ⁡Θ(𝑛3^{𝑛})

**Type:** MCQ

**Answer:** VERIFICATION REQUIRED

**Source:** GATE 2024 CS2, `12-PYQ/2024/set-02/question-paper.pdf`

---

## 2023

### Q.14

**Question:**

Consider the Deterministic Finite-state Automaton (DFA) A shown below. The
DFA runs on the alphabet {0, 1}, and has the set of states {s, p, q, r}, with s being
the start state and p being the only final state.
0
1
s^{1} p q
1
0 0
r
0,1
Which one of the following regular expressions correctly describes the language
accepted by A?

**Options:**

A. 1(0^{∗}11)^{∗}
B. 0(0 + 1)^{∗}
C. 1(0 + 11)^{∗}
D. 1(110^{∗})^{∗}

**Type:** MCQ

**Answer:** VERIFICATION REQUIRED

**Source:** GATE 2023 CS, `12-PYQ/2023/question-paper.pdf`

---

## 2022

### Q.51

**Question:**

Consider the following recurrence:
f (1)  1;
f (2 n)  2 f ( n) −1, for n ≥ 1;
f (2n 1)  2 f ( n) 1, for n ≥1.
Then, which of the following statements is/are TRUE?

**Options:**

A. f (2^{n} −1)  2^{n} −1
B. f (2^{n} ) 1
C. f (5 ⋅ 2^{n} )  2^{n}1 1
D. f (2^{n} 1)  2^{n} 1

**Type:** MSQ

**Answer:** VERIFICATION REQUIRED

**Source:** GATE 2022 CS, `12-PYQ/2022/question-paper.pdf`

---

## 2021

### Q.30

**Paper:** CS Set-1

**Question:**

Consider the following recurrence relation.
T(n) = T(n/2) + T(2n/5) + In ifn>0
if n = 0
Which one of the following options is correct?

**Options:**

A. I(n) = e(n5/2)
B. T(n) = e(nlogn)
C. T(п) =0(n)
D. T(n) = e((logn)5/2)| GATE Graduate Aptitude Test in Engineering 2021 2021 Organising Institute - IIT Bombay

**Type:** MCQ

**Answer:** VERIFICATION REQUIRED

**Source:** GATE 2021 CS Set-1, `12-PYQ/2021/set-01/question-paper.pdf`

---

### Q.39

**Paper:** CS Set-2

**Question:**

For constants a ≥ 1 and b > 1, consider the following recurrence defined on the
non-negative integers:
T(n) =a• T (Б) + f(n)
Which one of the following options is correct about the recurrence T(n)?

**Options:**

A. PS →T
B. R→T
C. P→R
D. PS → Q

**Type:** MCQ

**Answer:** VERIFICATION REQUIRED

**Source:** GATE 2021 CS Set-2, `12-PYQ/2021/set-02/question-paper.pdf`

---

## 2020

### Q.2

**Question:**

For parameters a and b, both of which are o(I), T(n)=T(n')+1, and T(b) =1.
Then T(n) is

**Options:**

A. o(loga log, n)
B. O(l0gub n) () O(log, l0g,")
D. O(log, log,n)

**Type:** MCQ

**Answer:** VERIFICATION REQUIRED

**Source:** GATE 2020 CS, `12-PYQ/2020/question-paper.pdf`

---

## 2017

### Q.30

**Paper:** Session 2

**Question:**

Correct : 2 Wrong: -0.66
Consider the recurrence function
T(N) = (2T(VII) + 1, n>2
0<n≤2
Then T(n) in terms of O notation is

**Options:**

A. 0(log logn)
B. ®(logn)
C. 0(Vn)
D. 0(n)

**Type:** MCQ

**Answer:** VERIFICATION REQUIRED

**Source:** GATE 2017 CS Session 2, `12-PYQ/2017/set-02/question-paper.pdf`

---

## 2016

### Q.2

**Paper:** CS-1

**Question:**

Let a_{n} be the number of n-bit strings that do NOT contain two consecutive 1s. Which one of
the following is the recurrence relation for a_{n}?

**Options:**

A. a_{n} = a_{n}−1 + 2a_{n}−2
B. a_{n} = a_{n}−1 + a_{n}−2
C. a_{n} = 2a_{n}−1 + a_{n}−2
D. a_{n} = 2a_{n}−1 + 2a_{n}−2

**Type:** MCQ

**Answer:** VERIFICATION REQUIRED

**Source:** GATE 2016 CS-1, `12-PYQ/2016/set-01/question-paper.pdf`

---

### Q.27

**Paper:** CS-1

**Question:**

Consider the recurrence relation a_{1} = 8, a_{n} = 6n^{2} + 2n + a_{n}−1. Let a_{99} = K × 10^{4}. The value
of K is .

**Options:**

The paper does not print options for this numerical-answer question.

**Type:** NAT

**Answer:** VERIFICATION REQUIRED

**Source:** GATE 2016 CS-1, `12-PYQ/2016/set-01/question-paper.pdf`

---

## 2015

### Q.45

**Paper:** 7 February, Shift 1

**Question:**

Let a„ represent the number of bit strings of length n containing two consecutive 1s. What is the
recurrence relation for a„ ?

**Options:**

A. a,-2 +a,-1+2"-2
B. a„-2+2a„-1+2"-2
C. 2a2 +a„-) +2"-2
D. 2a„-2 +2a,-1 +2"-2

**Type:** MCQ

**Answer:** VERIFICATION REQUIRED

**Source:** GATE 2015 CS, 7 February Shift 1, `12-PYQ/2015/set-01/question-paper.pdf`

---

## 2014

### Q.13

**Paper:** SET-2

**Question:**

Which one of the following correctly determines the solution of the recurrence relation with
T(1) = 1?
T(n) = 2T (#) + logn
ଶ

**Options:**

A. Θ(݊)
B. Θ(݊log݊)
C. Θ(^{ଶ})
D. Θ(log݊)

**Type:** MCQ

**Answer:** VERIFICATION REQUIRED

**Source:** GATE 2014 CS SET-2, `12-PYQ/2014/set-02/question-paper.pdf`

---

## 2008

### Q.78

**Question:**

Which of the following recurrences does x„ satisfy?

**Options:**

A. x„=2X.-) (5)x„=x (w/2]+1
C. x=X\w/2j+n
D. x„=X.-) +X„-2

**Type:** MCQ

**Answer:** VERIFICATION REQUIRED

**Source:** GATE 2008 CS, `12-PYQ/2008/question-paper.pdf`

---

### Q.79

**Question:**

The value of x, is

**Options:**

A. 5
B. 7
C. 8
D. 16 Statement for Linked Answer Questions 80 and 81: The subset-sum problem is defined as follows. Given a set of n positive integers, S ={a,,az,a,.....a„), and a positive integer W, is there a subset of S whose elements sum to W? A dynamic program for solving this problem uses a 2-dimensional Boolean array, X, with n rows and W+1 columns. X[i,j]. I≤i≤n, 0≤ j ≤W, is TRUE if and only if there is a subset of {a,,az,...,a,) whose elements sum to j.

**Type:** MCQ

**Answer:** VERIFICATION REQUIRED

**Source:** GATE 2008 CS, `12-PYQ/2008/question-paper.pdf`

---
