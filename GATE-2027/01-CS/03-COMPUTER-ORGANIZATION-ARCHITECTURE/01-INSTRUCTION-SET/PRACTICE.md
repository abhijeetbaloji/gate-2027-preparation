# Instruction Set — Practice (original questions)

All questions are original (new numbers and scenarios). Answers sit directly under each question; attempt before reading. Every answer was recomputed
by `/tmp/coa-verify-01-instruction-set.py`. Conventions: 1 K = 2¹⁰; bits vs bytes are stated per question. Method: [`NOTES.md`](NOTES.md).
MSQ = one or more options correct, no partial marking. Where an encoding is described, *all bit patterns are legal and decoding is by prefix* unless stated.

---

## Level 1 — Conceptual

### Q1 — MCQ (Level 1)

Which one of the following is part of the Instruction Set Architecture of a processor?

A. The associativity of the L1 data cache
B. The number of general-purpose registers that instructions can name
C. The number of stages in the instruction pipeline
D. Whether the control unit is hardwired or microprogrammed

**Answer:** B

**Solution:** The ISA is the programmer-visible contract (NOTES §1.3). The registers instructions can name are encoded in the instruction fields, so a binary depends on them. Cache associativity, pipeline depth and the style of the control unit are implementation choices: the same binary runs unchanged on chips that differ in all three.

**Concept tested:** ISA vs microarchitecture.
**Difficulty:** Easy
**Common trap:** Treating "number of registers" as hidden; only *physical* renamed registers are hidden, architectural ones are ISA.

---

### Q2 — MSQ (Level 1)

Two chips X and Y are binary-compatible implementations of the same ISA (any program binary runs on both). Which of the following may differ between X and Y?

A. The clock frequency
B. The size of the L2 cache
C. The binary opcode assigned to the ADD instruction
D. The number of pipeline stages

**Answer:** A, B, D

**Solution:** Binary compatibility means identical instruction encodings and architectural behaviour. Frequency, cache size and pipeline depth only affect speed. If the ADD opcode differed, a binary containing ADD would not run correctly on both, so C cannot differ.

**Concept tested:** What is fixed by the ISA.
**Difficulty:** Easy
**Common trap:** Thinking a "faster" chip needs a different ISA.

---

### Q3 — MCQ (Level 1)

A byte-addressable machine stores the 64-bit value 0x0102030405060708 starting at address 1000 using big-endian byte order. The byte stored at address 1005 is

A. 0x03
B. 0x04
C. 0x06
D. 0x08

**Answer:** C

**Solution:** Big-endian puts the most significant byte at the lowest address:

```
address  1000 1001 1002 1003 1004 1005 1006 1007
byte      01   02   03   04   05   06   07   08
```
Address 1005 holds 0x06. (0x03 is what a little-endian layout would store there; 0x08 is at 1007; 0x04 at 1003.)

**Concept tested:** Endianness (NOTES §9).
**Difficulty:** Easy
**Common trap:** Mixing up big- and little-endian; counting from 1 instead of 0.

---

### Q4 — NAT (Level 1)

A one-address accumulator machine runs `LOAD B; MUL C; ADD A; STORE Y` to compute Y = A + B × C. Each instruction occupies one word (one memory read to fetch it) and each memory operand named by an instruction causes exactly one data-memory access. The total number of memory accesses (instruction fetches plus data accesses) is ______.

**Answer:** 8

**Solution:** Fetches: 4 instructions × 1 = 4. Data accesses: LOAD B (1), MUL C (1), ADD A (1), STORE Y (1) = 4. Total = 4 + 4 = **8**. (Execution check: B·C + A computed correctly in the accumulator, then stored.)

**Concept tested:** Instruction fetch vs data references (NOTES §2.2, §4.3).
**Difficulty:** Easy
**Common trap:** Forgetting that fetches are memory accesses too.

---

## Level 2 — Standard GATE

### Q5 — NAT (Level 2)

A processor has 70 instruction types and 40 general-purpose registers. Every instruction is 36 bits long with the format `opcode | Rd | Rs1 | Rs2 | immediate`, where every register field has the same width and the opcode is a single fixed field. The maximum number of bits available for the immediate is ______.

