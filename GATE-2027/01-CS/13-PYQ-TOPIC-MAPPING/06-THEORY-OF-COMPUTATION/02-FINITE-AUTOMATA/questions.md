# GATE PYQs

## 2026

### Q.26

**Paper:** GATE 2026 CS-1 (forenoon)

**Question:**

Let  M  be a nondeterministic finite automaton (NFA) with 6 states over a finite
alphabet.
Which of the following options CANNOT be the number of states in the minimal
deterministic finite automaton (DFA) that is equivalent to 𝑀 ?

**Options:**

A. 32
B. 65
C. 1
D. 128

**Type:** MCQ

**Answer:** VERIFICATION REQUIRED

**Source:** GATE 2026 CS-1 (forenoon), `12-PYQ/2026/set-01/question-paper.pdf`

---

### Q.47

**Paper:** GATE 2026 CS-2 (afternoon)

**Question:**

Consider the following two finite automata 𝐷_{1} and 𝐷_{2}.
Which of the following statements is/are true?

**Options:**

A. 𝐿(𝐷_{1}) = 𝐿(𝐷_{2})
B. 𝐿(𝐷_{1}) is a proper subset of 𝐿(𝐷_{2})
C. 𝐿(𝐷_{1}) ∩𝐿(𝐷_{2}) = { 𝜖}
D. (𝐿(𝐷_{1}) ∪𝐿(𝐷_{2}))^{∗} consists of all strings in {0,1}^{∗} whose length is divisible by 3

**Type:** MCQ

**Answer:** VERIFICATION REQUIRED

**Source:** GATE 2026 CS-2 (afternoon), `12-PYQ/2026/set-02/question-paper.pdf`

---

## 2025

### Q.28

**Paper:** GATE 2025 CS-1

**Question:**

A regular language  𝐿 is accepted by a non-deterministic finite automaton (NFA)
with 𝑛 states. Which of the following statement(s) is/are FALSE?

**Options:**

A. 𝐿 may have an accepting NFA with < 𝑛 states.
B. 𝐿 may have an accepting DFA with < 𝑛 states.
C. There exists a DFA with ≤2^{𝑛} states that accepts 𝐿.
D. Every DFA that accepts 𝐿 has > 2^{𝑛} states.

**Type:** MCQ

**Answer:** VERIFICATION REQUIRED

**Source:** GATE 2025 CS-1, `12-PYQ/2025/set-01/question-paper.pdf`

---

### Q.50

**Paper:** GATE 2025 CS-1

**Question:**

Consider the following deterministic finite automaton (DFA) defined over the
alphabet, Σ = {𝑎, 𝑏}. Identify which of the following language(s) is/are accepted by
the given DFA.

**Options:**

A. The set of all strings containing an even number of 𝑏’s.
B. The set of all strings containing the pattern 𝑏𝑎𝑏.
C. The set of all strings ending with the pattern 𝑏𝑎𝑏.
D. The set of all strings not containing the pattern 𝑎𝑏𝑎.

**Type:** MCQ

**Answer:** VERIFICATION REQUIRED

**Source:** GATE 2025 CS-1, `12-PYQ/2025/set-01/question-paper.pdf`

---

### Q.60

**Paper:** GATE 2025 CS-2

**Question:**

Let  Σ = {1,2,3,4}.  For  𝑥∈Σ^{∗}, let  𝑝𝑟𝑜𝑑(𝑥) be the product of symbols in
𝑥 modulo 7. We take 𝑝𝑟𝑜𝑑(𝜖) = 1, where 𝜖 is the null string.
For example, 𝑝𝑟𝑜𝑑(124) = (1 × 2 × 4) mod 7 = 1.
Define  𝐿= {𝑥∈Σ^{∗} | 𝑝𝑟𝑜𝑑(𝑥) = 2}.
The number of states in a minimum state DFA for 𝐿 is ___________. (Answer in
integer)

**Options:**

The paper does not print options for this numerical-answer question.

**Type:** NAT

**Answer:** VERIFICATION REQUIRED

**Source:** GATE 2025 CS-2, `12-PYQ/2025/set-02/question-paper.pdf`

---

## 2024

### Q.50

**Paper:** GATE 2024 CS1

**Question:**

Consider the 5-state DFA  𝑀 accepting the language 𝐿(𝑀) ⊂(0 + 1)^{∗} shown
below.  For any string 𝑤∈(0 + 1)^{∗} let  𝑛 (𝑤) be the number of 0^{′}𝑠 in 𝑤 and
0
𝑛_{1}(𝑤) be the number of 1′𝑠 in 𝑤.
Which of the following statements is/are FALSE?

