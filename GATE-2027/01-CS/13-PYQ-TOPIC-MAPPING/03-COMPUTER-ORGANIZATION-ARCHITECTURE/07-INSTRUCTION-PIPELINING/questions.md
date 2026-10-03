# GATE PYQs

## 2025

### Q.61

**Paper:** GATE 2025 CS-2

**Question:**

An application executes 6.4 × 10^{8} number of instructions in 6.3 seconds. There are
four types of instructions, the details of which are given in the table. The duration
of a clock cycle in nanoseconds is _________. (rounded off to one decimal place)
Instruction type  Clock cycles required per  Number of instructions
instruction (CPI)  executed
Branch  2  2.25 × 10^{8}
Load  5  1.20 × 10^{8}
Store  4  1.65 × 10^{8}
Arithmetic  3  1.30 × 10^{8}

**Options:**

The paper does not print options for this numerical-answer question.

**Type:** NAT

**Answer:** VERIFICATION REQUIRED

**Source:** GATE 2025 CS-2, `12-PYQ/2025/set-02/question-paper.pdf`

---

## 2024

### Q.31

**Paper:** GATE 2024 CS2

**Question:**

An instruction format has the following structure:
Instruction Number: Opcode destination reg, source reg-1, source reg-2
Consider the following sequence of instructions to be executed in a pipelined
processor:
I1: DIV R3, R1, R2
I2: SUB R5, R3, R4
I3: ADD R3, R5, R6
I4: MUL R7, R3, R8
Which of the following statements is/are TRUE?

**Options:**

A. There is a RAW dependency on R3 between I1 and I2
B. There is a WAR dependency on R3 between I1 and I3
C. There is a RAW dependency on R3 between I2 and I3
D. There is a WAW dependency on R3 between I3 and I4

**Type:** MCQ

**Answer:** VERIFICATION REQUIRED

**Source:** GATE 2024 CS2, `12-PYQ/2024/set-02/question-paper.pdf`

---

## 2016

### Q.32

**Paper:** GATE 2016 CS-1

**Question:**

The stage delays in a 4-stage pipeline are 800, 500, 400 and 300 picoseconds. The first
stage (with delay 800 picoseconds) is replaced with a functionally equivalent design involving
two stages with respective delays 600 and 350 picoseconds. The throughput increase of the
pipeline is  percent.

**Options:**

The paper does not print options for this numerical-answer question.

**Type:** NAT

**Answer:** VERIFICATION REQUIRED

**Source:** GATE 2016 CS-1, `12-PYQ/2016/set-01/question-paper.pdf`

---

### Q.33

**Paper:** GATE 2016 CS-2

**Question:**

Consider a 3 GHz (gigahertz) processor with a three-stage pipeline and stage latencies τ_{1},
τ_{2}, and τ_{3} such that τ_{1} = 3τ_{2}/4 = 2τ_{3}. If the longest pipeline stage is split into two pipeline
stages of equal latency, the new frequency is  GHz, ignoring delays in the pipeline
registers.

**Options:**

The paper does not print options for this numerical-answer question.

**Type:** NAT

**Answer:** VERIFICATION REQUIRED

**Source:** GATE 2016 CS-2, `12-PYQ/2016/set-02/question-paper.pdf`

---

## 2015

### Q.48

**Paper:** GATE 2015 CS, 8 February Shift 1

**Question:**

Consider the following reservation table for a pipeline having three stages S1, S2 and S3.
Time →
2 3 4 5
The minimum average latency (MAL) is
Correct Answer :

**Options:**

The paper does not print options for this numerical-answer question.

**Type:** NAT

**Answer:** VERIFICATION REQUIRED

**Source:** GATE 2015 CS, 8 February Shift 1, `12-PYQ/2015/set-03/question-paper.pdf`

---

## 2014

### Q.55

**Paper:** GATE 2014 CS SET-1

**Question:**

Consider two processors ܲ_{ଵ}and ܲ_{ଶ} executing the same instruction set. Assume that under identical
conditions, for the same input, a program running on ܲ_{ଶ} takes 25% less time but incurs 20% more
CPI (clock cycles per instruction) as compared to the program running on ܲ_{ଵ}. If the clock frequency
of ܲ_{ଵ} is 1GHz, then the clock frequency of ܲ_{ଶ} (in GHz) is _________.

**Options:**

The paper does not print options for this numerical-answer question.

**Type:** NAT

**Answer:** VERIFICATION REQUIRED

**Source:** GATE 2014 CS SET-1, `12-PYQ/2014/set-01/question-paper.pdf`

---

### Q.9

**Paper:** GATE 2014 CS SET-3

**Question:**