**Answer:** 11

**Solution:** Opcode ⌈log₂ 70⌉ = 7 (64 < 70 ≤ 128). Register field ⌈log₂ 40⌉ = 6 (32 < 40 ≤ 64); three fields = 18 bits. Immediate = 36 − 7 − 18 = **11**.

**Concept tested:** Fixed-field sizing (NOTES §6.1).
**Difficulty:** Easy–Medium
**Common trap:** Using 5 bits for 40 registers (2⁵ = 32 < 40).

---

### Q6 — NAT (Level 2)

An instruction contains an opcode chosen from 9 instruction types, three register identifiers (from 20 registers) and a 14-bit immediate. Each instruction must start on a byte boundary in memory. A program has 250 instructions. The size of the program text, in bytes, is ______.

**Answer:** 1250

**Solution:** Opcode ⌈log₂ 9⌉ = 4; each register ⌈log₂ 20⌉ = 5 → 15; immediate 14. Bits per instruction = 4 + 15 + 14 = 33 → ⌈33/8⌉ = 5 bytes. Program = 250 × 5 = **1250 bytes**.

**Concept tested:** Byte-aligned program size (NOTES §6.2).
**Difficulty:** Medium
**Common trap:** ⌈250 × 33 / 8⌉ = 1032 — rounding on the whole program instead of per instruction.

---

### Q7 — MCQ (Level 2)

A zero-address stack machine has `PUSH v`, `POP v` and the binary instructions `ADD`, `SUB`, `MUL`, `DIV` (they pop two values and push one result). No `DUP` or `SWAP` exists. The minimum number of instructions that computes V = (A − B) × (C + D) / (E − F) and stores it in memory variable V is

A. 11
B. 12
C. 13
D. 17

**Answer:** B

**Solution:** Leaves = 6 (A, B, C, D, E, F) → 6 PUSH; operators = 5 (−, +, ×, −, /) → 5 binary instructions; 1 POP V. Total = 6 + 5 + 1 = **12**. Postfix: `A B − C D + × E F − /` then `POP V`. A (11) forgets the POP.

**Concept tested:** Stack-machine counting (NOTES §4.2).
**Difficulty:** Easy–Medium
**Common trap:** Omitting the final POP; counting variables fewer times than they appear.

---

### Q8 — NAT (Level 2)

An 18-bit instruction has a 6-bit opcode and two 6-bit address fields in the two-address format. 40 of the 64 possible 6-bit opcodes are used for two-address instructions. All remaining 6-bit opcodes are used as prefixes for one-address instructions of format `prefix(6) | extension(6) | address(6)`. The maximum number of one-address instructions that can be encoded is ______.

**Answer:** 1536

**Solution:** Free prefixes = 64 − 40 = 24. Each prefix plus a 6-bit extension gives 2⁶ = 64 opcodes. Total = 24 × 64 = **1536**. Cake check: one-address opcode length 12 → 2¹² − 40 × 2⁶ = 4096 − 2560 = 1536.

**Concept tested:** One expansion level of the opcode (NOTES §6.4.3, §6.4.10).
**Difficulty:** Medium
**Common trap:** Multiplying the free prefixes by 6 or by 12 instead of 2⁶.

---

### Q9 — MCQ (Level 2)

A processor is a load–store machine. In every instruction the **first operand is the destination**; ALU instructions take three register operands; `LOAD Rd, M` reads memory variable M; `STORE M, Rs` writes memory variable M. Which sequence correctly computes the statement A = B × C + D (A, B, C, D are memory variables; R1…R5 are registers)?

A. `LOAD R1, B ; LOAD R2, C ; MUL R3, R1, R2 ; ADD A, R3, D`
B. `LOAD R1, B ; MUL R1, R1, C ; ADD R1, R1, D ; STORE A, R1`
C. `LOAD R1, B ; LOAD R2, C ; MUL R3, R1, R2 ; LOAD R4, D ; ADD R5, R3, R4 ; STORE A, R5`
D. `LOAD R1, B ; LOAD R2, C ; MUL R3, R1, R2 ; LOAD R4, D ; ADD R5, R3, R4 ; STORE R5, A`

**Answer:** C

