# Microprogrammed Control Unit — Notes

Scope: the second half of the syllabus phrase "Design of control unit – hardwired and microprogrammed". Companion topic: [01-HARDWIRED](../01-HARDWIRED/NOTES.md).

---

## 0. Where this fits

| Item | Detail |
|---|---|
| Syllabus line | "Instruction set and addressing modes. Design of arithmetic and logic unit (ALU). **Design of control unit – hardwired and microprogrammed.** Memory interfacing and hierarchy: … I/O interface (interrupt and DMA). Instruction pipelining, pipeline hazards." |
| Prerequisites | Registers, buses, tri-state / multiplexed bus, ROM, decoder, multiplexer, counters, flip-flops: [Digital Logic – combinational circuits](../../../02-DIGITAL-LOGIC/02-DESIGN-OF-COMBINATIONAL-AND-SEQUENTIAL-CIRCUITS/01-COMBINATIONAL-CIRCUITS/) and [sequential circuits](../../../02-DIGITAL-LOGIC/02-DESIGN-OF-COMBINATIONAL-AND-SEQUENTIAL-CIRCUITS/02-SEQUENTIAL-CIRCUITS/). Instruction formats and what an instruction does: [Instruction Set](../../01-INSTRUCTION-SET/), [Addressing Modes](../../02-ADDRESSING-MODES/). |
| Sibling | [Hardwired control](../01-HARDWIRED/NOTES.md) — the same job (turn an opcode into control signals, step by step) done with fixed logic instead of a stored program. Read both; GATE-style statements compare them. |
| What depends on this | [Instruction pipelining](../../07-INSTRUCTION-PIPELINING/) (why RISC wants simple, single-cycle-per-stage control), [Interrupt](../../06-IO-INTERFACE/01-INTERRUPT/) (register-transfer sequences for interrupt entry look exactly like microroutines), CPU-time / CPI reasoning in [Performance](../../05-MEMORY-INTERFACING-AND-HIERARCHY/01-PERFORMANCE/). |

**Conventions used in this folder:** 1 K = 2¹⁰, 1 M = 2²⁰. Sizes of control stores are counted in **bits** unless stated. Iron law: CPU time = IC × CPI × clock period = IC × CPI / f. `⌈x⌉` is ceiling.

---

## 1. Evidence snapshot (read this first, it tells you how hard to study each part)

**PYQ evidence for this exact leaf: none mapped.** The mapping file for this topic says no question was identified ([questions.md](../../../13-PYQ-TOPIC-MAPPING/03-COMPUTER-ORGANIZATION-ARCHITECTURE/04-DESIGN-OF-CONTROL-UNIT/02-MICROPROGRAMMED/questions.md)). A keyword search of the text-extractable 2013–2026 papers found no microprogram / microinstruction / control-word / control-store text either (details and limits in [PYQ.md](PYQ.md)). The 2007–2012 papers are scanned and could not be searched. So depth here is **syllabus-driven** (the topic is named on the official syllabus) plus the skills in the existing 12-question practice file. It is **not** driven by any observed PYQ frequency.

Two *adjacent* items exist in other folders (not answered here): a hardwired-vs-RISC-design-characteristics question is mapped to the hardwired sibling, and a "read a sequence of micro-operations" question family is mapped to the interrupt topic. They are the closest real exam contact; both are covered in spirit by Sections 3, 5 and 10.

| Section | Rating | Why |
|---|---|---|
| 2–3 Control memory, microinstruction, CAR, fetch routine | **MEDIUM (syllabus + practice Q1, Q3, Q10)** | Definitions are the only way conceptual MCQ/MSQ on this topic can be set. |
| 4 Micro-operation listings (fetch, ADD, LOAD, branch) | **MEDIUM** | Needed to read micro-operation sequences; the closest adjacent real PYQ family. |
| 5 Formats: horizontal / vertical / field-encoded; width | **HIGH (syllabus + practice Q2, Q4, Q5, Q6, Q9, Q11)** | Most of the existing practice questions are width arithmetic. |
| 6 Sequencing and next-address logic | **MEDIUM (practice Q8, Q10)** | Absolute address field range, mapping ROM, conditional branch, increment. |
| 7 Control-store size | **HIGH (practice Q3, Q7, Q9, Q11)** | Direct numeric problems: words × width, CAR bits. |
| 8 Timing, CPI, hardwired comparison | **MEDIUM (practice Q12, Q6)** | One timing problem + comparison statements. |
| 9 Nanoprogramming, writable control store | **LOW–MEDIUM (user-requested depth, no practice question)** | Included for completeness of "microprogrammed"; not tied to a practice item. |

---

## 2. The idea in one picture

A CPU's datapath (registers, ALU, buses) is a set of switches: "put PC on the bus", "load MAR", "ALU adds", "memory read". To execute one machine instruction, you must turn the right switches on, in the right order, one **step** at a time.

- **Hardwired control:** a pile of gates computes "which switches are on at step *t* for opcode *x*".
- **Microprogrammed control:** *write the switch settings in a table* and read the table row by row. Each row (a **microinstruction**) says which switches to turn on in this step and which row to read next. The table lives in a small, fast, read-only memory. The control unit becomes a tiny computer inside the computer: the "program" is the table, the "program counter" is a small register, and the "instructions" are rows of control bits.