Consider the following processors (ns stands for nanoseconds). Assume that the pipeline registers
have zero latency.
P1: Four-stage pipeline with stage latencies 1 ns, 2 ns, 2 ns, 1 ns.
P2: Four-stage pipeline with stage latencies 1 ns, 1.5 ns, 1.5 ns, 1.5 ns.
P3: Five-stage pipeline with stage latencies 0.5 ns, 1 ns, 1 ns, 0.6 ns, 1 ns.
P4: Five-stage pipeline with stage latencies 0.5 ns, 0.5 ns, 1 ns, 1 ns, 1.1 ns.
Which processor has the highest peak clock frequency?

**Options:**

A. P1
B. P2
C. P3
D. P4

**Type:** MCQ

**Answer:** VERIFICATION REQUIRED

**Source:** GATE 2014 CS SET-3, `12-PYQ/2014/set-03/question-paper.pdf`

---

## 2013

### Q.45

**Paper:** GATE 2013 CS Booklet A

**Question:**

Consider an instruction pipeline with five stages without any branch prediction: Fetch Instruction
(FI), Decode Instruction (DI), Fetch Operand (FO), Execute Instruction (EI) and Write Operand
(WO). The stage delays for FI, DI, FO, EI and WO are 5 ns, 7 ns, 10 ns, 8 ns and 6 ns, respectively.
There are intermediate storage buffers after each stage and the delay of each buffer is 1 ns. A
program consisting of 12 instructions I_{1}, I_{2}, I_{3}, …, I_{12} is executed in this pipelined processor.
Instruction I_{4} is the only branch instruction and its branch target is I_{9}. If the branch is taken during
the execution of this program, the time (in ns) needed to complete the program is

**Options:**

A. 132
B. 165
C. 176
D. 328

**Type:** MCQ

**Answer:** VERIFICATION REQUIRED

**Source:** GATE 2013 CS Booklet A, `12-PYQ/2013/set-01/question-paper.pdf`

---

### Q.28

**Paper:** GATE 2013 CS Booklet B

**Question:**

Consider an instruction pipeline with five stages without any branch prediction: Fetch Instruction
(FI), Decode Instruction (DI), Fetch Operand (FO), Execute Instruction (EI) and Write Operand
(WO). The stage delays for FI, DI, FO, EI and WO are 5 ns, 7 ns, 10 ns, 8 ns and 6 ns, respectively.
There are intermediate storage buffers after each stage and the delay of each buffer is 1 ns. A
program consisting of 12 instructions I_{1}, I_{2}, I_{3}, …, I_{12} is executed in this pipelined processor.
Instruction I_{4} is the only branch instruction and its branch target is I_{9}. If the branch is taken during
the execution of this program, the time (in ns) needed to complete the program is

**Options:**

A. 132
B. 165
C. 176
D. 328

**Type:** MCQ

**Answer:** VERIFICATION REQUIRED

**Source:** GATE 2013 CS Booklet B, `12-PYQ/2013/set-02/question-paper.pdf`

---

### Q.39

**Paper:** GATE 2013 CS Booklet C

**Question:**

Consider an instruction pipeline with five stages without any branch prediction: Fetch Instruction
(FI), Decode Instruction (DI), Fetch Operand (FO), Execute Instruction (EI) and Write Operand
(WO). The stage delays for FI, DI, FO, EI and WO are 5 ns, 7 ns, 10 ns, 8 ns and 6 ns, respectively.
There are intermediate storage buffers after each stage and the delay of each buffer is 1 ns. A
program consisting of 12 instructions I_{1}, I_{2}, I_{3}, …, I_{12} is executed in this pipelined processor.
Instruction I_{4} is the only branch instruction and its branch target is I_{9}. If the branch is taken during
the execution of this program, the time (in ns) needed to complete the program is

**Options:**

A. 132
B. 165
C. 176
D. 328

**Type:** MCQ

**Answer:** VERIFICATION REQUIRED

**Source:** GATE 2013 CS Booklet C, `12-PYQ/2013/set-03/question-paper.pdf`

---

### Q.33

**Paper:** GATE 2013 CS Booklet D

**Question:**

Consider an instruction pipeline with five stages without any branch prediction: Fetch Instruction
(FI), Decode Instruction (DI), Fetch Operand (FO), Execute Instruction (EI) and Write Operand
(WO). The stage delays for FI, DI, FO, EI and WO are 5 ns, 7 ns, 10 ns, 8 ns and 6 ns, respectively.
There are intermediate storage buffers after each stage and the delay of each buffer is 1 ns. A
program consisting of 12 instructions I_{1}, I_{2}, I_{3}, …, I_{12} is executed in this pipelined processor.
Instruction I_{4} is the only branch instruction and its branch target is I_{9}. If the branch is taken during
the execution of this program, the time (in ns) needed to complete the program is

