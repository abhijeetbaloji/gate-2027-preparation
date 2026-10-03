# Hardwired Control — Formulas and Relations

Conventions: 1 K = 2¹⁰; byte-addressable memory, 4-byte instructions unless stated; one control step = one clock cycle unless a memory wait stretches it. Back to the derivations: [NOTES.md](NOTES.md).

---

## A. Control-signal logic

### A1. Control signal as a sum of products

```
signal = Σ over (instruction i, step Tk) where it is asserted  [ i · Tk · (flag, if conditional) ]
         + Σ over fetch steps where it is asserted              [ Tk ]
```

- **Symbols:** `i` = instruction-decoder output, `Tk` = step-decoder output, flag = optional condition.
- **When it applies:** hardwired control with instruction decoder + step counter (NOTES §6–§7).
- **Why:** the signal must be 1 exactly in the (opcode, step) cells listed in the micro-operation table; each cell is an AND, the signal is the OR of those cells.
- **Example (verified against the NOTES tables):** `Yin = (ADD + BR)·T4`, `Rain = (ADD + LD)·T6 + LDI·T8`, `End = (ADD + LD + ST + BR)·T6 + LDI·T8`.
- **Misuse:** putting a flag on the whole signal instead of only on the conditional term (`PCin = T2 + BRZ·T6·Z`, not `(T2 + BRZ·T6)·Z`); including two `…out` terms in the same (instruction, step) cell on a single-bus datapath.

### A2. Number of product terms and OR inputs

```
OR fan-in of a signal = number of (flattened) product terms in its equation
```

- Five-instruction machine of the NOTES: 20 signals, 52 flattened product terms in total (e.g. `End` 5, `WMFC` 5, `Rbout` 4).
- **Assumes** no factoring; factored forms `(a + b)·T4` have a smaller OR but an extra OR in front of the AND.

### A3. Shared AND gates (instruction·step)

```
distinct (instruction, step) AND gates = number of (instruction, step) cells in which at least one signal is asserted
```

- Five-instruction machine: 3 + 3 + 3 + 3 + 5 = **17** two-input ANDs (fetch rows use T1…T3 directly; no AND).
- **Assumes** every such AND is built once and shared by all signals using it.

---

## B. Counters, states and encodings

### B1. Step-counter width (step counter + instruction decoder organisation)

```
counter bits = ⌈log₂ (number of steps in the longest instruction, fetch included)⌉
```

- Example: longest instruction = 3 fetch + 5 execute = 8 steps ⇒ ⌈log₂ 8⌉ = **3**. For 11 steps ⇒ 4. For 9 steps ⇒ 4 (2³ = 8 < 9).
- **Misuse:** using total states of all instructions (that is B2); forgetting fetch steps; using ⌊log₂⌋.

### B2. Finite-state-machine (one-state-per-state) register width

```
S = fetch states + Σ_i (private execute states of instruction i) − (merged identical states)
state bits = ⌈log₂ S⌉
```

- Example: fetch 3, execute 3, 3, 3, 3, 5 ⇒ S = 20 ⇒ **5 bits**; with a shared 2-state LD/LDI prefix S = 18 ⇒ 5 bits.
- **Assumes** identical states are merged only when they assert identical signals *and* behave identically afterwards.
- **Misuse:** applying B2 to a design with a step counter (B1) or vice versa. Read which design the question describes.

### B3. One-hot (delay-element) flip-flop count

```
one-hot flip-flops = S  (states)   — no decoder
one-hot step ring (instruction decoded separately) = number of steps in longest instruction
```

- Example: S = 19 ⇒ 19 flip-flops vs ⌈log₂ 19⌉ = 5 binary ⇒ 14 more flip-flops.
- **Why:** one flip-flop per state, exactly one holds 1. Cost: flip-flops. Gain: no decoder delay, simpler equations.

### B4. Decoder gate count (no sharing)

```
k-to-2ᵏ decoder using n outputs: n AND gates of k inputs  =  n·(k − 1) two-input ANDs   (+ up to k inverters)
```

- Example: 3-to-8 using 8 outputs: 8 × 2 = **16**; using 5 outputs: **10**; 4-to-16 using 11 outputs: 11 × 3 = **33**.
- **Misuse:** counting k inputs per gate as k gates; counting all 2ᵏ outputs when only n are used.

### B5. ROM / PLA table implementation

```
ROM words = 2^(opcode bits + step bits)
ROM bits  = ROM words × (number of control signals per word)
ROM bytes = ROM bits / 8
```

- Example: 4-bit opcode + 2-bit step, 10 signals ⇒ 2⁶ × 10 = **640 bits** = 80 bytes. 5-bit opcode, 4-bit step, 26 signals ⇒ 512 × 26 = 13 312 bits = **1664 bytes**.
- **Assumes** every (opcode, step) combination is addressable and every word has one bit per signal (no encoding).
- **Misuse:** adding the address bits instead of using them as an exponent; mixing bits and bytes. This is a *truth-table* ROM, not a microprogram control store.

---

## C. Performance relations

### C1. Iron law

```
CPU time = IC × CPI × T_clk = IC × CPI / f
```

- Units: T_clk in s (ns = 10⁻⁹ s), f in Hz (MHz = 10⁶). Example: IC = 5×10⁶, CPI = 6.4, f = 400 MHz ⇒ 5×10⁶ × 6.4 / 400×10⁶ = **0.08 s = 80 ms**.

