# Instruction Set — Notes (GATE CS 2027)

> Self-contained notes. Conventions used in the whole COA folder: 1 K = 2¹⁰, 1 M = 2²⁰, 1 G = 2³⁰ (binary prefixes) unless a
> question says otherwise; memory is byte-addressable unless a question says "word-addressable"; sizes are in **bytes** unless
> a line says "bits". Iron law: CPU time = IC × CPI × clock period = IC × CPI / f. Math is plain Markdown + Unicode.
> Every numeric example here was recomputed by `/tmp/coa-verify-01-instruction-set.py` (outside the repository).

---

## 0. Where this fits

**Syllabus line (COA):** "Instruction set and addressing modes. Design of arithmetic and logic unit (ALU). Design of control unit —
hardwired and microprogrammed. Memory interfacing and hierarchy: performance, cache memory mapping. I/O interface (interrupt and DMA).
Instruction pipelining, pipeline hazards."
This folder owns the first sentence's first half: **Instruction set** (what the machine can do and how an instruction is encoded).
The second half, *addressing modes*, is a separate leaf: [`../02-ADDRESSING-MODES/`](../02-ADDRESSING-MODES/).

**Prerequisites**
- Binary numbers, powers of two, ⌈log₂ n⌉ (to size bit fields). Two's complement for signed immediates:
  [`../../02-DIGITAL-LOGIC/03-NUMBER-REPRESENTATION-AND-ARITHMETIC/`](../../02-DIGITAL-LOGIC/03-NUMBER-REPRESENTATION-AND-ARITHMETIC/).
- Basic notion of a program as a sequence of instructions stored in memory (stored-program idea).

**What depends on this topic**
- [`../02-ADDRESSING-MODES/`](../02-ADDRESSING-MODES/) — how an *operand field* is interpreted (the fields counted here).
- [`../04-DESIGN-OF-CONTROL-UNIT/`](../04-DESIGN-OF-CONTROL-UNIT/) — the opcode decoding and the fetch–decode–execute micro-steps of §2.
- [`../07-INSTRUCTION-PIPELINING/`](../07-INSTRUCTION-PIPELINING/) and [`../08-PIPELINE-HAZARDS/`](../08-PIPELINE-HAZARDS/) — fixed-length load/store RISC
  instructions are what make a clean 5-stage pipeline possible; the iron law of §8 is the base of all pipeline speedup questions.
- [`../05-MEMORY-INTERFACING-AND-HIERARCHY/01-PERFORMANCE/`](../05-MEMORY-INTERFACING-AND-HIERARCHY/01-PERFORMANCE/) — CPI with memory stalls (bridge in §8.6).
- Compiler design (register allocation, spilling) — only the ISA-visible part is used here (§7).

---

## 0.1 Evidence snapshot (what drives the depth of each section)

Source: the mapping file [`questions.md`](../../13-PYQ-TOPIC-MAPPING/03-COMPUTER-ORGANIZATION-ARCHITECTURE/01-INSTRUCTION-SET/questions.md)
(17 mapped entries = 11 distinct questions, of which 1 is misfiled; 10 are on-topic or partly on-topic — see [`PYQ.md`](PYQ.md)), a search of the extracted paper text for
related questions filed under other leaves, and the 18-question existing practice file.

| Section | Priority | Evidence |
|---|---|---|
| §6 Instruction **encoding arithmetic** (fixed fields, byte alignment, format bit, expanding opcodes) | **HIGH-VALUE** | 6 of the 10 distinct mapped questions (2016 ×2, 2020, 2024, 2025, 2026 CS-2) are bit-field/opcode counting; related ones filed under other leaves (2018, 2024 CS-2 Q57) use the same method; existing practice Q4, Q9–Q11, Q14, Q16, Q18. |
| §3 Address-count machines and what an address field can name | **HIGH-VALUE** | 2015 Q22 (conceptual); practice Q2, Q12. |
| §4 Expression evaluation / load-store sequences | **HIGH-VALUE** | 2026 CS-1 Q15 (load-store sequence for an assignment); practice Q1, Q6, Q8, Q15. |
| §5 RISC vs CISC | MEDIUM | practice Q7; a RISC-characteristics question is filed under the hardwired-control leaf (2018). |
| §8 Iron law, CPI, MIPS, Amdahl | MEDIUM | practice Q5, Q13, Q17; iron-law ratio and CPI questions are filed under pipelining leaves. Needed as a base for the whole COA folder. |
| §1 ISA vs organization | MEDIUM | An "is X part of the ISA?" question exists in the paper text filed under the cache leaf (2025 CS-2 Q28); cheap to learn. |
| §7 Register pressure / spilling | LOW–MEDIUM | 8 of 17 mapped entries (2013, but only 2 distinct questions) — the code segment is **not** in the mapping text (see §7). |
| §2 Registers and instruction cycle | MEDIUM (prerequisite) | Required for the memory-access counting in §4 and for control-unit leaves. |
| §9 Endianness and alignment | LOW | Only existing practice Q3; no mapped PYQ. Kept short. |

---

## 1. ISA, organization, implementation — what is "in" the instruction set?

### 1.1 Intuition
Think of a car. The **driver's manual** (pedals, gear positions, what turning the wheel does) is the *interface*. The engine size,
number of cylinders, turbo, fuel injection are the *implementation*. Two cars with different engines can obey the same manual.
The **Instruction Set Architecture (ISA)** is that manual for a processor: everything a *programmer or compiler* can see and must
rely on. The **microarchitecture / organization** is how a particular chip realises that interface.

### 1.2 Definitions

- **ISA**: the programmer-visible contract — the set of instructions and their encodings, the registers (how many, how wide, special roles),
  the data types, the addressing modes, the memory model (address-space size, word size, byte order, alignment rules), and how
  exceptions/interrupts/I-O are presented to software.
- **Organization / microarchitecture**: how the ISA is implemented — pipeline depth, number of functional units, cache sizes and levels,
  branch predictor, bus widths inside the chip, hardwired vs microprogrammed control.
- **Implementation / technology**: transistor process, clock frequency, power.

```
        software (compiler, OS)            <- sees only the ISA
  ------------------------------------  ISA boundary
        microarchitecture                  <- pipeline, caches, predictor, control style
        circuits / technology              <- clock frequency, process
```

### 1.3 Classification table (use this for "is it part of the ISA?" questions)

| Item | ISA? | Why |
|---|---|---|
| Instruction opcodes and their formats / field widths | **Yes** | The binary program depends on them |
| Number of architectural (programmer-visible) general-purpose registers, their width | **Yes** | The compiler allocates them; a binary uses their names |
| Addressing modes offered | **Yes** | Part of how instructions name operands |
| Address-space size, word size, endianness, alignment rule | **Yes** | Visible in every load/store |
| Condition codes / flags, special registers (PC, SP) visible to software | **Yes** | Instructions read/write them |
| Number of pipeline stages | No | Same program runs on a 5-stage and a 14-stage chip |
| Clock frequency | No | Performance detail, not behaviour |
| Cache size, number of cache levels, associativity, block size | No (normally) | Transparent to software; only performance changes. *Cache-management instructions*, if any, are ISA, but the cache's geometry is not |
| Hardwired vs microprogrammed control unit | No | Implementation style |
| Number of physical (renamed) registers inside the chip | No | Hidden; only architectural registers are visible |
| Number of ALUs, issue width | No | Same |

