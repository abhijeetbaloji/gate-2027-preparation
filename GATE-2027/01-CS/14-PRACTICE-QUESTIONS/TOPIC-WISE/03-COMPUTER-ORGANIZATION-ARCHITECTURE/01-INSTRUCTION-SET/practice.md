# Instruction Set — Practice Questions

Original practice for GATE CS. These questions are not from any GATE paper. Attempt the questions before reading the solutions.

## Level 1 — Conceptual

## Q1 — MCQ

A load-store processor can read or write memory only with explicit load and store instructions. Arithmetic instructions use registers only. For the statement \(S = P - Q\), where \(P\), \(Q\), and \(S\) are distinct memory variables, how many data-memory accesses are required? Do not count instruction fetches.

A. 1  
B. 2  
C. 3  
D. 4

---

## Q2 — MCQ

How many explicit operand addresses does a one-address instruction contain?

A. 0  
B. 1  
C. 2  
D. 3

---

## Q3 — MCQ

A byte-addressable machine stores the 32-bit word \(0\text{xA1B2C3D4}\) at address 400 using little-endian byte order. Which byte is stored at address 401?

A. \(0\text{xA1}\)  
B. \(0\text{xB2}\)  
C. \(0\text{xC3}\)  
D. \(0\text{xD4}\)

---

## Q4 — NAT

A processor uses a fixed 20-bit instruction. The opcode occupies 7 bits and one register field occupies 5 bits. The rest of the instruction is an immediate constant. How many bits are available for that immediate?

---

## Level 2 — Standard GATE Style

## Q5 — MCQ

An instruction mix and its CPI are:

| Class | Fraction of instructions | CPI |
|---|---|---|
| ALU | 0.50 | 1 |
| Load | 0.20 | 5 |
| Store | 0.10 | 4 |
| Branch | 0.20 | 2 |

The average CPI is

A. 1.8  
B. 2.3  
C. 2.7  
D. 3.4

---

## Q6 — NAT

A zero-address stack machine evaluates \(W = (P + Q) \times (R - S)\). `PUSH` reads one memory variable and pushes it. `ADD`, `SUB`, and `MUL` pop two values and push one result. `POP` writes the top of the stack to memory. \(P, Q, R, S, W\) are distinct memory variables. What is the minimum number of instructions?

---

## Q7 — MSQ

Select all that apply to a typical RISC instruction set, as compared with a typical CISC instruction set of the same era.

A. ALU operations are usually register-to-register.  
B. Instructions are usually fixed length.  
C. A typical arithmetic instruction edits a string in memory.  
D. Memory is accessed by separate load and store instructions.

---

## Q8 — MCQ

A two-address machine evaluates \(W = (P + Q) \times (R - S)\). A binary instruction uses its first address as both a source and the destination. Inputs \(P, Q, R, S\) must not be overwritten. Temporaries and a final move into \(W\) are allowed. The minimum number of instructions is

A. 4  
B. 5  
C. 6  
D. 8

---

## Q9 — NAT

An instruction set has exactly 100 distinct operations, and the opcode is a fixed-length field. What is the minimum number of opcode bits?

---

## Level 3 — Multi-Step

## Q10 — NAT

A processor has 40 distinct instruction types and 128 general-purpose registers. Every instruction is 32 bits long, and the opcode is a fixed field large enough for all 40 types. The instruction `ADDI Rd, Rs, #imm` names two registers. What is the maximum number of bits that can be given to the immediate?

---

## Q11 — NAT

A CPU has 16-bit instructions and 6-bit address fields. A two-address encoding is `| opcode 4 | address 6 | address 6 |`. Nine of the 16 possible 4-bit opcodes are used for two-address instructions. Every remaining opcode is a prefix of a one-address instruction `| prefix 4 | opcode extension 6 | address 6 |`. How many distinct one-address opcodes does this encoding provide?

---

## Q12 — MSQ

Select all that apply.

A. On a stack machine, a binary arithmetic operation has no explicit operand address.  
B. A three-address instruction can name a destination that is different from both sources.  
C. A two-address instruction can name three distinct locations.  
D. On an accumulator machine, a binary arithmetic operation leaves one operand implicit.

