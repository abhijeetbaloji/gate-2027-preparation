# Instruction Pipelining — Notes (ideal pipeline model and stage-level timing)

## 0. Where this fits

**Syllabus line (GATE CS COA):** "… Instruction pipelining, pipeline hazards."
This folder owns the **ideal-pipeline model**: how many cycles, how many nanoseconds, what speedup, what clock, what CPI.
The sibling folder [`../08-PIPELINE-HAZARDS`](../08-PIPELINE-HAZARDS/) owns *why* a pipeline stalls (structural / data / control hazards, forwarding, stall counting, branch prediction, delay slots). Here a stall is only a *number you are given* (for example "20 % of instructions lose 2 cycles").

| Before this topic | After this topic |
|---|---|
| [`../01-INSTRUCTION-SET`](../01-INSTRUCTION-SET/) (what an instruction does, register vs memory operands) | [`../08-PIPELINE-HAZARDS`](../08-PIPELINE-HAZARDS/) (stalls, forwarding, branch handling) |
| [`../04-DESIGN-OF-CONTROL-UNIT`](../04-DESIGN-OF-CONTROL-UNIT/) (multi-cycle control: instruction = several micro-steps) | [`../05-MEMORY-INTERFACING-AND-HIERARCHY/01-PERFORMANCE`](../05-MEMORY-INTERFACING-AND-HIERARCHY/01-PERFORMANCE/) (cache-miss stalls added to CPI) |
| [`../../02-DIGITAL-LOGIC/02-DESIGN-OF-COMBINATIONAL-AND-SEQUENTIAL-CIRCUITS`](../../02-DIGITAL-LOGIC/02-DESIGN-OF-COMBINATIONAL-AND-SEQUENTIAL-CIRCUITS/) (registers/latches, clock period = logic delay + register delay) | [`../../08-OPERATING-SYSTEMS/08-MEMORY-MANAGEMENT-AND-VIRTUAL-MEMORY`](../../08-OPERATING-SYSTEMS/08-MEMORY-MANAGEMENT-AND-VIRTUAL-MEMORY/) (TLB position in the memory stage) |

**Conventions used throughout (same as the rest of the COA folder)**

```
k      = number of pipeline stages            N = number of instructions
t_i    = combinational delay of stage i        d = pipeline-register overhead per stage (setup + clk-to-Q)
T_p    = pipeline clock period = max(t_i) + d  T_np = time of ONE instruction on the non-pipelined machine
Iron law : CPU time = IC × CPI × clock period = IC × CPI / f
Ideal k-stage pipeline, N instructions, no stalls : (k + N − 1) cycles
CPI_pipelined = 1 + (average stall cycles per instruction)
Classic 5-stage RISC: IF, ID/RF, EX, MEM, WB.  Register file: written in 1st half of a cycle, read in 2nd half (matters only for hazards; see sibling).
1 K = 2^10, 1 M = 2^20, 1 G = 2^30 (a clock "1 GHz" means 10^9 Hz — GHz/ns are decimal).
```

---

## 1. Evidence snapshot (what drives the depth of each section)

Counted from the mapping file [`questions.md`](../../13-PYQ-TOPIC-MAPPING/03-COMPUTER-ORGANIZATION-ARCHITECTURE/07-INSTRUCTION-PIPELINING/questions.md): **16 mapped entries (2008–2025), 13 distinct questions** (the 2013 five-stage question is printed four times, once in each booklet). One entry is misfiled (a DMA question). Several mapped entries are really hazard questions (see [`PYQ.md`](PYQ.md)). The **sibling mapping** holds about a dozen further *ideal-pipeline timing* questions (latency/latch/CPI/stall-speedup numerics) that belong to the model taught here — so the numerical skills below are far more heavily examined than this folder's own mapping suggests.

| Section | Weight | Evidence |
|---|---|---|
| §4–§5 k+N−1, speedup variants, clock = max + overhead | **HIGH-VALUE** | Stage-delay → clock/frequency/speedup entries (2016 ×2, 2014 Set-3, 2011) in this mapping; same pattern fills the sibling mapping (2025, 2023, 2021, …). Practice Q2–Q13, Q15–Q16, Q19–Q20. |
| §6 Splitting a stage, unbalanced stages, diminishing returns | **HIGH-VALUE** | 2016 ×2 are literally "split the slowest stage"; practice Q12, Q13, Q16, Q19. |
| §8 CPI / iron law / instruction mix / frequency comparison | **HIGH-VALUE** | 2025 CS-2 (mix → clock period), 2014 Set-1 (CPI vs frequency); practice Q17. Sibling mapping: many "speedup with stall %" items. |
| §7.1–§7.2 multi-cycle stage, in-order table of cycles | **MEDIUM** | 2009 (table of cycles per stage; table partly missing in the mapping); practice Q18; several sibling-mapping items (variable PO/EX cycles). |
| §3 Gantt reading, completed-by-cycle counting | **MEDIUM** | Practice Q15, Q4, Q9; prerequisite for every other section. |
| §7.3 Non-linear pipeline (reservation table, MAL) | **MEDIUM-LOW** | One mapped entry (2015); its table is missing in the mapping, so only the method is taught. |
| §9.1 Taken branch, fetch stalls (stage-level timing) | **MEDIUM** | 2013 (4 booklets, 1 question) — shared with the hazards sibling. |
| §9.2 TLB/cache position in the memory stage | **LOW** | One conceptual entry (2008). |
| §10 Arithmetic pipeline, superscalar paragraph | **LOW** | Not examined in the mapped entries or the practice file; concept paragraph only. |

**Practice-file skills that NOTES must supply (existing `practice.md`, Q1–Q20):** k+N−1 cycle count; speedup Nk/(k+N−1); unbalanced stages (sum / max); register overhead with non-pipelined time *without* overhead; clock = max + overhead; asymptotic speedup; replacing a stage by two; smallest k for a target speedup; instructions completed in the first C cycles; CPI/frequency speedup; extra EX cycles that stall the pipeline; tricky "is the old clock still valid" traps. Everything is covered below; the coverage map is in §16.

---

## 2. Intuition and mechanism

### 2.1 Laundry / assembly line

