# Hardwired Control — Practice (24 original questions)

All questions are original and solvable from [NOTES.md](NOTES.md). Unless a question says otherwise: **single internal bus** with registers Y and Z as in NOTES §4 (one `…out` per step; a register loaded in step Tk is usable from Tk+1; `Read` is asserted in the step that loads MAR; `Write` in the step that loads MDR; decoding the opcode takes no separate step); byte-addressable memory; 1 K = 2¹⁰.
MCQ = exactly one correct option. MSQ = one or more correct options, no partial marking. NAT = numeric answer with the stated precision.

Instruction notation used in several questions: `ADD Ra,Rb,Rc` is Ra ← Rb + Rc; `LD Ra,(Rb)` is Ra ← M[Rb]; `ST Ra,(Rb)` is M[Rb] ← Ra; `BR off` is PC ← PC + off; `LDI Ra,(Rb)` is Ra ← M[M[Rb]].

---

## Level 1 — Conceptual

### Q1 — MCQ — Level 1

Which of the following is **not** normally an input of the control-signal generator of a hardwired control unit?

A. the outputs of the instruction (opcode) decoder
B. the outputs of the step (timing) decoder
C. the ALU condition flags
D. a microinstruction word read from a control store

**Answer:** D

**Solution:** A hardwired generator computes each signal from the decoded opcode (A), the decoded step (B) and, for conditional actions, flags (C). A control store holding microinstructions belongs to the microprogrammed organisation (NOTES §6, §12).

**Concept tested:** inputs of the hardwired control-signal generator.

**Difficulty:** Easy

**Common trap:** thinking a hardwired unit still reads some "control word".

---

### Q2 — MSQ — Level 1

On the single-bus reference datapath, which of the following sets of signals can be asserted **together in one control step**? (One or more options correct.)

A. `R1out` and `R2out`
B. `R1out`, `MARin` and `Yin`
C. `PCout` and `Zout`
D. `Zout`, `PCin` and `R4in`

**Answer:** B, D

**Solution:** Only one source may drive a single bus per step, but any number of registers may latch the bus value. A has two `out` signals and C has two `out` signals → bus conflicts. B has one `out` (R1) and two `in` signals → legal. D has one `out` (Z) and two `in` signals → legal.

**Concept tested:** one `out` per step, many `in`.

**Difficulty:** Easy

**Common trap:** treating `in` signals as also driving the bus.

---

### Q3 — MCQ — Level 1

In a hardwired control unit with a step counter, the signal `End` is asserted in the last step of every instruction. Its main effect is to

A. load the PC with the branch target
B. reset the step counter so that the next clock begins a new fetch at T1
C. tell the memory that the read is complete
D. select the constant 4 as the left ALU input

**Answer:** B

**Solution:** `End` returns the sequencing state to the beginning (fetch T1). Loading the PC is `PCin`, memory completion is MFC (which ends a WMFC step), and the constant 4 is chosen by `Select4` (NOTES §3, §6).

**Concept tested:** role of `End` and the step counter.

**Difficulty:** Easy

**Common trap:** confusing `End` with `WMFC`/MFC.

---

### Q4 — MCQ — Level 1

Which statement best explains why hardwired control is the usual choice for a RISC processor?

A. RISC has few simple, fixed-format instructions, so the number of (instruction, step) combinations is small and the control path is short
B. A hardwired unit lets a new complex instruction be added by writing new words to a ROM
C. A hardwired unit contains a control store that can be patched after fabrication
D. RISC instructions have variable length, which needs a sequencer that only hardwired logic provides

**Answer:** A

**Solution:** B and C describe microprogramming. D is wrong because RISC instructions are typically fixed length. A matches the argument in NOTES §12.2: small regular tables give a small AND-OR network and a fast control path.

**Concept tested:** RISC ↔ hardwired link.

**Difficulty:** Easy

**Common trap:** attributing microprogram properties to hardwired control.

---

## Level 2 — Standard GATE

### Q5 — NAT — Level 2

In a controller with an instruction decoder and a binary step counter, the longest instruction (fetch included) needs 11 control steps. What is the minimum number of bits in the step counter? (Integer.)

**Answer:** 4

**Solution:** Need 2ᵏ ≥ 11. 2³ = 8 < 11 ≤ 16 = 2⁴ ⇒ k = ⌈log₂ 11⌉ = 4.

**Concept tested:** step-counter width.

**Difficulty:** Easy

**Common trap:** ⌊log₂ 11⌋ = 3.

---

### Q6 — MCQ — Level 2

