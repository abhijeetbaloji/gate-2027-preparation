# GATE PYQs

## 2026

### Q.16

**Paper:** GATE 2026 CS-1 (forenoon)

**Question:**

Which one of the following dependencies among the register operands of different
instructions can cause a data hazard in a pipelined processor?

**Options:**

A. Read-after-read
B. Read-after-write
C. Write-after-read
D. Write-after-write

**Type:** MCQ

**Answer:** VERIFICATION REQUIRED

**Source:** GATE 2026 CS-1 (forenoon), `12-PYQ/2026/set-01/question-paper.pdf`

---

## 2025

### Q.56

**Paper:** GATE 2025 CS-2

**Question:**

Assume that there are no pipeline stalls due to branches and other hazards. The time
taken to process 1000 instructions in microseconds is __________ . (rounded off to
two decimal places)

**Options:**

The paper does not print options for this numerical-answer question.

**Type:** NAT

**Answer:** VERIFICATION REQUIRED

**Source:** GATE 2025 CS-2, `12-PYQ/2025/set-02/question-paper.pdf`

---

## 2024

### Q.30

**Paper:** GATE 2024 CS1

**Question:**

Consider a 5-stage pipelined processor with Instruction Fetch (IF), Instruction
Decode (ID), Execute (EX), Memory Access (MEM), and Register Writeback (WB)
stages. Which of the following statements about forwarding is/are CORRECT?
In a pipelined execution, forwarding means the result from a source stage of an

**Options:**

A. earlier instruction is passed on to the destination stage of a later instruction In forwarding, data from the output of the MEM stage can be passed on to the
B. input of the EX stage of the next instruction
C. Forwarding cannot prevent all pipeline stalls Forwarding does not require any extra hardware to retrieve the data from the
D. pipeline stages

**Type:** MCQ

**Answer:** VERIFICATION REQUIRED

**Source:** GATE 2024 CS1, `12-PYQ/2024/set-01/question-paper.pdf`

---

### Q.56

**Paper:** GATE 2024 CS1

**Question:**

A given program has 25% load/store instructions. Suppose the ideal CPI (cycles per
instruction) without any memory stalls is 2. The program exhibits 2% miss rate on
instruction cache and 8% miss rate on data cache. The miss penalty is 100 cycles.
The speedup (rounded off to two decimal places) achieved with a perfect cache (i.e.,
with NO data or instruction cache misses) is _________

**Options:**

The paper does not print options for this numerical-answer question.

**Type:** NAT

**Answer:** VERIFICATION REQUIRED

**Source:** GATE 2024 CS1, `12-PYQ/2024/set-01/question-paper.pdf`

---

### Q.58

**Paper:** GATE 2024 CS1

**Question:**

Consider the entries shown below in the forwarding table of an IP router. Each entry
consists of an IP prefix and the corresponding next hop router for packets whose
destination IP address matches the prefix. The notation “/N” in a prefix indicates a
subnet mask with the most significant N bits set to 1.
Prefix  Next hop router
10.1.1.0/24  R1
10.1.1.128/25  R2
10.1.1.64/26  R3
10.1.1.192/26  R4
This router forwards 20 packets each to 5 hosts. The IP addresses of the hosts are
10.1.1.16, 10.1.1.72, 10.1.1.132, 10.1.1.191, and 10.1.1.205 . The number of
packets forwarded via the next hop router R2 is _______

**Options:**

The paper does not print options for this numerical-answer question.

**Type:** NAT

**Answer:** VERIFICATION REQUIRED

**Source:** GATE 2024 CS1, `12-PYQ/2024/set-01/question-paper.pdf`

---

### Q.58

**Paper:** GATE 2024 CS2

**Question:**

A non-pipelined instruction execution unit operating at 2 GHz takes an average of
6 cycles to execute an instruction of a program P. The unit is then redesigned to
operate on a 5-stage pipeline at 2 GHz. Assume that the ideal throughput of the
pipelined unit is 1 instruction per cycle. In the execution of program P,
20% instructions incur an average of 2 cycles stall due to data hazards and
20% instructions incur an average of 3 cycles stall due to control hazards. The
speedup (rounded off to one decimal place) obtained by the pipelined design over
the non-pipelined design is _________

