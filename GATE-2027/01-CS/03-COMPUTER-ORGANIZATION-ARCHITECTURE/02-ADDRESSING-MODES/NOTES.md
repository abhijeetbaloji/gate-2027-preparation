# Addressing Modes — NOTES

Self-contained study notes for GATE CS 2027. Read top to bottom once; later use the section index in
[REVISION.md](REVISION.md), [FORMULAS.md](FORMULAS.md) and [SHORTCUTS.md](SHORTCUTS.md).

---

## 0. Where this fits

**Syllabus line (COA):** "Instruction set and addressing modes. …" — this folder owns the *addressing modes* half of that sentence.

| Item | Detail |
|---|---|
| Prerequisites | Binary/hex, two's complement and sign extension (bridge in §3.6 → [../../02-DIGITAL-LOGIC/03-NUMBER-REPRESENTATION-AND-ARITHMETIC/01-FIXED-POINT](../../02-DIGITAL-LOGIC/03-NUMBER-REPRESENTATION-AND-ARITHMETIC/01-FIXED-POINT)); what a register, the PC and memory are; byte- vs word-addressability |
| Sibling topic that this one plugs into | [../01-INSTRUCTION-SET](../01-INSTRUCTION-SET) — instruction formats, opcode/field budget, RISC vs CISC, load/store architectures |
| Depends on this topic | [../03-ARITHMETIC-AND-LOGIC-UNIT](../03-ARITHMETIC-AND-LOGIC-UNIT) (the 2008 auto-increment question is *filed* there in the mapping), [../04-DESIGN-OF-CONTROL-UNIT](../04-DESIGN-OF-CONTROL-UNIT) (micro-steps that compute the EA), [../07-INSTRUCTION-PIPELINING](../07-INSTRUCTION-PIPELINING) and [../08-PIPELINE-HAZARDS](../08-PIPELINE-HAZARDS) (EA computation lives in EX; auto-increment writes a second register; load-use stalls on pointer chasing), [../05-MEMORY-INTERFACING-AND-HIERARCHY](../05-MEMORY-INTERFACING-AND-HIERARCHY) (every memory reference counted here is a potential cache access) |
| Outside COA (bridge only) | Relocation by base register / PC-relative code ties to loaders and paging: [../../08-OPERATING-SYSTEMS/08-MEMORY-MANAGEMENT-AND-VIRTUAL-MEMORY](../../08-OPERATING-SYSTEMS/08-MEMORY-MANAGEMENT-AND-VIRTUAL-MEMORY); array address arithmetic is the same as in [../../04-PROGRAMMING-DATA-STRUCTURES](../../04-PROGRAMMING-DATA-STRUCTURES) |

---

## 1. Evidence snapshot (why each section is as deep as it is)

**PYQ evidence (from `13-PYQ-TOPIC-MAPPING`, counted by me):** 3 mapped entries in this topic's own mapping file (2026 Q.14, 2024 Q.57,
2011 Q.21) and 1 more on-topic entry (2008 Q.33) that the mapping files under the ALU topic. The other two entries in the ALU mapping file
(2020 Q.4, 2016 Q.33) are *not* addressing-mode questions. No addressing-mode question was found by keyword search in the extracted
2013-2026 text outside these. Details: [PYQ.md](PYQ.md).

| Cluster | Skill | Section | Value | Evidence |
|---|---|---|---|---|
| A. Mode ↔ high-level construct matching | Know which mode serves constants, pointers, array elements, record fields | §5, §6 | **HIGH-VALUE** | 2026 Q.14 |
| B. Naming a mode from an instruction like `d(R)` | Distinguish displacement/base vs base-indexed vs scaled register-indirect vs immediate/register | §4.9, §4.13 | **HIGH-VALUE** | 2011 Q.21 |
| C. Instruction-field budget | opcode bits = length − (mode + register fields + literal field); opcodes per mode | §9 | **HIGH-VALUE** | 2024 Q.57 |
| D. Statement-style conceptual (auto-increment) | increment = operand size; no EA adder; relocation | §4.7, §8, §7 | **MEDIUM-HIGH** | 2008 Q.33 (filed under ALU) |
| E. EA / operand computation from a register-memory snapshot | apply formula, follow pointers | §4, §12.1 | **HIGH-VALUE** | existing practice Q3, Q5, Q7, Q8, Q11, Q13 |
| F. Memory-access counting | instruction fetch + pointer reads + operand access | §10 | **HIGH-VALUE** | existing practice Q9, Q14 |
| G. PC-relative / branch targets | PC after increment, sign extension, scaling, range | §7 | **HIGH-VALUE** | existing practice Q3, Q11, Q13 |
| H. Array / record / pointer address arithmetic | base + index × size, row-major, field offsets | §11 | **MEDIUM-HIGH** | existing practice Q4, Q10, Q13, Q14; and 2026 Q.14 |
| I. EA timing / cycle counting | cycles per mode in a stated model | §10.3 | **MEDIUM** | not in PYQs; arises indirectly in pipeline/control-unit questions; included as a prerequisite |
| J. Relocation / position-independent code | why PC-relative and base-register modes help | §7.6 | **MEDIUM** | 2008 Q.33 (statement I), existing practice Q6 |

**Existing-practice skills that NOTES must support:** define immediate / register-indirect; PC-relative target with displacement;
array element via base+index; post-increment by operand size; evaluate true/false statements about modes; base+displacement EA;
multi-level indirection with a memory table; memory-access counting; scaled-index byte address; signed hex displacement; auto-increment
and auto-decrement sequence; chained PC-relative → pointer → scaled index; access count for a load-store sequence. Mapping in §17.

---

## 2. Intuition: why addressing modes exist

An instruction must say **what to operate on**. If every instruction carried a full memory address for every operand, programs would be
long and could not express the things real programs do all the time:

```
 What the program does                  What the instruction needs
 -----------------------------------    ---------------------------------------------
 use a constant (x + 5)                 value inside the instruction  → no memory trip
 use a local variable again and again   a tiny register number        → no memory trip
 follow a pointer (*p)                  address held in a register/memory cell
 walk through an array (a[i], i++)      base + a number that changes each iteration
 touch a field of a struct              record start + fixed offset
 jump a few instructions forward/back   a small signed number relative to where we are
 load the program anywhere in memory    addresses that do NOT hard-code absolute numbers
 push/pop a stack                       an address that steps by the item size
```

An **addressing mode** is a rule that turns the bits in the instruction (plus some machine state: registers, PC, memory) into the operand.
Different rules trade: instruction length, number of memory accesses, flexibility, and relocatability.

A tiny picture — the "street address" analogy:

