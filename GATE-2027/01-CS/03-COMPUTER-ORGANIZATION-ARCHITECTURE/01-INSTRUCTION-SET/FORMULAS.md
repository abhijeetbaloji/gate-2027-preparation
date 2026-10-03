# Instruction Set — Formulas

Conventions: 1 K = 2¹⁰, 1 M = 2²⁰, 1 G = 2³⁰. ⌈x⌉ = ceiling, ⌊x⌋ = floor. L = instruction length in bits. Derivations and context: [`NOTES.md`](NOTES.md).
Every example below was recomputed by script (`/tmp/coa-verify-01-instruction-set.py`).

---

## A. Field sizing

### A1. Bits to name n objects
- **Statement:** bits = ⌈log₂ n⌉.
- **Symbols:** n = number of distinct objects (registers, opcodes, addressing modes, memory words); result in bits.
- **When:** any field that must distinguish n values. With a single fixed-length opcode field, n = number of distinct instructions/opcodes.
- **Why:** b bits give 2ᵇ patterns; need 2ᵇ ≥ n.
- **Example:** n = 24 → 5; n = 40 → 6; n = 64 → 6; n = 65 → 7; n = 1 → 0.
- **Misuse:** treating "64 registers" as 64 bits; using ⌊log₂ n⌋; using n−1.

### A2. Leftover field width (maximum immediate / offset)
- **Statement:** w = L − opcode − Σ(register fields) − Σ(other fixed fields).
- **Symbols:** L bits; opcode = ⌈log₂ k⌉ for k instruction types (single field); register field = ⌈log₂ r⌉ each.
- **When:** fixed-length formats with one undetermined field. The question must list every other field.
- **Why:** the fields tile the L bits exactly.
- **Example:** L = 32, 90 types, 35 registers, `opcode|Rd|Rs|imm`: 32 − 7 − 2·6 = **13**.
- **Misuse:** wrong number of register fields (read the instruction shape, e.g. `ADD R1, #25` has one); forgetting an "unused" or "mode" field.

### A3. Signed / unsigned range of a w-bit field
- **Statement:** unsigned 0 … 2ʷ−1; two's complement −2ʷ⁻¹ … 2ʷ⁻¹−1.
- **Example:** w = 12 → 0…4095 or −2048…2047.
- **Misuse:** using the unsigned range for a branch offset that must be signed.

### A4. Maximum registers for a given minimum immediate (reverse problem)
- **Statement:** registers = 2^⌊(L − opcode − w_min)/m⌋, m = number of register fields (all equal width), result a power of two.
- **Why:** the register bits available must be split equally into m fields; leftover bits are wasted.
- **Example:** L = 32, opcode 7 bits (100 operations), immediate ≥ 12, m = 2: ⌊13/2⌋ = 6 → **64** registers; m = 3: ⌊13/3⌋ = 4 → **16** registers.
- **Misuse:** using 2^(13/2) or forgetting the floor.

---

## B. Program size

### B1. Byte-aligned program size
- **Statement:** size (bytes) = N × ⌈b/8⌉, b = bits of one instruction.
- **Why:** each instruction begins on a byte boundary, so padding is added to every instruction.
- **Example:** b = 4 + 3·6 + 13 = 35 → 5 bytes; N = 60 → **300 bytes**. (Wrong: ⌈60·35/8⌉ = 263.) 4-byte-word aligned: 2 words = 8 bytes each → 480 bytes.
- **Misuse:** rounding once for the whole program.

### B2. Multi-word instructions
- **Statement:** program words = Σ (1 + number of full address words) per instruction; fetch reads per instruction = its length in words.
- **When:** CISC-style models where memory addresses live in extra words.

---

## C. Opcode sizing with several formats

### C1. Format bit with equal split
- **Statement:** opcode bits = 1 + ⌈log₂(n/2)⌉ = ⌈log₂ n⌉.
- **When:** n instructions equally divided between 2 types, one opcode bit selects the type.
- **Example:** n = 200 → 1 + 7 = 8.

### C2. Format bit with unequal split
- **Statement:** opcode bits = 1 + ⌈log₂ n_max⌉, n_max = operations in the larger type.
- **Example:** 100 R-type + 20 I-type → 1 + 7 = 8 (the flat ⌈log₂ 120⌉ = 7 is wrong here).
- **Misuse:** applying the flat formula to unequal types.