**Options:**

The paper does not print options for this numerical-answer question.

**Type:** NAT

**Answer:** VERIFICATION REQUIRED

**Source:** GATE 2024 CS2, `12-PYQ/2024/set-02/question-paper.pdf`

---

## 2023

### Q.33

**Paper:** GATE 2023 CS

**Question:**

Consider a 3-stage pipelined processor having a delay of 10 ns (nanoseconds),
20 ns, and 14 ns, for the first, second, and the third stages, respectively. Assume
that there is no other delay and the processor does not suffer from any pipeline
hazards. Also assume that one instruction is fetched every cycle.
The total execution time for executing 100 instructions on this processor is
ns.

**Options:**

The paper does not print options for this numerical-answer question.

**Type:** NAT

**Answer:** VERIFICATION REQUIRED

**Source:** GATE 2023 CS, `12-PYQ/2023/question-paper.pdf`

---

### Q.65

**Paper:** GATE 2023 CS

**Question:**

The forwarding table of a router is shown below.
Subnet Number Subnet Mask Interface ID
200.150.0.0  255.255.0.0  1
200.150.64.0  255.255.224.0  2
200.150.68.0  255.255.255.0  3
200.150.68.64  255.255.255.224  4
Default  0
A packet addressed to a destination address 200.150.68.118 arrives at the router.
It will be forwarded to the interface with ID  .

**Options:**

The paper does not print options for this numerical-answer question.

**Type:** NAT

**Answer:** VERIFICATION REQUIRED

**Source:** GATE 2023 CS, `12-PYQ/2023/question-paper.pdf`

---

## 2022

### Q.61

**Paper:** GATE 2022 CS

**Question:**

A processor X_{1} operating at 2 GHz has a standard 5-stage RISC instruction pipeline
having a base CPI (cycles per instruction) of one without any pipeline hazards.
For a given program P that has 30% branch instructions, control hazards incur 2
cycles stall for every branch. A new version of the processor X_{2}operating at same
clock frequency  has an additional branch predictor unit (BPU) that completely
eliminates stalls for correctly predicted branches. There is neither any savings nor
any additional stalls for wrong predictions. There are no structural hazards and data
hazards for X_{1}and X_{2}. If the BPU has a prediction accuracy of 80%, the speed up
(rounded off to two decimal places) obtained by X_{2} over X_{1} in executing
P is____________.

**Options:**

The paper does not print options for this numerical-answer question.

**Type:** NAT

**Answer:** VERIFICATION REQUIRED

**Source:** GATE 2022 CS, `12-PYQ/2022/question-paper.pdf`

---

## 2021

### Q.53

**Paper:** GATE 2021 CS Set-1

**Question:**

A five-stage pipeline has stage delays of 150, 120, 150, 160 and 140 nanoseconds.
The registers that are used between the pipeline stages have a delay of 5 nanoseconds
The total time to execute 100 independent instructions on this pipeline, assuming
there are no pipeline stalls, is - _ nanoseconds.
GATE Graduate Aptitude Test in Engineering 2021
2021 Organising Institute - IIT Bombay

**Options:**

The paper does not print options for this numerical-answer question.

**Type:** NAT

**Answer:** VERIFICATION REQUIRED

**Source:** GATE 2021 CS Set-1, `12-PYQ/2021/set-01/question-paper.pdf`

---

### Q.53

**Paper:** GATE 2021 CS Set-2

**Question:**

Consider a pipelined processor with 5 stages, Instruction Fetch (IF), Instruction
Decode (ID), Execute (EX), Memory Access (MEM), and Write Back (WB). Each stage
of the pipeline, except the EX stage, takes one cycle. Assume that the ID stage
merely decodes the instruction and the register read is performed in the EX stage.
The EX stage takes one cycle for ADD instruction and two cycles for MUL instruction.
Ignore pipeline register latencies.
Consider the following sequence of 8 instructions:
ADD, MUL, ADD, MUL, ADD, MUL, ADD, MUL
Assume that every MUL instruction is data-dependent on the ADD instruction just
MUL instruction just before it. The Speedup is defined as follows: before it and every ADD instruction (except the first ADD) is data-dependent on the
Speedup = Execution time without operand forwarding
Execution time with operand forwarding
The Speedup achieved in executing the given instruction sequence on the pipelined
processor (rounded to 2 decimal places) is -

