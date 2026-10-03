# GATE PYQs

## 2026

### Q.28

**Paper:** GATE 2026 CS-1 (forenoon)

**Question:**

Which of the following statements is/are true?

**Options:**

A. LL(1) parser uses backtracking
B. For a grammar to be LL(1), it must be left-recursive
C. For a grammar to be LL(1), it must be left-factored
D. The LL(1) parsers are more powerful than the SLR parsers

**Type:** MCQ

**Answer:** VERIFICATION REQUIRED

**Source:** GATE 2026 CS-1 (forenoon), `12-PYQ/2026/set-01/question-paper.pdf`

---

### Q.61

**Paper:** GATE 2026 CS-1 (forenoon)

**Question:**

Consider the recursive functions represented by the following code segment:
int bar(int n){
if (n == 1) return 0;
else return 1 + bar(n/2);
}
int foo(int n){
if (n == 1) return 1;
else return 1 + foo(bar(n));
}
The smallest positive integer n for which foo(n) returns 5 is ______. (answer in
integer)
Note: Ignore syntax errors (if any) in the function.

**Options:**

The paper does not print options for this numerical-answer question.

**Type:** NAT

**Answer:** VERIFICATION REQUIRED

**Source:** GATE 2026 CS-1 (forenoon), `12-PYQ/2026/set-01/question-paper.pdf`

---

### Q.39

**Paper:** GATE 2026 CS-2 (afternoon)

**Question:**

Consider a table 𝑇, where the elements 𝑇[𝑖][𝑗], 0 ≤𝑖, 𝑗≤𝑛, represent the cost of
the optimal solutions of different subproblems of a problem that is being solved
using a dynamic programming algorithm. The recursive formulation to compute the
table entries is as follows:
𝑇[0][𝑘] = 𝑇[𝑘][0] = 1  for  𝑘= 0,1,2, … , 𝑛
𝑇[𝑖][𝑗] = 2𝑇[𝑖−1][𝑗] + 3𝑇[𝑖][𝑗−1]  for  1 ≤𝑖, 𝑗≤𝑛
Consider the following two algorithms to compute entries of  𝑇.  Assume that for
both the algorithms, for all 0 ≤𝑖, 𝑗≤𝑛, 𝑇[𝑖][𝑗] has been initialized to 1.
Algorithm 𝐵_{1}:  For 𝑖= 1, 2, … , 𝑛
For 𝑗= 1, 2, … , 𝑛
𝑇[𝑖][𝑗] = 2𝑇[𝑖−1][𝑗] + 3𝑇[𝑖][𝑗−1]
Algorithm 𝐵_{2}:  For 𝑠= 2, 3, … , 2𝑛
For 𝑖= 1, 2, … , 𝑛
For 𝑗= 1, 2, … , 𝑛
If (𝑖+ 𝑗== 𝑠)
𝑇[𝑖][𝑗] = 2𝑇[𝑖−1][𝑗] + 3𝑇[𝑖][𝑗−1]
Algorithm 𝐵_{𝑘}, 𝑘∈{1,2} is said to be correct if and only if it calculates the correct
values of 𝑇[𝑖][𝑗], for all 0 ≤𝑖, 𝑗≤𝑛, (as per the recursive formulation) at the end
of the execution of the algorithm 𝐵_{𝑘}.
Which one of the following statements is true?

**Options:**

A. Both algorithms 𝐵_{1} and 𝐵_{2} are correct
B. Algorithm 𝐵_{1} is correct, but algorithm 𝐵_{2} is incorrect
C. Algorithm 𝐵_{2} is correct, but algorithm 𝐵_{1} is incorrect
D. Both algorithms 𝐵_{1} and 𝐵_{2} are incorrect

**Type:** MCQ

**Answer:** VERIFICATION REQUIRED

**Source:** GATE 2026 CS-2 (afternoon), `12-PYQ/2026/set-02/question-paper.pdf`

---

## 2025

### Q.30

**Paper:** GATE 2025 CS-2

**Question:**

Consider the two lists List I and List II given below:
List I  List II
(i) Context free languages  (a) Closed under union
(ii) Recursive languages  (b) Not closed under complementation
(iii) Regular languages  (c) Closed under intersection
For matching of items in List I with those in List II, which of the following
option(s) is/are CORRECT?

**Options:**

