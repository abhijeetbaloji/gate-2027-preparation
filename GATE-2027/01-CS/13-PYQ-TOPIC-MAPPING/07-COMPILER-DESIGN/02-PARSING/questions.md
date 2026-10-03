# GATE PYQs

## 2025

### Q.46

**Paper:** GATE 2025 CS-1

**Question:**

Which of the following statement(s) is/are TRUE while computing First and Follow
during top down parsing by a compiler?

**Options:**

A. For a production 𝐴→𝜖, 𝜖 will be added to 𝐹𝑖𝑟𝑠𝑡(𝐴).
B. If there is any input right end marker, it will be added to 𝐹𝑖𝑟𝑠𝑡(𝑆), where 𝑆 is the start symbol.
C. For a production 𝐴→𝜖, 𝜖 will be added to 𝐹𝑜𝑙𝑙𝑜𝑤(𝐴).
D. If there is any input right end marker, it will be added to 𝐹𝑜𝑙𝑙𝑜𝑤(𝑆), where 𝑆 is the start symbol.

**Type:** MCQ

**Answer:** VERIFICATION REQUIRED

**Source:** GATE 2025 CS-1, `12-PYQ/2025/set-01/question-paper.pdf`

---

## 2024

### Q.26

**Paper:** GATE 2024 CS1

**Question:**

Which of the following is/are Bottom-Up Parser(s)?

**Options:**

A. Shift-reduce Parser
B. Predictive Parser
C. LL(1) Parser
D. LR Parser

**Type:** MCQ

**Answer:** VERIFICATION REQUIRED

**Source:** GATE 2024 CS1, `12-PYQ/2024/set-01/question-paper.pdf`

---

### Q.38

**Paper:** GATE 2024 CS1

**Question:**

Consider the following grammar 𝐺, with 𝑆 as the start symbol. The grammar 𝐺 has
three incomplete productions denoted by (1), (2), and (3).
𝑆→𝑑𝑎𝑇 |  (1)
𝑇→𝑎𝑆 | 𝑏𝑇 |  (2)
𝑅→  (3)  | 𝜖
The set of terminals is {𝑎, 𝑏, 𝑐, 𝑑, 𝑓}. The FIRST and FOLLOW sets of the different
non-terminals are as follows.
FIRST(𝑆) = {𝑐, 𝑑, 𝑓},  FIRST(𝑇) = {𝑎, 𝑏, 𝜖},  FIRST(𝑅) = {𝑐, 𝜖}
FOLLOW(𝑆) = FOLLOW(𝑇) = {𝑐, 𝑓, $},  FOLLOW(𝑅) = {𝑓}
Which one of the following options CORRECTLY fills in the incomplete
productions?

**Options:**

A. (1) 𝑆→𝑅𝑓 (2) 𝑇→𝜖 (3) 𝑅→𝑐𝑇𝑅
B. (1) 𝑆→𝑓𝑅 (2) 𝑇→𝜖 (3) 𝑅→𝑐𝑇𝑅
C. (1) 𝑆→𝑓𝑅 (2) 𝑇→𝑐𝑇 (3) 𝑅→𝑐𝑅
D. (1) 𝑆→𝑅𝑓 (2) 𝑇→𝑐𝑇 (3) 𝑅→𝑐𝑅

**Type:** MCQ

**Answer:** VERIFICATION REQUIRED

**Source:** GATE 2024 CS1, `12-PYQ/2024/set-01/question-paper.pdf`

---

### Q.65

**Paper:** GATE 2024 CS2

**Question:**