**Solution:** Apply the four-question test (NOTES §4.4). A: the final ADD names memory operands A and D — not allowed. B: MUL and ADD use memory operands C and D. D: all arithmetic is fine, but STORE has the register first; with destination-first the memory variable must come first, so the operands are reversed. C loads B, C, D into registers, multiplies, adds, and stores with the destination first. Simulation with B = 3, C = 4, D = 5 gives A = 17.

**Concept tested:** Load–store restriction and operand-order convention.
**Difficulty:** Medium
**Common trap:** Accepting a sequence that looks short but puts a memory operand inside an ALU instruction.

---

### Q10 — NAT (Level 2)

A processor runs at 2.5 GHz and has an average CPI of 1.25. Its native MIPS rating is ______.

**Answer:** 2000

**Solution:** MIPS = f / (CPI × 10⁶) = 2.5×10⁹ / (1.25 × 10⁶) = **2000**.

**Concept tested:** MIPS formula (NOTES §8.2).
**Difficulty:** Easy
**Common trap:** Dividing by 10⁹ instead of 10⁶; multiplying f by CPI.

---

## Level 3 — Multi-step

### Q11 — NAT (Level 3)

A 16-bit instruction set uses 4-bit address fields. The formats are: three-address `opcode(4) | a | a | a`; two-address `opcode(8) | a | a`; one-address `opcode(12) | a`; zero-address `opcode(16)`. Each level re-uses the freed address field as opcode extension of **all** unused prefixes of the level above. 12 three-address, 40 two-address and 300 one-address instructions are defined. The maximum number of zero-address instructions is ______.

**Answer:** 1344

**Solution:** Level slots: three-address 2⁴ = 16 prefixes; unused = 16 − 12 = 4 → two-address slots = 4 × 16 = 64. Used 40 → 24 free → one-address slots = 24 × 16 = 384. Used 300 → 84 free → zero-address slots = 84 × 16 = **1344**. Cake check: 2¹⁶ − 12·2¹² − 40·2⁸ − 300·2⁴ = 65536 − 49152 − 10240 − 4800 = 1344.

**Concept tested:** Multi-level expanding opcodes (NOTES §6.4.10).
**Difficulty:** Medium
**Common trap:** Applying the multiplication by 16 only once; subtracting counts at the wrong level.

---

### Q12 — NAT (Level 3)

A processor has 32 registers and 24-bit instructions of three types:
X: three register operands; Y: two register operands and a 6-bit immediate; Z: one register operand and a 12-bit offset.
Variable-length opcodes are permitted; every bit not used by an operand field is part of the opcode. 100 X-type opcodes and 20 Y-type opcodes are already assigned. The maximum number of Z-type opcodes is ______.

**Answer:** 93

**Solution:** Register field = 5 bits. Operand bits: X = 15, Y = 10 + 6 = 16, Z = 5 + 12 = 17. Opcode lengths: o_X = 9, o_Y = 8, o_Z = 7. N_Z = 2⁷ − 100·2⁷⁻⁹ − 20·2⁷⁻⁸ = 128 − 25 − 10 = **93**.

**Concept tested:** Cake rule with three opcode lengths (NOTES §6.4.3, 6.4.7).
**Difficulty:** Medium
**Common trap:** Subtracting 100 + 20 = 120 directly.

---

### Q13 — NAT (Level 3)

A processor has 40 architectural registers and 32-bit instructions. Its ISA has 180 distinct instructions, equally divided between R-type (`opcode | UNUSED | Rd | Rs1 | Rs2`) and I-type (`opcode | Rd | Rs | immediate`). One bit of the opcode distinguishes R-type from I-type and the remaining opcode bits encode the operation. All register fields have equal size. Let X = number of UNUSED bits, Y = number of opcode bits, Z = number of immediate bits. The value of Z − X + Y is ______.

**Answer:** 14

**Solution:** 180/2 = 90 operations per type → ⌈log₂ 90⌉ = 7; plus format bit → Y = 8. Registers: ⌈log₂ 40⌉ = 6. X = 32 − 8 − 3·6 = 6. Z = 32 − 8 − 2·6 = 12. Z − X + Y = 12 − 6 + 8 = **14**.

