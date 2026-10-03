# GATE PYQs

## 2026

### Q.17

**Paper:** GATE 2026 CS-1 (forenoon)

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

### Q.24

**Paper:** GATE 2026 CS-2 (afternoon)

**Question:**

Consider the following functions, where 𝑛 is a positive integer.
𝑛^{1/3}  ,  log(𝑛) ,  log(𝑛!), 2log(𝑛)
Which one of the following options lists the functions in increasing order of
asymptotic growth rate?
Note: Assume the base of log to be 2.

**Options:**

A. log(𝑛) , 𝑛^{1/3}, 2log(𝑛) , log(𝑛!)
B. 𝑛^{1/3}, log(𝑛) , log(𝑛!) , 2log(𝑛)
C. log(𝑛) , 𝑛^{1/3}, log(𝑛!) , 2log(𝑛)
D. 2log(𝑛) , 𝑛^{1/3}, log(𝑛) , log(𝑛!)

**Type:** MCQ

**Answer:** VERIFICATION REQUIRED

**Source:** GATE 2026 CS-2 (afternoon), `12-PYQ/2026/set-02/question-paper.pdf`

---

### Q.25

**Paper:** GATE 2026 CS-2 (afternoon)

**Question:**

Which of the following can be recurrence relation(s) corresponding to an algorithm
with time complexity Θ(𝑛)?

**Options:**

A. 𝑇(𝑛) = 𝑇(𝑛−1) + 1, 𝑇(1) = 1
B. 𝑛 𝑇(𝑛) = 2𝑇( ) + 1, 𝑇(1) = 1 2
C. 𝑛 𝑇(𝑛) = 2𝑇( ) + 𝑛, 𝑇(1) = 1 2
D. 𝑇(𝑛) = 𝑇(𝑛−1) + 𝑛, 𝑇(1) = 1

**Type:** MCQ

**Answer:** VERIFICATION REQUIRED

**Source:** GATE 2026 CS-2 (afternoon), `12-PYQ/2026/set-02/question-paper.pdf`

---

## 2025

### Q.20

**Paper:** GATE 2025 CS-1

**Question:**

𝑇(𝑛) = 2𝑇(𝑛−1) + 𝑛2^{𝑛} for 𝑛 > 0,  𝑇(0) = 1.
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

**Paper:** GATE 2024 CS1

**Question:**

