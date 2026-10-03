# DMA — Common Mistakes

Concepts: [NOTES.md](NOTES.md). Formulas: [FORMULAS.md](FORMULAS.md). Practice: [PRACTICE.md](PRACTICE.md).

## 1. Conceptual confusions

| Mistake | Correct picture |
|---|---|
| "DMA means no interrupts" | One completion (and error) interrupt per block remains; per-unit device readiness goes to the controller as DREQ |
| "Cycle stealing stops the CPU for the block" | The CPU loses one bus cycle per stolen cycle and runs in between; holding the bus for the whole block is burst mode |
| "Burst is always better" | Better DMA throughput, worse worst-case CPU stall; unusable under a stall limit |
| "Transparent mode is fast" | Zero CPU delay but DMA gets only idle cycles; no throughput guarantee |
| "CPU and DMA can master the bus together" | One master at a time on a shared bus; the CPU can only do bus-free work during DMA tenure |
| "Interrupt-driven I/O is always better than polling" | Depends on ISR time vs device period; claims need their assumptions |
| "DMA is for slow devices" | DMA is for bulk/fast transfers; slow rare devices stay with PIO/interrupts |
| "Write-through cache fixes DMA coherence" | Only the output direction (memory already current); input still needs invalidation |
| "DMA uses virtual addresses" | Physical addresses; pages pinned |
| "Address register width depends on block size" | It depends on memory size; the count register depends on block size |

## 2. Formula mistakes

- Using R = p × f without the bytes per cycle w, or with w taken from the device width instead of the bytes moved per bus cycle.
- Forgetting k = 2 for detached (store-and-forward) DMA on a shared bus.
- Slowdown as p instead of 1/(1 − p).
- Burst occupancy as N (omitting A) and stealing as N (omitting A per unit).
- Break-even with the stolen cycles omitted from the per-byte DMA cost, or rounding instead of floor + 1.
- Bursts = file/capacity without the ceiling.
- Sustained bandwidth taken as peak; address cycle counted per word on a multiplexed burst.

## 3. Numerical / calculation mistakes

- Bits vs bytes: the final ×8 forgotten (or applied twice).
- KB as 1000 instead of 1024 in count-register problems; 2^m in units vs bytes (word size multiplier ignored).
- 2.5 % entered as 0.25 or 25; MHz as 2^20.
- ns/µs conversions in stall limits: 1.5 µs = 1500 ns.
- Dividing by the wrong clock when the CPU cycle and bus cycle differ.
- Reporting p > 100 % instead of "infeasible".
- Floor instead of ceiling when counting acquisitions or programmings; ceiling instead of "floor + 1" at an exact tie.

## 4. PYQ-derived traps (kinds of questions that exist in the mapping)

Years and numbers are those in the [mapping file](../../../13-PYQ-TOPIC-MAPPING/03-COMPUTER-ORGANIZATION-ARCHITECTURE/06-IO-INTERFACE/02-DMA/questions.md). The mapping lists no verified answers.

| Year / Q# | Kind | Trap pattern |
|---|---|---|
| 2024 CS1 Q.15 | Statement set mixing DMA modes, programmed vs interrupt I/O, vectored vs non-vectored interrupts | Each option is a separate fact from a different part of the syllabus; one option is about CPU utilisation (CPU view) and another about throughput (bus view); read words carefully |
| 2024 CS2 Q.11 | Rate from clock, percent of cycles, bytes per cycle, asked in bits per second | Bytes vs bits; unit moved per cycle; the percent is of processor cycles |
| 2022 CS Q.17 | Best mechanism for bulk disk-to-memory transfer | Distinguish throughput from simplicity and CPU involvement |
| 2021 CS Set-2 Q.20 | Rate with a one-character-per-cycle DMA at a stated percent of a 2 MHz clock, asked in bits per second | The "character" is 8 bits; percent given as a decimal fraction; NAT, no options |
| 2020 CS Q.3 | Four statements across daisy chaining, vectored interrupts, polling and DMA bus mastership | Statements from different topics tested one by one; one of them is about who owns the bus when |
| 2016 CS-1 Q.31 | Count register width, file size in KB, byte-addressable memory: number of bus acquisitions | KB = 1024; unit size; ceiling; interpreting "minimum number of times the controller gets the bus" |

## 5. Examination-time mistakes

- Skipping the unit line "bytes per cycle" and multiplying numbers blindly.
- Not stating an assumption (count register convention, cycle = bus cycle) when the question leaves it open.
- Spending time on statement options in order instead of eliminating the obviously wrong ones (definitions of the modes).
- Mixing two topics in one statement (interrupt vs DMA) and applying the wrong rule.
- Not checking p ≤ 1.

## 6. How to check yourself

- [ ] Did I write w (bytes per bus cycle) and k (cycles per unit) before multiplying?
- [ ] Did I use the clock the percentage refers to?
- [ ] Did I convert to bits/bytes as the answer requires?
- [ ] KB -> bytes with 1024? Ceiling where counting acquisitions?
- [ ] Is p ≤ 1?
- [ ] Is each statement answer based on a definition, not on a vague memory?
- [ ] For burst vs stealing, did I include A and distinguish throughput from worst-case stall?

---

## My Mistakes

| Date | Source | Question | Mistake | Root cause | Fix / Rule |
|---|---|---|---|---|---|
|  |  |  |  |  |  |
|  |  |  |  |  |  |
|  |  |  |  |  |  |
