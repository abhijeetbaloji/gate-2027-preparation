# Microprogrammed Control — Formulas

Conventions: 1 K = 2¹⁰. Widths are in **bits**. `⌈x⌉` = ceiling. All examples were checked by script. Context and derivations: [NOTES.md](NOTES.md). Sibling topic: [hardwired control](../01-HARDWIRED/NOTES.md).

Symbols: N = number of control-store words (microinstructions); W = bits per word; a = next-address field bits; c = condition-select bits; p = nano pointer bits; D = distinct control patterns; M = microinstructions; t_CS = control-store access time; t_µ = microcycle.

---

## A. Addressing the control store

### A1. CAR (micro-PC) width

```
 CAR bits = ⌈log₂ N⌉
```
- **When:** a CAR that must be able to hold the address of any of N words.
- **Why:** b bits give 2ᵇ addresses, need 2ᵇ ≥ N.
- **Example:** N = 1000 → 10 bits (2⁹ = 512 < 1000 ≤ 1024). N = 100 → 7. N = 128 → 7. N = 129 → 8. N = 29 → 5.
- **Misuse:** using N − 1 or ⌊log₂ N⌋; using log₂ of the *bit count* instead of the word count.

### A2. Words addressable by an absolute next-address field

```
 words addressable = 2ᵃ
```
- **When:** the only way a word names its successor is an a-bit absolute field.
- **Example:** a = 9 → 512 words (not 9, 18 or 1024).

### A3. Opcode-concatenation layout

```
 CAR bits = (opcode bits) + (step bits) ; address = opcode ‖ step ; routine block = 2^(step bits) words
```
- **When:** start address = opcode shifted left by `step bits`.
- **Why:** each opcode owns a block of 2^s consecutive words.
- **Example:** 4-bit opcode, s = 3 → CAR 7 bits, 128-word space, longest routine without jumping out = 8.
- **Misuse:** forgetting that shorter routines still occupy the whole block (unused words count if the question asks "size of control store").

### A4. Mapping ROM size

```
 mapping ROM bits = 2^(opcode bits) × CAR bits         (one entry per possible opcode value)
```
- **When:** a ROM translates opcode → start address. Use the number of **possible opcode values** (2^bits) unless told only some are implemented.
- **Example:** Mini-1: 4 entries × 4 bits = 16 bits. 5-bit opcode, CAR 7 → 32 × 7 = 224 bits.

---

## B. Field encoding and word width

### B1. Bits of one encoded field

```
 exactly one of n always chosen :  ⌈log₂ n⌉
 at most one of n (none allowed) :  ⌈log₂ (n + 1)⌉
```
- **Why:** need n (or n + 1) distinct codes.
- **Examples:** n = 20 with none → 5; n = 8 with none → **4**; n = 8 without none → 3; n = 16 with none → 5; n = 15 with none → 4; n = 1 with none → 1.
- **Misuse:** forgetting + 1; applying it to signals that can be asserted **simultaneously**.

### B2. Independent (direct) signals

```
 k signals that may be asserted together and are not grouped : k bits
```
- A one-signal group costs exactly 1 bit (= the horizontal case).

### B3. Horizontal width

```
 W_horizontal = (signals) + (sequencing: mode + c) + a
```
- **Example:** 18 signals + 3-bit condition select + 6-bit next address, no encoding, no separate mode field → 27 bits.

### B4. Field-encoded width

```
 W_encoded = Σ over groups ⌈log₂ (nᵢ + 1)⌉  +  (direct signal bits)  +  (sequencing bits)  +  a
```
- Apply the ceiling **per group**, not to the total. Example: groups of 3 and 3 with none → 2 + 2 = 4, not ⌈log₂ 7⌉ = 3.
- Minimum number of groups = colouring of the "asserted together" conflict graph (NOTES 5.5). Example: 6-cycle conflict among six signals → two groups of three → 4 bits.

### B5. Condition-select field

```
 c = ⌈log₂ (k + 1)⌉        k testable conditions plus an "always / no test" code
 c = ⌈log₂ k⌉              if unconditional jumps have their own mode and c covers only conditions
```
- **Example:** 6 conditions + unconditional → 3; 8 conditions + unconditional → **4** (not 3).

### B6. Sequencing-format widths

```
 one-address + cond :  a + c
 two-address + cond :  2a + c
 variable format    :  ROM word = 1 + max(signal bits, c + a)
```
- **Example:** 18 signal bits, c = 3, a = 7 → 28 / 35 / 19. Saving of variable vs one-address = 9 bits per word.
- **Misuse:** forgetting that variable format needs extra words for branch-only microinstructions; compare total (words × width).

