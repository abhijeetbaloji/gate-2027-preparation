# Addressing Modes — MISTAKES

Typical mistakes for this topic (general error patterns, not records of any person's errors). Theory: [NOTES.md](NOTES.md).

## 1. Conceptual confusions

| Mistake | Correct idea |
|---|---|
| Treating register addressing as if the register were an address | Register direct: the operand IS the register's content. No EA. |
| Mixing register direct and register indirect | Indirect: the register content is an *address*; one memory read follows. |
| Giving immediate an EA | Immediate has no EA; the operand is in the instruction. |
| "Indirect" always memory-indirect or always register-indirect | Read the question: if the pointer is in a register, it is register indirect. |
| Auto-increment = relocation | Relocation needs PC-relative / base-register references. Auto-increment only steps a pointer. |
| Auto-increment needs an extra EA adder | EA = register contents; only the +size update needs an adder (which may be shared). |
| Base vs index treated as different hardware | Same adder; the role (fixed vs varying) differs. |
| Direct mode can reach anything | Bounded by 2^(address-field bits). Register-based modes are bounded by register width. |
| Array ↔ offset and record ↔ index swapped (matching question) | Array element = subscript (index); record field = fixed offset (displacement). |

## 2. Formula mistakes

- Post-increment using the new value; pre-decrement using the old value.
- Increment of 1 instead of the operand size (or pointer size in `@(R)+`).
- PC-relative target = branch address + offset (should use updated PC).
- Skipping the scale factor L for offsets counted in instructions.
- Row-major vs column-major swapped; wrong dimension (rows vs columns) as the row length.
- Ignoring the lower bound `lb` of an array.
- Opcode bits: forgetting a register field; subtracting the wrong number of mode bits; dividing opcode space by number of modes when the mode field is separate.
- Pre-indexed vs post-indexed indirect EA mixed up.

## 3. Numerical / calculation mistakes

- Sign extension forgotten (0xF6 → +246 instead of −10); using an 8-bit rule on a 12-bit field.
- Hex carries: 0x3FF8 + 8 = 0x4000 (the carry ripples through the F digits).
- Bytes vs words: a 14-bit field on 4-byte words reaches 64 KB, not 16 KB.
- Counting registers as memory accesses; forgetting the instruction fetch; forgetting the store; one pointer read per indirect *level*.
- Off-by-one: backward branch to the branch itself has offset −1, not 0.
- K = 1000 instead of 1024.

## 4. PYQ-derived traps (entries that exist in the mapping; newest → oldest)

| Year / Q# | Trap pattern |
|---|---|
| 2026 Q.14 | Matching: confusing "base with index" and "base with offset"; or "indirect" vs "register indirect". |
| 2024 Q.57 | Field-budget: forgetting a register field; confusing per-mode opcode count with total opcode count. |
| 2011 Q.21 | Naming: one-register-plus-constant vs two-register vs scaled; textbook naming differences. |
| 2008 Q.33 (filed under ALU) | Statement-style: assuming auto-increment gives relocation or needs a dedicated EA ALU; forgetting that the step equals the operand size. |

## 5. Examination-time mistakes

- Answering a matching question by option-letter memory instead of constructing the pairs.
- Not stating which PC value you use in a branch question when the problem is ambiguous (state it in rough work).
- Reading "bytes" for a field the question counts in "instructions".
- Skipping the multi-word-instruction check in access counting.
- Forgetting that NAT answers need the requested unit (KB, bytes, decimal).

## 6. How to check yourself

1. Did I write the EA formula first?
2. Did I use the current register values (before the side effect for post-increment)?
3. Did I follow every pointer level?
4. Did I count: fetch + pointer reads + operand + store? Did I exclude registers?
5. Did I sign-extend and scale offsets? Did I add to the updated PC?
6. Do the units (bytes/words/KB) match the question?
7. For field budgets: did I include every field, and is the mode field separate or merged?
8. For statement questions: did I decide each by the definition (EA, side effect, absolute numbers, stride)?

---

## My Mistakes

| Date | Source | Question | Mistake | Root cause | Fix / Rule |
|------|--------|----------|---------|------------|------------|
|      |        |          |         |            |            |