Washing (30 min) → drying (30 min) → folding (30 min). One load takes 90 min start to finish. If you wait for each load to finish before starting the next, 4 loads take 360 min. If, the moment load 1 moves to the dryer, load 2 enters the washer, then the machines work in parallel:

```
time (min) :  0    30    60    90   120   150   180
washer     : [L1] [L2]  [L3]  [L4]
dryer      :      [L1]  [L2]  [L3]  [L4]
folder     :            [L1]  [L2]  [L3]  [L4]
                                              ↑ all 4 done at 180 min = (3 + 4 − 1) × 30
```

Three facts to carry forward:

1. One load still takes 90 min (**latency is not reduced**).
2. After the first load, a load finishes every 30 min = the length of the **slowest** step (**throughput** = 1 per 30 min).
3. The first 2 slots and last 2 slots are partly empty (**fill** and **drain**), which is why speedup < number of stages for finite N.

### 2.2 Non-pipelined versus pipelined processor

A non-pipelined (single-cycle or multi-cycle) processor finishes one instruction before starting the next. A pipelined processor cuts the instruction's work into k stages separated by **pipeline registers**; every clock edge each instruction moves one stage forward, so up to k instructions are in flight, each in a different stage.

```
Non-pipelined (multi-cycle, one instruction at a time)
 I1: IF ID EX ME WB
 I2:                IF ID EX ME WB
 I3:                               IF ID EX ME WB      → 3 instr in 15 cycles

Pipelined
 I1: IF ID EX ME WB
 I2:    IF ID EX ME WB
 I3:       IF ID EX ME WB                              → 3 instr in 7 cycles = 5 + 3 − 1
```

### 2.3 The instruction-processing stages

Generic model: any instruction is split into **k** stages, each doing one piece of work in one clock. Classic 5-stage RISC pipeline:

| Stage | Work | Main hardware |
|---|---|---|
| IF | Fetch instruction at PC; compute PC + 4 | PC, instruction memory / I-cache |
| ID (RF) | Decode; read source registers; sign-extend immediate; generate control signals | register file (read ports), control |
| EX | ALU operation, or effective-address computation, or branch compare/target | ALU |
| MEM | Data-memory read (load) or write (store) | D-cache / data memory (and its TLB) |
| WB | Write result into the register file | register file (write port) |

What each instruction class does in each stage (a **fixed-length** pipeline: every instruction passes through all five stages even if a stage has nothing to do for it — this is why the ideal CPI is exactly 1):

| Class | IF | ID | EX | MEM | WB |
|---|---|---|---|---|---|
| ALU reg-reg | fetch | read Rs, Rt | ALU op | idle (value passes through) | write Rd |
| Load | fetch | read base | address = base + offset | read memory | write loaded value |
| Store | fetch | read base, data | address | write memory | idle |
| Branch | fetch | read operands | compare / target | (PC update in some designs) | idle |

Other textbooks name the stages FI, DI, FO, EI, WO (fetch instruction, decode instruction, fetch operand, execute, write operand) or IF, ID, OF, PO, WB. The number and names change from question to question; the **model is the same**: you are always told how many cycles/ns each stage needs.

### 2.4 Pipeline registers: what they hold and why they cost time

Between every pair of stages there is a bank of flip-flops/latches clocked together. Its job is to **freeze the outputs of stage i for one cycle** so stage i+1 can use them while stage i starts on the *next* instruction.

```
 PC →[IF]→ IF/ID →[ID]→ ID/EX →[EX]→ EX/MEM →[MEM]→ MEM/WB →[WB]
          │          │            │              │
 IF/ID  : instruction word, PC+4
 ID/EX  : PC+4, register values A and B, sign-extended immediate, destination-register number, control bits for EX/MEM/WB
 EX/MEM : ALU result, store data (B), compare/zero flag, destination-register number, control bits for MEM/WB
 MEM/WB : data read from memory, ALU result (carried past MEM), destination-register number, control bits for WB
```

Notes: (a) control bits and the destination-register number travel **with** the instruction through every latch, otherwise WB would not know where to write; (b) a store's data value rides in EX/MEM; (c) a register bank adds delay **d = setup time + clock-to-Q delay (+ skew)** to every stage, so a stage's usable time per cycle is `t_i + d`. That overhead is what keeps real speedup below k even with perfectly balanced stages.

---

## 3. Space-time (Gantt) diagrams, latency and throughput

### 3.1 Reading the diagram

Columns = clock cycles, rows = instructions (or stages). A cell shows which instruction is in which stage in that cycle.

```
k = 5, N = 4, no stalls
cycle :   1   2   3   4   5   6   7   8
I1    :  IF  ID  EX  ME  WB
I2    :      IF  ID  EX  ME  WB
I3    :          IF  ID  EX  ME  WB
I4    :              IF  ID  EX  ME  WB
          └ fill ─────┘   └─ drain ──┘
busy stages per cycle: 1 2 3 4 4 3 2 1     (steady state would be 5)
```

The same data by **stage** (a stage-time diagram; useful for utilisation and for multi-cycle stages):

```
cycle :   1   2   3   4   5   6   7   8
IF    :  I1  I2  I3  I4
ID    :      I1  I2  I3  I4
EX    :          I1  I2  I3  I4
MEM   :              I1  I2  I3  I4
WB    :                  I1  I2  I3  I4
```

Rules you can read off:

- Instruction i (1-indexed) is in stage s during cycle `i + s − 1`.
- Instruction i **completes** at the end of cycle `k + i − 1`; the **first** completes at cycle k, then one per cycle.
- Total cycles for N instructions = completion cycle of the last = `k + N − 1`.
- In the first k−1 cycles the pipe is filling; in the last k−1 draining.

### 3.2 Latency versus throughput

```
Latency of one instruction  = k × T_p                 (time from entering IF to leaving WB)
Throughput (steady state)   = 1 / T_p  instructions per unit time
```

- **Pipelining does not reduce the latency of an instruction compared with the non-pipelined machine** — it increases it, because every stage is stretched to the slowest stage and each stage pays register overhead: `k·T_p = k·(max t_i + d) ≥ Σ t_i + k·d ≥ T_np`.
- It **increases throughput**: from 1/T_np to 1/T_p instructions per unit time.
- Nuance: *within* two pipelines, deepening an unbalanced one can lower the latency (faster clock × more stages) — see Example 3 in §6. Never conclude "latency drops" relative to the non-pipelined machine.