**Options:**

A. 132
B. 165
C. 176
D. 328

**Type:** MCQ

**Answer:** VERIFICATION REQUIRED

**Source:** GATE 2013 CS Booklet D, `12-PYQ/2013/set-04/question-paper.pdf`

---

## 2011

### Q.28

**Paper:** GATE 2011 CS Booklet A

**Question:**

2011
On a non-pipelined sequential processor, a program segment, which is a part of the interrupt service
routine, is given to transfer 500 bytes from an I/O device to memory.
Initialize the address register
Initialize the count to 500
LOOP: Load a byte from device
Store in memory at address given by address register
Increment the address register
Decrement the count
If count != 0 go to LOOP
Assume that each statement in this program is equivalent to a machine instruction which takes one
clock cycle to execute if it is a non-load/store instruction. The load-store instructions take two clock
cycles to execute.
The designer of the system also has an alternate approach of using the DMA controller to
implement the same transfer. The DMA controller requires 20 clock cycles for initialization and
other overheads. Each DMA transfer cycle takes two clock cycles to transfer one byte of data from
the device to the memory.
What is the approximate speedup when the DMA controller based design is used in place of the
interrupt driven program based input-output?
(А) 3.4 (B) 4.4 (C) 5.1 (D) 6.7

**Options:**

The paper does not print options for this numerical-answer question.

**Type:** NAT

**Answer:** VERIFICATION REQUIRED

**Source:** GATE 2011 CS Booklet A, `12-PYQ/2011/question-paper.pdf`

---

### Q.41

**Paper:** GATE 2011 CS Booklet A

**Question:**

Consider an instruction pipeline with four stages (S1, S2, S3 and S4) each with combinationa
Delays for thtehtages ind for the plarth ne reie rsave as giceh singe and at the end of the last slage.
Pipeline Register (Delay 1ns) Pipeline Register (Delay 1ns) Pipeline Register (Delay 1ns) Pipeline Register (Delay 1ns)
Stage Stage Stage Stage
S1 → Delay •S2 S3 Delay S4
Delay Delay
5ns 6ns 11ns 8ns
What is the approximate speed up of the pipeline in steady state under ideal conditions when
compared to the corresponding non-pipeline implementation?

**Options:**

A. 4.0
B. 2.5
C. 1.1
D. 3.0

**Type:** MCQ

**Answer:** VERIFICATION REQUIRED

**Source:** GATE 2011 CS Booklet A, `12-PYQ/2011/question-paper.pdf`

---

## 2009

### Q.28

**Paper:** GATE 2009 CS

**Question:**

Consider a 4 stage pipeline processor. The number of cycles needed by the four instructions I1, I2,
I3, 14 in stages S1, S2, S3, S4 is shown below :
S1 S2 S3 S4
I1 2 1 1
12 3
I3
I4 1 2 2 2
What is the number of cycles needed to execute the following loop ?
for (i = 1 to 2) (I1; 12; I3; I4;)

**Options:**

A. 16
B. 23
C. 28
D. 30

**Type:** MCQ

**Answer:** VERIFICATION REQUIRED

**Source:** GATE 2009 CS, `12-PYQ/2009/question-paper.pdf`

---

## 2008

### Q.38

**Paper:** GATE 2008 CS

**Question:**

In an instruction execution pipeline, the earliest that the data TLB (Translation Lookaside Buffer)
can be accessed is

**Options:**

A. before effective address calculation has started
B. during effective address calculation
C. after effective address calculation has completed
D. after data cache lookup has completed

**Type:** MCQ

**Answer:** VERIFICATION REQUIRED

**Source:** GATE 2008 CS, `12-PYQ/2008/question-paper.pdf`

---

### Q.77

**Paper:** GATE 2008 CS

**Question:**

The following code is to run on a pipelined processor with one branch delay slot:
I1: ADD R2 < R7 + R8
12: SUB R4 < R5-R6
13: ADD R1 < R2 + R3
14: STORE Memory[R4] < R1
BRANCH to Label if R1 == 0
Which of the instructions I1, 12, I3 or 14 can legitimately occupy the delay slot without any other
program modification?

**Options:**

A. II
B. 12
C. I3
D. 14 Statement for Linked Answer Questions 78 and 79: Let x„ denote the number of binary strings of length n that contain no consecutive Os.

**Type:** MCQ

**Answer:** VERIFICATION REQUIRED

**Source:** GATE 2008 CS, `12-PYQ/2008/question-paper.pdf`

---
