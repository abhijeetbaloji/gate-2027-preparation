# Addressing Modes — Practice Questions

Original practice for GATE CS. These questions are not from any GATE paper. Attempt the questions before reading the solutions.

## Level 1 — Conceptual

## Q1 — MCQ

In immediate addressing, the operand value is

A. the contents of a named register  
B. encoded in the instruction itself  
C. stored in the memory word whose address is in a register  
D. produced by adding the program counter to a register

---

## Q2 — MCQ

In register-indirect addressing, the effective address is

A. the register number written in the instruction  
B. the contents of the named register  
C. the program counter plus a displacement  
D. the immediate field, interpreted as a signed constant

---

## Q3 — NAT

A word-addressable machine fetches a one-word branch at address 200. After the fetch, the PC contains 201. The branch uses PC-relative addressing with displacement \(-20\), and the displacement is added to the updated PC. What is the effective target address?

---

## Level 2 — Standard GATE Style

## Q4 — MCQ

The high-level reference `a[i]` has the base address of `a` in one register and the index `i` in another. Which addressing mode produces the element address directly?

A. Immediate  
B. Register  
C. Base plus index  
D. Memory indirect

---

## Q5 — NAT

Register `R2` contains 1000. The instruction `LOAD R1, (R2)+` uses post-increment register-indirect addressing and then adds the 4-byte operand size to `R2`. What is `R2` after the instruction?

---

## Q6 — MSQ

Select all that apply.

A. Immediate addressing does not need an extra memory access to obtain the operand value.  
B. Memory-indirect addressing reads a pointer from memory before it reads the operand.  
C. Reading a register is normally faster than a memory-indirect operand fetch.  
D. PC-relative branches can be position independent.

---

## Q7 — MCQ

Base register `R7` contains 5000 and the displacement is \(+24\). The effective address is

A. 24  
B. 5000  
C. 4976  
D. 5024

---

## Level 3 — Multi-Step

## Q8 — NAT

A load uses two levels of memory indirection. The instruction names address 40. Memory contains \(M[40] = 75\), \(M[75] = 12\), and \(M[12] = 99\). The effective address is \(M[M[40]]\), and the operand is the word at that address. What value is loaded?

---

## Q9 — MCQ

An accumulator machine executes `ADD` with one memory-indirect operand. Include the instruction fetch and every memory read required to obtain the operand. The accumulator itself is not in memory. How many memory accesses occur?

A. 1  
B. 2  
C. 3  
D. 4

---

## Q10 — NAT

An array of 8-byte records begins at byte address 2000. The index register contains 5 and the scale factor is 8. The displacement is 0. What is the byte address of element 5?

---

## Level 4 — Tricky / Trap-Based

## Q11 — NAT

A 4-byte branch is stored at byte address \(0\text{x1F0}\). After it is fetched, the PC is \(0\text{x1F4}\). The signed 8-bit displacement is \(0\text{xF6}\), and the target is the updated PC plus that displacement. Give the target as a decimal byte address.

---

## Q12 — MSQ

`R3` starts at 80. The operand size is 2 bytes. The two instructions execute in order:

```
LOAD R1, (R3)+
LOAD R2, -(R3)
```

The first is post-increment. The second is pre-decrement. Select all that apply.

A. The effective address of the first load is 80.  
B. After the first load, `R3` contains 82.  
C. The effective address of the second load is 80.  
D. After the second load, `R3` contains 78.

---

## Level 5 — Challenge

## Q13 — NAT

A byte-addressable machine executes one instruction as follows.

- The instruction is at address 1000 and is 4 bytes long, so the updated PC is 1004.
- A PC-relative displacement of \(+20\) selects a pointer word. The 32-bit word at that address contains the integer 2000.
- That integer is a base address. Index register `X` contains 3 and the scale is 4.

The operand address is \(\text{base} + X \times 4\). What is that address?

---

## Q14 — MCQ

