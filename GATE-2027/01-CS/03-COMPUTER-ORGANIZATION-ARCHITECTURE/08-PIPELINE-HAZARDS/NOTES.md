# Pipeline Hazards — Structural, Data and Control (GATE CS 2027)

## 0. Where this fits

**Syllabus line (COA):** "… Instruction pipelining, pipeline hazards."

| Item | Detail |
|---|---|
| Prerequisite (read first) | [07-INSTRUCTION-PIPELINING](../07-INSTRUCTION-PIPELINING/NOTES.md): ideal k-stage pipeline, `k + N − 1` cycles, speedup, stage-delay/clock-period calculations. This file **links to it for those basics and owns everything that goes wrong** (stalls). |
| Other prerequisites | Instruction format and register operands ([01-INSTRUCTION-SET](../01-INSTRUCTION-SET/)), addressing modes (effective-address calculation happens in EX), control-unit idea of "control signals per stage" ([04-DESIGN-OF-CONTROL-UNIT](../04-DESIGN-OF-CONTROL-UNIT/)). |
| Depends on this topic | CPI/performance reasoning in [05-MEMORY-INTERFACING-AND-HIERARCHY/01-PERFORMANCE](../05-MEMORY-INTERFACING-AND-HIERARCHY/) (cache-miss stalls are added to the same CPI sum), interrupts in [06-IO-INTERFACE/01-INTERRUPT](../06-IO-INTERFACE/) (precise interrupts in a pipeline), register-allocation ideas in Compiler Design (false dependences). |
| Bridge, not owned here | Hit-time/miss-penalty maths: [05-…/01-PERFORMANCE](../05-MEMORY-INTERFACING-AND-HIERARCHY/). Logic-gate design of muxes/comparators: 02-DIGITAL-LOGIC. |

### Evidence snapshot (what drives the depth of each section)

