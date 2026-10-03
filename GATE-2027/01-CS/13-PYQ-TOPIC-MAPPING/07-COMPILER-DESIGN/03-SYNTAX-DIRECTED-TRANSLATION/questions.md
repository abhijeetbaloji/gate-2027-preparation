# GATE PYQs

## 2026

### Q.53

**Paper:** GATE 2026 CS-1 (forenoon)

**Question:**

Consider the following two syntax-directed definitions SDD1 and SDD2 for type
declarations.
SDD1  SDD2
Grammar  Semantic Rules  Grammar  Semantic Rules
(G1)  (G2)
𝐷 →𝑇 𝑉  𝐷. 𝑡𝑦𝑝𝑒 = 𝑇. 𝑡𝑦𝑝𝑒  𝐷→𝐷  𝑖𝑑  𝐷. 𝑡𝑦𝑝𝑒= 𝐷 . 𝑡𝑦𝑝𝑒
1  1
𝑉. 𝑡𝑦𝑝𝑒 = 𝑇. 𝑡𝑦𝑝𝑒  𝑝𝑢𝑡(𝑖𝑑. 𝑒𝑛𝑡𝑟𝑦, 𝐷_{1}. 𝑡𝑦𝑝𝑒)
𝑇 → 𝑖𝑛𝑡  𝑇. 𝑡𝑦𝑝𝑒 = 𝑖𝑛𝑡  𝐷 → 𝑇 𝑖𝑑  𝐷. 𝑡𝑦𝑝𝑒 = 𝑇. 𝑡𝑦𝑝𝑒
𝑇 → 𝑓𝑙𝑜𝑎𝑡  𝑇. 𝑡𝑦𝑝𝑒 = 𝑓𝑙𝑜𝑎𝑡  𝑝𝑢𝑡(𝑖𝑑. 𝑒𝑛𝑡𝑟𝑦, 𝑇. 𝑡𝑦𝑝𝑒)
𝑉→𝑉_{1} 𝑖𝑑  𝑉_{1}. 𝑡𝑦𝑝𝑒= 𝑉. 𝑡𝑦𝑝𝑒
𝑝𝑢𝑡(𝑖𝑑. 𝑒𝑛𝑡𝑟𝑦, 𝑉. 𝑡𝑦𝑝𝑒)  𝑇 →𝑖𝑛𝑡  𝑇. 𝑡𝑦𝑝𝑒 = 𝑖𝑛𝑡
𝑇 → 𝑓𝑙𝑜𝑎𝑡  𝑇. 𝑡𝑦𝑝𝑒 = 𝑓𝑙𝑜𝑎𝑡
𝑉 → 𝑖𝑑  𝑝𝑢𝑡(𝑖𝑑. 𝑒𝑛𝑡𝑟𝑦, 𝑉. 𝑡𝑦𝑝𝑒)
𝐷 is the start symbol, and 𝑖𝑛𝑡, 𝑓𝑙𝑜𝑎𝑡 and 𝑖𝑑 are the three terminals. The non-terminal
𝑉_{1} is the same as 𝑉 and the non-terminal 𝐷_{1} is the same as 𝐷. Here, the subscript is
used to differentiate the grammar symbols on the two sides of a production. The
function 𝑝𝑢𝑡 updates the symbol table with the type information for an identifier.
Let P and Q be the languages specified by grammars G1 and G2, respectively.
Which of the following statements is/are true?

**Options:**

A. The languages P and Q are the same
B. SDD2 is S-attributed and contains only synthesized attributes
C. SDD1 is L-attributed and contains only inherited attributes
D. The specifications of SDD1 and SDD2 are such that the same entries get added to the symbol table

**Type:** MCQ

**Answer:** VERIFICATION REQUIRED

**Source:** GATE 2026 CS-1 (forenoon), `12-PYQ/2026/set-01/question-paper.pdf`

---

## 2025

### Q.22

**Paper:** GATE 2025 CS-2

**Question:**

Given the following syntax directed translation rules:
Rule 1: 𝑅 → 𝐴𝐵 {𝐵. 𝑖= 𝑅. 𝑖−1; 𝐴. 𝑖= 𝐵. 𝑖; 𝑅. 𝑖= 𝐴. 𝑖+ 1; }
Rule 2: 𝑃 → 𝐶𝐷 {𝑃. 𝑖= 𝐶. 𝑖+ 𝐷. 𝑖; 𝐷. 𝑖= 𝐶. 𝑖+ 2; }
Rule 3: 𝑄 → 𝐸𝐹 {𝑄. 𝑖= 𝐸. 𝑖+ 𝐹. 𝑖; }
Which ONE is the CORRECT option among the following?

**Options:**

A. Rule 1 is S-attributed and L-attributed; Rule 2 is S-attributed and not L-attributed; Rule 3 is neither S-attributed nor L-attributed
B. Rule 1 is neither S-attributed nor L-attributed; Rule 2 is S-attributed and L- attributed; Rule 3 is S-attributed and L-attributed
C. Rule 1 is neither S-attributed nor L-attributed; Rule 2 is not S-attributed and is L-attributed; Rule 3 is S-attributed and L-attributed
D. Rule 1 is S-attributed and not L-attributed; Rule 2 is not S-attributed and is L-attributed; Rule 3 is S-attributed and L-attributed