A small machine has the following micro-operations (all rows are single-bus steps; End is omitted for brevity).

```
Fetch: T1: PCout, MARin, Read, Select4, Add, Zin
       T2: Zout, PCin, WMFC
       T3: MDRout, IRin
MOV Ra,Rb : T4: Rbout, Rain
LDA Ra,(Rb): T4: Rbout, MARin, Read ; T5: WMFC ; T6: MDRout, Rain
STA Ra,(Rb): T4: Rbout, MARin ; T5: Raout, MDRin, Write ; T6: WMFC
JMP Rb    : T4: Rbout, PCin
```

Which equation correctly gives `MARin`?

A. `T1 + (LDA + STA)·T4`
B. `T1 + LDA·T4`
C. `(T1 + LDA + STA)·T4`
D. `T1 + (LDA + STA)·T5`

**Answer:** A

**Solution:** `MARin` appears in fetch T1 and in step T4 of LDA and of STA, nowhere else. B omits STA. C factors T4 over T1, but T1 and T4 are never both 1, so the fetch term would vanish. D uses the wrong step.

**Concept tested:** deriving a control equation from the table.

**Difficulty:** Medium

**Common trap:** factoring a common step across a fetch term.

---

### Q7 — NAT — Level 2

For the machine of NOTES §5 the step structure is:

- Fetch: 3 steps (T1, T2 with WMFC, T3).
- ADD: 3 execute steps, none with WMFC.
- LD: 3 execute steps, one of them a WMFC step.
- ST: 3 execute steps, one of them a WMFC step.
- BR: 3 execute steps, none with WMFC.
- LDI: 5 execute steps, two of them WMFC steps.

Every non-WMFC step lasts 1 cycle; every WMFC step lasts L = 2 cycles. Instruction mix: ADD 35 %, LD 25 %, ST 10 %, BR 20 %, LDI 10 %. Find the average CPI. (Two decimal places.)

**Answer:** 7.75

**Solution:**
- Fetch = 1 + 2 + 1 = 4 cycles.
- ADD = 4 + 3 = 7; BR = 4 + 3 = 7.
- LD = 4 + (1 + 2 + 1) = 8; ST = 4 + (1 + 1 + 2) = 8.
- LDI = 4 + (1 + 2 + 1 + 2 + 1) = 11.
- CPI = 0.35·7 + 0.25·8 + 0.10·8 + 0.20·7 + 0.10·11 = 2.45 + 2.00 + 0.80 + 1.40 + 1.10 = **7.75**.

**Concept tested:** weighted CPI with memory wait.

**Difficulty:** Medium

**Common trap:** unweighted mean of the five cycle counts (8.2), or forgetting that fetch also contains a WMFC step.

---

### Q8 — NAT — Level 2

A hardwired multi-cycle processor runs at 400 MHz with average CPI 6.4. How long does it take to execute 5 × 10⁶ instructions? Give the answer in milliseconds.

**Answer:** 80 (ms)

**Solution:** Time = IC × CPI / f = 5×10⁶ × 6.4 / (400×10⁶ Hz) = 3.2×10⁷ / 4×10⁸ = 0.08 s = **80 ms**.

**Concept tested:** iron law.

**Difficulty:** Easy

**Common trap:** using MHz as Hz or ns/ms slips.

---

### Q9 — MCQ — Level 2

On the single-bus datapath the instruction `ST Ra,(Rb)` (M[Rb] ← Ra) is executed after fetch. Ignore the final wait step. Which schedule of control steps is legal and correct?

A. S1: `Rbout, MARin` ; S2: `Raout, MDRin, Write`
B. S1: `Rbout, Raout, MARin, MDRin` ; S2: `Write`
C. S1: `Raout, MDRin, Write` ; S2: `Rbout, MARin`
D. S1: `Rbout, MARin, Read` ; S2: `Raout, MDRin, Write`

**Answer:** A

**Solution:** A loads the address first, then the data with `Write`. B drives the bus from two registers in S1 (conflict). C asserts `Write` before MAR holds the address. D asserts `Read` in a store; a store issues only `Write`.

**Concept tested:** legal one-bus schedule, memory command conventions.

**Difficulty:** Medium

**Common trap:** `Read` in a store; two `out` signals.

---

### Q10 — MCQ — Level 2

When does a hardwired control unit normally examine the interrupt-request line?

A. at the end of an instruction, before the next fetch begins
B. in the middle of an ALU operation, abandoning the instruction
C. only during a memory-wait step inside an execute phase
D. only when the step counter overflows

