# Hardwired Control — Shortcuts

Only shortcuts that follow from the definitions in [NOTES.md](NOTES.md). Each has its limits stated.

---

## S1. Counter / state-register width from a power-of-two table

- **What it solves:** minimum bits for N steps or N states (binary encoding).
- **When to use:** any "how many bits does the step counter / state register need" question.
- **Why it works:** k bits give 2ᵏ codes, so we need the smallest k with 2ᵏ ≥ N.
- **Table:** 2 → 1, 3–4 → 2, 5–8 → 3, 9–16 → 4, 17–32 → 5, 33–64 → 6.
- **Example:** 11 steps ⇒ 9–16 row ⇒ 4 bits. 19 states ⇒ 17–32 row ⇒ 5 bits. Exactly 8 steps ⇒ 3 bits (not 4: the range 5–8 includes 8).
- **Limitation / trap:** first decide *what N is*: longest instruction (step counter) vs all distinct states (FSM) vs steps in a one-hot ring (N flip-flops, no log).

## S2. "Bus transfers + waits" count for execute steps on a one-bus datapath

- **What it solves:** execute steps of an instruction on the reference datapath of NOTES §4 without writing the whole table.
- **When to use:** "how many cycles/steps does instruction X take" on a single-bus machine where each step has at most one `…out`.
- **Rule:** execute steps = (number of distinct values that must be driven onto the bus) + (number of memory-wait steps that cannot share a step with a bus transfer).
- **Why it works:** with one bus, each step has at most one source driving it, so every value that must travel needs its own step; a memory wait does not drive the bus.
- **Examples (all agree with the tables of NOTES §5):**
  - `ADD Ra,Rb,Rc`: bus values = Rb, Rc, Z → 3, no waits → **3**.
  - `LD Ra,(Rb)`: Rb, MDR → 2, plus 1 wait → **3**.
  - `ST Ra,(Rb)`: Rb, Ra → 2, plus 1 wait → **3**.
  - `BR off`: PC, offset, Z → **3**.
  - `LDI Ra,(Rb)`: Rb, MDR, MDR → 3, plus 2 waits → **5**.
  - `LD Ra,d(Rb)`: Rb, offset, Z, MDR → 4, plus 1 wait → **5**.
- **Limitation / trap:** (i) a wait can be merged with an independent bus transfer (fetch does `Zout, PCin, WMFC` in one step), so in fetch the formula gives 3 outs (PC, Z, MDR) = 3 steps with the wait hidden; (ii) a datapath with two buses or a dedicated incrementer needs fewer steps; (iii) the question's own datapath always wins.

## S3. Parallel branches: max, not sum

- **What it solves:** clock period when instruction decoder and step decoder feed the control logic.
- **When to use:** whenever two paths start at the same edge and join at one gate.
- **Why it works:** the joining gate waits for the later input; the earlier one is hidden.
- **Example:** clk→Q 0.5, decoders 1.0 and 0.7 ns in parallel, logic 1.8 ns ⇒ 0.5 + 1.0 + 1.8 = 3.3 ns, not 0.5 + 1.7 + 1.8 = 4.0 ns.
- **Limitation / trap:** only for truly parallel paths; if one decoder feeds the other, add. Also "stable earlier" inputs (opcode already in IR) are just paths with shorter delay; take the max of what is left.

## S4. ROM size by shift

- **What it solves:** bits/bytes of a ROM addressed by (opcode, step) with one bit per control signal.
- **Method:** words = 2^(a + b); bits = words × w; bytes = bits / 8. Compute 2^(a+b) × w by doubling w a+b times.
- **Example:** a = 4, b = 4, w = 20: 20 → ×2⁸ = 5120 bits ⇒ 640 bytes.
- **Limitation / trap:** only when there is no encoding of the control word and every address is stored. Don't add bits; they multiply (address bits are an exponent).

## S5. CPI as "base + memory extras"

- **What it solves:** change of CPI when memory latency changes, without redoing every instruction.
- **Rule:** CPI(L) = CPI(L = 1) + (average number of WMFC steps per instruction) × (L − 1).
- **Why it works:** each WMFC step lasts L cycles instead of 1; no other step changes.
- **Example (NOTES machine, mix 40/25/15/15/5 %):** average WMFC steps = 1 (fetch) + 0.25 (LD) + 0.15 (ST) + 0.05 × 2 (LDI has two) = 1.5. CPI(1) = 6.10 ⇒ CPI(3) = 6.10 + 1.5 × 2 = **9.10** (matches the direct computation).
- **Limitation / trap:** L = ⌈T_mem / T_clk⌉ must be an integer ≥ 1; the formula assumes the wait step does nothing else that is longer than L cycles.

## S6. Compare designs by time per instruction

- **What it solves:** which of two control/datapath designs is faster.
- **Method:** time = CPI × T_clk for both; ratio = time₁ / time₂.
- **Example:** single-cycle 1 × 770 = 770 ps; multi-cycle 4.10 × 220 = 902 ps ⇒ single-cycle is faster in that example.
- **Limitation / trap:** use identical overhead assumptions in both designs; for pipelines use CPI = 1 + stall cycles per instruction.

## S7. Step-splitting break-even

- **What it solves:** whether shortening the clock by splitting the longest step pays off.
- **Rule:** new CPI × new T_clk < old CPI × old T_clk, with new CPI = old CPI + (split steps per instruction).
- **Example:** 6.1 × 6.0 = 36.6 ns vs (6.1 + 1.4) × 4.4 = 33.0 ns ⇒ pays off.
- **Limitation / trap:** the new clock is capped by the *next* longest step; once the long step is shorter than that, further splitting gains nothing.

## S8. Reading an equation off a column of the table

- **What it solves:** writing a signal's equation fast.
- **Method:** put the micro-operation table in columns by instruction, rows by step; for a signal, read off which cells contain it; group by step: `(I₁ + I₂)·Tk`.
- **Check:** at most one `…out` in any cell on a single bus; a signal that appears in fetch has a pure `Tk` term.
- **Limitation / trap:** flags must be attached only to the conditional cell (`BRZ·T6·Z`).

---

## Do NOT use

1. **"Number of bits = number of steps."** Bits = ⌈log₂ steps⌉ (binary), or steps (one-hot ring) — know which.
2. **Unweighted mean of cycle counts as CPI.** Counterexample: cycles 6 and 14 with mix 95 % / 5 %: unweighted mean 10, weighted 0.95·6 + 0.05·14 = 6.4.
3. **"Multi-cycle is always faster than single-cycle."** Counterexample: NOTES §11 (770 ps vs 902 ps).
4. **"A shorter clock means a faster machine."** The CPI may rise more than the clock falls (see S7 failing case: if the new CPI were 8.5 the new time would be 8.5 × 4.4 = 37.4 ns > 36.6 ns).
5. **"Hardwired is always better because it is faster."** It is faster, but costly to design and to change for a large instruction set; GATE statements about flexibility, cost, and ISA size go the other way.
6. **Elimination of options in a RISC-characteristics question without checking each feature separately.** Check each statement on its own merits (NOTES §12.2); do not trust a pattern of options.
7. **Adding the two decoder delays** (S3) or **counting opcode decode as an extra step** in the model of NOTES §4.