```
 Immediate        "the parcel IS in this letter"
 Register         "it is in locker #5 right here on the desk"
 Direct           "it is at house number 4096"
 Indirect         "house 4096 holds a note with the real house number"
 Register ind.    "the note is on my desk (in a register); go to that house"
 Displacement     "from the house on my desk, walk 24 doors further"
 Relative         "from where I'm standing now, walk 5 doors back"
 Auto-increment   "use the house on my desk, then move the desk-note to the next house"
```

---

## 3. Terminology, conventions and the one formula behind most modes

### 3.1 Definitions

| Term | Meaning |
|---|---|
| **Operand** | The data value the instruction uses (or the place a result goes). |
| **Effective address (EA)** | The *memory address* of the operand after the mode's rule is applied. Only memory-resident operands have an EA. |
| **Immediate / register operands** | Have **no EA** (the operand is in the instruction / in a register). Do not write "EA = …" for them in exam answers. |
| **Mode field** | Bits in the instruction (or inside the opcode) that choose the rule. |
| **Address field / literal field** | The bits that carry a constant: a memory address, a displacement, an immediate, or a branch offset. |
| **PC** | Program counter; during execution of an instruction it normally already points to the **next** instruction (see §7.1). |
| **Pointer** | A memory cell or register whose *value* is an address. |
| **Base / index register** | Registers added to the address field. "Base" = start of something (segment, record, frame); "index" = the varying part (subscript). |
| **Scale** | Constant multiplier (1, 2, 4, 8) applied to an index register so that the index counts elements, not bytes. |

### 3.2 Notation used throughout these notes

```
 #k        immediate: operand = k
 Rn        register: operand = Rn
 k         direct / absolute: EA = k
 @k        memory indirect: EA = M[k]
 (Rn)      register indirect: EA = Rn
 (Rn)+     post-increment:   EA = Rn, then Rn ← Rn + size
 -(Rn)     pre-decrement:    Rn ← Rn − size, then EA = Rn
 d(Rn)     displacement:     EA = Rn + d
 (Rb,Ri)   base + index:     EA = Rb + Ri
 d(Rb,Ri,s) scaled:          EA = Rb + Ri × s + d
 d(PC)     PC-relative:      EA = PC_updated + d
 M[x]      content of memory at address x
```

(Assembly syntax differs across textbooks; GATE gives the semantics in words. Always translate to an EA formula before answering.)

### 3.3 Conventions I use (state them in your own answers too)

- **K = 2¹⁰, M = 2²⁰, G = 2³⁰.**
- **Addressability is always stated.** Byte-addressable: address increments of 1 per byte; the stride of a 4-byte int is 4. Word-addressable: address
  increments of 1 per *word*; the stride of a one-word item is 1. If a problem does not say, say which you assume.
- **Memory-reference counting convention (§10):** one memory access = one read or one write of one memory word. An instruction that fits in one
  memory word costs one access to fetch; a longer instruction costs ⌈length / word width⌉ accesses. Register reads/writes are **not** counted.
  A store counts as a memory access.
- **PC convention:** the PC has already been advanced past the current instruction when the operand address is formed (§7.1). If a question uses
  another convention, it will say so.

### 3.4 The master formula

Almost every non-trivial mode is a special case of

```
        EA  =  [ base part ]  +  [ index part × scale ]  +  [ constant part ]
                 Rb / PC / SP       Ri                       d (from instruction)
```

| Mode | base part | index part | constant part |
|---|---|---|---|
| direct | – | – | k |
| register indirect | Rn | – | – |
| displacement (base / index / SP / PC style) | Rn or PC or SP | – | d |
| base + index | Rb | Ri | – |
| scaled, with displacement | Rb | Ri × s | d |

Memory indirection (`@`) is *not* part of this sum — it wraps another mode: it replaces "operand at EA" by "pointer at EA; operand at the pointer".

### 3.5 Anatomy of an operand fetch

```
 instruction ──decode──► mode field + literal/register fields
                               │
                 ┌─────────────┴──────────────┐
                 │ form EA (adder / register / pointer read) │
                 └─────────────┬──────────────┘
                               ▼
                 memory read (operand)   or   register read   or   use literal
                               ▼
                       execute, then write result
 side effect (auto-inc/dec): register updated too
```

### 3.6 Prerequisite / bridge — sign extension (belongs to Digital Logic)

Displacements and branch offsets are usually **signed two's-complement** numbers narrower than the address. Before adding, the hardware
**sign-extends**: copy the top bit into the added upper bits.

```
 8-bit  0xF6 = 1111 0110  → as signed: 246 − 256 = −10
 8-bit  0x36 = 0011 0110  → +54
 12-bit 0xFA0              → 4000 − 4096 = −96
 16-bit 0xFFE0             → 65504 − 65536 = −32
 n-bit signed range: −2^(n−1) … +2^(n−1) − 1       n-bit unsigned: 0 … 2^n − 1
```

If a field is stated "unsigned displacement" (typical for base-register addressing of record fields) there is no sign extension.

---

## 4. The modes, one by one

For each mode: **EA / operand rule → operand-fetch memory references → registers → typical HLL construct → strengths / limits.**
"Operand-fetch references" counts only the data accesses to *read* a source operand (add 1 more for a store to memory, and add the
instruction fetch separately, see §10).

### 4.1 Implied (implicit) addressing

- **Rule:** the opcode itself names the operand(s) — an accumulator, the top of stack, the flag register, the PC, the stack pointer.
  No operand field at all. Examples: `CLC` (clear carry), `INC A` on an accumulator machine, `ADD` on a stack machine (pops two, pushes one), `PUSH`/`POP` using SP implicitly.
- **Data refs:** 0 for register-held implied operands; for a stack machine the implied operand is *in the stack in memory*, so it costs a memory reference if the stack top is not cached in registers.
- **Strength:** shortest instruction (zero-address). **Limit:** very restricted; the machine state must be fixed by convention.
- Some books call "implied" and "implicit" the same; "register addressing" is *explicit* about which register.

### 4.2 Immediate addressing

- **Rule:** operand = the literal in the instruction. No EA.
- **Data refs:** 0 (the literal arrives with the instruction fetch).
- **Registers:** none for the operand.
- **HLL:** **constants** — `x = x + 5`, `i < 100`, initialising a variable, small offsets.
- **Strength:** fastest; no pointer; **Limit:** value range limited by the literal field (n-bit signed: −2ⁿ⁻¹…2ⁿ⁻¹−1); the value cannot change at run time (self-modifying code aside); a full-width constant often needs two instructions or an extra instruction word.

### 4.3 Register (direct) addressing

