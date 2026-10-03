# Addressing Modes — FORMULAS

Conventions: K = 2¹⁰, M = 2²⁰, G = 2³⁰. Byte-addressable unless stated. `M[x]` = memory content at address x. Derivations and context: [NOTES.md](NOTES.md).

---

## A. Effective address (EA) of the operand

### A1. Immediate / register / implied
```
 immediate : operand = k              (no EA)
 register  : operand = Rn             (no EA)
 implied   : operand fixed by opcode  (no EA field)
```
- **Applies:** operand not in memory. **Why:** the value travels with the instruction or lives in the register file.
- **Misuse:** writing "EA = Rn" for register addressing (Rn is not a memory address).

### A2. Direct and indirect
```
 direct              : EA = k            operand = M[k]
 indirect (1 level)  : EA = M[k]         operand = M[M[k]]
 indirect (L levels) : EA = M[M[…M[k]…]] (L reads) ; operand = M[EA]
```
- **Symbols:** k = address field. **Example (original):** M[30] = 64, M[64] = 21, M[21] = 88. Single-level indirect from 30: EA = 64, operand = 21. Two-level: EA = M[M[30]] = 21, operand = 88.
- **Misuse:** counting one fewer pointer read than the number of levels.

### A3. Register indirect and auto-inc/dec
```
 register indirect : EA = Rn
 post-increment (Rn)+ : EA = Rn(old) ;  Rn ← Rn + s
 pre-decrement  -(Rn) : Rn ← Rn − s ;   EA = Rn(new)
 s = operand size in address units (byte-addressable: bytes; word-addressable one-word operand: 1)
```
- **Why:** the register steps to the next element; the use-then-step / step-then-use order matches the push/pop stack discipline.
- **Example:** R = 2400, s = 8: `(R)+` uses 2400, R = 2408. `-(R)` then uses 2400 again, R = 2400.
- **Misuse:** using the new value for post-increment; stepping by 1 rather than s.

### A4. Displacement family
```
 EA = Rn + d     (base-register, index-style, SP/FP-relative)
 EA = PC_updated + d  (PC-relative)
```
- **Symbols:** d = signed or unsigned constant of the instruction (state which). **Example:** R5 = 7200, d = +36 → EA = 7236.
- **Misuse:** adding to the old PC; forgetting to sign-extend.

### A5. Two-register and scaled forms
```
 base + index : EA = Rb + Ri (+ d)
 scaled       : EA = Rb + Ri × s + d     s ∈ {1, 2, 4, 8}
```
- **Example:** Rb = 100, Ri = 8, s = 4, d = 0 → EA = 132.

### A6. Indirect with index
```
 pre-indexed (index added, then pointer read)  : EA = M[ k + Rx ]
 post-indexed (pointer read, then index added) : EA = M[ k ] + Rx
```
- **Example:** k = 40, Rx = 8, M[40] = 100, M[48] = 500 → pre: EA = 500; post: EA = 108.
- **Misuse:** swapping the two orders.

### A7. Autoincrement-deferred (machine-defined)
```
 @(Rn)+ : EA = M[Rn] ;  Rn ← Rn + (size of a pointer word)
```
- **Misuse:** stepping by the operand size instead of the pointer size.

---

## B. PC-relative branches

### B1. Target
```
 target = PC_updated + sext(field) × L
 PC_updated = A_branch + L_branch
```
- **Symbols:** L = instruction length in bytes when the field counts instructions (L = 1 in word-addressed units). Assumption: PC already incremented.
- **Example:** A = 0x2000, L = 4, field (12 bits) 0xFA0 → sext = −96 → target = 8196 − 384 = 7812.
- **Variant:** if the hardware adds to A_branch rather than PC_updated, subtract L_branch.

### B2. Reach of an n-bit signed offset field
```
 offsets (instructions): −2^(n−1) … 2^(n−1) − 1
 bytes from PC_updated : −2^(n−1)·L … (2^(n−1) − 1)·L
 total distinct targets: 2^n
```
- **Example:** n = 16, L = 2 → backward 65536 bytes, forward 65534 bytes from the updated PC.