**Options:**

A. States 2 and 4 are distinguishable in 𝑀
B. States 3 and 4 are distinguishable in 𝑀
C. States 2 and 5 are distinguishable in 𝑀
D. Any string 𝑤 with 𝑛_{0}(𝑤) = 𝑛_{1}(𝑤) is in 𝐿(𝑀)

**Type:** MCQ

**Answer:** VERIFICATION REQUIRED

**Source:** GATE 2024 CS1, `12-PYQ/2024/set-01/question-paper.pdf`

---

### Q.22

**Paper:** GATE 2024 CS2

**Question:**

Which one of the following regular expressions is equivalent to the language
accepted by the DFA given below?
0
1  0
1

**Options:**

A. 0^{∗}1(0 + 10^{∗}1)^{∗}
B. 0^{∗}(10^{∗}11)^{∗}0^{∗}
C. 0^{∗}1(010^{∗}1)^{∗}0^{∗}
D. 0(1 + 0^{∗}10^{∗}1)^{∗}0^{∗}

**Type:** MCQ

**Answer:** VERIFICATION REQUIRED

**Source:** GATE 2024 CS2, `12-PYQ/2024/set-02/question-paper.pdf`

---

## 2023

### Q.14

**Paper:** GATE 2023 CS

**Question:**

Consider the Deterministic Finite-state Automaton (DFA) A shown below. The
DFA runs on the alphabet {0, 1}, and has the set of states {s, p, q, r}, with s being
the start state and p being the only final state.
0
1
s^{1}  p  q
1
0  0
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

### Q.63

**Paper:** GATE 2023 CS

**Question:**

Consider the language L over the alphabet {0, 1}, given below:
L = {w ∈{0, 1}^{∗} | w does not contain three or more consecutive 1’s}.
The minimum number of states in a Deterministic Finite-State Automaton (DFA)
for L is  .

**Options:**

The paper does not print options for this numerical-answer question.

**Type:** NAT

**Answer:** VERIFICATION REQUIRED

**Source:** GATE 2023 CS, `12-PYQ/2023/question-paper.pdf`

---

## 2022

### Q.12

**Paper:** GATE 2022 CS

**Question:**

Which one of the following regular expressions correctly represents the language
of the finite automaton given below?

**Options:**

A. ab bab^{*} *  ba ^{*}aba^{*}
B. (ab b^{*} )^{*}ab^{*}  (ba^{*} a )^{*}ba^{*}
C. (ab b^{*}  ba^{*} a)^{*} (a^{*}  b^{*})
D. (ba a^{*}  ab b^{*} )^{*} (ab^{*}  ba^{*})

**Type:** MCQ

**Answer:** VERIFICATION REQUIRED

**Source:** GATE 2022 CS, `12-PYQ/2022/question-paper.pdf`

---

## 2021

### Q.38

**Paper:** GATE 2021 CS Set-1

**Question:**

Consider the following language.
L = {w € {0,1} | w ends with the substring 011}
Which one of the following deterministic finite automata accepts L?
0
start

**Options:**

A. 0,1 +8
B. start → 0 start → 0
C. 1 0 start
D. GATE Graduate Aptitude Test in Engineering 2021 2021 Organising Institute - IIT Bombay

**Type:** MCQ

**Answer:** VERIFICATION REQUIRED

**Source:** GATE 2021 CS Set-1, `12-PYQ/2021/set-01/question-paper.pdf`

---

## 2020

### Q.51

**Paper:** GATE 2020 CS

**Question:**