- **Rule:** operand = contents of register named in the instruction. No EA (the register is not a memory address).
- **Data refs:** 0. **Registers:** ⌈log₂ R⌉ bits to name one of R registers.
- **HLL:** scalar variables the compiler keeps in registers (loop counters, temporaries, `register` variables).
- **Strength:** fastest, short fields; **Limit:** only R values fit; names are fixed at compile time.

### 4.4 Direct (absolute) addressing

- **Rule:** EA = address field `k`. Operand = M[k].
- **Data refs:** 1.
- **HLL:** **global/static variables** whose address is known at compile or link time.
- **Strength:** simple. **Limits:** (i) the address field has width `a`, so only 2ᵃ locations are reachable directly (§9.3); (ii) absolute numbers are baked into the code, so moving the program requires **relocation** (patching every such address) (§7.5).

### 4.5 Indirect (memory-indirect) addressing

- **Rule:** the instruction's address field `k` locates a **pointer**; EA = M[k]; operand = M[M[k]].
  Multi-level: EA = M[M[…M[k]…]] (k levels = k pointer reads).
- **Data refs:** 2 for single-level (1 pointer read + 1 operand read); (L + 1) for L levels.
- **Registers:** none required (a flag bit in the instruction usually says "indirect", or an indirect mode code).
- **HLL:** **pointer dereference** where the pointer variable itself lives in memory (`y = *p;` with `p` a global in memory); handles/descriptors; jump tables (`goto *table[i]` uses more modes); call-by-reference parameters whose address sits in a memory cell.
- **Strength:** the pointer can be changed without changing the code; the reachable range is the width of the *pointer word*, not of the address field, so a short address field can still reach all memory. **Limit:** extra memory trip(s) per level; slow; rarely in modern load/store ISAs (they do the pointer load as a separate `LOAD`).
- **Ambiguity trap:** many textbooks use "indirect addressing" for memory-indirect, and "register indirect" for the register version. A question
  that says only "indirect" almost always means memory-indirect; if the pointer is in a register it is called **register indirect**.

### 4.6 Register-indirect addressing

- **Rule:** EA = Rn. Operand = M[Rn].
- **Data refs:** 1. **Registers:** 1 (⌈log₂ R⌉ bits).
- **HLL:** **pointer dereference with the pointer in a register**: `*p`, `p->field` when the offset is 0, linked-list walking (`p = p->next` is a register-indirect load whose result goes back into the same register when `next` is at offset 0).
- **Strength:** address space limited only by register width; short instruction; one memory trip. **Limit:** no offset — need `d(Rn)` for fields not at offset 0.

### 4.7 Auto-increment and auto-decrement

Two directions, two timings (all four combinations exist in real machines, GATE uses the classic pair):

```
 post-increment  (Rn)+ :  EA = Rn ;   then Rn ← Rn + size          ("use, then step forward")
 pre-decrement   -(Rn) :  Rn ← Rn − size ; then EA = Rn            ("step back, then use")
 pre-increment   +(Rn) :  Rn ← Rn + size ; then EA = Rn            (less common)
 post-decrement  (Rn)- :  EA = Rn ;   then Rn ← Rn − size          (less common)
```

- **Increment/decrement size = the size of the operand being accessed**, so that the register steps from one element to the next:
  a byte → 1, a 2-byte short → 2, a 4-byte int/float → 4, an 8-byte double → 8 (byte-addressable machine). On a word-addressable machine with one-word
  operands the step is 1. (The special case where it steps by the size of a *pointer* instead — autoincrement-deferred — is in §4.12.)
- **Data refs:** 1 (same as register indirect); the register update is an extra *register* write, not a memory access.
- **Registers:** 1 register that is both read and written.
- **HLL:** `*p++` and `*--p`; array traversal loops; copying `*dst++ = *src++`; **stack**: `PUSH x` ≡ store at `-(SP)`, `POP x` ≡ load from `(SP)+` for a stack that grows toward lower addresses (the opposite pairing, `+(SP)` push and `(SP)-` pop, for a stack growing upward).
- **Strength:** removes a separate `ADD Rn, Rn, #size` instruction in loops; compact. **Limits:** it does *not* make code relocatable; it changes a register as a side effect, so it complicates exception restart (the register was already updated), pipelines (a second register write) and instructions using the same register twice.
- **Hardware view:** the EA is just the register value (no addition is needed to form it); the +size/−size update can use a small dedicated incrementer, the PC-style adder or the main ALU in another cycle. So the mode **does not logically force** an extra ALU "for effective-address calculation" — that is an implementation choice (see §8 for the full statement-by-statement analysis).

### 4.8 The displacement family — one formula, several uses

All of these compute **EA = Rn + d** (or PC + d) with a constant `d` in the instruction. They differ in *which register plays which role*, which
tells the compiler what is changing and what is constant:

| Name | Register | Constant `d` | Typical use | Relocation |
|---|---|---|---|---|
| **Base-register** (base + offset) | `Rb` = start address of a record / segment / frame | small unsigned/signed offset | **record fields**, `p->field`, local variable at a fixed frame offset | change `Rb` only |
| **Index** (in the "constant + index register" sense) | `Ri` = varying subscript (in bytes) | start address of an array (may be a full address) | `a[i]` for a statically allocated array: `EA = &a + Ri` | patch `d` |
| **Relative (PC-relative)** | PC | signed offset of target from PC | branches, constants/data close to code, position-independent code | none needed |
| **SP-/FP-relative (stack-relative)** | SP or frame pointer | offset into the stack frame | locals and parameters | none needed |

Important points:
- *Hardware-wise* base-register, index and SP-relative are the same adder. The label depends on **which operand is the "moving" one**.
- Some textbooks call `X(Ri)` simply **"index mode"** even when `X` is a small offset; others call `d(Rn)` **"displacement"** or **"base with offset"**.
  The names are not standardised. In a *question with options*, decide by **register count and role** (§4.9), not by the word you remember.
- **Data refs:** 1 for operand read. **Instruction-length cost:** the displacement field must be in the instruction (shorter than a full address ⇒ cheaper than direct).
- **Range:** `Rn` can be any register value; `d` ranges over its field width (signed or unsigned). Reach from a given `Rn`: Rn + [dmin, dmax]. For PC-relative with offset field n bits signed: see §7.3.

### 4.9 `LW R1, 20(R2)` — what is it?

```
 LW  R1, 20(R2)       EA = 20 + R2        ONE register + ONE constant       → displacement (base + offset)
 LW  R1, (R2)         EA = R2             one register, no constant         → register indirect
 LW  R1, (R2, R3)     EA = R2 + R3        TWO registers                     → base + index (base-indexed)
 LW  R1, (R2,R3,4)    EA = R2 + R3×4      two registers + scale             → scaled index
 LW  R1, #20          operand = 20        no memory                         → immediate
 LW  R1, R2           operand = R2        register content                  → register direct
```

