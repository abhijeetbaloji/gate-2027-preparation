# Mistakes — I/O Interface and Interrupts

Common errors, grouped by type. Section "My Mistakes" at the bottom is for you to fill in; nothing there is pre-written.

## 1. Conceptual confusions

| # | Mistake | Correct idea | NOTES |
|---|---|---|---|
| 1 | "The CPU services an interrupt the moment it is raised" | It checks at the end of the current instruction (if enabled/unmasked) | §6.2 |
| 2 | "Vectored means no ISR software is needed" | Vectored removes the *search for the source*, not the ISR | §8 |
| 3 | "Daisy chain = the CPU polls the devices one by one" | The acknowledge is passed along the chain; the winning device identifies itself | §9.2 |
| 4 | "Non-vectored interrupts are polled by the CPU all the time" | The CPU is interrupted first; only the common routine then searches | §8.1 |
| 5 | "Interrupt-driven I/O is always better than polling" | For busy devices polling a ready device is cheaper than per-word interrupts | §4.4, E5 |
| 6 | "Interrupt = DMA" | An interrupt transfers control; DMA transfers data without CPU instructions | §4.3 |
| 7 | "A page fault is an I/O interrupt" | It is a synchronous fault; the saved PC is the faulting instruction | §11 |
| 8 | "Every interrupt causes a context switch" | The scheduler decides; only events that block the running process force it out | §13 |
| 9 | "Masking discards the request" | Latched requests stay pending; only IF/mask delay them | §6.6 |
| 10 | "NMI can be disabled by clearing IF" | NMI is non-maskable | §6.1 |
| 11 | "Memory-mapped I/O needs special instructions" | Isolated I/O needs them; memory-mapped uses load/store | §3 |
| 12 | "Closest to the CPU in a daisy chain = lowest priority" | Closest sees the grant first = highest priority | §9.2 |

## 2. Formula mistakes

| # | Mistake | Fix |
|---|---|---|
| 1 | Polling fraction counts only the polls that find an event | Charge c_p for every poll (rate = 1/interval), processing only for found events |
| 2 | Interrupt fraction uses entry/exit only (no ISR body) or body only | c_i = entry + save + body + restore + return |
| 3 | Max rate computed from the whole second instead of the allowed budget | λ_max = β / c with β from the question (e.g. 20 %) |
| 4 | Job time = work × (1 + f) | work / (1 − f) when f is the wall-clock share |
| 5 | Return address = interrupted address + 4 always | Add the *actual byte length*; use the target for a taken branch; faulting address for a fault |
| 6 | Cascade capacity = 8 × chips | (8 − k) + 8k = 8 + 7k with a master and k slaves |
| 7 | Vector address = n × entry size | base + n × entry size |
| 8 | Usable RAM = 2ⁿ (memory-mapped) | 2ⁿ − I/O window |
| 9 | Port bits = ⌈log₂ (used ports)⌉ with aligned blocks | ⌈log₂ D⌉ + log₂ R with R a power of two |

## 3. Numerical / calculation mistakes

- μs vs ms: 20 ms interval → 50 polls/s, *not* 0.05 or 5000.
- cycles ↔ time: 100 MHz → 10 ns/cycle, so 8 μs = 800 cycles (not 80).
- Percent vs fraction: 0.063 is 6.3 %.
- Binary vs decimal MB for device rates: state the assumption; 2²⁰ vs 10⁶ changes the answer by ≈ 4.9 %.
- Hex vs decimal when computing vector-table addresses (0x35 = 53).
- Forgetting the master input lost per slave in cascaded PICs.
- Rounding mid-way in ratio questions: round once at the end.
- Adding overheads twice (the per-interrupt cost already includes processing).
- In timeline problems, forgetting the remaining length of a preempted ISR.

## 4. PYQ-derived traps (newest → oldest; entries really in the mapping)

| Year / Q# | Trap pattern |
|---|---|
| 2026 Q.18 | Equating daisy-chain identification with CPU polling; overlooking that a non-vectored mechanism first needs software to find the source |
| 2024 CS2 Q.25 | Treating every interrupt as a forced context switch; mixing events where the *process itself* must wait with those where the OS merely gets control |
| 2023 Q.34 | Not counting the polls that find nothing; mixing ms/μs; counting processing twice on the interrupt side |
| 2018 Q.9 | Placing "load new PC" before "save status", or "pop status" before the ISR body |
| 2013 Q.28/45/34/39 (Booklets A–D) | Mistaking a sequence that stores the old PC in memory and overwrites PC for an ordinary fetch or a branch |
| 2011 Q.11 | Ranking sources by user-visible importance instead of the consequence of delay |
| 2009 Q.8 | Believing the CPU responds at once, at the end of fetch, or at fixed intervals |
| 2008 Q.64 | Confusing "the process waits" (sync/async I/O semantics) with "an ISR runs" (hardware completion handling) |
| 2007 Q.73 | Using a fixed 4-byte increment, ignoring instruction lengths and branches; trying to guess numbers when the listing is missing |

## 5. Examination-time mistakes

- Not reading the priority direction (larger-is-higher vs smaller-is-higher).
- Not noting whether nesting is enabled, or what the tie-break rule is.
- Misreading "byte-addressable" and "32-bit word" (4 bytes).
- Skipping the sanity check: fractions must be below 1 or below the stated budget.
- Not noting MSQ rules (one or more correct, no partial marks) and choosing only the first true option.
- Spending time on figure-less questions: if a listing/figure is missing in the PDF extract, open the PDF.

## 6. How to check yourself

1. Did I write the unit next to every number (μs, ms, cycles, bytes)?
2. Did I compute polls per second from the interval?
3. For a timeline: at each event, did I list the unfinished routines and their priorities?
4. Return address: instruction length in bytes, branch taken or not, fault or not?
5. Ordering: finish → save → load PC → ISR → restore, in that order?
6. Did I answer what was asked (a ratio, a percentage, a time, a count)?

---

## My Mistakes

| Date | Source | Question | Mistake | Root cause | Fix / Rule |
|---|---|---|---|---|---|
|  |  |  |  |  |  |