---

## 4. Derivations

### 4.1 Total cycles = k + N − 1

The first instruction needs k cycles (it must pass all k stages). Once it enters stage 2, the next instruction enters stage 1, so from then on one instruction **leaves** the last stage per cycle, assuming no stall. The remaining N − 1 instructions therefore finish one per cycle after the first:

```
cycles = k  +  (N − 1)
         └ first instruction     └ each of the other N − 1 adds exactly one cycle
time   = (k + N − 1) × T_p
```

Sanity checks: N = 1 → k cycles (no overlap); N → ∞ → ≈ N cycles (CPI → 1). This is also the **ideal CPI formula**: `CPI_pipe = (k + N − 1)/N = 1 + (k − 1)/N → 1`.

Instruction-count facts that GATE likes:

```
cycle at which the i-th instruction completes : k + i − 1
instructions completed within the first C cycles (stall-free, started empty) : max(0, C − k + 1)
instructions that have *entered* the pipe within C cycles : C   (if C ≤ N)
busy stages in cycle c (stall-free, N ≥ k) : c for c ≤ k ; k for k ≤ c ≤ N ; N + k − c for N ≤ c ≤ N + k − 1
```

### 4.2 The four speedup formulas — state which one you are using

Speedup S = (time on non-pipelined machine) / (time on pipelined machine) for the **same N instructions**.

**(V1) Same clock, non-pipelined takes k cycles per instruction** (the "idealised textbook" case)

```
S = N·k / (k + N − 1)          (cycles; clock cancels)
S → k  as N → ∞                 S < k for every finite N
```

**(V2) Different times** — non-pipelined instruction time T_np, pipelined clock T_p (the general GATE case)

```
S = N·T_np / ((k + N − 1)·T_p)
```

**(V3) Asymptotic / steady-state speedup** (the question says "steady state", "very large N", "ideal conditions", or "approximate speedup in steady state")

```
S_∞ = T_np / T_p
```

Balanced stages and no register overhead: T_np = k·T_p so S_∞ = k.
Unbalanced stages: `S_∞ = Σ t_i / max t_i` (zero overhead) — the pipeline is limited by its slowest stage.
With overhead: `S_∞ = Σ t_i / (max t_i + d)` **if** the non-pipelined machine has no pipeline registers (the standard assumption — see §5.1).

**(V4) CPI / frequency form** (instruction counts equal, N large)

```
S = (CPI_np / f_np) / (CPI_pipe / f_pipe) = (CPI_np × f_pipe) / (CPI_pipe × f_np)
with CPI_pipe = 1 + average stall cycles per instruction
```

V1 is V2 with T_np = k·T_p. V3 is V2 with N → ∞. V4 is V2 written per instruction.

### 4.3 Efficiency, throughput, utilisation

```
Efficiency   η = S / k                       (fraction of the ideal k-fold speedup achieved)
For V1:  η = N / (k + N − 1)  =  (stage-slots used) / (stage-slots available)
Throughput   = N / ((k + N − 1)·T_p)  → 1/T_p  as N → ∞      (instructions per unit time; mind ns vs s)
Stage utilisation in steady state (unbalanced stages, same clock):  U_i = t_i / T_p   (the slowest stage has U = 1 − d/T_p)
```

Why η = N/(k+N−1) for V1: the Gantt chart has k rows × (k+N−1) columns of slots, of which exactly N·k are busy (each instruction occupies each stage once).

**How large must N be?** Set η = f (a target fraction of k): `N k/(k+N−1) = f k → N = f(k−1)/(1−f)`.

```
Half of the ideal speedup (S = k/2):   N = k − 1
90 % efficiency:                       N = 9(k − 1)           (k = 5 → N = 36)
```

Check with k = 5 (V1): N = 4 → S = 20/8 = 2.5 = k/2 ✓; N = 36 → S = 180/40 = 4.5, η = 0.9 ✓; and the number of instructions completed in the first 30 cycles is 30 − 5 + 1 = 26, the 7th instruction completes at cycle 5 + 7 − 1 = 11.

### 4.4 Why the asymptotic speedup caps at k (and at T_np/d)

With balanced stages and register overhead d, splitting T = T_np into k equal stages gives `T_p = T/k + d`, so

```
S_∞(k) = T / (T/k + d) = k·T / (T + k·d)  <  k      and      S_∞(k) → T/d  as k → ∞
```

Adding stages helps with diminishing returns; the register overhead sets a hard ceiling `T/d`. (Real designs also lose to hazards; see §6.3.)

---

## 5. Clock period, frequency and what "non-pipelined time" means

### 5.1 Clock period

```
T_p = max(t_1, …, t_k) + d          f = 1 / T_p
```

Every stage must fit in one clock; the slowest decides. If the question says "pipeline registers have zero latency" or "ignore delays in the pipeline registers", d = 0. If the delay is given **per register** and registers sit after each stage, d is added **once per cycle** (not once per register in the whole pipe). Do not add d to the *sum* of stage delays for the non-pipelined time unless the question says the non-pipelined machine also has registers.

### 5.2 How the non-pipelined time is defined — exact assumption to state

| Variant | T_np | T_p | Use when |
|---|---|---|---|
| A. No overhead | Σ t_i | max t_i | "ignore register delays", "zero latency" |
| B. Overhead only in pipeline (standard) | Σ t_i (no registers in a non-pipelined design) | max t_i + d | "registers of delay d between stages", non-pipelined machine described as just the combinational logic |
| C. Overhead in both | Σ t_i + d (one register at the end) or whatever the question defines | max t_i + d | only if explicitly stated |
| D. Cycle-count world | k cycles of the pipeline clock | one cycle | "non-pipelined takes k cycles per instruction on the same clock" (V1) |
| E. Given directly | e.g. "non-pipelined: 36 ns per instruction" or CPI_np with its own f_np | from stages | use as stated |

When a question is silent, write the assumption in your working: "non-pipelined time = Σ combinational delays (no registers)". In an exam, check whether the figure shows registers also in the non-pipelined version; absent evidence, use B.

### 5.3 Worked Examples 1 and 2 (verified)

**Example 1 — straight k+N−1.** k = 4 stages, clock 3 ns, N = 10, no stalls. Non-pipelined: 4 stages × 3 ns = 12 ns per instruction.