How to classify an exam instruction in 10 seconds: **(1)** Is the data operand coming from memory at all? **(2)** How many *registers* take part in forming
the address? **(3)** Is there a constant? **(4)** Is there a multiplier? **(5)** Is there a pointer fetch from memory?
- One register, constant added → *displacement family* (called "base", "index" or "displacement" depending on the book).
- One register, no constant → *register indirect*.
- Two registers added → *base + index* (also "base-indexed").
- Register × scale → *scaled* (often "scaled index" or "register indirect scaled" when no base).
- If no memory is involved the mode is "register" (operand is the register) or "immediate" (operand is the literal).

The options in a question determine the right word: match **structure** (registers + constant) rather than hunting for the book's preferred name.
I deliberately give no option letter for the actual 2011 PYQ; solve it with this table and verify against the official key.

### 4.10 Base + index addressing (two registers)

- **Rule:** EA = Rb + Ri. With an optional displacement: EA = Rb + Ri + d.
- **Data refs:** 1. **Registers:** 2.
- **HLL:** `a[i]` where **both the base address and the index are only known at run time** (a pointer to an array, a parameter array, dynamically allocated array); elements whose size is 1 byte (scale 1).
- **Strength:** both parts variable; **Limit:** if the element size is > 1 the index must be pre-multiplied (extra instruction) unless the machine has scaling (§4.11).

### 4.11 Scaled index addressing

- **Rule:** EA = Rb + Ri × s + d, with s ∈ {1, 2, 4, 8} (x86/ARM style; the scale is a small field or a shift amount).
- **Data refs:** 1. **Registers:** 2.
- **HLL:** `a[i]` where `a` has 2/4/8-byte elements; with `d` also: `rec[i].field` when the record size equals the scale (e.g. 8) and `d` = field offset.
- **Limit:** the multiplier is only a power-of-two small constant; for a record size like 24 bytes the index must be computed by `i × 24` first and then used with scale 1 (worked in §11.3).
- Without a base register ("register indirect scaled" = `(Ri × s)` or `d(,Ri,s)`) EA = Ri × s + d.

### 4.12 Memory-indirect combinations (edge cases)

- **Indirect + displacement, "pre-indexed":** EA = M[ k + Rx ] — the index is added *before* the pointer is read (an array of pointers: `*(tbl[i])`).
- **Indirect + displacement, "post-indexed":** EA = M[ k ] + Rx — the pointer is read first and the index added after (pointer to an array: `p[i]`).
- **Autoincrement-deferred (some ISAs, e.g. `@(R)+`):** EA = M[R]; then R ← R + size of a *pointer* (not of the operand). This is a classic trap: the step is the pointer width.
- **Data refs:** 2 (pointer read + operand read) for each of these.
- Worked values in §12.1.

### 4.13 Master comparison table (single-word instruction, accumulator-style source operand)

| Mode | Operand / EA | Data refs to read operand | Total refs incl. instruction fetch (1-word instr.) | Registers used | HLL meaning | Relocatable? |
|---|---|---|---|---|---|---|
| Implied (accumulator) | fixed by opcode | 0 | 1 | implicit | — | yes |
| Immediate | operand = k | 0 | 1 | 0 | constant | yes |
| Register | operand = Rn | 0 | 1 | 1 | register variable | yes |
| Direct | EA = k | 1 | 2 | 0 | global variable | **no** (absolute) |
| Indirect (1 level) | EA = M[k] | 2 | 3 | 0 | pointer in memory | **no** (absolute k) |
| Indirect (L levels) | EA = M[…M[k]] | L + 1 | L + 2 | 0 | pointer to pointer… | no |
| Register indirect | EA = Rn | 1 | 2 | 1 | pointer in register | yes |
| Auto-increment / decrement | EA = Rn (±) | 1 | 2 | 1 (updated) | `*p++`, stack | yes |
| Displacement (base / index / SP) | EA = Rn + d | 1 | 2 | 1 | record field, local, array | yes if reg is the moved item |
| PC-relative | EA = PC + d | 1 | 2 | PC | branch, nearby data | **yes** |
| Base + index | EA = Rb + Ri (+d) | 1 | 2 | 2 | array element | yes (Rb changes) |
| Scaled index | EA = Rb + Ri×s + d | 1 | 2 | 2 | array of 2/4/8-byte items | yes |
| Memory-indirect + index | EA = M[k+Rx] or M[k]+Rx | 2 | 3 | 1 | array of pointers / pointer to array | no |

(The "total refs" column assumes the instruction is one memory word; for longer instructions add fetches, §10.1.)

---

## 5. Mapping high-level constructs to modes (2026-type matching)

Build the answer from the **meaning of the data element**, not from memorised option letters.

| High-level data element | Natural mode | Why |
|---|---|---|
| **Constant** (`5`, `'A'`, `NULL`) | immediate | value is known at compile time; fits in the instruction |
| **Local scalar** kept in a register | register | no memory |
| **Global/static scalar** | direct (absolute) | fixed address |
| **Pointer** (value is an address; `*p`) | **indirect** (pointer in memory) or **register indirect** (pointer in a register) | the address of the data is itself data |
| **Array element** `a[i]` | **index / base + index / scaled index** | one part fixed (start of array), another varying (i) |
| **Record/struct field** `s.f` or `p->f` | **base with offset/displacement** | one fixed record start (in a register) + a compile-time-fixed field offset |
| Stack local / parameter | SP- or FP-relative | frame at a known offset |
| Loop over array with `p++` | auto-increment | steps by element size |
| Branch targets, loops, `goto` | PC-relative | nearby, position independent |

**Why array ↔ index and record ↔ displacement (and not the reverse):** in `a[i]` the *varying* quantity is `i`, chosen at run time, while the array
start is a constant of the program ⇒ "index" is the register part. In `s.f` the *varying* part is *which record* (a base that may point to any record
of that type) and the *fixed* part is the compile-time offset of field `f` ⇒ "base register + constant offset". When a question lists "Base with index"
next to "Base with offset", the **index form carries a changing subscript (array element)** and the **offset form carries a fixed field offset (record element)**.

How to attack a matching question:
1. Pair the unambiguous ones first (constant ↔ immediate; pointer ↔ indirect).
2. Between the remaining two, ask "is the variable part a subscript or is it a fixed offset?"
3. Eliminate options that contradict any certain pair.
I do not state the option letter for the actual 2026 PYQ; the pairings above are the concept and you must verify against the official key.