A load-store program evaluates `b[i] = *p + 5`. The pointer `p` is already in `Rp`, the base of array `b` is in `Rb`, and `i` is in `Ri`. The instruction sequence is

```
LOAD  R1, (Rp)          ; register indirect
ADDI  R1, R1, #5        ; immediate add
STORE R1, (Rb, Ri, 4)   ; base + scaled index
```

Each instruction occupies one memory word. The immediate is inside its instruction. The indexed store computes its address in the ALU and does not read an extra pointer from memory. How many memory accesses does the sequence perform, counting instruction fetches and data accesses?

A. 3  
B. 4  
C. 5  
D. 6

## Answer Key

| Q | Type | Answer |
|---|------|--------|
| 1 | MCQ | B |
| 2 | MCQ | B |
| 3 | NAT | 181 |
| 4 | MCQ | C |
| 5 | NAT | 1004 |
| 6 | MSQ | A, B, C, D |
| 7 | MCQ | D |
| 8 | NAT | 99 |
| 9 | MCQ | C |
| 10 | NAT | 2040 |
| 11 | NAT | 490 |
| 12 | MSQ | A, B, C |
| 13 | NAT | 2012 |
| 14 | MCQ | C |

## Detailed Solutions

### Q1

Answer: B

Immediate addressing carries the operand in the instruction word. No register or memory location is read to obtain that value.

### Q2

Answer: B

Register-indirect mode uses the register contents as the address. The register number only selects which register holds that address.

### Q3

Answer: 181

The displacement is applied to the PC after the one-word instruction has been fetched.

\[
201 + (-20) = 181
\]

### Q4

Answer: C

An array element address is a base plus an index. Immediate mode supplies a constant, register mode supplies a value already in a register, and memory indirect follows a pointer in memory.

### Q5

Answer: 1004

Post-increment uses the old register value as the address and then adds the operand size.

\[
1000 + 4 = 1004
\]

### Q6

Answer: A, B, C, D

The immediate value travels with the instruction, so A is true and E is false. Memory indirect needs a pointer read and then an operand read. A register read avoids that memory traffic. A PC-relative displacement stays valid if the code and its target move together.

### Q7

Answer: D

\[
5000 + 24 = 5024
\]

### Q8

Answer: 99

The first memory word is a pointer to a pointer.

\[
M[M[40]] = M[75] = 12
\]

The operand is \(M[12] = 99\).

### Q9

Answer: C

The accesses are:

1. fetch the instruction,
2. read the pointer from the address named in the instruction,
3. read the operand from the address found in that pointer.

A direct operand would stop after two accesses. Indirection adds the pointer fetch, for a total of 3.

### Q10

Answer: 2040

Element 5 starts \(5 \times 8\) bytes after the base.

\[
2000 + 5 \times 8 = 2040
\]

### Q11

Answer: 490

\(0\text{x1F4} = 500\). The bit pattern \(0\text{xF6} = 246\) is negative in 8-bit two’s complement:

\[
246 - 256 = -10
\]

\[
500 + (-10) = 490
\]

The same target in hexadecimal is \(0\text{x1EA}\).

### Q12

Answer: A, B, C

The first load uses 80 and then increments `R3` by 2, leaving 82. The second load decrements `R3` by 2 before the access, so both the register and the effective address become 80. Statement D would be true only if the pre-decrement happened from 82 without returning to the original address, but \(82 - 2 = 80\), not 78.

### Q13

Answer: 2012

The pointer address is the updated PC plus the displacement.

\[
1004 + 20 = 1024
\]

The word at 1024 contains the base 2000. The scaled index adds

\[
3 \times 4 = 12
\]

\[
2000 + 12 = 2012
\]

### Q14

Answer: C

The three instruction fetches contribute 3 accesses. `LOAD` reads one data word through `Rp`. `ADDI` uses an immediate and accesses no data memory. `STORE` writes one data word. The total is \(3 + 1 + 1 = 5\).
