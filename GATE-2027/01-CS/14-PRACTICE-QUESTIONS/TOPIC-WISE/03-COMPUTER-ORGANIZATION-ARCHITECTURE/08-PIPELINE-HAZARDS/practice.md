# Pipeline Hazards — Practice Questions

Original practice for GATE CS. These questions are not from any GATE paper. Attempt the questions before reading the solutions.

The pipeline in the numerical questions has stages IF, ID, EX, MEM, and WB. Separate instruction and data memories are used unless a question says there is one memory port. A stall-free run of \(N\) instructions takes \(5 + N - 1\) cycles, and every stated stall is added to that total.

## Level 1 — Conceptual

## Q1 — MCQ

Which dependence is a read-after-write data hazard?

A. A later instruction reads a register that an earlier instruction writes  
B. A later instruction writes a register that an earlier instruction only reads  
C. Two instructions read the same register  
D. An adder produces a carry into the next bit

---

## Q2 — MCQ

A control hazard is caused by

A. a branch or jump whose next PC is not yet known  
B. two instructions that both need the register file’s read port in different cycles  
C. a register read with no dependence  
D. a capacity miss in a fully associative cache

---

## Q3 — MCQ

A write-after-read dependence is

A. a later read of a register written earlier  
B. a later write of a register that an earlier instruction reads  
C. two writes of different registers  
D. a taken branch with a filled delay slot

---

## Q4 — MCQ

Splitting one memory port into an instruction memory and a data memory removes which hazard in a 5-stage pipeline?

A. The structural hazard between IF and MEM  
B. Every RAW hazard  
C. Every control hazard  
D. A write-after-write hazard on the register file

---

## Level 2 — Standard GATE Style

## Q5 — NAT

There is no forwarding. The register file writes in the first half of WB and reads in the second half of ID, so a consumer can read a register in the same cycle its producer writes it. Four ALU instructions form a chain: each of the last three reads the register written by the instruction immediately before it. Each back-to-back dependence inserts 2 stall cycles. How many cycles does the chain take?

---

## Q6 — MCQ

Full forwarding from the EX and MEM results into EX is available. An ADD writes `R1`, and the next instruction is a dependent ADD that reads `R1`. How many stall cycles does that dependence insert?

A. 0  
B. 1  
C. 2  
D. 3

---

## Q7 — NAT

Forwarding into EX is available. A load value can be used by the immediately following instruction only after a 1-cycle load-use stall. ALU results forward with no stall. The committed sequence is

```
LOAD R1, 0(R2)
ADD  R3, R1, R4
SUB  R5, R3, R6
OR   R7, R8, R9
```

`OR` is independent. How many cycles does this sequence take?

---

## Q8 — MSQ

Select all that apply to a simple in-order 5-stage pipeline.

A. Forwarding reduces RAW stalls on ALU results.  
B. Forwarding does not, by itself, choose the correct PC after a branch.  
C. One memory port shared by IF and MEM can cause a structural hazard.  
D. If every register write occurs in WB and instructions write in program order, a WAW pair does not need a stall to preserve that order.

---

## Q9 — MCQ

The pipeline predicts that branches are not taken, and a taken branch is resolved at the end of EX. The pipeline is full, and the branch itself is not stalled. How many already fetched instructions are flushed?

A. 0  
B. 1  
C. 2  
D. 3

---

## Level 3 — Multi-Step

## Q10 — NAT

Use forwarding into EX, a 1-cycle penalty when a use immediately follows a load, and no penalty for an ALU dependence. Predict not-taken. A taken branch resolved at the end of EX costs 2 stall cycles when the instructions behind it are flushed. The committed sequence is

```
ADD  R1, R2, R3
SUB  R4, R1, R5
LOAD R6, 0(R4)
ADD  R7, R6, R8
BEQ  R7, R0, target     ; taken
OR   R9, R7, R8         ; target
```

There is no structural hazard. How many cycles are required until `OR` completes WB?

---

## Q11 — MCQ

The pipeline has one memory port. Every load or store therefore collides with a later instruction’s IF and inserts 1 structural stall. Loads and stores are 25 percent of instructions. There are no other stalls. The CPI is

A. 1  
B. 1.25  
C. 1.5  
D. 2

---

## Q12 — NAT

Branches are 20 percent of instructions. The pipeline has no branch predictor that avoids the penalty, and every branch costs 3 stall cycles. There are no other stalls. The effective CPI, with ideal base CPI 1, is ______.

---

## Q13 — MSQ

Forwarding is present, so a use immediately after a load costs one stall, while an independent instruction between them removes that stall. The program is

```
LOAD R1, 0(R2)
ADD  R3, R1, R4
SUB  R5, R6, R7
OR   R8, R5, R9
```

Select all that apply.

A. As written, `ADD` causes a 1-cycle load-use stall.  
B. Moving `SUB` to the position between `LOAD` and `ADD` removes that stall.  
C. `OR` reads `R5`, so it must remain after `SUB`.  
D. That move changes the value computed by `ADD`.

---

## Level 4 — Tricky / Trap-Based

