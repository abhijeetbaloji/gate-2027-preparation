# Addressing Modes — PRACTICE (original questions)

24 original questions, answers directly under each. All numbers were script-verified. Conventions unless a question says otherwise:
byte-addressable memory; K = 2¹⁰; one-word instructions fetched with one memory access; register accesses are not memory accesses;
the PC already points to the next instruction when an address is formed. Theory: [NOTES.md](NOTES.md).

---

## Level 1 — Conceptual

### Q1 — MCQ — Level 1
For which of the following addressing modes does the notion of an *effective address* **not** apply?

A. Direct  
B. Immediate  
C. Register indirect  
D. Memory indirect

**Answer:** B

**Solution:** An effective address is the memory address of the operand. Direct: EA = k. Register indirect: EA = contents of the register. Memory indirect: EA = M[k]. Immediate: the operand is the literal in the instruction, so there is no memory address to compute.

**Concept tested:** EA vs operand (NOTES §3.1, §4.2).

**Difficulty:** Easy.

**Common trap:** Calling the immediate literal the "EA".

---

### Q2 — NAT — Level 1
A word-addressable machine has 4-byte words and uses direct addressing with a 14-bit address field. How many kilobytes of memory can the address field reach directly? (K = 2¹⁰ bytes.) Give an integer.

**Answer:** 64

**Solution:** 2¹⁴ words are addressable. 2¹⁴ × 4 bytes = 65536 bytes = 65536 / 1024 = 64 KB.

**Concept tested:** Address-field width vs addressable memory (NOTES §9.3).

**Difficulty:** Easy.

**Common trap:** Reporting 2¹⁴ bytes = 16 KB by forgetting that each address names a 4-byte word.

---

### Q3 — NAT — Level 1
Register `R5` holds 0x3FF8. The instruction `LOAD R1, (R5)+` loads an 8-byte operand with post-increment, on a byte-addressable machine. What is `R5` after the instruction, as a decimal integer?

**Answer:** 16384

**Solution:** The EA is the old value 0x3FF8. Then R5 ← R5 + 8 = 0x3FF8 + 8 = 0x4000 = 4 × 4096 = 16384.

**Concept tested:** Increment equals operand size; post-increment (NOTES §4.7).

**Difficulty:** Easy.

**Common trap:** Adding 1, or answering with the hex value without converting.

---

## Level 2 — Standard GATE

### Q4 — NAT — Level 2
A 4-byte branch instruction is located at byte address 2048 (decimal). It uses PC-relative addressing; the offset field is +9 and is counted in **instructions**. The PC is already incremented. What is the branch target address (decimal)?

**Answer:** 2088

**Solution:** PC_updated = 2048 + 4 = 2052. Byte offset = 9 × 4 = 36. Target = 2052 + 36 = 2088.

**Concept tested:** PC-relative target with scaling (NOTES §7.1–7.2).

**Difficulty:** Easy–medium.

**Common trap:** Using 2048 as the base (gives 2084), or adding 9 bytes (2061).

---

### Q5 — MCQ — Level 2
Match each high-level element in List I with the addressing mode that suits it best in List II.

| List I | List II |
|---|---|
| P. the literal 7 in `count = count + 7` | 1. base + index |
| Q. `v = *q`, where `q` is held in a register | 2. immediate |
| R. field `salary` of a record whose start address is in a register | 3. register indirect |
| S. `tbl[k]` with the table start in one register and `k` (already in bytes) in another | 4. base with displacement |

A. P–2, Q–3, R–4, S–1  
B. P–2, Q–4, R–3, S–1  
C. P–2, Q–3, R–1, S–4  
D. P–3, Q–2, R–4, S–1

**Answer:** A

**Solution:** The literal is an immediate. A pointer held in a register is dereferenced by register indirect. A record field has a fixed offset from a record start held in a register ⇒ base with displacement. A table element has two run-time parts (start, subscript) ⇒ base + index. B swaps Q and R, C swaps R and S, D swaps P and Q.

**Concept tested:** Mode ↔ construct matching (NOTES §5).

**Difficulty:** Medium.

**Common trap:** Assigning "index" to the record field because the word "offset" feels like an index.

---

### Q6 — MSQ — Level 2 (one or more options correct; no partial marking)
Select **all** correct statements.

A. In memory-indirect addressing, the reachable memory size is bounded by the width of the pointer word, not by the width of the instruction's address field.  
B. Base-register addressing allows a program to be relocated by changing one register.  
C. Post-increment addressing makes a program position-independent.  
D. Direct addressing with a 16-bit address field can reach every byte of a 4 GB byte-addressable memory.

**Answer:** A, B

