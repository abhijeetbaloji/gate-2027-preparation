# GATE PYQs

## 2012

### Q.36

**Paper:** GATE 2012 CS Booklet A

**Question:**

Consider the program given below, in a block-structured pseudo-language with lexical scoping and
nesting of procedures permitted.
Program main;
Var ...
Procedure A1;
Var ...
Call A2;
End A1
Procedure A2;
Var ...
Procedure A21;
Var ...
Call A1;
End A21
Call A21;
End A2
Call A1;
End main.
Consider the calling chain: Main  A1  A2  A21  A1
The correct set of activation records along with their access links is given by

**Options:**

B. Main Main A1 A1 A2 A2 A21 A21 A1 A1 FRAME ACCESS FRAME ACCESS POINTER LINKS POINTER LINKS
D. Main Main FRAME A1 A1 POINTER A2 A2 A21 A21 ACCESS LINKS A1 FRAME ACCESS POINTER LINKS CS-A 9/20 2012 COMPUTER SCIENCE & INFORMATION TECH. – CS

**Type:** MCQ

**Answer:** VERIFICATION REQUIRED

**Source:** GATE 2012 CS Booklet A, `12-PYQ/2012/question-paper.pdf`

---