Analogy: a music box (rows of pins on a drum = control store; the rotating drum position = micro-PC; each pin row plucks a set of notes at once = a set of control signals). Replace the drum and you get a different tune without rebuilding the box. That is the flexibility argument.

---

## 3. Terminology and organisation

### 3.1 Vocabulary (the convention used in these notes)

| Term | Meaning |
|---|---|
| **Control signal** | One wire that enables something: a register load (`MARin`), a bus driver (`PCout`), an ALU function, a memory read/write. |
| **Micro-operation** | One elementary register-transfer or ALU action, e.g. `MAR ← PC`. Several micro-operations that are compatible happen in the **same step**. |
| **Microinstruction** | One row of the control store: all control signals asserted in one step **plus** the information needed to choose the next microinstruction. |
| **Control word** | The control-signal part of a microinstruction. (Books differ: some call the whole row the control word. If a question gives widths of "control word" and "next-address field" separately, add them.) |
| **Microroutine / microprogram** | The sequence of microinstructions that implements one machine instruction (or the shared fetch). The whole contents of the control store is the microprogram. |
| **Control memory / control store (CS)** | The (usually ROM) holding microinstructions. It is **internal to the CPU**, not part of the program-visible address space, and not main memory. |
| **CAR / micro-PC (µPC)** | Control Address Register: holds the control-store address of the microinstruction being read. Width = ⌈log₂ (number of CS words)⌉. |
| **CDR / microinstruction register (µIR)** | Control Data Register: latches the microinstruction just read; its bits drive the datapath. |
| **Mapping ROM / opcode decoder** | Converts the opcode in IR into the starting CS address of that instruction's microroutine. |
| **Sequencer** | The logic that computes the next CAR value (increment, load jump address, map, return). |
| **Microcycle** | Time to read and execute one microinstruction. |

Do not confuse **micro-operation** (what happens) with **microinstruction** (the stored row, which carries several micro-operations).

### 3.2 Organisation

```
                    +-------------------+
   IR.opcode ------>|   Mapping ROM     |---+
                    +-------------------+   |
                                            v
  status flags --> +---------+   +------------------------------+
  (ZF, CF, ...)    |condition|   |   Next-address MUX / logic   |<-- return addr (SBR)
                   | select  |-->|  CAR+1 | addr field | MAP | RET|<-- addr field (from CDR)
                   +---------+   +--------------+---------------+
                                                |
                                                v
                                         +-------------+
                                         |     CAR     |  (micro-PC)
                                         +------+------+
                                                | address
                                                v
                                    +------------------------+
                                    |  Control store (ROM)   |   N words × W bits
                                    +-----------+------------+
                                                | W bits
                                                v
                                         +-------------+
                                         |     CDR     |  (microinstruction register)
                                         +------+------+
        +--------------------+------------------+--------------------+
        | signal fields      | (decoders if     | next-address info  |
        v                    v  encoded)        v  (cond sel, addr)  |
   datapath control lines  ----------------> to the MUX/logic -------+
```

One microcycle: CAR → read CS → CDR → (decode) → datapath acts, and in parallel the next-address logic forms the new CAR.

### 3.3 One machine instruction = fetch routine + execute routine

All instructions share one **fetch microroutine** at a fixed CS address (say 0). Its last microinstruction uses the **MAP** next-address mode: the CS address of the right execute routine is produced from the opcode now sitting in IR. Each execute routine ends with a jump back to the fetch address.

```
  CS address 0:  F0 -> F1 -> F2 --MAP(opcode)--+--> ADD routine  ----+
                 ^                             |--> LOAD routine ---+|
                 |                             |--> STORE routine --+|
                 |                             +--> BZ routine -----+|
                 +---------------- jump to 0 <------------------------+
```

Why shared? Fetch is identical for every instruction; storing it once saves control-store words (Section 7).

---

## 4. Reference machine "Mini-1" and micro-operation listings

All worked examples in Sections 5–8 use this machine so numbers stay consistent.

**Datapath (single internal bus):**

```
   Drive the bus (xxout):  PC, MDR, T, IR(addr/offset field), R0..R3   (one at a time)
   Load from the bus (xxin): PC, MAR, MDR, IR, A, R0..R3
   ALU:  T ← A op bus  (op = ADD, SUB, AND)   or   T ← bus + 1 (INC)
   Tin latches the ALU output into T and updates ZF (zero flag)
   Memory: word-addressed, one word = one instruction/datum. MAR holds the address.
```

- Exactly **one** source may drive the bus per step; several registers may load from the bus in the same step.
- `Read`: memory delivers `M[MAR]` into MDR; assumption (stated, as every exam question must): **memory finishes within one microcycle**, so MDR is valid from the *next* step. Slower memory adds wait microinstructions (Section 8.4).
- IR format: opcode (2 bits), register field, address/offset field. Register names `R1`, `R2` are written literally below for readability; in a real design the register select comes from IR fields, so one routine serves every register choice.
- Opcodes: `00` ADD, `01` LOAD, `10` STORE, `11` BZ (branch if zero).