### C2. CPI of a multi-cycle hardwired design

```
cycles(instruction) = Σ cycles of each of its control steps
CPI = Σ_i  (fraction_i × cycles(i))
```

- NOTES machine, L = 1 (every step 1 cycle): cycles 6, 6, 6, 6, 8; mix 40/25/15/15/5 % ⇒ CPI = **6.10**.
- **Misuse:** an unweighted average of the instruction cycle counts.

### C3. Memory wait cycles

```
L = ⌈ T_mem / T_clk ⌉          (whole cycles from the address-load edge to data ready)
cycles of a WMFC step = max(1, L)
fetch cycles = 1 + max(1,L) + 1
LD cycles    = fetch + 1 + max(1,L) + 1
ST cycles    = fetch + 1 + 1 + max(1,L)
LDI cycles   = fetch + 1 + max(1,L) + 1 + max(1,L) + 1
```

- Example L = 3: fetch 5, ADD 8, LD 10, ST 10, BR 8, LDI 14 ⇒ with mix 40/25/15/15/5 % CPI = **9.10**.
- **Assumes** the other work in the wait step (e.g. `PC ← Z`) hides under the wait.
- **Misuse:** truncating ⌈ ⌉; adding the wait to every step instead of to the WMFC steps only.

### C4. Clock-period constraint of a hardwired step

```
T_clk ≥ t_clk→Q + max(t_instr-dec , t_step-dec) + t_logic + t_reg-out + t_bus + t_ALU + t_setup
```

- **Why:** control signals cannot be valid before the registers that produce them have changed and their decoders and AND-OR network have settled; then the datapath must propagate before the next edge. The two decoders work in parallel ⇒ max, not sum.
- Example: 0.5 + max(1.0, 0.7) + 1.8 + 0.4 + 0.8 + 2.4 + 0.3 = **7.2 ns** (138.9 MHz). Second example with parallel decoders of 1.5 ns and 1.2 ns, clk→Q 0.8 ns, control logic 3.0 ns and a final setup 0.2 ns (no datapath term, control-only path): 0.8 + 1.5 + 3.0 + 0.2 = 5.5 ns.
- **Misuse:** summing the decoder delays; leaving out clk→Q or setup; including an ALU term in a step where the ALU is not used (but remember the clock is set by the worst step).

### C5. Cycle time and CPI of the three organisations

```
single-cycle : T_clk = (longest instruction path) + overhead ; CPI = 1
multi-cycle  : T_clk = (longest step) + overhead ; CPI = weighted average of step counts
pipelined    : T_clk = (longest stage) + pipeline-register overhead ; CPI = 1 + average stall cycles
time per instruction = CPI × T_clk
```

- NOTES §11 example: 770 ps (single), 4.10 × 220 = 902 ps (multi), 1.25 × 220 = 275 ps (pipelined).
- **Misuse:** comparing CPI alone; assuming multi-cycle always beats single-cycle (it does not when stages are unbalanced and overhead is paid every step).

### C6. Speed-up

```
speed-up of B over A = time per instruction (A) / time per instruction (B)
```

- Example: 770 / 902 = **0.854** (multi-cycle is slower than single-cycle in that example); 902 / 275 = **3.28** (pipelined over multi).

### C7. Splitting a long step (trade clock for CPI)

```
new CPI = old CPI + (average number of split steps per instruction)
new T_clk = max( other steps , (long step + extra latch overhead) / 2 )
split pays off iff  new CPI × new T_clk < old CPI × old T_clk
```

- Example: (6.1 + 1.4) × 4.4 = 33.0 ns vs 6.1 × 6.0 = 36.6 ns ⇒ speed-up **1.11**.
- **Misuse:** looking only at the shorter clock.

### C8. Ideal k-stage pipeline (bridge)

```
cycles for N instructions = k + N − 1       (no stalls)
```

- Owner: [../../07-INSTRUCTION-PIPELINING](../../07-INSTRUCTION-PIPELINING). Used here only to compare with multi-cycle.

---

## D. Hardwired vs microprogrammed control time

```
hardwired control time per instruction     = (steps) × T_clk
microprogrammed control time per instruction = (microinstructions executed) × (control-store access + next-address overhead)
```

- Example: 5 × 2 ns = 10 ns vs 7 × 3 ns = 21 ns ⇒ microprogrammed is 2.1× slower.
- **Assumes** one microinstruction per step with no overlap of control-store fetch and execution.
- Detailed microprogram formulas live in [../02-MICROPROGRAMMED](../02-MICROPROGRAMMED).

---

## Quick anchors

| Formula | Anchor |
|---|---|
| Control signal as sum of products | A1 |
| Shared instruction·step ANDs | A3 |
| Step-counter bits | B1 |
| FSM state bits | B2 |
| One-hot flip-flops | B3 |
| Decoder gates | B4 |
| ROM size | B5 |
| Iron law | C1 |
| Weighted CPI | C2 |
| Memory wait cycles | C3 |
| Clock-period constraint | C4 |
| Single / multi / pipelined | C5 |
| Speed-up | C6 |
| Splitting a long step | C7 |
| Hardwired vs micro time | D |