A. (i) – (a), (ii) – (b), and (iii) – (c)
B. (i) – (b), (ii) – (a), and (iii) – (c)
C. (i) – (b), (ii) – (c), and (iii) – (a)
D. (i) – (a), (ii) – (c), and (iii) – (b)

**Type:** MCQ

**Answer:** VERIFICATION REQUIRED

**Source:** GATE 2025 CS-2, `12-PYQ/2025/set-02/question-paper.pdf`

---

## 2023

### Q.24

**Paper:** GATE 2023 CS

**Question:**

Which of the following statements is/are CORRECT?

**Options:**

A. The intersection of two regular languages is regular.
B. The intersection of two context-free languages is context-free.
C. The intersection of two recursive languages is recursive.
D. The intersection of two recursively enumerable languages is recursively enumerable.

**Type:** MCQ

**Answer:** VERIFICATION REQUIRED

**Source:** GATE 2023 CS, `12-PYQ/2023/question-paper.pdf`

---

## 2022

### Q.23

**Paper:** GATE 2022 CS

**Question:**

Which of the following statements is/are TRUE?

**Options:**

A. Every subset of a recursively enumerable language is recursive.
B. If a language L and its complement L are both recursively enumerable, then L must be recursive.
C. Complement of a context-free language must be recursive.
D. If L_{1} and L_{2} are regular, then L_{1} ∩ L_{2} must be deterministic context-free.

**Type:** MCQ

**Answer:** VERIFICATION REQUIRED

**Source:** GATE 2022 CS, `12-PYQ/2022/question-paper.pdf`

---

## 2021

### Q.12

**Paper:** GATE 2021 CS Set-1

**Question:**

Let (M) denote an encoding of an automaton M. Suppose that E = {0,1}. Which
of the following languages is/are NOT recursive?

**Options:**

A. L = {(M)| M is a DFA such that L(M) = Ø}
B. L = {(M)| M is a DFA such that L(M) = 2*}
C. L = {(M)| M is a PDA such that L(M) = Ø}
D. I = {(M)| M is a PDA such that L(M) = 2*} GATE Graduate Aptitude Test in Engineering 2021 2021 Organising Institute - IIT Bombay

**Type:** MCQ

**Answer:** VERIFICATION REQUIRED

**Source:** GATE 2021 CS Set-1, `12-PYQ/2021/set-01/question-paper.pdf`

---

## 2020

### Q.9

**Paper:** GATE 2020 CS

**Question:**

Consider the following statements.
I. Symbol table is accessed only during lexical analysis and syntax analysis.
II. Compilers for programming languages that support recursion necessarily
need heap storage for memory allocation in the run-time environment.
III. Errors violating the condition 'any variable must be declared before its
use' are detected during syntax analysis.
Which of the above statements is/are TRUE?

**Options:**

A. Ionly
B. I and IIl only
C. Il only
D. None of I, Il, and III

**Type:** MCQ

**Answer:** VERIFICATION REQUIRED

**Source:** GATE 2020 CS, `12-PYQ/2020/question-paper.pdf`

---

### Q.26

**Paper:** GATE 2020 CS

**Question:**

Which of the following languages are undecidable? Note that (M) indicates
encoding of the Turing machine M.
41 = [(M)|L(M) = Ø}
Lz = {(M,w, q)| M on input w reaches state q in exactly 100 steps)
Lz = {(M)| L(M) is not recursive)
L4 = {(M)| L(M) contains at least 21 members}

**Options:**

A. Ly, Lz, and L4 only
B. Ly and Lz only
C. Lz and Lz only
D. L2, Lz, and Ly only

**Type:** MCQ

**Answer:** VERIFICATION REQUIRED

**Source:** GATE 2020 CS, `12-PYQ/2020/question-paper.pdf`

---

## 2018

### Q.7

**Paper:** GATE 2018 CS

**Question:**

The set of all recursively enumerable languages is

**Options:**

A. closed under complementation.
B. closed under intersection.
C. a subset of the set of all recursive languages.
D. an uncountable set.

**Type:** MCQ

**Answer:** VERIFICATION REQUIRED

**Source:** GATE 2018 CS, `12-PYQ/2018/question-paper.pdf`

---

## 2017

### Q.32

**Paper:** GATE 2017 CS Session 2

**Question:**

Correct : 2 Wrong : 0.66
Consider the following expression grammar G :
E->E-TT
T->T+EF
F -> (E)1 id
Which of the following grammars is not left recursive, but is equivalent to G?

