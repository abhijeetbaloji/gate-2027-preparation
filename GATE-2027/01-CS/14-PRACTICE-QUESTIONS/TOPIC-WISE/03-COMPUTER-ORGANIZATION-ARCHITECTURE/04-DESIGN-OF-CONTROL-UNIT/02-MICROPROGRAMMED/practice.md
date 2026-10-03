# Microprogrammed Control — Practice Questions

Original practice for GATE CS. These questions are not from any GATE paper. Attempt the questions before reading the solutions.

## Level 1 — Conceptual

## Q1 — MCQ

Control memory in a microprogrammed control unit stores

A. the user program  
B. microinstructions  
C. cache tags  
D. page-table entries

---

## Q2 — MCQ

Horizontal microprogramming is characterized by

A. a short control word whose fields are heavily encoded and then decoded  
B. a wide control word with a separate bit for most control signals  
C. the absence of a control memory  
D. a hardwired sequencer with no control word

---

## Q3 — NAT

A control memory holds 64 microinstructions. How many bits are required in a microprogram counter that can address every microinstruction?

---

## Level 2 — Standard GATE Style

## Q4 — NAT

A horizontal microinstruction has one bit for each of 24 control signals and an 8-bit next-address field. There is no extra encoding. How many bits wide is the control word?

---

## Q5 — MCQ

A vertical format may assert at most one of 24 control signals. One extra code means “assert none”. How many bits does that encoded field need?

A. 4  
B. 5  
C. 24  
D. 25

---

## Q6 — MSQ

Select all that apply.

A. A horizontal control word is wider than a fully vertical encoding of the same signals.  
B. A vertical microinstruction normally needs an external decoder.  
C. Changing a microprogram is usually easier than rewiring a hardwired control unit.  
D. Control memory is part of the memory space that user programs address.

---

## Level 3 — Multi-Step

## Q7 — NAT

A horizontal control memory has 128 words of 40 bits each. How many bits does the control memory contain?

---

## Q8 — MCQ

Every microinstruction contains a 7-bit absolute next-address field, and that field is the only way a microinstruction names its successor. What is the maximum number of microinstructions this field can address?

A. 7  
B. 14  
C. 128  
D. 256

---

## Level 4 — Tricky / Trap-Based

## Q9 — NAT

A control word is encoded as follows.

| Field | Choices | Bits |
|---|---|---|
| ALU operation | 16 mutually exclusive operations | 4 |
| Register select | 32 registers | 5 |
| Memory command | none, read, write, fetch | 2 |
| Direct signals | 10 signals that may be simultaneous | 10 |
| Next address | 256 control-memory words | 8 |

The control memory contains 256 microinstructions. How many bits does it contain?

---

## Q10 — MSQ

Select all that apply.

A. A mapping ROM can translate a machine opcode into the starting control-memory address of its microroutine.  
B. A conditional microbranch can test an ALU flag.  
C. Every microinstruction must carry an absolute next address; a micro-PC increment is impossible.  
D. The fetch microroutine is normally shared by every machine instruction.

---

## Level 5 — Challenge

## Q11 — NAT

An unencoded horizontal word has 45 control bits plus a 9-bit next address. An encoded alternative partitions the 45 signals into 9 groups of 5. In each group exactly one of the five actions is selected, so each group is encoded in the minimum number of bits. The 9-bit next address is unchanged. Control memory has 512 words. How many bits does the encoded design save compared with the horizontal design?

---

## Q12 — MCQ

Control memory has an 8 ns access, and the next microinstruction is not fetched until the current one has finished. A machine instruction averages 6 microinstructions. A hardwired implementation of the same instruction uses 4 clocks of 10 ns. The microprogrammed control time exceeds the hardwired control time by

A. 8 ns  
B. 16 ns  
C. 24 ns  
D. 48 ns

## Answer Key

| Q | Type | Answer |
|---|------|--------|
| 1 | MCQ | B |
| 2 | MCQ | B |
| 3 | NAT | 6 |
| 4 | NAT | 32 |
| 5 | MCQ | B |
| 6 | MSQ | A, B, C |
| 7 | NAT | 5120 |
| 8 | MCQ | C |
| 9 | NAT | 7424 |
| 10 | MSQ | A, B, D |
| 11 | NAT | 9216 |
| 12 | MCQ | A |

## Detailed Solutions

### Q1

Answer: B

Control memory holds the microprogram. User instructions live in main memory. Cache tags and page tables are memory-system structures, not the control store.

### Q2

Answer: B

Horizontal control gives most datapath signals their own bit, so several compatible signals can be asserted by one wide word. Vertical control packs mutually exclusive signals into short encoded fields. Hardwired control has no control word.

### Q3

Answer: 6

\(2^6 = 64\), so the microprogram counter needs 6 bits.

### Q4

Answer: 32

The 24 signal bits are already horizontal. Adding the next-address field gives

\[
24 + 8 = 32
\]

### Q5

Answer: B

The field must name one of 24 signals or name no signal. That is 25 codes. \(2^4 = 16 < 25\) and \(2^5 = 32 \ge 25\), so the field is 5 bits. A horizontal encoding would have used 24 bits.

### Q6

Answer: A, B, C

Horizontal words are wider because they are not packed through a decoder. Vertical fields are decoded outside the control word. A microprogram can be rewritten without changing the datapath equations, and each ISA instruction expands into a microroutine. Control memory is an internal control store, not user-addressable main memory, so D is false.

### Q7

Answer: 5120

\[
128 \times 40 = 5120
\]

### Q8

Answer: C

A 7-bit address distinguishes \(2^7 = 128\) control-memory locations. The question says the field is absolute and is the only successor mechanism, so the address space is exactly those 128 words.

### Q9

Answer: 7424

The control-word width is

\[
4 + 5 + 2 + 10 + 8 = 29 \text{ bits}
\]

The direct signals stay one bit each because they may be asserted together. The other fields are mutually exclusive, so they are encoded.

\[
256 \times 29 = 7424
\]

### Q10

Answer: A, B, D

Opcode mapping and conditional tests on flags are standard sequencing tools. Fetch is entered for every instruction before the opcode selects a microroutine. A micro-PC can advance sequentially, so an absolute next address is not mandatory. Vertical encoding shortens the signal fields; it does not remove the need to choose the next microinstruction. C and E are false.

### Q11

Answer: 9216

Five mutually exclusive actions need \(\lceil \log_2 5 \rceil = 3\) bits because \(2^2 = 4 < 5\) and \(2^3 = 8 \ge 5\). Nine groups use \(9 \times 3 = 27\) bits. With the next address, the encoded word is

\[
27 + 9 = 36 \text{ bits}
\]

The horizontal word is

\[
45 + 9 = 54 \text{ bits}
\]

Each of the 512 words saves \(54 - 36 = 18\) bits.

\[
512 \times 18 = 9216
\]

### Q12

Answer: A

Six microinstructions at 8 ns take

\[
6 \times 8 = 48 \text{ ns}
\]

The hardwired sequence takes

\[
4 \times 10 = 40 \text{ ns}
\]

\[
48 - 40 = 8 \text{ ns}
\]
