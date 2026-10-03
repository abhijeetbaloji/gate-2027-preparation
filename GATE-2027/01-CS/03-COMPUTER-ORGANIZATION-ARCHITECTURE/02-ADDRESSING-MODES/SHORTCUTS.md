# Addressing Modes — SHORTCUTS

Only shortcuts that are valid under the stated conditions. Background: [NOTES.md](NOTES.md); formulas: [FORMULAS.md](FORMULAS.md).

---

## S1. Memory-reference count = fetches + (pointer reads) + (operand reads/writes)

- **What it solves:** "how many memory accesses does this instruction / sequence perform?"
- **When:** any count that includes instruction fetch, one-word instructions, registers not counted.
- **Why it works:** every mode is "form EA, then touch memory once" with indirection adding one read per pointer level. Immediate and register modes touch no data memory.
- **Quick table (data refs):** imm 0, reg 0, direct 1, reg-indirect 1, disp/index/scaled/PC-rel 1, auto-inc/dec 1, memory-indirect L levels → L + 1.
- **Example:** `ADD R1, @(L1)` with one level = 1 fetch + 2 data = 3. A 4-instruction loop body with 2 loads and 1 store, all one word: 4 + 3 = 7.
- **Limit:** change it when the instruction is longer than a memory word (add fetches), when the question counts only *data* accesses, or when it counts the "execute-time" accesses of a micro-programmed implementation.

## S2. Post-increment uses the OLD value, pre-decrement uses the NEW value

- **What it solves:** tracing `(R)+` / `-(R)` sequences and stack push/pop.
- **Why:** definition of the modes. A pre-decrement followed by a post-increment on the same register and size accesses the **same address** and leaves the register unchanged.
- **Example:** R = 80, s = 2: `(R)+` → EA 80, R = 82; then `-(R)` → R = 80, EA 80.
- **Limit:** applies when both use the same register and the same operand size; if sizes differ the register does not return to the start.

## S3. Opcodes per mode = 2^(opcode bits); never divide by the number of modes when the mode field is separate

- **What it solves:** field-budget questions ("opcodes possible for every mode").
- **Why:** a separate mode field means every (opcode, mode) combination is a distinct bit pattern; each mode may reuse all opcode patterns.
- **Example:** 32-bit instruction, 3-bit mode, two 5-bit register fields, 12-bit literal: opcode bits = 32 − 3 − 10 − 12 = 7 → 128 per mode.
- **Limit:** if the mode is merged into the opcode field (total w bits), the number of opcodes that support every one of μ modes is 2^w / μ.

## S4. Count branch distance in instructions, not bytes

- **What it solves:** PC-relative problems with fixed-length instructions and an offset counted in instructions.
- **Why:** `target = PC_updated + offset × L`; so target is "offset instructions after the next instruction". A target 5 instructions ahead of the next instruction has offset +5; one instruction back (the branch itself) has offset −1.
- **Example:** 4-byte instructions, field −3 → target = next instruction address − 12.
- **Limit:** only when the field is counted in instructions and the target is aligned. If the field is in bytes, do not multiply.

## S5. Negative hex offset: magnitude = 2ⁿ − field

- **What it solves:** reading signed hex displacements quickly.
- **Why:** two's complement. 8-bit 0xF6: 256 − 246 = 10 → −10. 16-bit 0xFFE0: 65536 − 65504 = 32 → −32.
- **Check first:** the sign bit is the top bit **of the field width given** (8-bit field: ≥ 0x80 is negative; 12-bit field: ≥ 0x800 is negative).
- **Limit:** do not apply an 8-bit rule to a 12-bit field.

## S6. Classify an address mode by "number of registers + constant + scale + pointer-read"

- **What it solves:** naming questions and matching questions.
- **Why:** the mode is *defined* by how EA is assembled: 1 register + constant → displacement family; 1 register alone → register indirect; 2 registers → base+index; register × s → scaled; extra memory read → indirect; none → direct/immediate.
- **Example:** EA = R2 + R5×8 + 12 → scaled index with displacement.
- **Limit:** words differ between books; use the formula and match it to the closest option.

## S7. Matching HLL elements: constant → immediate, pointer → indirect, subscript → index, fixed field offset → base + offset

- **Why:** each mode puts the *changing* quantity where the program changes it: constant (never changes), pointer (data holding an address), subscript (varies per iteration, register), struct field (constant offset added to a record base).
- **Limit:** the compiler may implement an array element with a pointer or displacement; the exam wants the canonical pairing.

## S8. Direct-mode reach = 2^a × (bytes per addressable unit)

- **Example:** 18-bit address field on a byte-addressable machine → 256 KB; on a machine with 2-byte words → 512 KB.
- **Limit:** applies to direct mode only; register-based modes are limited by register width.

## S9. Step between neighbouring array elements

- **What it solves:** address of A[i+1] given A[i]: add `size`. Next row (row-major): add C × size; next column in column-major: add R × size.
- **Example:** 4-byte, 30 columns, row-major: moving one row down adds 120 bytes.
- **Limit:** ignores bound changes; recompute for lower bounds ≠ 0.

## S10. Scaling doubles / quadruples reach

- A PC-relative field counted in instructions of length L reaches L times farther than the same field counted in bytes.
- **Limit:** requires aligned targets.

---

## Do NOT use

1. **"Indirect always means 2 accesses."** It means 2 data accesses for one level (3 with the fetch). For a 3-level chain there are 4 data accesses (5 with the fetch).
2. **"Offset field ≥ 0x80 means negative."** Only for an 8-bit field. A 12-bit field 0x0F0 is +240.
3. **"Divide opcode space by the number of modes."** Only when mode bits are merged into the opcode, not when the mode field is separate.
4. **"The register that is bigger is the base."** Role, not value, makes a register the base or index; EA = Rb + Ri is symmetric.
5. **"PC-relative offset is always added to the branch address."** Add to the updated PC unless the question states otherwise.
6. **"Auto-increment steps by 1."** It steps by the operand size; for autoincrement-deferred, by the pointer size.
7. **"Immediate addressing has EA = the literal."** There is no EA; the literal is the operand.