**Control signals:** bus sources `PCout, MDRout, Tout, IRout, R0out..R3out` (8); bus destinations `PCin, MARin, MDRin, IRin, Ain, R0in..R3in` (9); `Tin`; ALU function (`ADD, SUB, AND, INC`); memory `Read, Write`.

### 4.1 Micro-operation listings (one row = one microinstruction = one step)

**Fetch (shared)**

| Step | Micro-operations | Signals asserted | Next |
|---|---|---|---|
| F0 | MAR ← PC; start read; T ← PC + 1 | `PCout, MARin, Read, INC, Tin` | +1 |
| F1 | PC ← T | `Tout, PCin` | +1 |
| F2 | IR ← MDR | `MDRout, IRin` | MAP(opcode) |

F0 shows why a microinstruction carries several micro-operations: `MARin` (loads from the bus) and `Tin` (loads the ALU output) are compatible and happen together. F1 cannot merge into F0 (it needs T, which is only valid after F0), and cannot merge with F2 (both want to drive the bus).

**ADD R1, R2** (R1 ← R1 + R2)

| Step | Micro-operations | Signals | Next |
|---|---|---|---|
| A0 | A ← R1 | `R1out, Ain` | +1 |
| A1 | T ← A + R2 | `R2out, ADD, Tin` | +1 |
| A2 | R1 ← T | `Tout, R1in` | JUMP 0 |

**LOAD R1, addr** (R1 ← M[addr])

| Step | Micro-operations | Signals | Next |
|---|---|---|---|
| L0 | MAR ← IR.addr; start read | `IRout, MARin, Read` | +1 |
| L1 | R1 ← MDR | `MDRout, R1in` | JUMP 0 |

**STORE R1, addr** (M[addr] ← R1)

| Step | Micro-operations | Signals | Next |
|---|---|---|---|
| S0 | MAR ← IR.addr | `IRout, MARin` | +1 |
| S1 | MDR ← R1 | `R1out, MDRin` | +1 |
| S2 | write memory | `Write` | JUMP 0 |

**BZ offset** (if ZF = 1 then PC ← PC + offset). PC was already incremented during fetch.

| Step | Micro-operations | Signals | Next |
|---|---|---|---|
| B0 | A ← PC (harmless if branch not taken) | `PCout, Ain` | if ZF = 0 JUMP 0 else +1 |
| B1 | T ← A + IR.offset | `IRout, ADD, Tin` | +1 |
| B2 | PC ← T | `Tout, PCin` | JUMP 0 |

B0 does useful work *before* the decision: loading A is harmless if the branch is not taken, so the not-taken path costs only 1 microinstruction.

**Microinstruction counts (fetch included):** ADD 3 + 3 = 6; LOAD 3 + 2 = 5; STORE 3 + 3 = 6; BZ taken 3 + 3 = 6; BZ not taken 3 + 1 = 4.

### 4.2 Control-store layout (compact, using a mapping ROM)

```
 CS addr  0  1  2 | 3  4  5 | 6  7 | 8  9 10 | 11 12 13      14 words
          F0 F1 F2 | A0 A1 A2| L0 L1| S0 S1 S2 | B0 B1 B2
 Mapping ROM (4 entries): 00 -> 3,  01 -> 6,  10 -> 8,  11 -> 11   (each entry 4 bits)
 Jump target "0" = fetch.
```

### 4.3 Reading a micro-operation sequence (skill)

1. Read each row as one time step.
2. Note which register drives the bus and which load.
3. Ask what the sequence *achieves* by composing the transfers. Original example: `MDR ← R2; MAR ← IR.addr; M[MAR] ← MDR` is a store of R2 (compare with Mini-1 STORE). `MAR ← PC; MDR ← M[MAR]; IR ← MDR; PC ← PC + 1` is an instruction fetch. For any list, track what is read from memory, what is written to memory, and whether PC is merely incremented or overwritten.
4. Check legality: one bus source per step (single-bus machine); a value is used only after it was produced in an *earlier* step (or, in the same step, only as the **old** value of a parallel transfer).
5. Decide what the question really asks: *which kind of operation* (fetch, operand fetch, branch, interrupt entry) or *which signals* are asserted. For "which operation", identify the registers that are read from and written to memory and where the PC goes.

---

## 5. Microinstruction formats and width

### 5.1 Horizontal

One bit per control signal (or per elementary action). Several bits can be 1 at once, so many micro-operations run in parallel. No (or almost no) decoding between CDR and the datapath.

```
 | PCout | MDRout | Tout | IRout | R0out .. R3out | PCin | MARin | ... | Tin | ADD | SUB | AND | INC | Read | Write | seq | addr |
```

- Width ≈ (number of control signals) + sequencing bits.
- Pros: fastest (CDR bits drive the wires), maximum parallelism, short microprograms.
- Cons: very wide control store (expensive in ROM bits), hard to read and to modify, most bits are 0 in any word (low information density).

### 5.2 Vertical (fully encoded)

Signals are encoded into a few binary fields (like a machine-language opcode); decoders expand them. In the extreme, one field names *one* micro-operation, so each microinstruction does one thing.

- Width is small, microprograms are **longer** (more microinstructions, since one word does less), and every microinstruction pays a **decoder delay**.
- Pros: narrow control store words, easy to read. Cons: slower, less parallelism, extra decoder hardware.

