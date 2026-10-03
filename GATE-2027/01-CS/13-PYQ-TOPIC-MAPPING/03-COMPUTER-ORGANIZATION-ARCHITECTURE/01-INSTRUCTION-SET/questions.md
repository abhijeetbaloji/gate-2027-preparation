# GATE PYQs

## 2026

### Q.15

**Paper:** GATE 2026 CS-1 (forenoon)

**Question:**

Consider a processor P whose instruction set architecture is the load-store
architecture. The instruction format is such that the first operand of any instruction
is the destination operand.
Which one of the following sequences of instructions corresponds to the high-level
language statement Z = X + Y ?
Note: X, Y, and Z are memory operands. R0, R1, and R2 are registers.

**Options:**

A. ADD Z, X, Y
B. LOAD R0, X ADD Z, R0, Y
C. ADD R0, X, Y STORE Z, R0
D. LOAD R0, X LOAD R1, Y ADD R2, R0, R1 STORE Z, R2

**Type:** MCQ

**Answer:** VERIFICATION REQUIRED

**Source:** GATE 2026 CS-1 (forenoon), `12-PYQ/2026/set-01/question-paper.pdf`

---

### Q.44

**Paper:** GATE 2026 CS-2 (afternoon)

**Question:**

Consider a processor that has 16 general purpose registers and it uses 2-byte
instruction format for all its instructions. Variable-sized opcodes are permitted.
There are three different types of instructions; M-type, R-type, and C-type. Each
M-type instruction has 2 register operands and a 6-bit immediate operand. Each R-
type instruction has 3 register operands. Each C-type instruction has a register
operand and a 6-bit offset value. If there are 2 unique M-type opcodes and 7 unique
R-type opcodes, which one of the following options gives the maximum number of
unique opcodes possible for C-type instructions?

**Options:**

A. 8
B. 4
C. 64
D. 16

**Type:** MCQ

**Answer:** VERIFICATION REQUIRED

**Source:** GATE 2026 CS-2 (afternoon), `12-PYQ/2026/set-02/question-paper.pdf`

---

## 2025

### Q.37

**Paper:** GATE 2025 CS-1

**Question:**

A processor has 64 general-purpose registers and 50 distinct instruction types. An
instruction is encoded in 32-bits. What is the maximum number of bits that can be
used to store the immediate operand for the given instruction?
ADD R1, #25  // R1 = R1 + 25

**Options:**

A. 16
B. 20
C. 22
D. 24

**Type:** MCQ

**Answer:** VERIFICATION REQUIRED

**Source:** GATE 2025 CS-1, `12-PYQ/2025/set-01/question-paper.pdf`

---

## 2024

### Q.61

**Paper:** GATE 2024 CS2

**Question:**

A processor uses a 32-bit instruction format and supports byte-addressable memory
access. The ISA of the processor has 150 distinct instructions. The instructions are
equally divided into two types, namely R-type and I-type, whose formats are shown
below.
R-type Instruction Format:
OPCODE UNUSED DST Register  SRC Register1  SRC Register 2
I-type Instruction Format:
OPCODE DST Register SRC Register # Immediate value/address
In the OPCODE, 1 bit is used to distinguish between I-type and R-type instructions
and the remaining bits indicate the operation. The processor has 50 architectural
registers, and all register fields in the instructions are of equal size.
Let 𝑋 be the number of bits used to encode the UNUSED field, 𝑌 be the number
of bits used to encode the OPCODE field, and 𝑍 be the number of bits used to
encode the immediate value/address field. The value of 𝑋+ 2𝑌+ 𝑍 is ________
Let 𝐿  be the language represented by the regular expression  𝑏^{∗}𝑎𝑏^{∗}(𝑎𝑏^{∗}𝑎𝑏^{∗})^{∗}

**Options:**

The paper does not print options for this numerical-answer question.

**Type:** NAT

**Answer:** VERIFICATION REQUIRED

**Source:** GATE 2024 CS2, `12-PYQ/2024/set-02/question-paper.pdf`

---

## 2020

### Q.44

**Paper:** GATE 2020 CS

**Question:**

A processor has 64 registers and uses 16-bit instruction format. It has two types of
instructions: I-type and R-type. Each I-type instruction contains an opcode, a
register name, and a 4-bit immediate value. Each R-type instruction contains an
opcode and two register names. If there are 8 distinct I-type opcodes, then the
maximum number of distinct R-type opcodes is

**Options:**

The paper does not print options for this numerical-answer question.

**Type:** NAT

**Answer:** VERIFICATION REQUIRED

**Source:** GATE 2020 CS, `12-PYQ/2020/question-paper.pdf`

---

## 2016

### Q.10