**Binary compatibility** means two processors implement the same ISA. Intel and AMD x86 chips differ massively inside but run the
same machine code; a newer chip with a larger cache is still the same ISA.

> Edge case: *virtual-memory page size* or a *memory-ordering model* are visible to systems software and are specified at the ISA/architecture level in
> real processors. GATE-level questions only ask the clear-cut cases in the table.

---

## 2. CPU registers and the instruction cycle

### 2.1 Registers you must know

| Register | Holds | Notes |
|---|---|---|
| **PC** (program counter) | Address of the *next* instruction | Updated during fetch (+ instruction size) or by a branch |
| **IR** (instruction register) | The instruction being executed | Control unit decodes the opcode bits of IR |
| **MAR** (memory address register) | Address placed on the address bus | Loaded from PC (fetch) or from an operand address |
| **MDR / MBR** (memory data/buffer register) | Word read from / to be written to memory | Data bus ↔ CPU |
| **ACC** (accumulator) | Implicit operand and result of one-address ALU ops | Only on accumulator machines |
| **GPRs** R0…Rn | Operands and results | Named by *register fields* of the instruction |
| **SP** (stack pointer) | Address of top of the memory stack | For call/return and stack machines' memory stack |
| **Flags / PSW** | Z (zero), N (negative), C (carry), V (overflow), … | Set by ALU ops, tested by conditional branches |

### 2.2 The instruction cycle (register-transfer view)

```
FETCH    MAR <- PC
         MDR <- M[MAR]                    (1 memory read)
         PC  <- PC + instruction size     (in addressable units; a byte-addressed machine with 4-byte
                                           instructions adds 4)
         IR  <- MDR
DECODE   control unit reads the opcode (and mode bits) of IR
EXECUTE  depends on the instruction class:
   ALU, register operands : Rd <- Rs1 op Rs2                      (0 data-memory accesses)
   LOAD  Rd, addr         : MAR <- addr ; MDR <- M[MAR] ; Rd <- MDR   (1 read)
   STORE Rs, addr         : MAR <- addr ; MDR <- Rs ; M[MAR] <- MDR   (1 write)
   BRANCH (taken)         : PC <- target                           (0 data-memory accesses)
   (then check for pending interrupts, repeat)
```

**Memory references per instruction = 1 (fetch) + number of operand references.** A multi-word (variable-length) instruction needs
one fetch read per word. Instruction fetches are *instruction-memory* references; the data reads and writes of LOAD/STORE and
memory-operand ALU instructions are *data-memory* references. Always read whether a question wants "data accesses", "memory
accesses including fetch" or "instruction count".

---

## 3. Operand-addressing styles: how many addresses?

### 3.1 Intuition
Evaluate `Z = X + Y`. How much of the "where are the operands and where does the result go" must the instruction spell out?
The fewer the places the instruction names *explicitly*, the more it relies on **implied** places (the accumulator, the top of
the stack). Implied places cost no bits but force extra data-movement instructions.

### 3.2 The five classic styles

| Style | Typical ALU instruction | Explicit addresses | Implicit |
|---|---|---|---|
| **Stack (0-address)** | `ADD` | 0 (only `PUSH a`/`POP a` carry 1 address) | both sources = top two stack entries, result pushed |
| **Accumulator (1-address)** | `ADD m` | 1 | other source **and** destination = ACC |
| **2-address** | `ADD d, s` (d ← d + s) | 2 | destination = first source (it is overwritten) |
| **3-address** | `ADD d, s1, s2` | 3 | none |
| **Load–store (register–register)** | `ADD Rd, Rs1, Rs2`; `LOAD Rd, m`; `STORE Rs, m` | arithmetic: 3 *register* fields; only LOAD/STORE touch memory | none |

Two extra flavours of the *3-address* and *2-address* forms:
- **Register machines** — each address field names a *processor register*.
- **Memory-to-memory machines** — each address field names a *memory location* (textbook model; real example: VAX-style). 

So the answer to "what can the address field of a 3-address instruction specify?" is: **a memory operand or a processor register,
depending on the machine; the instruction does not need an address field for an implied operand**. A register that is implied
(accumulator, top of stack) is by definition *not named* by any field — it belongs to the 0/1-address styles. The question to ask is
always "is this operand named by a field, or implied by the opcode?".

### 3.3 Trade-off

```
more explicit addresses  ->  longer instruction, fewer instructions per program
fewer explicit addresses ->  shorter instruction, more instructions (extra LOAD/STORE/PUSH/POP/MOV)
```
Example sizing: a memory-to-memory 3-address instruction with 16-bit addresses and an 8-bit opcode is 8 + 3×16 = 56 bits.
A load–store instruction with 32 registers is 8 + 3×5 = 23 bits, but a program needs extra LOAD/STORE instructions.

### 3.4 What kinds of instructions exist (classification only)

Data transfer (LOAD, STORE, MOV, PUSH, POP) · arithmetic/logic (ADD, SUB, AND, SHIFT, compare) · control transfer (JUMP, conditional
branch, CALL, RETURN) · system/I-O (trap, IN/OUT, halt). Branches carry one address field (target or offset) and often implied
condition flags; a `RETURN` can have zero address fields (the return address is on the stack).

---

## 4. Evaluating expressions: counting instructions and memory accesses

This is the standard way GATE-style questions test §3. The method: **write the code for the machine, then count**.

### 4.1 Setup and ground rules (state them in every answer)
- Variables are in memory (`A, B, C, …`), the result variable is also in memory.
- An **input must not be overwritten** unless the question says it may be.
- Temporaries live in registers (register machines) or in memory (accumulator / 2-address memory machines).
- A variable's repeated occurrence: stack machines `PUSH` it again each time (no `DUP` assumed); load–store machines can keep it in a
  register (load once). Memory-operand machines name it again for free.

### 4.2 Closed-form counting rules (verified)

Let *leaves* = operand occurrences in the expression, *ops* = binary operators. Every leaf occurrence is a distinct variable
unless stated.