```
cycles   = 4 + 10 − 1 = 13
time     = 13 × 3 ns  = 39 ns
non-pipe = 10 × 12 ns = 120 ns
S        = 120 / 39   = 3.08       (not 4: fill/drain loss; asymptote is 4)
```

**Example 2 — unbalanced stages with register overhead (Variant B).** Stage delays 120, 180, 150, 90, 160 ps; every pipeline register adds 20 ps; N = 1000; no stalls.

```
T_p   = max(120,180,150,90,160) + 20 = 200 ps
T_np  = 120+180+150+90+160            = 700 ps          (no registers)
time  = (5 + 1000 − 1) × 200 ps = 1004 × 200 = 200 800 ps = 200.8 ns
non-pipe time = 1000 × 700 ps = 700 000 ps
S     = 700 000 / 200 800 = 3.486
S_∞   = 700 / 200 = 3.5            (not 5: slowest stage 180 + 20 overhead)
η     = 3.486 / 5 = 0.697
Stage utilisation (t_i / T_p): 0.60, 0.90, 0.75, 0.45, 0.80 → the 180-ps stage is the busy one
Latency of one instruction = 5 × 200 = 1000 ps  (vs 700 ps non-pipelined: latency went UP)
Throughput = 1 / 200 ps = 5 instructions per ns (steady state)
```

---

## 6. Unbalanced stages, splitting a stage, diminishing returns

### 6.1 The slowest stage is the whole story

Speeding up (or ignoring) any stage other than the slowest changes nothing about throughput. To raise the clock rate you must shorten **the longest stage** — and after you do, the *next* longest stage becomes the limit.

**Rule for "split the longest stage into two":**

1. Replace the longest stage t_max by two stages of the stated delays (equal halves t_max/2 unless told otherwise).
2. Recompute `new T_p = max(all stages after the split) + d`. Note d is paid again by **every** stage including the two new ones.
3. Throughput ratio = old T_p / new T_p. "Throughput increase %" = (old T_p / new T_p − 1) × 100. Frequency ratio is the same ratio.

### 6.2 Worked Examples 3 and 4

**Example 3 — throughput gain from splitting (d = 0 and d = 50 ps).** Stage delays 700, 400, 500, 300 ps. Replace the 700-ps stage by two stages 450 ps and 250 ps.

```
d = 0   : old T_p = 700 ps ; new stages 450, 250, 400, 500, 300 → new T_p = 500 ps
          throughput increase = 700/500 − 1 = 40 %
d = 50  : old T_p = 750 ; new T_p = 500 + 50 = 550
          throughput increase = 750/550 − 1 = 36.4 %
Trap    : 450 is smaller than 700, but the pipe is now limited by the 500-ps stage, not by 450.
Latency : old 4 × 700 = 2800 ps, new 5 × 500 = 2500 ps  → latency fell here only because the unbalanced pipe got faster;
          both are still above the non-pipelined sum 1900 ps.
```

**Example 4 — frequency from stage ratios.** Four stages are in the ratio 5 : 8 : 6 : 4 and the pipeline runs at 2.5 GHz with zero register delay. The longest stage (ratio 8) is split into two equal halves.

```
Longest stage = 1/2.5 GHz = 0.4 ns → one ratio unit = 0.05 ns → stages 0.25, 0.40, 0.30, 0.20 ns
Split 0.40 → 0.20 + 0.20: stages 0.25, 0.20, 0.20, 0.30, 0.20 → longest = 0.30 ns
new f = 1/0.30 ns = 3.33 GHz     (not 5 GHz: the 0.30-ns stage now limits)
```

### 6.3 Diminishing returns and the optimal depth idea (concept; not a standard GATE computation)

With balanced stages `S_∞(k) = k·T/(T + k·d)`: each extra stage buys less than the previous one (concave, bounded by T/d).

**Example 5 — table of diminishing returns** (T = 90 ns, d = 3 ns):

```
k     :   1      5       10     15     30
S_∞   :  0.97   4.29    7.50   10.0   15.0        ceiling T/d = 30
```

In a real machine hazards add a penalty that grows with depth (a flush costs about k − 1 cycles). A simple model: a fraction p of instructions cause a flush of (k − 1) cycles:

```
time per instruction = (T/k + d) × (1 + p·(k − 1))
minimised at         k* = √( T·(1 − p) / (d·p) )
```

Verified example: T = 64 ns, d = 1 ns, p = 0.10 → k* = √(64·0.9/(1·0.1)) = √576 = 24, giving 12.1 ns/instruction.
Samples (ns per instruction): k = 4 → 22.1; 8 → 15.3; 16 → 12.5; 24 → **12.1**; 32 → 12.3; 64 → 14.6.
The message: "deeper is better" stops being true once hazard penalties and register overhead dominate. GATE asks the simple version (k, d → speedup) far more often than the optimum.

### 6.4 Replicating a slow stage (parallel units)

If one stage is 2× slower than the rest, you can **replicate** it m times and dispatch instructions round-robin; each copy then needs only to accept an instruction every m cycles, so the stage behaves like a stage of delay t/m (assuming consecutive instructions are independent).

**Example 6 — replication.** Stages 4 ns, 10 ns, 5 ns (zero overhead), 100 independent instructions.

```
Single copy : clock = max = 10 ns, 3 stages → (3 + 99) × 10 ns = 1020 ns
Two copies of the 10-ns stage (round-robin): each copy gets a new instruction only every 2 cycles, so run
  the pipeline at the 5-ns clock; the 10-ns unit is a 2-cycle stage → cycle pattern (1, 2, 1), latency 4 cycles
  → (4 + 99) × 5 ns = 515 ns      (verified with a cycle-by-cycle simulation: no stall occurs)
```

Replication roughly halves the time here because the 10-ns stage was the only thing limiting the clock; the new limit is the 5-ns stage. Replication needs independent consecutive instructions and extra hardware.

### 6.5 Arithmetic pipelines

See §10: the same k + N − 1 logic applies to pipelining a floating-point adder across a stream of operand pairs.

---

## 7. Non-uniform timing

### 7.1 One multi-cycle stage (closed form)

