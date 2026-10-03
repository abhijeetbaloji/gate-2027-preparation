# GATE PYQs

## 2026

### Q.45

**Paper:** GATE 2026 CS-2 (afternoon)

**Question:**

Consider the control flow graph given below.
Which one of the following options is the set of live variables at the exit point of
each basic block?

**Options:**

A. B1:{a, b, c, e, f}, B2:{d, e}, B3:{b, c, e, f}, B4:∅
B. B1:∅, B2:{d, e}, B3:{a, c, f}, B4:∅
C. B1:{a, b, c, e, f}, B2:{d, e}, B3:{c, e, f}, B4:∅
D. B1:∅, B2:{d, e, f}, B3:{a, b, c, e, f}, B4:∅

**Type:** MCQ

**Answer:** VERIFICATION REQUIRED

**Source:** GATE 2026 CS-2 (afternoon), `12-PYQ/2026/set-02/question-paper.pdf`

---

## 2023

### Q.37

**Paper:** GATE 2023 CS

**Question:**

Consider the control flow graph shown.
ENTRY
B1
i = m − 1
j = n
a = 10
B2
i = i + 1
j = j − 1
B3
a = 20
B4
i = a + 1
EXIT
Which one of the following choices correctly lists the set of live variables at the exit
point of each basic block?

**Options:**

A. B1: {}, B2: {a}, B3: {a}, B4: {a}
B. B1: {i, j}, B2: {a}, B3: {a}, B4: {i}
C. B1: {a, i, j}, B2: {a, i, j}, B3: {a, i}, B4: {a}
D. B1: {a, i, j}, B2: {a, j}, B3: {a, j}, B4: {a, i, j}

**Type:** MCQ

**Answer:** VERIFICATION REQUIRED

**Source:** GATE 2023 CS, `12-PYQ/2023/question-paper.pdf`

---

## 2021

### Q.38

**Paper:** GATE 2021 CS Set-2

**Question:**

For a statement S in a program, in the context of liveness analysis, the following
sets are defined:
USE(S) : the set of variables used in S
IN (S) : the set of variables that are live at the entry of S
OUT(S) : the set of variables that are live at the exit of S
Consider a basic block that consists of two statements, S1 followed by S2.
Which one of the following statements is correct?

**Options:**

A. OUT (S1) = IN (S2)
B. OUT(SI) = IN(SI) U USE(S1)
C. OUT (S1) = IN (S2) U OUT(S2)
D. OUT (S1) = USE (S1) U IN(S2)

**Type:** MCQ

**Answer:** VERIFICATION REQUIRED

**Source:** GATE 2021 CS Set-2, `12-PYQ/2021/set-02/question-paper.pdf`

---

## 2014

### Q.17

**Paper:** GATE 2014 CS SET-1

**Question:**

Which one of the following is FALSE?

**Options:**

A. A basic block is a sequence of instructions where control enters the sequence at the beginning and exits at the end.
B. Available expression analysis can be used for common subexpression elimination.
C. Live variable analysis can be used for dead code elimination.
D. ݔ= 4 ∗5 ⇒ݔ= 20 is an example of common subexpression elimination.

**Type:** MCQ

**Answer:** VERIFICATION REQUIRED

**Source:** GATE 2014 CS SET-1, `12-PYQ/2014/set-01/question-paper.pdf`

---