---

## Q13 — NAT

A program executes \(6 \times 10^{8}\) instructions. The average CPI is 2.5 and the clock frequency is 3 GHz. The execution time, in milliseconds, is ______.

---

## Level 4 — Tricky / Trap-Based

## Q14 — NAT

A CPU has 24-bit instructions and 6-bit address fields. A three-address encoding is `| opcode 6 | address | address | address |`, so there are 64 possible three-address opcodes. Thirty-six of them are used for three-address instructions. Every remaining opcode is expanded into two-address instructions by using the spare 6-bit address field as an opcode extension. How many distinct two-address opcodes does this provide?

---

## Q15 — MCQ

A one-address accumulator machine evaluates \(Y = A \times B + C \times D - E\). The inputs must not be overwritten. One temporary memory location is allowed. `LOAD`, `STORE`, `MUL`, `ADD`, and `SUB` are the only instructions, and each names at most one memory operand. The minimum number of instructions is

A. 4  
B. 6  
C. 8  
D. 10

---

## Q16 — NAT

A fixed 32-bit instruction format has a 256-operation opcode, two equal register fields, and an immediate of at least 10 bits. The number of registers must be a power of two. What is the maximum number of registers?

---

## Level 5 — Challenge

## Q17 — NAT

The same program is compiled for two instruction sets.

| Machine | Instructions | CPI | Clock |
|---|---|---|---|
| R | \(5 \times 10^{8}\) | 1.2 | 2.4 GHz |
| C | \(2 \times 10^{8}\) | 3.6 | 1.6 GHz |

The speedup of R over C, that is \(T_C / T_R\), rounded to one decimal place, is ______.

---

## Q18 — MSQ

A 24-bit instruction names registers with 4-bit fields (16 registers). Select all that apply.

A. If an instruction contains only an opcode and three register fields, the opcode is 12 bits.  
B. If an instruction contains an opcode, two register fields, and an 8-bit immediate, the opcode is 8 bits.  
C. The encoding can simultaneously assign all \(2^{12}\) three-register opcodes and 256 distinct immediate opcodes with no format bit and no unused opcode values.  
D. If a 2-bit format field is reserved, a three-register instruction still has 10 opcode bits in the remaining 22 bits.

## Answer Key

| Q | Type | Answer |
|---|------|--------|
| 1 | MCQ | C |
| 2 | MCQ | B |
| 3 | MCQ | C |
| 4 | NAT | 8 |
| 5 | MCQ | B |
| 6 | NAT | 8 |
| 7 | MSQ | A, B, D |
| 8 | MCQ | C |
| 9 | NAT | 7 |
| 10 | NAT | 12 |
| 11 | NAT | 448 |
| 12 | MSQ | A, B, D |
| 13 | NAT | 500 |
| 14 | NAT | 1792 |
| 15 | MCQ | C |
| 16 | NAT | 128 |
| 17 | NAT | 1.8 |
| 18 | MSQ | A, B, D |

## Detailed Solutions

### Q1

Answer: C

A load-store evaluation needs `LOAD P`, `LOAD Q`, a register subtract, and `STORE S`. The memory operands produce two reads and one write. Instruction fetches are excluded, so the data-memory count is 3.

### Q2

Answer: B

A one-address instruction carries one explicit address. The other operand, typically the accumulator, is implied by the opcode.

### Q3

Answer: C

Little-endian order places the least significant byte at the lowest address. The bytes of \(0\text{xA1B2C3D4}\) are therefore

| Address | Byte |
|---|---|
| 400 | \(0\text{xD4}\) |
| 401 | \(0\text{xC3}\) |
| 402 | \(0\text{xB2}\) |
| 403 | \(0\text{xA1}\) |

Address 401 holds \(0\text{xC3}\).

### Q4

Answer: 8

\[
20 - 7 - 5 = 8
\]

### Q5

Answer: B

\[
\begin{align*}
\text{CPI}
&= 0.50(1) + 0.20(5) + 0.10(4) + 0.20(2) \\
&= 0.50 + 1.00 + 0.40 + 0.40 \\
&= 2.3
\end{align*}
\]