Consider the following language.
L = {x € {a, b}*| number of a's in x is divisible by 2 but not divisible by 3}
The minimum number of states in a DFA that accepts L is

**Options:**

The paper does not print options for this numerical-answer question.

**Type:** NAT

**Answer:** VERIFICATION REQUIRED

**Source:** GATE 2020 CS, `12-PYQ/2020/question-paper.pdf`

---

## 2019

### Q.48

**Paper:** GATE 2019 CS (printed header Set-2)

**Question:**

Let E be the set of all bijections from (1,..., 5} to (1,...,5), where id denotes the identity
function, i.e. id(j) = j,Vj. Let • denote composition on functions. For a string x =
X1X2...Xn EX",n ≥O, letn(x)= x1°x2°.O Xn-
Consider the language L = {x E [*| n(x) = id). The minimum number of states in any
DFA accepting L is _

**Options:**

The paper does not print options for this numerical-answer question.

**Type:** NAT

**Answer:** VERIFICATION REQUIRED

**Source:** GATE 2019 CS (printed header Set-2), `12-PYQ/2019/question-paper.pdf`

---

## 2018

### Q.6

**Paper:** GATE 2018 CS

**Question:**

Let N be an NFA with n states. Let k be the number of states of a minimal DFA which is
equivalent to N. Which one of the following is necessarily true?

**Options:**

A. 𝑘≥2^{𝑛}
B. 𝑘≥𝑛
C. 𝑘≤𝑛^{2}
D. 𝑘≤2^{𝑛}

**Type:** MCQ

**Answer:** VERIFICATION REQUIRED

**Source:** GATE 2018 CS, `12-PYQ/2018/question-paper.pdf`

---

## 2017

### Q.25

**Paper:** GATE 2017 CS Session 2

**Question:**

Correct: 1 Wrong : 0
The minimum possible mumber of states of a deterministic finite automaton that accepts the regular
language L = {w1aw2 | w1, w2 e {a, b}*. .|w1|=2,|12≥3}1s

**Options:**

The paper does not print options for this numerical-answer question.

**Type:** NAT

**Answer:** VERIFICATION REQUIRED

**Source:** GATE 2017 CS Session 2, `12-PYQ/2017/set-02/question-paper.pdf`

---

### Q.39

**Paper:** GATE 2017 CS Session 2

**Question:**

Correct: 2 Wrong: -0.66
Let & denote the transition function and & denote the extended transition function of the e-NFA
whose transition table is given below:
a b
→ 90 {92} {91) {90}
91 {92} {92} {93}
92 {go)
93 {92}
Then 8(g2, aba) is
(А) Ø (B) (90, 91, 93) (C) {90,91,92) (D) {9o, 92, 93}

**Options:**

The paper does not print options for this numerical-answer question.

**Type:** NAT

**Answer:** VERIFICATION REQUIRED

**Source:** GATE 2017 CS Session 2, `12-PYQ/2017/set-02/question-paper.pdf`

---

## 2016

### Q.16

**Paper:** GATE 2016 CS-2

**Question:**

The number of states in the minimum sized DFA that accepts the language defined by the
regular expression
(0 + 1)^{∗}(0 + 1)(0 + 1)^{∗}
is  .

**Options:**

The paper does not print options for this numerical-answer question.

**Type:** NAT

**Answer:** VERIFICATION REQUIRED

**Source:** GATE 2016 CS-2, `12-PYQ/2016/set-02/question-paper.pdf`

---

### Q.42

**Paper:** GATE 2016 CS-2

**Question:**

Consider the following two statements:
I. If all states of an NFA are accepting states then the language accepted by the NFA is Σ^{∗}.
II. There exists a regular language A such that for all languages B, A ∩ B is regular.
Which one of the following is CORRECT?

**Options:**

A. Only I is true
B. Only II is true
C. Both I and II are true
D. Both I and II are false

**Type:** MCQ

**Answer:** VERIFICATION REQUIRED

**Source:** GATE 2016 CS-2, `12-PYQ/2016/set-02/question-paper.pdf`

---

## 2015

### Q.49

**Paper:** GATE 2015 CS, 7 February Shift 1

**Question:**

a
M:
a
Consider the DFAs M and N given above. The number of states in a minimal DFA that accepts the
language L(M) N L(N) is_
Correct Answer :

**Options:**

The paper does not print options for this numerical-answer question.

**Type:** NAT

**Answer:** VERIFICATION REQUIRED

**Source:** GATE 2015 CS, 7 February Shift 1, `12-PYQ/2015/set-01/question-paper.pdf`

---

### Q.27

**Paper:** GATE 2015 CS, 7 February Shift 2

**Question:**

4.

Match the following:
P. Lexical analysıs 1. Graph coloring
Q. Parsing 2. DFA minimization
R. Register allocation 3. Post-order traversal
S. Expression evaluation 4. Production tree

**Options:**

A. P-2, Q-3, R-1, S-4
B. P-2, Q-1, R-4, S-3
C. P-2, Q-4, R-1, S-3
D. P-2, Q-3, R-4, S-1

**Type:** MCQ

**Answer:** VERIFICATION REQUIRED

**Source:** GATE 2015 CS, 7 February Shift 2, `12-PYQ/2015/set-02/question-paper.pdf`

---

### Q.45

**Paper:** GATE 2015 CS, 7 February Shift 2

**Question:**

The number of states in the minimal deterministic finite automaton corresponding to the regular
expression (0 + 1)*(10) is _
Correct Answer :

**Options:**

The paper does not print options for this numerical-answer question.

**Type:** NAT

**Answer:** VERIFICATION REQUIRED

**Source:** GATE 2015 CS, 7 February Shift 2, `12-PYQ/2015/set-02/question-paper.pdf`

---

### Q.32

**Paper:** GATE 2015 CS, 8 February Shift 1

**Question:**

Let L be the language represented by the regular expression [*00112* where [ = (0,1). What is
the minimum number of states in a DFA that recognizes L (complement of L)?

**Options:**

A. 4
B. 5
C. 6
D. 8

**Type:** MCQ

**Answer:** VERIFICATION REQUIRED

**Source:** GATE 2015 CS, 8 February Shift 1, `12-PYQ/2015/set-03/question-paper.pdf`

---

## 2014

### Q.16

**Paper:** GATE 2014 CS SET-1

**Question:**

Consider the finite automaton in the following figure.
0,1  1
1 0,1 0,1 93 90 91 92
CS01 (GATE 2014)
What is the set of reachable states for the input string 0011?

**Options:**

A. {90,91,92}
B. {90,91}
C. {90,91,92,93}
D. {ݍ_{ଷ}}

**Type:** MCQ

**Answer:** VERIFICATION REQUIRED

**Source:** GATE 2014 CS SET-1, `12-PYQ/2014/set-01/question-paper.pdf`

---

### Q.36

**Paper:** GATE 2014 CS SET-1

**Question:**

Which of the regular expressions given below represent the following DFA?
0  0  1
1
I)  0*1(1+00*1)*
II)  0*1*1+11*0*1
III) (0+1)*1

**Options:**

A. I and II only
B. I and III only
C. II and III only
D. I, II, and III

**Type:** MCQ

**Answer:** VERIFICATION REQUIRED

**Source:** GATE 2014 CS SET-1, `12-PYQ/2014/set-01/question-paper.pdf`

---

## 2013

### Q.33

**Paper:** GATE 2013 CS Booklet A

**Question:**

Consider the DFA A given below.
Which of the following are FALSE?
1.  Complement of L(A) is context-free.
2.  L(A) = L((11*0+0)(0 + 1)*0*1*)
3.  For the language accepted by A, A is the minimal DFA.
4.  A accepts all strings over {0, 1} of length at least 2.

**Options:**

A. 1 and 3 only
B. 2 and 4 only
C. 2 and 3 only
D. 3 and 4 only

**Type:** MCQ

**Answer:** VERIFICATION REQUIRED

**Source:** GATE 2013 CS Booklet A, `12-PYQ/2013/set-01/question-paper.pdf`

---

### Q.40

**Paper:** GATE 2013 CS Booklet B

**Question:**

Consider the DFA A given below.
Which of the following are FALSE?
1.  Complement of L(A) is context-free.
2.  L(A) = L((11*0+0)(0 + 1)*0*1*)
3.  For the language accepted by A, A is the minimal DFA.
4.  A accepts all strings over {0, 1} of length at least 2.

**Options:**

A. 1 and 3 only
B. 2 and 4 only
C. 2 and 3 only
D. 3 and 4 only

**Type:** MCQ

**Answer:** VERIFICATION REQUIRED

**Source:** GATE 2013 CS Booklet B, `12-PYQ/2013/set-02/question-paper.pdf`

---

### Q.29

**Paper:** GATE 2013 CS Booklet C

**Question:**

Consider the DFA A given below.
Which of the following are FALSE?
1.  Complement of L(A) is context-free.
2.  L(A) = L((11*0+0)(0 + 1)*0*1*)
3.  For the language accepted by A, A is the minimal DFA.
4.  A accepts all strings over {0, 1} of length at least 2.

**Options:**

A. 1 and 3 only
B. 2 and 4 only
C. 2 and 3 only
D. 3 and 4 only

**Type:** MCQ

**Answer:** VERIFICATION REQUIRED

**Source:** GATE 2013 CS Booklet C, `12-PYQ/2013/set-03/question-paper.pdf`

---

### Q.44

**Paper:** GATE 2013 CS Booklet D

**Question:**

Consider the DFA A given below.
Which of the following are FALSE?
1.  Complement of L(A) is context-free.
2.  L(A) = L((11*0+0)(0 + 1)*0*1*)
3.  For the language accepted by A, A is the minimal DFA.
4.  A accepts all strings over {0, 1} of length at least 2.

**Options:**

A. 1 and 3 only
B. 2 and 4 only
C. 2 and 3 only
D. 3 and 4 only

**Type:** MCQ

**Answer:** VERIFICATION REQUIRED

**Source:** GATE 2013 CS Booklet D, `12-PYQ/2013/set-04/question-paper.pdf`

---

## 2012

### Q.12

**Paper:** GATE 2012 CS Booklet A

**Question:**

What is the complement of the language accepted by the NFA shown below?
Assume  = {a} and  is the empty string.
a  


**Options:**

A. ∅
B. {}
C. a^{*}
D. {a , } CS-A 3/20 2012 COMPUTER SCIENCE & INFORMATION TECH. – CS

**Type:** MCQ

**Answer:** VERIFICATION REQUIRED

**Source:** GATE 2012 CS Booklet A, `12-PYQ/2012/question-paper.pdf`

---

### Q.46

**Paper:** GATE 2012 CS Booklet A

**Question:**

Consider the set of strings on {0,1} in which, every substring of 3 symbols has at most two zeros.
For example, 001110 and 011001 are in the language, but 100010 is not. All strings of length less
than 3 are also in the language. A partially completed DFA that accepts this language is shown
below.
00
0
1
0  01
0
0  1
  q  0, 1
1  0
1  10
11
1
The missing arcs in the DFA are

**Options:**

B. 00 01 10 11 q 00 01 10 11 q 00 1 0 00 0 1 01 1 01 1 10 0 10 0 11 0 11 0
D. 00 01 10 11 q 00 01 10 11 q 00 1 0 00 1 0 01 1 01 1 10 0 10 0 11 0 11 0 CS-A 11/20 2012 COMPUTER SCIENCE & INFORMATION TECH. – CS

**Type:** MCQ

**Answer:** VERIFICATION REQUIRED

**Source:** GATE 2012 CS Booklet A, `12-PYQ/2012/question-paper.pdf`

---

## 2011

### Q.42

**Paper:** GATE 2011 CS Booklet A

**Question:**

Definition of a language L with alphabet {a) is given as following.
L={a" (k > 0, and n is a positive integer constant}
What is the minimum number of states needed in a DFA to recognize L?

**Options:**

A. k+l
B. n+1
C. 2"+1
D. 2k+1

**Type:** MCQ

**Answer:** VERIFICATION REQUIRED

**Source:** GATE 2011 CS Booklet A, `12-PYQ/2011/question-paper.pdf`

---

### Q.45

**Paper:** GATE 2011 CS Booklet A

**Question:**

2011
A deterministic finite automaton (DFA) D with alphabet E ={a,b} is given below.
a,
a, b a, b
Which of the following finite state machines is a valid minimal DFA which accepts the same
language as D?

**Options:**

B. a,b a,b b a,b a,b a a a,b
D. b a, b b a, b b a, b

**Type:** MCQ

**Answer:** VERIFICATION REQUIRED

**Source:** GATE 2011 CS Booklet A, `12-PYQ/2011/question-paper.pdf`

---

## 2010

### Q.41

**Paper:** GATE 2010 CS

**Question:**

Let w be any string of length a in (0,1!". Let & be the set of all subsirings of wi. What is the
minimum number of states in a non delerministic finite automaton that accepts L?

**Options:**

A. «-1
B. :
C. #+1
D. 21-L

**Type:** MCQ

**Answer:** VERIFICATION REQUIRED

**Source:** GATE 2010 CS, `12-PYQ/2010/question-paper.pdf`

---

## 2009

### Q.41

**Paper:** GATE 2009 CS

**Question:**

The above DFA accepts the set of all strings over (0, 1) that

**Options:**

A. begin either with 0 or 1.
B. end with 0.
C. end with 00.
D. contain the substring 00.

**Type:** MCQ

**Answer:** VERIFICATION REQUIRED

**Source:** GATE 2009 CS, `12-PYQ/2009/question-paper.pdf`

---

## 2007

### Q.29

**Paper:** GATE 2007 CS

**Question:**

A minimum state deterministic finite automaton accepting the language
L=wwe (0,1)", number of Os and ls in w are divisible by 3 and 5, respectively) has

**Options:**

A. 15 states
B. 11 states
C. 10 states
D. 9 states CS - 6/24

**Type:** MCQ

**Answer:** VERIFICATION REQUIRED

**Source:** GATE 2007 CS, `12-PYQ/2007/question-paper.pdf`

---
