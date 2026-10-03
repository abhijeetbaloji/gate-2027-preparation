# Instruction Pipelining — Practice Questions

Original practice for GATE CS. These questions are not from any GATE paper. Attempt the questions before reading the solutions.

For a \(k\)-stage pipeline with no stalls, \(N\) instructions take

\[
k + N - 1
\]

cycles. The speedup against a non-pipelined implementation that uses the same clock and takes \(k\) cycles per instruction is

\[
\frac{Nk}{k + N - 1}
\]

When stage delays differ, the non-pipelined time per instruction is the sum of the combinational stage delays. The pipeline clock is the slowest stage plus any stated register overhead. Asymptotic speedup is that non-pipelined time divided by the pipeline clock.

## Level 1 — Conceptual

## Q1 — MCQ

An instruction pipeline improves throughput by

A. keeping several instructions in different stages at the same time  
B. executing only one instruction anywhere in the CPU  
C. replacing the register file with a DMA buffer  
D. requiring two ALUs inside every instruction

---

## Q2 — NAT

One instruction enters an empty 5-stage pipeline and there are no stalls. How many cycles pass before that instruction completes the last stage?

---

## Q3 — MCQ

After a scalar pipeline is full, and while it has no stalls, its instruction throughput is

A. one instruction per cycle  
B. one instruction every \(k\) cycles  
C. \(k\) instructions per cycle  
D. one instruction only on the first cycle

---

## Q4 — NAT

A 4-stage pipeline executes 8 instructions with no stalls. How many cycles does it take?

---

## Level 2 — Standard GATE Style

## Q5 — NAT

A 5-stage pipeline and a non-pipelined processor use the same clock. The non-pipelined processor takes 5 cycles per instruction. For 46 instructions and no pipeline stalls, the speedup \(T_{\text{non-pipe}} / T_{\text{pipe}}\), to one decimal place, is ______.

---

## Q6 — MCQ

Four stages have combinational delays 3 ns, 4 ns, 2 ns, and 5 ns. Pipeline-register overhead is 0. The asymptotic speedup over the non-pipelined sum of those delays is

A. 2  
B. 2.8  
C. 4  
D. 14

---

## Q7 — NAT

Stage delays are 5 ns, 6 ns, 4 ns, and 7 ns. Every pipeline register adds 1 ns. The non-pipelined implementation pays the sum of the combinational delays and does not pay the register overhead. The asymptotic speedup, to two decimal places, is ______.

---

## Q8 — MSQ

Select all that apply.

A. The pipeline clock must accommodate the slowest stage, including its register overhead.  
B. With balanced stages, no stalls, and a very large \(N\), speedup approaches the number of stages.  
C. A faster stage does not set the clock if another stage is slower.  
D. The ideal CPI of a scalar pipeline with no hazards is 1.

---

## Q9 — NAT

A 6-stage pipeline has a 2 ns clock and no stalls. How many nanoseconds are required for 100 instructions?

---

## Q10 — MCQ

A 4-stage pipeline has combinational delays 200 ps, 400 ps, 300 ps, and 100 ps. Each pipeline register adds 50 ps. The clock period is

A. 350 ps  
B. 400 ps  
C. 450 ps  
D. 1000 ps

---

## Level 3 — Multi-Step

## Q11 — NAT

Four balanced stages each take 5 ns, and register overhead is 0. The non-pipelined instruction time is the sum, 20 ns, on the same technology. For 12 instructions and no stalls, the speedup is ______.

---

## Q12 — MCQ

A 5-stage pipeline has combinational delays IF 8 ns, ID 6 ns, EX 14 ns, MEM 8 ns, and WB 6 ns. Every pipeline register adds 1 ns, so the present clock is 15 ns. EX is replaced by two stages of 8 ns and 7 ns. The new register between them also adds 1 ns, and every stage pays that overhead. The new clock is

A. 7 ns  
B. 8 ns  
C. 9 ns  
D. 15 ns

---

## Q13 — NAT

A non-pipelined implementation has 40 ns of combinational logic. It is split into \(k\) equal stages, and each pipeline register adds 2 ns. The asymptotic speedup is

\[
\frac{40}{40/k + 2}
\]

What is the smallest integer \(k\) that makes this speedup at least 4?

---

## Q14 — MSQ

A scalar pipeline has the stages IF, ID, EX, MEM, and WB. Select all that apply.