Suppose instruction i takes `c_i` cycles in **one particular stage** (say PO/EX) and exactly **one** cycle in every other stage; stages are in order, no overtaking, the multi-cycle stage is not pipelined internally (an instruction occupies it for all c_i cycles), and no other stalls exist. The multi-cycle stage is never starved (the stages before it can deliver an instruction every cycle) and never blocks the stages after it (it releases at most one instruction per cycle). So it is busy continuously from the cycle the first instruction arrives:

```
total cycles = (stages before it) + Σ c_i + (stages after it)  =  k − 1 + Σ c_i
             = (k + N − 1) + Σ (c_i − 1)                            ← "ideal + extra cycles"
```

This holds wherever the multi-cycle stage is (first, middle or last), and with or without buffers between stages. The extra `Σ(c_i − 1)` is the number of stall cycles the slow stage injects into the front of the pipe.

**Example 7 — variable-latency EX.** k = 5, N = 60. In the EX stage 40 instructions take 1 cycle, 15 take 2 cycles, 5 take 4 cycles; other stages 1 cycle.

```
Σ(c_i − 1) = 15×1 + 5×3 = 30
total = (5 + 60 − 1) + 30 = 94 cycles
(the plain Σc_i form: k − 1 + Σc_i = 4 + (40 + 30 + 20) = 94 ✓)
CPI = 94/60 = 1.567
```

**When the closed form fails:** two or more multi-cycle stages, or a stage whose delay depends on the previous instruction. Use §7.2.

### 7.2 General in-order schedule (table of cycles per stage)

Table `t[i][s]` = cycles instruction i spends in stage s (a 2009-style entry gives such a table; the version in the mapping is incomplete, so no numbers from it are used here). Two timing models:

```
(Buffered / infinite buffers between stages)           (Blocking / no buffers — GATE's usual Gantt)
 start[i][s] = max( finish[i][s−1], finish[i−1][s] )    start[i][s] = max( finish[i][s−1], leave[i−1][s] )
 finish[i][s] = start[i][s] + t[i][s]                   where leave[i−1][s] = start[i−1][s+1]   (previous instruction leaves
                                                          stage s only when it enters s+1; for the last stage leave = finish)
total cycles = finish[N][last stage]
```

Buffered ≤ blocking in total time. Blocking is the picture where an instruction **stays in its stage** (holding it) until the next stage is free — this is what "the pipeline stalls" means in Gantt charts. In both, one instruction cannot pass another and each stage holds one instruction at a time. **State the model you use.** When every stage is 1 cycle or when only one stage is multi-cycle, both give the same total.

**Example 8 — table with two multi-cycle stages** (original numbers). Four stages, four instructions, cycles per stage:

```
        S1 S2 S3 S4
  I1     1  2  1  1
  I2     1  1  3  1
  I3     2  1  1  1
  I4     1  2  2  1
```

Blocking Gantt (cell = instruction in that stage during that cycle; `*` = finished its stage but is held because the next stage is busy):

```
cycle :    1   2   3   4   5   6   7   8   9  10  11  12
S1    :   I1  I2 I2*  I3  I3  I4 I4*
S2    :       I1  I1  I2      I3 I3*  I4  I4
S3    :               I1  I2  I2  I2  I3      I4  I4
S4    :                   I1          I2  I3          I4
```

```
blocking total = 12 cycles       buffered total = 11 cycles   (verified by the recurrence)
```

Reading it: I2 finishes S1 in cycle 2 but S2 is busy with I1 until cycle 3, so I2 waits in S1 (cycle 3) and delays I3's start of S1. The one-cycle difference comes from buffers letting I2 leave S1 early.

### 7.3 Non-linear pipelines: reservation table and minimum average latency (MAL)

*(Included because one mapped entry asks for the minimum average latency; the table in the mapping is missing, so only the method is shown.)*

In a **linear** pipeline an instruction visits stages 1 → k once. In a **non-linear** pipeline (feedback / reuse of stages) an operation may use a stage in several different time slots. A **reservation table** marks which stage is busy in which cycle for ONE operation:

```
 time →   0  1  2  3  4  5          (n = 6 columns)
 S1       X  .  X  .  .  X
 S2       .  X  .  .  X  .
 S3       .  .  .  X  .  X
```

Start a second operation `p` cycles after the first (latency p). It **collides** if any stage would be used by both in the same cycle, i.e. if p equals the distance between two X's in one row.

1. **Forbidden latencies** = all pairwise differences of X positions within any row. Here: S1 → {2, 3, 5}, S2 → {3}, S3 → {2}. Forbidden = {2, 3, 5}. Latencies ≥ n are always allowed.
2. **Collision vector** C = (C_{n−1} … C_1), with C_j = 1 if j is forbidden: C = 1 0 1 1 0 (positions 5…1).
3. **State diagram**: start state = C. From a state, a latency p (not forbidden in that state, p < n) leads to `(state >> p) OR C`; any latency ≥ n returns to the start state.
4. A **latency cycle** is a closed walk; its average latency = (sum of latencies) / (number of latencies). **MAL** = minimum over all cycles.
5. Lower bound: `MAL ≥ max number of X's in any single row` (that stage must handle that many uses per operation).

State diagram for the table above:

```
 start 10110 ──1──► 11111 ──(≥6)──► 10110        cycle (1,6): average 3.5
 start 10110 ──4──► 10111 ──4──► 10111            cycle (4):   average 4
 10111 ──(≥6)──► 10110
```

Cycles found: (1, 6) → 3.5; (4) → 4; (≥6) → ≥ 6. **MAL = 3.5** (lower bound 3 is not reached). Verified by brute force over all periodic latency sequences. Traps: (a) forbidden latency means *any two X's in the same row*, not only adjacent ones; (b) the average is over the cycle, not just the smallest latency; (c) after a shift, always OR with the original C (new operation's own constraints).

---

## 8. CPI view, the iron law and instruction mixes

### 8.1 The iron law

```
CPU time = IC × CPI × T_clk = IC × CPI / f             (same program → same IC unless stated)
Performance ratio (speedup of X over Y) = Time_Y / Time_X
```

