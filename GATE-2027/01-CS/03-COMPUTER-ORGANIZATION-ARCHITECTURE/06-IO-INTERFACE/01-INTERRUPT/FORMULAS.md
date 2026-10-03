# Formulas — I/O Interface and Interrupts

Conventions: 1 K = 2¹⁰ etc. for memory; rates and clocks as given (plain numbers); costs in **seconds** (convert μs → 10⁻⁶ s,
cycles → cycles / f). Fractions are "CPU seconds per wall-clock second". See [`NOTES.md`](NOTES.md) for derivations in context.

---

## A. I/O addressing

### F1. Usable RAM with memory-mapped I/O
```
 usable RAM addresses = 2ⁿ − W
```
- n = address bits; W = size of the reserved I/O window (bytes, byte-addressable).
- Applies only to **memory-mapped** I/O. Isolated I/O leaves 2ⁿ untouched.
- Why: every address claimed by a device decoder cannot also select RAM.
- Example: n = 32, W = 4 KB → 4 294 963 200 bytes. Misuse: subtracting the number of *registers* instead of the size of the window when each device decodes an aligned block.

### F2. Port-address bits (aligned blocks)
```
 port bits = ⌈log₂ D⌉ + log₂ R        D = number of controllers, R = ports per controller (power of two, aligned)
```
- Applies when each controller decodes an aligned block of R ports. If ports are numbered contiguously with no
  alignment, bits = ⌈log₂ (total ports)⌉.
- Example: D = 40, R = 8 → 6 + 3 = 9 bits (contiguous 320 ports would also give ⌈log₂ 320⌉ = 9, but 40 × 6 = 240 contiguous gives 8 — alignment matters).
- Misuse: using ⌈log₂ (D × registers-used)⌉ when R is not a power of two.

---

## B. CPU-time (fraction) formulas

### F3. Activity fraction
```
 fraction = rate (events/s) × cost (s/event)
```
- Units: rate in s⁻¹, cost in s. Result dimensionless; × 100 for percent.
- Why: in one second there are `rate` events, each uses `cost` CPU seconds.
- Misuse: using a per-event cost that already includes another term, then adding that term again.

### F4. Polling fraction
```
 f_poll = f_p × c_p + λ × c_e        f_p = 1/T_p (polls/s)
```
- c_p = CPU cost of one poll; λ = event rate; c_e = processing per found event.
- Assumes every poll costs c_p regardless of whether it finds an event; processing only for found events.
- Example: T_p = 20 ms, c_p = 50 μs, λ = 1/s, c_e = 400 μs → 50 × 50 μs + 400 μs = 2900 μs/s = 0.29 %.
- Misuse: counting only the polls that succeed.

### F5. Minimum polling rate (no overrun)
```
 f_p ≥ λ / B        equivalently  T_p ≤ B / λ
```
- B = items the device can buffer; λ = items/s produced. For B = 1: poll at least as often as events arrive.
- Why: the buffer fills in B/λ seconds; a poll within that time can empty it.
- Example: B = 16 bytes, λ = 4000 B/s → T_p ≤ 4 ms, f_p ≥ 250 polls/s.

### F6. Interrupt fraction
```
 f_int = λ × c_i                  c_i = entry + register save + ISR body + restore + return
```
- Applies to each interrupt source; for several sources, **add** the fractions (F7).
- Example: 5000 /s × 12 μs = 6 %.

### F7. Total interrupt load
```
 f_total = Σ over sources (λ_k × c_k)       must be < 1 (strictly less, with room for the main program)
```
- Example: 100 /s × 200 μs + 250 /s × 100 μs = 20 ms + 25 ms = 45 ms/s = 4.5 %.

### F8. Per-interrupt cost from cycles
```
 c_i (cycles) = hardware entry + (registers saved × cycles per save) + ISR body
                + (registers restored × cycles per restore) + return
 c_i (s)      = cycles / f_clock
```
- Example: 20 + 12×2 + 300 + 12×2 + 20 = 388 cycles at 1 GHz = 0.388 μs.
- Misuse: forgetting the restore half, or counting registers saved per cycle instead of cycles per register.

### F9. Maximum sustainable rate for a CPU budget
```
 λ_max = β / c          β = allowed CPU fraction (β = 1 for the whole CPU), c = CPU seconds per event
```
- Example: 20 % budget, 25 μs per interrupt → 0.20 / 25 μs = 8000 /s.
- With several sources, subtract the other sources' fractions from β first.