Consider the following recurrence relation:
𝑇(𝑛) = {√𝑛𝑇(√𝑛) + 𝑛  for  𝑛≥1,
1  for  𝑛= 1.
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

**Paper:** GATE 2024 CS2

**Question:**

Let 𝑇(𝑛) be the recurrence relation defined as follows:
𝑇(0) = 1,
𝑇(1) = 2, and
𝑇(𝑛) = 5𝑇(𝑛−1) −6𝑇(𝑛−2)  for 𝑛≥2
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

### Q.29

**Paper:** GATE 2023 CS

**Question:**

Let f and g be functions of natural numbers given by f (n) = n and g(n) = n^{2}.
Which of the following statements is/are TRUE?

**Options:**

A. f ∈ O(g)
B. f ∈ Ω(g)
C. f ∈ o(g)
D. f ∈ Θ(g)

**Type:** MCQ

**Answer:** VERIFICATION REQUIRED

**Source:** GATE 2023 CS, `12-PYQ/2023/question-paper.pdf`

---

### Q.54

**Paper:** GATE 2023 CS

**Question:**

Consider functions Function 1 and Function 2 expressed in pseudocode as
follows:
Function 1  Function 2
while n > 1 do  for i = 1 to 100 ∗ n do
for i = 1 to n do  x = x + 1;
x = x + 1;  end for
end for
n = ⌊n/2⌋;
end while
Let f_{1}(n) and f_{2}(n) denote the number of times the statement “x = x + 1” is
executed in Function 1 and Function 2, respectively.
Which of the following statements is/are TRUE?

**Options:**

A. f_{1}(n) ∈ Θ(f_{2}(n))
B. f_{1}(n) ∈ o(f_{2}(n))
C. f_{1}(n) ∈ ω(f_{2}(n))
D. f_{1}(n) ∈ O(n)

**Type:** MCQ

**Answer:** VERIFICATION REQUIRED

**Source:** GATE 2023 CS, `12-PYQ/2023/question-paper.pdf`

---

## 2021

### Q.3

**Paper:** GATE 2021 CS Set-1

**Question:**

Consider the following three functions.
f1 = 10" f2 =nogr f3=nv
Which one of the following options arranges the functions in the increasing order
of asymptotic growth rate?

**Options:**

A. f3,f2, f1
B. f2. f1, f3
C. fi,f2, f3
D. f2.f3. f1

**Type:** MCQ

**Answer:** VERIFICATION REQUIRED

**Source:** GATE 2021 CS Set-1, `12-PYQ/2021/set-01/question-paper.pdf`

---

### Q.5

**Paper:** GATE 2021 CS Set-1

**Question:**

Consider the following statements.
S1 : Every SLR(1) grammar is unambiguous but there are certain
unambiguous grammars that are not SLR(1).
S2: For any context-free grammar, there is a parser that takes at
most O(n) time to parse a string of length n.
Which one of the following options is correct?

**Options:**

A. | Si is true and S2 is false
B. | S, is false and Sz is true
C. | Si is true and Sa is true
D. Sy is false and Sz is false

**Type:** MCQ

**Answer:** VERIFICATION REQUIRED

**Source:** GATE 2021 CS Set-1, `12-PYQ/2021/set-01/question-paper.pdf`

---

## 2014

### Q.11

**Paper:** GATE 2014 CS SET-1

**Question:**

Let G be a graph with n vertices and m edges. What is the tightest upper bound on the running time
of Deepth First Seaarch on ܩ, whhen ܩ is repreesented as an adjacency maatrix?

**Options:**

A. 0(n)
B. 0(n+m)
C. O(n2)
D. ®(m2)

**Type:** MCQ

**Answer:** VERIFICATION REQUIRED

**Source:** GATE 2014 CS SET-1, `12-PYQ/2014/set-01/question-paper.pdf`

---

### Q.13

**Paper:** GATE 2014 CS SET-2

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

### Q.38

**Paper:** GATE 2014 CS SET-2

**Question:**

Suppose P, Q, R, S, T are sorted sequences having lengths 20, 24, 30, 35, 50 respectively.  They are
to be merged into a single sequence by merging together two sequences at a time.  The number of
comparisons that will be needed in the worst case by the optimal algorithm for doing this is ____.

**Options:**

The paper does not print options for this numerical-answer question.

**Type:** NAT

**Answer:** VERIFICATION REQUIRED

**Source:** GATE 2014 CS SET-2, `12-PYQ/2014/set-02/question-paper.pdf`

---

## 2013

### Q.6

**Paper:** GATE 2013 CS Booklet A

**Question:**

Which one of the following is the tightest upper bound that represents the number of swaps
required to sort n numbers using selection sort?

**Options:**

A. O(log n)
B. O(n)
C. O(n log n)
D. O(n^{2})

**Type:** MCQ

**Answer:** VERIFICATION REQUIRED

**Source:** GATE 2013 CS Booklet A, `12-PYQ/2013/set-01/question-paper.pdf`

---

### Q.31

**Paper:** GATE 2013 CS Booklet A

**Question:**

Consider the following function:
int unknown(int n){
int i, j, k=0;
for (i=n/2; i<=n; i++)
for (j=2; j<=n; j=j*2)
k = k + n/2;
return (k);
}
The return value of the function is

**Options:**

A. Θ(n^{2})
B. Θ(n^{2}log n)
C. Θ(n^{3})
D. Θ(n^{3}logn)

**Type:** MCQ

**Answer:** VERIFICATION REQUIRED

**Source:** GATE 2013 CS Booklet A, `12-PYQ/2013/set-01/question-paper.pdf`

---

### Q.20

**Paper:** GATE 2013 CS Booklet B

**Question:**

Which one of the following is the tightest upper bound that represents the number of swaps
required to sort n numbers using selection sort?

**Options:**

A. O(log n)
B. O(n)
C. O(n log n)
D. O(n^{2})

**Type:** MCQ

**Answer:** VERIFICATION REQUIRED

**Source:** GATE 2013 CS Booklet B, `12-PYQ/2013/set-02/question-paper.pdf`

---

### Q.42

**Paper:** GATE 2013 CS Booklet B

**Question:**

Consider the following function:
int unknown(int n){
int i, j, k=0;
for (i=n/2; i<=n; i++)
for (j=2; j<=n; j=j*2)
k = k + n/2;
return (k);
}
The return value of the function is

**Options:**

A. Θ(n^{2})
B. Θ(n^{2}log n)
C. Θ(n^{3})
D. Θ(n^{3}logn) CS-B 9/20 2013COMPUTER SCIENCE & INFORMATION TECH. - CS

**Type:** MCQ

**Answer:** VERIFICATION REQUIRED

**Source:** GATE 2013 CS Booklet B, `12-PYQ/2013/set-02/question-paper.pdf`

---

### Q.7

**Paper:** GATE 2013 CS Booklet C

**Question:**

Which one of the following is the tightest upper bound that represents the number of swaps
required to sort n numbers using selection sort?

**Options:**

A. O(log n)
B. O(n)
C. O(n log n)
D. O(n^{2}) CS- C 2/20 2013COMPUTER SCIENCE & INFORMATION TECH. - CS

**Type:** MCQ

**Answer:** VERIFICATION REQUIRED

**Source:** GATE 2013 CS Booklet C, `12-PYQ/2013/set-03/question-paper.pdf`

---

### Q.31

**Paper:** GATE 2013 CS Booklet C

**Question:**

Consider the following function:
int unknown(int n){
int i, j, k=0;
for (i=n/2; i<=n; i++)
for (j=2; j<=n; j=j*2)
k = k + n/2;
return (k);
}
The return value of the function is

**Options:**

A. Θ(n^{2})
B. Θ(n^{2}log n)
C. Θ(n^{3})
D. Θ(n^{3}logn)

**Type:** MCQ

**Answer:** VERIFICATION REQUIRED

**Source:** GATE 2013 CS Booklet C, `12-PYQ/2013/set-03/question-paper.pdf`

---

### Q.19

**Paper:** GATE 2013 CS Booklet D

**Question:**

Which one of the following is the tightest upper bound that represents the number of swaps
required to sort n numbers using selection sort?

**Options:**

A. O(log n)
B. O(n)
C. O(n log n)
D. O(n^{2})

**Type:** MCQ

**Answer:** VERIFICATION REQUIRED

**Source:** GATE 2013 CS Booklet D, `12-PYQ/2013/set-04/question-paper.pdf`

---

### Q.42

**Paper:** GATE 2013 CS Booklet D

**Question:**

Consider the following function:
int unknown(int n){
int i, j, k=0;
for (i=n/2; i<=n; i++)
for (j=2; j<=n; j=j*2)
k = k + n/2;
return (k);
}
The return value of the function is

**Options:**

A. Θ(n^{2})
B. Θ(n^{2}log n)
C. Θ(n^{3})
D. Θ(n^{3}logn)

**Type:** MCQ

**Answer:** VERIFICATION REQUIRED

**Source:** GATE 2013 CS Booklet D, `12-PYQ/2013/set-04/question-paper.pdf`

---

## 2012

### Q.18

**Paper:** GATE 2012 CS Booklet A

**Question:**

Let W(n) and A(n) denote respectively, the worst case and average case running time of an
algorithm executed on an input of size n.  Which of the following is ALWAYS TRUE?

**Options:**

A. A(n) = Ω (W(n))
B. A(n) = Θ (W(n))
C. A(n) = O (W(n))
D. A(n) = o (W(n))

**Type:** MCQ

**Answer:** VERIFICATION REQUIRED

**Source:** GATE 2012 CS Booklet A, `12-PYQ/2012/question-paper.pdf`

---

### Q.39

**Paper:** GATE 2012 CS Booklet A

**Question:**

A list of  n strings, each of length  n, is sorted into lexicographic order using the merge-sort
algorithm. The worst case running time of this computation is

**Options:**

A. O (n log n)
B. O (n^{2} log n)
C. O (n^{2} + log n)
D. O (n^{2})

**Type:** MCQ

**Answer:** VERIFICATION REQUIRED

**Source:** GATE 2012 CS Booklet A, `12-PYQ/2012/question-paper.pdf`

---

## 2011

### Q.37

**Paper:** GATE 2011 CS Booklet A

**Question:**

Which of the given options provides the increasing order of asymptotic complexity of functions
fi.f2.fs and fa?
f(n)=2' f2(n) =n312 J3(n) = n logzn f.(n) =n°"

**Options:**

A. 248000
B. 44000
C. 19000
D. 25000

**Type:** MCQ

**Answer:** VERIFICATION REQUIRED

**Source:** GATE 2011 CS Booklet A, `12-PYQ/2011/question-paper.pdf`

---

## 2009

### Q.11

**Paper:** GATE 2009 CS

**Question:**

What is the number of swaps required to sort n elements using selection sort, in the worst case ?

**Options:**

A. O(n)
B. O(n log n)
C. 0(n)
D. O(n? log n)

**Type:** MCQ

**Answer:** VERIFICATION REQUIRED

**Source:** GATE 2009 CS, `12-PYQ/2009/question-paper.pdf`

---

### Q.35

**Paper:** GATE 2009 CS

**Question:**

The running time of an algorithm is represented by the following recurrence relation :
n≤3
T(п) = T 72 +cn otherwise
3
Which one of the following represents the time complexity of the algorithm?

**Options:**

A. O(n)
B. O(n log n)
C. 0(n?)
D. O(n? log n)

**Type:** MCQ

**Answer:** VERIFICATION REQUIRED

**Source:** GATE 2009 CS, `12-PYQ/2009/question-paper.pdf`

---

## 2008

### Q.7

**Paper:** GATE 2008 CS

**Question:**

The most efficient algorithm for finding the number of connected components in an undirected
graph on n vertices and m edges has time complexity

**Options:**

A. О(n)
B. (m)
C. ©(m+ n)
D. ®(mn) 2008 MAIN PAPER - CS

**Type:** MCQ

**Answer:** VERIFICATION REQUIRED

**Source:** GATE 2008 CS, `12-PYQ/2008/question-paper.pdf`

---

### Q.39

**Paper:** GATE 2008 CS

**Question:**

Consider the following functions:
f(n)=2"
g(n)= n!
h(n)= n°gn
Which of the following statements about the asymptotic behaviour of f (n),g(n), and h(n) is
true?

**Options:**

A. f (n) =0(g(n)); g(n) = 0(h(n))
B. f (n) =2(g(n)); g(n) = O(h(n))
C. g(n) = O(f(n)); h(n) = O(f(n))
D. h(n) = O(f (n)); g(n) = 2(f (n))

**Type:** MCQ

**Answer:** VERIFICATION REQUIRED

**Source:** GATE 2008 CS, `12-PYQ/2008/question-paper.pdf`

---

### Q.44

**Paper:** GATE 2008 CS

**Question:**

The subset-sum problem is defined as follows: Given a set S of n positive integers and a positive
integer W, determine whether there is a subset of S whose elements sum to W.
An algorithm Q solves this problem in O(nW) time. Which of the following statements is false?

**Options:**

A. Q solves the subset-sum problem in polynomial time when the input is encoded in unary
B. Q solves the subset-sum problem in polynomial time when the input is encoded in binary
C. The subset sum problem belongs to the class NP
D. The subset sum problem is NP-hard

**Type:** MCQ

**Answer:** VERIFICATION REQUIRED

**Source:** GATE 2008 CS, `12-PYQ/2008/question-paper.pdf`

---

### Q.74

**Paper:** GATE 2008 CS

**Question:**

The running time of f1 (n) and f2 (n) are

**Options:**

A. O(n) and O(n)
B. ©(2") and (n)
C. ©(n) and O(2")
D. ©(2") and O(2")

**Type:** MCQ

**Answer:** VERIFICATION REQUIRED

**Source:** GATE 2008 CS, `12-PYQ/2008/question-paper.pdf`

---