---

## C. Control-store size

### C1. Number of words

```
 N = (shared fetch words) + Σ over instructions (execute-routine words)
```
- Fetch counted **once**. If per-instruction counts already include fetch, do not add it again.
- **Example:** fetch 3; routines 4, 6, 3, 8, 5 → N = 29, CAR = 5.

### C2. Total bits

```
 control-store bits = N × W            (+ mapping ROM bits if present)
```
- **Example:** 29 words × (24 + 5) = 841 bits. Mini-1 encoded: 14 × 19 = 266 bits (+16 map). Horizontal: 14 × 30 = 420 bits.
- **Bytes:** bits / 8. Keep bits unless asked (841 bits is not a whole number of bytes).
- **Misuse:** using N = 2^CAR when the ROM is physically smaller (state which: used words vs address space). In a shift layout, the address space is 2^(CAR bits) words.

### C3. Saving of encoding

```
 saving = N × (W_horizontal − W_encoded)       (same N)
```
- **Example:** 300 words, 50 − 30 = 20 bits each → 6 000 bits.
- **Misuse:** if the two designs have different N (vertical needs more words), compute N_h × W_h − N_v × W_v instead. E.g. 300 × 56 = 16 800 vs 410 × 31 = 12 710.

### C4. Subroutine sharing

```
 inline words   = (callers) × (routine length)
 shared words   = (routine length) + (callers)          (one call word per caller; return folded into last word)
 saving         = inline − shared
```
- **Example:** 10 callers × 5-word routine: 50 vs 15 → saves 35 words; +1 microcycle per call.

---

## D. Nanoprogramming

### D1. Two-level store size

```
 p = ⌈log₂ D⌉
 flat       = M × W
 two-level  = M × p + D × W
 beneficial iff  M × p + D × W < M × W   (needs D ≪ M)
```
- **Example:** M = 2048, W = 100, D = 256 → p = 8; flat 204 800; two-level 41 984 bits. Counter-example: M = 512, W = 60, D = 500 → 34 608 > 30 720.
- **Misuse:** forgetting the nanostore term D × W; forgetting that sequencing bits (if given) are in the microstore word as well.

### D2. Extra control-store time

```
 t_control-store ≈ t_micro + t_nano        (serial accesses)
```
- **Example:** 10 + 12 = 22 ns. Overlap/pipelining of the two accesses is only valid if the question says so.

---

## E. Timing and CPI

### E1. Microcycle

```
 non-overlapped : t_µ = t_CS + t_decode + t_datapath
 overlapped     : t_µ = max(t_CS, t_decode + t_datapath)
```
- **Example:** 10, 2, 12 ns → 24 ns vs 14 ns.
- **Misuse:** using the overlapped formula when the question says the next word is fetched only after the current one completes; adding decode/datapath when the question defines the microcycle as the access time.

### E2. Machine-instruction control time

```
 T_instr = (microinstructions executed, fetch included) × t_µ
 difference to hardwired = n_µ × t_µ − n_clk × T_clk
```
- **Example:** 6 × 24 = 144 ns vs 4 × 12 = 48 ns → +96 ns. Overlapped with one wasted cycle at a taken jump: (6 + 1) × 14 = 98 ns.

### E3. Average CPI in microcycles

```
 CPI = Σ fᵢ × µᵢ ;  CPU time = IC × CPI × t_µ     (one microinstruction per clock)
```
- **Example (Mini-1 mix 40/30/10/10/10 %, µ = 6, 5, 6, 6, 4):** CPI = 5.5; at 10 ns → 55 ns per instruction.
- **Misuse:** weighting with percentages that do not sum to 1; counting fetch twice.

### E4. Loop microroutine count

```
 microinstructions = fetch + setup + (body length × iterations) + finish
```
- **Example:** 3 + 1 + 3n + 1; n = 4 → 17.

---

## F. Qualitative relations (stated as comparison rules)

| Relation | Direction |
|---|---|
| Horizontal vs vertical: word width | horizontal wider |
| Horizontal vs vertical: parallelism | horizontal more |
| Horizontal vs vertical: number of microinstructions for the same job | vertical more |
| Horizontal vs vertical: decoder delay | vertical has it |
| Total bits (N × W) | depends — compute |
| Microprogrammed vs hardwired: speed | hardwired faster (same functionality) |
| Microprogrammed vs hardwired: modification | microprogrammed easier |
| Nanoprogramming vs flat store: storage / speed | less storage / slower |
| Writable vs ROM control store: flexibility / per-bit cost-speed | WCS more flexible / usually costlier and slower |
