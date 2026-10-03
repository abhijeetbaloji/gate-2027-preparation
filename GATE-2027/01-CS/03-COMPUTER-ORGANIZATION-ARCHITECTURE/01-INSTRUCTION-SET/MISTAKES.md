# Instruction Set — Mistakes Log

Method and corrections: [`NOTES.md`](NOTES.md). Mapping data: [`PYQ.md`](PYQ.md). The "My Mistakes" table at the bottom is for you to fill in.

---

## 1. Conceptual confusions

1. **ISA vs organization:** believing clock frequency, cache size or pipeline depth are part of the ISA. They change speed, not the programmer-visible contract.
2. **Architectural vs physical registers:** only architectural registers (named by instruction fields) are ISA.
3. **Load–store means "no memory operand in ALU instructions"**, not "fewer instructions". It usually *raises* the instruction count.
4. **Implied operand ≠ address field:** the accumulator and top of stack are named by the opcode, not by a field. An address field names a memory location or a register.
5. **Stack machine ≠ stack in memory:** a stack machine's ALU operands are the top two entries; `PUSH`/`POP` are its only memory-accessing instructions.
6. **Two-address destroys the first operand;** a three-address instruction does not.
7. **MIPS is not performance;** a lower-MIPS machine can finish sooner if its instruction count is lower.
8. **RISC vs CISC mix-ups:** hardwired control, fixed length, load/store are RISC traits; microprogrammed control and memory-operand arithmetic are CISC traits (typical, not absolute).
9. **Endianness changes byte order only,** not the address of the word (always the lowest-addressed byte).

## 2. Formula mistakes

1. **Bits vs count:** field width is ⌈log₂ n⌉ for n objects. 64 registers → 6 bits, not 64.
2. **Floor instead of ceiling:** 24 registers need 5 bits (2⁴ = 16 < 24).
3. **Combining register fields:** ⌈log₂ r³⌉ ≠ 3⌈log₂ r⌉ (24 registers: 14 vs 15).
4. **Max opcodes of the target:** subtracting n_i directly instead of n_i × 2^(o_T − o_i).
5. **Floor each type separately** instead of adding exact fractions and flooring once.
6. **Chain recursion misuse:** (S − n) must be multiplied by 2^w (width of the freed field), once per level.
7. **Opcode length written as the full L − 3w for every format:** each type has its own o_t = L − its operand bits.
8. **Equal-split flat opcode applied to an unequal split** with a format bit.
9. **Double-counting the format bit** (adding 1 to ⌈log₂ total⌉).
10. **Amdahl:** using the fraction of instructions instead of the fraction of original *time*.
11. **Weighted CPI:** weights must be instruction fractions summing to 1.

## 3. Numerical / calculation mistakes

1. Byte-aligned size computed as ⌈N·b/8⌉ instead of N·⌈b/8⌉.
2. Bits vs bytes in the final answer (program size in bytes, immediates in bits).
3. 1 K = 1000 instead of 1024 when converting memory size to address bits.
4. "x % less time" turned into ratio x instead of 1 − x; "x % more CPI" into x instead of 1 + x.
5. Unit slips: MIPS uses 10⁶ (not 10⁹); GHz ↔ ns.
6. Stack instruction count forgetting the final POP, or counting a repeated variable once.
7. Accumulator count forgetting the final STORE, or the temporary STORE when both operands are intermediate.
8. Two-address count: forgetting `MOV` of an input into a scratch location; or forgetting that the final result must reach the destination.
9. Counting memory accesses without the instruction fetches, or counting `ADD d, s` as 2 data accesses (it reads d, reads s, writes d → 3).
10. Register-pressure count including dead variables or ignoring that the destination can reuse a dying source's register.

## 4. PYQ-derived traps (kinds of question; no answers given)

Entries below exist in the mapping ([`questions.md`](../../13-PYQ-TOPIC-MAPPING/03-COMPUTER-ORGANIZATION-ARCHITECTURE/01-INSTRUCTION-SET/questions.md)); newest → oldest.

| Year / Q# | Trap pattern |
|---|---|
| 2026 CS-2 Q44 | Expanding opcodes with three formats of different opcode lengths; the target's opcode is the longest, so no fractions, but each used opcode must be scaled by 2^(o_T − o_i). |
| 2026 CS-1 Q15 | Load–store with a destination-first convention: reject any sequence whose ALU instruction names a memory operand, and check STORE operand order. |
| 2025 CS-1 Q37 | Maximum immediate bits: read the instruction shape to count register fields (one register in an add-immediate form); register count not a power of two. |
| 2024 CS-2 Q61 | Format bit + equal division + "UNUSED" field; the opcode field includes the format bit; combine X, Y, Z into the asked expression only at the end. (The mapping entry also carries an unrelated regular-expression sentence — ignore it.) |
| 2020 CS Q44 | Two-format fixed length, maximum opcodes of the second format given a count of the first: compute o for both formats, then scale (check which format has the shorter opcode — scaling then divides, giving fractions). |
| 2016 CS-2 Q31 | Byte-aligned per-instruction padding; five fields including three register identifiers. |
| 2016 CS-2 Q10 | Register count not a power of two ⇒ ceiling; two register fields; "immediate bits available". |
| 2015 CS Q22 | "Implied accumulator" is not named by an address field. |
| 2013 (Booklets A–D) | Liveness/spill questions whose code segment is absent from the mapping text; do not guess numbers. |

Related traps from questions filed under other leaves (not counted in this topic's mapping): mixed integer/floating-point register widths changing opcode lengths (2018), "opcodes per addressing mode" with a mode field (2024 CS-2 Q57), iron-law ratio with relative CPI/time (2014).

## 5. Examination-time mistakes

1. Not rereading the instruction shape (extra/missing register field).
2. Skipping the "state assumptions" step: addressability, whether inputs may be overwritten, whether the destination can be scratch.
3. Doing the whole encoding in decimal fractions without sanity-checking 0 ≤ answer ≤ 2^(o_T).
4. Spending time counting the optimal accumulator program when the recursion gives it in seconds.
5. Forgetting to convert the final answer to the requested unit (bytes, ms, GHz).

## 6. How to check yourself

- [ ] Do the fields I subtracted add back to L exactly?
- [ ] Is every ⌈log₂ ⌉ computed on a count (not on a bit count) and rounded up?
- [ ] Did I use the right opcode length for **each** format?
- [ ] For expanding opcodes: converted all used opcodes to the target's unit and floored once?
- [ ] Is 0 ≤ answer ≤ 2^(o_T)? Do used counts already fit in their own slices?
- [ ] Program size: per-instruction rounding?
- [ ] Machine-code count: did I include POP/STORE/MOV and a temporary where needed?
- [ ] Performance: instruction fractions for CPI, time fractions for Amdahl, 10⁶ for MIPS?

---

## My Mistakes

| Date | Source | Question | Mistake | Root cause | Fix / Rule |
|------|--------|----------|---------|------------|------------|
| | | | | | |