A. A register-register ADD computes in EX and writes the register file in WB.  
B. A load reads data memory in MEM.  
C. In any one clock, only one stage may hold an instruction.  
D. Different instructions may occupy different stages in the same clock.

---

## Level 4 — Tricky / Trap-Based

## Q15 — NAT

A 6-stage pipeline has a 1.25 ns clock and never stalls. It starts empty. How many instructions complete the last stage during the first 200 cycles?

---

## Q16 — MCQ

Four stages have delays 2 ns, 2 ns, 2 ns, and 6 ns. Register overhead is 0. The asymptotic speedup over the 12 ns non-pipelined instruction is

A. 2  
B. 3  
C. 4  
D. 6

---

## Q17 — NAT

A non-pipelined processor has CPI 4 and a 2 GHz clock. A pipelined implementation of the same instruction set has CPI 1.25, including its bubbles, and a 2.5 GHz clock. The speedup of the pipeline, using CPU time proportional to \(\text{CPI}/f\), is ______.

---

## Level 5 — Challenge

## Q18 — NAT

A 5-stage pipeline runs 100 instructions: 80 ALU operations and 20 multiplies. An ALU instruction uses the EX stage for one cycle. A multiply uses EX for three cycles, and the two extra EX cycles stall the pipeline. There are no other stalls. How many cycles are required?

---

## Q19 — NAT

Combinational logic of 48 ns is divided into \(k\) equal stages with a 2 ns register overhead on the pipeline clock. Asymptotic speedup is \(48 / (48/k + 2)\). What is the smallest integer \(k\) for which the speedup is at least 6?

---

## Q20 — MSQ

Thirty instructions run on a 5-stage pipeline. The stages are equal, the clock is 4 ns, and there are no stalls. The non-pipelined processor on the same logic takes \(5 \times 4 = 20\) ns per instruction. Select all that apply.

A. The pipeline takes 34 cycles.  
B. The pipeline takes 136 ns.  
C. The speedup against that non-pipelined processor is greater than 4.  
D. The asymptotic speedup for a very large instruction count is 5.

## Answer Key

| Q | Type | Answer |
|---|------|--------|
| 1 | MCQ | A |
| 2 | NAT | 5 |
| 3 | MCQ | A |
| 4 | NAT | 11 |
| 5 | NAT | 4.6 |
| 6 | MCQ | B |
| 7 | NAT | 2.75 |
| 8 | MSQ | A, B, C, D |
| 9 | NAT | 210 |
| 10 | MCQ | C |
| 11 | NAT | 3.2 |
| 12 | MCQ | C |
| 13 | NAT | 5 |
| 14 | MSQ | A, B, D |
| 15 | NAT | 195 |
| 16 | MCQ | A |
| 17 | NAT | 4 |
| 18 | NAT | 144 |
| 19 | NAT | 8 |
| 20 | MSQ | A, B, C, D |

## Detailed Solutions

### Q1

Answer: A

Pipeline stages hold different instructions at the same time. The machine is still scalar: each stage does one piece of one instruction per cycle. DMA and extra ALUs are not what creates the overlap.

### Q2

Answer: 5

The single instruction must walk through all 5 stages.

\[
5 + 1 - 1 = 5
\]

### Q3

Answer: A

Once every stage is busy, a scalar pipeline without stalls accepts one new instruction per cycle and retires one instruction per cycle. It does not retire \(k\) instructions in one cycle.

### Q4

Answer: 11

\[
4 + 8 - 1 = 11
\]

### Q5

Answer: 4.6

Non-pipelined cycles: \(46 \times 5 = 230\). Pipeline cycles:

\[
5 + 46 - 1 = 50
\]

\[
\frac{230}{50} = 4.6
\]

The same result is \(Nk/(k+N-1)\).

### Q6

Answer: B

\[
3 + 4 + 2 + 5 = 14 \text{ ns}
\]

The pipeline clock is the maximum, 5 ns.

\[
\frac{14}{5} = 2.8
\]

The stage count is 4, but the stages are unbalanced, so the asymptotic speedup is less than 4.

### Q7

Answer: 2.75

\[
5 + 6 + 4 + 7 = 22 \text{ ns}
\]

\[
\text{pipeline clock} = 7 + 1 = 8 \text{ ns}
\]

\[
\frac{22}{8} = 2.75
\]