## Q14 — NAT

Forwarding is present. A use in the instruction immediately after a load costs 1 stall; one independent instruction between a load and its use costs 0. ALU dependences cost 0. The branch is not taken and is resolved in EX, so it adds no stall under predict-not-taken. The committed sequence is

```
LOAD R1, 0(R2)
ADD  R3, R1, R4
LOAD R5, 0(R3)
SUB  R6, R7, R8
AND  R9, R5, R6
BEQ  R9, R0, skip       ; not taken
OR   R10, R9, R1
XOR  R11, R10, R6
```

How many cycles does the sequence take?

---

## Q15 — MCQ

The pipeline has one branch delay slot. Branches are 15 percent of instructions. The compiler fills the slot with a useful independent instruction 70 percent of the time; otherwise the slot is a NOP and costs 1 extra cycle. No other stalls occur. The CPI is

A. 1  
B. 1.045  
C. 1.15  
D. 1.30

---

## Q16 — NAT

The ideal CPI is 1 and the clock is 2 GHz. Thirty percent of instructions are loads, and 40 percent of those loads are followed immediately by a use that stalls for 1 cycle. Branches are 20 percent of instructions and each costs 2 stall cycles. There are no other stalls. A program of \(10^{9}\) instructions takes how many milliseconds?

---

## Level 5 — Challenge

## Q17 — NAT

Forwarding into EX is available. A load-use stall of 1 cycle occurs only when the next instruction uses the loaded register. An independent instruction between the load and the use removes it. ALU forwarding has no stall. Predict not-taken, and a taken branch resolved at the end of EX fetches its target on the next cycle, adding a 2-cycle penalty when two wrong-path fetches are flushed. The committed instructions are

```
ADD  R1, R2, R3
LOAD R4, 0(R1)
SUB  R5, R8, R9
AND  R6, R4, R5
BEQ  R6, R0, target     ; taken
OR   R7, R6, R1         ; target
XOR  R8, R7, R2
```

How many cycles elapse until `XOR` completes WB?

---

## Q18 — MSQ

Select all that apply to the 5-stage pipeline used above.

A. Separate instruction and data memories remove the IF/MEM structural hazard.  
B. Forwarding does not remove the one-cycle stall when the instruction immediately after a load uses the loaded value.  
C. An independent instruction scheduled between that load and its use can remove the stall.  
D. Under predict-not-taken, resolving a branch in ID flushes fewer instructions than resolving it in EX.

## Answer Key

| Q | Type | Answer |
|---|------|--------|
| 1 | MCQ | A |
| 2 | MCQ | A |
| 3 | MCQ | B |
| 4 | MCQ | A |
| 5 | NAT | 14 |
| 6 | MCQ | A |
| 7 | NAT | 9 |
| 8 | MSQ | A, B, C, D |
| 9 | MCQ | C |
| 10 | NAT | 13 |
| 11 | MCQ | B |
| 12 | NAT | 1.6 |
| 13 | MSQ | A, B, C |
| 14 | NAT | 13 |
| 15 | MCQ | B |
| 16 | NAT | 760 |
| 17 | NAT | 13 |
| 18 | MSQ | A, B, C, D |

## Detailed Solutions

### Q1

Answer: A

Read-after-write means the reader needs the value that the earlier writer has not yet produced. Write-after-read is the opposite order. Two reads do not create a data hazard. A carry is an adder signal, not an instruction dependence.

### Q2

Answer: A

A branch or jump changes the PC, but the target or the condition may be unknown when the next instruction would be fetched. That is a control hazard. A cache capacity miss is a memory-hierarchy stall, not the definition of a control hazard.

### Q3

Answer: B

Write-after-read means an earlier instruction must read the old value before a later instruction overwrites it. The RAW case is the later read. A delay slot is a control-hazard technique, not a name for WAR.

### Q4

Answer: A

IF and MEM both need memory in the same cycle when the pipeline is full and a load or store is in MEM. Separate memories remove that structural collision. They do not remove RAW dependences or uncertainty about a branch PC.

### Q5

Answer: 14

Without forwarding, the consumer’s ID must line up with the producer’s WB. In a 5-stage pipe that separation is two bubbles for every back-to-back ALU dependence. Three dependences insert \(3 \times 2 = 6\) stalls.

\[
5 + 4 - 1 + 6 = 14
\]

Cycle check, writing the stage that holds each instruction:

| Cycle | What happens |
|---|---|
| 1–3 | I1 moves IF, ID, EX |
| 3–5 | I2 is held in ID until I1 is in WB on cycle 5; I2 reads it there |
| 6 | I2 enters EX |
| 6–8 | I3 waits in ID until I2 reaches WB |
| 9 | I3 enters EX |
| 9–11 | I4 waits until I3 reaches WB |
| 12–14 | I4 finishes EX, MEM, and WB |

I4 completes on cycle 14.

### Q6

Answer: A

The first ADD produces its result at the end of EX. Forwarding sends that result to the second ADD, which is in EX on the next cycle. The instructions stay one cycle apart, so the dependence inserts 0 stalls.