**Options:**

A. E -> E - TIT
B. E -> TE' T->T+FIF E' →> -TE' | € F -> (E) l id T->T+FIF F -> (E) l id
C. E -> TX
D. E -> TX | (TX) X -> -TX |€ X -> -TX | +TX |є T -> FY T -> id Y -> +FY |€ F -> (E) lid

**Type:** MCQ

**Answer:** VERIFICATION REQUIRED

**Source:** GATE 2017 CS Session 2, `12-PYQ/2017/set-02/question-paper.pdf`

---

### Q.40

**Paper:** GATE 2017 CS Session 2

**Question:**

Correct : 2 Wrong : -0.66
Consider the following languages.
L1 = {a" |p is a prime number}
Lz ={a"bm(2m |n ≥ 0,m ≥ 0}
Lz= {a"b"(2n |n=0}
L4 = {a"b"|n ≥ 1}
Which of the following are CORRECT?
I. Ly is context-free but not regular.
II. Lz is not context-free.
III. Lz is not context-free but recursive.
IV. L4 is deterministic context-free.

**Options:**

A. I, II and IV only
B. II and III only
C. I and IV only
D. III and IV only

**Type:** MCQ

**Answer:** VERIFICATION REQUIRED

**Source:** GATE 2017 CS Session 2, `12-PYQ/2017/set-02/question-paper.pdf`

---

## 2016

### Q.44

**Paper:** GATE 2016 CS-1

**Question:**

Let X be a recursive language and Y be a recursively enumerable but not recursive language.
Let W and Z be two languages such that Y reduces to W , and Z reduces to X (reduction means
the standard many-one reduction). Which one of the following statements is TRUE?

**Options:**

A. W can be recursively enumerable and Z is recursive.
B. W can be recursive and Z is recursively enumerable.
C. W is not recursively enumerable and Z is recursive.
D. W is not recursively enumerable and Z is not recursive.

**Type:** MCQ

**Answer:** VERIFICATION REQUIRED

**Source:** GATE 2016 CS-1, `12-PYQ/2016/set-01/question-paper.pdf`

---

### Q.18

**Paper:** GATE 2016 CS-2

**Question:**

Consider the following types of languages: L_{1} : Regular, L_{2} : Context-free, L_{3} : Recursive,
L_{4} : Recursively enumerable. Which of the following is/are TRUE?
I. L_{3} ∪ L_{4} is recursively enumerable
II. L_{2} ∪ L_{3} is recursive
III. L_{1}∗ ∩ L_{2} is context-free
IV. L_{1} ∪ L_{2} is context-free

**Options:**

A. I only
B. I and III only
C. I and IV only
D. I, II and III only

**Type:** MCQ

**Answer:** VERIFICATION REQUIRED

**Source:** GATE 2016 CS-2, `12-PYQ/2016/set-02/question-paper.pdf`

---

### Q.39

**Paper:** GATE 2016 CS-2

**Question:**

The given diagram shows the flowchart for a recursive function A(n). Assume that all
statements, except for the recursive calls, have O(1) time complexity. If the worst case time
complexity of this function is O(n^{α} ), then the least possible value (accurate up to two decimal
positions) of α is  .
Flowchart for Recursive Function A(n)
Start
A(n/2)
Return  A(n/2)  A(n/2)  A(n/2)  Return
A(n/2)
Return  A(n/2)  Return

**Options:**

The paper does not print options for this numerical-answer question.

**Type:** NAT

**Answer:** VERIFICATION REQUIRED

**Source:** GATE 2016 CS-2, `12-PYQ/2016/set-02/question-paper.pdf`

---

### Q.44

**Paper:** GATE 2016 CS-2

**Question:**

Consider the following languages.
L_{1} = {⟨M⟩| M takes at least 2016 steps on some input},
L_{2} = {⟨M⟩| M takes at least 2016 steps on all inputs} and
L_{3} = {⟨M⟩| M accepts ε},
where for each Turing machine M, ⟨M⟩ denotes a specific encoding of M. Which one of the
following is TRUE?

**Options:**

A. L_{1} is recursive and L_{2}, L_{3} are not recursive
B. L_{2} is recursive and L_{1}, L_{3} are not recursive
C. L_{1}, L_{2} are recursive and L_{3} is not recursive
D. L_{1}, L_{2}, L_{3} are recursive

**Type:** MCQ

**Answer:** VERIFICATION REQUIRED

**Source:** GATE 2016 CS-2, `12-PYQ/2016/set-02/question-paper.pdf`

---

### Q.45

**Paper:** GATE 2016 CS-2

**Question:**

Which one of the following grammars is free from left recursion?

**Options:**

A. S → AB A → Aa | b B → c
B. S → Ab | Bb | c A → Bd | ε B → e
C. S → Aa | B A → Bb | Sc | ε B → d
D. S → Aa | Bb | c A → Bd | ε B → Ae | ε CS(Set B) 13/18

**Type:** MCQ

**Answer:** VERIFICATION REQUIRED

**Source:** GATE 2016 CS-2, `12-PYQ/2016/set-02/question-paper.pdf`

---

## 2015

### Q.28

**Paper:** GATE 2015 CS, 7 February Shift 1

**Question:**

For any two languages L1 and L2 such that Ly is context-free and L2 is recursively enumerable but
not recursive, which of the following is/are necessarily true?
I. L, (complement of Li) is recursive
II. L2 (complement of Lz) is recursive
II. I, is context-free
IV. L, U Lz is recursively enumerable

**Options:**

A. I only (В) III only
C. III and TV only
D. Iand IV only 2 $ B 3.% C 4.VD

**Type:** MCQ

**Answer:** VERIFICATION REQUIRED

**Source:** GATE 2015 CS, 7 February Shift 1, `12-PYQ/2015/set-01/question-paper.pdf`

---

### Q.38

**Paper:** GATE 2015 CS, 8 February Shift 1

**Question:**

Consider the following recursive C function.
void get (int n)
if (n<l) return;
get (n-1) ;
get (n-3) ;
printf("%d" ,n);
If get (6) function is being called in main () then how many times will the get () function be
invoked before returning to the main ()?
(А) 15 (B) 25 (C) 35 (D) 45

**Options:**

The options could not be read from the local paper. The PDF listed in Source is the authoritative copy.

**Type:** MCQ

**Answer:** VERIFICATION REQUIRED

**Source:** GATE 2015 CS, 8 February Shift 1, `12-PYQ/2015/set-03/question-paper.pdf`

---

## 2014

### Q.35

**Paper:** GATE 2014 CS SET-1

**Question:**

Let L be a language and L be its complement. Which one of the following is NOT a viable
possibility?

**Options:**

A. I and II only
B. 1 and IIl only
C. II and IIl only
D. Both L and L are recursive.

**Type:** MCQ

**Answer:** VERIFICATION REQUIRED

**Source:** GATE 2014 CS SET-1, `12-PYQ/2014/set-01/question-paper.pdf`

---

### Q.16

**Paper:** GATE 2014 CS SET-2

**Question:**

Let  ܣ ≤_{௠} ܤ denotes that language A is mapping reducible (also known as many-to-one reducible)
to language B. Which one of the following is FALSE?

**Options:**

A. If ܣ ≤_{௠} ܤ and B is recursive then A is recursive.
B. If ܣ ≤_{௠} ܤ and A is undecidable then B is undecidable.
C. If ܣ ≤_{௠} ܤ and B is recursively enumerable then A is recursively enumerable.
D. If ܣ ≤_{௠} ܤ and B is not recursively enumerable then A is not recursively enumerable.

**Type:** MCQ

**Answer:** VERIFICATION REQUIRED

**Source:** GATE 2014 CS SET-2, `12-PYQ/2014/set-02/question-paper.pdf`

---

### Q.35

**Paper:** GATE 2014 CS SET-2

**Question:**

Let  < ܯ> be the encoding of a Turing machine as a string over  ߑ= {0, 1}. Let
L = { < M > | M is a Turing machine that accepts a string of length 2014 }. Then, L is

**Options:**

A. decidable and recursively enumerable
B. undecidable but recursively enumerable
C. undecidable and not recursively enumerable
D. decidable but not recursively enumerable CS02 (GATE 2014)

**Type:** MCQ

**Answer:** VERIFICATION REQUIRED

**Source:** GATE 2014 CS SET-2, `12-PYQ/2014/set-02/question-paper.pdf`

---

### Q.13

**Paper:** GATE 2014 CS SET-3

**Question:**

Suppose depth first search is executed on the graph below starting at some unknown vertex.
Assume that a recursive call to visit a vertex is made only after first checking that the vertex
has not been visited earlier.  Then the maximum possible recursion depth (including the
initial call)  is  _________.
CS03 (GATE 2014)

**Options:**

The paper does not print options for this numerical-answer question.

**Type:** NAT

**Answer:** VERIFICATION REQUIRED

**Source:** GATE 2014 CS SET-3, `12-PYQ/2014/set-03/question-paper.pdf`

---

## 2013

### Q.32

**Paper:** GATE 2013 CS Booklet A

**Question:**

Consider the following languages.
L_{1} = {_{0}^{p} 1^{q} 0^{r} | p, q, r ≥ 0}
L_{2} ={_{0}^{p} 1^{q} 0^{r} | p, q, r ≥ ,0 p ≠ r }
Which one of the following statements is FALSE?

**Options:**

A. L_{2} is context-free.
B. L_{1}∩ L_{2}is context-free.
C. Complement of L_{2} is recursive.
D. Complement of L_{1} is context-free but not regular.

**Type:** MCQ

**Answer:** VERIFICATION REQUIRED

**Source:** GATE 2013 CS Booklet A, `12-PYQ/2013/set-01/question-paper.pdf`

---

### Q.41

**Paper:** GATE 2013 CS Booklet B

**Question:**

Consider the following languages.
L_{1} ={_{0}^{p} 1^{q} 0^{r} | p, q, r ≥ 0}
L_{2} ={_{0}^{p} 1^{q} 0^{r} | p, q, r ≥ ,0 p ≠ r }
Which one of the following statements is FALSE?

**Options:**

A. L_{2} is context-free.
B. L_{1}∩ L_{2}is context-free.
C. Complement of L_{2} is recursive.
D. Complement of L_{1} is context-free but not regular.

**Type:** MCQ

**Answer:** VERIFICATION REQUIRED

**Source:** GATE 2013 CS Booklet B, `12-PYQ/2013/set-02/question-paper.pdf`

---

### Q.30

**Paper:** GATE 2013 CS Booklet C

**Question:**

Consider the following languages.
L_{1} ={_{0}^{p} 1^{q} 0^{r} | p, q, r ≥ 0}
L_{2} ={_{0}^{p} 1^{q} 0^{r} | p, q, r ≥ ,0 p ≠ r }
Which one of the following statements is FALSE?

**Options:**

A. L_{2} is context-free.
B. L_{1}∩ L_{2}is context-free.
C. Complement of L_{2} is recursive.
D. Complement of L_{1} is context-free but not regular.

**Type:** MCQ

**Answer:** VERIFICATION REQUIRED

**Source:** GATE 2013 CS Booklet C, `12-PYQ/2013/set-03/question-paper.pdf`

---

### Q.43

**Paper:** GATE 2013 CS Booklet D

**Question:**

Consider the following languages.
L_{1} = {_{0}^{p} 1^{q} 0^{r} | p, q, r ≥ 0}
L_{2} ={_{0}^{p} 1^{q} 0^{r} | p, q, r ≥ ,0 p ≠ r }
Which one of the following statements is FALSE?

**Options:**

A. L_{2} is context-free.
B. L_{1}∩ L_{2}is context-free.
C. Complement of L_{2} is recursive.
D. Complement of L_{1} is context-free but not regular. CS- D 9/20 2013COMPUTER SCIENCE & INFORMATION TECH. - CS

**Type:** MCQ

**Answer:** VERIFICATION REQUIRED

**Source:** GATE 2013 CS Booklet D, `12-PYQ/2013/set-04/question-paper.pdf`

---

## 2012

### Q.24

**Paper:** GATE 2012 CS Booklet A

**Question:**

Which of the following problems are decidable?
1)  Does a given program ever produce an output?
2)  If L is a context-free language, then, is  L  also context-free?
3)  If L is a regular language, then, is  L  also regular?
4)  If L is a recursive language, then, is  L  also recursive?