**Solution:** A: the pointer is read from memory and may be 32 bits; the address field only locates the pointer. B: all addresses are base + offset, so moving the block means changing the base. C: false; the register that steps through memory must still be initialised to an address, so the mode itself does not remove absolute addresses; PC-relative or base-register forms do. D: 16 bits reach only 2¹⁶ locations.

**Concept tested:** Reach, relocation (NOTES §7.6, §9.3).

**Difficulty:** Medium.

**Common trap:** Crediting auto-increment with relocation properties.

---

### Q7 — NAT — Level 2
A one-word load uses **three-level indirection**: the instruction's address field names a location holding a pointer; the target of that pointer holds a second pointer; the target of the second holds a third pointer; the target of the third pointer is the operand. How many memory accesses does the instruction perform in total, counting the instruction fetch? (Result goes to a register.)

**Answer:** 5

**Solution:** 1 instruction fetch + 3 pointer reads + 1 operand read = 5.

**Concept tested:** Reference counting with L-level indirection (NOTES §10.2).

**Difficulty:** Medium.

**Common trap:** Counting L reads for L levels and forgetting the final operand read (4), or forgetting the fetch.

---

### Q8 — MCQ — Level 2
On a machine with 32-bit addresses, the base register holds 0x00002000 and the 16-bit displacement field of a load holds 0xFFE0 (a **signed** two's-complement displacement). What is the effective address?

A. 0x00001FE0  
B. 0x00002020  
C. 0x0000FFE0  
D. 0x0001FFE0

**Answer:** A

**Solution:** 0xFFE0 = 65504 ≥ 32768 ⇒ negative: 65504 − 65536 = −32. EA = 0x2000 − 32 = 0x1FE0. B adds +32 (wrong sign), D zero-extends the field (0x2000 + 0xFFE0 = 0x1FFE0), C is the raw field.

**Concept tested:** Sign extension of displacement (NOTES §3.6, §4.8).

**Difficulty:** Medium.

**Common trap:** Zero-extending a signed displacement.

---

## Level 3 — Multi-step

### Q9 — NAT — Level 3
An integer array is declared `A[5..60]` (lower bound 5), elements are 4 bytes, and `A` starts at byte address 7000. What is the byte address of `A[23]`? (decimal)

**Answer:** 7072

**Solution:** Element number from the start = 23 − 5 = 18. Address = 7000 + 18 × 4 = 7000 + 72 = 7072.

**Concept tested:** 1-D array address with lower bound; base + scaled index (NOTES §11.1).

**Difficulty:** Medium.

**Common trap:** Using 23 × 4 (7092).

---

### Q10 — NAT — Level 3
A row-major array `float F[0..14][0..39]` has 4-byte elements and base address 12000 (byte-addressable). What is the byte address of `F[6][9]`? (decimal)

**Answer:** 12996

**Solution:** Elements before it = 6 × 40 + 9 = 249. Bytes = 249 × 4 = 996. Address = 12000 + 996 = 12996.

**Concept tested:** Row-major 2-D address (NOTES §11.2).

**Difficulty:** Medium.

**Common trap:** Using 15 (rows) instead of 40 (columns) as the row length.

---

### Q11 — NAT — Level 3
An array of 20-byte records starts at byte address 4000. A field `w` is at offset 12 in each record. A compiler computes the address of `rec[7].w` using base + index with scale 1 and a displacement. What is the effective address (decimal)?

**Answer:** 4152

**Solution:** Index register = 7 × 20 = 140 (20 is not a legal scale, so the multiplication is done first). EA = 4000 + 140 + 12 = 4152.

**Concept tested:** Record array addressing with displacement (NOTES §11.3).

**Difficulty:** Medium.

**Common trap:** Using scale 4 or 8 for a 20-byte record.

---

### Q12 — NAT — Level 3
A 40-bit instruction contains a separate 4-bit addressing-mode field, three register-operand fields (the machine has 64 registers), an 11-bit literal field, and an opcode field; there are no other fields. What is the maximum number of different opcodes that can be used with each addressing mode?

**Answer:** 128

**Solution:** Register fields = 3 × log₂ 64 = 18 bits. Opcode bits = 40 − 4 − 18 − 11 = 7. Because the mode field is separate, every mode can combine with all 2⁷ = 128 opcode patterns.

**Concept tested:** Field-budget (NOTES §9.1).

**Difficulty:** Medium.

**Common trap:** Dividing 128 by the number of modes; or using 2 register fields.

---

### Q13 — NAT — Level 3
Instructions are 2 bytes long and aligned. A PC-relative branch has a 16-bit signed offset counted in instructions. The PC already points to the next instruction. What is the largest forward distance, in bytes, from the updated PC to a reachable target?

**Answer:** 65534

**Solution:** Largest offset = 2¹⁵ − 1 = 32767 instructions. Bytes = 32767 × 2 = 65534.

**Concept tested:** Branch reach (NOTES §7.3).

**Difficulty:** Medium.

**Common trap:** Using 2¹⁶ − 1, or forgetting the factor 2.

---

### Q14 — NAT — Level 3
Use this timing model: every memory access takes 3 clock cycles; instruction decode takes 1 cycle; one address addition takes 1 cycle; writing the destination register takes 1 cycle; nothing else costs time. The instruction `LOAD R1, @20(R2)` adds 20 to `R2`, reads the pointer stored at that address, and then reads the operand at the address held in that pointer. How many clock cycles does it take?

**Answer:** 12

**Solution:** Fetch 3 + decode 1 + address addition 1 + pointer read 3 + operand read 3 + register write 1 = 12.

**Concept tested:** Cycle counting per mode in a stated model (NOTES §10.3).

**Difficulty:** Medium.

**Common trap:** Omitting the instruction fetch or one memory read.

---

### Q15 — MCQ — Level 3
A word-addressable machine has R3 = 12 and an instruction address field k = 20. Memory: M[20] = 60, M[32] = 90, M[72] = 41. Instruction X uses **pre-indexed indirect** addressing (EA = M[k + R3]); instruction Y uses **post-indexed indirect** addressing (EA = M[k] + R3). What are the effective addresses (EA of X, EA of Y)?

A. (90, 72)  
B. (72, 90)  
C. (60, 32)  
D. (32, 72)

**Answer:** A

**Solution:** X: k + R3 = 32; EA = M[32] = 90. Y: M[20] = 60; EA = 60 + 12 = 72. B swaps the orders, C forgets the indirection/index, D forgets to dereference for X.

**Concept tested:** Indirect with index (NOTES §4.12).

**Difficulty:** Medium–hard.

**Common trap:** Mixing the order of "add index" and "read pointer".

---

## Level 4 — Tricky / trap-based

### Q16 — MCQ — Level 4
An instruction has a single 8-bit field that jointly encodes the operation and the addressing mode. Four addressing modes are supported and every operation must be available in all four modes. How many distinct operations can the instruction set have?

A. 256  
B. 128  
C. 64  
D. 4

**Answer:** C

**Solution:** 2⁸ = 256 distinct patterns; each operation consumes 4 patterns (one per mode). 256 / 4 = 64.

**Concept tested:** Merged opcode+mode field (NOTES §9.1).

**Difficulty:** Medium.

**Common trap:** Treating the field as opcode only (256).

---

### Q17 — MSQ — Level 4 (one or more options correct; no partial marking)
Byte-addressable machine; stack grows toward lower addresses; items are 4 bytes; SP = 4096 initially. `PUSH` is `-(SP)` store; `POP` is load from `(SP)+`. The sequence executed is PUSH P, PUSH Q, POP R, POP S. Select all correct statements.

A. P is stored at address 4092.  
B. Q is stored at address 4088.  
C. R receives the value of P.  
D. SP is 4096 after the four instructions.

**Answer:** A, B, D

**Solution:** PUSH P: SP = 4092, P stored at 4092. PUSH Q: SP = 4088, Q at 4088. POP R: load from 4088 (Q's value), SP = 4092. POP S: load from 4092 (P's value), SP = 4096. So C is false (R gets Q).

**Concept tested:** Pre-decrement / post-increment stack discipline (NOTES §4.7, §12.6).

**Difficulty:** Medium.

**Common trap:** Assuming first-pushed = first-popped.

---

### Q18 — NAT — Level 4
Instructions are 2 bytes long. A branch is at byte address 0x3A40. It uses PC-relative addressing with an 8-bit signed offset field 0xE9 counted in **instructions**; the PC is already incremented. Give the target as a decimal byte address.

**Answer:** 14868

**Solution:** 0xE9 = 233 ≥ 128 ⇒ 233 − 256 = −23 instructions = −46 bytes. PC_updated = 0x3A42 = 14914. Target = 14914 − 46 = 14868 (= 0x3A14).

**Concept tested:** Sign extension + scaling + updated PC (NOTES §7.2).

**Difficulty:** Medium–hard.

**Common trap:** Forgetting the scale (14914 − 23) or using 0x3A40 as the base.

---

### Q19 — NAT — Level 4
An assembler calculates the byte offset for a branch at address 1000 (4-byte instruction) to a target at address 1060, assuming that the offset is added to the **address of the branch instruction itself** (so it encodes 60). The hardware, however, adds the byte offset to the **updated PC**. At what address does the branch actually land?

**Answer:** 1064

**Solution:** Updated PC = 1000 + 4 = 1004. Landing = 1004 + 60 = 1064 (4 bytes past the intended target).

**Concept tested:** Which PC value is used (NOTES §7.1).

**Difficulty:** Medium.

**Common trap:** Assuming the answer is 1060.

---

### Q20 — MSQ — Level 4 (one or more options correct; no partial marking)
A machine defines the mode `@(R)+` as: EA = M[R]; then R is increased by the size of a **pointer word** (2 bytes). R = 500, M[500] = 2000 (a 2-byte pointer), M[2000] = 77 (a 4-byte operand). Select all correct statements about one execution of `LOAD R1, @(R)+`.

A. The effective address is 2000.  
B. The operand loaded is 77.  
C. R becomes 504.  
D. R becomes 502.

**Answer:** A, B, D

**Solution:** EA = M[500] = 2000; operand = M[2000] = 77. The step is the pointer size (2), not the operand size (4): R = 502, so C is false.

**Concept tested:** Autoincrement-deferred step size (NOTES §4.12).

**Difficulty:** Hard.

**Common trap:** Stepping by the operand size.

---

### Q21 — MCQ — Level 4
Three loads on a hypothetical machine compute EA as follows: I1: EA = R4 + R6; I2: EA = R4 + 28; I3: EA = R4 + R6 × 4. Which option names the modes of I1, I2, I3 in order?

A. base + index; displacement (base + offset); scaled index  
B. displacement; base + index; scaled index  
C. scaled index; displacement; base + index  
D. base + index; scaled index; displacement

**Answer:** A

**Solution:** I1 has two registers added ⇒ base + index. I2 has one register plus a constant ⇒ displacement. I3 has a register multiplied by a scale ⇒ scaled index.

**Concept tested:** Classifying by formula (NOTES §4.9).

**Difficulty:** Medium.

**Common trap:** Naming from the book's word rather than the formula.

---

## Level 5 — Challenge

### Q22 — NAT — Level 5
A byte-addressable machine executes a 4-byte instruction located at 3000 as follows. First operand: PC-relative with displacement −8 (bytes, added to the updated PC), giving the address of a 4-byte pointer word. The word at that address is 6000. Second step: the operand address is formed as pointer + X × 8 + 12, where X (index register) = 7 and the scale is 8. Give the final operand address (decimal).

**Answer:** 6068

**Solution:** Updated PC = 3000 + 4 = 3004. Pointer word address = 3004 − 8 = 2996, which contains 6000. Operand address = 6000 + 7 × 8 + 12 = 6000 + 56 + 12 = 6068.

**Concept tested:** Chained PC-relative → pointer → scaled index + displacement (NOTES §7, §4.11).

**Difficulty:** Hard.

**Common trap:** Using 3000 as the PC base (pointer at 2992).

---

### Q23 — NAT — Level 5
A linked list has 6 nodes. Node layout: value at offset 0, next pointer at offset 4; the last node's next is 0. R1 initially points to the first node. All instructions are one word. The loop is

```
L:    BEQ  R1, R0, DONE     ; R0 = 0 ; branch taken when R1 = 0
      LW   R2, 0(R1)
      ADD  R3, R3, R2
      LW   R1, 4(R1)
      J    L
DONE:
```
How many memory accesses (instruction fetches plus data reads) occur from the first execution of `L` until the `BEQ` branches to `DONE` (the instruction at `DONE` is not counted)?

**Answer:** 43

**Solution:** Per node: 5 instruction fetches + 2 data reads (the two `LW`) = 7. Six nodes: 42. The final `BEQ` with R1 = 0 adds 1 fetch. Total 43.

**Concept tested:** Access counting with displacement/register-indirect loads (NOTES §10, §11.4).

**Difficulty:** Hard.

**Common trap:** Omitting the final loop test, or forgetting the instruction fetches.

---

### Q24 — NAT — Level 5
A code+data block is moved as a whole by +0x1000 in memory by the loader (no patching). It contains five instructions: (i) `BNE loop` using PC-relative addressing to a label inside the block; (ii) `LOAD R1, 0x2340` using direct addressing to a variable inside the block; (iii) `ADD R2, R2, #25`; (iv) `JMP 0x2380` with an absolute target inside the block; (v) `LOAD R3, 12(R4)`, where R4 was set earlier by a PC-relative address computation to point to a data structure inside the block. How many of the five still behave correctly without patching?

**Answer:** 3

**Solution:** (i) correct: target − PC is unchanged. (iii) correct: the immediate is not an address. (v) correct: R4 is computed from the PC at run time, so it moves with the block. (ii) and (iv) contain absolute addresses that now refer to the old locations. Count = 3.

**Concept tested:** Relocation, position independence (NOTES §7.6).

**Difficulty:** Hard.

**Common trap:** Treating direct addresses within the same block as safe, or distrusting (v).
