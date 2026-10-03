# Pipeline Hazards — Practice (original questions)

All questions are original (not from any GATE paper and not copied from the repository's existing practice file). Every answer is placed directly under its question and was checked with `/tmp/coa-verify-hazards.py` (pipeline simulator + independent ready-time calculator).

**Conventions (unless a question overrides):** classic 5-stage in-order pipeline IF → ID → EX → MEM → WB; separate instruction and data memories; register file **RF-A** (written first half of WB, read second half of ID); full forwarding into EX unless stated; first instruction's IF in cycle 1; completion = end of WB of the last instruction. MSQ = one or more options correct, no partial marking.

Theory: [`NOTES.md`](NOTES.md) · Formulas: [`FORMULAS.md`](FORMULAS.md).

---

## Level 1 — Conceptual

### Q1 (MCQ, L1)
In a simple **in-order** 5-stage pipeline where every instruction reads registers in ID and writes in WB, which dependence can cause a **data hazard**?

A. Read-after-read (RAR)  
B. Read-after-write (RAW)  
C. Write-after-read (WAR)  
D. Write-after-write (WAW)

**Answer:** B

**Solution:** Only RAW makes a later reader need a value the earlier writer has not yet produced in WB. WAR and WAW are name dependences that do not stall this organisation because the earlier read always happens before the later write (NOTES §4.3). RAR is not a dependence.

**Concept tested:** dependence vs hazard in-order.

**Difficulty:** Easy.

**Common trap:** picking "all except RAR".

---

### Q2 (MCQ, L1)
A **control hazard** arises when

A. two instructions need the register file in the same cycle  
B. the next instruction address is not known when the pipeline would fetch it  
C. a load is immediately followed by an instruction that uses the loaded register  
D. the instruction and data caches map to the same physical memory

**Answer:** B

**Solution:** Branches and jumps change the PC before the target/condition is resolved — that is a control hazard (NOTES §7). (C) is a data (load-use) hazard. (A) is structural if ports collide. (D) describes a memory organisation choice, not the definition of a control hazard.

**Concept tested:** control hazard definition.

**Difficulty:** Easy.

---

### Q3 (MSQ, L1)
Operand **forwarding** in a pipelined processor: select all correct statements. (One or more options correct.)

A. A result from the EX/MEM pipeline register can be sent to an ALU input in EX of a later instruction.  
B. Forwarding can remove every pipeline stall caused by data dependences.  
C. Forwarding requires extra multiplexers and comparators on the datapath.  
D. Forwarding chooses the correct branch target after a conditional branch.

**Answer:** A, C

**Solution:** A and C match the bypass hardware (NOTES §6). B is false: load-use still needs one stall. D is false: PC control is separate from operand forwarding.

**Concept tested:** forwarding mechanism and limits.

**Difficulty:** Easy.

**Common trap:** selecting B because "forwarding fixes data hazards".

---

### Q4 (MCQ, L1)
**Register renaming** in an out-of-order pipeline is primarily used to

A. translate virtual addresses to physical addresses  
B. eliminate false (WAR/WAW) dependences by mapping architectural registers to a larger physical register file  
C. replace compile-time register allocation entirely  
D. remove every RAW stall including load-use bubbles

**Answer:** B

**Solution:** Renaming breaks name clashes (WAR/WAW); RAW remains real data flow (NOTES §9). It is not address translation (A), not a substitute for all compiler allocation (C), and does not remove load-use stalls (D).

**Concept tested:** renaming purpose.

**Difficulty:** Easy.

---

## Level 2 — Standard GATE style

### Q5 (NAT, L2)
There is **no forwarding**. The register file uses **RF-B** (a value written in WB is readable only from the **next** cycle). Five ALU instructions form a chain: each of the last four reads the register written by the instruction immediately before it (`ADD R1,…`; `SUB R4,R1,R2`; `OR R5,R6,R7`; `AND R8,R4,R5`; `XOR R9,R8,R1`). How many clock cycles until `XOR` completes WB?

**Answer:** 18

**Solution:** Ready-time with gate `X_p + 4` (RF-B): X = 3, 7, 8, 12, 16 → total = 16 + 2 = **18**. Equivalently: base `5 + 5 − 1 = 9`, plus 9 stall cycles. Each adjacent ALU→ALU pair at `d = 1` costs 3 stalls under RF-B without forwarding.

**Concept tested:** no-forwarding stall counting, RF-B.

**Difficulty:** Medium.

**Common trap:** using RF-A (would give 14 cycles).

---

### Q6 (NAT, L2)
**Full forwarding** into EX is available (RF-A). The committed sequence is:

```
LW  R1, 0(R2)
LW  R3, 4(R2)
ADD R4, R1, R3
SW  R4, 8(R2)
LW  R5, 0(R4)
SUB R6, R5, R1
```

How many cycles until `SUB` completes WB?

**Answer:** 12

**Solution:** Stall analysis: `ADD` uses `R1` from the immediately preceding load-related chain — `R3` is two instructions after its load (0 stalls); `ADD` is adjacent to the first `LW` on `R1` → **1** load-use stall. `SW` data from `ADD` → 0 (MEM-stage forwarding). `LW R5` uses `R4` as address from `ADD` → 0. `SUB` uses `R5` from adjacent load → **1** load-use stall. Total = `6 + 5 − 1 + 2 = 12`.

**Concept tested:** load-use, store data vs address, forwarding.

**Difficulty:** Medium.

---

### Q7 (NAT, L2)
Branches are **18 %** of all instructions; **55 %** of branches are taken. A branch resolved at the end of **EX** has penalty `P = 2`; if resolved at the end of **ID**, `P = 1`. The pipeline uses predict-not-taken. By how much does the **CPI** decrease when resolution moves from EX to ID? (Give a decimal rounded to three places; ideal CPI = 1.)

**Answer:** 0.099

**Solution:** CPI reduction = `f_b × p_t × (P_EX − P_ID) = 0.18 × 0.55 × (2 − 1) = 0.099`. Only taken branches pay the penalty under PNT.

**Concept tested:** control-hazard CPI formula.

**Difficulty:** Medium.

**Common trap:** using `f_b × P` without `p_t`.

---

### Q8 (NAT, L2)
The pipeline has **one unified memory port** (IF cannot run in a cycle when any earlier load/store is in MEM). **No other stalls.** The program is:

```
ADD R1,R2,R3 ; LW R4,0(R9) ; SW R1,4(R9) ; ADD R5,R4,R4
SUB R6,R7,R7 ; LW R8,8(R9) ; OR R10,R11,R11 ; AND R12,R13,R13
```

(eight instructions). How many cycles until `AND` completes WB?

**Answer:** 14

**Solution:** Three load/store instructions each block one fetch while in MEM before the last instruction is fetched → 3 structural stalls. Base `8 + 4 = 12`; total **14**. With split I/D memories the same program takes 12 cycles.

**Concept tested:** unified-memory structural hazard.

**Difficulty:** Medium.

---

### Q9 (MCQ, L2)
The pipeline predicts branches **not taken**. A branch is **taken** and resolved at the end of **EX**. The pipeline is full and the branch itself is not stalled. How many already-fetched instructions are flushed?

A. 0  
B. 1  
C. 2  
D. 3

**Answer:** C

**Solution:** Penalty `P = r − 1` with `r = 3` (EX) → **2** wrong-path instructions flushed (NOTES §7.1).

**Concept tested:** branch flush count.

**Difficulty:** Easy.

**Common trap:** answering 3 (`P = r`).

---

## Level 3 — Multi-step

### Q10 (NAT, L3)
**Full forwarding**, RF-A, predict-not-taken. The original sequence is:

```
LW R1,0(R8) ; LW R2,4(R8) ; ADD R3,R1,R2 ; LW R4,8(R8)
ADD R5,R3,R4 ; SW R5,12(R8)
```

The compiler reorders to:

```
LW R1,0(R8) ; LW R2,4(R8) ; LW R4,8(R8) ; ADD R3,R1,R2)
ADD R5,R3,R4 ; SW R5,12(R8)
```

How many cycles does the **scheduled** version take until `SW` completes WB?

**Answer:** 10

**Solution:** Original order: two load-use stalls (`ADD R3` after `LW R2` is fine at `d=2`, but `ADD R3` needs `R1` at `d=1` from first `LW`; `ADD R5` adjacent to `LW R4`) → 12 cycles. Scheduled: each load has at least one instruction before its use → **0** load-use stalls → `6 + 4 = 10`.

**Concept tested:** compiler scheduling to remove load-use.

**Difficulty:** Medium.

---

### Q11 (NAT, L3)
Ideal CPI = 1. **25 %** of instructions are loads; **40 %** of loads are immediately followed by a dependent use that stalls **1** cycle (with forwarding). **20 %** of instructions are branches; **70 %** of branches are taken and each taken branch costs **2** stall cycles under predict-not-taken. No other stalls. What is the effective CPI? (Two decimal places.)

**Answer:** 1.38

**Solution:**
```
CPI = 1 + 0.25×0.40×1 + 0.20×0.70×2
    = 1 + 0.10 + 0.28 = 1.38
```

**Concept tested:** mixed data + control CPI.

**Difficulty:** Medium.

---

### Q12 (NAT, L3)
A **2-bit saturating branch predictor** starts in state **01** (weakly not-taken). A loop branch executes with outcomes **T,T,T,T,T,N** (five iterations), and this entire pattern repeats **4 times** (24 branch outcomes total). How many **mispredictions** occur?

**Answer:** 5

**Solution:** Trace simulation: warm-up misses on early taken branches while state climbs from 01, plus one miss on each loop exit (N predicted T). For this trace starting at 01: **5** mispredictions total (verified by script).

**Concept tested:** 2-bit counter trace.

**Difficulty:** Hard.

**Common trap:** assuming 1 miss per loop execution (steady-state count) without counting warm-up.

---

### Q13 (MSQ, L3)
Consider:

```
I1: MUL R1, R2, R3
I2: ADD R4, R1, R5
I3: SUB R5, R6, R7
I4: AND R1, R4, R5
I5: OR  R4, R1, R9
```

Select all correct statements. (One or more options correct.)

A. There is a RAW dependence from I1 to I2 on R1.  
B. There is a WAR dependence between I2 and I3 on R5.  
C. There is a WAW dependence between I1 and I4 on R1.  
D. In an in-order 5-stage pipeline, the WAR pair in (B) causes a pipeline stall.

**Answer:** A, B, C

**Solution:** A: I2 reads R1 written by I1. B: I2 reads R5, I3 writes R5 (anti-dependence). C: both write R1. D is false: WAR does not stall in-order (NOTES §4.3).

**Concept tested:** dependence classification.

**Difficulty:** Medium.

---

### Q14 (NAT, L3)
Using the CPI from Q11 (**1.38**), compare a **non-pipelined** machine (CPI = 4) at **1.5 GHz** with the pipelined machine at **1.2 GHz** on the same program. What is the speedup? (Two decimal places.)

**Answer:** 2.32

**Solution:**
```
Speedup = (CPI_np / f_np) / (CPI_pipe / f_pipe)
        = (4 / 1.5) / (1.38 / 1.2) = 2.667 / 1.15 = 2.32
```

**Concept tested:** speedup with different clocks.

**Difficulty:** Medium.

**Common trap:** using CPI ratio only (gives 2.90).

---

## Level 4 — Tricky / trap-based

### Q15 (NAT, L4)
A **4-stage** pipeline IF → ID → EX → WB is used. IF, ID, WB take 1 cycle each. EX takes **4 cycles** for `DIV`, **3** for `MUL`, **1** for `ADD`/`SUB`. Operand **forwarding from the end of EX** into the next instruction's EX is available. Sequence:

```
DIV R1,R2,R3 ; MUL R4,R5,R6 ; ADD R7,R1,R4 ; SUB R8,R7,R2
```

How many cycles until `SUB` completes WB?

**Answer:** 12

**Solution:** Serial EX occupancy dominates: `2 (IF,ID fill) + 4 + 3 + 1 + 1 + 1 (WB) = 12`. Forwarding satisfies dependences without extra bubbles beyond serial EX use.

**Concept tested:** multi-cycle EX structural + data scheduling.

**Difficulty:** Hard.

**Common trap:** answering 8 (ignoring multi-cycle EX).

---

### Q16 (NAT, L4)
**No forwarding**, RF-A. Five instructions:

```
ADD R1,R2,R3 ; SUB R4,R1,R5 ; AND R6,R1,R7 ; OR R8,R4,R6 ; XOR R9,R8,R2
```

How many cycles until `XOR` completes WB?

**Answer:** 15

**Solution:** Ready-time: X = 3, 6, 7, 11, 13 → total = 15. True extra stalls = 6 (not 8 from naively summing isolated pair stalls 2+1+1+2+2). The wait for R4 (I2→I4) is partly covered by the wait for R1.

**Concept tested:** non-additive stalls in a chain.

**Difficulty:** Hard.

**Common trap:** summing per-pair stalls → 8 extra → 17 cycles.

---

### Q17 (MCQ, L4)
One **branch delay slot**; branches are **15 %** of instructions. The compiler fills the slot usefully **70 %** of the time; otherwise a NOP wastes 1 cycle per branch. No other stalls. CPI = ?

A. 1.000  
B. 1.045  
C. 1.150  
D. 1.300

**Answer:** B

**Solution:** `CPI = 1 + f_b × (1 − u) = 1 + 0.15 × 0.30 = 1.045`.

**Concept tested:** delay-slot CPI.

**Difficulty:** Medium.

---

### Q18 (NAT, L4)
**Full forwarding**, predict-not-taken. Sequence:

```
LW  R1, 0(R2)
BNE R1, R0, L    ; taken
ADD R3, R4, R5   ; L:
SUB R6, R3, R3
```

The branch is resolved at the end of **ID**. How many cycles until `SUB` completes WB? (The answer is the same if resolution is in **EX** for this sequence.)

**Answer:** 11

**Solution:** Load → branch on `R1` with `d = 1`: 2 data stalls (load → branch in ID, forwarding). Taken branch, PNT, resolve ID: +1 control (1 flushed). Resolve EX: +2 control but 1 data stall saved vs ID on operand timing — net **11** either way. Four instructions, base 8, +3 extra = 11.

**Concept tested:** load-to-branch stalls; ID vs EX resolution tradeoff.

**Difficulty:** Hard.

---

### Q19 (NAT, L4)
Stage delays (ns): IF 0.9, ID 1.0, EX 1.2, MEM 1.2, WB 0.8; latch 0.1 ns.

**Without forwarding:** average data stalls 0.45 cycles/instruction, control stalls 0.15; EX stage unchanged.  
**With forwarding:** EX grows to 1.25 ns; data stalls 0.08, control stalls 0.15.

What is the speedup in **time per instruction** from adding forwarding? (Two decimal places.)

**Answer:** 1.25

**Solution:**
```
τ_no  = max(0.9,1.0,1.2,1.2,0.8) + 0.1 = 1.3 ns
τ_fwd = max(0.9,1.0,1.25,1.2,0.8) + 0.1 = 1.35 ns
t_no  = (1 + 0.45 + 0.15) × 1.3 = 2.08 ns/instr
t_fwd = (1 + 0.08 + 0.15) × 1.35 = 1.66 ns/instr
Speedup = 2.08 / 1.66 = 1.25
```

**Concept tested:** forwarding vs clock period tradeoff.

**Difficulty:** Hard.

---

## Level 5 — Challenge

### Q20 (NAT, L5)
A **2-bit saturating predictor** starts in state **01**. Branch outcomes are **T,N,T,N,T,N,T,N,T,N** (10 branches). How many mispredictions?

**Answer:** 10

**Solution:** Alternating pattern: state flips weakly each time; prediction always lags actual → **10** mispredictions. (With initial state 00 the count would be 5 — initial state matters.)

**Concept tested:** predictor limits on alternating branches.

**Difficulty:** Hard.

---

### Q21 (NAT, L5)
**Full forwarding**, predict-not-taken, branch resolved at end of **EX**. The body below executes **4 times**; after each body a `BNE R6,R0,L` executes (taken for the first 3 branches, not taken on the 4th). One final `ADD` follows.

```
LW  R1,0(R5) ; ADD R2,R1,R3 ; SW R2,0(R5)
ADD R5,R5,R4 ; SUB R6,R5,R7
```

How many cycles until the final `ADD` completes WB?

**Answer:** 39

**Solution:** 25 instructions total; simulator gives **39** cycles (includes load-use stalls in the body, 2-cycle taken-branch penalties for the first three branches, and no penalty on the final not-taken branch).

**Concept tested:** combined data + control scheduling on a loop.

**Difficulty:** Challenge.

---

### Q22 (NAT, L5)
Branches are **20 %** of instructions. The architecture has **two** branch delay slots. Slot 1 is filled usefully **60 %** of the time; slot 2 **25 %** of the time; otherwise each unfilled slot costs 1 cycle. No other stalls. CPI = ? (two decimal places.)

**Answer:** 1.23

**Solution:**
```
CPI = 1 + f_b × [(1 − 0.60) + (1 − 0.25)]
    = 1 + 0.20 × [0.40 + 0.75] = 1.23
```

**Concept tested:** multiple delay slots.

**Difficulty:** Medium.

---

### Q23 (MCQ, L5)
For predict-**taken** vs predict-**not-taken**, with branch penalty `P = 2` on misprediction/wrong path and `T_p = 1` cycle to obtain the target on a correct taken prediction, predict-taken is cheaper only if the fraction of branches taken `p_t` satisfies

A. `p_t > 1/2`  
B. `p_t > 2/3`  
C. `p_t > 3/4`  
D. `p_t > 4/5`

**Answer:** B

**Solution:** Break-even: `p_t > P/(2P − T_p) = 2/(4 − 1) = 2/3` (NOTES §7.2, FORMULAS D3).

**Concept tested:** predict-taken vs PNT break-even.

**Difficulty:** Medium.

---

### Q24 (NAT, L5)
Ideal CPI = 1, clock **2 GHz**. Loads are **30 %** of instructions; **40 %** of loads are immediately followed by a 1-cycle use stall. Branches are **20 %** of instructions; each costs **2** stall cycles (stall-until-resolved). A program of **10⁹** instructions: execution time in **milliseconds** (integer)?

**Answer:** 760

**Solution:**
```
CPI = 1 + 0.30×0.40×1 + 0.20×2 = 1 + 0.12 + 0.40 = 1.52
T = 10⁹ × 1.52 / (2 × 10⁹) s = 0.76 s = 760 ms
```

**Concept tested:** CPI to wall-clock time.

**Difficulty:** Medium.

---

### Q25 (NAT, L5)
Branches are **25 %** of instructions. Penalty on a wrong prediction or BTB miss = **3** cycles. BTB hit rate **80 %**; on a hit the direction is correct **90 %** of the time. On a miss, **60 %** of branches are taken (each pays full penalty). No other stalls. CPI = ? (two decimal places.)

**Answer:** 1.15

**Solution:**
```
stalls/branch = 0.8×0.1×3 + 0.2×0.6×3 = 0.24 + 0.36 = 0.60
CPI = 1 + 0.25 × 0.60 = 1.15
```

**Concept tested:** BTB effective CPI (NOTES §7.7).

**Difficulty:** Hard.

---

### Q26 (NAT, L5)
A 5-stage pipeline reads operands in **EX** (ID only decodes). EX takes **4 cycles** for `MUL`, **1** for `ADD`/`SUB`. Operand forwarding from the end of EX is available. Sequence (each instruction depends on the previous):

```
MUL R1,R2,R3 ; ADD R4,R1,R5 ; SUB R6,R2,R5 ; MUL R7,R4,R6 ; ADD R8,R7,R1
```

What is the speedup of execution **with** forwarding over **without** forwarding (RF-A, operands read in EX)? (Two decimal places.)

**Answer:** 1.20

**Solution:** Simulator: **15** cycles with forwarding, **18** without (EX may start in producer's WB cycle without forwarding). Speedup = 18/15 = **1.20**. (With RF-B next-cycle read: 21 cycles without forwarding → speedup 1.40.)

**Concept tested:** variable-latency EX + forwarding speedup (2021 Set-2 / 2007 pattern).

**Difficulty:** Challenge.

**Common trap:** treating forwarding as eliminating all stalls regardless of multi-cycle EX occupancy.
