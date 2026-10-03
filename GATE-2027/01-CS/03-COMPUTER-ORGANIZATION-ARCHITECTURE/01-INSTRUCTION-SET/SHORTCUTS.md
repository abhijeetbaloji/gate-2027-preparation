# Instruction Set — Shortcuts

Only shortcuts that are mathematically valid under the stated condition. Background: [`NOTES.md`](NOTES.md). Examples recomputed by script.

---

## S1. Powers-of-two ladder for field sizes
- **What it solves:** ⌈log₂ n⌉ in your head.
- **When to use:** any "how many bits to name n things".
- **Why it works:** ⌈log₂ n⌉ is the smallest b with 2ᵇ ≥ n. Memorise 2⁵=32, 2⁶=64, 2⁷=128, 2⁸=256, 2¹⁰=1024.
- **Example:** 90 types → 64 < 90 ≤ 128 → 7. 24 registers → 16 < 24 ≤ 32 → 5. 100 operations → 7.
- **Limitation / trap:** n must be the *count*; exactly a power of two gives that exponent (64 → 6), one more gives +1 (65 → 7).

## S2. "Draw the boxes, subtract" for the leftover field
- **What it solves:** maximum immediate/offset bits.
- **When to use:** one undetermined field in a fixed-length instruction.
- **Why it works:** the fields partition the L bits.
- **Example:** L = 36, 70 types (7), three register fields from 40 registers (3 × 6 = 18): 36 − 7 − 18 = **11**.
- **Limitation / trap:** each register field is ⌈log₂ r⌉ **separately** — do not take ⌈log₂(r³)⌉. (24 registers: 3×5 = 15 bits, but ⌈log₂ 24³⌉ = 14 — wrong shortcut.) Count the register fields from the given instruction.

## S3. Work in the target's unit (cake rule in integers)
- **What it solves:** maximum opcodes of a target type when other formats have used some.
- **When to use:** variable-length opcodes in a fixed-length instruction; target has the longest opcode (no fractions) or any length (fractions allowed).
- **Why it works:** an opcode of length o_i uses 2^(o_T − o_i) of the target's opcode slots. Convert every used opcode into target slots, add, subtract from 2^(o_T), floor once.
- **Example:** o = 3 (5 used), o = 5 (9 used), target o = 7: 5·16 + 9·4 = 116 slots used → 128 − 116 = **12**.
- **Limitation / trap:** if some o_i > o_T the conversion is a fraction; add all fractions before flooring. Not valid when a separate format bit or a reserved range is stated.

## S4. Chain recursion for 3 → 2 → 1 → 0 address schemes
- **What it solves:** how many 2-/1-/0-address opcodes survive after using some in the higher-address level.
- **When to use:** the free address field of the same width w is consumed as extension, and **all** unused prefixes are extended.
- **Why it works:** each unused prefix times 2ʷ gives the next level's slots.
- **Example:** L = 20, w = 5, 3-address opcode 5 bits (32 slots), use 20 → (32−20)·32 = 384; use 300 → (384−300)·32 = 2688; use 2000 → (2688−2000)·32 = **22016**.
- **Limitation / trap:** operand fields freed per level may have different widths (then multiply by 2^(freed bits) each time); if a level is only partially extended, use S3.

## S5. Equal split ⇒ flat opcode bits
- **What it solves:** opcode width when a format bit selects between two equally large types.
- **Why it works:** 1 + ⌈log₂(n/2)⌉ = ⌈log₂ n⌉ for every n (checked for n = 2…10 000).
- **Example:** 180 instructions equally split → 1 + ⌈log₂ 90⌉ = 8 = ⌈log₂ 180⌉.
- **Limitation / trap:** fails for unequal splits (100 R + 20 I: shared field needs 7 bits + 1 format bit = 8, whereas ⌈log₂ 120⌉ = 7).

