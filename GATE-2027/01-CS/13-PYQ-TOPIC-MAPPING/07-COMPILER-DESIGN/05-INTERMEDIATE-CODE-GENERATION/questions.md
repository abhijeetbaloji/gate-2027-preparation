# GATE PYQs

## 2025

### Q.52

**Paper:** GATE 2025 CS-1

**Question:**

Refer to the given 3-address code sequence. This code sequence is split into basic
blocks. The number of basic blocks is ________. (Answer in integer)
1001: i = 1
1002: j = 1
1003: t1 = 10*i
1004: t2 = t1+j
1005: t3 = 8*t2
1006: t4 = t3-88
1007: a[t4] = 0.0
1008: j = j+1
1009: if j <= 10 goto 1003
1010: i = i+1
1011: if i <= 10 goto 1002
1012: i = 1
1013: t5 = i-1
1014: t6 = 88*t5
1015: a[t6] = 1.0
1016: i = i+1
1017: if i <= 10 goto 1013

**Options:**

The paper does not print options for this numerical-answer question.

**Type:** NAT

**Answer:** VERIFICATION REQUIRED

**Source:** GATE 2025 CS-1, `12-PYQ/2025/set-01/question-paper.pdf`

---

## 2024

### Q.39

**Paper:** GATE 2024 CS1

**Question:**

Consider the following pseudo-code.
𝐿1:  𝑡1 = −1
𝐿2:  𝑡2 = 0
𝐿3:  𝑡3 = 0
𝐿4:  𝑡4 = 4 ∗𝑡3
𝐿5:  𝑡5 = 4 ∗𝑡2
𝐿6:  𝑡6 = 𝑡5 ∗𝑀
𝐿7:  𝑡7 = 𝑡4 + 𝑡6
𝐿8:  𝑡8 = 𝑎[𝑡7]
𝐿9:  if  𝑡8 <= 𝑚𝑎𝑥 goto  𝐿11
𝐿10:  𝑡1 = 𝑡8
𝐿11:  𝑡3 = 𝑡3 + 1
𝐿12:  if  𝑡3 < 𝑀 goto  𝐿4
𝐿13:  𝑡2 = 𝑡2 + 1
𝐿14:  if  𝑡2 < 𝑁 goto  𝐿3
𝐿15:  𝑚𝑎𝑥 = 𝑡1
Which one of the following options CORRECTLY specifies the number of basic
blocks and the number of instructions in the largest basic block, respectively ?

**Options:**

A. 6 and 6
B. 6 and 7
C. 7 and 7
D. 7 and 6

**Type:** MCQ

**Answer:** VERIFICATION REQUIRED

**Source:** GATE 2024 CS1, `12-PYQ/2024/set-01/question-paper.pdf`

---

### Q.43

**Paper:** GATE 2024 CS2

**Question:**

Consider the following expression: 𝑥[𝑖] = (𝑝+ 𝑟) ∗−𝑠[𝑖] + 𝑢/𝑤. The following
sequence shows the list of triples representing the given expression, with entries
missing for triples (1), (3), and (6).
(0)  +  𝑝  𝑟
(1)
(2) uminus (1)
(3)
(4)  /  𝑢  𝑤
(5)  +  (3)  (4)
(6)
(7)  =  (6) (5)
Which one of the following options fills in the missing entries CORRECTLY?

**Options:**

A. (1) =[]⁡⁡𝑠⁡⁡𝑖 (3) * (0) (2) (6) []=⁡⁡𝑥⁡⁡𝑖
B. (1) []=⁡⁡𝑠⁡⁡𝑖 (3) –⁡(0)⁡(2) (6) =[] ⁡𝑥⁡⁡(5)
C. (1) =[] ⁡𝑠⁡𝑖 (3) * (0)⁡⁡(2) (6) []= ⁡𝑥⁡⁡(5)
D. (1) []= ⁡𝑠⁡⁡𝑖 (3) –⁡(0)⁡(2) (6) =[] 𝑥⁡⁡𝑖

**Type:** MCQ

**Answer:** VERIFICATION REQUIRED

**Source:** GATE 2024 CS2, `12-PYQ/2024/set-02/question-paper.pdf`

---

## 2015

### Q.46

**Paper:** GATE 2015 CS, 7 February Shift 1

**Question:**

A variable x is said to be live at a statement S; in a program if the following three conditions hold
simultaneously:
i. There exists a statement S; that uses x
11. There is a path from S; to S; in the flow graph corresponding to the program
iii. The path has no intervening assignment to x including at S; and S;
1 p=q+r
s=p+q
u=S*v
2 v=r+u 3 9=s*u
4 q=v+r
The variables which are live both at the statement in basic block 2 and at the statement in basic
block 3 of the above control flow graph are

**Options:**

A. p, S, и
B. r, s, u
C. r, u
D. q, v

**Type:** MCQ

**Answer:** VERIFICATION REQUIRED

**Source:** GATE 2015 CS, 7 February Shift 1, `12-PYQ/2015/set-01/question-paper.pdf`

---

### Q.44

**Paper:** GATE 2015 CS, 7 February Shift 2

**Question:**

36

Consider the intermediate code given below.
(1) i = 1
(2) ] = 1
(3) t1 = 5 * i
(4) t2 = t1 + j
(5) t3 = 4 * t2
(6) t4 = t3
(7) a[t4] = -1
(8) j = j + 1
(9) if j<=5 goto (3)
(10) i=i+1
(11) if i<5 goto (2)
The number of nodes and edges in the control-flow-graph constructed for the above code,
respectively, are

**Options:**

A. 5 and 7
B. 6 and 7
C. 5 and 5
D. 7 and 8 4 % D

**Type:** MCQ

**Answer:** VERIFICATION REQUIRED

**Source:** GATE 2015 CS, 7 February Shift 2, `12-PYQ/2015/set-02/question-paper.pdf`

---

## 2014

### Q.34

**Paper:** GATE 2014 CS SET-3

**Question:**

Consider the basic block given below.
a = b + c
c = a + d
d = b + c
e = d - b
a = e + b
The minimum number of nodes and edges present in the DAG representation of the above basic
block respectively are

**Options:**

A. 6 and 6
B. 8 and 10
C. 9 and 12
D. 4 and 4

**Type:** MCQ

**Answer:** VERIFICATION REQUIRED

**Source:** GATE 2014 CS SET-3, `12-PYQ/2014/set-03/question-paper.pdf`

---

## 2007

### Q.54

**Paper:** GATE 2007 CS

**Question:**

In a simplified computer the instructions are:
OP Rj,R; - Performs R; OP R; and stores the result in register Ri.
OP m,R; - Performs val OP R; and stores the result in Rj. val denotes the
content of memory location m.
MOV m,R; - Moves the content of memory location m to register R;.
MOV Ri,m - Moves the content of register R; to memory location m.
The computer has only two registers, and OP is either ADD or SUB. Consider the
following basic block:
t=a+b
12=c+d
[3 = e - 12
t4=t1 - t3
Assume that all operands are initially in memory. The final value of the computation
should be in memory. What is the minimum number of MOV instructions in the code
generated for this basic block?

**Options:**

A. 2
B. 3
C. 5
D. 6

**Type:** MCQ

**Answer:** VERIFICATION REQUIRED

**Source:** GATE 2007 CS, `12-PYQ/2007/question-paper.pdf`

---