### Q6

Answer: 8

```
PUSH P
PUSH Q
ADD
PUSH R
PUSH S
SUB
MUL
POP W
```

That is 8 instructions. Each input must be pushed, the two binary operations on \((P+Q)\) and \((R-S)\) are required, the multiply combines them, and one pop stores \(W\).

### Q7

Answer: A, B, D

RISC designs favour register-register ALU operations, fixed-length instructions, load/store data transfer, and a small addressing-mode set. A memory-to-memory string edit is a CISC-style complex instruction, so C does not apply.

### Q8

Answer: C

```
MOV T1, P
ADD T1, Q
MOV T2, R
SUB T2, S
MUL T1, T2
MOV W, T1
```

The first address of each binary operation is also the destination, so each product term needs a move before the arithmetic, and \(W\) needs a final move. Six instructions is the minimum under the stated constraint.

### Q9

Answer: 7

\(2^6 = 64 < 100\) and \(2^7 = 128 \ge 100\). The opcode needs 7 bits.

### Q10

Answer: 12

Forty types need 6 opcode bits because \(2^5 = 32 < 40 \le 64 = 2^6\). Each of 128 registers needs \(\log_2 128 = 7\) bits. Two register fields use 14 bits.

\[
32 - 6 - 14 = 12
\]

### Q11

Answer: 448

Four opcode bits give 16 two-address slots. Nine are consumed, leaving \(16 - 9 = 7\) prefixes. Each prefix plus a 6-bit extension gives \(2^6 = 64\) one-address opcodes.

\[
7 \times 64 = 448
\]

### Q12

Answer: A, B, D

A stack operation names no operand address, and an accumulator operation names only the memory operand. A three-address instruction has a separate destination field. Two address fields cannot name three locations. Big-endian placement puts the most significant byte at the smallest address. C is false.

### Q13

Answer: 500

\[
T = \frac{N \times \text{CPI}}{f}
= \frac{6 \times 10^{8} \times 2.5}{3 \times 10^{9}}
= 0.5 \text{ s}
= 500 \text{ ms}
\]

### Q14

Answer: 1792

A 6-bit three-address opcode has 64 values. Using 36 of them leaves \(64 - 36 = 28\) prefixes. Each prefix is extended by the unused 6-bit field, producing \(2^6 = 64\) two-address opcodes.

\[
28 \times 64 = 1792
\]

### Q15

Answer: C

```
LOAD A
MUL B
STORE T1
LOAD C
MUL D
ADD T1
SUB E
STORE Y
```

The accumulator holds only one intermediate value, so \(A \times B\) must be stored before \(C \times D\) is formed. Eight instructions is the minimum.

### Q16

Answer: 128

Two hundred fifty-six operations need 8 opcode bits. Reserving at least 10 immediate bits leaves

\[
32 - 8 - 10 = 14
\]

bits for two equal register fields, so each field has 7 bits. The largest power-of-two register file is \(2^7 = 128\). A wider immediate would leave fewer register bits.

### Q17

Answer: 1.8

\[
\begin{align*}
T_R &= \frac{5 \times 10^{8} \times 1.2}{2.4 \times 10^{9}} = 0.25 \text{ s} \\
T_C &= \frac{2 \times 10^{8} \times 3.6}{1.6 \times 10^{9}} = 0.45 \text{ s} \\
\frac{T_C}{T_R} &= \frac{0.45}{0.25} = 1.8
\end{align*}
\]

### Q18

Answer: A, B, D

Three register fields occupy \(3 \times 4 = 12\) bits, so a format with no other operand field has a 12-bit opcode. Two registers plus an 8-bit immediate occupy 16 bits, leaving an 8-bit opcode. Using all \(2^{12}\) three-register opcodes fills the entire 24-bit space, so C is impossible. With a 2-bit format field, the remaining length is 22 bits and three registers take 12, leaving \(22 - 12 = 10\) opcode bits. Register specifiers are 4 bits because there are 16 registers.