**Concept tested:** Format bit with equal split (NOTES §6.3).
**Difficulty:** Medium
**Common trap:** Computing opcode as ⌈log₂ 180⌉ = 8 and then adding another format bit (9) — the format bit is already inside the 8.

---

### Q14 — NAT (Level 3)

The following straight-line segment is compiled for a processor whose instructions have at most two source operands and one destination, all in registers; a destination register may be the same as a source register that is not used again. `a`, `b`, `c` are in registers at entry. After the segment only `t6` is used; every other variable is dead.

```
t1 = a + b
t2 = t1 * c
t3 = t1 - a
t4 = t2 + t3
t5 = t4 * c
t6 = t5 + t1
```
The minimum number of registers that suffices without any spill (no reordering allowed) is ______.

**Answer:** 4

**Solution:** Live sets after each statement: after 1: {a, c, t1}; after 2: {a, c, t1, t2}; after 3 (a dies here): {c, t1, t2, t3}; after 4: {c, t1, t4}; after 5: {t1, t5}; after 6: {t6}. The largest live-out set has 4 members and the interference graph needs 4 colours. At the entry {a,b,c} is 3, at statement 1 b dies so t1 can reuse its register. Answer **4**.

**Concept tested:** Liveness and register pressure (NOTES §7).
**Difficulty:** Medium
**Common trap:** Counting all nine variables, or forgetting that `a` is still needed by statement 3.

---

### Q15 — MCQ (Level 3)

A one-address accumulator machine has only `LOAD m`, `STORE m`, `ADD m`, `SUB m`, `MUL m` (ACC ← ACC op m for ADD/SUB/MUL). Inputs must not be overwritten; temporaries may be stored in memory. The minimum number of instructions to compute Y = (A + B) × (C + D) − E and store it in Y is

A. 6
B. 7
C. 8
D. 9

**Answer:** C

**Solution:** Using the recursion of NOTES §4.2: cost(A+B) = 2, cost(C+D) = 2; the product has two complex operands → 2 + 2 + 2 = 6; `− E` (leaf) → 7; final STORE → 8.
```
LOAD C ; ADD D ; STORE T ; LOAD A ; ADD B ; MUL T ; SUB E ; STORE Y
```
Fewer is impossible: four leaves need four memory-operand instructions, E needs one, the second sum must be parked (STORE T) and used (MUL T), and Y must be stored — 8.

**Concept tested:** Accumulator machine with a temporary.
**Difficulty:** Medium
**Common trap:** Giving 7 (omitting the final STORE) or 6.

---

### Q16 — NAT (Level 3)

Processor P1 and P2 implement the same ISA and run the same program. P2 takes 40 % less time than P1 but has a 25 % higher CPI. P1 runs at 2 GHz. The clock frequency of P2, in GHz, rounded to two decimal places, is ______.

**Answer:** 4.17

**Solution:** IC is the same. T₂/T₁ = 0.6, CPI₂/CPI₁ = 1.25. T = IC·CPI/f ⇒ f₂ = f₁ × (CPI₂/CPI₁) / (T₂/T₁) = 2 × 1.25 / 0.6 = 4.1667 ≈ **4.17 GHz**.

**Concept tested:** Ratio method (NOTES §8.4).
**Difficulty:** Medium
**Common trap:** Using 0.4 instead of 0.6 for the time ratio; or 0.25 for the CPI ratio.

---

## Level 4 — Tricky / trap-based

### Q17 — NAT (Level 4)

A processor has 16 registers and 20-bit instructions. Types: T1 has three register operands; T2 has one register operand and an 8-bit immediate; T3 has one register operand and a 10-bit offset. Variable-length opcodes are permitted and every bit not used by an operand is opcode. 37 opcodes of T1 and 10 opcodes of T2 are assigned. The maximum number of opcodes for T3 is ______.

**Answer:** 52

**Solution:** Register field = 4 bits. Operand bits: T1 = 12, T2 = 12, T3 = 14. Opcode lengths: 8, 8, 6. Fraction rule: N = 2⁶ − 37/2² − 10/2² = 64 − 9.25 − 2.5 = 52.25 → floor → **52**. The two partial prefixes share a 6-bit prefix: 47 eight-bit opcodes fill ⌈47/4⌉ = 12 six-bit prefixes.