### Q7

Answer: 9

The ADD immediately uses the load, so it contributes 1 stall. SUB reads the ADD result and receives it by forwarding, for 0 stalls. OR is independent.

\[
5 + 4 - 1 + 1 = 9
\]

The load is in MEM while the ADD is held in ID for the extra cycle. On the next cycle the load is in WB and the ADD is in EX, which is the forwarding window. SUB then uses the ADD result one cycle later, with no further stall. OR finishes WB two cycles after SUB, on cycle 9.

### Q8

Answer: A, B, C, D

Forwarding covers ALU RAW hazards whose result exists before WB, but a branch still needs a PC decision. A single memory cannot serve IF and MEM together. In-order WB means the later write happens later, so a pure WAW pair does not need an extra stall in this pipeline. The compiler, not an extra ALU, is what fills a delay slot with a safe instruction. E is false.

### Q9

Answer: C

While the branch moves IF, then ID, then EX, the next two sequential instructions are fetched. The decision is known at the end of EX, so those two are flushed and the target is fetched on the following cycle. The penalty is 2.

### Q10

Answer: 13

Dependences:

- SUB reads R1 from ADD: ALU forwarding, 0 stalls.
- LOAD uses R4 as an address from SUB: forwarding into EX, 0 stalls.
- The second ADD reads R6 from the load and is the next instruction: 1 load-use stall.
- BEQ reads R7 from that ADD: ALU forwarding, 0 stalls.
- BEQ is taken and resolved in EX: 2 penalty cycles.
- OR is the target, fetched after the redirect.

\[
5 + 6 - 1 + 1 + 2 = 13
\]

The load-use bubble is inserted while the load moves through MEM, before `BEQ` reaches EX. The taken branch is resolved at the end of EX and only then fetches `OR`, so the 2-cycle penalty comes after the load-use stall. The two penalties do not overlap. `OR` finishes WB on cycle 13.

### Q11

Answer: B

Base CPI is 1. Each data-memory instruction adds one stall, and those instructions are one quarter of the mix.

\[
\text{CPI} = 1 + 0.25 \times 1 = 1.25
\]

### Q12

Answer: 1.6

\[
\text{CPI} = 1 + 0.20 \times 3 = 1.6
\]

### Q13

Answer: A, B, C

ADD is immediately after the load, so the written order has one load-use stall. SUB does not read R1 or write a register that ADD reads, so it can sit between them and give the load time to finish MEM before ADD enters EX. OR reads R5 from SUB, so moving SUB earlier still requires OR to follow SUB. ADD still reads R1 and R4, so its result is unchanged. The four instructions contain no branch. D is false.

### Q14

Answer: 13

The first ADD immediately uses the first load: 1 stall. The second load uses the ADD result as an address: forwarding, 0 stalls. SUB is independent and sits between the second load and AND, so AND’s use of R5 has 0 load-use stalls. AND’s use of R6 and BEQ’s use of R9 are ALU forwardings. The branch is not taken, so predict-not-taken pays nothing. The last two instructions are on the correct path.

\[
5 + 8 - 1 + 1 = 13
\]

### Q15

Answer: B

Only the unfilled 30 percent of delay slots cost a cycle, and only on the 15 percent of instructions that are branches.

\[
\text{CPI} = 1 + 0.15 \times 0.30 \times 1 = 1.045
\]

A useful instruction in the slot does the work that would have been a separate instruction, so it adds no extra CPI.

### Q16

Answer: 760

Load-use stalls per instruction:

\[
0.30 \times 0.40 \times 1 = 0.12
\]

Branch stalls per instruction:

\[
0.20 \times 2 = 0.40
\]

\[
\text{CPI} = 1 + 0.12 + 0.40 = 1.52
\]

\[
T = \frac{10^{9} \times 1.52}{2 \times 10^{9}} = 0.76 \text{ s} = 760 \text{ ms}
\]

### Q17

Answer: 13

SUB does not use R4, and it stands between the load and AND. AND therefore reaches EX on the cycle after the load completes MEM, and forwarding supplies R4 with no stall. AND also forwards R5 from SUB. BEQ uses R6 from AND on the next cycle, again by forwarding.

The taken branch is resolved at the end of its EX cycle. Two wrong-path instructions have been fetched and are flushed. The target OR is fetched on the next cycle, which is a 2-cycle penalty relative to a stall-free schedule.

\[
5 + 7 - 1 + 2 = 13
\]

A load-use stall must not be added: the independent SUB already provides the one instruction of spacing that load-use forwarding needs. XOR depends on OR by an ALU forwarding path, so it adds no further stall and completes WB on cycle 13.

### Q18

Answer: A, B, C, D

Separate memories let IF and MEM proceed together. A load produces data at the end of MEM, which is too late for an immediately following instruction already in EX, so one stall remains; an intervening independent instruction removes it. A branch resolved in ID has fetched only one successor, whereas resolution in EX has fetched two, so the ID penalty is smaller under predict-not-taken. RAW is a property of the instruction stream and can be classified without scoreboarding or out-of-order issue. E is false.