**Answer:** A

**Solution:** To keep instructions atomic the controller samples the request when the instruction completes (where `End` would reset the counter); if an enabled interrupt is pending it enters the interrupt sequence instead of fetch T1 (NOTES §13).

**Concept tested:** interrupt as a control input.

**Difficulty:** Easy

**Common trap:** thinking an interrupt can split an instruction midway.

---

## Level 3 — Multi-step

### Q11 — NAT — Level 3

A tiny processor has three instructions with the following execute steps; in every execute step at least one control signal is asserted. `MOV` has 1 execute step, `ADD` has 3, `LD` has 3. The fetch steps T1–T3 use only the step decoder. Using one shared 2-input AND gate for every distinct (instruction output · step output) pair that is needed, how many such AND gates are required? (Integer.)

**Answer:** 7

**Solution:** Every (instruction, execute-step) cell with a signal needs one AND of the form `instruction · Tk`: MOV 1 + ADD 3 + LD 3 = **7**. Fetch signals are pure `Tk` terms and need no AND with an instruction output.

**Concept tested:** counting instruction·step AND gates.

**Difficulty:** Medium

**Common trap:** counting fetch steps too, or counting one AND per signal instead of per distinct pair.

---

### Q12 — NAT — Level 3

A designer implements the control function as a ROM addressed by a 4-bit opcode and a 4-bit step number. Each ROM word holds 20 control signals, one bit per signal. What is the ROM size in **bytes**? (Integer.)

**Answer:** 640 (bytes)

**Solution:** Address bits = 4 + 4 = 8 ⇒ 2⁸ = 256 words. Bits = 256 × 20 = 5120. Bytes = 5120 / 8 = **640**.

**Concept tested:** ROM implementation of the control truth table.

**Difficulty:** Medium

**Common trap:** answering 5120 (bits), or adding 4 + 4 + 20.

---

### Q13 — NAT — Level 3

The slowest control step of a hardwired processor drives a register onto the bus, through the ALU and into register Z. Delays: register clock-to-Q 0.5 ns; instruction decoder 1.2 ns; step decoder 0.8 ns (both decoders start at the same clock edge and run in parallel); control logic 1.5 ns; register-output gate 0.4 ns; bus 0.7 ns; ALU 2.1 ns; Z-register setup time 0.3 ns. The control signals must settle before the data path is exercised. Minimum clock period in ns? (One decimal place.)

**Answer:** 6.7 (ns)

**Solution:** Control ready = 0.5 + max(1.2, 0.8) + 1.5 = 3.2 ns. Data path = 0.4 + 0.7 + 2.1 + 0.3 = 3.5 ns. Period ≥ 3.2 + 3.5 = **6.7 ns** (f ≈ 149 MHz).

**Concept tested:** clock-period constraint with parallel decoders.

**Difficulty:** Medium

**Common trap:** summing both decoders (7.5 ns).

---

### Q14 — NAT — Level 3

A finite-state-machine controller uses one distinct state for every control state. It has a 4-state shared fetch and four instructions whose private execute-state counts are 2, 4, 6 and 3. No states are merged. How many **more** flip-flops does a one-hot encoding need than a minimum-width binary state register? (Integer.)

**Answer:** 14

**Solution:** S = 4 + 2 + 4 + 6 + 3 = 19. Binary: ⌈log₂ 19⌉ = 5 (2⁴ = 16 < 19 ≤ 32). One-hot: 19. Difference = 19 − 5 = **14**.

**Concept tested:** one-hot vs binary state count.

**Difficulty:** Medium

**Common trap:** using the longest instruction (4 + 6 = 10 states) as N, or giving 19 or 5.

---

### Q15 — NAT — Level 3

A memory needs L = 5 clock cycles to deliver data after the address is loaded. For the memory-indirect `LDI Ra,(Rb)` of NOTES §5.3, steps T1–T3 are fetch and T4–T8 are execute, with WMFC in fetch T2 and in execute T5 and T7 (each WMFC step lasts L cycles; all other steps last 1 cycle). How many clock cycles does the complete instruction (fetch + execute) take? (Integer.)

**Answer:** 20

**Solution:** Fetch = 1 + 5 + 1 = 7 cycles. Execute = T4 (1) + T5 (5) + T6 (1) + T7 (5) + T8 (1) = 13 cycles. Total = 7 + 13 = **20**.

**Concept tested:** indirection cost with slow memory.

**Difficulty:** Medium