### F10. Crossover rate (polling vs interrupts)
```
 λ* = f_p × c_p / (c_i − c_e)
```
- c_i = total interrupt cost per event (includes the processing c_e); polling is charged c_e per found event too, so c_e cancels.
  If the problem says "ignore processing", c_i − c_e is simply the interrupt overhead.
- Below λ*, interrupts consume less CPU; above λ*, polling does.
- Example: poll fraction 3 % (T_p = 100 μs, c_p = 3 μs), interrupt overhead 40 μs → λ* = 0.03 / 40 μs = 750 /s.

### F11. Wall-clock stretch of a job
```
 time = work / (1 − f_total)
```
- f_total is the share of **wall-clock** time spent in interrupt/polling work. Example: 6 % → 10 s becomes 10.638 s.

### F12. DMA fraction (preview)
```
 f_dma = (R / S) × (c_setup + c_completion)       R = device bytes/s, S = block size (bytes)
```
- Example (NOTES E5): R = 400 000 B/s, S = 2048 B → 195.3125 blocks/s × 16 μs = 0.3125 %.

---

## C. Interrupt mechanics

### F13. Return (saved) address
```
 external interrupt or trap :  saved PC = address of interrupted instruction + its length   (fall-through)
                               saved PC = branch/jump/call target                            (if it was taken)
 fault (e.g. page fault)    :  saved PC = address of the faulting instruction itself
```
- Length in **bytes** for byte-addressable memory (a 32-bit word = 4 bytes).
- Example: instruction at 1204 of length 6 → saved PC 1210; a taken `CALL 1500` at 1210 → saved PC 1500.

### F14. Latency, response, and the deadline condition
```
 latency  = (longest non-interruptible stretch) + hardware entry
 response = latency + software save + ISR up to the "critical" action (+ rest of ISR + restore for full service time)
 deadline: latency + time to critical action  ≤  device overrun time
```
- Example: (120 + 40 + 12) cycles at 200 MHz = 0.86 μs.
- Definitions vary; state yours. Conservative bound adds the two worst cases even if they cannot coincide.

### F15. Interrupt vector table address
```
 address(entry n) = B + n × e          table size = N × e
```
- B = table base (bytes), n = vector number, e = entry size (bytes), N = number of vectors.
- Example: B = 0x4000, e = 8, n = 42 → 0x4150. 256 × 4 B = 1 KB.
- Misuse: using n × e without the base; mixing hex and decimal.

### F16. Pipelined flush cost (concept)
```
 refill cycles per interrupt ≈ k − 1       (k-stage pipeline, younger instructions squashed and refetched)
```
- Add to entry + ISR cycles. Often ignored unless the question states it.

---

## D. Priority and multiple devices

### F17. Number of priority levels
```
 levels = high − low + 1        (inclusive integer range)
```
- 0…7 gives 8.

### F18. Preemption condition (nesting enabled)
```
 preempt  ⇔  priority(new) strictly higher than current level  (and the interrupt is not masked, IF = 1)
```
- Equal → waits. Direction of "higher" is defined by the question.

### F19. Active request selection (parallel scheme)
```
 active = pending AND NOT(mask)        winner = highest-priority set bit of `active`
```
- Example: pending 1100 1010, mask 1000 0010, IR0 highest → active 0100 1000 → IR3.

### F20. Daisy-chain grant delay
```
 delay to device k = k × d        (d = pass-through delay per device, device 1 nearest the CPU)
```
- Example: d = 10 ns, k = 8 → 80 ns. Total chain wait grows linearly with chain length.

### F21. Cascaded PIC capacity
```
 lines = (8 − k) + 8k = 8 + 7k        one master (8 inputs), k slaves each using one master input
 chips needed for n lines: k = ⌈(n − 8)/7⌉ (for n > 8), chips = k + 1
```
- Example: n = 20 → k = ⌈12/7⌉ = 2 → 3 chips (capacity 22). Maximum with 8 slaves: 64 lines.
- Assumes single-level cascade and 8-input chips.

### F22. Nested-ISR timeline invariants
```
 busy period with no idle gap:  last finish = first arrival + Σ (ISR lengths + overheads)
 a preempted routine resumes only after every higher-priority unfinished routine has completed
```
- The sum rule is valid only if the CPU never idles between the first arrival and the last finish; check arrival times against the running finish time.
- Individual finish times still need the timeline (NOTES §10.3); only the *last* finish is given by the sum.
- Example (NOTES E15): busy 0–15, finish times B = 7, C = 11, A = 15.