### 5.3 Hybrid / field-encoded (what real designs and most exam problems use)

Partition the signals into **groups (fields)**. Signals inside a group are *mutually exclusive* (never needed in the same step) and are encoded together; groups are independent, so parallelism *between* groups is kept. A **single-signal group costs 1 bit** (it is the horizontal case).

```
 | bus-source (4) | bus-dest (4) | ALU (2) | mem (2) | Tin (1) | seq (2) | next-addr (CAR bits) |
```

Spectrum: **horizontal** (no encoding) ⟷ **field-encoded** ⟷ **vertical** (one field). More encoding → narrower store, slower microcycle (decode), less parallelism, more microinstructions.

### 5.4 Bits needed for one encoded field

If a field selects **one of n** alternatives:

```
 always exactly one chosen :  ⌈log₂ n⌉ bits
 may also choose "none"    :  ⌈log₂ (n + 1)⌉ bits
```

Why: a b-bit field has 2ᵇ codes; you need n (or n + 1) distinct codes, so 2ᵇ ≥ n (or n + 1).

**Worked example 1 (verified).** Number of bits for a group of n signals, at most one asserted, "none" allowed:

| n | codes needed (n+1) | bits |
|---|---|---|
| 1 | 2 | 1 |
| 7 | 8 | 3 |
| 8 | 9 | **4** (not 3: 8 codes would leave no code for "none") |
| 15 | 16 | 4 |
| 16 | 17 | **5** |

Without "none" (exactly one is always chosen): n = 8 → 3 bits; n = 5 → 3 bits.

*When is "none" needed?* If, in some microinstruction, the group would not be used (no source drives the bus, no register loads), there must be a code meaning "nothing". If a signal is already gated by a separate enable (in Mini-1, the ALU function does nothing unless `Tin` is asserted), the ALU function field can be the plain ⌈log₂ 4⌉ = 2 bits. Always read the question: it states whether "none" is a choice.

### 5.5 Which signals may share a field?

Two signals may be put in the same group **iff no microinstruction ever asserts both**. Build a *conflict graph* (edge = "are asserted together in some step"); a group must be an independent set; the minimum number of groups is a graph-colouring problem. Total bits = Σ over groups ⌈log₂ (size + 1)⌉.

**Worked example 2 (verified by brute force).** Six signals A–F. Steps assert these pairs together: AD, BD, CE, AF, BE, CF.

```
 Conflict edges: A-D, B-D, C-E, A-F, B-E, C-F  (a 6-cycle A-D-B-E-C-F-A)
 Independent sets of size 3: {A,B,C} and {D,E,F}
 Group 1 = {A,B,C}: ⌈log₂ 4⌉ = 2 bits     Group 2 = {D,E,F}: ⌈log₂ 4⌉ = 2 bits
 Total = 4 bits   (horizontal = 6 bits; partition 3+2+1 = 2+2+1 = 5 bits; 2+2+2 = 6 bits)
```

Trap: you may only put signals together if they are *never* simultaneous. Putting A and D into one field would make the pair AD impossible to issue.

### 5.6 Width of a whole microinstruction

```
 W = Σ (signal-field bits) + (sequencing bits) + (next-address bits)
 horizontal : signal bits = number of signals
 encoded    : signal bits = Σ ⌈log₂ (group size + 1)⌉   (or without +1 when no 'none')
```

**Worked example 3: Mini-1 (verified).**

- Bus source: 8 signals + none → ⌈log₂ 9⌉ = **4**
- Bus destination: 9 signals + none → ⌈log₂ 10⌉ = **4**
- ALU function: 4 functions (gated by Tin) → ⌈log₂ 4⌉ = **2**
- Memory: Read, Write, none → ⌈log₂ 3⌉ = **2**
- `Tin`: **1**
- Sequencing mode (INC, JUMP, MAP, JUMP-if-ZF=0): **2**
- Next-address field: CS has 14 words → ⌈log₂ 14⌉ = **4**

```
 W_encoded    = 4 + 4 + 2 + 2 + 1 + 2 + 4 = 19 bits
 W_horizontal = 8 + 9 + 4 (ALU) + 2 (Read, Write) + 1 + 2 + 4 = 30 bits
 Control store: encoded 14 × 19 = 266 bits; horizontal 14 × 30 = 420 bits
 (plus mapping ROM 4 entries × 4 bits = 16 bits)
```

Encoding saves 154 bits (36.7 % of the horizontal 420) for Mini-1's tiny microprogram, at the price of three decoders and a longer microcycle.

---

## 6. Sequencing: how the next microinstruction is chosen

### 6.1 Methods (all feed one next-address MUX)

| Mode | Next CAR | Typical use |
|---|---|---|
| **Increment** | CAR + 1 | straight-line steps (most of the microprogram). |
| **Absolute jump** | address field of the microinstruction | go back to fetch; skip to a shared tail. |
| **Conditional branch** | if (selected status bit) then address field else CAR + 1 | loops, "branch taken?" tests (ZF, carry, sign…). |
| **Mapping** | f(opcode) from mapping ROM or from bit concatenation | entering the execute routine after fetch. |
| **Subroutine call / return** | call: save CAR + 1 in SBR, load address; return: CAR ← SBR | share a microsubroutine such as effective-address computation. |
| **Address modification** | OR/concatenate mode bits into the address | one routine start for each addressing mode, chosen by IR mode bits. |