- Non-pipelined / multi-cycle CPI_np = Σ (fraction of class j) × (cycles of class j).
- Pipelined CPI_pipe = 1 + Σ (fraction of instructions affected) × (stall cycles each) — "20 % of instructions lose 3 cycles" contributes 0.2 × 3 = 0.6. The ideal 1 assumes N is large (fill/drain ignored). For finite N the exact figure is `(k + N − 1)/N + stalls`.
- Frequency comparison: from `T = IC·CPI/f`, for the same IC: `f_2 = f_1 × (CPI_2/CPI_1) × (T_1/T_2)`.

Where stalls come from is the sibling's job. Here they are inputs; always "add stall cycles to the pipelined CPI, never to the non-pipelined one".

### 8.2 Worked Examples 9–11

**Example 9 — multi-cycle versus pipeline, new clock.** Non-pipelined: 1.6 GHz, instruction mix ALU 50 % (4 cycles), load 30 % (5), store 10 % (4), branch 10 % (3). Pipelined version (same ISA): 1.25 GHz, and 15 % of instructions lose 2 stall cycles.

```
CPI_np   = 0.5×4 + 0.3×5 + 0.1×4 + 0.1×3 = 2 + 1.5 + 0.4 + 0.3 = 4.2
CPI_pipe = 1 + 0.15×2 = 1.3
time per instruction: non-pipelined = 4.2/1.6 GHz = 2.625 ns ; pipelined = 1.3/1.25 GHz = 1.04 ns
S = 2.625 / 1.04 = 2.52
```

**Example 10 — pipeline clock limited by one slow stage.** Multi-cycle machine at 1 GHz (1 ns clock): mix ALU 50 % (4), load 25 % (5), store 15 % (4), branch 10 % (3) → CPI_np = 2.0 + 1.25 + 0.6 + 0.3 = 4.15, i.e. 4.15 ns per instruction. Pipeline stage delays IF 1, ID 0.8, EX 1, MEM 2, WB 0.8 ns (zero overhead), CPI_pipe = 1.1.

```
T_p = max = 2 ns (MEM) → time per instruction = 1.1 × 2 = 2.2 ns
S = 4.15 / 2.2 = 1.89      (not ≈ 4 or 5: the slow MEM stage wastes most of the benefit)
```

**Example 11 — comparing two processors with CPI and frequency.** P1: 1 GHz, CPI = c. P2 runs the same program in 30 % less time with a CPI that is 25 % higher.

```
T = IC·CPI/f  →  T2/T1 = (CPI2/CPI1)·(f1/f2) = 1.25 × (1/f2 [GHz])  and  T2/T1 = 0.70
f2 = 1.25 / 0.70 = 1.786 GHz
```

**Example 12 — mix and total time → clock period.** A program has 5.0 × 10^8 instructions: 2.0 × 10^8 ALU (3 cycles), 1.5 × 10^8 load (5), 0.5 × 10^8 store (4), 1.0 × 10^8 branch (2). It runs in 4.2 s.

```
total cycles = 2.0e8×3 + 1.5e8×5 + 0.5e8×4 + 1.0e8×2 = 6e8 + 7.5e8 + 2e8 + 2e8 = 17.5e8
T_clk = 4.2 s / 17.5e8 = 2.4e-9 s = 2.4 ns         (frequency 416.7 MHz)
CPI   = 17.5e8 / 5.0e8 = 3.5
```

Traps: use total cycles (Σ count × CPI), not Σ count; keep 10^8 factors; convert s → ns last; confirm the class counts add up to the stated total instruction count.

### 8.3 Superscalar (concept only)

A **w-issue** superscalar pipeline can start up to w instructions per cycle; ideal CPI = 1/w. Real issue is limited by dependencies and resources (sibling topic). It is not examined in the mapped entries; do not spend time beyond this paragraph.

---

## 9. Stage-level timing that touches other topics

### 9.1 A taken branch with no prediction (stage-level timing only)

*(Full treatment — policies, delay slots, branch prediction — is in [`../08-PIPELINE-HAZARDS`](../08-PIPELINE-HAZARDS/).)*

Assume: no prediction, fetch stalls (or wrong-path fetches are discarded) until the branch outcome is known at the end of stage r, and the target is fetched in the next cycle. The branch is the p-th executed instruction; m instructions are executed from the target to the end.

```
fetch slots for I1..Ip : cycles 1..p
branch resolves        : end of cycle p + r − 1   (it is in stage r in that cycle)
target fetched         : cycle p + r
last instruction fetched : p + r + m − 1 ; it completes k − 1 cycles later
total cycles = p + r + m + k − 2        (penalty = r − 1 cycles compared with no taken branch)
```

**Example 13.** k = 5 (IF ID EX MEM WB), branch resolved at end of EX (r = 3). Program of 10 instructions; I3 is a taken branch to I8, so I4–I7 are skipped. Executed: I1, I2, I3, I8, I9, I10.

```
p = 3, r = 3, m = 3 (I8, I9, I10)  → total = 3 + 3 + 3 + 5 − 2 = 12 cycles
without the taken branch penalty (6 instructions straight): 5 + 6 − 1 = 10 → penalty 2 = r − 1 ✓
```

Hidden assumptions to check in a question: *which stage resolves the branch* (stage r); whether instructions after the branch are fetched speculatively (flushed) or fetching stops — same total; whether time = cycles × T with `T = max stage + buffer delay`. The mapped 2013 question family leaves some of this to the reader; verify against the paper and the official key.

### 9.2 Dependences (definition only)

Three register dependences between two instructions: **RAW** (true; second reads what the first writes), **WAR** (anti; second writes what the first reads), **WAW** (output; both write the same register). Which of them is a *hazard* in a given pipeline, and how many stalls it costs, is in the sibling folder. A quick classification rule used in a mapped entry: label by the order *(first access)-then-(second access)* on the same register: R→W is WAR, W→R is RAW, W→W is WAW.

### 9.3 Bridge: where the TLB sits in the MEM stage

*(Prerequisite / bridge — owned by [`../05-MEMORY-INTERFACING-AND-HIERARCHY`](../05-MEMORY-INTERFACING-AND-HIERARCHY/) and [`../../08-OPERATING-SYSTEMS/08-MEMORY-MANAGEMENT-AND-VIRTUAL-MEMORY`](../../08-OPERATING-SYSTEMS/08-MEMORY-MANAGEMENT-AND-VIRTUAL-MEMORY/).)*