**Concept tested:** Target with the shortest opcode, fractions and floor (NOTES §6.4.8–9).
**Difficulty:** Hard
**Common trap:** Rounding each type separately: 64 − ⌈37/4⌉ − ⌈10/4⌉ = 51; or subtracting 47 directly (17).

---

### Q18 — NAT (Level 4)

A processor has 16 registers and 32-bit instructions. Its ISA has 120 operations: 100 are R-type and 20 are I-type (`opcode | Rd | Rs | immediate`). The first opcode bit distinguishes R-type from I-type; the remaining operation field has the same width for both types and is just large enough for the larger type. The maximum number of bits for the immediate in I-type is ______.

**Answer:** 16

**Solution:** Operation field = ⌈log₂ 100⌉ = 7, plus the format bit → opcode = 8 bits. Register fields: 4 bits each → 8. Immediate = 32 − 8 − 8 = **16**. (Using the flat ⌈log₂ 120⌉ = 7 would wrongly give 17.)

**Concept tested:** Format bit with unequal split (NOTES §6.3).
**Difficulty:** Medium–Hard
**Common trap:** Sizing the opcode for all 120 operations together.

---

### Q19 — MCQ (Level 4)

Machine A is rated 1000 MIPS and runs a program of 3 × 10⁹ instructions. Machine B is rated 400 MIPS and runs the same program compiled to 8 × 10⁸ instructions. Which statement is correct?

A. A is faster because its MIPS rating is higher.
B. B is faster, by a factor of 1.5.
C. They take the same time.
D. A is faster, by a factor of 2.5.

**Answer:** B

**Solution:** T = IC / (MIPS × 10⁶). T_A = 3×10⁹ / 10⁹ = 3 s; T_B = 8×10⁸ / (4×10⁸) = 2 s. B is faster, by 3/2 = 1.5.

**Concept tested:** MIPS is not a performance measure across ISAs (NOTES §8.2).
**Difficulty:** Medium
**Common trap:** Choosing the higher MIPS.

---

### Q20 — MSQ (Level 4)

Which of the following statements are correct?

A. Replacing a memory-to-memory ISA by a load–store ISA usually increases the number of instructions executed for the same program.
B. A processor with a lower CPI always executes a given program faster than one with a higher CPI.
C. A fixed-length instruction format wastes some bits in simple instructions compared with a variable-length format.
D. MIPS ratings are a valid way to rank processors with different instruction sets.

**Answer:** A, C

**Solution:** A: memory-operand instructions are replaced by LOAD/STORE plus register operations → more instructions. B is false because time = IC × CPI / f; a different IC or clock may reverse the order. C: a register increment in a fixed 32-bit format still occupies 32 bits, whereas a variable-length format can use fewer. D is false (Q19).

**Concept tested:** ISA trade-offs and the iron law (NOTES §5, §8).
**Difficulty:** Medium
**Common trap:** "Lower CPI means faster."

---

### Q21 — NAT (Level 4)

A word-addressable machine has 16-bit words. An instruction occupies one word plus one extra word for each memory address it names. All operands are in memory. The program is
`MOV T, X ; ADD T, Y ; MOV Z, T`, where `MOV d, s` copies s into d and `ADD d, s` computes d ← d + s. Each operand read and each result write is one data-memory access. The total number of memory accesses (fetching instruction words + data accesses) is ______.

**Answer:** 16

**Solution:**
- `MOV T, X`: 3 words fetched; data: read X, write T = 2 → 5.
- `ADD T, Y`: 3 words fetched; data: read T, read Y, write T = 3 → 6.
- `MOV Z, T`: 3 words fetched; data: read T, write Z = 2 → 5.
Total = 5 + 6 + 5 = **16**.

**Concept tested:** Multi-word instructions and memory references (NOTES §6.5, §4.3).
**Difficulty:** Medium
**Common trap:** Counting one fetch per instruction; forgetting that `ADD d, s` reads d.

---

### Q22 — NAT (Level 4)