**Common trap:** counting the three WMFC steps as 1 cycle each (8 cycles total).

---

### Q16 — NAT — Level 3

A classic five-stage datapath has stage delays IF 180 ps, ID 120 ps, EX 160 ps, MEM 200 ps, WB 90 ps and a register overhead of 20 ps per clock cycle in every design. Compare a **single-cycle** implementation (clock = delay of the longest instruction, which uses all five stages, plus overhead) with a **multi-cycle hardwired** implementation (clock = longest stage + overhead). The multi-cycle design takes 4, 5, 4 and 3 cycles for R-type, load, store and branch; the mix is 45 %, 25 %, 10 %, 20 %. What is the speed-up of the multi-cycle design over the single-cycle design? (Two decimal places.)

**Answer:** 0.86

**Solution:** Single-cycle clock = 180 + 120 + 160 + 200 + 90 + 20 = 770 ps; CPI = 1 ⇒ 770 ps per instruction. Multi-cycle clock = 200 + 20 = 220 ps; CPI = 0.45·4 + 0.25·5 + 0.10·4 + 0.20·3 = 1.80 + 1.25 + 0.40 + 0.60 = 4.05; time = 4.05 × 220 = 891 ps. Speed-up = 770 / 891 = **0.86** (the multi-cycle design is slower).

**Concept tested:** single vs multi-cycle.

**Difficulty:** Medium

**Common trap:** assuming multi-cycle must win; forgetting the per-cycle overhead.

---

## Level 4 — Tricky / trap-based

### Q17 — MSQ — Level 4

Select all statements that are correct about hardwired and microprogrammed control (typical textbook comparison). (One or more options correct.)

A. For a very large instruction set with long irregular sequences, designing a hardwired unit is generally more costly than designing it for a small regular set.
B. With comparable technology, a hardwired unit usually has a shorter control delay per step because no control-store access is needed.
C. A new instruction can be added to a hardwired unit by writing new words into a control memory, with no change to the gates.
D. A hardwired unit cannot support instructions with different numbers of cycles.

**Answer:** A, B

**Solution:** A and B are the standard comparison. C describes microprogramming. D is false: different instructions simply assert `End` at different steps (NOTES §7.2).

**Concept tested:** hardwired vs microprogrammed comparison.

**Difficulty:** Medium

**Common trap:** flipping the flexibility property.

---

### Q18 — NAT — Level 4

A one-hot (delay-element) controller has a 2-state fetch and three instruction classes. Class A has 6 execute states. Class B has 6 execute states, of which the first 4 are identical in signals and behaviour to the first 4 of class A and are shared with it. Class C has 2 execute states. All other states are private. How many flip-flops does the controller need? (Integer.)

**Answer:** 12

**Solution:** Fetch 2 + A 6 + B's non-shared 6 − 4 = 2 + C 2 = 2 + 6 + 2 + 2 = **12**. (Without sharing it would be 16.)

**Concept tested:** shared states in one-hot controllers.

**Difficulty:** Medium

**Common trap:** forgetting to subtract the shared four, or subtracting them from class A as well.

---

### Q19 — MCQ — Level 4

For `LD Ra,d(Rb)` (Ra ← M[Rb + d]) the following five control steps appear (after fetch) in shuffled order:

```
(1) MDRout, Rain
(2) Zout, MARin, Read
(3) Rbout, Yin
(4) IRoffsetout, Add, Zin
(5) WMFC
```

Which order executes them correctly?

A. 3, 4, 2, 5, 1
B. 4, 3, 2, 5, 1
C. 3, 4, 5, 2, 1
D. 3, 2, 4, 5, 1

**Answer:** A

**Solution:** (3) puts Rb in Y; (4) adds offset from the bus and saves in Z; (2) sends Z to MAR and starts Read; (5) waits; (1) moves MDR into Ra. B adds before Y holds Rb. C waits before the read is issued. D reads Z before it is computed.

**Concept tested:** ordering micro-operations by dependencies.

**Difficulty:** Medium

**Common trap:** swapping the two operand steps; putting the wait before the command.

---

### Q20 — MCQ — Level 4

The only instruction in a machine that changes the PC, besides fetch, is `BRZ` (branch if the Z flag is 1), whose PC load occurs in step T6. Which equation for `PCin` is correct?

A. `T2 + BRZ·T6·Z`
B. `(T2 + BRZ·T6)·Z`
C. `T2·Z + BRZ·T6`
D. `T2 + BRZ·T6 + Z`

**Answer:** A