**Options:**

The paper does not print options for this numerical-answer question.

**Type:** NAT

**Answer:** VERIFICATION REQUIRED

**Source:** GATE 2021 CS Set-2, `12-PYQ/2021/set-02/question-paper.pdf`

---

## 2020

### Q.15

**Paper:** GATE 2020 CS

**Question:**

Consider the following statements about the functionality of an IP based router.
I. A router does not modify the IP packets during forwarding.
II. It is not necessary for a router to implement any routing protocol.
III. A router should reassemble IP fragments if the MTU of the outgoing link is
larger than the size of the incoming IP packet.
Which of the above statements is/are TRUE?

**Options:**

A. 1and Il only
B. Ionly
C. Il and Ill only
D. Il only

**Type:** MCQ

**Answer:** VERIFICATION REQUIRED

**Source:** GATE 2020 CS, `12-PYQ/2020/question-paper.pdf`

---

### Q.43

**Paper:** GATE 2020 CS

**Question:**

Consider a non-pipelined processor operating at 2.5 GHz. It takes 5 clock cycles
to complete an instruction. You are going to make a 5-stage pipeline out of this
processor. Overheads associated with pipelining force you to operate the pipelined
processor at 2 GHz. In a given program, assume that 30% are memory
instructions, 60% are ALU instructions and the rest are branch instructions.
5% of the memory instructions cause stalls of 50 clock cycles each due to cache
misses and 50% of the branch instructions cause stalls of 2 cycles each. Assume
that there are no stalls associated with the execution of ALU instructions. For this
program, the speedup achieved by the pipelined processor over the non-pipelined
processor (round off to 2 decimal places) is

**Options:**

The paper does not print options for this numerical-answer question.

**Type:** NAT

**Answer:** VERIFICATION REQUIRED

**Source:** GATE 2020 CS, `12-PYQ/2020/question-paper.pdf`

---

### Q.54

**Paper:** GATE 2020 CS

**Question:**

Consider a database implemented using B+ tree for file indexing and installed on
a disk drive with block size of 4 KB. The size of search key is 12 bytes and the
size of tree/disk pointer is 8 bytes. Assume that the database has one million
records. Also assume that no node of the B+ tree and no records are present
initially in main memory. Consider that each record fits into one disk block. The
minimum number of disk accesses required to retrieve any record in the database
is

**Options:**

The paper does not print options for this numerical-answer question.

**Type:** NAT

**Answer:** VERIFICATION REQUIRED

**Source:** GATE 2020 CS, `12-PYQ/2020/question-paper.pdf`

---

## 2018

### Q.50

**Paper:** GATE 2018 CS

**Question:**

The instruction pipeline of a RISC processor has the following stages: Instruction Fetch (IF),
Instruction Decode (ID), Operand Fetch (OF), Perform Operation (PO) and Writeback (WB).
The IF, ID, OF and WB stages take 1 clock cycle each for every instruction. Consider a
sequence of 100 instructions. In the PO stage, 40 instructions take 3 clock cycles each, 35
instructions take 2 clock cycles each, and the remaining 25 instructions take 1 clock cycle
each. Assume that there are no data hazards and no control hazards.
The number of clock cycles required for completion of execution of the sequence of
instructions is ______.

**Options:**

The paper does not print options for this numerical-answer question.

**Type:** NAT

**Answer:** VERIFICATION REQUIRED

**Source:** GATE 2018 CS, `12-PYQ/2018/question-paper.pdf`

---

## 2015

### Q.55

**Paper:** GATE 2015 CS, 7 February Shift 1

**Question:**

14020