**Paper:** GATE 2016 CS-2

**Question:**

A processor has 40 distinct instructions and 24 general purpose registers. A 32-bit instruction
word has an opcode, two register operands and an immediate operand. The number of bits
available for the immediate operand field is  .
CS(Set B)  2/18

**Options:**

The paper does not print options for this numerical-answer question.

**Type:** NAT

**Answer:** VERIFICATION REQUIRED

**Source:** GATE 2016 CS-2, `12-PYQ/2016/set-02/question-paper.pdf`

---

### Q.31

**Paper:** GATE 2016 CS-2

**Question:**

Consider a processor with 64 registers and an instruction set of size twelve. Each instruction
has five distinct fields, namely, opcode, two source register identifiers, one destination register
identifier, and a twelve-bit immediate value. Each instruction must be stored in memory in
a byte-aligned fashion. If a program has 100 instructions, the amount of memory (in bytes)
consumed by the program text is  .

**Options:**

The paper does not print options for this numerical-answer question.

**Type:** NAT

**Answer:** VERIFICATION REQUIRED

**Source:** GATE 2016 CS-2, `12-PYQ/2016/set-02/question-paper.pdf`

---

## 2015

### Q.22

**Paper:** GATE 2015 CS, 7 February Shift 1

**Question:**

For computers based on three-address instruction formats, each address field can be used to specify
which of the following:
(S1) A memory operand
(S2) A processor register
(S3) An implied accumulator register

**Options:**

A. Either S1 or S2
B. Either S2 or S3
C. Only S2 and S3
D. All of S1, S2 and S3

**Type:** MCQ

**Answer:** VERIFICATION REQUIRED

**Source:** GATE 2015 CS, 7 February Shift 1, `12-PYQ/2015/set-01/question-paper.pdf`

---

### Q.52

**Paper:** GATE 2015 CS, 7 February Shift 2

**Question:**

Consider the C program below.
#include <stdio.h>
int *A, stkTop;
int stkFunc (int opcode, int val)
static int size=0, stkTop=0;
switch (opcode) {
case -1: size = val; break;
case 0: if (stkTop < size) A[stkToptł] = val; break;
default: if (stkTop) return Al--stkTop];
return -1;
int main ()
int B[20]; A = B; stkTop = -1;
stkFunc (-1, 10);
stkFunc ( 0, 5);
stkFunc ( 0, 10);
printf ("*d\n", stkFunc (1, 0) + stkFunc (1, 0));
The value printed by the above program is
Correct Answer :

**Options:**

The paper does not print options for this numerical-answer question.

**Type:** NAT

**Answer:** VERIFICATION REQUIRED

**Source:** GATE 2015 CS, 7 February Shift 2, `12-PYQ/2015/set-02/question-paper.pdf`

---

## 2013

### Q.48

**Paper:** GATE 2013 CS Booklet A

**Question:**

Suppose the instruction set architecture of the processor has only two registers. The only allowed
compiler optimization is code motion, which moves statements from one place to another while
preserving correctness. What is the minimum number of spills to memory in the compiled code?

**Options:**

A. 0
B. 1
C. 2
D. 3

**Type:** MCQ

**Answer:** VERIFICATION REQUIRED

**Source:** GATE 2013 CS Booklet A, `12-PYQ/2013/set-01/question-paper.pdf`

---

### Q.49

**Paper:** GATE 2013 CS Booklet A

**Question:**

What is the minimum number of registers needed in the instruction set architecture of the processor
to compile this code segment without any spill to memory? Do not apply any optimization other
than optimizing register allocation.

**Options:**

A. 3
B. 4
C. 5
D. 6 Common Data for Questions 50 and 51: The procedure given below is required to find and replace certain characters inside an input character string supplied in array A. The characters to be replaced are supplied in array oldc, while their respective replacement characters are supplied in array newc. Array A has a fixed length of five characters, while arrays oldc and newc contain three characters each. However, the procedure is flawed. void find_and_replace (char *A, char *oldc, char *newc) { for (int i=0; i<5; i++) for (int j=0; j<3; j++) if (A[i] == oldc[j]) A[i] = newc[j]; } The procedure is tested with the following four test cases. (1) oldc = “abc”, newc = “dab” (2) oldc = “cde”, newc = “bcd” (3) oldc = “bca”, newc = “cda” (4) oldc = “abc”, newc = “bac”

**Type:** MCQ

**Answer:** VERIFICATION REQUIRED

**Source:** GATE 2013 CS Booklet A, `12-PYQ/2013/set-01/question-paper.pdf`

---

### Q.50

**Paper:** GATE 2013 CS Booklet B

**Question:**