Remarks for exam use:

- A micro-PC *can* increment, so a microinstruction does **not** need an absolute next address in every word. A design that does require it (every word names its successor) is legal but wide.
- A branch tests a **status bit** (flag). With k testable conditions plus "unconditional", the condition-select field has ⌈log₂ (k + 1)⌉ bits (the extra code means "always/no test"). If a separate unconditional-jump mode exists, k conditions alone may need only ⌈log₂ k⌉; read the format.

### 6.2 Mapping the opcode to a start address

**(a) Mapping ROM.** Indexed by the opcode, outputs a full CS start address. Fully flexible: routines may be any length and anywhere; the CS can be compact. Cost: ROM of 2^(opcode bits) entries × CAR bits, plus one extra ROM delay.

**(b) Concatenation / shift.** Start address = `opcode ‖ 00…0` (shift the opcode left by s bits). Each routine is given a block of 2ˢ words. No mapping ROM, trivial hardware, very fast. Cost: every routine, however short, occupies a full block; routines longer than 2ˢ words must **jump out** to a continuation block; unused blocks waste words.

**Worked example 4 (verified).** A machine has a 4-bit opcode and reserves 8 words per routine (s = 3).

- CAR width for the routine area = 4 + 3 = **7 bits** → 2⁷ = 128 words of address space.
- Longest routine that fits without jumping = 2³ = **8** microinstructions.
- A 9-step routine needs a jump to a shared continuation in the spare area.

**Mini-1 layouts compared (verified).** Mini-1 has 2-bit opcodes and at most 3-word routines. Shift layout with address `1 ‖ opcode(2) ‖ step(2)` uses CS addresses 16–31 for execute routines and 0–2 for fetch:

```
 compact + mapping ROM : 14 words × 19 bits + 16-bit map ROM = 282 bits   (CAR = 4 bits)
 shift layout          : 32 words × 20 bits                   = 640 bits   (CAR = 5 bits; 18 of 32 words unused)
```

Hence "simple and fast mapping" costs about 2.3× more ROM here. For GATE-style questions read which scheme is stated.

### 6.3 Branch-address generation and formats of the sequencing part

| Format | Sequencing bits | Remarks |
|---|---|---|
| **Two-address**: true-address and false-address fields + condition select | 2a + c | Every word can branch; very wide. |
| **One-address + condition select**: next = addr if cond else CAR + 1 | a + c | Common; every word has the address field. |
| **Variable format**: a type bit distinguishes *operate* microinstructions (signal fields, no address; next = CAR + 1) from *branch* microinstructions (condition + address, no signals) | 1 + max(signal bits, c + a) per ROM word | Narrower, but a branch costs an extra microinstruction slot because it cannot also drive signals. |

(a = next-address bits, c = condition-select bits.)

**Worked example 5 (verified).** 18 signal bits, c = 3, a = 7.

```
 One-address format      : 18 + 3 + 7        = 28 bits per word
 Two-address format      : 18 + 3 + 7 + 7    = 35 bits per word
 Variable format         : 1 + max(18, 3+7)  = 19 bits per word
 Saving per word (variable vs one-address) = 28 − 19 = 9 bits
```

The variable format only pays if branches are infrequent enough that the extra branch-only words do not cancel the saving: compare (words × width) for both designs.

### 6.4 Microsubroutines

A microinstruction with mode CALL stores CAR + 1 in the subroutine register SBR, then jumps; the subroutine's last word uses RETURN (CAR ← SBR). Single-level SBR is the common textbook case; nested calls need a stack. One extra microinstruction per call site is paid in both space and time.

**Worked example 6 (verified).** Ten instructions each need the same 5-step address-computation sequence.

```
 inline  : 10 × 5            = 50 words
 shared  : 5 (routine, last word returns) + 10 call words = 15 words
 saved   : 35 words ; cost: +1 microcycle per execution (the call word does no datapath work, assumption)
```

---

## 7. Control-store size

### 7.1 Recipe (do in this order)