Consider a non-pipelined processor with a clock rate of 2.5 gigahertz and average cycles per
instruction of four. The same processor is upgraded to a pipelined processor with five stages; but
due to the internal pipeline delay, the clock speed is reduced to 2 gigahertz. Assume that there are
no stalls in the pipeline. The speed up achieved in this pipelined processor 1s_
Correct Answer :

**Options:**

The paper does not print options for this numerical-answer question.

**Type:** NAT

**Answer:** VERIFICATION REQUIRED

**Source:** GATE 2015 CS, 7 February Shift 1, `12-PYQ/2015/set-01/question-paper.pdf`

---

### Q.53

**Paper:** GATE 2015 CS, 7 February Shift 2

**Question:**

15

Consider the sequence of machine instructions given below:
MUL R5, RO, R1
DIV R6, R2, R3
ADD R7, R5, R6
SUB R8, R7, R4
In the above sequence, RO to R8 are general purpose registers. In the instructions shown, the first
register stores the result of the operation performed on the second and the third registers. This
sequence of instructions is to be executed in a pipelined instruction processor with the following 4
stages: (1) Instruction Fetch and Decode (IF), (2) Operand Fetch (OF), (3) Perform Operation (PO)
and (4) Write back the result (WB). The IF, OF and WB stages take 1 clock cycle each for any
instruction. The PO stage takes 1 clock cycle for ADD or SUB instruction, 3 clock cycles for MUL
instruction and 5 clock cycles for DIV instruction. The pipelined processor uses operand
forwarding from the PO stage to the OF stage. The number of clock cycles taken for the execution
of the above sequence of instructions is
Correct Answer :

**Options:**

The paper does not print options for this numerical-answer question.

**Type:** NAT

**Answer:** VERIFICATION REQUIRED

**Source:** GATE 2015 CS, 7 February Shift 2, `12-PYQ/2015/set-02/question-paper.pdf`

---

### Q.49

**Paper:** GATE 2015 CS, 8 February Shift 1

**Question:**

Consider the following code sequence having five instructions 11 to Is. Each of these instructions
has the following format.
OP Ri, Rj, Rk
where operation OP is performed on contents of registers Rj and Rk and the result is stored in
register R1.
41: ADD R1, R2, R3
12: MUL R7, R1, R3
1z: SUB R4, R1, R5
4: ADD R3, R2, R4
15: MUL R7, R8, R9
Consider the following three statements.
S1: There is an anti-dependence between instructions 12 and Is
S2: There is an anti-dependence between instructions 12 and 14
S3: Within an instruction pipeline an anti-dependence always creates one or more stalls
Which one of above statements is/are correct?

**Options:**

A. Only S1 is true
B. Only S2 1s true
C. Only S1 and S3 are true
D. Only S2 and S3 are true 4 % D

**Type:** MCQ

**Answer:** VERIFICATION REQUIRED

**Source:** GATE 2015 CS, 8 February Shift 1, `12-PYQ/2015/set-03/question-paper.pdf`

---

## 2014

### Q.43

**Paper:** GATE 2014 CS SET-1

**Question:**

Consider a 6-stage instruction pipeline, where all stages are perfectly balanced.Assume that there is
no cycle-time overhead of pipelining. When an application is executing on this 6-stage pipeline, the
speedup achieved with respect to non-pipelined execution if 25% of the instructions incur 2
pipeline stall cycles is ______________________.

**Options:**

The paper does not print options for this numerical-answer question.

**Type:** NAT

**Answer:** VERIFICATION REQUIRED

**Source:** GATE 2014 CS SET-1, `12-PYQ/2014/set-01/question-paper.pdf`

---

### Q.43

**Paper:** GATE 2014 CS SET-3

**Question:**

An instruction pipeline has five stages, namely, instruction fetch (IF), instruction decode and
register fetch (ID/RF), instruction execution (EX), memory access (MEM), and register writeback
(WB) with stage latencies 1 ns, 2.2 ns, 2 ns, 1 ns, and 0.75 ns, respectively (ns stands for
nanoseconds). To gain in terms of frequency, the designers have decided to split the ID/RF stage
into three stages (ID, RF1, RF2) each of latency 2.2/3 ns. Also, the EX stage is split into two stages
(EX1, EX2) each of latency 1 ns. The new design has a total of eight pipeline stages. A program
has 20% branch instructions which execute in the EX stage and produce the next instruction pointer
at the end of the EX stage in the old design and at the end of the EX2 stage in the new design. The
IF stage stalls after fetching a branch instruction until the next instruction pointer is computed. All
instructions other than the branch instruction have an average CPI of one in both the designs. The
execution times of this program on the old and the new design are  P and  Q nanoseconds,
respectively. The value of P/Q is __________.