The data TLB translates a **virtual address** into a **physical address**. In a load/store, the virtual address is the output of the **effective-address calculation** (base register + offset, done in EX). Therefore reason with *data dependence*: a unit can start only when its input exists. Ask: what input does the TLB need, and which stage/operation produces it? In a pipeline with a physically-tagged cache the TLB lookup precedes the tag compare, and with a virtually-indexed cache the cache-index step can overlap with the TLB lookup. Stage-level questions of this kind are about *ordering of operations*, not arithmetic.

---

## 10. Instruction pipeline versus arithmetic pipeline (concept paragraph)

An **instruction pipeline** overlaps different phases of *different instructions*. An **arithmetic pipeline** overlaps phases of the *same operation applied to a stream of operands* — e.g. a floating-point adder split into compare-exponents → align-mantissas → add → normalise. The k + N − 1 timing is identical.

**Example 14.** A 4-stage FP-add pipeline with 2 ns per stage processes 100 operand pairs:

```
time = (4 + 100 − 1) × 2 ns = 206 ns            non-pipelined: 100 × 4 × 2 = 800 ns
S = 800/206 = 3.88 (asymptote 4)
```

Neither the mapped entries nor the existing practice file ask for FP-adder details; this paragraph is for completeness only.

---

## 11. Step-by-step GATE procedure (ideal-pipeline numerics)

```
1  Identify the ask: cycles / time / clock / frequency / throughput / speedup / efficiency / CPI / instruction count.
2  List k, N, each stage delay t_i, overhead d, any stall rule, any multi-cycle stage, any instruction mix.
3  Clock:  T_p = max(t_i) + d   (if stage delays already include overhead, do not add again — read the wording).
4  Non-pipelined time per instruction: write the variant (A–E of §5.2). If CPI/f given, use V4.
5  Cycle count:  k + N − 1 (+ stalls). Time = cycles × T_p. Convert units LAST (ps/ns/µs/s).
6  Speedup = non-pipelined time / pipelined time.  "Steady state / large N" → ratio of times per instruction only.
7  Check: speedup ≤ k (when stall-free & same technology), CPI ≥ 1, latency ≥ T_np, frequency units (GHz vs ns).
8  If the question changes the design (split a stage, add a stage, replicate) → recompute step 3 with the NEW stage list; the new max may be a different stage.
```

---

## 12. PYQ patterns (recognition, recipe, traps — no answers)

| # | Pattern (mapped years) | How to recognise | Recipe | Trap |
|---|---|---|---|---|
| P1 | **Highest peak clock frequency among pipeline designs** (2014 Set-3) | Several processors listed with stage latencies, "highest frequency" | Frequency = 1 / max(stage) (+ d); compare the maxima only | Choosing the deepest pipeline or the smallest sum. Zero-latency registers means d = 0. |
| P2 | **Split the longest stage** (2016 CS-1: throughput %; 2016 CS-2: new frequency) | "replaced by two stages", "split into two stages of equal latency" | §6.1 rule; throughput % = old/new − 1; frequency = 1/new max | New limit is another stage; "percent increase" is (ratio − 1) × 100, not the ratio; stage ratios given algebraically (τ1 = 3τ2/4 = 2τ3) → pick a unit, build all three delays, then split. |
| P3 | **Steady-state speedup with register delay shown in a figure** (2011) | Figure with stage delays and a register delay; "approximate speedup in steady state under ideal conditions" | V3: Σ stage delays (no registers in the non-pipelined version) ÷ (max stage + register delay) | Adding register delays to the non-pipelined time, or forgetting them in the pipelined clock. The mapped text is OCR-garbled but the structure is clear; check the PDF. |
| P4 | **Cycle count from a per-instruction, per-stage cycle table** (2009; table incomplete in the mapping) | A table of cycles each instruction spends in each stage, executed in a loop | §7.2 recurrence (blocking Gantt); a loop of m iterations repeats the instruction sequence; mind overlap between iterations | Adding per-instruction totals (no overlap) or assuming overlap that violates in-order stage occupancy. |
| P5 | **Processor comparison via CPI and time** (2014 Set-1) | "takes x % less time but y % more CPI", frequency asked | §8.1 / Example 11 | Percent-change algebra (less time → 0.75, not 1/0.75 mistakes); same IC. |
| P6 | **Instruction mix with different CPI → clock period** (2025 CS-2) | Table: instruction types, CPI, counts; total time given; clock period asked | Total cycles = Σ count × CPI; T_clk = time / cycles (Example 12) | 10^8 factors; counts do not need to sum to anything else; "pipeline" word not involved. |
| P7 | **Pipelined time with a taken branch, no prediction** (2013, 4 booklets, one question) | Five stages, stage delays, buffer delay per stage, 12 instructions, one taken branch | T = max stage + buffer; cycles from §9.1 formula; time = cycles × T; read which stage resolves the branch | Using the non-pipelined sum; counting skipped instructions; wrong r (see sibling). |
| P8 | **Non-linear pipeline MAL** (2015; table missing) | Reservation table with X's, "minimum average latency" | §7.3 forbidden latencies → collision vector → state diagram → cheapest cycle | Using only adjacent X's; forgetting latencies ≥ n are free; averaging wrongly. |
| P9 | **Where in the pipeline can a unit start** (2008, TLB) | "earliest that … can be accessed" | §9.3: identify the producer of the unit's input | Treating it as a timing arithmetic question. |
| P10 | **Dependence labelling / delay-slot candidate** (2024 CS-2, 2008) | Instruction listing, RAW/WAR/WAW or "can occupy delay slot" | §9.2; delay slots in the sibling | Mixing up the ordering convention. |

Not-yet-mapped-here but structurally identical items live in the sibling's mapping (see [`PYQ.md`](PYQ.md)): total time = (k + N − 1)·(max stage + latch); speedup with a stall fraction; variable-cycle PO/EX stage; non-pipelined CPI/frequency versus pipelined frequency.

---

## 13. Traps and misconceptions

