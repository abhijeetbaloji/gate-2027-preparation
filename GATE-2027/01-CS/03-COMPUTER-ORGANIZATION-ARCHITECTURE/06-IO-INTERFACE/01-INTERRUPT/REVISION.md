# Revision — I/O Interface and Interrupts

## Key definitions
- **I/O module:** status (ready/busy/error), control (start, IE), data registers; each is a **port**.
- **Memory-mapped I/O:** ports in the memory address space, ordinary load/store, loses RAM addresses, region uncacheable.
  **Isolated I/O:** separate port space, `IN`/`OUT`, memory space intact, extra control signal.
- **Programmed I/O (polling):** CPU loops on status. **Interrupt-driven:** device raises IRQ, CPU runs ISR per word.
  **DMA:** controller moves the block; CPU gets one completion interrupt ([`../02-DMA`](../02-DMA/NOTES.md)).
- **Interrupt:** async, from a device → saved PC = *next* instruction. **Trap:** sync, intentional (syscall) → next instruction.
  **Fault:** sync, recoverable (page fault, divide error) → saved PC = the *faulting* instruction.
- **Vectored:** device supplies the identifier → direct ISR. **Non-vectored:** one common entry, software finds the source.
- **Maskable:** controlled by IF/mask. **NMI:** cannot be masked.

## Sequence (memorise)
```
 IRQ -> finish current instruction -> accept (IF=1, not masked) -> INTA/vector
     -> hardware saves PC (+flags) -> PC <- ISR entry -> ISR saves regs -> service device
     -> restore regs -> IRET (pop flags, PC) -> resume
```
Anchors: instruction finishes first; save before load PC; restore last.

## Must-remember formulas
```
 fraction = rate × cost                     λ_max = β / cost
 polling  = (1/T_p)×c_poll + λ×c_proc       interrupt = λ × c_int
 min poll rate ≥ λ / buffer_items           crossover λ* = f_p c_p / (c_int − c_proc)
 stretch  = work / (1 − fraction)
 vector entry address = base + n × entry_size ; table size = N × entry_size
 active = pending AND NOT mask               cascade lines = 8 + 7k
 priority levels = high − low + 1
 usable RAM = 2ⁿ − I/O window                port bits = ⌈log₂ D⌉ + log₂ R
```

## Table: schemes for many devices
| Scheme | Source found by | Priority from |
|---|---|---|
| Software poll | CPU software | poll order |
| Daisy chain | device on grant (no CPU poll) | physical position (closest first) |
| Parallel + encoder | hardware | encoder / mask |
| Cascaded PIC | PIC supplies vector | programmed |

## Fast-solve checklist
1. Interrupt "when?" → end of current instruction.
2. Ordering → three anchors.
3. Return address → next-instruction address; branch target; fault → same instruction.
4. Numerics → convert to μs/s; poll rate = 1/interval; include polls that find nothing.
5. Nested timeline → strictly higher preempts; equal waits; resume most recent unfinished; apply tie-break.
6. Priority "who first?" → critical hardware > deadline-bound devices > human-speed devices.

## Top traps
- "Handled immediately" / "at end of fetch" / "at fixed intervals" — all wrong.
- Daisy chain ≠ CPU polling; vectored ≠ no software.
- Interrupt not always cheaper than polling (busy device).
- Equal priority does not preempt; priority direction from the question.
- Saved PC for a fault is the faulting instruction.
- Units: μs vs ms; cycles → seconds.
- Not every interrupt causes a context switch.

## Concepts seen in mapped PYQs (evidence: [`PYQ.md`](PYQ.md))
When an interrupt is serviced; event ordering; return address; interrupt-entry micro-operations; polling vs interrupt CPU-time ratio;
which source has highest priority; vectored vs non-vectored and daisy-chain statements; sync/async I/O statements; context-switch
consequences of interrupts (partly OS).