### Q8

Answer: A, B, C, D

The clock follows the slowest stage and its overhead. Balanced stall-free speedup tends to \(k\), and ideal scalar CPI is 1. The first instruction still needs \(k\) cycles, so nothing is completed on cycle 1 of an empty pipeline. E is false.

### Q9

Answer: 210

\[
6 + 100 - 1 = 105 \text{ cycles}
\]

\[
105 \times 2 = 210 \text{ ns}
\]

### Q10

Answer: C

The slowest combinational stage is 400 ps. The register overhead is added once per clock.

\[
400 + 50 = 450 \text{ ps}
\]

The sum 1000 ps would be the non-pipelined combinational total, not the pipeline clock.

### Q11

Answer: 3.2

Non-pipelined time:

\[
12 \times 20 = 240 \text{ ns}
\]

Pipeline cycles and time:

\[
4 + 12 - 1 = 15, \quad 15 \times 5 = 75 \text{ ns}
\]

\[
\frac{240}{75} = 3.2
\]

### Q12

Answer: C

The new combinational delays are 8, 6, 8, 7, 8, and 6 ns. The maximum is 8 ns, and every stage still pays 1 ns of register overhead.

\[
8 + 1 = 9 \text{ ns}
\]

The old 14 ns EX stage is no longer present, so the clock is not 15 ns.

### Q13

Answer: 5

The inequality is

\[
\frac{40}{40/k + 2} \ge 4
\]

\[
40 \ge 4\left(\frac{40}{k} + 2\right)
\]

\[
10 \ge \frac{40}{k} + 2
\]

\[
8 \ge \frac{40}{k}
\]

\[
k \ge 5
\]

Check \(k = 5\): the clock is \(40/5 + 2 = 10\) ns and the speedup is \(40/10 = 4\). For \(k = 4\) the clock is 12 ns and the speedup is \(40/12 < 4\). The smallest such \(k\) is 5.

### Q14

Answer: A, B, D

ADD uses the ALU in EX and writes in WB. LOAD uses MEM for the data read. Different instructions occupy the five stages together, including a WB overlapping a later IF. C denies that overlap, so it is false.

### Q15

Answer: 195

Instruction \(i\), counting from 1, completes WB on cycle

\[
6 + i - 1
\]

Require \(5 + i \le 200\), so \(i \le 195\). The first instruction finishes on cycle 6, and each later instruction finishes one cycle later. Over 200 cycles the pipeline retires \(200 - 5 = 195\) instructions. The five cycles that do not retire an instruction are the initial fill.

### Q16

Answer: A

\[
\frac{2 + 2 + 2 + 6}{6} = \frac{12}{6} = 2
\]

A balanced 4-stage pipeline would approach speedup 4. The 6 ns stage limits this one to 2.

### Q17

Answer: 4

\[
\frac{T_{\text{old}}}{T_{\text{new}}}
= \frac{4 / 2}{1.25 / 2.5}
= \frac{2}{0.5}
= 4
\]

The higher pipeline clock and the residual CPI of 1.25 cancel in such a way that the speedup equals the non-pipelined CPI.

### Q18

Answer: 144

The stall-free base is

\[
5 + 100 - 1 = 104
\]

Each multiply contributes \(3 - 1 = 2\) extra EX cycles.

\[
20 \times 2 = 40
\]

\[
104 + 40 = 144
\]

### Q19

Answer: 8

\[
\frac{48}{48/k + 2} \ge 6
\]

\[
48 \ge 6\left(\frac{48}{k} + 2\right)
\]

\[
8 \ge \frac{48}{k} + 2
\]

\[
k \ge 8
\]

At \(k = 8\) the clock is \(48/8 + 2 = 8\) ns and the speedup is exactly 6. At \(k = 7\) the clock is \(48/7 + 2 \approx 8.86\) ns and the speedup is about 5.42, which is below 6.

### Q20

Answer: A, B, C, D

\[
5 + 30 - 1 = 34 \text{ cycles}
\]

\[
34 \times 4 = 136 \text{ ns}
\]

Non-pipelined time:

\[
30 \times 20 = 600 \text{ ns}
\]

\[
\frac{600}{136} = \frac{75}{17} \approx 4.41 > 4
\]

Equal stages make the asymptotic speedup equal to the stage count, 5. Five cycles is only enough to finish the first instruction, so E is false.
