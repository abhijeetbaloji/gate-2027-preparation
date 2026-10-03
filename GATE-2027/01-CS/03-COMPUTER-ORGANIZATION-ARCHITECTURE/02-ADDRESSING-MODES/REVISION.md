# Addressing Modes — REVISION (last minute)

Full detail: [NOTES.md](NOTES.md). Convention: byte-addressable unless stated; K = 2¹⁰; PC already points to the next instruction.

## Definitions
- **Operand** = the data. **EA** = memory address of the operand. Immediate and register operands have **no EA**.
- Mode = rule combining instruction bits with registers / PC / memory to find the operand.

## Mode table
| Mode | EA / operand | Data refs | HLL |
|---|---|---|---|
| Immediate | operand = k | 0 | constant |
| Register | operand = Rn | 0 | register variable |
| Direct | EA = k | 1 | global variable |
| Indirect | EA = M[k] | 2 (L levels: L+1) | pointer in memory |
| Register indirect | EA = Rn | 1 | pointer in register |
| Auto-inc (Rn)+ | EA = Rn(old); Rn += s | 1 | `*p++`, pop |
| Auto-dec -(Rn) | Rn −= s; EA = Rn(new) | 1 | `*--p`, push |
| Displacement d(Rn) | EA = Rn + d | 1 | record field, local |
| Base + index | EA = Rb + Ri | 1 | array element |
| Scaled | EA = Rb + Ri×s + d | 1 | element of 2/4/8-byte array |
| PC-relative | EA/target = PC_updated + d | 1 (data) | branches, position-independent code |
| Implied | fixed by opcode | 0 | accumulator, stack, flags |

## Formulas
```
 branch target = PC_updated + sext(field) × L       PC_updated = branch address + its length
 n-bit signed range: −2^(n−1) … 2^(n−1)−1           PC-relative reach: −2^(n−1)·L … (2^(n−1)−1)·L
 opcode bits = L_instr − mode − register fields − literal ;  opcodes per mode = 2^(opcode bits)
 direct reach = 2^a units ;  &A[i] = base + (i−lb)×size ;  row-major &M[i][j] = base + ((i−r0)×C + (j−c0))×size
 total refs = fetches + pointer reads + operand reads + stores     (registers/immediates = 0)
```

## Diagram
```
 indirect:  instr.k ──► M[k] = pointer ──► M[pointer] = operand      (2 data reads)
 reg-ind:   Rn ──► M[Rn] = operand                                  (1 data read)
 scaled:    Rb + Ri×s + d ──► M[EA] = operand                       (1 data read, adder + shifter)
 PC-rel:    branch @A, len L → PC = A+L → target = A+L + off×L
```

## Fast-solve checklist
1. Write the EA formula. 2. Plug in current register values. 3. Follow pointers. 4. Apply side effects. 5. Count references (fetch first!). 6. State assumptions.

## Top traps
- Post-increment uses the old value; pre-decrement the new value; step = operand size.
- Indirect = extra memory read per level; total includes instruction fetch.
- PC-relative: add to the **updated** PC; sign-extend; scale by instruction length.
- Direct mode is bounded by the address-field width; register-based modes are not.
- Names vary by book: classify by register count + constant + scale.
- Separate mode field ⇒ opcodes per mode = 2^(opcode bits) (do not divide by modes).
- Auto-increment ≠ relocation; PC-relative and base-register are.

## Evidence-based high-frequency concepts
- Matching constructs ↔ modes (2026 Q.14); naming `d(R)` (2011 Q.21); field-budget opcodes per mode (2024 Q.57); auto-increment statements (2008 Q.33, filed under ALU).
- Existing practice stresses: EA computation, PC-relative targets, access counting.