Caveat: real compilers can compile `a[i]` with base + displacement or a pointer-increment loop; the exam asks for the **canonical** textbook pairing.

---

## 6. Why exactly these modes? What each one buys (and costs)

```
 Mode             Instruction bits   Memory trips   Flexibility    Typical cost
 immediate        literal            0              low            literal width
 register         ⌈log2 R⌉           0              low            only R values
 direct           address width a     1              medium         a bits; non-relocatable
 reg indirect     ⌈log2 R⌉           1              high           no offset
 displacement     reg + d bits        1              high           adder in the path
 base+index       2 reg fields        1              very high      adder (+ shifter)
 memory indirect  address width a     2+             high           slow
 auto-inc/dec     ⌈log2 R⌉           1              loops          writes a register
```

CISC ISAs (VAX, x86, 68k) provide many modes ⇒ fewer instructions but variable length and complex decode. RISC load/store ISAs offer
only a few (register, immediate, `d(Rn)`, PC-relative) and do everything else with extra instructions — this is the §1-level link to
[../01-INSTRUCTION-SET](../01-INSTRUCTION-SET).

---

## 7. PC-relative addressing, branches, and relocatable code

### 7.1 Which PC value is used? (state your assumption)

The PC is normally incremented **during instruction fetch**, so by the time the target is calculated it already holds the address of the *next* sequential
instruction. The standard rule:

```
 target = PC_updated + offset           PC_updated = address of branch + length of branch instruction
```

Variants that appear (a question will state them): (i) hardware adds to the **address of the branch itself**; (ii) in a pipelined machine the PC may
already be two instructions ahead. The only safe approach is to **read the assumption from the question** and, if absent, use the updated PC and say so.

### 7.2 Offset encoding: sign extension and scaling

```
 byte-addressable, instruction length L bytes (e.g. 4), offset field n bits signed, counted in instructions:

        target = PC_updated + sext(field) × L
```

- The field is **sign-extended** first (§3.6), so a field with its top bit 1 is a backward branch.
- If instructions are aligned to L bytes, the low log₂L offset bits would always be 0, so the field is stored **in units of instructions** (scaled by L) to gain log₂L extra bits of reach.
- A *word-addressable* machine with 1-word instructions has L = 1 in address units; no scaling needed.

### 7.3 Reachable range

For an n-bit signed offset field counted in instructions of L bytes:

```
 offset in instructions : −2^(n−1)  …  +2^(n−1) − 1
 target range (bytes)   : [ PC_updated − 2^(n−1)·L ,  PC_updated + (2^(n−1) − 1)·L ]
 Number of different targets: 2^n
```

The asymmetry (one more backward than forward) is from two's complement. If the machine's PC points to the branch itself, shift the interval by L.

### 7.4 Worked example 1 — decode a PC-relative branch (byte-addressable, 4-byte instructions)

Branch at **0x2000**, updated PC = 0x2004 = 8196. Offset field 12 bits = **0xFA0**, counted in instructions.

```
 sign: 0xFA0 = 4000; 4000 ≥ 2048 → negative → 4000 − 4096 = −96 instructions
 byte offset: −96 × 4 = −384
 target = 8196 − 384 = 7812 = 0x1E84
 If the hardware used the branch's own address (8192): 8192 − 384 = 7808 → differs by L = 4
 Range for 12-bit field: −2048 … +2047 instructions → −8192 … +8188 bytes from updated PC → 8196−8192 = 4 … 8196+8188 = 16384
```

### 7.5 Worked example 2 — encode an offset

Branch at 0x4000 (16384), 4-byte instruction, target 0x3F00 (16128), 8-bit field in instructions.

```
 PC_updated = 16384 + 4 = 16388
 difference  = 16128 − 16388 = −260 bytes         must be a multiple of 4: −260/4 = −65 ✓.
 −65 within −128 … 127 ✓
 field = −65 + 256 = 191 = 0xBF
```

If the difference were not a multiple of 4 (misaligned target) or outside [−128, 127], the branch cannot be encoded — the assembler would use a longer form (absolute/register jump).

### 7.6 Relocation, self-relocating and position-independent code

**Problem:** the loader may place a program at different memory addresses on different runs.

- An instruction containing an **absolute** number (direct address, jump to an absolute label) breaks if the program moves — the loader must **patch** every such number ("relocation").
- **PC-relative references to things that move together with the code** (branches within the module, constants placed next to code) stay correct without any patching, because
  (target − PC) is unchanged if both move by the same amount. Code that uses only such references (and registers loaded via PC-relative address computation) is **self-relocating / position-independent**.
- **Base-register addressing** gives *hardware relocation*: the program uses addresses relative to a base register; the OS/loader changes one register to move the whole block.
- **Immediate** values and **register** operands are unaffected by moving the program (an immediate that *contains an address* is affected, though).
- **Auto-increment is not a relocation mechanism**: it steps a pointer register, but the starting value of that register must still come from somewhere (an absolute address ⇒ needs relocation; a PC-relative address computation ⇒ fine).

Check yourself (PRACTICE Q24 drills this): if a code+data block is moved as a whole by +0x1000, a PC-relative branch inside the block is still correct, but a direct-address load of a variable inside the block now points to the old, wrong place until the loader patches it.

---

## 8. Auto-increment: truth-testing typical statements (the 2008 style)

The mapping files the 2008 auto-increment question under the **ALU** topic, but it is an addressing-mode concept (the update step uses an adder). The
question asks which of three statements about the mode are true. The three claims, paraphrased, and how to *decide* them:

| Claim (paraphrase) | Decision procedure | Reasoning |
|---|---|---|
| "Auto-increment is useful for creating self-relocating code." | Does the mode remove absolute addresses from the code? | No. The register steps through memory, but its starting value is an address that must still be supplied (absolute ⇒ relocation needed; PC-relative ⇒ the PC-relative part provides the independence, not the auto-increment). Position independence comes from PC-relative / base-register addressing. |
| "If included, the ISA needs an *additional ALU* for EA calculation." | What is the EA? | EA = the register's content. No addition is needed to form it. The register's +size update can be done by a small incrementer or the existing ALU in an extra micro-step, so a second ALU is a design option, not a logical necessity. |
| "The amount of increment depends on the size of the data item accessed." | What must the register hold after the step? | The address of the next *element*. A byte → +1, 4-byte word → +4, 8-byte double → +8 (on a byte-addressable machine). Increment = operand size by definition of the mode. |

I give these as *concept verdicts by reasoning*. The mapping does not hold a verified key; **check the official answer for the PYQ yourself**, and
use the decision procedure for any variation: for each statement, find the EA and the register update and ask "does this require arithmetic for EA?", "does the code still contain absolute numbers?", "what is the stride?".