**Solution:** The flag qualifies only the branch term. B and C would stop the PC from advancing during fetch whenever Z = 0, so sequential execution would break. D would load the PC whenever Z = 1, in every step.

**Concept tested:** flags in control equations.

**Difficulty:** Medium

**Common trap:** qualifying the whole signal.

---

### Q21 — MSQ — Level 4

Select all design characteristics that are typical of a RISC processor. (One or more options correct.)

A. Only load and store instructions access memory; arithmetic instructions use registers.
B. All instructions have the same length, so register fields are at fixed bit positions.
C. A large microprogram ROM interprets most instructions so that complex instructions can be added without new logic.
D. Each instruction supports many addressing modes, so that fewer instructions are needed.

**Answer:** A, B

**Solution:** A and B are standard RISC properties (NOTES §12.2). C is the microprogrammed/CISC approach. D is the opposite of RISC, which uses few addressing modes.

**Concept tested:** RISC characteristics, judged statement by statement.

**Difficulty:** Medium

**Common trap:** accepting "many addressing modes" because it sounds powerful.

---

## Level 5 — Challenge

### Q22 — NAT — Level 5

Stage delays: IF 150 ps, ID 100 ps, EX 130 ps, MEM 190 ps, WB 80 ps; register overhead 10 ps per cycle in both organisations. A **multi-cycle** controller needs 4, 5, 4 and 3 cycles for R-type, load, store and branch with mix 40 %, 25 %, 15 %, 20 %. A **pipelined** version with the same clock has 0.25 stall cycles per instruction on average. What is the speed-up of the pipelined design over the multi-cycle design? (Two decimal places.)

**Answer:** 3.24

**Solution:** Both clocks = 190 + 10 = 200 ps, so the speed-up equals the CPI ratio. Multi-cycle CPI = 0.40·4 + 0.25·5 + 0.15·4 + 0.20·3 = 1.60 + 1.25 + 0.60 + 0.60 = 4.05. Pipelined CPI = 1 + 0.25 = 1.25. Times: 4.05 × 200 = 810 ps vs 1.25 × 200 = 250 ps. Speed-up = 810/250 = **3.24**.

**Concept tested:** multi-cycle vs pipelined comparison.

**Difficulty:** Hard

**Common trap:** computing speed-up as the stage-count ratio 5.

---

### Q23 — NAT — Level 5

The slowest control step (an ALU step) takes 5.0 ns and sets the clock; the next-slowest step takes 3.6 ns. Average CPI is 5.2. Splitting every ALU step into two steps adds 0.4 ns of latch overhead in total, so the two halves take (5.0 + 0.4)/2 ns each. The average instruction contains 1.5 ALU steps. What is the speed-up in time per instruction obtained by splitting? (Two decimal places.)

**Answer:** 1.08

**Solution:** Old time per instruction = 5.2 × 5.0 = 26.0 ns. New clock = max(3.6, (5.0 + 0.4)/2 = 2.7) = 3.6 ns. New CPI = 5.2 + 1.5 = 6.7. New time = 6.7 × 3.6 = 24.12 ns. Speed-up = 26.0 / 24.12 = **1.08**.

**Concept tested:** trading clock period against CPI.

**Difficulty:** Hard

**Common trap:** using the half-ALU time (2.7 ns) as the new clock; ignoring the CPI increase.

---

### Q24 — NAT — Level 5

Clock period 8 ns; main-memory access time 25 ns, i.e. L = ⌈25/8⌉ clock cycles for each WMFC step (all other steps 1 cycle). Steps: fetch = T1, T2 (WMFC), T3. ADD has 3 execute steps (no WMFC). LD has 3 execute steps (one WMFC). LDI has 5 execute steps (two WMFC). The mix is ADD 50 %, LD 30 %, LDI 20 %. What is the average time per instruction in ns? (Integer.)

**Answer:** 92 (ns)

**Solution:** L = ⌈25/8⌉ = ⌈3.125⌉ = 4. Fetch = 1 + 4 + 1 = 6 cycles. ADD = 6 + 3 = 9. LD = 6 + (1 + 4 + 1) = 12. LDI = 6 + (1 + 4 + 1 + 4 + 1) = 17. Average cycles = 0.5·9 + 0.3·12 + 0.2·17 = 4.5 + 3.6 + 3.4 = 11.5. Time = 11.5 × 8 = **92 ns**.

**Concept tested:** memory wait with ceiling, weighted CPI, time.

**Difficulty:** Hard

**Common trap:** truncating L to 3 (gives 78.4 ns); applying the wait to every step.