Suppose the instruction set architecture of the processor has only two registers. The only allowed
compiler optimization is code motion, which moves statements from one place to another while
preserving correctness. What is the minimum number of spills to memory in the compiled code?

**Options:**

A. 0
B. 1
C. 2
D. 3

**Type:** MCQ

**Answer:** VERIFICATION REQUIRED

**Source:** GATE 2013 CS Booklet B, `12-PYQ/2013/set-02/question-paper.pdf`

---

### Q.51

**Paper:** GATE 2013 CS Booklet B

**Question:**

What is the minimum number of registers needed in the instruction set architecture of the processor
to compile this code segment without any spill to memory? Do not apply any optimization other
than optimizing register allocation.

**Options:**

A. 3
B. 4
C. 5
D. 6 CS-B 11/20 2013COMPUTER SCIENCE & INFORMATION TECH. - CS Linked Answer Questions Statement for Linked Answer Questions 52 and 53: Relation R has eight attributes ABCDEFGH. Fields of R contain only atomic values. F={CH→G, A→BC, B→CFH, E→A, F→EG} is a set of functional dependencies (FDs) so that F^{+} is exactly the set of FDs that hold for R.

**Type:** MCQ

**Answer:** VERIFICATION REQUIRED

**Source:** GATE 2013 CS Booklet B, `12-PYQ/2013/set-02/question-paper.pdf`

---

### Q.48

**Paper:** GATE 2013 CS Booklet C

**Question:**

What is the minimum number of registers needed in the instruction set architecture of the processor
to compile this code segment without any spill to memory? Do not apply any optimization other
than optimizing register allocation.

**Options:**

A. 3
B. 4
C. 5
D. 6

**Type:** MCQ

**Answer:** VERIFICATION REQUIRED

**Source:** GATE 2013 CS Booklet C, `12-PYQ/2013/set-03/question-paper.pdf`

---

### Q.49

**Paper:** GATE 2013 CS Booklet C

**Question:**

Suppose the instruction set architecture of the processor has only two registers. The only allowed
compiler optimization is code motion, which moves statements from one place to another while
preserving correctness. What is the minimum number of spills to memory in the compiled code?

**Options:**

A. 0
B. 1
C. 2
D. 3 CS- C 11/20 2013COMPUTER SCIENCE & INFORMATION TECH. - CS Common Data for Questions 50 and 51: The procedure given below is required to find and replace certain characters inside an input character string supplied in array A. The characters to be replaced are supplied in array oldc, while their respective replacement characters are supplied in array newc. Array A has a fixed length of five characters, while arrays oldc and newc contain three characters each. However, the procedure is flawed. void find_and_replace (char *A, char *oldc, char *newc) { for (int i=0; i<5; i++) for (int j=0; j<3; j++) if (A[i] == oldc[j]) A[i] = newc[j]; } The procedure is tested with the following four test cases. (1) oldc = “abc”, newc = “dab” (2) oldc = “cde”, newc = “bcd” (3) oldc = “bca”, newc = “cda” (4) oldc = “abc”, newc = “bac”

**Type:** MCQ

**Answer:** VERIFICATION REQUIRED

**Source:** GATE 2013 CS Booklet C, `12-PYQ/2013/set-03/question-paper.pdf`

---

### Q.50

**Paper:** GATE 2013 CS Booklet D

**Question:**

What is the minimum number of registers needed in the instruction set architecture of the processor
to compile this code segment without any spill to memory? Do not apply any optimization other
than optimizing register allocation.

**Options:**

A. 3
B. 4
C. 5
D. 6

**Type:** MCQ

**Answer:** VERIFICATION REQUIRED

**Source:** GATE 2013 CS Booklet D, `12-PYQ/2013/set-04/question-paper.pdf`

---

### Q.51

**Paper:** GATE 2013 CS Booklet D

**Question:**

Suppose the instruction set architecture of the processor has only two registers. The only allowed
compiler optimization is code motion, which moves statements from one place to another while
preserving correctness. What is the minimum number of spills to memory in the compiled code?

**Options:**

A. 0
B. 1
C. 2
D. 3 CS- D 11/20 2013COMPUTER SCIENCE & INFORMATION TECH. - CS Linked Answer Questions Statement for Linked Answer Questions 52 and 53: Relation R has eight attributes ABCDEFGH. Fields of R contain only atomic values. F={CH→G, A→BC, B→CFH, E→A, F→EG} is a set of functional dependencies (FDs) so that F^{+} is exactly the set of FDs that hold for R.

**Type:** MCQ

**Answer:** VERIFICATION REQUIRED

**Source:** GATE 2013 CS Booklet D, `12-PYQ/2013/set-04/question-paper.pdf`

---