1. **Count words N**: shared fetch microinstructions + Σ (microinstructions in each execute routine). Shared fetch is counted **once**, not once per instruction. If a question gives per-instruction counts that *include* fetch, do not add fetch again.
2. **CAR width** = ⌈log₂ N⌉ (if a shift layout, use the layout's address width and its 2^width words).
3. **Next-address field** = CAR width (absolute-address field) unless the question gives it.
4. **Width W** = signal bits (horizontal or Σ encoded fields) + sequencing bits + next-address bits.
5. **Bits** = N × W. Bytes = bits / 8. Add mapping ROM bits (entries × CAR bits) if present.

### 7.2 Worked examples

**Example 7 (verified).** Fetch = 3 words. Five instructions have execute routines of 4, 6, 3, 8, 5 words. Signal field = 24 bits; absolute next-address field.

```
 N = 3 + (4+6+3+8+5) = 29 words
 CAR = ⌈log₂ 29⌉ = 5 bits   (2⁴ = 16 < 29 ≤ 32)
 W = 24 + 5 = 29 bits
 Control store = 29 × 29 = 841 bits = 105.125 bytes (not an integer number of bytes; stay in bits)
```

Trap: the shared-fetch words counted five times would give 4 × 3 extra = 12 extra words and 41 words → 6-bit CAR → different answer.

**Example 8 (field-encoded vs horizontal, verified).** A design has: a 9-signal bus-source group, a 15-signal destination group, an 8-signal ALU group (each group: at most one asserted, "none" allowed); a Read/Write/none memory group (2 signals); 5 independent flag-control signals; 3 testable conditions plus "unconditional" (condition-select field kept in both designs); N = 300 words; absolute next-address field.

```
 groups: ⌈log₂10⌉=4, ⌈log₂16⌉=4, ⌈log₂9⌉=4, ⌈log₂3⌉=2, flags 5
 condition select: ⌈log₂(3+1)⌉ = 2 ; next address: ⌈log₂300⌉ = 9
 W_enc = 4+4+4+2+5+2+9 = 30 bits ; W_hor = 9+15+8+2+5+2+9 = 50 bits
 bits: 300×30 = 9 000 vs 300×50 = 15 000 -> saving 6 000 bits
```

The ALU group (8 signals + none = 9 codes) needs **4** bits, not 3, because 8 is a power of two; the 15-signal group fits exactly in 4 bits (16 codes). Always add the "none" code when "none" is allowed.

### 7.3 Cost / speed of wide vs narrow stores (qualitative, but exam statements rely on it)

- Horizontal: fewer words (more work per word), many more bits per word. Total bits can be larger *or* smaller depending on how many extra words the vertical design needs. **Do not assume vertical is always smaller in total**; compute both (N_v × W_v vs N_h × W_h).
- Vertical: narrower words, more words, plus decoder delay per microinstruction.

---

## 8. Timing, CPI, and comparison with hardwired

### 8.1 Microcycle time

```
 Non-overlapped (read, then decode, then act):
     t_µ = t_CS + t_decode + t_datapath
 Overlapped (CDR latches the word; next word is read while the current one executes):
     t_µ = max(t_CS , t_decode + t_datapath)
```

Overlap breaks down at taken jumps/branches: the word fetched speculatively is wasted, costing about one extra microcycle per taken branch/map/jump (state this assumption if you use it).

**Worked example 9 (verified).** t_CS = 10 ns, t_decode = 2 ns, t_datapath = 12 ns; a machine instruction needs 6 microinstructions.

```
 Non-overlapped: t_µ = 10 + 2 + 12 = 24 ns -> 6 × 24 = 144 ns
 Overlapped    : t_µ = max(10, 14) = 14 ns -> 6 × 14 = 84 ns
 Overlapped, one taken jump (one wasted cycle): (6 + 1) × 14 = 98 ns
 Hardwired reference: 4 clocks of 12 ns = 48 ns -> microprogrammed is slower by 144 − 48 = 96 ns (non-overlapped)
```

### 8.2 Time of a machine instruction and CPI

```
 time(instruction) = (number of microinstructions executed) × t_µ
 CPI (in microcycle clocks) = Σ fᵢ × µᵢ           (fᵢ = instruction frequency, µᵢ = microinstructions incl. fetch)
 CPU time = IC × CPI × t_µ                          (iron law with 1 microinstruction per clock)
```

**Worked example 10: Mini-1 (verified).** Mix: ADD 40 %, LOAD 30 %, STORE 10 %, BZ taken 10 %, BZ not taken 10 %. µ counts from Section 4.1: 6, 5, 6, 6, 4.

```
 CPI = 0.4×6 + 0.3×5 + 0.1×6 + 0.1×6 + 0.1×4 = 2.4 + 1.5 + 0.6 + 0.6 + 0.4 = 5.5 microcycles
 At 10 ns per microcycle: average = 55 ns per machine instruction
```

This is why microprogrammed machines of simple design have CPI well above 1, and why pipelined RISC (CPI near 1) prefers hardwired control ([pipelining](../../07-INSTRUCTION-PIPELINING/)).

### 8.3 Microprogrammed vs hardwired

| Aspect | Hardwired (see [sibling](../01-HARDWIRED/NOTES.md)) | Microprogrammed |
|---|---|---|
| Speed | Fast: signals come straight from logic; clock limited by gate depth | Slower: a control-store access (and decode) every step |
| Flexibility / modification | Rewire / redesign logic | Change ROM contents (or WCS); add instructions by adding routines |
| Design effort & errors | Hard for large, irregular instruction sets (random logic) | Systematic; easier to debug and test |
| Cost / area | Cheap for small, regular ISAs | Needs control store + sequencer; pays off for complex ISAs |
| Typical use | RISC-style, simple fixed-format ISAs, pipelined cores | CISC-style complex instructions; emulation; field patches |
| Complex instruction (string move, etc.) | Many states, large FSM | Just a longer microroutine (or loop) |

Border case: a ROM addressed by (opcode, step counter) that directly outputs control signals is a *hardwired* implementation (the sibling topic explains why); it becomes *microprogrammed* only when the ROM words also carry or imply their own successor and a micro-PC/sequencer steps through them.

These are *tendencies*, not absolutes: many modern CISC cores decode common instructions with hardwired logic and use microcode only for rare, complex ones.

### 8.4 Edge cases in timing

- Slow memory: a Read followed by a "wait" microinstruction that loops until the memory-complete signal arrives, so µ count depends on memory latency (state it).
- Conditional branch not taken costs fewer microinstructions than taken (BZ: 1 vs 3 after fetch).
- If the question says the next microinstruction is fetched only after the current finishes, use the **non-overlapped** formula and ignore overlap.
- Practice-style simplification ("each microinstruction takes the control-store access time") sets t_µ = t_CS; use exactly what the question defines.

---

## 9. Nanoprogramming, writable control store

### 9.1 Two-level control store (nanoprogramming)

Problem: a wide horizontal store with M microinstructions often repeats the **same control patterns** many times. Idea: keep the distinct wide patterns once in a **nanostore** (D patterns × W bits) and let the **microstore** hold only a short **pointer** (⌈log₂ D⌉ bits) per microinstruction (plus sequencing information, which we ignore in the counts below unless given).

```
 CAR -> [ microstore: M words × p bits ] --pointer--> [ nanostore: D words × W bits ] -> datapath
 Flat (single-level)   : M × W
 Two-level             : M × p + D × W        where p = ⌈log₂ D⌉
 Saves bits when       : M × p + D × W < M × W
```

**Worked example 11 (verified).** M = 2048, W = 100, D = 256 distinct patterns.

```
 p = ⌈log₂ 256⌉ = 8
 flat = 2048 × 100 = 204 800 bits
 two-level = 2048 × 8 + 256 × 100 = 16 384 + 25 600 = 41 984 bits   (saves 162 816 bits)
```

**Counter-example (verified):** M = 512, W = 60, D = 500 (almost all patterns distinct): p = 9; two-level = 512×9 + 500×60 = 34 608 > flat 30 720. Nanoprogramming only helps when D ≪ M.

Costs: **two serial memory accesses** per microinstruction (micro then nano), so the microcycle gets longer (if micro access 10 ns and nano access 12 ns and they cannot overlap, the control-store part alone is 22 ns); more hardware complexity. Benefit: small total storage; classic use in some commercial CISC processors.

*Name clash:* "two-level" is also used for field-encoded microinstructions (a decoder level). Nanoprogramming is a second **memory** level, not a decoder.

### 9.2 Writable control store (WCS)

Control store built from RAM (or flash) instead of ROM: microprogram is loaded at start-up; can be patched in the field, extended, or replaced to **emulate** a different ISA; allows user microprogramming on some machines. Costs: volatile (must be reloaded), RAM slower/larger than ROM per bit, security/protection of the control store. Still internal to the CPU: **not** user-addressable main memory.

---

## 10. Question patterns for this topic (syllabus-derived; no PYQ evidence)

These come from the syllabus line and the existing practice file, not from a mapped PYQ. Treat them as probable *shapes*, not as measured frequencies.

| Pattern | Recognise by | Recipe | Trap |
|---|---|---|---|
| Control-memory/CAR width | "N microinstructions", "bits in micro-PC" | CAR = ⌈log₂ N⌉ | N = 2ᵏ + 1 needs k + 1 bits; N = 2ᵏ needs exactly k. |
| Horizontal width | "one bit per signal" + other fields | Σ signal bits + other fields | Forgetting next-address / condition fields. |
| Encoded field | "mutually exclusive", "at most one", "none" | ⌈log₂ (n+1)⌉ or ⌈log₂ n⌉ | Forgetting the "none" code; applying encoding to signals that may be simultaneous. |
| Mixed-format word | table of fields, some encoded, some direct | Sum the **given** bit counts; keep simultaneous signals 1 bit each | Re-encoding what is already counted in bits. |
| Total store | "N words" × "W bits" | N × W; add mapping ROM if asked | Bits vs bytes; counting fetch once per instruction. |
| Saving of encoded vs horizontal | "how many bits does encoding save" | N × (W_h − W_v) | Using different N for the two designs unless told. |
| Absolute next-address range | "k-bit next-address field is the only successor mechanism" | 2ᵏ words addressable | Answering k or 2k. |
| Time compare | µ count × access time vs clocks × period | difference of two products | Adding datapath/decode time when the question defines the microcycle as access time only. |
| Conceptual statements | MCQ/MSQ on horizontal/vertical, mapping ROM, fetch sharing, WCS | Sections 3, 5, 6, 9 | "Control memory is user-addressable" is false. |
| Micro-operation sequence reading | register-transfer list | Section 4.3 | Not noticing bus conflicts or what the sequence composes to. |

---

## 11. Traps and misconceptions

1. **Horizontal ≠ always faster in total or always larger in total.** It is wider per word; vertical needs more words; compute both totals.
2. **Control memory is not main memory** and not part of the user address space.
3. **Micro-operation ≠ microinstruction ≠ machine instruction.**
4. **Fetch is shared** and counted once; each machine instruction is fetch + its own routine.
5. **Encoded field size forgets "none"**: ⌈log₂ n⌉ vs ⌈log₂ (n+1)⌉ differs exactly when n is a power of two.
6. **Do not encode signals that must be asserted together**; they need separate fields/bits (e.g. Mini-1's `MARin` with `Tin`).
7. **Vertical needs decoders** → extra delay; horizontal needs (almost) none.
8. **Next-address field width follows from N**, not from the signal count; but if the successor is "CAR + 1" most of the time, a design may omit the field in non-branch words (variable format).
9. **Microprogrammed ≠ slower in every case**: it is slower than a comparable hardwired design because of control-store access per step; a question that defines times explicitly overrides the intuition.
10. **Do not claim a fixed rule for RISC/CISC** beyond tendencies (Section 8.3).

## 12. Edge cases and assumptions to state

- Binary prefixes: 1 K = 2¹⁰; "512 microinstructions" is exactly 2⁹ words.
- Whether "none" is a legal choice for a field.
- Whether the next-address field exists in **every** microinstruction.
- Whether sequencing/condition bits are inside the quoted "control word width".
- Whether fetch microinstructions are included in a per-instruction count.
- Overlap of control-store read with execution (serial vs overlapped microcycle).
- Memory speed relative to the microcycle (wait microinstructions).
- Number of bits is an integer: apply ceiling at **each field**, not once to the sum.

## 13. Connections to other COA topics

- [Hardwired control](../01-HARDWIRED/NOTES.md): same function; compare in Section 8.3. Counters/decoders from digital logic implement the step and opcode decoding there; ROM, MUX, register implement them here.
- [Instruction set / addressing modes](../../01-INSTRUCTION-SET/): operand-fetch routines (Section 6.4) correspond to addressing-mode work.
- [Pipelining](../../07-INSTRUCTION-PIPELINING/): microcode-per-instruction cannot sustain one-instruction-per-cycle; pipeline stages need fast control.
- [Interrupt](../../06-IO-INTERFACE/01-INTERRUPT/): the interrupt-entry sequence (save PC, load vector) is a microroutine of the Section 4.3 kind.
- [Performance](../../05-MEMORY-INTERFACING-AND-HIERARCHY/01-PERFORMANCE/): CPI, iron law.

---

## 14. Worked example 12: tracing a microroutine with a loop (verified)

Microroutine "REPEAT-ADD n": shift-style routine with a loop. Control-store words:

```
 20 : CNT ← n (from IR)             next +1
 21 : body part 1                   next +1
 22 : body part 2                   next +1
 23 : CNT ← CNT − 1                 if CNT ≠ 0 JUMP 21 else +1
 24 : (finish)                      JUMP 0
```

Count microinstructions for n = 4 (fetch of 3 included):

```
 fetch 3 + word 20 (1) + loop body (words 21,22,23) × 4 = 12 + word 24 (1) = 17 microinstructions
 general: 3 + 1 + 3n + 1 = 3n + 5       (n = 4 -> 17)
```

Trap: the test at word 23 happens **after** the decrement; the loop body runs n times, not n − 1 or n + 1.

---

## 15. Existing practice coverage map

Each question in [practice.md](../../../14-PRACTICE-QUESTIONS/TOPIC-WISE/03-COMPUTER-ORGANIZATION-ARCHITECTURE/04-DESIGN-OF-CONTROL-UNIT/02-MICROPROGRAMMED/practice.md):

| Q# | Skill | NOTES section |
|---|---|---|
| 1 | What control memory holds | 3.1, 3.2 |
| 2 | Horizontal definition | 5.1, 5.3 |
| 3 | Micro-PC width from number of microinstructions | 3.1, 7.1 (CAR = ⌈log₂ N⌉) |
| 4 | Horizontal width = signals + next address | 5.6, 7.1 |
| 5 | Encoded field with a "none" code | 5.4 (Worked example 1) |
| 6 | Horizontal vs vertical, decoder, flexibility, control memory space | 5.1–5.3, 8.3, 3.1 |
| 7 | Bits in control memory = words × width | 7.1 |
| 8 | Range of an absolute next-address field | 6.1, 10 (pattern) |
| 9 | Mixed table: encoded + direct fields, total store | 5.6, 7.2 (Example 8) |
| 10 | Mapping ROM, conditional branch, increment vs absolute address, shared fetch | 3.3, 6.1, 6.2 |
| 11 | Savings of group encoding vs horizontal | 5.4, 7.2 (Example 8) |
| 12 | Microprogram time vs hardwired time | 8.1, 8.2 |

## 16. Self-check

1. What is stored in the control store and who can address it?
2. Distinguish micro-operation, microinstruction, microroutine.
3. What does CAR hold and how wide must it be for N words?
4. Why is the fetch routine shared, and how does control leave it?
5. Give two ways to map an opcode to a start address and one drawback of each.
6. Compute the bits of a field choosing among 16 alternatives with and without a "none" code.
7. When may two signals share an encoded field?
8. How do horizontal and vertical formats compare in width, parallelism, speed and number of microinstructions?
9. How many bits does a condition-select field need for k conditions plus "unconditional"?
10. Compute control-store bits given routine lengths, fetch length, signal bits.
11. When does nanoprogramming reduce total storage, and what is its timing cost?
12. State three advantages and three disadvantages of microprogrammed vs hardwired control.