| Machine | Instructions for `Z = expr` | Rule |
|---|---|---|
| Stack | leaves + ops + 1 | one `PUSH` per leaf, one op per operator, one `POP Z` |
| 3-address (memory-to-memory or register) | ops | the last operator writes `Z` directly |
| Load–store, enough registers | (distinct variables loaded) + ops + 1 | `LOAD` each variable once, op per operator, one `STORE` |
| Accumulator | cost(root) + 1 (final `STORE`) | recursion below |
| 2-address (destination = first source) | ops + (#`MOV`s) [+1 if `Z` cannot be a scratch location] | see below |

**Accumulator recursion.** `cost(leaf) = 1` (a `LOAD`). For `op(l, r)`:
```
r is a leaf                          : cost(l) + 1                 (ACC op r)
l is a leaf and op is + or *         : cost(r) + 1                 (commute: ACC op l)
l is a leaf and op is - or /         : cost(r) + 3                 (STORE T; LOAD l; OP T)
both children complex                : cost(l) + cost(r) + 2       (one child must be STOREd to a temp, then used as memory operand)
```
The "both complex" case is the heart of the matter: the accumulator can hold only **one** intermediate value; a second one must be
parked in memory with a `STORE` and re-used as a memory operand — that costs 2 extra instructions.

**2-address (destructive) rule.** `ADD d, s` computes d ← d op s, so the first operand's location is destroyed.
- If the first operand is an *input variable* (or still needed), copy it first: `MOV T, X` (+1).
- If the first operand is a temporary holding a sub-result, no copy is needed.
- For `+` and `*`, if the left child is a leaf and the right child is a computed temporary, swap the operands to avoid the `MOV`.
- Count = ops + (number of operators whose first operand, after swapping, is a leaf).
- The final value must end in `Z`. If `Z` may be used as the working location from the start (it is not an input), no extra move is
  needed; if the question only allows a final `MOV Z, T`, add 1.
  **Read the statement: whether the destination may be used as a scratch location changes the count by one.**

(The accumulator and 2-address rules were checked against exhaustive breadth-first search over programs for the expressions in this file and 83 random expression
trees of up to 5 distinct leaves; the search assumes no algebraic rewriting and commutativity of `+`, `*` only. The stack, 3-address and load–store
rules were checked by executing the programs on sample data.)

### 4.3 Worked example — one expression on every machine

Expression: **W = (A + B) × (C − D) + E**, inputs must not change. Leaves = 5, ops = 4.

```
STACK (10 instr, 6 data refs, max stack depth 3)       ACCUMULATOR (8 instr, 8 data refs)
  PUSH A      stack: A                                   LOAD  C       ACC = C
  PUSH B      A B                                        SUB   D       ACC = C-D
  ADD         (A+B)                                      STORE T1      T1  = C-D
  PUSH C      (A+B) C                                    LOAD  A
  PUSH D      (A+B) C D                                  ADD   B       ACC = A+B
  SUB         (A+B) (C-D)                                MUL   T1      ACC = (A+B)*(C-D)
  MUL         X                                          ADD   E
  PUSH E      X E                                        STORE W
  ADD         result
  POP  W

2-ADDRESS (d <- d op s)  (7 instr, 18 data refs)       3-ADDRESS (4 instr, 12 data refs, memory-to-memory)
  MOV T1, A                                                ADD T1, A,  B
  ADD T1, B       T1 = A+B                                 SUB T2, C,  D
  MOV T2, C                                                MUL T1, T1, T2
  SUB T2, D       T2 = C-D                                 ADD W,  T1, E
  MUL T1, T2
  ADD T1, E                                            LOAD-STORE (10 instr, 6 data refs)
  MOV W,  T1                                               LOAD R1,A ; LOAD R2,B ; ADD R1,R1,R2
  (6 instr if W is allowed as scratch: replace T1 by W     LOAD R2,C ; LOAD R3,D ; SUB R2,R2,R3
   and drop the final MOV)                                 MUL R1,R1,R2 ; LOAD R2,E ; ADD R1,R1,R2
                                                           STORE R1,W
```

Summary (verified by executing each program on sample data):

| Machine | Instructions | Data-memory refs | Instruction fetches (1 word each) | Total memory refs |
|---|---|---|---|---|
| Stack | 10 | 6 (5 PUSH + 1 POP) | 10 | 16 |
| Accumulator | 8 | 8 | 8 | 16 |
| 2-address memory (7-instr version) | 7 | 18 (MOV = 2, ALU op = 3) | 7 | 25 |
| 3-address memory | 4 | 12 (2 reads + 1 write each) | 4 | 16 |
| Load–store | 10 | 6 | 10 | 16 |

Lesson: fewer instructions does not mean fewer memory references. (Instruction fetch count assumes each instruction is one word;
memory-operand instructions are often longer — see §6.7 for multi-word instructions.)

### 4.4 Load–store sequences for an assignment (`Z = X + Y`-type)

On a load–store machine **no arithmetic instruction may name a memory operand**. For `P = Q − S` (memory variables `P, Q, S`; registers `R0, R1, …`)
with the convention that the **first operand is the destination**:

```
LOAD  R1, Q        ; R1 <- Q            (destination register first, memory source second)
LOAD  R2, S        ; R2 <- S
SUB   R3, R1, R2   ; R3 <- R1 - R2      (three register operands)
STORE P,  R3       ; P  <- R3           (destination = memory operand P comes first, source register second)
```
Typical wrong candidates: `SUB P, Q, S` (memory operands in an ALU instruction), `LOAD R1, Q` followed by `SUB R3, R1, S` (one source still in memory),
and `STORE R3, P` (operands reversed for a destination-first convention).

**Checking a candidate sequence (a four-question test):**
1. Does any ALU instruction contain a memory operand? If yes, the sequence is **not** load–store.
2. Is every source loaded into a register before it is used, and is nothing overwritten while still needed?
3. Is the result stored to memory at the end?
4. Does the operand **order** respect the stated convention (destination first ⇒ `LOAD Rd, mem`, `STORE mem, Rs`, `ADD Rd, Rs1, Rs2`)?
Minimum for `Z = X + Y` on a load–store machine: 4 instructions (2 LOAD, 1 ADD, 1 STORE) and 3 data-memory references.

---

## 5. RISC vs CISC

### 5.1 Why the two philosophies exist
A CISC (complex instruction set computer) tries to make instructions *powerful* so one instruction does a lot (memory-operand arithmetic, string
moves, many addressing modes), keeping programs short (low IC) when memory was expensive. A RISC (reduced instruction set computer) keeps
instructions *simple and regular* so that the hardware can run them fast and overlapped (low CPI, short clock), and lets the compiler
generate more but simpler instructions (higher IC).

### 5.2 Characteristics

| Feature | RISC (typical) | CISC (typical) | Consequence |
|---|---|---|---|
| Instruction length | **Fixed** (e.g. 32 bits) | Variable (1–15+ bytes) | Fixed: decode in one step, next PC known immediately → pipelines well |
| Memory access | Only `LOAD`/`STORE` | Many instructions take memory operands | RISC ALU ops are **register-to-register** |
| Addressing modes | Few and simple | Many and complex | simpler control and address logic |
| Registers | Many (32+) | Fewer | fewer spills; compiler keeps data in registers |
| Control unit | Typically **hardwired** | Typically **microprogrammed** | speed vs flexibility |
| Instruction count for same program | Higher | Lower | trade-off with CPI |
| CPI | Close to 1 (pipelined) | Higher and variable | |
| Code size | Larger | Smaller | |

Typical RISC examples: MIPS, ARM, RISC-V. Typical CISC: x86, VAX. (Modern x86 chips internally translate to RISC-like micro-ops — a
microarchitecture fact, not an ISA fact.)

### 5.3 How the ISA choice moves the iron-law terms (preview of §8)

```
CPU time = IC  x  CPI  x  T
RISC:      up      down   down (simple stages)
CISC:      down    up     (longer / uneven)
```
No design wins automatically: only the product matters.

---

## 6. Instruction encoding arithmetic  (**HIGH-VALUE**)

An instruction is a bit string. Typical GATE questions give the *size of the instruction set*, the *number of registers*, the *word length*
and a *layout*, then ask for the size of one field, or for how many opcodes can still be assigned. Everything follows from a handful of rules.

### 6.1 Fixed fields

**Rule 1 — sizing a field to name `n` things:** bits = ⌈log₂ n⌉.

| n | 1 | 2 | 3–4 | 5–8 | 9–16 | 17–32 | 33–64 | 65–128 |
|---|---|---|---|---|---|---|---|---|
| bits | 0 | 1 | 2 | 3 | 4 | 5 | 6 | 7 |

Examples: 24 registers → 5 bits (not 4: 2⁴ = 16 < 24); 64 registers → 6 bits; 65 → 7 bits; 40 instruction types → 6 bits.
**n is the count of distinct things named, not a bit count.** "64 registers" does not mean 64 bits.

**Rule 2 — the leftover field:** immediate/offset bits = L − opcode − Σ(register fields) − Σ(other fixed fields).

**What is "opcode size" when the question says "k instructions" or "k instruction types"?** Distinct opcodes needed = k, so
opcode bits = ⌈log₂ k⌉ *when the opcode is a single fixed-length field*. If several instruction formats share the opcode space, use §6.3–§6.4.

**GATE procedure**
1. Draw the instruction as a row of boxes from the question (do not assume the number of register fields — **count the register operands in
   the instruction given**; `ADD R1, #25` names *one* register).
2. Compute each box width: opcode ⌈log₂ k⌉, each register field ⌈log₂ r⌉.
3. Subtract from L. The remainder is the maximum width of the field left undetermined ("maximum immediate bits").
4. Check: the boxes must add to L.

**Worked example 6.1-a.** 32-bit instructions, 90 instruction types, 35 registers, format `opcode | Rd | Rs | imm`.
- Opcode ⌈log₂ 90⌉ = 7 (2⁶ = 64 < 90 ≤ 128).
- Register fields ⌈log₂ 35⌉ = 6 each → 12 bits.
- Immediate = 32 − 7 − 12 = **13 bits**.

**Worked example 6.1-b (reverse direction).** 32-bit instructions, 100 operations, `opcode | Rd | Rs | imm` with the immediate required to be at least 12 bits;
largest register file? Opcode 7 bits; bits left for two equal register fields = 32 − 7 − 12 = 13 → ⌊13/2⌋ = 6 bits each → 2⁶ = **64 registers**
(the 13th bit is wasted; widening to 7 bits would need 14). If the format had three register fields: ⌊13/3⌋ = 4 → 16 registers.

**Signed/unsigned immediate range:** a w-bit immediate holds 0 … 2ʷ−1 (unsigned) or −2ʷ⁻¹ … 2ʷ⁻¹−1 (two's complement). With w = 12:
0…4095 or −2048…2047.

### 6.2 Byte-aligned (or word-aligned) program size

Instructions stored in memory occupy whole bytes. If the fields add to *b* bits, one instruction occupies ⌈b/8⌉ bytes, because **each instruction
starts on a byte boundary**; the padding is per instruction, not per program.

```
program size (bytes) = N  x  ceil(b / 8)           (NOT ceil(N*b / 8))
```
Worked example 6.2: 11 instruction types, 3 register fields from 40 registers, a 13-bit immediate.
b = ⌈log₂ 11⌉ + 3·⌈log₂ 40⌉ + 13 = 4 + 18 + 13 = 35 bits → ⌈35/8⌉ = 5 bytes. 60 instructions → **300 bytes**.
The wrong shortcut ⌈60·35/8⌉ = 263 bytes ignores per-instruction alignment. If instead each instruction must start on a 4-byte word
boundary: ⌈35/32⌉ = 2 words = 8 bytes each → 480 bytes. State which alignment you assume; "byte-aligned" ⇒ 8 bits.

### 6.3 Several formats distinguished by a format bit

Sometimes the question gives two formats (say R-type and I-type) and states "1 bit of the opcode distinguishes the type; the remaining bits
indicate the operation". Then:

```
opcode bits  =  1 (format bit)  +  ceil(log2 (max operations in one type))
```
- If the instructions are **equally divided** between the two types (n/2 each), 1 + ⌈log₂(n/2)⌉ = ⌈log₂ n⌉ always, so the answer equals the
  flat computation — but only in the equal-split case.
- If the split is **unequal**, the operation field must be sized for the *larger* type, so you pay more than a flat ⌈log₂ n⌉.

Worked example 6.3-a (equal split). 32-bit instructions, 200 instructions equally divided into R-type and I-type, 40 registers,
all register fields equal size. R-type: `opcode | unused | Rd | Rs1 | Rs2`. I-type: `opcode | Rd | Rs | imm`.
- Per type: 100 operations → ⌈log₂ 100⌉ = 7; with the format bit opcode = **8 bits** (same as ⌈log₂ 200⌉ = 8).
- Registers: ⌈log₂ 40⌉ = 6 bits.
- R-type unused field X = 32 − 8 − 3·6 = **6**. I-type immediate Z = 32 − 8 − 2·6 = **12**. Y = opcode = 8.
- Any combination follows, e.g. X + 2Y + Z = 6 + 16 + 12 = **34**.

Worked example 6.3-b (unequal split). 120 operations: 100 are R-type, 20 are I-type, 1 format bit then an operation field shared in width:
operation field = ⌈log₂ 100⌉ = 7, opcode = **8 bits**. A flat ⌈log₂ 120⌉ = 7 would wrongly give 1 spare bit to the immediate.

**Trap:** do not subtract the format bit twice, and do not forget that "opcode" in the problem may *include* the format bit — read the sentence.

### 6.4 Variable-length (expanding) opcodes — the "fraction of encoding space" method  (**the most frequent calculation**)

#### 6.4.1 Intuition
Imagine the 2ᴸ possible bit patterns of an L-bit instruction as a **cake**. An instruction with a k-bit opcode, whatever its operand
bits, claims **2⁻ᵏ of the cake** (it fixes k bits and leaves the others free for operands). Two different instructions must claim
**disjoint** slices — otherwise the decoder could not tell them apart. A shorter opcode claims a bigger slice. "Variable-sized
opcodes are permitted" means: different formats may have different opcode lengths, as long as no opcode is a prefix of another.

#### 6.4.2 Setup
For every instruction **type** t (a set of instructions with identical operand layout):
```
operand bits of t   = sum of its operand fields (registers, immediate, offset, ...)
opcode length o_t   = L - operand bits of t        (all remaining bits belong to the opcode/extension)
max opcodes of t    = 2^(o_t)                      (if t were alone)
slice of one opcode = 2^(-o_t) of the cake
```

#### 6.4.3 The rule
If type i has n_i opcodes assigned, the maximum number of opcodes of a target type T with opcode length o_T is

```
N_T(max) = floor( 2^(o_T) x ( 1 - sum_i  n_i x 2^(-o_i) ) )
         = floor( 2^(o_T)  -  sum_i  n_i x 2^(o_T - o_i) )
```
- If every other type has o_i ≤ o_T (target has the **longest** opcode), each term n_i·2^(o_T − o_i) is an integer; no floor is needed.
- If some o_i > o_T (target has a **shorter** opcode than a used type), terms like n_i / 2^(o_i − o_T) can be fractions. **Add the fractions first, then take the floor
  once.**

#### 6.4.4 Why it is correct (derivation)
- *Necessary:* the slices are disjoint, so Σ (slices) ≤ 1. Adding m opcodes of T needs Σ n_i·2^(−o_i) + m·2^(−o_T) ≤ 1, which gives the formula.
- *Sufficient:* arrange the opcodes by increasing length, always taking the next free prefix (canonical assignment). While the total slice ≤ 1,
  this never overflows and never makes one opcode a prefix of another. Therefore the formula is exactly the maximum. (This is the Kraft
  inequality, here derived directly from the cake picture. The script verified every example below by actually constructing the
  prefix-free code and checking prefix-freeness.)
- *Floor:* if the free space is not a multiple of the target's slice, the leftover fraction cannot hold a whole opcode.

#### 6.4.5 Solving procedure (GATE)
1. List every instruction type with its operand fields; compute operand bits and o_t = L − operand bits.
2. Note the opcode counts already assigned (n_i). Identify the target type T.
3. Compute N_T = 2^(o_T) − Σ n_i · 2^(o_T − o_i) (fractions allowed), then floor.
4. Sanity checks: 0 ≤ N_T ≤ 2^(o_T); the used counts must not already exceed their slices (n_i ≤ 2^(o_i), and Σ ≤ 1).
5. State assumptions: all bit patterns are legal; no separate format bit unless stated; opcode = every bit not claimed by an operand field.

#### 6.4.6 Worked example A — two types
16-bit instructions, 32 registers (5-bit fields). Type A: `opcode | R | imm6` — operand bits 5 + 6 = 11 → o_A = 5. Type B: `opcode | R | R` — operand bits 10 → o_B = 6.
Suppose 11 type-A opcodes are assigned. In 6-bit units each type-A opcode (5 bits) eats 2 slots.
N_B = 2⁶ − 11·2 = 64 − 22 = **42**. (Check with the cake: 11/32 used; 21/32 × 64 = 42.)

#### 6.4.7 Worked example B — three types, target has the longest opcode
16-bit instructions, 8 registers (3-bit fields).
- Type A: 3 registers + 4-bit imm → operand bits 13 → o_A = 3. Assigned: 5.
- Type B: 2 registers + 5-bit imm → 11 → o_B = 5. Assigned: 9.
- Target C: 1 register + 6-bit offset → 9 → o_C = 7.
N_C = 2⁷ − 5·2⁴ − 9·2² = 128 − 80 − 36 = **12**.

#### 6.4.8 Worked example C — target has the shortest opcode (fractions!)
Use the layouts of example B, but now the *target* is type A (3-bit opcode, 8 prefixes) and 9 opcodes of type B (5-bit) are assigned; type C is unused.
N_A = 2³ − 9/2² = 8 − 2.25 = 5.75 → floor → **5**. (Picture: each 3-bit prefix contains four 5-bit opcodes, so the nine type-B opcodes occupy ⌈9/4⌉ = 3 whole prefixes —
two full ones and one holding just one opcode — leaving 8 − 3 = 5 prefixes for type A.)
The "⌈used/4⌉" shortcut is only safe with **one** other type; with several types add exact fractions first (example D).

#### 6.4.9 Worked example D — the floor over several types
24-bit instructions, 32 registers (5 bits).
- X: 3 registers → 15 operand bits → o_X = 9, assigned 100.
- Y: 2 registers + 6-bit imm → 16 → o_Y = 8, assigned 21.
- Target Z: 1 register + 12-bit offset → 17 → o_Z = 7.
N_Z = 2⁷ − 21/2 − 100/4 = 128 − 10.5 − 25 = 92.5 → **92**.
Why "round each type separately" is wrong: take a 6-bit-opcode target and two other types with 8-bit opcodes, 37 and 10 opcodes assigned.
Rounding each upward to whole 6-bit prefixes gives 64 − ⌈37/4⌉ − ⌈10/4⌉ = 64 − 10 − 3 = 51, but the two partial prefixes can share (37 + 10 = 47 opcodes
fill ⌈47/4⌉ = 12 prefixes), so the correct value is ⌊64 − 47/4⌋ = 52.
Always add the exact fractions of all types, *then* take one floor.

#### 6.4.10 The classic chain: 3-address → 2-address → 1-address → 0-address
When a long-opcode format is created by **re-using an operand field as opcode extension**, the same cake rule gives a recursion.
Let *w* = width of one address field, L the instruction length.

```
level 3-addr :  opcode = L - 3w bits;  slots S3 = 2^(L-3w)
level 2-addr :  free prefixes = S3 - n3          ; slots S2 = (S3 - n3) * 2^w
level 1-addr :  free prefixes = S2 - n2          ; slots S1 = (S2 - n2) * 2^w
level 0-addr :  free prefixes = S1 - n1          ; slots S0 = (S1 - n1) * 2^w
```
Worked example E: 20-bit instruction, w = 5. 3-address opcode = 20 − 15 = 5 bits → S3 = 32. Use n3 = 20.
S2 = (32 − 20)·32 = **384**. Use n2 = 300 → S1 = (384 − 300)·32 = **2688**. Use n1 = 2000 → S0 = (2688 − 2000)·32 = **22016** zero-address opcodes.
(Each step equals the cake formula: e.g. a 2-address opcode is 10 bits, 2¹⁰ − 20·2⁵ = 1024 − 640 = 384.)

Remember: the chain method *requires* that the operand field being re-used is exactly of width w and that remaining 3-address opcodes are all
extended. If only *some* free prefixes are extended, count by the cake formula.

#### 6.4.11 Mixed register files (integer and floating-point registers of different widths)
A field naming one of 8 integer registers is 3 bits, one of 32 floating-point registers is 5 bits. Operand bits differ per type, hence opcode
lengths differ. Worked example F: 16-bit instructions, 8 integer registers (3 bits), 32 FP registers (5 bits).
- T1: 3 integer registers → 9 bits → o = 7, assigned 12.
- T2: 2 FP registers → 10 bits → o = 6, assigned 12.
- T3: 1 integer + 1 FP register → 8 bits → o = 8, assigned 20.
- T4: 1 FP register → 5 bits → o = 11. Maximum T4 opcodes = 2¹¹ − 12·2⁴ − 12·2⁵ − 20·2³ = 2048 − 192 − 384 − 160 = **1312**.

#### 6.4.12 Opcode-space problems that look different
- A separate **addressing-mode field** or **unused field** is just another fixed box: subtract it before computing the opcode width.
  ("Maximum opcodes per addressing mode" with a mode field of m bits means the opcode field is L − m − (registers) − (immediate) bits wide; see also
  [`../02-ADDRESSING-MODES/`](../02-ADDRESSING-MODES/).)
- A format bit (§6.3) is a 1-bit prefix: it halves the cake into two independent halves.
- If the question wants the **total** number of distinct instructions possible, add the maximum for each type only if the types are in separate halves of the cake;
  otherwise use the fraction rule.

### 6.5 Instruction length versus memory size

- **Address field width** = ⌈log₂ (number of addressable locations)⌉. A 64 K-word memory (word-addressable) needs 16 address bits; 1 MB byte-addressable needs 20.
- **Does the instruction fit?** A one-address instruction in a 24-bit word with a 16-bit address leaves 24 − 16 = 8 bits for the opcode (up to 256 opcodes, with no mode or register fields).
  A two-address instruction with two 16-bit addresses needs 32 bits for addresses alone — it cannot fit in a 24-bit word without being split over several words.
- **Variable-length (multi-word) instructions:** an instruction with a memory operand = 1 word + 1 extra word per full address. Program size = Σ words; the PC advances by the instruction's length;
  instruction fetches per instruction = its word count.
- **PC-relative branch range:** a w-bit signed offset reaches −2ʷ⁻¹ … 2ʷ⁻¹−1 *units* from the (updated) PC. If the unit is an instruction word of 4 bytes, w = 12 gives −8192 … +8188 bytes.
- **PC width** = address-space bits.

### 6.6 Summary table of encoding rules

| Question asks | Compute |
|---|---|
| bits to name n objects | ⌈log₂ n⌉ |
| max immediate bits | L − opcode − Σ register fields − other fixed fields |
| max registers (at least w imm bits) | 2^⌊(L − opcode − w)/(#reg fields)⌋ |
| program size, byte-aligned | N × ⌈b/8⌉ |
| opcode bits with format bit, equal split | 1 + ⌈log₂(n/2)⌉ (= ⌈log₂ n⌉) |
| opcode bits with format bit, unequal split | 1 + ⌈log₂(larger type)⌉ |
| max opcodes of target T | ⌊2^(o_T) − Σ n_i 2^(o_T − o_i)⌋ |
| 3→2→1→0-address chain | S_{k+1} = (S_k − n_k)·2^w |

---

## 7. Register pressure and spilling  (**LOW–MEDIUM; 2013 entries — read the data-limitation warning**)

> **Data limitation.** The two 2013 questions in the mapping (spill count with only two registers and code motion; minimum registers with no
> spill) refer to "this code segment", **but the code segment is not printed in the mapping text** (the mapping stores only the question stems).
> It is present in the original paper (and in the noisy text extraction of it), but this repository's mapping file alone cannot be used to solve
> them, and no official answer is asserted anywhere in these notes. What follows teaches the *method* and applies it to an original code segment.

### 7.1 Concepts
- A value is **live** at a program point if it may still be read later without being re-computed. A variable defined but never used again is **dead**.
- **Register pressure** at a point = number of values simultaneously live.
- If at some point more values are live than there are registers, at least one live value must be kept in memory: it is **spilled**
  (`STORE` it, later `LOAD` it back before use).
- **Interference graph:** vertices = variables; an edge when two variables are live at the same time. The minimum number of registers needed with no spill
  = chromatic number of this graph. For **straight-line code** it equals the **maximum register pressure** (the graph is an interval graph).
  With branches it can exceed the maximum pressure; build the graph.
- Dead-after-use sharing: in `d = a + b` where `a` dies at this instruction, `d` may reuse `a`'s register ("each instruction has at most two source operands
  and one destination" lets the destination coincide with a source).

### 7.2 Procedure
1. Write the instructions in order; mark each variable's *last use* (variables stated to be dead after the segment have no further use).
2. For each program point list the live set (work backwards from the end: live-in = (live-out − defined) ∪ used).
3. Registers needed = max over points of max(|live-in|, |live-out|) for straight-line code (this already allows the destination to take a dying source's register).
4. **Code motion** (reordering independent statements, preserving dependencies) can lower the maximum pressure: move a definition as late as possible
   (closest to its use), move a use as early as possible.
5. With k registers and pressure P > k somewhere, at least P − k values must be in memory at that point ⇒ at least one spill when P > k. The *exact* minimum number of
   spills depends on the machine model (whether a spilled value must be stored once, reloaded each use, etc.); state the model.

### 7.3 Worked example (original)
Statements (constants are materialised into registers; `e` is the only value live at the end):
```
original:                 after code motion (still correct):
1: a = 1                  1: a = 1
2: b = 2                  2: b = 2
3: c = 3                  3: d = a + b
4: d = a + b              4: c = 3
5: e = d * c              5: e = d * c
live after 3: {a,b,c}     live after 2: {a,b}   after 3: {d}   after 4: {d,c}   after 5: {e}
max pressure 3            max pressure 2
```
Original order needs **3 registers**; moving `c = 3` down to just before its use makes **2 registers** enough (verified by interference-graph colouring and by
trying all dependency-respecting orders). With only two registers, the original order must spill at least one value; the reordered code needs no spill.

### 7.4 Worked example with live-in values (original)
`a` and `b` are in registers at entry; `t` is the result; everything else is dead after the segment.
```
p = a + b        live after: {a,b,p}         <- 3 live
q = a - b        live after: {p,q}
r = p * q        live after: {p,q,r}         <- 3 live
s = p + r        live after: {q,s}
t = q * s        live after: {t}
```
Maximum pressure 3 ⇒ **3 registers**; with 2 registers a spill is unavoidable (no reordering helps: the dependencies fix the order).

### 7.5 Optional: registers needed for an expression tree (Sethi–Ullman idea)
For an expression tree evaluated with register operands, give each leaf label 1; for an operator with children labels l, r the label is max(l, r) if l ≠ r, else l + 1.
The root label = registers needed with no spill when the larger subtree is evaluated first. Examples: (A+B)·(C+D) → 3; ((A+B)·(C+D))·((E+F)·(G+H)) → 4.
The same number is the maximum **stack depth** needed by a stack machine that evaluates the bigger subtree first (§4).

---

## 8. CPU performance basics that belong with the ISA

### 8.1 The iron law (**memorise**)
```
CPU time = Instruction count (IC)  x  CPI  x  clock period T  =  IC x CPI / f
```
- IC: instructions *executed* (dynamic), not instructions in the program text.
- CPI: average clock cycles per instruction. For a mix, **CPI = Σ fᵢ × CPIᵢ**, where fᵢ are the fractions of *instructions* (not of time).
- f = clock frequency, T = 1/f. Convert: 1 GHz ⇒ T = 1 ns.

Derivation: time = cycles × T; total cycles = Σ ICᵢ × CPIᵢ = IC × (Σ fᵢ CPIᵢ) = IC × CPI.

Worked example 8-a. 8×10⁸ instructions, mix 40 % CPI 1, 30 % CPI 2, 20 % CPI 3, 10 % CPI 6, f = 2 GHz.
CPI = 0.4 + 0.6 + 0.6 + 0.6 = **2.2**. Time = 8×10⁸ × 2.2 / 2×10⁹ = **0.88 s**.

### 8.2 MIPS
```
MIPS = IC / (execution time x 10^6) = f / (CPI x 10^6)
```
Above: MIPS = 2000 / 2.2 ≈ 909.1. **MIPS cannot compare machines with different ISAs** because one ISA instruction can do more work than another.
A machine with a smaller MIPS can finish the same program sooner if its IC is lower.

Worked example 8-b. Machine A: 1000 MIPS but needs 3×10⁹ instructions → 3 s. Machine B: 400 MIPS and needs 0.8×10⁹ → 2 s. B is faster, by 1.5×,
despite its lower MIPS rating.

### 8.3 Comparing machines with different ISAs
Compute each time with the iron law, then take the ratio. Worked example 8-c: program on machine R: 9×10⁸ instructions, CPI 1.1, f = 3 GHz → T_R = 0.33 s.
Machine C: 3×10⁸ instructions, CPI 4.0, f = 2 GHz → T_C = 0.60 s. Speedup of R over C = 0.60/0.33 ≈ **1.82**.

### 8.4 The ratio method (when absolute IC is not given)
Same program, same ISA ⇒ IC cancels. Then

```
T2/T1 = (CPI2/CPI1) x (f1/f2)      ==>      f2 = f1 x (CPI2/CPI1) / (T2/T1)
```
Worked example 8-d. Processor 2 runs the program in 20 % less time with 50 % higher CPI than processor 1 (same ISA); f1 = 2 GHz.
f2 = 2 × 1.5 / 0.8 = **3.75 GHz**. (Check: higher CPI needs a higher clock to still win.)

### 8.5 Amdahl's law (brief)
If a fraction p of the **original execution time** is accelerated by factor s:
```
speedup = 1 / ( (1 - p) + p/s )         limit as s -> infinity : 1/(1-p)
```
p=0.6, s=4: 1/(0.4 + 0.15) = 1.818; limit 2.5.
**p must be a fraction of time, not of instruction count.** When the improvement is expressed through CPI with IC and f fixed, use the CPI ratio:
FP instructions 25 % of instructions with CPI 4, others CPI 1.5 ⇒ CPI = 0.25·4 + 0.75·1.5 = 2.125; improving FP CPI to 2 ⇒ 0.5 + 1.125 = 1.625;
speedup = 2.125/1.625 ≈ **1.308**.

### 8.6 Prerequisite / bridge — memory stalls and pipelines (owned elsewhere)
- Cache misses add stall cycles: **CPI = CPI_base + (memory references per instruction) × miss rate × miss penalty (cycles)**. Example: base 1.5, 1.3 references per instruction
  (1 fetch + 0.3 data), miss rate 4 %, penalty 50 cycles ⇒ 1.5 + 1.3·0.04·50 = **4.1**. Full treatment: [`../05-MEMORY-INTERFACING-AND-HIERARCHY/01-PERFORMANCE/`](../05-MEMORY-INTERFACING-AND-HIERARCHY/01-PERFORMANCE/).
- Pipelined machines: k-stage ideal pipeline, N instructions ⇒ (k + N − 1) cycles; CPI_pipelined = 1 + average stall cycles. See
  [`../07-INSTRUCTION-PIPELINING/`](../07-INSTRUCTION-PIPELINING/) and [`../08-PIPELINE-HAZARDS/`](../08-PIPELINE-HAZARDS/).

### 8.7 How ISA decisions move the three terms

| ISA decision | IC | CPI | T |
|---|---|---|---|
| Powerful memory-operand instructions (CISC) | ↓ | ↑ | may ↑ (complex decode) |
| Load–store, fixed length (RISC) | ↑ | ↓ | ↓ (simple stages) |
| More registers | ↓ (fewer spills) | ↓ | possibly slower register file |
| Longer instructions / more addressing modes | ↓ | ↑ | ↑ |
| Better compiler | ↓ | – | – |

---

## 9. Endianness and alignment (practice-driven, LOW)

- A **byte-addressable** memory stores one byte per address. A multi-byte word occupies consecutive addresses and the question is *which byte comes first*.
- **Big-endian:** the most significant byte (MSB) is at the lowest address. **Little-endian:** the least significant byte (LSB) at the lowest address.

```
value 0x12345678 stored at address 1000:
address         1000  1001  1002  1003
big-endian       12    34    56    78
little-endian    78    56    34    12
```
The word's address is the address of its lowest-addressed byte in both cases. Reading the same four bytes with the other convention gives the byte-reversed value:
bytes AA BB CC DD at 2000…2003 read as a little-endian word = 0xDDCCBBAA; as big-endian = 0xAABBCCDD.
For a 64-bit value 0x0102030405060708 at 1000, address 1005 holds 0x06 (big-endian) or 0x03 (little-endian).

- **Alignment:** a word of 2ᵏ bytes is *aligned* if its address is a multiple of 2ᵏ (address 1002 is not 4-byte aligned: 1002 mod 4 = 2). Strict ISAs fault or are slow on misaligned
  accesses; compilers pad structures. Endianness and alignment rules are part of the ISA (§1).

---

## 10. PYQ patterns (concept and method only — no official answers)

(Years refer to entries in the mapping; see [`PYQ.md`](PYQ.md) for the table and the mapping noise.)

| # | Pattern | Recognise | Recipe | Trap |
|---|---|---|---|---|
| P1 | **Maximum immediate bits** (2016 CS-2 Q10, 2025 CS-1 Q37, related existing practice Q4/Q10) | "k instructions, r registers, L-bit word, opcode + registers + immediate" | §6.1 : ⌈log₂ k⌉, ⌈log₂ r⌉ per register field, subtract | Count the register fields **in the instruction shown**; non-power-of-two counts need ⌈ ⌉ |
| P2 | **Byte-aligned program size** (2016 CS-2 Q31) | "stored in memory in a byte-aligned fashion … program of N instructions" | §6.2 : bits per instruction → ⌈b/8⌉ bytes → × N | Round per instruction, not on the total |
| P3 | **Format-bit R/I types, size of unused / opcode / immediate** (2024 CS-2 Q61) | two formats, "1 bit distinguishes the type", equal division | §6.3 | Opcode field *includes* the format bit; equal split ⇒ equals ⌈log₂ total⌉ |
| P4 | **Max opcodes left for a type** (2020 CS Q44, 2026 CS-2 Q44; related, filed elsewhere: 2018 Q51, 2024 CS-2 Q57) | "variable-sized/expanding opcodes", some opcodes of other formats used | §6.4 cake rule | Mixing opcode lengths; forgetting the floor; subtracting counts from the wrong unit |
| P5 | **Load–store sequence for an assignment** (2026 CS-1 Q15) | candidate instruction sequences; dest-first operand convention | §4.4 four-question test | An ALU instruction with a memory operand is not load–store; operand order of STORE |
| P6 | **What an address field can specify** (2015 CS Q22) | statements about memory operand / register / implied accumulator | §3 : explicit vs implied | An implied register is not named by a field |
| P7 | **Min registers / min spills for a code segment** (2013, 2 distinct questions) | code segment + number of registers + allowed optimisation | §7 liveness procedure | Code segment is missing in the mapping; spill count depends on model |
| P8 | RISC characteristics, ISA membership, iron-law ratio, CPI with stalls (filed under other leaves) | statements about RISC; "part of ISA"; relative time/CPI/frequency | §5, §1, §8.4, §8.6 | MIPS ≠ performance across ISAs; frequency is not ISA |

---

## 11. Traps and misconceptions

1. **Bits vs count:** "64 registers" needs 6 bits per register field, not 64.
2. **⌈log₂⌉ forgotten** for non-powers of two (24 → 5, 40 → 6, 90 → 7).
3. **Wrong number of register fields** — take it from the instruction shown (`ADD R1, #25` has one).
4. **Per-program rounding** for byte alignment instead of per-instruction.
5. **Unequal split + format bit**: size the shared field for the larger type.
6. **Expanding-opcode arithmetic in the wrong unit:** subtract `n_i × 2^(o_T − o_i)`, not `n_i`.
7. **Floor each type separately** instead of summing fractions first (example D in §6.4.9).
8. **Using the chain recursion when only some prefixes are extended** — use the cake rule.
9. **Counting the new opcode length as full L:** opcode = L − operand bits of that type, not L − 3w always.
10. **Accumulator machine forgetting the temporary:** two live intermediates need a `STORE` + memory operand.
11. **Stack machine with a repeated variable:** pushes once per occurrence (no `DUP` unless offered).
12. **Load–store: memory operand inside an ALU instruction**, or wrong operand order of `STORE`.
13. **MIPS is not performance** across ISAs; IC and CPI both matter.
14. **Frequency, cache size, pipeline depth are not part of the ISA.**
15. **Endianness:** the word's address is the lowest byte's address in both orders; only the byte placement changes.
16. **Two-address destination:** the destination is also a source and is overwritten — copy an input first, unless the question permits overwriting.

---

## 12. Edge cases and assumptions to state

- Opcode length for a single fixed field = ⌈log₂ k⌉; with k = 1 it is 0 bits.
- "Instruction types" vs "distinct instructions/opcodes" — if the question counts *types* but formats allow several opcodes each, re-read.
- Every encoding is assumed fully usable (no reserved/illegal patterns) and decodable by prefix.
- Register-file / memory-operand assumptions in §4 (inputs must not be overwritten; whether the destination can be scratch; unlimited temporaries).
- Whether instruction fetches count as "memory accesses" in a counting question.
- Byte vs word addressability for address-field width and PC increments.
- Immediate signedness (§6.1).
- Alignment unit for program size (byte, 2-byte, word).

---

## 13. Connections to other COA topics

- **Addressing modes** reinterpret the operand fields counted here (immediate, register, direct, indirect, indexed, relative) → [`../02-ADDRESSING-MODES/`](../02-ADDRESSING-MODES/).
- **Control unit** decodes the opcode bits sized in §6 and sequences the micro-steps of §2.2 → [`../04-DESIGN-OF-CONTROL-UNIT/`](../04-DESIGN-OF-CONTROL-UNIT/).
- **Pipelining/hazards:** fixed-length, load–store RISC instructions allow a regular IF-ID-EX-MEM-WB pipeline; data hazards are about the register fields (RAW/WAR/WAW)
  → [`../07-INSTRUCTION-PIPELINING/`](../07-INSTRUCTION-PIPELINING/), [`../08-PIPELINE-HAZARDS/`](../08-PIPELINE-HAZARDS/).
- **Memory hierarchy:** CPI with memory stalls → [`../05-MEMORY-INTERFACING-AND-HIERARCHY/01-PERFORMANCE/`](../05-MEMORY-INTERFACING-AND-HIERARCHY/01-PERFORMANCE/).
- **ALU:** executes the ALU instructions → [`../03-ARITHMETIC-AND-LOGIC-UNIT/`](../03-ARITHMETIC-AND-LOGIC-UNIT/).
- **Digital logic number representation:** immediates and offsets are two's-complement → [`../../02-DIGITAL-LOGIC/03-NUMBER-REPRESENTATION-AND-ARITHMETIC/`](../../02-DIGITAL-LOGIC/03-NUMBER-REPRESENTATION-AND-ARITHMETIC/).
- **Compiler design:** register allocation and spilling → [`../../07-COMPILER-DESIGN/`](../../07-COMPILER-DESIGN/).

---

## 14. Existing practice coverage map

File: [`practice.md`](../../14-PRACTICE-QUESTIONS/TOPIC-WISE/03-COMPUTER-ORGANIZATION-ARCHITECTURE/01-INSTRUCTION-SET/practice.md). (Q# → section → skill.)

| Q# | Section | Skill |
|---|---|---|
| 1 | §4.2, §4.4 | data-memory references of a load–store assignment |
| 2 | §3.2 | explicit addresses of a one-address instruction |
| 3 | §9 | little-endian byte placement |
| 4 | §6.1 | leftover immediate bits |
| 5 | §8.1 | weighted CPI |
| 6 | §4.2 | stack-machine instruction count |
| 7 | §5.2 | RISC characteristics |
| 8 | §4.2 (2-address rule) | 2-address destructive operations; **note the "may the destination be used as scratch?" assumption** |
| 9 | §6.1 | opcode bits for fixed-length field |
| 10 | §6.1 | max immediate with register fields |
| 11 | §6.4.3, §6.4.10 | one expanding level |
| 12 | §3.2, §4 | statements about addressing styles |
| 13 | §8.1 | iron law, unit conversion |
| 14 | §6.4.10 | expanding level with spare field |
| 15 | §4.2 (accumulator recursion) | accumulator-machine count with a temporary |
| 16 | §6.1 (reverse), §6.6 | max registers given opcode and minimum immediate |
| 17 | §8.3 | ISA comparison with the iron law |
| 18 | §6.1, §6.4, §6.3 | field-width statements, impossible full encoding |

---

## 15. Self-check

1. Name three things that belong to the ISA and three that do not.
2. State the fetch micro-operations in register-transfer form and say how many memory references an ADD with one memory operand makes.
3. What is the instruction count of `Z = (A+B)*(C+D)` on a stack machine? On a load–store machine? On a 3-address memory machine?
4. Why does an accumulator machine need a temporary for `(A+B)*(C+D)`?
5. Give the four-question test for a load–store sequence.
6. Compute ⌈log₂⌉ of 24, 40, 64, 65.
7. Why is byte-aligned program size N × ⌈b/8⌉ and not ⌈N·b/8⌉?
8. How many opcode bits does a two-type format need when one bit distinguishes the types and the two types are unequal in size?
9. State the cake rule for the maximum number of opcodes of a target type and explain why the floor is needed.
10. How do you convert a 3→2→1-address expanding scheme into the cake rule?
11. What does a register's last use have to do with the minimum number of registers?
12. State the iron law and explain why MIPS cannot rank machines with different ISAs.