### B3. Encoding an offset
```
 field = (target − PC_updated) / L     must be an integer and in the range above
 two's complement field = field mod 2^n
```
- **Example:** (16128 − 16388) / 4 = −65 → 8-bit field 256 − 65 = 191 = 0xBF.

### B4. Sign extension
```
 n-bit field f (unsigned reading): signed value = f − 2^n  if f ≥ 2^(n−1) else f
 0xF6 (8 bit) → −10 ; 0xFA0 (12 bit) → −96 ; 0xFFE0 (16 bit) → −32
```

---

## C. Instruction encoding

### C1. Opcode bits
```
 opcode bits = L_instr − mode bits − (number of register fields × ⌈log₂ R⌉) − literal bits
 opcodes (separate mode field) = 2^(opcode bits)    — available for EVERY mode
 (opcode, mode) pairs = 2^(opcode bits) × (number of legal mode codes)
 mode bits = ⌈log₂ (number of modes)⌉
```
- **Example (original):** 28 − 3 − 10 − 9 = 6 → 64 opcodes per mode; 64 × 8 = 512 pairs.
- **Merged mode+opcode field of w bits:** distinct opcodes = 2^w / (modes per opcode) when every opcode supports all modes. Example w = 8, 4 modes → 64.
- **Misuse:** subtracting an unused register field; dividing by modes when the mode field is separate.

### C2. Literal ranges
```
 n-bit signed   : −2^(n−1) … 2^(n−1) − 1
 n-bit unsigned : 0 … 2^n − 1
```

### C3. Direct-mode reach
```
 addressable units = 2^a        (a = address-field bits)
 bytes: byte-addressable → 2^a ; word-addressable with w-byte words → 2^a × w
```
- **Example:** a = 16, w = 4 → 2¹⁶ × 4 = 256 KB. Required a for 4 GB byte-addressable memory = 32.

### C4. Instruction fetch references
```
 fetch refs = ⌈ instruction bits / memory word bits ⌉
```

---

## D. Memory reference counts

```
 total refs = fetch refs + Σ over operands (operand refs by mode) + (1 per memory store)
 operand refs: immediate 0 ; register 0 ; implied 0 ; direct 1 ; register indirect 1 ; auto-inc/dec 1 ;
               displacement/base/index/scaled/PC-relative 1 ; indirect L levels: L + 1 ; pre/post-indexed indirect 2
```
- **Example:** `MOV (R1)+, (R2)+` = 1 + 1 + 1 = 3 refs; 10 executions = 30. `LOAD (Rp); ADDI #5; STORE (Rb,Ri,4)` with 1-word instructions = 3 fetches + 1 + 0 + 1 = 5.
- **Misuse:** counting registers, forgetting the store, forgetting that indirect adds one *per level*.

### D2. Cycle count in a stated model
```
 cycles = fetch + decode + EA stage + operand read + execute
```
- **Example:** memory = 2 cycles, other steps 1: displacement load = 2 + 1 + 1 + 2 + 1 = 7; memory indirect = 2 + 1 + 2 + 2 + 1 = 8. State your model!

---

## E. Array, record and pointer address arithmetic

```
 1-D           : &A[i] = base + (i − lb) × size
 2-D row-major : &M[i][j] = base + ((i − r0) × C + (j − c0)) × size     (C = #columns)
 2-D col-major : &M[i][j] = base + ((j − c0) × R + (i − r0)) × size     (R = #rows)
 record field  : &(rec[i].f) = base + i × recsize + offset(f)
 pointer table : &T[i][j] = M[tbl + i × ptrsize] + j × size
```
- **Examples (original):** A[37] (lb 0, 4 B, base 5000) = 5148, with lb = 1: 5144. M[7][12] (20×30, 4 B, base 8000): row-major 8888, column-major 8988. rec[9].age (24-B records, offset 16, base 3000) = 3232. Row-pointer table at 6000, row 3 pointer = 9000, element 5 → 9020.
- **Misuse:** ignoring the lower bound; swapping row/column major; using scale 4 for a 24-byte record.
