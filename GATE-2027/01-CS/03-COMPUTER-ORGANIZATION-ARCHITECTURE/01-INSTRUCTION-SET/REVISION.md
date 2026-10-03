# Instruction Set — Last-minute Revision

Details: [`NOTES.md`](NOTES.md) · formulas: [`FORMULAS.md`](FORMULAS.md). 1 K = 2¹⁰.

## Definitions in one breath
- **ISA** = programmer-visible contract: opcodes/formats, architectural registers, addressing modes, word size/endianness/alignment.
  **Not ISA:** clock, cache size/levels, pipeline depth, hardwired vs microprogrammed, number of ALUs.
- **Fetch:** MAR←PC; MDR←M[MAR]; PC←PC+size; IR←MDR. Memory refs per instruction = 1 fetch + operand refs.
- **Styles:** stack 0-address · accumulator 1-address · 2-address (d←d op s, destination destroyed) · 3-address · load–store (only LOAD/STORE touch memory, ALU on registers).
  An *implied* operand (ACC, top of stack) is not named by any address field.
- **RISC:** fixed length, load/store, register–register ALU, few modes, many registers, usually hardwired, higher IC / lower CPI. **CISC:** the opposite.

## Must-remember formulas
```
bits to name n things     = ceil(log2 n)            (24 regs->5, 40->6, 64->6, 65->7)
max immediate             = L - opcode - sum(register fields) - other fixed fields
program size (byte-aligned)= N x ceil(b/8)           (not ceil(N*b/8))
format-bit opcode         = 1 + ceil(log2 larger type);  equal split => ceil(log2 total)
opcode length of a type   = L - operand bits of that type
max opcodes of target T   = floor( 2^oT - sum n_i * 2^(oT - o_i) )     (add fractions, floor once)
chain 3->2->1->0 address  : S_next = (S_now - used) * 2^w
CPU time = IC x CPI x T = IC x CPI / f ;  CPI = sum f_i CPI_i ;  MIPS = f/(CPI x 10^6)
ratio method (same IC):   f2 = f1 x (CPI2/CPI1) / (T2/T1)
Amdahl: 1/((1-p) + p/s)  (p = fraction of original TIME)
```

## Counting table for Z = expr (leaves distinct)
| Machine | Instructions |
|---|---|
| Stack | leaves + ops + 1 |
| 3-address | ops |
| Load–store | loads + ops + 1 |
| Accumulator | cost(root)+1; both children complex ⇒ +2 (STORE temp + use) |
| 2-address | ops + MOVs (first operand a leaf) [+1 if Z cannot be scratch] |

## Cake picture (expanding opcodes)
```
2^L patterns; an opcode of length o owns 2^-o of them. Used slices must sum to <= 1.
  Example: o_A = 3 (5 used), o_B = 5 (9 used), target o_C = 7
     slots of 7-bit unit:  128 total
                           - 5 * 2^(7-3) = 80   (A)
                           - 9 * 2^(7-5) = 36   (B)
                           = 12 left for C
  Convert everything into the TARGET's slot unit, subtract, floor once.
```

## Fast-solve checklist
1. Draw the instruction boxes; count register fields in the given shape.
2. ⌈log₂⌉ each field separately; subtract from L.
3. Several formats? format bit (flat vs larger type) or expanding opcodes (cake rule)?
4. Byte-aligned? round **per instruction**.
5. Counting machine code? write the code, then count; state if inputs may be overwritten / whether the destination can be scratch.
6. Performance? iron law; fractions are of **instructions** for CPI, of **time** for Amdahl.

## Top traps
- 64 registers ≠ 64 bits; non-powers of two need ⌈ ⌉.
- Wrong number of register fields; forgetting an UNUSED/mode field.
- Rounding program size once; unequal split with a format bit; flooring each type separately.
- Scaling: subtract n_i × 2^(o_T − o_i), not n_i.
- Accumulator machine needs a STORE when two complex operands; stack machine pushes repeated variables again.
- ALU instruction with a memory operand is not load–store; STORE operand order follows the destination-first convention.
- MIPS ≠ speed across ISAs; frequency/cache/pipeline depth are not ISA.
- Code segment of the 2013 spill questions is absent from the mapping text — method only (live ranges, interference graph, code motion).

## High-frequency PYQ concepts (from the mapping)
Instruction-field arithmetic (2016 ×2, 2020, 2024, 2025, 2026), expanding opcodes (2020, 2026), load–store sequence (2026), address-field semantics (2015), register allocation/spills (2013). Related ones filed under other leaves: RISC characteristics (2018), ISA membership (2025), opcodes per mode (2024), mixed-register-file opcodes (2018).