Consider the following augmented grammar, which is to be parsed with a SLR
parser. The set of terminals is {𝑎,𝑏,𝑐,𝑑,#,@}
𝑆^{′} →𝑆
𝑆→𝑆𝑆⁡|⁡𝐴𝑎⁡|⁡𝑏𝐴𝑐⁡|⁡𝐵𝑐⁡|⁡𝑏𝐵𝑎
𝐴→𝑑#
𝐵→@
Let 𝐼_{0} = 𝐶𝐿𝑂𝑆𝑈𝑅𝐸({𝑆^{′} →⁡• 𝑆}). The number of items in the set 𝐺𝑂𝑇𝑂(𝐼_{0}, 𝑆)
is ___________

**Options:**

The paper does not print options for this numerical-answer question.

**Type:** NAT

**Answer:** VERIFICATION REQUIRED

**Source:** GATE 2024 CS2, `12-PYQ/2024/set-02/question-paper.pdf`

---

## 2022

### Q.13

**Paper:** GATE 2022 CS

**Question:**

Which one of the following statements is TRUE?

**Options:**

A. The LALR(1) parser for a grammar G cannot have reduce-reduce conflict if the LR(1) parser for G does not have reduce-reduce conflict.
B. Symbol table is accessed only during the lexical analysis phase.
C. Data flow analysis is necessary for run-time memory management.
D. LR(1) parsing is sufficient for deterministic context-free languages.

**Type:** MCQ

**Answer:** VERIFICATION REQUIRED

**Source:** GATE 2022 CS, `12-PYQ/2022/question-paper.pdf`

---

### Q.65

**Paper:** GATE 2022 CS

**Question:**

Consider the following grammar along with translation rules.
S → S_{1} # T  {S_{•}val  S_{1}•val * T_{•}val}
S → T  {S   T }
•val  •val
T → T %R  {T   T   R }
1  •val  1•val  •val
T → R  {T  R }
•val  •val
R → id  {R  id }
•val  •val
Here  #  and  %  are operators and id is a token that represents an integer and  id_{•}val
represents the corresponding integer value. The set of non-terminals is { S , T , R , P}
and a subscripted non-terminal indicates an instance of the non-terminal.
Using this translation scheme, the computed value of  S_{•}val  for root of the parse tree
for the expression  20#10%5#8%2%2  is _____________.

**Options:**

The paper does not print options for this numerical-answer question.

**Type:** NAT

**Answer:** VERIFICATION REQUIRED

**Source:** GATE 2022 CS, `12-PYQ/2022/question-paper.pdf`

---

## 2019

### Q.3

**Paper:** GATE 2019 CS (printed header Set-2)

**Question:**

Which one of the following kinds of derivation is used by LR parsers?

**Options:**

A. Leftmost
B. Leftmost in reverse
C. Rightmost
D. Rightmost in reverse

**Type:** MCQ

**Answer:** VERIFICATION REQUIRED

**Source:** GATE 2019 CS (printed header Set-2), `12-PYQ/2019/question-paper.pdf`

---

## 2018

### Q.38

**Paper:** GATE 2018 CS

**Question:**

Consider the following parse tree for the expression a#b$c$d#e#f, involving two binary
operators $ and #.
Which one of the following is correct for the given parse tree?

**Options:**

A. $ has higher precedence and is left associative; # is right associative
B. # has higher precedence and is left associative; $ is right associative
C. $ has higher precedence and is left associative; # is left associative
D. # has higher precedence and is right associative; $ is left associative

**Type:** MCQ

**Answer:** VERIFICATION REQUIRED

**Source:** GATE 2018 CS, `12-PYQ/2018/question-paper.pdf`

---

## 2015

### Q.65

**Paper:** GATE 2015 CS, 8 February Shift 1

**Question:**

Consider the following grammar G
S→ FH
F→pc
dl c
where S,F, and H are non-terminal symbols, p, d, and c are terminal symbols. Which of the
following statement(s) is/are correct?
S1. LL(1) can parse all strungs that are generated using grammar G
S2. LR(1) can parse all strings that are generated using grammar G

**Options:**

A. Only S1
B. Only S2
C. Both S1 and S2
D. Neither S1 nor S2

**Type:** MCQ

**Answer:** VERIFICATION REQUIRED

**Source:** GATE 2015 CS, 8 February Shift 1, `12-PYQ/2015/set-03/question-paper.pdf`

---

## 2013

### Q.9

**Paper:** GATE 2013 CS Booklet A

**Question:**

What is the maximum number of reduce moves that can be taken by a bottom-up parser for a
grammar with no epsilon- and unit-production (i.e., of type A → є and A → a) to parse a string
with n tokens?

**Options:**

A. n/2
B. n-1
C. 2n-1
D. 2^{n}

**Type:** MCQ

**Answer:** VERIFICATION REQUIRED

**Source:** GATE 2013 CS Booklet A, `12-PYQ/2013/set-01/question-paper.pdf`

---

### Q.40

**Paper:** GATE 2013 CS Booklet A

**Question:**

Consider the following two sets of LR(1) items of an LR(1) grammar.
X → c.X, c/d  X → c.X, $
X → .cX, c/d  X → .cX, $
X → .d, c/d  X → .d, $
Which of the following statements related to merging of the two sets in the corresponding LALR
parser is/are FALSE?
1.  Cannot be merged since look aheads are different.
2.  Can be merged but will result in S-R conflict.
3.  Can be merged but will result in R-R conflict.
4.  Cannot be merged since goto on c will lead to two different sets.

**Options:**

A. 1 only
B. 2 only
C. 1 and 4 only
D. 1, 2, 3 and 4

**Type:** MCQ

**Answer:** VERIFICATION REQUIRED

**Source:** GATE 2013 CS Booklet A, `12-PYQ/2013/set-01/question-paper.pdf`

---

### Q.17

**Paper:** GATE 2013 CS Booklet B

**Question:**

What is the maximum number of reduce moves that can be taken by a bottom-up parser for a
grammar with no epsilon- and unit-production (i.e., of type A → є and A → a) to parse a string
with n tokens?

**Options:**

A. n/2
B. n-1
C. 2n-1
D. 2^{n}

**Type:** MCQ

**Answer:** VERIFICATION REQUIRED

**Source:** GATE 2013 CS Booklet B, `12-PYQ/2013/set-02/question-paper.pdf`

---

### Q.33

**Paper:** GATE 2013 CS Booklet B

**Question:**

Consider the following two sets of LR(1) items of an LR(1) grammar.
X → c.X, c/d  X → c.X, $
X → .cX, c/d  X → .cX, $
X → .d, c/d  X → .d, $
Which of the following statements related to merging of the two sets in the corresponding LALR
parser is/are FALSE?
1.  Cannot be merged since look aheads are different.
2.  Can be merged but will result in S-R conflict.
3.  Can be merged but will result in R-R conflict.
4.  Cannot be merged since goto on c will lead to two different sets.

**Options:**

A. 1 only
B. 2 only
C. 1 and 4 only
D. 1, 2, 3 and 4

**Type:** MCQ

**Answer:** VERIFICATION REQUIRED

**Source:** GATE 2013 CS Booklet B, `12-PYQ/2013/set-02/question-paper.pdf`

---

### Q.4

**Paper:** GATE 2013 CS Booklet C

**Question:**

What is the maximum number of reduce moves that can be taken by a bottom-up parser for a
grammar with no epsilon- and unit-production (i.e., of type A → є and A → a) to parse a string
with n tokens?

**Options:**

A. n/2
B. n-1
C. 2n-1
D. 2^{n}

**Type:** MCQ

**Answer:** VERIFICATION REQUIRED

**Source:** GATE 2013 CS Booklet C, `12-PYQ/2013/set-03/question-paper.pdf`

---

### Q.44

**Paper:** GATE 2013 CS Booklet C

**Question:**

Consider the following two sets of LR(1) items of an LR(1) grammar.
X → c.X, c/d  X → c.X, $
X → .cX, c/d  X → .cX, $
X → .d, c/d  X → .d, $
Which of the following statements related to merging of the two sets in the corresponding LALR
parser is/are FALSE?
1.  Cannot be merged since look aheads are different.
2.  Can be merged but will result in S-R conflict.
3.  Can be merged but will result in R-R conflict.
4.  Cannot be merged since goto on c will lead to two different sets.

**Options:**

A. 1 only
B. 2 only
C. 1 and 4 only
D. 1, 2, 3 and 4

**Type:** MCQ

**Answer:** VERIFICATION REQUIRED

**Source:** GATE 2013 CS Booklet C, `12-PYQ/2013/set-03/question-paper.pdf`

---

### Q.22

**Paper:** GATE 2013 CS Booklet D

**Question:**

What is the maximum number of reduce moves that can be taken by a bottom-up parser for a
grammar with no epsilon- and unit-production (i.e., of type A → є and A → a) to parse a string
with n tokens?

**Options:**

A. n/2
B. n-1
C. 2n-1
D. 2^{n}

**Type:** MCQ

**Answer:** VERIFICATION REQUIRED

**Source:** GATE 2013 CS Booklet D, `12-PYQ/2013/set-04/question-paper.pdf`

---

### Q.29

**Paper:** GATE 2013 CS Booklet D

**Question:**

Consider the following two sets of LR(1) items of an LR(1) grammar.
X → c.X, c/d  X → c.X, $
X → .cX, c/d  X → .cX, $
X → .d, c/d  X → .d, $
Which of the following statements related to merging of the two sets in the corresponding LALR
parser is/are FALSE?
1.  Cannot be merged since look aheads are different.
2.  Can be merged but will result in S-R conflict.
3.  Can be merged but will result in R-R conflict.
4.  Cannot be merged since goto on c will lead to two different sets.

**Options:**

A. 1 only
B. 2 only
C. 1 and 4 only
D. 1, 2, 3 and 4

**Type:** MCQ

**Answer:** VERIFICATION REQUIRED

**Source:** GATE 2013 CS Booklet D, `12-PYQ/2013/set-04/question-paper.pdf`

---

## 2012

### Q.51

**Paper:** GATE 2012 CS Booklet A

**Question:**

How many tuples does the result of the following SQL query contain?
SELECT A.Id
FROM A
WHERE A.Age  >  ALL (SELECT B.Age
FROM B
WHERE B.Name = ‘Arun’)

**Options:**

A. 4
B. 3
C. 0
D. 1 CS-A 14/20 2012 COMPUTER SCIENCE & INFORMATION TECH. – CS Linked Answer Questions Statement for Linked Answer Questions 52 and 53: For the grammar below, a partial LL(1) parsing table is also presented along with the grammar. Entries that need to be filled are indicated as E1, E2, and E3.  is the empty string, $ indicates end of input, and, | separates alternate right hand sides of productions. S  a A b B | b A a B |  A  S B  S a b $ S E1 E2 S   A A  S A  S error B B  S B  S E3

**Type:** MCQ

**Answer:** VERIFICATION REQUIRED

**Source:** GATE 2012 CS Booklet A, `12-PYQ/2012/question-paper.pdf`

---

### Q.52

**Paper:** GATE 2012 CS Booklet A

**Question:**

The FIRST and FOLLOW sets for the non-terminals A and B are

**Options:**

A. = {a, b} FOLLOW
B. = {a, b}
C. FIRST
D. FIRST

**Type:** MCQ

**Answer:** VERIFICATION REQUIRED

**Source:** GATE 2012 CS Booklet A, `12-PYQ/2012/question-paper.pdf`

---

## 2011

### Q.1

**Paper:** GATE 2011 CS Booklet A

**Question:**

In a compiler, keywords of a language are recognized during

**Options:**

A. parsing of the program
B. the code generation
C. the lexical analysis of the program
D. dataflow analysis

**Type:** MCQ

**Answer:** VERIFICATION REQUIRED

**Source:** GATE 2011 CS Booklet A, `12-PYQ/2011/question-paper.pdf`

---

### Q.27

**Paper:** GATE 2011 CS Booklet A

**Question:**

Consider two binary operators 'f' and "I' with the precedence of operator | being lower than that
of the operator †. Operator T is right associative while operator 1 is left associative. Which one of
the following represents the parse tree for expression (7|31413|2)?

**Options:**

B. 2
C. N 2 3 CS-A 7/20

**Type:** MCQ

**Answer:** VERIFICATION REQUIRED

**Source:** GATE 2011 CS Booklet A, `12-PYQ/2011/question-paper.pdf`

---

## 2010

### Q.37

**Paper:** GATE 2010 CS

**Question:**

The program beloss uses six lemporary variables a, b. c.d, e, f.
a =1
b = 10
с = 20
d a + b
e =c + d
f = c + e
b=c+e
e =b + f
d = 5 + e
return d + f
Assuming that all opcrations lake their opcrands from registers, what is the minimum number of
registers nceded lo exccute this program without spilling?

**Options:**

A. (O*10*1)* (13)U*(10*10)*)* 1)0(10*1)4
B. LR(1) but not LL
C. Both LL/1) and LK(I)
D. 0*(10*1)*10* 924

**Type:** MCQ

**Answer:** VERIFICATION REQUIRED

**Source:** GATE 2010 CS, `12-PYQ/2010/question-paper.pdf`

---

## 2008

### Q.55

**Paper:** GATE 2008 CS

**Question:**

An LALR(1) parser for a grammar G can have shift-reduce (S-R) conflicts if and only if

**Options:**

A. the SLR(1) parser for G has S-R conflicts
B. the LR(1) parser for G has S-R conflicts
C. the LR(0) parser for G has S-R conflicts
D. the LALR(1) parser for G has reduce-reduce conflicts

**Type:** MCQ

**Answer:** VERIFICATION REQUIRED

**Source:** GATE 2008 CS, `12-PYQ/2008/question-paper.pdf`

---