A zero-address stack machine evaluates the postfix form of `((A + B) × (C + D)) × ((E + F) × (G + H))` using the straightforward left-to-right postfix order `A B + C D + × E F + G H + × ×`. Each PUSH adds one entry; each binary operation pops two and pushes one. The maximum stack depth reached is ______.

**Answer:** 4

**Solution:** Running depth: A(1) B(2) +(1) C(2) D(3) +(2) ×(1) E(2) F(3) +(2) G(3) H(4) +(3) ×(2) ×(1). Maximum = **4**.

**Concept tested:** Stack depth by scanning (NOTES §4, §7.5).
**Difficulty:** Medium
**Common trap:** Counting 8 (the number of operands) or stopping after the first subtree.

---

## Level 5 — Challenge

### Q23 — MSQ (Level 5)

A processor has 32 registers and 20-bit instructions. Format F: three register operands. Format G: two register operands and a 7-bit immediate. Variable-length opcodes are permitted (all bits not used by operands are opcode). Which statements are correct?

A. Format F has a 5-bit opcode.
B. Format G has a 4-bit opcode.
C. If 20 opcodes of format F are assigned, at most 3 opcodes of format G can still be assigned.
D. If 3 opcodes of format G are assigned, at most 20 opcodes of format F can still be assigned.

**Answer:** A, C, D

**Solution:** Register field = 5 bits. F: operand bits 15 → opcode 5 (A true). G: 10 + 7 = 17 → opcode 3 (B false). C: G opcode length 3; each F opcode takes 1/4 of a G slot: 8 − 20/4 = 3 (true). D: each G opcode (3 bits) uses 2⁵⁻³ = 4 five-bit slots: 32 − 3·4 = 20 (true).

**Concept tested:** Cake rule in both directions (NOTES §6.4).
**Difficulty:** Hard
**Common trap:** Thinking the shorter-opcode format must have fewer opcodes; forgetting that G consumes 4 F-slots each.

---

### Q24 — NAT (Level 5)

A processor has 8 registers and 16-bit instructions with four formats:
F1: three register operands; F2: two register operands and a 4-bit immediate; F3: one register operand and a 6-bit address; F4: no operand.
Variable-length opcodes are permitted. 40 F1, 5 F2 and 30 F3 opcodes are assigned. The maximum number of F4 opcodes is ______.

**Answer:** 24576

**Solution:** Register field = 3 bits. Operand bits: F1 = 9, F2 = 6 + 4 = 10, F3 = 3 + 6 = 9, F4 = 0. Opcode lengths: 7, 6, 7, 16. N = 2¹⁶ − 40·2⁹ − 5·2¹⁰ − 30·2⁹ = 65536 − 20480 − 5120 − 15360 = **24576**. (Cake check: 40/128 + 5/64 + 30/128 = 0.625 used; 0.375 × 65536 = 24576.)

**Concept tested:** Opcode space with four formats.
**Difficulty:** Hard
**Common trap:** Using the wrong power (2^(16−7) = 512 for F1, 2^(16−6) = 1024 for F2).

---

### Q25 — NAT (Level 5)

The following code runs on a processor with register-only 3-address instructions (a destination register may be a source register that is not used again). A constant assignment such as `a = 1` needs a register for the value. Only `g` is live after the segment. The only permitted optimisation is **code motion** (reordering statements without breaking dependences). The minimum number of registers needed to run the segment without any spill is ______.

```
a = 1
b = 2
c = 3
d = 4
e = a + b
f = c + d
g = e * f
```

**Answer:** 3

**Solution:** In the given order, after `d = 4` the values a, b, c, d are all live → 4 registers. Reorder: `a=1; b=2; e=a+b; c=3; d=4; f=c+d; g=e*f`: live sets {a}, {a,b}, {e}, {e,c}, {e,c,d}, {e,f}, {g} → peak 3. Two registers are not enough in any order: `f = c + d` needs c, d live together, and `e` (or a and b, if f is computed first) is live at the same time, giving 3. All dependency-respecting orders were enumerated by script: minimum 3.

**Concept tested:** Code motion lowering register pressure (NOTES §7.2–7.3).
**Difficulty:** Hard
**Common trap:** Answering 4 (original order) or 2.