Other statement-style claims worth testing the same way:
- "Auto-increment needs two memory accesses to fetch the operand." False; one memory access (the other action is a register update).
- "Auto-decrement lets a stack grow downward with push." True with `-(SP)` for push and `(SP)+` for pop (decrement before store; increment after load).
- "The register value used as EA is the value after the increment in `(R)+`." False; post-increment uses the old value.

---

## 9. Interplay with instruction encoding

### 9.1 Field budget

Instruction length `L` bits is divided among **opcode**, **mode**, **register fields**, and **literal/address field**:

```
 L = opcode bits + mode bits + (number of register fields × ⌈log₂ R⌉) + literal-field bits
```

Rearranged: **opcode bits = L − mode bits − register-field bits − literal bits**; number of distinct opcodes = 2^(opcode bits).

- A *separate mode field* of m bits can encode up to 2^m modes. With μ modes needed, m = ⌈log₂ μ⌉ (5 modes ⇒ 3 bits; the other three codes unused).
- If the mode field is separate, **every opcode can be combined with every mode**, so each mode may use all 2^(opcode bits) opcodes. "Maximum
  number of opcodes possible for every addressing mode" asks for exactly 2^(opcode bits).
- The *total number of (opcode, mode) pairs* encodable = 2^(opcode bits) × 2^(mode bits) (if all mode codes are legal).
- If instead the mode bits are **folded into the opcode** (a single combined field of w bits), the number of instruction *variants* is 2^w, and with μ modes per opcode the number of distinct opcodes is 2^w / μ (if all modes are available for all of them).
- Orthogonality: RISC fixed-length ISAs often use a different instruction *format* per addressing style (immediate format vs register format) rather than a mode field; then the "mode" is implied by the opcode.

### 9.2 Worked example 3 — field budget (original numbers)

A 28-bit instruction has: mode field wide enough for 5 modes, two register operand fields (32 registers), and a 9-bit literal field.

```
 mode bits   = ⌈log₂ 5⌉ = 3
 reg bits    = 2 × log₂ 32 = 10
 literal     = 9
 opcode bits = 28 − 3 − 10 − 9 = 6    → 2⁶ = 64 opcodes per mode
 pairs encodable (all 3-bit mode codes legal) = 64 × 8 = 512; only the 5 needed modes: 64 × 5 = 320
 9-bit signed immediate: −256 … 255 ; unsigned: 0 … 511
```

### 9.3 Address-field width vs addressable memory

- **Direct mode:** an address field of `a` bits reaches only 2ᵃ distinct locations.
  - Byte-addressable: 2ᵃ bytes. `a = 16` ⇒ 64 KB.
  - Word-addressable with w-byte words: 2ᵃ × w bytes. `a = 16`, 4-byte words ⇒ 256 KB.
  - To reach a memory of 2ᴹ addressable units with direct mode, `a ≥ M`; for 4 GB byte-addressable memory, a = 32.
- **Indirect mode** removes the limit: the *pointer word* may be 32 bits even if the address field is 12 bits; the reachable memory is determined by the pointer width (but only pointers stored in the first 2¹² locations can be named).
- **Register-indirect / displacement / base+index:** the reachable range is set by the **register width** (plus the displacement range), not by the address field. This is why direct mode "limits addressable space" while register-based modes do not.
- **Displacement field width `d` bits:** limits the reach from the base register: unsigned d bits ⇒ offsets 0…2ᵈ−1; signed ⇒ −2ᵈ⁻¹…2ᵈ⁻¹−1. A 12-bit unsigned field cannot reach field offset 5000 in a big struct.
- **Variable-length instructions:** a full 32-bit address can sit in an *extra word* following the opcode; then direct mode costs one extra instruction-fetch reference (§10.1).

### 9.4 Register-field width

R registers need ⌈log₂ R⌉ bits per register operand; 16 registers ⇒ 4 bits; 32 ⇒ 5; 64 ⇒ 6. A mode needing 0, 1 or 2 registers wastes the unused fields (unless they are reused as literal bits).

---

## 10. Counting memory references and cycles

### 10.1 Instruction-fetch references

```
 fetch refs = ⌈ instruction length (bits) / memory word width (bits) ⌉      (if the whole instruction must be fetched)
```
A 32-bit instruction on 16-bit memory words costs 2 fetch references. A direct-address instruction with the address in a *second word* costs 2 fetches.
Unless stated, assume one fetch per instruction.

### 10.2 Reference table for one source operand (one-word instruction)

Total = instruction fetch (1) + operand refs + (1 if the result is stored to memory).

| Mode | operand refs | Example total for `ADD A, X` (result in accumulator) |
|---|---|---|
| implied / immediate / register | 0 | 1 |
| direct, register indirect, auto-inc/dec, displacement, base+index, scaled, PC-relative | 1 | 2 |
| memory indirect (1 level) | 2 | 3 |
| memory indirect (L levels) | L + 1 | L + 2 |
| indirect + index (pre- or post-) | 2 | 3 |

Two-memory-operand CISC instruction: `MOV (R1)+, (R2)+` = 1 fetch + 1 read + 1 write = **3**; executed 10 times = 30 (original numbers).
`ADD @A, @B` into a register = 1 + 2 + 2 = 5 (single-level indirect, two operands).

### 10.3 Cycle counting in a stated model

Model (assumptions for this example only): memory access = 2 clock cycles; decode = 1; register-to-register ALU or address addition = 1; execute = 1;
operand registers read in the decode cycle. Instruction `ADD R1, <operand>`:

```
 cycles = fetch(2) + decode(1) + EA stage + operand read + execute(1)

 Mode             EA stage              operand read   total
 immediate        0                      0              4
 register         0                      0              4
 direct           0 (address in IR)      2              6
 register ind.    0                      2              6
 auto-increment   0 (+1 update overlaps) 2              6
 displacement     1 (add)                2              7
 base + index     1 (add)                2              7
 scaled index     2 (shift, add)         2              8
 memory indirect  2 (pointer read)       2              8
```
(Verified by script.) Change the model assumptions ⇒ change the numbers; **always state the model**. Relationship to pipelines: in a 5-stage pipeline,
the displacement/indexing addition happens in EX and the memory access in MEM, which is why complex modes are removed in RISC designs.

---

## 11. Arrays, records and pointers — worked address arithmetic

### 11.1 One-dimensional arrays

```
 &A[i] = base + (i − lowerbound) × size
```
Byte-addressable, `int A[0..99]`, 4 bytes, base 5000: &A[37] = 5000 + 37×4 = **5148**.
If the lower bound is 1 (Pascal-style `A[1..100]`): &A[37] = 5000 + 36×4 = **5144**. (Using the wrong lower bound is a common off-by-one slip.)

