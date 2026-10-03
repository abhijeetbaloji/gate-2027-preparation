# Instruction Pipelining — Practice (original questions)

All questions are original (not from any GATE paper and not copied from the repository's existing practice file). Every answer is placed directly under its question and was checked with a script (`/tmp/coa-verify-pipelining-practice.py`).
Conventions: ideal pipelines are in-order, one instruction enters per cycle, no stalls unless stated; clock = slowest stage + register overhead; GHz = 10^9 Hz. MSQ = one or more options correct, no partial marking.
Theory: [`NOTES.md`](NOTES.md). Hazard identification and stall counting: [`../08-PIPELINE-HAZARDS`](../08-PIPELINE-HAZARDS/).

---

## Level 1 — Conceptual

### Q1 (MCQ, L1)
Compared with a non-pipelined unit built from the same logic, a k-stage pipeline with pipeline registers

A. cuts the latency of each instruction to about 1/k and leaves throughput unchanged
B. does not cut the latency of an individual instruction (it normally rises slightly) but raises throughput
C. improves both latency and throughput by a factor of k
D. leaves throughput unchanged but lets the CPI fall below 1

**Answer:** B
**Solution:** One instruction still passes through all k stages, each stretched to the slowest stage plus register delay, so latency = k·T_p ≥ T_np. After the fill, one instruction completes per cycle, so throughput rises from 1/T_np to 1/T_p. A and C claim the latency falls. D is false: a scalar pipeline has CPI ≥ 1.
**Concept tested:** latency versus throughput (NOTES §3.2).
**Difficulty:** Easy.
**Common trap:** believing "pipelining makes each instruction faster".

### Q2 (MSQ, L1)
In a 5-stage pipeline (IF, ID, EX, MEM, WB) with registers between the stages, which statements are correct? (One or more options correct.)

A. The ID/EX register carries the register operands read in ID and the destination-register number towards later stages.
B. The EX/MEM register carries the data a store instruction will write to memory.
C. The IF/ID register holds the ALU result of the previous instruction.
D. The setup and clock-to-Q delay of the registers is added to the usable cycle time of every stage.

**Answer:** A, B, D
**Solution:** A, B, D match the register contents (NOTES §2.4). C is false: the IF/ID register holds the fetched instruction word and PC+4; ALU results appear first in EX/MEM.
**Concept tested:** pipeline registers and their overhead.
**Difficulty:** Easy.

### Q3 (NAT, L1)
A 6-stage pipeline has a clock of 2.5 ns and never stalls. The first instruction enters stage 1 at time 0. At what time, in ns, does the 4th instruction leave the last stage?

**Answer:** 22.5
**Solution:** The 4th instruction completes at cycle k + i − 1 = 6 + 4 − 1 = 9. Time = 9 × 2.5 ns = 22.5 ns.
**Concept tested:** completion cycle k + i − 1 (NOTES §4.1).
**Difficulty:** Easy.
**Common trap:** 4 × 6 × 2.5 = 60 ns (no overlap).

### Q4 (NAT, L1)
A 5-stage pipeline executes 10 instructions without stalls. How many stages are busy during clock cycle 12 (cycles are numbered from 1)?

**Answer:** 3
**Solution:** Total cycles = 5 + 10 − 1 = 14. Cycle 12 lies in the drain: busy stages = N + k − c = 10 + 5 − 12 = 3. Check directly: instruction i is in stage c − i + 1 when that lies between 1 and 5: i = 8 (stage 5), 9 (stage 4), 10 (stage 3).
**Concept tested:** reading the Gantt chart; fill and drain.
**Difficulty:** Easy.
**Common trap:** answering 5 (steady-state value).

---

## Level 2 — Standard GATE style

### Q5 (NAT, L2)
A 5-stage ideal pipeline has a 1.5 ns clock. How many nanoseconds does it need for 200 instructions?

**Answer:** 306
**Solution:** cycles = 5 + 200 − 1 = 204; time = 204 × 1.5 ns = 306 ns.
**Concept tested:** time = (k + N − 1)·T.
**Difficulty:** Easy.
**Common trap:** 200 × 1.5 = 300 ns.

### Q6 (MCQ, L2)
A 6-stage pipeline and a non-pipelined machine (6 cycles per instruction) use the same clock. For 30 instructions without stalls the speedup is

A. 4.50
B. 5.14
C. 5.00
D. 6.00

**Answer:** B
**Solution:** S = Nk/(k + N − 1) = 30·6/35 = 180/35 = 5.14. C is Nk/(N + k) (off by one cycle); D is the limit N → ∞; A has no basis.
**Concept tested:** speedup, same-clock case (V1).
**Difficulty:** Easy.
**Common trap:** using k + N in the denominator.

### Q7 (NAT, L2)
Stage delays are 150, 210, 180, 120 and 190 ps. Each pipeline register adds 30 ps. 2000 instructions run without stalls. How many nanoseconds does the pipelined execution take (two decimal places)?

**Answer:** 480.96
**Solution:** T_p = 210 + 30 = 240 ps. Cycles = 5 + 2000 − 1 = 2004. Time = 2004 × 240 ps = 480 960 ps = 480.96 ns.
**Concept tested:** clock = max + overhead, then (k + N − 1) × T_p, unit conversion.
**Difficulty:** Medium.
**Common trap:** ps → ns conversion (÷1000); using Σ delays as the clock.

### Q8 (NAT, L2)
Stage delays are 60, 110, 80, 50 and 100 ps; each pipeline register adds 15 ps. The non-pipelined design is the same logic without pipeline registers. What is the asymptotic speedup (two decimals)?

**Answer:** 3.20
**Solution:** T_np = 60 + 110 + 80 + 50 + 100 = 400 ps. T_p = 110 + 15 = 125 ps. S_∞ = 400/125 = 3.20.
**Concept tested:** variant B of the non-pipelined time (NOTES §5.2).
**Difficulty:** Easy.
**Common trap:** answering 5 (stage count) or adding 15 ps × 5 to the numerator (gives 3.80).

### Q9 (MSQ, L2)
An 8-stage pipeline runs 57 instructions without stalls; the non-pipelined machine uses the same clock and needs 8 cycles per instruction. Select all correct statements. (One or more options correct.)

A. The pipeline needs 64 cycles.
B. The speedup is 7.125.
C. The efficiency (speedup divided by the number of stages) is about 0.89.
D. With 1000 instructions the speedup would be exactly 8.

**Answer:** A, B, C
**Solution:** A: 8 + 57 − 1 = 64. B: 57·8/64 = 7.125. C: 7.125/8 = 0.8906 = 57/64. D: 1000·8/1007 = 7.94 < 8; the speedup reaches 8 only as N → ∞.
**Concept tested:** V1 speedup, efficiency η = N/(k + N − 1).
**Difficulty:** Medium.

### Q10 (NAT, L2)
A 7-stage pipeline has a 0.5 ns clock and starts empty with no stalls. How many instructions have completed after 2 µs?

**Answer:** 3994
**Solution:** 2 µs = 2000 ns = 4000 cycles. Completed = C − k + 1 = 4000 − 7 + 1 = 3994 (the first completes at cycle 7).
**Concept tested:** completed-by-cycle formula.
**Difficulty:** Medium.
**Common trap:** 4000, or 4000 − 7 = 3993.

### Q11 (MCQ, L2)
Pipeline registers have zero delay. The designs and their stage delays (ns) are:
P1: 3 stages — 1.2, 1.6, 1.1
P2: 4 stages — 0.9, 1.0, 1.4, 0.7
P3: 5 stages — 0.6, 0.9, 0.8, 0.9, 0.5
P4: 6 stages — 0.5, 0.5, 0.8, 0.7, 0.95, 0.4
Which design has the highest peak clock frequency?

A. P1
B. P2
C. P3
D. P4

**Answer:** C
**Solution:** Clock = longest stage: P1 1.6, P2 1.4, P3 0.9, P4 0.95 ns. The smallest is P3 (0.9 ns, 1.11 GHz); P4 is deeper but its 0.95-ns stage limits it (1.05 GHz).
**Concept tested:** f = 1/max stage delay.
**Difficulty:** Easy.
**Common trap:** choosing the deepest pipeline.

---

## Level 3 — Multi-step numerical

### Q12 (NAT, L3)
Four pipeline stages have delays 650, 380, 500 and 260 ps and registers add nothing. The 650-ps stage is replaced by two stages of 350 ps and 300 ps. By what percent does the throughput increase?

**Answer:** 30
**Solution:** Old clock = 650 ps. New stages: 350, 300, 380, 500, 260 → new clock = 500 ps (the unchanged 500-ps stage). Throughput ratio = 650/500 = 1.30 → +30 %.
**Concept tested:** splitting a stage; the next-slowest stage becomes the limit.
**Difficulty:** Medium.
**Common trap:** using 350 as the new clock (85.7 %).

### Q13 (NAT, L3)
A four-stage pipeline with zero register delay runs at 4 GHz. Its stage delays are in the ratio 3 : 7 : 5 : 6. The longest stage is split into two equal halves. What is the new maximum frequency in GHz (two decimals)?

**Answer:** 4.67
**Solution:** The longest stage (7 units) equals 1/4 GHz = 0.25 ns, so 1 unit = 0.25/7 ns. After splitting, stages are 3, 3.5, 3.5, 5, 6 units; the maximum is 6 units = 6 × 0.25/7 = 0.2143 ns. f = 1/0.2143 ns = 4.67 GHz (= 4 × 7/6).
**Concept tested:** frequency after splitting; ratio-defined stage delays.
**Difficulty:** Medium.
**Common trap:** answering 8 GHz by treating the 3.5-unit halves as the limit.

### Q14 (NAT, L3)
A non-pipelined multi-cycle processor runs at 2.4 GHz with this mix: ALU 45 % (4 cycles), load 25 % (5), store 12 % (4), branch 18 % (3). A pipelined version of the same ISA runs at 2 GHz and 20 % of its instructions lose 2 stall cycles each. Speedup of the pipelined design (two decimals)?

**Answer:** 2.42
**Solution:** CPI_np = 0.45·4 + 0.25·5 + 0.12·4 + 0.18·3 = 1.8 + 1.25 + 0.48 + 0.54 = 4.07. CPI_pipe = 1 + 0.2·2 = 1.4. Time per instruction: non-pipelined = 4.07/2.4 = 1.696 ns; pipelined = 1.4/2.0 = 0.700 ns. S = 1.696/0.700 = 2.42.
**Concept tested:** iron law with a mix and different clocks (NOTES §8).
**Difficulty:** Medium.
**Common trap:** adding the stall to the non-pipelined CPI; ignoring the clock difference (gives 2.91).

### Q15 (NAT, L3)
A 6-stage pipeline executes 80 instructions. Stage 3 takes 1 cycle for 55 instructions, 3 cycles for 15 instructions and 6 cycles for 10 instructions; every other stage takes 1 cycle for every instruction. There are no other stalls. How many cycles does the run take?

**Answer:** 165
**Solution:** Ideal = 6 + 80 − 1 = 85. Extra cycles = 15 × (3 − 1) + 10 × (6 − 1) = 30 + 50 = 80. Total = 165. (Same as k − 1 + Σc_i = 5 + (55 + 45 + 60) = 165.)
**Concept tested:** one multi-cycle stage closed form (NOTES §7.1).
**Difficulty:** Medium.
**Common trap:** adding Σc_i without the k − 1 fill, or using c_i instead of c_i − 1 in the extras.

### Q16 (MCQ, L3)
Processor P1 runs at 2 GHz with CPI 1.6 on a program. P2 (same ISA) takes 20 % less time on the same program but has a 25 % higher CPI. P2's clock frequency is

A. 2.5 GHz
B. 3.125 GHz
C. 2.4 GHz
D. 1.6 GHz

**Answer:** B
**Solution:** T = IC·CPI/f. T_2/T_1 = (CPI_2/CPI_1)(f_1/f_2) → 0.8 = 1.25 × 2/f_2 → f_2 = 2.5/0.8 = 3.125 GHz. A = 2 × 1.25 (ignores the time reduction); C = 2 × 1.2; D = 2 × 0.8.
**Concept tested:** CPI/time/frequency algebra.
**Difficulty:** Medium.
**Common trap:** inverting a ratio.

### Q17 (NAT, L3)
Stage delays are 3 ns, 8 ns and 4 ns, registers add nothing, and 200 independent instructions run. The 8-ns stage is replicated into two identical copies used alternately, so the pipeline can run at a 4-ns clock with that stage taking 2 cycles in each copy. How many nanoseconds does the program take?

**Answer:** 812
**Solution:** Cycle pattern (1, 2, 1) → latency 4 cycles; no stall occurs because each copy receives a new instruction only every 2 cycles. Cycles = 4 + 199 = 203; time = 203 × 4 ns = 812 ns. (Without replication: clock 8 ns, 3 stages → (3 + 199) × 8 = 1616 ns.)
**Concept tested:** replicated stage; clock = new max; fill counted in cycles of the new clock.
**Difficulty:** Medium.
**Common trap:** using 3 stages at 4 ns, (3 + 199) × 4 = 808 ns — the 8-ns unit still occupies 2 cycles, so the latency is 4 cycles.

### Q18 (NAT, L3)
A program has 4.0 × 10^8 instructions: 1.5 × 10^8 ALU (4 cycles), 1.0 × 10^8 load (5 cycles), 0.6 × 10^8 store (4 cycles), 0.9 × 10^8 branch (3 cycles). It runs in 3.22 s. The clock period in ns is

**Answer:** 2.0
**Solution:** Total cycles = 6.0e8 + 5.0e8 + 2.4e8 + 2.7e8 = 16.1e8. T_clk = 3.22 s / 16.1e8 = 2.0 ns. (The class counts add to 4.0e8, as stated.)
**Concept tested:** iron law, cycles = Σ count × CPI.
**Difficulty:** Medium.
**Common trap:** dividing by the instruction count (gives 8.05 ns) or losing a power of 10.

### Q19 (NAT, L3)
Stage delays are 40, 80, 60 and 20 ns with zero register delay. In steady state, what is the average utilisation (in percent) of the four stages?

**Answer:** 62.5
**Solution:** Clock = 80 ns. Stage i is busy t_i/80 of each cycle: 50 %, 100 %, 75 %, 25 %. Average = 250/4 = 62.5 %. This equals S_∞/k = (200/80)/4 = 0.625.
**Concept tested:** utilisation U_i = t_i/T_p; efficiency = S_∞/k.
**Difficulty:** Medium.

### Q20 (MCQ, L3)
A 5-stage floating-point multiplier pipeline with a 2.5 ns clock processes 64 independent operand pairs without stalls. The time taken is

A. 160 ns
B. 170 ns
C. 172.5 ns
D. 800 ns

**Answer:** B
**Solution:** (5 + 64 − 1) × 2.5 = 68 × 2.5 = 170 ns. A ignores the fill (64 × 2.5); C uses k + N cycles; D is the non-pipelined time 64 × 5 × 2.5.
**Concept tested:** arithmetic pipeline uses the same k + N − 1 model (NOTES §10).
**Difficulty:** Easy.

---

## Level 4 — Tricky / trap-based

### Q21 (NAT, L4)
Stage delays are 250, 400, 250 and 200 ps and every stage pays a 40-ps pipeline-register overhead. The 400-ps stage is split into two stages of 200 ps each, and the new register also costs 40 ps. By what percent (one decimal) does the throughput increase?

**Answer:** 51.7
**Solution:** Old clock = 400 + 40 = 440 ps. New stages: 250, 200, 200, 250, 200 → new clock = 250 + 40 = 290 ps. Ratio = 440/290 = 1.517 → +51.7 %.
**Concept tested:** overhead on every stage; the new limit is a 250-ps stage.
**Difficulty:** Medium.
**Common trap:** ignoring the overhead (400/250 − 1 = 60 %).

### Q22 (NAT, L4)
Non-pipelined: 42 ns per instruction. Pipelined: 6 stages, clock 9 ns, no stalls. For 30 instructions the speedup (two decimals) is

**Answer:** 4.00
**Solution:** Non-pipelined time = 30 × 42 = 1260 ns. Pipelined = (6 + 30 − 1) × 9 = 315 ns. S = 1260/315 = 4.00. (The asymptote is 42/9 = 4.67, and k = 6 is not the right numerator.)
**Concept tested:** V2 speedup with different times and finite N.
**Difficulty:** Medium.
**Common trap:** using Nk/(k + N − 1) = 5.14.

### Q23 (MSQ, L4)
A balanced 8-stage pipeline (same clock as the non-pipelined machine, which needs 8 cycles per instruction) runs N instructions without stalls. Select all correct statements. (One or more options correct.)

A. For N = 7 the speedup is 4.
B. For N = 100 the efficiency exceeds 0.93.
C. For N = 8 the efficiency is exactly 0.5.
D. For every finite N the speedup is below 8.

**Answer:** A, B, D
**Solution:** A: 7·8/14 = 4 (half the ideal at N = k − 1). B: 100/107 = 0.9346 > 0.93. C: 8/15 = 0.533, not 0.5. D: Nk/(k + N − 1) < k whenever k > 1.
**Concept tested:** speedup/efficiency formulas and limits.
**Difficulty:** Medium.

### Q24 (NAT, L4)
A 5-stage pipeline (IF, ID, EX, MEM, WB) has a 2-ns clock. A program executes 12 instructions I1…I12 in program order except that I5 is a taken branch whose target is I10, so I6–I9 are not executed. There is no prediction: fetch stops after the branch and restarts at the target in the cycle after the branch outcome is known, which is the end of its EX stage. There are no other stalls. How many nanoseconds does the program take?

**Answer:** 28
**Solution:** Executed order: I1…I5, I10, I11, I12 (8 instructions). p = 5 (branch position), r = 3 (EX), m = 3 (I10–I12). Cycles = p + r + m + k − 2 = 5 + 3 + 3 + 5 − 2 = 14 (= ideal 5 + 8 − 1 = 12 plus r − 1 = 2 bubble cycles). Time = 14 × 2 = 28 ns.
**Concept tested:** stage-level timing of a taken branch (cross-reference to the hazards folder).
**Difficulty:** Hard.
**Common trap:** counting the skipped instructions; forgetting the r − 1 bubbles.

### Q25 (MCQ, L4)
Stages of a pipeline have delays 5, 8, 8 and 4 ns (register delay 0). Which single design change reduces the clock period?

A. Split the first 8-ns stage into two 4-ns stages
B. Speed up the 5-ns stage to 3 ns
C. Speed up the 4-ns stage to 2 ns
D. Split both 8-ns stages into two 4-ns stages each

**Answer:** D
**Solution:** The clock is the maximum (8 ns). A leaves the other 8-ns stage; B and C leave both 8-ns stages. Only D removes both, giving stages 5, 4, 4, 4, 4, 4 → clock 5 ns.
**Concept tested:** ties for the slowest stage.
**Difficulty:** Medium.

---

## Level 5 — Challenge

### Q26 (NAT, L5)
Four stages S1–S4; each of four instructions stays in a stage for the following number of cycles. The pipeline has no buffers: an instruction stays in its stage until the next stage is free, stages hold one instruction each, instructions cannot overtake.

```
        S1 S2 S3 S4
  I1     1  2  1  1
  I2     1  1  2  1
  I3     2  1  1  1
  I4     1  2  1  2
```
How many cycles are needed to complete the four instructions?

**Answer:** 11
**Solution (blocking Gantt, cycles 1–11; * = finished but held):**

```
cycle :    1   2   3   4   5   6   7   8   9  10  11
S1    :   I1  I2 I2*  I3  I3  I4
S2    :       I1  I1  I2      I3  I4  I4
S3    :               I1  I2  I2  I3      I4
S4    :                   I1      I2  I3      I4  I4
```
I2 finishes S1 in cycle 2 but S2 is busy with I1 until cycle 3, so I2 waits and I3 starts S1 only in cycle 4. I4 finishes S2 in cycle 8, uses S3 in cycle 9, S4 in cycles 10–11. (With ideal buffers between stages the total would be 10; the naive "ideal 7 + all extras 5 = 12" is also wrong.)
**Concept tested:** general schedule with a cycles-per-stage table (NOTES §7.2).
**Difficulty:** Hard.
**Common trap:** summing times or ignoring the blocking.

### Q27 (NAT, L5)
Use this model: a pipeline of k stages built from T = 50 ns of logic split into equal stages, register overhead d = 2 ns, and a fraction p = 0.02 of instructions each causing a flush of (k − 1) cycles. Time per instruction = (T/k + d)(1 + p(k − 1)). What integer k minimises it?

**Answer:** 35
**Solution:** Expanding: T(1 − p)/k + Tp + d(1 − p) + dpk. Setting the derivative to zero: k* = √(T(1 − p)/(dp)) = √(50 × 0.98/(2 × 0.02)) = √1225 = 35. Time at k = 35: 5.760 ns; at 34: 5.761; at 36: 5.761.
**Concept tested:** diminishing returns / optimal depth (NOTES §6.3).
**Difficulty:** Hard.
**Common trap:** assuming the speedup keeps improving with k.

### Q28 (NAT, L5)
A non-linear pipeline has this reservation table (X = stage busy):

```
 time →  0  1  2  3  4
 S1      X  .  .  X  .
 S2      .  .  X  .  X
 S3      .  X  .  .  X
```
What is the minimum average latency (MAL)?

**Answer:** 2.5
**Solution:** Forbidden latencies: S1 {3}, S2 {2}, S3 {3} → {2, 3}. Collision vector (C4 C3 C2 C1) = 0110. State diagram: from 0110, latency 1 → (0110 >> 1) OR 0110 = 0111; latency 4 → 0110; from 0111 the only allowed latency below 5 is 4 → 0110; any latency ≥ 5 returns to 0110. Cycles: (1, 4) → 2.5; (4) → 4; (≥ 5) → ≥ 5. Lower bound = max X's in a row = 2. MAL = 2.5 (the cycle (1, 4) is valid: initiations at times 0, 1, 5, 6, 10, … never collide).
**Concept tested:** forbidden latencies, collision vector, state diagram, MAL (NOTES §7.3).
**Difficulty:** Hard.
**Common trap:** forgetting that latency 1 is allowed; averaging only one latency.
