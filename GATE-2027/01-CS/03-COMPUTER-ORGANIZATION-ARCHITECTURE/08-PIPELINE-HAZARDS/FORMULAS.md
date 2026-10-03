# Pipeline Hazards — Formulas and Rules

All formulas assume the conventions of [NOTES.md §1](NOTES.md): 5-stage IF–ID–EX–MEM–WB, in-order, no buffering between stages, separate I/D memory unless stated, ideal CPI 1, register file **RF-A** (written first half / read second half) unless **RF-B** is stated. Ideal-pipeline timing (`k + N − 1`, clock = max stage + latch) is in [../07-INSTRUCTION-PIPELINING](../07-INSTRUCTION-PIPELINING/NOTES.md). Every example below was checked by script.

Contents: [A. Counting cycles](#a-counting-cycles) · [B. Data-hazard stalls](#b-data-hazard-stalls) · [C. Structural hazards](#c-structural-hazards) · [D. Control hazards](#d-control-hazards) · [E. Dynamic prediction](#e-dynamic-prediction) · [F. Performance](#f-performance) · [G. Hardware conditions](#g-hardware-conditions)

---

## A. Counting cycles

### A1. Total cycles with stalls
**Statement:** `total cycles = (N + k − 1) + total stall cycles`; completion = end of WB of the last instruction.
**Symbols:** `N` instructions, `k` stages (5), stalls in cycles.
**Applies when:** stages are 1 cycle each; the first instruction's IF is cycle 1.
**Why:** a stall-free pipeline finishes in `k + N − 1`; each bubble delays every later instruction by one cycle.
**Example:** 8 instructions, 2 load-use stalls: `8 + 5 − 1 + 2 = 14`.
**Misuse:** when an EX stage takes `n > 1` cycles, the extra cycles are not "stalls from hazards" in the formula but still lengthen the total: count them (or schedule explicitly). Using `N × k` instead of `N + k − 1`.

### A2. CPI from cycle counts
**Statement:** `CPI = total cycles / N`; for large `N`, `CPI → 1 + average stalls per instruction`.
**Example:** 12 cycles for 8 instructions → 1.5 (includes the `k − 1 = 4` fill cycles; the long-run CPI would be 1.0 for that stall-free code).
**Misuse:** quoting `CPI = 1 + stalls` for a *short* program — use the cycle count.

### A3. Ready-time recurrence (sequences with several dependences)
**Statement:** with `X_i` = EX cycle of instruction `i` (1-cycle stages), `X_1 = 3`,
```
X_i = max( X_{i−1} + 1 ,  gate over each source's latest producer p )
gate: no forwarding RF-A : X_p + 3        no forwarding RF-B : X_p + 4
      forwarding, ALU p  : X_p + 1        forwarding, load p : X_p + 2
total = X_N + 2
```
**Why:** WB is two cycles after EX; the reader (ID) must be in the producer's WB cycle (RF-A) or after it (RF-B); the instruction occupies EX one cycle after the previous one at the earliest.
**Example:** `ADD R1; SUB R4,R1; AND R6,R1,R4; OR(indep)` without forwarding, RF-A: X = 3, 6, 9, 10 → total 12.
**Misuse:** adding the isolated stalls of each dependence (the maximum matters, after shifting).

---

## B. Data-hazard stalls

### B1. Single-dependence stall rule
**Statement:** `stalls = max(0, H − (d + U))`
**Symbols:** `d` = distance in instructions (1 = adjacent); `H` = offset from the producer's IF cycle at which the value is first usable; `U` = offset from the consumer's IF cycle at which it is used.
| Case | H | U |
|---|:-:|:-:|
| no forwarding, RF-A | 4 | 1 |
| no forwarding, RF-B | 5 | 1 |
| forwarding, ALU result into EX | 3 | 2 |
| forwarding, load result into EX | 4 | 2 |
| forwarding, ALU result into store data (MEM) | 3 | 3 |
| forwarding, load result into store data (MEM) | 4 | 3 |
| forwarding into a branch compared in ID, ALU result | 3 | 1 |
| forwarding into a branch compared in ID, load result | 4 | 1 |
**Applies when:** the dependence is the only thing delaying the consumer.
**Why:** the producer in IF at `t` has ID `t+1`, EX `t+2`, MEM `t+3`, WB `t+4`; the value exists after EX (ALU) or after MEM (load); the consumer, unstalled, uses it at `t + d + U`.
**Example:** load then ALU consumer, `d = 1`, forwarding: `max(0, 4 − 1 − 2) = 1`.
**Misuse:** applying it to a *chain* without re-computing distances after earlier stalls.

### B2. Closed forms (distance tables)
| Model | d = 1 | d = 2 | d = 3 |
|---|:-:|:-:|:-:|
| No forwarding, RF-A | 2 | 1 | 0 |
| No forwarding, RF-B | 3 | 2 | 1 |
| Forwarding, ALU→EX | 0 | 0 | 0 |
| Forwarding, LOAD→EX | 1 | 0 | 0 |
| Forwarding, LOAD→store data | 0 | 0 | 0 |
| Forwarding, ALU→branch in ID | 1 | 0 | 0 |
| Forwarding, LOAD→branch in ID | 2 | 1 | 0 |

Formulas: `max(0, 3 − d)`, `max(0, 4 − d)`, `0`, `max(0, 2 − d)`, `0`, `max(0, 2 − d)`, `max(0, 3 − d)`.

### B3. Load-use rule (with forwarding)
**Statement:** one stall if the instruction immediately after a load uses the loaded register in EX (as ALU operand or address); none if at least one instruction separates them.
**Why:** the loaded word exists only at the end of MEM, but the next instruction needs it at the start of its EX in the same cycle as the load's MEM.
**Misuse:** thinking forwarding removes it; stalling for a store whose **data** (not address) comes from the load.

### B4. Dependence classification
**Statement (i before j):** RAW if `D(i) ∈ S(j)` with no redefinition in between; WAR if `D(j) ∈ S(i)`; WAW if `D(i) = D(j)`. In the in-order 5-stage pipe only RAW is a hazard.
**Example:** `MUL R2,R3,R4` then `ADD R2,R5,R6` → WAW.
**Misuse:** calling a WAW pair "anti"; calling RAR a hazard.

---

## C. Structural hazards

### C1. Unified-memory fetch-slot loss
**Statement:** each load/store in MEM blocks the fetch of one instruction (dead fetch slot): `extra cycles = number of load/store MEM cycles that occur before the last instruction's fetch`.
**Long-run CPI:** `CPI = 1 + f_mem × 1` (`f_mem` = fraction of loads/stores).
**Example:** `LW, ADD, SUB, OR, AND` → `5 + 4 + 1 = 10` cycles; with the load last in a 4-instruction program: no extra cycle.
**Misuse:** adding one cycle to *every* load/store regardless of position.

### C2. Serial multi-cycle EX
**Statement:** with a non-pipelined EX taking `e_i` cycles for instruction `i`, the last instruction finishes no earlier than `2 + Σ e_i + 1` (fill IF, ID; serial EX; WB) in a 4-stage IF–ID–EX–WB pipe, regardless of dependences that forwarding satisfies.
**Example:** EX times 4, 3, 1, 1 → `2 + 9 + 1 = 12`.

---

## D. Control hazards

### D1. Branch penalty
**Statement:** resolved at the end of stage `r` (IF=1, ID=2, EX=3, MEM=4): `P = r − 1` cycles = number of wrong-path instructions flushed.
**Example:** EX → 2 flushed; MEM → 3.
**Misuse:** `P = r`.

### D2. CPI by branch policy
```
stall always       CPI = 1 + f_b × P
predict not taken  CPI = 1 + f_b × p_t × P
predict taken      CPI = 1 + f_b × [ p_t × T_p + (1 − p_t) × P ]
delay slots (n)    CPI = 1 + f_b × Σ_{j=1..n} (1 − u_j)      (u_j = fraction of slot j filled usefully)
```
**Symbols:** `f_b` branch fraction of all instructions; `p_t` fraction of branches taken; `T_p` cycles until the target address is known (e.g. 1 when computed in ID); `u_j` fraction of branches whose slot `j` is useful.
**Example:** `f_b = 0.2, p_t = 0.6, P = 2`: stall 1.40; predict-not-taken 1.24; predict-taken (`T_p = 1`) 1.28; one delay slot with 70 % filled and `f_b = 0.15`: 1.045.
**Misuse:** using `f_b` as the fraction *of branches* that are taken; counting NOPs both as extra instructions and as stall cycles.

### D3. Break-even between predict-taken and predict-not-taken
**Statement:** predict-taken is cheaper iff `p_t > P / (2P − T_p)`.
**Why:** `p_t T_p + (1 − p_t) P < p_t P ⇔ p_t (2P − T_p) > P`.
**Example:** `P = 2, T_p = 1` → `p_t > 2/3`; `P = 3, T_p = 1` → `p_t > 3/5`.
**Misuse:** applying it when the target is not known before the outcome (then `T_p = P` and predict-taken never helps).

### D4. Early resolution with dependent operands
**Statement:** moving resolution from EX to ID saves 1 control cycle *only if* the compared registers are ready; for a branch right after its producer the extra data stall cancels the gain (taken branch: 2 vs 2 after an ALU producer; 3 vs 3 after a load).
**Misuse:** assuming ID-resolution is always better.

### D5. Flush cost in deeper pipelines
**Statement:** `P` grows with the depth of the resolution stage; `CPI = 1 + f_b (1 − a) P`. Example `f_b = 0.2, a = 0.95`: `P = 2` → 1.02; `P = 14` → 1.14.

---

## E. Dynamic prediction

### E1. 1-bit predictor
State = last outcome; predict it again. A loop branch taken `n − 1` times then not taken: **2 mispredictions per execution** of the loop (exit, and first iteration of the next execution) in the steady state.

### E2. 2-bit saturating counter
States 00, 01 predict not-taken; 10, 11 predict taken. Taken: `s ← min(s+1, 3)`; not-taken: `s ← max(s−1, 0)`. Loop branch: **1 misprediction per execution** (exit only) once warmed up.
**Example:** `TTTTN` repeated 3 times: 1-bit from N → 6 mispredictions; 2-bit from 00 → 5 (from 01 → 4, from 11 → 3); alternating `T N T N …` ×10: 1-bit from N → 10, 2-bit from 01 → 10, 2-bit from 00 → 5.
**Misuse:** ignoring the initial state; thinking the 2-bit counter always beats the 1-bit counter (alternating patterns).

### E3. Effective CPI with prediction
`CPI = 1 + f_b × (1 − a) × P` (accuracy `a`; correct predictions cost 0). With a BHT only, a correctly predicted *taken* branch still costs `T_p` (target from ID). With a BTB hit the target is available in IF.
**BTB example** (penalty 3): hit rate 0.8, accuracy-on-hit 0.9, miss-taken fraction 0.6, `f_b = 0.25`: stalls/branch `0.8×0.1×3 + 0.2×0.6×3 = 0.60` → `CPI = 1.15`.

---

## F. Performance

### F1. Pipelined CPI
`CPI_pipe = CPI_ideal + Σ f_i s_i` (`f_i` = fraction of *all* instructions with event `i`, `s_i` = stall cycles per such instruction).
**Example:** loads 25 % (40 % followed immediately by a use, 1 stall), branches 20 % (60 % taken, P = 2): `1 + 0.10 + 0.24 = 1.34`.
**Misuse:** multiplying by the fraction of *loads* that stall without multiplying by the load frequency.

### F2. Execution time
`T = IC × CPI × τ`; finite program: `T = (N + k − 1 + S) τ`, `S` total stalls.

### F3. Speedup over a non-pipelined machine
`Speedup = (CPI_np × τ_np) / (CPI_pipe × τ_pipe)`.
With `CPI_np = k` stage-times at the same clock: `Speedup = k / (1 + s)` (`s` = stall cycles per instruction).
**Example:** `5/1.34 = 3.73`; with clocks 2 GHz → 1.6 GHz: `(5/2)/(1.34/1.6) = 2.985`.
**Misuse:** dropping the clock ratio; applying `k/(1+s)` when the pipelined clock differs.

### F4. Mixed stalls (hazards + cache)
`CPI = 1 + f_mem × m × M + f_b × q × P + …` (`m` miss rate, `M` miss penalty, `q` fraction of branches that stall).
**Example:** `1 + 0.25×0.04×40 + 0.15×0.6×2 = 1.58`; speedup vs (CPI 5 @ 2 GHz) with pipeline at 1.6 GHz: `2.53`.

### F5. Predictor speedup
`Speedup = (1 + f_b P) / (1 + f_b (1 − a) P)` when correct predictions remove the whole penalty and wrong ones pay `P`.
**Example:** `f_b = 0.25, P = 3, a = 0.9`: `1.75/1.075 = 1.63`.

### F6. Forwarding versus clock period
Forwarding is worth it iff `(1 + s_fwd) τ_fwd < (1 + s_no) τ_no`.
**Example:** `(1.3)(1.55) = 2.015` ns/instr vs `(1.7)(1.4) = 2.38` ns/instr → 1.18× faster although τ grew 10.7 %. Remember τ is the *maximum* stage + latch, so the stretched EX may or may not be the critical stage.

---

## G. Hardware conditions

### G1. Forwarding unit
```
ForwardA = 10 if EX/MEM.RegWrite ∧ EX/MEM.Rd ≠ 0 ∧ EX/MEM.Rd = ID/EX.Rs
         = 01 elif MEM/WB.RegWrite ∧ MEM/WB.Rd ≠ 0 ∧ MEM/WB.Rd = ID/EX.Rs
         = 00 otherwise                      (ForwardB with Rt)
```
Newest value has priority; `Rd = 0` never forwarded.

### G2. Load-use hazard detection (in ID)
`ID/EX.MemRead ∧ (ID/EX.Rt = IF/ID.Rs ∨ ID/EX.Rt = IF/ID.Rt)` ⇒ freeze PC and IF/ID, zero the control signals into ID/EX (bubble).

### G3. Number of delay slots
`n = P` (1 for ID resolution, 2 for EX resolution); filler from before the branch is always useful if it is independent of the branch condition and of every instruction between it and the branch.