**Options:**

The paper does not print options for this numerical-answer question.

**Type:** NAT

**Answer:** VERIFICATION REQUIRED

**Source:** GATE 2014 CS SET-3, `12-PYQ/2014/set-03/question-paper.pdf`

---

## 2012

### Q.20

**Paper:** GATE 2012 CS Booklet A

**Question:**

Register renaming is done in pipelined processors

**Options:**

A. as an alternative to register allocation at compile time
B. for efficient access to function parameters and local variables
C. to handle certain kinds of hazards
D. as part of address translation

**Type:** MCQ

**Answer:** VERIFICATION REQUIRED

**Source:** GATE 2012 CS Booklet A, `12-PYQ/2012/question-paper.pdf`

---

## 2009

### Q.60

**Paper:** GATE 2009 CS

**Question:**

What is the content of the array after two delete operations on the correct answer to the previous
question ?

**Options:**

A. { 14, 13, 12, 10, 8 }
B. ( 14, 12, 13, 8, 10 }
C. { 14, 13, 8, 12, 10 )
D. { 14, 13, 12, 8, 10 } 1ốc byu cà xuoĐa càs vads0r 2083 16529 Uiv bsan al losalpig Wabm nohitan stt stall monnim sil 2i loloula hosalo udl yil

**Type:** MCQ

**Answer:** VERIFICATION REQUIRED

**Source:** GATE 2009 CS, `12-PYQ/2009/question-paper.pdf`

---

## 2008

### Q.36

**Paper:** GATE 2008 CS

**Question:**

Which of the following are NOT true in a pipelined processor?
I. Bypassing can handle all RAW hazards.
II. Register renaming can eliminate all register carried WAR hazards.
III. Control hazard penalties can be eliminated by dynamic branch prediction.

**Options:**

A. I and II only
B. I and IIl only
C. II and IIl only
D. I,Il and lil

**Type:** MCQ

**Answer:** VERIFICATION REQUIRED

**Source:** GATE 2008 CS, `12-PYQ/2008/question-paper.pdf`

---

### Q.75

**Paper:** GATE 2008 CS

**Question:**

£1 (8) and f2 (8) return the values

**Options:**

A. 1661 and 1640
B. 59 and 59
C. 1640 and 1640
D. 1640 and 1661 Linked Answer Questions: Q.76 to Q.85 carry two marks each. Statement for Linked Answer Questions 76 and 77: Delayed branching can help in the handling of control hazards.

**Type:** MCQ

**Answer:** VERIFICATION REQUIRED

**Source:** GATE 2008 CS, `12-PYQ/2008/question-paper.pdf`

---

## 2007

### Q.37

**Paper:** GATE 2007 CS

**Question:**

Consider a pipelined processor with the following four stages:
IF: Instruction Fetch
ID: Instruction Decode and Operand Fetch
EX: Execute
WB: Write Back
The IF, ID and WB stages take one clock cycle each to complete the operation. The
number of clock cycles for the EX stage depends on the instruction. The ADD and
SUB instructions need 1 clock cycle and the MUL instruction needs 3 clock cycles in
the EX stage. Operand forwarding is used in the pipelined processor. What is the
number of clock cycles taken to complete the following sequence of instructions?
ADD R2, RI, RO R2 < R1 + RO
MUL R4, R3, R2 R4 < R3 * R2
SUB R6, R5, R4 R6 < R5 - R4

**Options:**

A. 7
B. 8
C. 10
D. 14

**Type:** MCQ

**Answer:** VERIFICATION REQUIRED

**Source:** GATE 2007 CS, `12-PYQ/2007/question-paper.pdf`

---