---

## D. Expanding (variable-length) opcodes

### D1. Opcode length of a type
- **Statement:** o_t = L − (operand bits of type t).
- **When:** every bit not claimed by an operand field belongs to the opcode (and its extensions).

### D2. Maximum opcodes of a target type (the "fraction of encoding space" rule)
- **Statement:**
  N_T = ⌊ 2^(o_T) − Σᵢ nᵢ · 2^(o_T − oᵢ) ⌋ = ⌊ 2^(o_T) · (1 − Σᵢ nᵢ · 2^(−oᵢ)) ⌋
- **Symbols:** o_T = target opcode length; nᵢ, oᵢ = opcodes already assigned to type i and their opcode length (bits).
- **When:** prefix-free (decodable) variable-length opcodes in a fixed-length instruction; every bit pattern of the opcode is allowed.
- **Why:** an opcode of length o claims 2⁻ᵒ of the 2ᴸ patterns; claims must be disjoint ⇒ Σ ≤ 1; canonical (shortest-first) assignment shows the bound is attainable.
  Take **one** floor at the end after adding exact fractions.
- **Examples:**
  - 16-bit, 32 registers; A: opcode+R+imm6 (o = 5), B: opcode+R+R (o = 6); 11 A-opcodes → N_B = 64 − 22 = **42**.
  - 16-bit, 8 registers; o = 3 (5 assigned), 5 (9 assigned), target o = 7 → 128 − 80 − 36 = **12**.
  - Target shortest: o_T = 3 with 9 opcodes of length 5 → ⌊8 − 2.25⌋ = **5**.
  - 24-bit, 32 registers; o = 9 (100), 8 (21), target 7 → ⌊128 − 25 − 10.5⌋ = **92**.
- **Misuse:** subtracting nᵢ without scaling by 2^(o_T − oᵢ); flooring each type separately; using the formula when a separate format bit is stated.

### D3. Expanding chain (re-using an address field as opcode extension)
- **Statement:** S₍k+1₎ = (S₍k₎ − n₍k₎) · 2ʷ, with S for the most-operand format = 2^(L − m·w) (m address fields of width w).
- **Symbols:** S_k = opcode slots at level k; n_k = opcodes used at level k; w = width of the freed address field.
- **Example:** L = 20, w = 5, m = 3: S₃ = 32; n₃ = 20 → S₂ = 12·32 = 384; n₂ = 300 → S₁ = 84·32 = 2688; n₁ = 2000 → S₀ = 688·32 = **22016**.
- **Why:** each unused prefix at level k, extended by w free bits, yields 2ʷ prefixes at the next level — a special case of D2.
- **Misuse:** applying it when only some free prefixes are extended or when the freed field has a different width.

---

## E. Instruction length vs memory

### E1. Address field width
- **Statement:** a = ⌈log₂(addressable locations)⌉; 64 K words → 16; 1 MB (byte-addressable) → 20.
- **Misuse:** counting bytes when memory is word-addressable (or vice versa).

### E2. PC-relative reach
- **Statement:** offset range −2ʷ⁻¹ … 2ʷ⁻¹ − 1 units; bytes = units × bytes per unit.
- **Example:** w = 12, 4-byte units → −8192 … +8188 bytes.

---

## F. Counting instructions on each machine type

For `Z = expr` with `leaves` operand occurrences and `ops` binary operators, all leaves distinct variables, inputs not overwritten:

| Machine | Instructions | Note |
|---|---|---|
| Stack (no DUP) | leaves + ops + 1 | PUSH per leaf, op, POP |
| 3-address | ops | final op writes Z |
| Load–store (enough registers) | distinct-variable loads + ops + 1 | |
| Accumulator | cost(root) + 1 | cost(leaf)=1; op(l, r): r leaf → cost(l)+1; l leaf & commutative → cost(r)+1; l leaf & non-commutative → cost(r)+3; both complex → cost(l)+cost(r)+2 |
| 2-address (d ← d op s) | ops + (#ops whose first operand, after commuting `+`/`*`, is a leaf) + (1 if Z cannot be used as scratch) | |

- **Example:** W = (A+B)·(C−D)+E: stack 10, 3-address 4, load–store 10, accumulator 8, 2-address 7 (6 if W may be scratch).
- **Data-memory references:** stack = leaves + 1; load–store = loads + 1; 3-address memory = 3·ops; each 2-address ALU op = 3, MOV = 2 (read source, write destination);
  accumulator = one per instruction.
- **Misuse:** forgetting the temporary on an accumulator machine; treating the destination as free to overwrite when an input is the first operand.

### F2. Stack depth
- **Statement:** scan the postfix string: +1 per operand, −1 per binary operator; depth = the maximum running value.
- **Example:** `A B + C D + * E F + G H + * *` → maximum **4**.

### F3. Register need of an expression tree (Sethi–Ullman label)
- **Statement:** leaf = 1; op node: max(l, r) if l ≠ r else l + 1. For (A+B)·(C+D) → 3.

---

## G. Register pressure

### G1. Registers without spilling (straight-line code)
- **Statement:** R_min = max over points of max(|live-in|, |live-out|); equals the chromatic number of the interference graph for straight-line code.
- **Why:** an interval graph is perfectly colourable with its maximum clique number of colours; a destination may share a dying source's register.
- **Example:** `a=1; b=2; c=3; d=a+b; e=d*c` → 3; after moving `c=3` below `d=a+b` → 2.
- **Misuse:** counting all variables ever defined instead of simultaneously live ones; with branches, build the interference graph (pressure is only a lower bound).

---

## H. Performance

### H1. Iron law
- **Statement:** T_CPU = IC × CPI × T = IC × CPI / f.
- **Units:** IC instructions; CPI cycles/instruction; T seconds (= 1/f); f Hz.
- **Example:** 6×10⁸ instructions × 2.5 CPI / 3×10⁹ Hz = 0.5 s.

### H2. Weighted CPI
- **Statement:** CPI = Σ fᵢ·CPIᵢ with fᵢ = fraction of **instructions** (Σ fᵢ = 1).
- **Example:** 0.4·1 + 0.3·2 + 0.2·3 + 0.1·6 = 2.2.
- **Misuse:** using fractions of time as fᵢ.

### H3. MIPS
- **Statement:** MIPS = IC/(T_exec·10⁶) = f/(CPI·10⁶).
- **Example:** f = 2 GHz, CPI 2.2 → 909.1 MIPS.
- **Misuse:** ranking machines with different ISAs by MIPS.

### H4. Ratio method
- **Statement:** T₂/T₁ = (IC₂/IC₁)·(CPI₂/CPI₁)·(f₁/f₂); same program and ISA ⇒ f₂ = f₁·(CPI₂/CPI₁)/(T₂/T₁).
- **Example:** 20 % less time, 50 % more CPI, f₁ = 2 GHz → 2·1.5/0.8 = **3.75 GHz**.
- **Misuse:** "25 % less time" means ratio 0.75, "20 % more CPI" means 1.2.

### H5. Amdahl's law
- **Statement:** speedup = 1/((1−p) + p/s), p = fraction of **original time** enhanced, s = its speedup; limit 1/(1−p).
- **Example:** p = 0.6, s = 4 → 1.818; limit 2.5.
- **CPI-based version:** speedup = CPI_old/CPI_new when IC and f are unchanged: 2.125/1.625 ≈ 1.308.

### H6. CPI with memory stalls (bridge)
- **Statement:** CPI = CPI_base + (references/instruction) × miss rate × miss penalty.
- **Example:** 1.5 + 1.3·0.04·50 = 4.1. Details: [`../05-MEMORY-INTERFACING-AND-HIERARCHY/01-PERFORMANCE/`](../05-MEMORY-INTERFACING-AND-HIERARCHY/01-PERFORMANCE/).

---

## I. Byte order

### I1. Placement of a w-byte value at address a
- **Big-endian:** byte i (0 = MSB) at a + i. **Little-endian:** byte i (0 = MSB) at a + (w−1−i); equivalently LSB at a.
- **Example:** 0x12345678 at 1000: BE 12 34 56 78; LE 78 56 34 12.
- **Aligned:** address ≡ 0 (mod word size in bytes).