**Options:**

A. 1, 2, 3, 4
B. 1, 2
C. 2, 3, 4
D. 3, 4

**Type:** MCQ

**Answer:** VERIFICATION REQUIRED

**Source:** GATE 2012 CS Booklet A, `12-PYQ/2012/question-paper.pdf`

---

## 2011

### Q.47

**Paper:** GATE 2011 CS Booklet A

**Question:**

The following is the comment written for a C function.
/* This function computes the roots of a quadratic equation
a.x^2 + b.x + c = 0. The function stores two real roots
in *root1 and *root2 and returns the status of validity
of roots. It handles four different kinds of cases.
(i) When coefficient a is zero irrespective of discriminant
(ii) When discriminant is positive
(iii) When discriminant is zero
(iv) When discriminant is negative.
Only in case (ii) and (iii), the stored roots are valid.
Otherwise 0 is stored in the roots. The function returns
0 when the roots are valid and -1 otherwise.
The function also ensures root1 ›= root2.
int get_luadRoots (float a, float b, float c,
float *rootl, float *root2);
A software test engineer is assigned the job of doing black box testing. He comes up with the
following test cases, many of which are redundant.
Test Input Set Expected Output Set
Case b root1 | root2 | Return Value
TI 0.0 0.0
T2 0.0 1.0 0.0 -1
T3 1.0 2.0 -1.0
T4 4.0 -12.0 1.5
TS 1.0 -2.0 -1.0
T6 1.0 1.0 0.0 -1
Which one of the following options provide the set of non-redundant tests using equivalence class
partitioning approach from input perspective for black box testing?

**Options:**

A. T1, T2, Т3, Т6
B. T1, T3, T4, T5
C. T2, T4, T5, T6
D. T2, T3, T4, T5 CS-A 13/20 2011 CS Common Data Questions Common Data for Questions 48 and 49: Consider the following recursive C function that takes two arguments. unsigned int foo (unsigned int n, unsigned int r) { if (n>0) return ((n8r) +foo(n/I, I)); else return 0; }

**Type:** MCQ

**Answer:** VERIFICATION REQUIRED

**Source:** GATE 2011 CS Booklet A, `12-PYQ/2011/question-paper.pdf`

---

## 2010

### Q.17

**Paper:** GATE 2010 CS

**Question:**

LerLil be arecursive language. Let LZand 1.3 languages that are recursively enumerable but nor
recursive. Which of the following statomenes is not necessarily rue?

**Options:**

A. L2 - L1 is recursively enumerable.
B. L1 - L.3 is recursively enumerable.
C. L2 M L3 is recursively enumnerable. {D) L2 UL3 is recursively enumerable.

**Type:** MCQ

**Answer:** VERIFICATION REQUIRED

**Source:** GATE 2010 CS, `12-PYQ/2010/question-paper.pdf`

---

## 2009

### Q.16

**Paper:** GATE 2009 CS

**Question:**

Which one of the following is FALSE?

**Options:**

A. There is a unique minimal DFA for every regular language.
B. Every NFA can be converted to an equivalent PDA.
C. Complement of every context-free language is recursive.
D. Every nondeterministic PDA can be converted to an equivalent deterministic PDA.

**Type:** MCQ

**Answer:** VERIFICATION REQUIRED

**Source:** GATE 2009 CS, `12-PYQ/2009/question-paper.pdf`

---

### Q.40

**Paper:** GATE 2009 CS

**Question:**

Let L =L, N Lz, where L, and L2 are languages as defined below :
LI = (a"'b"c a"b" |m, n≥0}
L2 = (abc*|i,j, k≥ 0}
Then L is

**Options:**

A. not recursive.
B. regular.
C. context-free but not regular.
D. recursively enumerable but not context-free.

**Type:** MCQ

**Answer:** VERIFICATION REQUIRED

**Source:** GATE 2009 CS, `12-PYQ/2009/question-paper.pdf`

---

### Q.42

**Paper:** GATE 2009 CS

**Question:**

Which of the following statements are TRUE?
I. There exist parsing algorithms for some programming languages whose complexities are
less than O(n').
II. A programming language which allows recursion can be implemented with static storage
allocation.
III. No L-attributed definition can be evaluated in the framework of bottom-up parsing.
IV. Code improving transformations can be performed at both source language and
intermediate code level.

**Options:**

A. I and II
B. I and IV
C. III and IV
D. I, III and IV

**Type:** MCQ

**Answer:** VERIFICATION REQUIRED

**Source:** GATE 2009 CS, `12-PYQ/2009/question-paper.pdf`

---

### Q.53

**Paper:** GATE 2009 CS

**Question:**

We wish to find the length of the longest common sub-sequence (LCS) of X[m] and Y[n] as
/(m, n), where an incomplete recursive definition for the function ((i,j) to compute the length of
the LCS of X[m] and Y[n] is given below :
((i,j) = 0 • if either 1=0 or j=0
= expr1 , if i,j>0 and X[i-1]=y[J-1]
= expI2 • if 1,j›0 and X[i-1]*Y[j-1]
Which one of the following options is correct?

**Options:**

A. expr1 =((i-1,J)+1
B. expr1 =((i,j-1)
C. expr2 = max(|(i-1,j), ((i,j-1))
D. expr2 = mаx(|(i-1,j-1), ((i,J))

**Type:** MCQ

**Answer:** VERIFICATION REQUIRED

**Source:** GATE 2009 CS, `12-PYQ/2009/question-paper.pdf`

---

## 2008

### Q.13

**Paper:** GATE 2008 CS

**Question:**

If Land Lare recursively enumerable then L is

**Options:**

A. regular
B. context-free
C. context-sensitive
D. recursive 3/24 2008 MAIN PAPER - CS

**Type:** MCQ

**Answer:** VERIFICATION REQUIRED

**Source:** GATE 2008 CS, `12-PYQ/2008/question-paper.pdf`

---

### Q.48

**Paper:** GATE 2008 CS

**Question:**

Which of the following statements is false?

**Options:**

A. Every NFA can be converted to an equivalent DFA
B. Every non-deterministic Turing machine can be converted to an equivalent deterministic Turing machine
C. Every regular language is also a context-free language
D. Every subset of a recursively enumerable set is recursive

**Type:** MCQ

**Answer:** VERIFICATION REQUIRED

**Source:** GATE 2008 CS, `12-PYQ/2008/question-paper.pdf`

---

## 2007

### Q.18

**Paper:** GATE 2007 CS

**Question:**

Which one of the following is a top-down parser?

**Options:**

A. Recursive descent parser.
B. Operator precedence parser.
C. An LR(k) parser.
D. An LALR(k) parser.

**Type:** MCQ

**Answer:** VERIFICATION REQUIRED

**Source:** GATE 2007 CS, `12-PYQ/2007/question-paper.pdf`

---

### Q.30

**Paper:** GATE 2007 CS

**Question:**

The language L = { 0'21' | i≥ 0} over the alphabet (0, 1, 2) is

**Options:**

A. not recursive.
B. is recursive and is a deterministic CFL.
C. is a regular language.
D. is not a deterministic CFL but a CFL.

**Type:** MCQ

**Answer:** VERIFICATION REQUIRED

**Source:** GATE 2007 CS, `12-PYQ/2007/question-paper.pdf`

---

### Q.44

**Paper:** GATE 2007 CS

**Question:**

In the following C function, let n≥ m.
int gcd (n,m)
if (n8m == 0) return m;
n = nsm;
return gcd(m,n) ;
How many recursive calls are made by this function?

**Options:**

A. O(logzn)
B. 2(n)
C. ®(1og,l0g,n)
D. ©(Vn)

**Type:** MCQ

**Answer:** VERIFICATION REQUIRED

**Source:** GATE 2007 CS, `12-PYQ/2007/question-paper.pdf`

---

### Q.45

**Paper:** GATE 2007 CS

**Question:**

What is the time complexity of the following recursive function:
int DoSomething (int n) (
if (n <= 2)
return 1;
else return (DoSomething (floor(sgrt (n))) + n) ;

**Options:**

A. O(n°)
B. O(nlog,n)
C. O(log,n)
D. ®(log, log, n) CS - 10/24

**Type:** MCQ

**Answer:** VERIFICATION REQUIRED

**Source:** GATE 2007 CS, `12-PYQ/2007/question-paper.pdf`

---

### Q.51

**Paper:** GATE 2007 CS

**Question:**

Consider the following C code segment:
int IsPrime(n)
int i,n;
for (i=2;i <= sqrt (n);1++)
if (n%i == 0) {printf ("Not Prime\n"); return 0;)
return 1;
}
Let T(n) denote the number of times the for loop is executed by the program on
input n. Which of the following is TRUE?

**Options:**

A. it is left recursive.
B. it is right recursive.
C. it is ambiguous.
D. it is not context-free. CS - 12/24

**Type:** MCQ

**Answer:** VERIFICATION REQUIRED

**Source:** GATE 2007 CS, `12-PYQ/2007/question-paper.pdf`

---