1. **T = N × k × T_p** instead of (k + N − 1) × T_p — forgetting that stages overlap, or forgetting fill.
2. **Off-by-one:** (k + N) or (N − 1) cycles. A single instruction takes exactly k cycles.
3. **"Speedup = k"** for any finite N or unbalanced stages. It is the limit for balanced stages, zero overhead, N → ∞.
4. **Register overhead:** adding d to the *sum* of stage delays for the non-pipelined time; or not adding it to the maximum.
5. **Using the sum of delays as the clock** (or the average). Clock = **max** + d.
6. **After splitting, using the old overhead-free halves only** — the new register adds d to every stage; the new maximum may be an unsplit stage.
7. **Latency vs throughput:** claiming pipelining makes one instruction faster.
8. **Units:** ps, ns, µs, s; GHz = 10^9 Hz; "time to process N instructions" asked in µs.
9. **Stalls in the wrong CPI:** stalls raise CPI_pipe only; the multi-cycle baseline has its own cycle counts.
10. **CPI < 1** for a scalar pipeline — impossible (superscalar excepted).
11. **Two multi-cycle stages** with the single-stage closed form.
12. **Same-clock assumption:** V1 assumes the non-pipelined machine takes exactly k pipeline-clock cycles per instruction; if a different time/clock is given, use V2/V4.
13. **Instructions completed in the first C cycles** is C − k + 1, not C.
14. **Mixing pipeline stage count with the number of instruction classes** (e.g. 5 stages vs 4 instruction types).

## 14. Edge cases and assumptions to state

- N = 1 → k cycles, speedup 1 (V1); N < k leaves the pipe never full.
- k = 1 → no pipelining; speedup 1.
- "Steady state" → ignore fill/drain; ratio of per-instruction times.
- Equal stages and d = 0 → T_np = k·T_p; speedup tends to k.
- If stage delays "include the register delay", do not add d again.
- If a stage delay is given in a table with different units (ps vs ns) convert first.
- Clock is a design constant: it cannot be tuned per instruction type; fast instructions still take a whole cycle per stage.
- Non-pipelined baseline may be *single-cycle* (clock = whole instruction, CPI 1) or *multi-cycle* (CPI = cycles per class); the question says which.
- Percent of instructions "stalling" is a per-instruction average CPI contribution (fraction × cycles).
- Ideal CPI = 1 ignores fill/drain; exact CPI = (k + N − 1)/N + stalls.
- Frequency and time questions on pipelines assume the clock is exactly the slowest stage (+ overhead); no slack.

---

## 15. Connections to other COA topics

- **Hazards (`../08-PIPELINE-HAZARDS`):** stall cycles feed CPI_pipe = 1 + stalls; forwarding changes the stall count; branch cost generalises §9.1.
- **Control unit (`../04-DESIGN-OF-CONTROL-UNIT`):** a multi-cycle (microprogrammed/hardwired FSM) design is the non-pipelined baseline: instruction = 3–5 cycles.
- **Memory hierarchy (`../05-…/01-PERFORMANCE`):** cache-miss stalls are added to CPI the same way as hazard stalls; AMAT replaces the "MEM = 1 cycle" assumption.
- **Instruction set/addressing modes (`../01-…`, `../02-…`):** load/store (register-memory split) architectures make pipelines simple; complex memory-operand instructions need multiple memory stages.
- **Interrupts (`../06-IO-INTERFACE/01-INTERRUPT`):** precise interrupts in a pipeline require draining or recording the state of instructions in flight.
- **Digital logic:** setup/hold and clock-to-Q define d; the critical path defines the clock.

---

## 16. Existing practice coverage map

(Question numbers refer to the existing file [`practice.md`](../../14-PRACTICE-QUESTIONS/TOPIC-WISE/03-COMPUTER-ORGANIZATION-ARCHITECTURE/07-INSTRUCTION-PIPELINING/practice.md); not reproduced.)

| Q# | Section | Skill |
|---|---|---|
| 1 | §2.2, §3 | Overlap of instructions in different stages |
| 2 | §4.1 | First instruction takes k cycles |
| 3 | §3.1, §3.2 | Steady-state throughput = 1 per cycle |
| 4 | §4.1 | k + N − 1 |
| 5 | §4.2 (V1) | Speedup Nk/(k + N − 1), same clock |
| 6 | §4.2 (V3), §6.1 | Unbalanced stages: Σ ÷ max |
| 7 | §5.2 variant B, Example 2 | Overhead in pipeline only; asymptotic speedup |
| 8 | §4.2–§4.3, §5.1 | True/false statements on clock, balance, ideal CPI |
| 9 | §4.1 | Time = (k + N − 1) × clock |
| 10 | §5.1 | Clock = max + overhead |
| 11 | §4.2 (V2), Example 1 | Time-based speedup with finite N |
| 12 | §6.1, Example 3 | Replace a stage by two; new max; overhead on every stage |
| 13 | §4.4 | Smallest k for a speedup target (T/(T/k + d)) |
| 14 | §2.3 | What each stage does for ALU/load; overlap of different instructions |
| 15 | §4.1 (completed-by-cycle formula) | C − k + 1 completed in the first C cycles |
| 16 | §4.2 (V3), Example 5 | One slow stage caps speedup |
| 17 | §4.2 (V4), §8.1, Example 9 | CPI and frequency speedup |
| 18 | §7.1, Example 7 | Extra EX cycles: (k + N − 1) + Σ(c_i − 1) |
| 19 | §4.4 | Smallest k for speedup 6 with overhead |
| 20 | §4.1–§4.3 | k + N − 1 cycles → time; speedup vs asymptote; equal stages |

Note: the solutions of existing Q8 and Q20 mention an option "E" that is not printed in the question; the answer keys A–D are consistent with the printed options (reported in the handoff).

## 17. Self-check (answers not given)

1. How many cycles does a k-stage pipeline need for N instructions and why exactly that many?
2. What is the speedup for N = k − 1 with equal stages and the same clock?
3. Why can pipelining increase the latency of an instruction?
4. What defines the clock period and what does the register overhead add?
5. What is the asymptotic speedup of stages 3, 7, 5, 4 ns with zero overhead? With 1 ns overhead?
6. After you split the slowest stage, which stage decides the new clock?
7. How is the non-pipelined time defined in a variant with register overhead only in the pipelined design?
8. What is the CPI of a pipeline where 25 % of instructions lose 2 cycles?
9. How many instructions have completed after C cycles in a k-stage pipeline?
10. When does the closed form k − 1 + Σc_i work, and when must you build a table?
11. What is a forbidden latency and how does the collision vector use it?
12. How do you compare two processors that differ in CPI and clock?