## S6. Per-instruction rounding for byte-aligned size
- **What it solves:** program size in bytes.
- **Why it works:** every instruction starts on a byte boundary.
- **Example:** 33 bits/instruction → 5 bytes; 250 instructions → **1250 bytes** (not ⌈250·33/8⌉ = 1032).
- **Limitation / trap:** if the question says instructions are packed without alignment, the total-bits formula is the right one — read the sentence.

## S7. Stack-machine count: leaves + ops + 1; depth by scanning
- **What it solves:** instruction count and maximum depth of a postfix evaluation.
- **When to use:** zero-address machine, no DUP/SWAP, each leaf occurrence distinct.
- **Why it works:** one PUSH per leaf, one instruction per operator, one POP for the result; depth = running (+1 per operand, −1 per operator) maximum.
- **Example:** V = (A−B)·(C+D)/(E−F): 6 + 5 + 1 = **12**; `AB+ CD+ * EF+ GH+ * *` has maximum depth **4**.
- **Limitation / trap:** a repeated variable is pushed again each time; a machine with DUP changes the count.

## S8. Accumulator machine: store only when both children are complex
- **What it solves:** instruction count with one accumulator and temporaries in memory.
- **Why it works:** the accumulator holds one intermediate; a second complex operand must be parked (STORE) and used as a memory operand.
- **Example:** Y = (A+B)·(C+D) − E: cost(A+B) = 2, cost(C+D) = 2, product (both complex) = 2 + 2 + 2 = 6, `− E` leaf +1 = 7, final STORE +1 = **8**.
- **Limitation / trap:** non-commutative operator with a complex right child and leaf left child costs +3 (STORE T; LOAD left; OP T), not +1.

## S9. Peak live count = registers (straight-line code)
- **What it solves:** minimum registers with no spill.
- **When to use:** no branches; destination may reuse a dying source's register.
- **Why it works:** interval graphs are colourable with their maximum clique.
- **Example:** `p=a+b; q=a-b; r=p*q; s=p+r; t=q*s` with a, b live-in: peak 3 → 3 registers.
- **Limitation / trap:** with branches the peak is only a lower bound; also code motion can reduce the peak, so check if reordering is allowed.

## S10. Ratio method for relative-performance questions
- **What it solves:** unknown frequency/CPI/time when only relative changes are given.
- **Why it works:** T = IC·CPI/f, so T₂/T₁ = (CPI₂/CPI₁)(f₁/f₂) if IC is equal.
- **Example:** 40 % less time (0.6) with 25 % more CPI (1.25), f₁ = 2 GHz → f₂ = 2·1.25/0.6 = 4.1667 GHz ≈ **4.17 GHz**.
- **Limitation / trap:** only when IC is unchanged (same program, same ISA). Convert "x % less/more" into ratios correctly.

---

## Do NOT use

1. **"Opcodes left = total − used" without scaling.** Counterexample: o = 3 type uses 5 opcodes, target has 7-bit opcodes: 128 − 5 = 123 is wrong; the correct value (with nothing else) is 128 − 5·16 = 48.
2. **Rounding each other-type's prefix usage up separately.** Counterexample: target o = 6, two other types with 8-bit opcodes, 37 and 10 used: per-type rounding gives 64 − 10 − 3 = 51, correct ⌊64 − 47/4⌋ = **52**.
3. **Flat ⌈log₂ n⌉ for unequal two-type formats with a format bit** (S5 counterexample).
4. **MIPS to compare processors with different ISAs.** Counterexample: A 1000 MIPS with 3×10⁹ instructions takes 3 s; B 400 MIPS with 8×10⁸ instructions takes 2 s.
5. **"Fewer instructions ⇒ fewer memory references."** In the §4.3 example the 3-address version takes 4 instructions but 12 data references, the load–store version 10 instructions but 6.
6. **Maximum pressure = registers needed when there are branches.** Build the interference graph.
7. **Unit-less "per cent" arithmetic in the ratio method:** "20 % more CPI" is ×1.2, not ×0.2.
