# GATE PYQs

## 2026

### Q.42

**Paper:** GATE 2026 CS-1 (forenoon)

**Question:**

Consider the control flow graph shown in the figure.
Which one of the following options correctly lists the set of redundant expressions
(common subexpressions) in the basic blocks B4 and B5?
Note: All the variables are integers.

**Options:**

A. B4: { 𝑏+ 𝑖 } B5: { 𝑐+ 𝑚 }
B. B4: { 𝑔 ∗ 𝑘 } B5: { 𝑐+ 𝑚 }
C. B4: { 𝑔 ∗ 𝑘, 𝑏+ 𝑖 } B5: { }
D. B4: { 𝑔 ∗ 𝑘 } B5: { }

**Type:** MCQ

**Answer:** VERIFICATION REQUIRED

**Source:** GATE 2026 CS-1 (forenoon), `12-PYQ/2026/set-01/question-paper.pdf`

---

## 2021

### Q.30

**Paper:** GATE 2021 CS Set-2

**Question:**

Consider the following ANSI C code segment:
z = x + 3 + y->f1 + y->f2;
for (i = 0; i < 200; i = i + 2){
if (z > i) {
P = p+ x + 3;
q = q + y->f1;
} else {
P = p + y->f2;
q= q + x + 3;
}
}
Assume that the variable y points to a struct (allocated on the heap) containing
two fields f1 and f2, and the local variables x, y, z, P, q, and i are allotted
registers. Common sub-expression elimination (CSE) optimization is applied on
the code. The number of addition and dereference operations (of the form y->f1
or y->f2 ) in the optimized code, respectively, are:

**Options:**

A. 403 and 102
B. 203 and 2
C. 303 and 102
D. 303 and 2 GATE Graduate Aptitude Test in Engineering 2021 2021 Organising Institute - IIT Bombay

**Type:** MCQ

**Answer:** VERIFICATION REQUIRED

**Source:** GATE 2021 CS Set-2, `12-PYQ/2021/set-02/question-paper.pdf`

---