Counted from the mapping file (`13-PYQ-TOPIC-MAPPING/.../08-PIPELINE-HAZARDS/questions.md`): **25 entries, 2007–2026**. After triage: **13 genuinely on-topic hazard questions**, **6 adjacent** (ideal-pipeline timing or cache-stall CPI: they are mapped here, but their skill belongs to topic 07 or topic 05), and **6 misfiled** (IP forwarding, a B+ tree, a heap, a C program — details in [PYQ.md](PYQ.md)). No entry is duplicated *inside this mapping* (the multi-booklet duplicates of 2013 sit in topic 07's mapping). Every answer in the mapping is "VERIFICATION REQUIRED", so this file teaches **methods** and never states an official answer.

| Section | Priority | Evidence |
|---|---|---|
| §5 Stall counting with/without forwarding, sequences with multi-cycle EX | **HIGH-VALUE** | 2021 Set-2, 2015 Set-2, 2007 (operand-forwarding timing with MUL/DIV/ADD) and the existing practice file (Q5–Q7, Q10, Q13, Q14, Q17) |
| §7 Control hazards: penalty, predict-not-taken, delay slot, predictor CPI | **HIGH-VALUE** | 2022, 2014 Set-3, 2024 CS-2, 2020, 2014 Set-1 (CPI with branch/stall fractions), 2008 (delayed-branch statement), practice Q9, Q10, Q12, Q15–Q17 |
| §3–§4 Dependence names (RAW/WAR/WAW) and which are real hazards | **HIGH-VALUE** | 2026, 2015 Set-3 (anti-dependence), 2008 Q36, 2012 (register renaming); sibling mapping adds a 2024 CS-2 dependence-classification entry |
| §8 CPI / speedup formulas with stalls and clock change | **HIGH-VALUE** | 2024 CS-2, 2022, 2020, 2014 Set-1, 2014 Set-3, practice Q11, Q12, Q16 |
| §6 Forwarding hardware, load-use interlock | MEDIUM | 2024 CS-1 (statements about forwarding), 2008; underlies every numeric stall count |
| §3 Structural hazards | MEDIUM | practice Q4, Q11; appears as the "single memory port" and "non-pipelined multi-cycle unit" patterns |
| §9 Register renaming / out-of-order (concept) | MEDIUM (concept only) | 2012 and 2008 statements |
| §10 Precise exceptions (concept) | LOW | no mapped entry; included because the syllabus phrase "pipeline hazards" is examined conceptually elsewhere and for interrupt topic continuity |

---

## 1. Conventions used everywhere in this file

1. **Classic 5-stage RISC pipeline:** `IF` (fetch) → `ID` (decode + register read) → `EX` (ALU / address calculation / branch compare) → `MEM` (data memory) → `WB` (register write). Every instruction passes through all five stages, one cycle each, unless a question says otherwise.
2. **Separate instruction and data memory** unless a structural hazard is being discussed.
3. **Register file timing — always state which one you assume:**
   - **RF-A (same-cycle):** the register file is *written in the first half* and *read in the second half* of a cycle. A consumer can therefore read in the same cycle in which the producer is in WB. (Default for this repo's COA folder.)
   - **RF-B (next-cycle):** a value written in WB can be read only in the *following* cycle.
4. **Forwarding ("full forwarding")**: a result is usable by the consumer's EX stage in the cycle after the producing stage ends (ALU result: after EX; load result: after MEM), through bypass paths EX→EX, MEM→EX (and MEM→MEM for store data).
5. **Instructions do not overtake each other.** Each stage holds one instruction; an instruction stays in a stage until the next stage is free (no buffers between stages, no out-of-order execution).
6. **Cycle counting:** with `N` instructions in a `k`-stage pipe, no stall: `N + k − 1` cycles (derivation: [07](../07-INSTRUCTION-PIPELINING/NOTES.md)). With stalls: `total = (N + k − 1) + total stall cycles`. `CPI_pipelined = 1 + average stall cycles per instruction`.
7. **Timing diagram symbols:** `IF ID EX MEM WB` are stages, `--` = the instruction is *held* in the stage before it (a stall cycle), `xx` = a wrong-path instruction that is later flushed.
8. **Iron law** (used in §8): `CPU time = IC × CPI × clock period`.

Every number in this file was checked with a small cycle-accurate in-order pipeline simulator (`/tmp/coa_hazard_sim.py`, verified against an independent closed-form method on thousands of random programs).

---

## 2. What is a hazard? The picture

A pipeline overlaps instructions so that, ideally, one instruction finishes every cycle. A **hazard** is a situation in which the *next instruction cannot execute in its scheduled cycle* without producing a wrong result or a resource conflict. The remedy is to **stall** (insert bubbles), or to add hardware that removes the need to stall (forwarding, duplicate resources, prediction).

```
Ideal:     I1  IF ID EX MEM WB
           I2     IF ID EX MEM WB
           I3        IF ID EX MEM WB          one instruction completes per cycle

Hazard:    I1  IF ID EX MEM WB
           I2     IF ID -- -- EX MEM WB       I2 cannot proceed -> 2 bubbles
           I3        IF -- -- ID EX MEM WB
```

**Three families**

| Family | Cause | Typical cure |
|---|---|---|
| **Structural** | Two instructions need the *same hardware resource in the same cycle* | Duplicate/pipeline the resource (split I/D memory, more RF ports), or stall |
| **Data** | An instruction needs a *value that an earlier, unfinished instruction has not yet produced* (or would overwrite one still needed) | Forwarding, stall (interlock), compiler scheduling, register renaming |
| **Control** | The *address of the next instruction* is not known yet (branch, jump, call, return) | Resolve earlier, predict, delayed branch, flush |

---

## 3. Structural hazards

### 3.1 Typical sources
1. **Single memory port (unified instruction + data memory).** In the cycle when a load/store is in MEM, the instruction fetch in IF wants the same port.
2. **Single register-file write port** while two instructions try to write in the same cycle (appears when instruction classes write in different stages, or with multi-cycle units finishing together).
3. **Single register-file read ports** too few for an instruction needing more operands than ports.
4. **Non-pipelined (or partly pipelined) functional unit** — a multi-cycle divider/multiplier that stays busy; the next divide must wait.

The classic 5-stage design avoids (1) by separate I-memory and D-memory (or I-cache/D-cache), and (2)/(3) by an RF with two read ports and one write port, using the half-cycle trick (RF-A) so that WB and ID never collide.

### 3.2 Counting a unified-memory stall
When a load/store is in MEM in cycle `m`, **no instruction can be fetched in cycle `m`**: the fetch slot is "dead". Every dead slot delays all later instructions by one cycle.

```
Program: LW, ADD, SUB, OR, AND      one memory port (IF and MEM share it)

Cycle                   1    2    3    4    5    6    7    8    9    10
LW  R1,0(R10)           IF   ID   EX   MEM  WB
ADD R2,R3,R4                 IF   ID   EX   MEM  WB
SUB R5,R6,R7                      IF   ID   EX   MEM  WB
OR  R8,R9,R3                                IF   ID   EX   MEM  WB
AND R11,R12,R4                                   IF   ID   EX   MEM  WB

(cycle 4: LW is in MEM and owns the memory port, so OR cannot be fetched until cycle 5)
```

* Total = 10 cycles = `5 + 5 − 1 + 1` (split memories would give 9).
* **Rule:** extra cycles = number of dead fetch slots = load/store MEM cycles that occur *before the last instruction has been fetched* (recompute the fetch cycles one by one, because each stall shifts the later MEM cycles too).
* **Tail effect (edge case):** if the load/store is among the last instructions so that nothing is left to fetch in its MEM cycle, it costs nothing. The 4-instruction program `ADD, SUB, OR, LW` (load last) takes 8 cycles with a unified memory — exactly the stall-free `4 + 5 − 1 = 8`. Do not blindly add "1 per load/store".
* **Averaged CPI:** if a fraction `f_mem` of instructions are loads/stores and each costs one dead fetch slot, `CPI = 1 + f_mem × 1`. Example: 25 % loads/stores → CPI 1.25 (this is the long-program limit; a 400-instruction program with a load every 4th instruction took 504 cycles → 1.26, the "+4" being pipeline fill).

### 3.3 Multi-cycle, non-pipelined EX (structural bottleneck)
If the EX stage of one instruction needs several cycles (MUL: 3, DIV: 5) and the unit is not pipelined, everything behind it queues. This is a *structural* hazard of the EX stage, and in a blocking pipeline it can swamp data dependences (see worked example E7 and practice Q16, where the total is determined by the serial EX time alone).

### 3.4 Cures and their price
| Cure | Cost |
|---|---|
| Split I/D memory (or caches) | Extra memory/cache hardware |
| More RF ports | RF area, access time |
| Pipeline the multi-cycle unit | Extra latches, more complex control; then WAW/WAR and write-port issues appear (see §4.5) |
| Stall (do nothing) | CPI increases |

---

## 4. Data dependences and data hazards

### 4.1 Dependence vs hazard
* A **dependence** is a property of the *program* (registers read/written by pairs of instructions).
* A **hazard** is a dependence that a particular *pipeline organisation* could get wrong if it did nothing special.

For instructions `i` before `j` in program order:

| Name | Also called | Condition | Meaning |
|---|---|---|---|
| **RAW** (read after write) | true / flow dependence | `j` reads a register that `i` writes | `j` needs the value `i` produces. **Real data flow** — can never be renamed away. |
| **WAR** (write after read) | anti-dependence | `j` writes a register that `i` reads | `j` must not overwrite the register before `i` has read it. Just a **name clash**. |
| **WAW** (write after write) | output dependence | `i` and `j` write the same register | The final value must be `j`'s; writes must happen in order. **Name clash**. |
| (RAR) | — | both only read | **No dependence, never a hazard.** |

WAR and WAW are **name (false) dependences**: they disappear if different registers are used (register renaming, §9). RAW does not.

### 4.2 Classifying the dependences in a code sequence (method)
1. Write the destination `D` and sources `S` of every instruction (`SW` has no destination; `LW` has a destination and a base source).
2. For every pair `i < j`:
   * **RAW** if `D(i) ∈ S(j)` and **no instruction between `i` and `j` redefines that register** (otherwise `j` reads the later value, so the flow comes from the nearer writer).
   * **WAR** if `D(j) ∈ S(i)`.
   * **WAW** if `D(i) = D(j)`.
3. List pairs with the register, e.g. `RAW(I1→I2, R1)`.

**Worked example E1.**
```
I1: MUL R1, R2, R3
I2: ADD R4, R1, R5
I3: SUB R5, R6, R7
I4: AND R1, R4, R5
I5: OR  R4, R1, R9
```
| Pair | Register | Type |
|---|---|---|
| I1 → I2 | R1 | RAW (I2 reads I1's R1) |
| I2 → I4 | R4 | RAW |
| I3 → I4 | R5 | RAW |
| I4 → I5 | R1 | RAW |
| I2, I3 | R5 | WAR (I2 reads R5, I3 writes it) |
| I2, I4 | R1 | WAR (I2 reads R1, I4 writes it) |
| I4, I5 | R4 | WAR (I4 reads R4, I5 writes it) |
| I1, I4 | R1 | WAW |
| I2, I5 | R4 | WAW |

Totals: 4 RAW, 3 WAR, 2 WAW. (A pair like I1→I4 on R1 is a *WAW*, not a RAW — I4 only writes R1.) Same-register WAW is usually the one students mislabel as WAR; the discriminator is **does the later instruction read or write that register in the earlier one?**

### 4.3 When can each hazard actually occur? (the key concept)
In the classic **in-order, 5-stage** pipeline of this file:

* All instructions read registers in **ID** (early) and write registers in **WB** (late), one instruction per stage, in order.
* **RAW is the only data hazard.** A reader (ID) can run ahead of the writer's WB, so it may read a stale value.
* **WAR cannot occur:** the earlier instruction's read (ID, cycle `c`) always happens before the later instruction's write (WB, at least three cycles after its own ID).
* **WAW cannot occur:** writes happen in WB in program order because instructions never overtake.

Therefore **"a dependence exists" ≠ "a hazard exists"**: WAR and WAW *dependences* are present in code but are not pipeline *hazards* here. This is the exact point that questions of the form "which dependence can cause a hazard in a pipelined processor?" test, and it must be read with the pipeline model in mind (see §9 for when the answer changes).

WAR/WAW become real hazards when **instructions can complete or issue out of order**:

* **WAW:** a long-latency instruction (e.g. a divide, 20 cycles) is followed by a short one (an add, 2 cycles) writing the same register, in a design where each functional unit writes on completion. The add finishes first; if the divide finishes later it overwrites the newer value:
```
DIV F0, F2, F4      writes F0 at cycle ~21
ADD F0, F6, F8      writes F0 at cycle ~4    <- order of writes reversed (WAW hazard)
```
* **WAR:** an instruction waits for an operand (issue stalled) while a later instruction with no dependences executes and writes the register the waiting one still needs to read (out-of-order issue), or a pipeline in which some instruction class reads an operand in a late stage.
* A **blocking in-order multi-cycle EX** (like the 4-stage example E7) still completes in order, so it introduces stalls but not WAW.

### 4.4 RAW through memory, stores and branches
* A store reads its **address register at EX** and its **data register at MEM**.
* A branch reads its operands at **EX** (or at **ID** if the comparator is in ID).
* A store→load dependence through *memory* is safe in this pipeline: loads and stores reach MEM in program order.

### 4.5 Summary table: what is a hazard where?
| Pipeline | RAW | WAR | WAW |
|---|---|---|---|
| In-order, uniform 5-stage (this file) | yes | no | no |
| In-order issue, multi-cycle/parallel FUs with completion out of order | yes | rare | **yes** |
| Out-of-order issue/execution (dynamic scheduling) | yes | yes | yes — removed by renaming (WAR, WAW) |

---

## 5. Stall counting — the core skill

### 5.1 Single-dependence rule (one producer, one consumer, nothing else stalling)

Let
* the producer be in IF at cycle `t`; the consumer is `d` instructions later (`d = 1` means adjacent), so it would be in IF at cycle `t + d` if nothing stalled;
* `H` = offset (counted from the producer's IF cycle) of the **first cycle in which the value can be used**;
* `U` = offset (counted from the consumer's own IF cycle) of the **cycle in which the consumer uses the value**.

Then

```
stall cycles = max( 0 , H − (d + U) )
```

| Situation | H | U | stalls = max(0, H − d − U) |
|---|---|---|---|
| No forwarding, RF-A (write 1st half, read 2nd half); consumer reads in ID | 4 (producer's WB cycle) | 1 (ID) | `max(0, 3 − d)` |
| No forwarding, RF-B (next-cycle read) | 5 | 1 | `max(0, 4 − d)` |
| Forwarding; ALU result → ALU/address input (EX) | 3 | 2 | `max(0, 1 − d)` = **0** |
| Forwarding; **load** result → ALU/address input | 4 | 2 | `max(0, 2 − d)` → **1 if d = 1** |
| Forwarding; ALU result → **store data** (needed in MEM) | 3 | 3 | 0 |
| Forwarding; load result → store data (MEM→MEM) | 4 | 3 | 0 |
| Forwarding; ALU result → branch compared in **ID** | 3 | 1 | `max(0, 2 − d)` → 1 if d = 1 |
| Forwarding; load result → branch compared in **ID** | 4 | 1 | `max(0, 3 − d)` → 2 if d = 1, 1 if d = 2 |

**Derivation.** With stage numbers IF=1 … WB=5 and the producer in IF at `t`: ID at `t+1`, EX at `t+2`, MEM at `t+3`, WB at `t+4`. An ALU result exists at the end of EX (cycle `t+2`), so it can be used from `t+3` (`H = 3`). A load result exists at the end of MEM (`t+3`), usable from `t+4` (`H = 4`). Without forwarding the value is in the register file only once written in WB: under RF-A a read in cycle `t+4` works (`H = 4`), under RF-B only from `t+5`. The consumer, if not delayed, is in IF at `t+d`, ID at `t+d+1`, EX at `t+d+2`, so it uses an operand at offset `U` = 1 (read in ID), 2 (EX), 3 (MEM) from its own IF. It must wait for the difference.

**Dependency-distance table (stalls vs d), verified by simulation**

| Producer → consumer | Model | d = 1 | d = 2 | d = 3 | d ≥ 4 |
|---|---|:-:|:-:|:-:|:-:|
| any ALU/load → ALU | no forwarding, RF-A | 2 | 1 | 0 | 0 |
| any ALU/load → ALU | no forwarding, RF-B | 3 | 2 | 1 | 0 |
| ALU → ALU | full forwarding | 0 | 0 | 0 | 0 |
| LOAD → ALU (also → address) | full forwarding | **1** | 0 | 0 | 0 |
| LOAD → store *data* | full forwarding (MEM→MEM) | 0 | 0 | 0 | 0 |
| ALU → branch resolved in ID | forwarding | 1 | 0 | 0 | 0 |
| LOAD → branch resolved in ID | forwarding | 2 | 1 | 0 | 0 |
| ALU → branch resolved in EX | forwarding | 0 | 0 | 0 | 0 |
| LOAD → branch resolved in EX | forwarding | 1 | 0 | 0 | 0 |

### 5.2 Sequences — the ready-time method (use this for anything with more than one dependence)
Stalls from different dependences **are not simply added**: an earlier stall pushes *all* later instructions back, which changes their distance in time and often satisfies a later dependence for free. Always schedule instruction by instruction.

Let `X_i` be the cycle in which instruction `i` is in EX (1-cycle stages). Instruction 1 has `X_1 = 3` (IF at cycle 1). For `i > 1`:

```
X_i = max( X_{i−1} + 1 ,  gate from every source register's latest producer p )

gate(p) :   no forwarding, RF-A :  X_p + 3        (reader's ID last cycle = producer's WB)
            no forwarding, RF-B :  X_p + 4
            forwarding, p is ALU :  X_p + 1
            forwarding, p is load:  X_p + 2
            forwarding into store data (needed in MEM):  X_i ≥ X_p   (ALU)  or  X_p + 1 (load)
            forwarding into a branch compared in ID:     X_i ≥ X_p + 2 (ALU) or X_p + 3 (load)

total cycles = X_N + 2        (MEM at X_N+1, WB at X_N+2)
stalls       = total − (N + 4)
```

For a **multi-cycle EX** producer, replace `X_p` by the *last* EX cycle of `p`, and `X_{i−1}+1` by the last EX cycle of `i−1` plus one (the unit is busy until then).

### 5.3 Worked example E2 — no forwarding, both register-file timings
```
I1: ADD R1, R2, R3
I2: SUB R4, R1, R5      (reads R1 from I1:  d = 1)
I3: AND R6, R1, R4      (reads R1 from I1 (d = 2) and R4 from I2 (d = 1))
I4: OR  R7, R8, R9      (independent)
```
Ready-time method, RF-A (gate = `X_p + 3`): X1 = 3. X2 = max(4, X1+3 = 6) = 6. X3 = max(7, R1: X1+3 = 6, R4: X2+3 = 9) = 9. X4 = max(10, –) = 10. Total = 10 + 2 = **12 cycles** (`8 + 4` stalls: 2 for I2, 2 for I3, 0 for I4).

```
RF-A (same-cycle read after WB write)
Cycle                   1    2    3    4    5    6    7    8    9    10   11   12
I1 ADD R1,R2,R3         IF   ID   EX   MEM  WB
I2 SUB R4,R1,R5              IF   ID   --   --   EX   MEM  WB
I3 AND R6,R1,R4                   IF   --   --   ID   --   --   EX   MEM  WB
I4 OR  R7,R8,R9                                  IF   --   --   ID   EX   MEM  WB
```
Under RF-B (gate = `X_p + 4`): X2 = 7, X3 = 11 (from R4: 7+4), X4 = 12, total **14 cycles** (6 stalls).
With full forwarding: all gates ≤ the natural slot → 8 cycles, 0 stalls.

**Non-additivity check.** Taken one at a time, I3's R1 dependence alone would cost 1 stall (d = 2) and its R4 dependence alone 2 stalls (d = 1): summing gives 3, but the real cost is 2, because the R4 wait already covers the R1 wait. Rule: **the stall of an instruction is the maximum over its sources, measured after earlier stalls have shifted everything.**

### 5.4 Worked example E3 — forwarding, load-use hazard, and compiler scheduling
Source: `a = b + c; d = e − f;` (all addresses off `R10`), full forwarding, RF-A.

```
Original order: 14 cycles (12 + 2 load-use stalls), CPI = 14/8 = 1.75
Cycle                   1    2    3    4    5    6    7    8    9    10   11   12   13   14
LW R1,0(R10)            IF   ID   EX   MEM  WB
LW R2,4(R10)                 IF   ID   EX   MEM  WB
ADD R3,R1,R2                      IF   ID   --   EX   MEM  WB
SW R3,8(R10)                           IF   --   ID   EX   MEM  WB
LW R4,12(R10)                                    IF   ID   EX   MEM  WB
LW R5,16(R10)                                         IF   ID   EX   MEM  WB
SUB R6,R4,R5                                               IF   ID   --   EX   MEM  WB
SW R6,20(R10)                                                   IF   --   ID   EX   MEM  WB
```
Instruction-level reasoning (what you do in the exam): `ADD` uses `R2` loaded by the *immediately preceding* `LW` → 1 stall; `SW R3` uses ADD's result as store data → 0 (ALU forwarding / MEM-stage need); `SUB` uses `R5` loaded immediately before → 1 stall; the final `SW` → 0. Total `12 + 2 = 14`.

**Reordered by the compiler** (move independent loads up so each load has ≥ 1 instruction before its use):
```
LW R1,0(R10); LW R2,4(R10); LW R4,12(R10); ADD R3,R1,R2; LW R5,16(R10); SW R3,8(R10); SUB R6,R4,R5; SW R6,20(R10)
```
Now `R2` is used 2 instructions after its load, `R5` is used 2 instructions after its load: 0 stalls, **12 cycles**, CPI = 1.5 (only pipeline fill remains: `12/8`). Legality: only instructions with no dependence between them may swap (here the three loads and the ADD/SW chain are independent in the moved positions).

Without forwarding (RF-A) the same two orders take **20** and **16** cycles — scheduling helps there too, but cannot remove everything.

### 5.5 Worked example E4 — stores and branches reading registers
Full forwarding:
* `LW R1,0(R2)` then `SW R1,4(R3)` (adjacent): store *data* is needed in MEM, the load result is available at the end of its MEM → forwarded MEM→MEM, **0 stalls**.
* `LW R1,0(R2)` then `SW R5,4(R1)` (R1 is the store's **address**, needed in EX): **1 stall**.
* `ADD R1,…` then `BEQ R1,…` with the branch compared in **EX**: 0 stalls; compared in **ID**: 1 stall (value not yet produced when ID wants it); `LW R1,…` then `BEQ R1,…`: 1 stall (EX) or **2 stalls** (ID).

### 5.6 Worked example E7 — multi-cycle EX (the PYQ-style "MUL/DIV/ADD" sequences)
Pipeline: IF, ID (reads operands), **EX of 1 cycle for ADD/SUB and 3 cycles for MUL**, WB (4 stages; operand forwarding from the end of EX into the next EX), blocking in-order.

```
I1: MUL R1,R2,R3   I2: ADD R4,R1,R5   I3: SUB R6,R4,R2   I4: MUL R7,R6,R1

Cycle                   1    2    3    4    5    6    7    8    9    10   11
MUL R1,R2,R3            IF   ID   EX   EX   EX   WB
ADD R4,R1,R5                 IF   ID   --   --   EX   WB
SUB R6,R4,R2                      IF   --   --   ID   EX   WB
MUL R7,R6,R1                                     IF   ID   EX   EX   EX   WB
```
Reasoning: I1 occupies EX in cycles 3–5. I2's EX can start at 6 (forwarding from end of cycle 5). I3 sits behind I2 and gets EX at 7 (I2's result forwarded). I4 needs `R6` (I3's, ready after 7) and `R1` (long ready) → EX 8–10, WB at 11. **11 cycles**. Without forwarding (RF-A, read in ID, write in WB) the same sequence takes **14 cycles**.

When the reader fetches operands in **EX itself** (ID only decodes; this is how some questions word it), the relevant gate is: *EX may start in the cycle where the producer is in WB (RF-A)* without forwarding, or *right after the producer's EX* with forwarding. Example (5-stage, EX = 1 cycle for ADD, 3 for MUL):
```
ADD R1,R2,R3 ; MUL R4,R1,R5 ; ADD R6,R4,R7 ; MUL R8,R6,R2     (each depends on the previous)
with forwarding: 12 cycles;  no forwarding, RF-A: 15;  no forwarding, RF-B: 18.
speedup from forwarding = 15/12 = 1.25 (RF-A) or 18/12 = 1.50 (RF-B)
```
*The register-file assumption changes the answer* — a real GATE-style question must state it, and when it does not, state your assumption in the solution.

### 5.7 Stall-counting procedure (step by step)
1. Fix the model: stages, forwarding or not, RF-A/RF-B, where branches resolve, which memory ports exist, multi-cycle units.
2. Write each instruction's destination and source registers (and which are used at EX / MEM / ID).
3. Compute `X_i` by the ready-time method; remember a load's result is later than an ALU result.
4. Add control penalties after the branch (§7) as a delay of the *next fetch*.
5. `total = X_N + 2` (or `(N + k − 1) + stalls`), `CPI = total / N`.
6. Sanity-check against the distance table for each adjacent pair.

---

## 6. Operand forwarding (bypassing) and hazard detection hardware

### 6.1 Idea
The result of an ALU instruction is *already computed* at the end of EX; waiting for WB and a register-file round-trip wastes two cycles. Forwarding copies it directly from a **pipeline register** back to the **ALU input**.

```
                      +--------- forward EX/MEM.ALUout (newest) ---------+
                      |             +---- forward MEM/WB.result (older) --+
                      v             v
 ID/EX.A  ----> [ 3:1 MUX ] ----> ALU input A
 ID/EX.B  ----> [ 3:1 MUX ] ----> ALU input B  --> ALU --> EX/MEM --> MEM --> MEM/WB --> WB
   ^   00 = value read from register file (ID)       ^ ForwardA/ForwardB select lines
   |   10 = from EX/MEM,  01 = from MEM/WB          | produced by the FORWARDING UNIT
```
Required hardware: a wider (3-input) multiplexer on each ALU input, wires from EX/MEM and MEM/WB back to those muxes, and a **forwarding unit** (comparators + logic).

### 6.2 Forwarding conditions (EX hazard, then MEM hazard)
For the instruction currently in EX with source registers `Rs`, `Rt`:
```
ForwardA = 10  if  EX/MEM.RegWrite  and  EX/MEM.Rd ≠ 0  and  EX/MEM.Rd = ID/EX.Rs     (from the instruction one ahead)
         = 01  else if  MEM/WB.RegWrite  and  MEM/WB.Rd ≠ 0  and  MEM/WB.Rd = ID/EX.Rs   (from the instruction two ahead)
         = 00  otherwise                                                                (register-file value)
ForwardB: same with Rt
```
* `Rd ≠ 0` because register 0 is hard-wired to zero and must never be forwarded.
* **Priority to the newest result** (EX/MEM before MEM/WB): in `ADD R1,R1,R2; ADD R1,R1,R3; ADD R1,R1,R4` the third add must see the second add's R1, not the first's, although both match.

Example E5: `I1: ADD R3,R1,R2; I2: SUB R5,R3,R4; I3: AND R6,R3,R5; I4: OR R7,R3,R6`.
* I2 in EX, I1 in MEM: `Rs=R3` matches `EX/MEM.Rd` → ForwardA = 10.
* I3 in EX, I2 in MEM, I1 in WB: `Rs=R3` matches only `MEM/WB.Rd` (I1) → ForwardA = 01; `Rt=R5` matches `EX/MEM.Rd` (I2) → ForwardB = 10.
* I4 in EX, I3 in MEM, I2 in WB: `Rt=R6` → ForwardB = 10; `R3` was produced three instructions earlier, already written in the first half of the cycle I4 was in ID (RF-A) → ForwardA = 00.

### 6.3 Why forwarding cannot fix the load-use hazard
The load's value appears only at the **end of MEM**. The instruction right behind it needs the value at the **start of its EX, which is the same cycle as the load's MEM**. Forwarding can only send values *forward in time*; the value does not exist yet. One bubble is unavoidable:

```
LW  R1,0(R2)    IF ID EX MEM WB
ADD R3,R1,R4       IF ID -- EX MEM WB      value leaves MEM at end of cycle 4, ADD's EX starts cycle 5
                                         (the load's MEM->EX forwarding path is used in cycle 5)
```
Hence: **ALU→ALU needs no stall with forwarding; load→dependent-next-instruction needs exactly 1.**

### 6.4 Hazard detection unit and interlock (stall insertion)
Placed in ID:
```
if ID/EX.MemRead  and  ( ID/EX.Rt = IF/ID.Rs  or  ID/EX.Rt = IF/ID.Rt ):   STALL
```
A **stall** (bubble) is implemented by: (1) **freezing the PC** and the **IF/ID register** (so the same instruction is fetched/decoded again), and (2) **zeroing the control signals** entering ID/EX, which turns the instruction in EX the next cycle into a NOP. This is called a **pipeline interlock**. Without forwarding, the detection unit stalls on *any* match with an instruction still in EX/MEM (and WB under RF-B).

Compilers can also avoid the hazard themselves by scheduling or by inserting NOPs (software interlock; the old MIPS "load delay slot").

### 6.5 What forwarding costs: the clock
Forwarding adds a mux level (and comparator-driven select) in the critical EX stage; the clock period can grow. Whether it pays off is decided by

```
time per instruction = (1 + stalls per instruction) × clock period
```
Example E6: stage delays IF 1.0, ID 1.1, EX 1.2, MEM 1.3, WB 0.9 ns, latch 0.1 ns.
* Without forwarding: clock = 1.3 + 0.1 = 1.4 ns, average stalls 0.5 (data) + 0.2 (control) = 0.7 → 1.7 × 1.4 = **2.38 ns/instr**.
* With forwarding: EX grows by 0.25 ns to 1.45 → clock = 1.45 + 0.1 = 1.55 ns, stalls 0.1 + 0.2 = 0.3 → 1.3 × 1.55 = **2.015 ns/instr**.
* Speedup ≈ 2.38 / 2.015 = **1.18**: forwarding wins although the clock slows by 10.7 %. (If forwarding had stretched the clock beyond about 1.4 × 1.7/1.3 = 1.83 ns, it would have lost.) Always compare the *product*.

---

## 7. Control hazards

### 7.1 The branch penalty
The instruction after a branch is fetched before the branch has been resolved. Number the stages IF=1, ID=2, EX=3, MEM=4. If a branch is **resolved at the end of stage `r`**, then `r − 1` instructions behind it are already in the pipe and (if the guess was wrong) must be flushed:

```
branch penalty  =  r − 1  cycles
resolved in ID : 1      resolved in EX : 2      resolved in MEM : 3
```
```
BEQ (taken), resolved in EX, fetch continues sequentially (predict not taken):
Cycle                   1    2    3    4    5    6    7
BEQ R1,R2,L             IF   ID   EX   MEM  WB
I+1 (wrong path)             IF   ID   xx
I+2 (wrong path)                  IF   xx
L: target                              IF   ID   EX   MEM
```
A branch is a "stall" for exactly the cycles between its own IF and the fetch of the correct next instruction.

**Unconditional jumps, calls, returns.** A jump (`J`, `JAL` = call) knows its target after decode: penalty 1 if the target is computed in ID. A return (`JR RA`) must first *read* a register; if `RA` was just loaded from the stack (`LW RA…; JR RA`) the load-to-branch spacing rules apply (2 extra stall cycles for a branch/jump that consumes a load result in ID). A call also writes the link register (a normal ALU-style result).

### 7.2 Policies for conditional branches
| Policy | What the pipeline does | Penalty when… |
|---|---|---|
| **Stall until resolved** | stop fetching after any branch | always `P` (= `r − 1`) |
| **Predict not taken** | keep fetching sequentially; flush if taken | `P` only when taken |
| **Predict taken** | fetch the target once it is known | wrong when not taken; right-and-taken still pays `T_p` (cycles until target address known, e.g. 1 if computed in ID) |
| **Delayed branch** | execute the next `P` instructions regardless | no flush; slots wasted if not usefully filled |
| **Dynamic prediction** | predict per branch from history | `P` on misprediction |

**Average CPI formulas** (branch frequency `f_b`, fraction taken `p_t`, penalty on resolution `P`, ideal CPI 1):
```
stall always      CPI = 1 + f_b × P
predict not taken CPI = 1 + f_b × p_t × P
predict taken     CPI = 1 + f_b × [ p_t × T_p + (1 − p_t) × P ]      (T_p = cycles to obtain the target)
dynamic, accuracy a   CPI = 1 + f_b × (1 − a) × P   (+ a small T_p term for correctly predicted taken branches if the target is not instantly available)
```
Worked example E8 (`f_b = 0.20`, `p_t = 0.6`):

| P | stall always | predict not taken | predict taken with `T_p = 1` |
|:-:|:-:|:-:|:-:|
| 1 | 1.20 | 1.12 | – |
| 2 | 1.40 | 1.24 | 1.28 |
| 3 | 1.60 | 1.36 | – |

*Predict-taken beats predict-not-taken only if* `p_t > P / (2P − T_p)`. For `P = 2, T_p = 1` that is `p_t > 2/3`; at `p_t = 0.6` predict-not-taken is better (1.24 vs 1.28). Derivation: `p_t T_p + (1 − p_t) P < p_t P` ⇔ `p_t (2P − T_p) > P`.

### 7.3 Resolving earlier — and its hidden cost
Moving the comparison into ID (a dedicated equality comparator) cuts the penalty to 1, but now the branch's operands are needed one stage sooner:

* If the branch depends on the instruction right before it, forwarding into ID is needed and one extra **data** stall appears; with a load-dependence two.
* Measured with the simulator (full forwarding, predict-not-taken, extra cycles over the stall-free count):

| Branch compared in | taken, independent of previous | taken, depends on previous ALU result | not taken, depends on previous ALU result |
|---|:-:|:-:|:-:|
| ID | 1 | **2** (1 data + 1 control) | 1 |
| EX | 2 | 2 | 0 |
| MEM | 3 | 3 | 0 |

So for a *taken* branch that depends on the immediately preceding instruction, resolving in ID gains nothing over EX (2 = 2), and with a preceding **load** (`LW R1,…; BNE R1,…`) ID-resolution costs 2 data + 1 control = 3 and EX-resolution costs 1 + 2 = 3 — **equal**. The benefit of early resolution exists only when the compared registers are ready.

### 7.4 Delayed branches (delay slots)
The architecture defines that the `n` instructions after a branch are **always executed**, whether or not the branch is taken. `n` equals the penalty `P` of the machine (1 slot if resolved in ID, 2 if in EX). The compiler tries to put *useful* instructions in the slots; otherwise it inserts `NOP`s (wasted cycles).

**Where to find a slot filler**
1. **From before the branch** (best; always useful): an instruction `X` that sits before the branch can be moved into the slot iff (a) the branch condition/target does not depend on `X`, and (b) `X` has no RAW, WAR or WAW dependence with any instruction lying between `X` and the branch (so that executing `X` *after* those instructions changes nothing). Typically the instruction just before the branch, if the branch does not use its result, or an earlier fully independent one.
2. **From the target** (useful if the branch is taken): copy the first target instruction into the slot and make the branch go to the second target instruction. If the branch falls through the copy still executes, so it must be harmless then (or the branch must be an *annulling/cancelling* branch that squashes the slot when the prediction is wrong).
3. **From the fall-through path** (useful if not taken): symmetric; harmless if taken, or annulled.

Correct behaviour trace (E9), 1 slot, branch resolved in ID, full forwarding:
```
Original order (branch depends on ADD R1; LW is independent of the branch)
 ADD R1,R2,R3 ; SUB R6,R7,R8 ; LW R4,0(R5) ; BEQ R1,R0,L ; NOP ; L: OR R9,R6,R2 ; XOR R10,R9,R4
 -> 7 instructions (one is the NOP), 11 cycles                                   [taken or not, the NOP executes]

LW moved into the slot (legal: LW is not read by BEQ and nothing between LW and BEQ exists)
 ADD R1,R2,R3 ; SUB R6,R7,R8 ; BEQ R1,R0,L ; LW R4,0(R5) <slot> ; L: OR R9,R6,R2 ; XOR R10,R9,R4
 -> 6 instructions, 10 cycles, no wasted cycle, same result
Same code without a delay slot (hardware stalls 1 cycle on every taken branch): 11 cycles
```
Slot instruction semantic: `LW` executes whether the branch is taken (next is `OR`) or not (next is the fall-through code).

**Trap (verified by simulation):** moving an instruction into the slot can *create* a hazard. Take `ADD R1,R2,R3 ; LW R4,0(R5) ; BEQ R1,R0,L ; NOP ; L: SUB …` (5 instructions, branch compared in ID). The `ADD` is two instructions ahead of the branch, so no data stall: 5 + 4 = **9 cycles**. Move `LW` into the slot: `ADD R1,R2,R3 ; BEQ R1,R0,L ; LW R4,0(R5) ; L: SUB …` (4 instructions). Now the branch is adjacent to its feeder `ADD`, the ID-comparator needs the value one cycle early, 1 data stall appears: 4 + 4 + 1 = **9 cycles** — the "filled" version is *not* faster. Always re-check the distance between a branch and the instruction that produces its operand.

**CPI with delay slots:** if the compiler fills a fraction `u` of slots with useful work and the rest with NOPs: `CPI = 1 + f_b × n × (1 − u)` counted per useful instruction. With one slot, `f_b = 0.15`, 70 % filled: `1 + 0.15 × 0.30 = 1.045`. For `n` slots filled with probabilities `u_1 … u_n`: `CPI = 1 + f_b × Σ (1 − u_j)`.

Drawback: the pipeline depth leaks into the ISA (deeper pipes need more slots, existing binaries break), which is why modern designs rely on prediction.

### 7.5 Static prediction
Fixed rule or compiler hint: always not-taken; always taken; **backward-taken / forward-not-taken** (loops branch backwards and are mostly taken; `if` branches forward and are mostly not taken); or a hint bit in the opcode. No hardware state.

### 7.6 Dynamic prediction: the 1-bit and 2-bit saturating counters
A **branch history table (BHT)**, indexed by low-order bits of the branch address, stores a small state per entry (different branches can alias to the same entry).

**1-bit predictor:** remembers the last outcome. Predict whatever happened last time.

**2-bit saturating counter** (values 0–3):
```
state  meaning            prediction
 00    strongly not-taken   N
 01    weakly   not-taken   N
 10    weakly   taken       T
 11    strongly taken       T

taken      : state = min(state + 1, 3)
not taken  : state = max(state − 1, 0)
```
The prediction changes only after **two consecutive** contrary outcomes (one exception can flip a weak state but not a strong one) — that is the whole point for loops.

Worked example E10: inner loop branch that is taken 4 times then not taken (5 iterations), executed 3 times in a row (outcomes `TTTTN TTTTN TTTTN`).

| # | outcome | 1-bit (start N): state → pred | | 2-bit (start 00): state → pred | |
|:-:|:-:|:-:|:-:|:-:|:-:|
| 1 | T | N → N | **miss** | 00 → N | **miss** |
| 2 | T | T → T | ok | 01 → N | **miss** |
| 3 | T | T → T | ok | 10 → T | ok |
| 4 | T | T → T | ok | 11 → T | ok |
| 5 | N | T → T | **miss** | 11 → T | **miss** |
| 6 | T | N → N | **miss** | 10 → T | ok |
| 7–9 | T,T,T | T → T | ok | 11 → T | ok |
| 10 | N | T → T | **miss** | 11 → T | **miss** |
| 11 | T | N → N | **miss** | 10 → T | ok |
| 12–14 | T | ok | ok | ok | ok |
| 15 | N | T → T | **miss** | 11 → T | **miss** |

Total mispredictions: **1-bit = 6, 2-bit = 5** (the 2-bit one pays 2 warm-up misses and then 1 per loop exit). In the steady state: 1-bit **2 misses per loop execution** (the exit, and the first iteration of the next execution), 2-bit **1 miss per loop execution** (the exit only). Verified: 50 executions of an 8-iteration loop → 99 vs 50 mispredictions.

**Initial state matters:** the same 15-outcome trace gives 2-bit = 3 misses if the counter starts at 11, 4 if it starts at 01, 5 if it starts at 00. For an *alternating* pattern `T N T N …` (10 outcomes): the 1-bit predictor starting at N and the 2-bit counter starting at 01 both mispredict **all 10**, while a 2-bit counter starting at 00 mispredicts 5. Never assume the initial state; use the one given.

### 7.7 Branch target buffer (BTB)
A BHT tells *direction* but the target must still be computed (available after ID: 1 bubble on a correct "taken"). A **BTB** is a small cache indexed by the branch's address that stores the **predicted target address** (and often prediction bits). It is consulted *in IF*, so on a hit the target is fetched in the very next cycle:

| Case | Penalty (branch resolved in EX, P = 2) |
|---|---|
| BTB hit, prediction correct (taken) | 0 |
| BTB hit, prediction wrong | P |
| BTB miss, branch not taken | 0 (fall-through is the default) |
| BTB miss, branch taken | P (and the BTB is updated) |

Worked example E11 (penalty `P = 3`): `f_b = 0.25`; BTB hit rate 80 %; given a hit the prediction is right 90 % of the time; on a miss 60 % of branches are taken. Stall cycles per branch `= 0.8 × 0.1 × 3 + 0.2 × 0.6 × 3 = 0.24 + 0.36 = 0.60`; `CPI = 1 + 0.25 × 0.60 = 1.15`.

### 7.8 Speculative execution and the flush (concept level)
**Speculation** = continuing to fetch (and, in advanced machines, to execute) instructions down the *predicted* path before the branch is resolved. In the simple in-order 5-stage pipeline nothing speculative reaches architectural state before the branch resolves (registers are written in WB, memory in MEM), so recovery is just a **flush**: convert the wrong-path instructions in IF/ID (and ID/EX) into bubbles and redirect the PC. The **flush cost** equals the penalty `P` (number of wrong-path instructions). In deeper pipelines `P` is larger; `CPI = 1 + f_b (1 − a) P`: with `f_b = 0.2`, `a = 95 %` this is 1.02 for `P = 2` but 1.14 for `P = 14` — prediction accuracy matters more as depth grows. Out-of-order processors additionally buffer speculative results (reorder buffer) so wrong-path results can be discarded; only the idea is needed.

### 7.9 Control hazards in a sentence-level cheat sheet
* Penalty = stages between IF and resolution; stall cycles are charged per *mispredicted/flushed* branch.
* A correctly predicted not-taken branch under predict-not-taken is free.
* A delay slot is free only if filled with a useful instruction.
* Dynamic prediction reduces *how often* the penalty is paid; it never reduces `P`, and it cannot make the penalty zero for all branches (cold and mispredicted branches still pay).

---

## 8. Performance formulas with hazards

1. **Pipelined CPI:** `CPI_pipe = CPI_ideal + Σ (frequency_i × stall cycles_i)`; with ideal CPI 1: `1 + Σ f_i s_i`. Sources add: load-use, branches, structural, cache misses.
2. **Execution time:** `T = IC × CPI × τ`; for a finite program `T = (N + k − 1 + total stalls) × τ`.
3. **Speedup over the non-pipelined processor:**
```
Speedup = (CPI_np × τ_np) / (CPI_pipe × τ_pipe)
```
 If the non-pipelined machine needs `k` stage-times per instruction (balanced stages, no latch overhead) and the pipelined clock is unchanged: `Speedup = k / (1 + stalls per instruction)`. State both assumptions. The ideal `k` is reached only when stalls → 0 and `N → ∞`.
4. **Different clocks:** if overhead forces a slower pipelined clock, use the general form with both `CPI` and `τ`.

Worked example E12 (data + control): load frequency 25 %, 40 % of loads are followed immediately by a dependent instruction (1 stall each); branches 20 %, 60 % taken, predict-not-taken, `P = 2`. `CPI = 1 + 0.25×0.40×1 + 0.20×0.60×2 = 1.34`. A non-pipelined machine (CPI 5) at the same clock → speedup `5 / 1.34 = 3.73`. If it ran at 2 GHz and the pipeline only reaches 1.6 GHz: `(5 / 2) / (1.34 / 1.6) = 2.985` — **do not forget the clock ratio**.

Worked example E13 (cache stalls enter the same sum): non-pipelined 2 GHz, CPI 5; pipelined at 1.6 GHz; 25 % memory instructions of which 4 % stall 40 cycles (cache miss); 15 % branches, 60 % of which stall 2 cycles. `CPI = 1 + 0.25×0.04×40 + 0.15×0.60×2 = 1.58`; speedup `= (5/2) / (1.58/1.6) = 2.53`. (Cache details: [05-…/01-PERFORMANCE](../05-MEMORY-INTERFACING-AND-HIERARCHY/).)

Worked example E14 (finite program): `N = 1000`, 5 stages, 300 total stall cycles: `1000 + 5 − 1 + 300 = 1304` cycles.

Worked example E15 (predictor value): branches 25 %, penalty 3 on every branch without a predictor; predictor accuracy 90 %, correct predictions cost 0, wrong ones cost 3 (no extra penalty over the baseline). `CPI_without = 1 + 0.25×3 = 1.75`; `CPI_with = 1 + 0.25×0.10×3 = 1.075`; speedup `= 1.75/1.075 = 1.63`.

---

## 9. Register renaming and out-of-order ideas (concept only)

* **Why:** WAR and WAW are *false* dependences created by reusing a small set of architectural register names. They are not data flow.
* **Register renaming** maps each architectural destination to a fresh **physical register** from a larger pool. After renaming, a later write goes to a different physical register than an earlier read or write of the "same" name, so **WAR and WAW disappear**; **RAW does not** (it is real data flow). Renaming therefore "handles certain kinds of hazards" (the false ones) and is *not* an alternative to compile-time register allocation, nor part of address translation.
* **Forwarding/bypassing** removes the *wait for WB* of a RAW dependence but **cannot remove all RAW stalls** — the load-use bubble remains.
* **Dynamic branch prediction** reduces the *frequency* of control stalls but **cannot eliminate all** control-hazard penalties (mispredictions, cold entries).
* **Out-of-order execution** (scoreboarding / Tomasulo-style dynamic scheduling) lets independent instructions run while others wait; this is where WAR/WAW become real hazards; only the idea is syllabus-relevant.

When a statement says "**all**", "**always**", "**eliminates every**", test it against these counter-examples (load-use for bypassing, mispredicted branch for prediction, true RAW for renaming).

---

## 10. Exceptions and interrupts in a pipeline (concept only)

Several instructions are in flight at once, and different stages can raise exceptions (page fault in IF/MEM, illegal opcode in ID, arithmetic overflow in EX). The machine must be **precise**: the saved state must look as if instructions before the faulting one finished and none after it started.
* Record the exception in a status flag in the pipeline registers and only act on it when the instruction reaches a **commit point** (WB), so earlier instructions (which may raise their own exceptions later in program order) are handled first.
* On the exception: flush all younger instructions, let older ones finish, save the faulting instruction's address (`EPC`), then fetch the handler.
* Delayed branches complicate this: after a branch + delay slot, restart needs both PCs. Interrupts (asynchronous) are taken at an instruction boundary in the same way. See [06-IO-INTERFACE/01-INTERRUPT](../06-IO-INTERFACE/).

---

## 11. PYQ patterns (methods only; no official answers)

| # | Pattern | Recognise by | Recipe | Trap |
|---|---|---|---|---|
| 1 | **Which dependence causes a hazard?** (2026-style) | "Which … dependence … data hazard in a pipelined processor?" with RAR/RAW/WAR/WAW | In-order pipeline: only RAW is a hazard; RAR is not a dependence | Answering "all except RAR" — WAR/WAW need out-of-order/variable-latency |
| 2 | **Classify dependences in a code listing** (2015 Set-3 anti-dependence; sibling mapping has a similar 2024 CS-2 item) | Statements "anti-dependence between I_j and I_k" | §4.2 pairwise table; anti = WAR (earlier **reads**, later **writes**) | Calling WAW "anti"; "an anti-dependence always creates a stall" — in an in-order pipe it does not |
| 3 | **Forwarding statements** (2024 CS-1) | MCQ/MSQ about what forwarding can do | Forwarding copies a result from a later stage's output to an earlier stage's input of a *later* instruction; needs muxes/paths; cannot prevent every stall (load-use) | "No extra hardware needed" is false |
| 4 | **Sequence with variable-latency EX and forwarding vs not** (2021 Set-2, 2015 Set-2, 2007) | MUL/DIV/ADD with different EX cycles, "operand forwarding from PO to OF" | §5.2/5.6: schedule each instruction; the producer's *last* EX cycle gates the consumer | Treating forwarding as "zero stalls" (EX is occupied for several cycles); not stating where registers are read |
| 5 | **CPI/speedup with stall fractions** (2024 CS-2, 2014 Set-1, 2020) | "x % of instructions incur y stall cycles", ideal CPI 1 | `CPI = 1 + Σ f s`; speedup via §8 | Forgetting the clock ratio when the pipelined clock differs; mixing percentage of *branches* with percentage of *all instructions* |
| 6 | **Branch predictor speedup** (2022) | "predictor with accuracy a eliminates stall for correct predictions" | `CPI_old = 1 + f_b P`; `CPI_new = 1 + f_b (1−a) P`; ratio | Double-counting the penalty on wrong predictions (they pay the *same* baseline penalty) |
| 7 | **Old vs new pipeline design, branch stalls** (2014 Set-3) | stage split; "IF stalls until next-IP computed"; compare execution times | Time = IC × CPI × τ for each design; CPI = 1 + f_b × (stages from IF to branch-resolution − 1) after splitting; τ = new max stage | Using the old penalty for the new design; forgetting that τ changes with the split |
| 8 | **Delayed branch statements / legal slot instruction** (2008, delay-slot family) | "which instruction can occupy the delay slot" | §7.4 legality: independent of branch condition and of instructions after it up to the branch | Moving the instruction that produces the branch condition; moving across a dependence |
| 9 | **Concept statements with "all/always"** (2008 Q36, 2012) | "Bypassing can handle all RAW", "renaming eliminates all WAR", "dynamic prediction eliminates control penalty" | Find a counter-example per §9 | Accepting absolute claims |
| 10 | **Memory-stall mix in pipelines** (2020; adjacent 2024 CS-1 CPI/speedup with cache) | Memory instructions with a miss rate and miss penalty added to branch stalls | One CPI sum; separate the percentage of *memory instructions* from the miss rate | Using the miss penalty on all instructions |
| 11 | **Ideal pipeline timing** (adjacent: 2025 Q56, 2023, 2021 Set-1, 2018, 2015 Set-1) | stage delays, latches, "no stalls" | Belongs to [07](../07-INSTRUCTION-PIPELINING/NOTES.md): clock = max stage + latch; time = `(k + N − 1)τ` | Not adding latch delay; using the sum of stage delays |

---

## 12. Traps and misconceptions

1. **Dependence ≠ hazard.** WAR/WAW dependences exist in code but are not hazards in the in-order 5-stage pipe.
2. **Forwarding does not cure everything:** load-use needs one stall; branches need their own treatment.
3. **Adding stalls per dependence** instead of scheduling the sequence (§5.3).
4. **Not stating the register-file timing** (RF-A vs RF-B changes no-forwarding counts by one per dependence).
5. **Counting stalls with the wrong distance:** instructions in between must be independent *and* distance is measured in instructions, but after earlier stalls the time distance is larger.
6. **Branch penalty = r − 1,** not r: resolved in EX costs 2, not 3.
7. **Predict-not-taken costs only on taken branches;** stall-always costs on every branch.
8. **Delay slots are filled from the compiler,** not by hardware; the slot executes irrespective of the outcome.
9. **A filled slot can reintroduce a stall** if it brings the branch next to its feeder (ID-resolved branch).
10. **Dynamic prediction does not remove `P`;** the formula multiplies by the misprediction rate.
11. **Forgetting the clock-period change** when forwarding/branch hardware lengthens a stage, or when speedup is asked between machines with different clocks.
12. **Load-use with store:** a store's *data* from the previous load needs no stall; its *address* does.
13. **Unified memory:** adding 1 stall per load/store ignores the tail (no fetch left to block).
14. **Treating a multi-cycle EX as free:** the unit is busy, later instructions queue behind it.
15. **Initial predictor state ignored** in trace questions.

## 13. Edge cases and assumptions to state in every answer
* Pipeline stages and which stage reads/writes registers.
* Forwarding: none / full / only EX→EX; whether MEM→EX exists; whether the register file is RF-A or RF-B.
* Where branches resolve; whether prediction is static or dynamic; initial predictor state.
* Whether the delay slot is filled; whether NOPs are counted as instructions in CPI.
* Separate or unified memory; structural limits on write ports.
* Whether the "stall cycles" in a question are *per instruction* or *per affected instruction* (percentage of what?).
* First instruction's IF in cycle 1; "completion" = end of WB of the last instruction.
* If the question gives "ideal CPI = 2" or similar, use `CPI = CPI_ideal + stalls`, not `1 + stalls`.

## 14. Connections to other COA topics
* [07-INSTRUCTION-PIPELINING](../07-INSTRUCTION-PIPELINING/NOTES.md): `k + N − 1`, clock period, speedup; this file adds stalls to them.
* [05-MEMORY-INTERFACING-AND-HIERARCHY](../05-MEMORY-INTERFACING-AND-HIERARCHY/): cache miss stalls enter the same CPI sum; IF and MEM share the cache/memory port.
* [04-DESIGN-OF-CONTROL-UNIT](../04-DESIGN-OF-CONTROL-UNIT/): control signals zeroed to make a bubble; forwarding-mux selects.
* [06-IO-INTERFACE](../06-IO-INTERFACE/): precise interrupts.
* [01-INSTRUCTION-SET](../01-INSTRUCTION-SET/) / [02-ADDRESSING-MODES](../02-ADDRESSING-MODES/): load/store, base+offset (address register used in EX), branch target computation.
* Digital Logic: the multiplexers and comparators used for forwarding.

## 15. Existing practice coverage map
(`14-PRACTICE-QUESTIONS/.../08-PIPELINE-HAZARDS/practice.md`, 18 questions; questions are not reproduced.)

| Q# | NOTES section | Skill |
|---|---|---|
| Q1 | §4.1 | RAW definition |
| Q2 | §2, §7.1 | control hazard definition |
| Q3 | §4.1 | WAR definition |
| Q4 | §3 | structural hazard from a single memory port |
| Q5 | §5.1–5.3 | no-forwarding stalls with RF-A, chain of ALU dependences |
| Q6 | §5.1 | forwarding removes ALU→ALU stall |
| Q7 | §5.1, §5.4 | load-use plus cycle count |
| Q8 | §2, §4.3, §3, §6 | MSQ on forwarding, branches, structural, WAW in order |
| Q9 | §7.1 | flush count `r − 1` |
| Q10 | §5.2 + §7.1 | load-use + taken branch penalty |
| Q11 | §3.2 | structural stall CPI |
| Q12 | §7.2, §8 | CPI = 1 + f × P |
| Q13 | §5.4 | rescheduling to remove load-use |
| Q14 | §5.2, §5.4 | spacing a load and its use; not-taken branch free |
| Q15 | §7.4 | delay-slot CPI |
| Q16 | §8 | CPI → execution time with clock |
| Q17 | §5.2, §7.1 | independent filler removes load-use + taken branch |
| Q18 | §3, §6.3, §5.4, §7.3 | MSQ: split memories, load-use, scheduling, ID vs EX resolution |

## 16. Self-check
1. Name the three hazard families and one cure for each.
2. Which of RAW/WAR/WAW can occur in the classic in-order 5-stage pipeline, and why?
3. When can WAW become a real hazard? Give a concrete instruction pair.
4. State the stall count for RAW at distances 1, 2, 3 without forwarding under RF-A and RF-B.
5. Why does a load followed immediately by its user still stall with full forwarding?
6. Compute the extra cycles when `LW` is followed by a branch that compares the loaded register, in ID and in EX.
7. Write the forwarding-unit condition for `ForwardA = 10` and explain the `Rd ≠ 0` and priority rules.
8. What is the branch penalty if branches resolve in MEM? How many instructions are flushed?
9. Compare predict-taken and predict-not-taken: give the break-even taken fraction.
10. Trace a 2-bit saturating counter over `T T N T T N` starting from 01.
11. Why does a delay slot filled with the branch's feeder not help?
12. How do you convert "x % of instructions stall y cycles, clock changed" into a speedup?
