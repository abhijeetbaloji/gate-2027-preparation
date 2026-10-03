# Microprogrammed Control — Mistakes to avoid

Generic, anticipated mistakes (nothing here is a record of your own errors; use the empty table at the bottom for that). Theory in [NOTES.md](NOTES.md).

## 1. Conceptual confusions

| Mistake | Correct idea |
|---|---|
| Treating control memory as main memory / user-addressable | It is an internal store, usually ROM (or WCS), invisible to user programs. |
| Mixing micro-operation, microinstruction, machine instruction | Machine instruction = sequence of microinstructions; microinstruction = one row with several micro-operations. |
| Thinking each machine instruction has its own fetch microroutine | One shared fetch routine; the opcode is mapped to the execute routine at the end of fetch. |
| Calling CAR the "PC" of the program | The PC addresses main memory instructions; CAR addresses the control store. |
| "Horizontal is always faster **and** smaller" | Horizontal is wider (more bits per word) but needs fewer, parallel microinstructions and no decoders. |
| "Vertical = slower only because ROM is slower" | Vertical needs a decoder per field and often more microinstructions. |
| "Nanoprogramming reduces storage regardless of data" | Only when D ≪ M; it also adds a second access. |
| Mixing the two "two-level" ideas | Field decoding (decoder level) ≠ nanoprogramming (second memory). |
| "Microprogrammed control is slower in every aspect" | It is slower than hardwired for the same function; it is more flexible and easier to modify. Compare as the question frames it. |

## 2. Formula mistakes

| Mistake | Fix |
|---|---|
| Field bits = ⌈log₂ n⌉ when "none" is allowed | Use ⌈log₂ (n + 1)⌉. Differs exactly at powers of two (8 → 4, 16 → 5). |
| Encoding signals that must be asserted together | They need separate fields/bits. Mutually exclusive only. |
| Sum then ceiling: ⌈log₂ (n₁ + n₂ + …)⌉ | Ceiling **per group**, then add. |
| CAR bits = ⌊log₂ N⌋ | Ceiling: N = 29 → 5, N = 65 → 7. |
| Horizontal width = number of signals only | Add next-address, condition-select and sequencing-mode bits. |
| Condition select = ⌈log₂ k⌉ with an "unconditional" option | Use ⌈log₂ (k + 1)⌉ if "always" shares the field. |
| Saving of encoding using different N for the two designs | Same N → N × ΔW; different N → compute each total. |
| Nano two-level = M × p only | Add D × W for the nanostore. |
| Microcycle as sum even when the word is latched and overlapped | Overlapped t_µ = max(t_CS, t_dec + t_dp). |

## 3. Numerical / calculation mistakes

- Bits vs bytes: 841 bits is not 841 bytes; divide by 8 only if asked.
- Counting the shared fetch once per instruction.
- Counting fetch twice when per-instruction counts already include it.
- Forgetting the mapping ROM (or the next-address bits in the width).
- Using a different next-address width in the compared designs, although it follows from N (⌈log₂ N⌉).
- Off-by-one in loops: the test after the decrement runs the body exactly n times.
- A "taken" branch vs "not taken" branch: number of microinstructions differs (Mini-1 BZ: 6 vs 4 incl. fetch).
- Forgetting the 1 K = 2¹⁰ convention for "1 K microinstructions" (= 1024).
- Using control-store access time only when the question defines the microcycle as access + decode + datapath (or the opposite).

## 4. PYQ-derived traps

**No mapped PYQ exists for this leaf**, so no PYQ-derived trap is claimed here. See [PYQ.md](PYQ.md). The nearest real items (in other folders) are a RISC design-characteristics comparison (2018 Q.5, hardwired sibling) and a register-transfer-list reading question (2013, mapped to the interrupt topic). Their trap *kinds*, without answers:
- Comparison questions: do not rely on a single slogan; check each characteristic separately.
- Register-transfer lists: identify the data flow (which register is saved to memory, which is loaded) before choosing the named operation.

## 5. Examination-time mistakes

- Skipping the statement that says whether "none" is a legal code.
- Not noticing "at most one" vs "exactly one".
- Not noticing "the next-address field is the only successor mechanism" (so micro-PC increment is excluded).
- Mixing "control word width" with "microinstruction width" when the problem lists sequencing fields separately.
- Not reading whether the store size should be words, bits or bytes.

## 6. How to check yourself

1. Underline: N, W, groups, "none", "at most one", simultaneity, units.
2. Write CAR = ⌈log₂ N⌉ before anything else.
3. Does every group have a ceiling and "+ none" if allowed?
4. Did you count shared fetch once?
5. Re-sum widths in a column (signals, mode, condition, address).
6. For comparisons (vertical vs horizontal, nano vs flat, micro vs hardwired): did you compute both sides?
7. Time questions: write which microcycle model is used.

---

## My Mistakes

| Date | Source | Question | Mistake | Root cause | Fix / Rule |
|---|---|---|---|---|---|
| | | | | | |
