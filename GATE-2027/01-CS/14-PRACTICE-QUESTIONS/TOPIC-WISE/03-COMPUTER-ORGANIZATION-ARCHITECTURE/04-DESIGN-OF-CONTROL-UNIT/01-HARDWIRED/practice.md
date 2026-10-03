# Hardwired Control — Practice Questions

Original practice for GATE CS. These questions are not from any GATE paper. Attempt the questions before reading the solutions.

## Level 1 — Conceptual

## Q1 — MCQ

A hardwired control unit produces control signals primarily by

A. reading microinstructions from a control memory  
B. combinational logic driven by the opcode and a timing state  
C. the ALU condition flags alone  
D. a DMA grant line

---

## Q2 — MCQ

The step counter, or timing state, in a hardwired control unit is used to

A. select a general-purpose register number  
B. distinguish the successive clock cycles of an instruction  
C. store the microprogram  
D. hold the immediate operand

---

## Level 2 — Standard GATE Style

## Q3 — NAT

The longest instruction uses 6 timing states, encoded in a binary state register. What is the minimum number of bits in that register?

---

## Q4 — MCQ

Which action belongs to instruction fetch and does not depend on the opcode?

A. Drive the PC onto the bus, load the MAR, and start a memory read  
B. Subtract the two ALU inputs  
C. Write the destination register of an ADD  
D. Load a branch target into the PC

---

## Q5 — MSQ

Select all that apply to hardwired control.

A. The control equations are implemented in logic rather than by a control-store lookup.  
B. Changing the instruction set usually means changing that logic.  
C. The primary control store is a microprogram ROM.  
D. Opcode bits are inputs of the control equations.

---

## Level 3 — Multi-Step

## Q6 — NAT

A designer compares a hardwired encoder with a ROM that stores the same control truth table. The ROM is addressed by a 3-bit opcode and a 3-bit state, and each word contains 12 control signals. How many bits does that ROM contain?

---

## Q7 — MCQ

After fetch and decode, a single-bus datapath executes `ADD R1, R2, R3`, defined as `R1 ← R2 + R3`. Both ALU input registers must be loaded, and they can be loaded only in different cycles. The addition and the write into `R1` occur together in a later cycle. How many execute cycles are required?

A. 2  
B. 3  
C. 4  
D. 5

---

## Level 4 — Tricky / Trap-Based

## Q8 — NAT

Fetch is implemented by 3 states shared by every instruction. Beyond fetch, `ADD` needs 3 states, `LOAD` needs 5 states, and `BRANCH` needs 2 states. These are the only instruction classes, and no execute state is shared between classes. A binary state register must distinguish every state. How many bits does it need?

---

## Q9 — MSQ

After fetch and decode, `STORE R1, (R2)` means \(M[R2] \leftarrow R1\). The execute states are

- T3: `R2out`, `MARin`
- T4: `R1out`, `MDRin`, memory `Write`
- T5: wait until memory completes

Select all that apply.

A. `R2out` is asserted in the state that sends the address to the MAR.  
B. Memory `Read` is asserted in the same state as the data write.  
C. `R1out` places the stored value on the bus.  
D. Memory `Write` is asserted in the state that sends the data toward memory.

---

## Level 5 — Challenge

## Q10 — NAT

The opcode decoder and the state decoder each take 2 ns and operate in parallel. After both decoder outputs are valid, the control equations take 5 ns. The state register has clock-to-Q delay 1 ns and setup time 1 ns. The opcode in the IR is already stable at the clock edge. What is the minimum clock period, in nanoseconds?

## Answer Key

| Q | Type | Answer |
|---|------|--------|
| 1 | MCQ | B |
| 2 | MCQ | B |
| 3 | NAT | 3 |
| 4 | MCQ | A |
| 5 | MSQ | A, B, D |
| 6 | NAT | 768 |
| 7 | MCQ | B |
| 8 | NAT | 4 |
| 9 | MSQ | A, C, D |
| 10 | NAT | 9 |

## Detailed Solutions

### Q1

Answer: B

Hardwired control decodes the opcode and the current timing state with combinational logic. A control memory belongs to microprogrammed control. Flags and DMA requests can qualify individual signals, but they are not the source of the whole control sequence.

### Q2

Answer: B

The step counter identifies T0, T1, T2, and so on. Register numbers come from instruction fields, the microprogram belongs to a control store, and the immediate is data, not timing state.

### Q3

Answer: 3

Six states need a binary code with \(2^k \ge 6\). Since \(2^2 = 4 < 6\) and \(2^3 = 8 \ge 6\), the register has 3 bits. A one-hot ring counter would use 6 flip-flops; the question asks for the binary encoding.

### Q4

Answer: A

Every instruction begins by sending the PC to memory and reading the instruction word. Subtract, destination write-back, and branch-target load are opcode-specific execute actions.

### Q5

Answer: A, B, D

Hardwired control is logic plus a state element, so the opcode and the state are equation inputs, and an ISA change changes the equations. A microprogram ROM is the defining store of microprogrammed control, so C does not apply.

### Q6

Answer: 768

The address is \(3 + 3 = 6\) bits, so the ROM has \(2^6 = 64\) words. Each word is 12 bits.

\[
64 \times 12 = 768
\]

### Q7

Answer: B

The single bus can load only one ALU input per cycle.

1. Place `R2` on the bus and load the first ALU input register.
2. Place `R3` on the bus and load the second ALU input register.
3. Add and write the result into `R1`.

That is 3 execute cycles. Fetch and decode are excluded by the question.

### Q8

Answer: 4

Shared fetch contributes 3 states, and the three classes contribute \(3 + 5 + 2 = 10\) private states.

\[
3 + 10 = 13
\]

\(2^3 = 8 < 13\) and \(2^4 = 16 \ge 13\), so the binary state register has 4 bits.

### Q9

Answer: A, C, D

T3 gates `R2` to the MAR, so A is true. T4 gates `R1` to the MDR and asserts `Write`, so C and D are true. A store does not assert `Read` in the write state, and `PCout` belongs to fetch rather than to the data phase. B and E are false.

### Q10

Answer: 9

The state bits become valid 1 ns after the clock. The parallel decoders then take 2 ns. The equations take 5 ns, and the next state must satisfy the 1 ns setup time.

\[
1 + 2 + 5 + 1 = 9 \text{ ns}
\]

The opcode decoder does not add a further 2 ns because it runs at the same time as the state decoder, and the IR is already stable.