**Type:** MCQ

**Answer:** VERIFICATION REQUIRED

**Source:** GATE 2025 CS-2, `12-PYQ/2025/set-02/question-paper.pdf`

---

## 2024

### Q.37

**Paper:** GATE 2024 CS1

**Question:**

Consider the following syntax-directed definition (SDD).
𝑆→𝐷𝐻𝑇𝑈  { 𝑆. 𝑣𝑎𝑙 = 𝐷. 𝑣𝑎𝑙 + 𝐻. 𝑣𝑎𝑙 + 𝑇. 𝑣𝑎𝑙 + 𝑈. 𝑣𝑎𝑙; }
𝐷→"M"𝐷_{1}  { 𝐷. 𝑣𝑎𝑙 = 5 + 𝐷_{1}. 𝑣𝑎𝑙; }
𝐷→𝜖  { 𝐷. 𝑣𝑎𝑙 = −5; }
𝐻→"L"𝐻_{1}  { 𝐻. 𝑣𝑎𝑙 = 5 ∗10 + 𝐻_{1}. 𝑣𝑎𝑙; }
𝐻→𝜖  { 𝐻. 𝑣𝑎𝑙 = −10; }
𝑇→"C"𝑇_{1}  { 𝑇. 𝑣𝑎𝑙 = 5 ∗100 + 𝑇_{1}. 𝑣𝑎𝑙; }
𝑇→𝜖  { 𝑇. 𝑣𝑎𝑙 = −5; }
𝑈→"K"  { 𝑈. 𝑣𝑎𝑙 = 5; }
Given "MMLK" as the input, which one of the following options is the CORRECT
value computed by the SDD (in the attribute 𝑆. 𝑣𝑎𝑙)?

**Options:**

A. 45
B. 50
C. 55
D. 65

**Type:** MCQ

**Answer:** VERIFICATION REQUIRED

**Source:** GATE 2024 CS1, `12-PYQ/2024/set-01/question-paper.pdf`

---

## 2023

### Q.60

**Paper:** GATE 2023 CS

**Question:**

Consider the syntax directed translation given by the following grammar and se-
mantic rules. Here N , I, F and B are non-terminals. N is the starting non-terminal,
and #, 0 and 1 are lexical tokens corresponding to input letters “#”, “0” and “1”,
respectively. X.val denotes the synthesized attribute (a numeric value) associated
with a non-terminal X. I_{1} and F_{1} denote occurrences of I and F on the right hand
side of a production, respectively. For the tokens 0 and 1, 0.val = 0 and 1.val = 1.
N → I # F N.val = I.val + F.val
I → I_{1} B  I.val = (2 I_{1}.val ) + B.val
I → B  I.val = B.val
F → B F_{1} F.val = 12(B.val + F_{1}.val )
F → B  F.val = 12B.val
B → 0  B.val = 0.val
B → 1  B.val = 1.val
The value computed by the translation scheme for the input string
10#011
is  . (Rounded offto three decimal places)

**Options:**

The paper does not print options for this numerical-answer question.

**Type:** NAT

**Answer:** VERIFICATION REQUIRED

**Source:** GATE 2023 CS, `12-PYQ/2023/question-paper.pdf`

---

## 2020

### Q.33

**Paper:** GATE 2020 CS

**Question:**

Consider the productions A → PQ and A→ XY. Each of the five non-terminals A,
P, Q, X, and Y has two attributes: s is a synthesized attribute, and i is an inherited
attribute. Consider the following rules.
Rule 1: P.i = A.i + 2, Q.i= P.i+ A.i, and A.s = P.s + Q.s
Rule 2: X.i = A.i+ Y.s and Y.i= X.s+ A.i
Which one of the following is TRUE?

**Options:**

A. Both Rule 1 and Rule 2 are L-attributed.
B. Only Rule 1 is L-attributed. () Only Rule 2 is L-attributed.
D. Neither Rule 1 nor Rule 2 is L-attributed.

**Type:** MCQ

**Answer:** VERIFICATION REQUIRED

**Source:** GATE 2020 CS, `12-PYQ/2020/question-paper.pdf`

---

## 2016

### Q.46

**Paper:** GATE 2016 CS-1

**Question:**

Consider the following Syntax Directed Translation Scheme (SDTS), with non-terminals
{S, A} and terminals {a, b}.
S −→ aA { print 1 }
S −→ a  { print 2 }
A −→ Sb { print 3 }
Using the above SDTS, the output printed by a bottom-up parser, for the input aab is:

**Options:**

A. 1 3 2
B. 2 2 3
C. 2 3 1
D. syntax error

**Type:** MCQ

**Answer:** VERIFICATION REQUIRED

**Source:** GATE 2016 CS-1, `12-PYQ/2016/set-01/question-paper.pdf`

---