Instruction form: `LOAD R1, (Rb, Ri, 4)` with Rb = 5000, Ri = 37 (scale 4); or without scaling: first `Ri' = Ri << 2`, then `(Rb, Ri')`.

### 11.2 Two-dimensional arrays

```
 row-major   :  &M[i][j] = base + ((i − r0) × C + (j − c0)) × size          C = number of columns
 column-major:  &M[i][j] = base + ((j − c0) × Rw + (i − r0)) × size         Rw = number of rows
```
`int M[0..19][0..29]` (20 rows, 30 columns), 4 bytes, base 8000, element [7][12]:
- row-major: 8000 + (7×30 + 12)×4 = 8000 + 222×4 = **8888**
- column-major: 8000 + (12×20 + 7)×4 = 8000 + 247×4 = **8988**

How the modes realise it: the compiler computes `row_offset = (i×C)×size` with ordinary arithmetic into a register, then uses **base + scaled index**:

```
 MUL  Rt, Ri, #(C×size)         ; row offset in bytes
 LOAD R1, (Rb, Rt) with displacement j×size   when j is a constant  → d(Rb,Rt)
 or     LOAD R1, (Rrow, Rj, 4)  with Rrow = Rb + Rt, Rj = j and scale 4
```

An array of **row pointers** (Java-style `int[][]`) uses *memory indirection* then index: with a table of 4-byte row pointers at 6000, row 3's pointer lives at 6000 + 3×4 = 6012 and holds 9000; element [3][5] = 9000 + 5×4 = **9020**: pre-indexed indirect (table read) followed by an index.

Which register holds what — "indexed" vs "base-register" for arrays:
- *Index-register style:* d = start of array (constant of the program), register = element offset (changes).
- *Base-register style:* register = start of array (changes between calls/relocations), d = constant offset (e.g. field/element at fixed position).
- Both use EA = register + d; the **role assignment** is the distinction. For `a[i]` with both unknown: base + index (two registers).

### 11.3 Arrays of records (struct arrays)

Record size 24 bytes, fields `name` at 0, `age` at 16, `score` at 20; array `rec[0..49]` at base 3000.
`rec[9].age` = 3000 + 9×24 + 16 = **3232**.
Scale factors are only 1, 2, 4, 8 — 24 is not one of them, so the compiler computes `Ri = 9 × 24 = 216` and then uses base+index with scale 1 and displacement 16:
`EA = Rb + Ri + 16 = 3000 + 216 + 16 = 3232`. If the record size were 8, a single `16(Rb, Ri, 8)` would do the job.

### 11.4 Linked structures — pointer chasing

Node = {int val at offset 0; Node *next at offset 4} (4-byte pointers). Head pointer in R1 = 200.
Memory: M[200]=7, M[204]=300, M[300]=9, M[304]=420, M[420]=5, M[424]=0.

```
 LOAD R2, 4(R1)      ; R2 = M[204] = 300    (displacement; R1 + field offset)
 LOAD R3, 4(R2)      ; R3 = M[304] = 420
 LOAD R4, 0(R3)      ; R4 = M[420] = 5      (register indirect = displacement 0)
 Memory references = 3 instruction fetches + 3 data reads = 6
 (each hop is a load that depends on the previous: a load-use hazard chain in a pipeline)
```

---

## 12. Step-by-step GATE solving procedures

### 12.1 Procedure A — compute EA and operand from a snapshot

1. Write the mode formula (§4.13).
2. Substitute register values (current values, before side effects).
3. If indirect, read memory for each pointer level.
4. Apply side effects (auto-inc/dec) after/before according to the mode.
5. Report: EA (if any), operand, final register values.

Worked example 4 — one snapshot, many modes. Registers R1 = 100, R2 = 40, R3 = 8. Memory (word-addressable): M[8] = 99, M[40] = 100, M[48] = 500,
M[100] = 300, M[108] = 55, M[132] = 77, M[140] = 7, M[300] = 11, M[500] = 123. The instruction's literal field k = 40.

| Mode | EA | Operand | Arithmetic |
|---|---|---|---|
| immediate `#40` | – | 40 | literal |
| register `R2` | – | 40 | R2 |
| direct `40` | 40 | 100 | M[40] |
| indirect `@40` | 100 | 300 | M[40] = 100 then M[100] |
| register indirect `(R2)` | 40 | 100 | M[R2] |
| register indirect `(R1)` | 100 | 300 | M[R1] |
| displacement `40(R1)` | 140 | 7 | 100 + 40 |
| base + index `(R1,R3)` | 108 | 55 | 100 + 8 |
| scaled `(R1,R3,4)` | 132 | 77 | 100 + 8×4 |
| pre-indexed indirect = M[40 + R3] | M[48] = 500 | M[500] = 123 | index added, then pointer read |
| post-indexed indirect = M[40] + R3 | 100 + 8 = 108 | 55 | pointer read, then index added |

### 12.2 Procedure B — memory-access count

1. Instruction fetch refs (§10.1).
2. For every source operand, operand refs from §10.2.
3. +1 for each memory destination.
4. Sum over the instruction sequence; **immediates and registers add 0**.

### 12.3 Procedure C — branch target (§7)

PC_updated → sign-extend field → scale by instruction size → add → check range/alignment.

### 12.4 Procedure D — field-budget (§9)

List every field in bits; opcode bits = remainder; opcodes = 2^bits; per-mode vs total depends on whether the mode field is separate.

### 12.5 Procedure E — statement truth-testing (§8)

For each statement: EA formula? Memory trips? Register side effects? Absolute numbers? Stride? Decide with the definition, not intuition.

### 12.6 Procedure F — auto-inc/dec sequence

Track the register after each instruction; for `(R)+` EA = old R; for `-(R)` EA = new R.

Worked example 5: R4 = 3000, 4-byte ints, four `ADD R1, (R4)+`: EAs 3000, 3004, 3008, 3012; R4 = 3016 at the end.
Stack: SP = 0x8000 (grows down, 4-byte items): `PUSH` = `-(SP)` store → SP = 0x7FFC, item at 0x7FFC; `POP` = `(SP)+` load from 0x7FFC → SP = 0x8000.

---

## 13. PYQ patterns (recognise → recipe → trap)

| # | Pattern | Recognise | Recipe | Trap |
|---|---|---|---|---|
| 1 | Matching HLL constructs to modes (2026 Q.14) | two lists, "immediate / indirect / base with index / base with offset" vs "constant / pointer / array element / record field" | §5 table; pair certain ones, then fixed-offset vs subscript | confusing array ↔ offset and record ↔ index; "indirect" vs "register indirect" |
| 2 | Name the mode of an instruction (2011 Q.21) | "EA obtained by adding constant and register" with four named options | §4.9: count registers, constant, scale | option wording "base indexed" (two registers) vs "register indirect scaled" (multiplier) vs displacement; textbooks differ on the word "index" |
| 3 | Field budget (2024 Q.57) | opcode + mode + register fields + literal in a fixed length | §9.1: opcode bits = remainder; per-mode = 2^bits | forgetting a register field; adding modes into the opcode count when mode field is separate; reading "per mode" as "total" |
| 4 | Statement truth-test on auto-increment (2008 Q.33, filed under ALU) | "which is/are true" with I, II, III | §8 decision procedure | assuming auto-increment gives relocation; assuming it needs an EA adder |
| 5 | EA from register/memory snapshot | numeric register/memory | §12.1 | forgetting the indirection level; word vs byte stride |
| 6 | Branch target | "PC-relative", signed offset | §7, §12.3 | wrong PC value; forgetting sign extension; forgetting scaling |
| 7 | Memory-access counting | "how many memory accesses" | §10, §12.2 | forgetting instruction fetch or pointer reads |

---

## 14. Traps and misconceptions

1. "Immediate has an EA." It does not; the operand is in the instruction.
2. "Register addressing has an EA of the register number." No — the register is not memory.
3. "Register indirect = register addressing." Register addressing reads the register *as data*; register indirect reads memory at the address in the register.
4. "Indirect needs 2 accesses total." It needs 2 *data* accesses; with the instruction fetch, 3.
5. "Post-increment uses the new value." It uses the old value; the register is updated afterwards (pre-decrement uses the new value).
6. "Auto-increment steps by 1." It steps by the operand size in address units.
7. "PC-relative offset is added to the address of the branch." Usually to the **updated PC** (address of the next instruction).
8. Forgetting sign extension (an 8-bit 0xF6 is −10, not +246).
9. Forgetting that offset fields are in instruction units (scaled), so reach is L times larger.
10. Believing a mode with a short address field can address all of memory: only direct mode is bound by the field width.
11. Mixing up names: "indexed" in one book = "displacement" in another; always read the formula.
12. Row-major vs column-major swapped; lower bound ignored.
13. Counting register accesses as memory accesses.
14. Forgetting that a store to memory is a memory access.
15. Believing PC-relative = relative to the start of the program (it is relative to the current instruction).
16. Treating `@(R)+` like `(R)+` — the step is the pointer size, not the operand size, if the machine defines it that way.

## 15. Edge cases and assumptions to state

- Byte- vs word-addressable; stride of an element; K = 2¹⁰.
- Which PC (updated or branch address; pipeline lead).
- Signed vs unsigned displacement/immediate fields.
- Single-word vs multi-word instructions.
- Whether a "store" counts as a memory reference (it does).
- Whether the mode field is a separate field or merged into the opcode.
- Whether indirect means memory or register indirect.
- Auto-inc/dec when the same register is also an explicit operand (`ADD R1, (R1)+`): result unspecified/implementation-defined in many ISAs; the question will define it.
- Overflow of EA past the address width: wraps modulo 2ᵃ in hardware.
- Misaligned PC-relative target: cannot be encoded when scaling by L.

---

## 16. Connections to other COA topics

- **Instruction set ([../01-INSTRUCTION-SET](../01-INSTRUCTION-SET)):** formats, opcode expansion, 0/1/2/3-address instructions; field budget (§9) is the same calculation.
- **ALU ([../03-ARITHMETIC-AND-LOGIC-UNIT](../03-ARITHMETIC-AND-LOGIC-UNIT)):** the adder that forms EA (base + index + displacement) and increments PC and auto-inc registers.
- **Control unit (04):** micro-steps `MAR ← EA; MDR ← M[MAR]` and the extra micro-steps for indirect/indexed modes.
- **Pipelining (07/08):** EA computed in EX; auto-increment gives a second write-back; pointer chasing causes load-use dependencies.
- **Memory hierarchy (05):** each reference counted in §10 is an access to the cache; PC-relative code has good instruction locality.
- **OS memory management:** hardware relocation by base register is the ancestor of paging; position-independent code lets shared libraries load anywhere.

## 17. Existing practice coverage map

| Existing Q# | Skill | NOTES section |
|---|---|---|
| Q1 | immediate definition | §4.2 |
| Q2 | register-indirect EA | §4.6 |
| Q3 | PC-relative target, word-addressable | §7.1–7.3, §12.3 |
| Q4 | a[i] with base + index registers | §4.10, §5, §11.1 |
| Q5 | post-increment by operand size | §4.7, §12.6 |
| Q6 | multi-statement mode properties (immediate, indirect, register speed, PC-relative position independence) | §4.2, §4.5, §4.3, §7.6 |
| Q7 | base + displacement | §4.8, §12.1 |
| Q8 | multi-level indirection with memory table | §4.5, §12.1 |
| Q9 | memory access count with indirect operand | §10.2, §12.2 |
| Q10 | scaled-index byte address | §4.11, §11.1 |
| Q11 | signed 8-bit hex displacement | §3.6, §7.2, §7.4 |
| Q12 | post-increment then pre-decrement trace | §4.7, §12.6 |
| Q13 | PC-relative pointer then scaled index | §7, §4.11, §12.1 |
| Q14 | access count of a load-store sequence with mixed modes | §10, §12.2 |

## 18. Self-check

1. For which modes does an "effective address" not exist?
2. Write the EA formula and the number of data memory references for each of: direct, indirect, register indirect, displacement, scaled index.
3. What is the difference between register direct and register indirect addressing?
4. In `(R)+` and `-(R)`, which register value is used as the EA, and by how much does the register change for a 4-byte operand?
5. How do you tell "displacement" from "base + index" from "scaled index" from an instruction's EA formula?
6. A branch at address A, length L, offset field n bits signed counted in instructions: what is the target, and the reachable range?
7. Why does PC-relative addressing give position-independent code, and why does auto-increment not?
8. How many opcodes per mode when a fixed-length instruction has a separate mode field? How does the answer change if the mode is merged into the opcode?
9. Why does direct addressing limit the addressable memory but register-indirect does not?
10. Compute &M[i][j] for a row-major and a column-major 2-D array with a given base, size and bounds.
11. For a record array whose record size is 24 bytes, why can't scale-4/8 addressing alone do `rec[i].f`?
12. Count the memory references (including instruction fetch) for a given instruction sequence mixing immediate, register-indirect, and indexed operands.
