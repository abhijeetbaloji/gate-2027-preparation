# Shortcuts — I/O Interface and Interrupts

Only valid shortcuts. Each states when it is safe. See [`NOTES.md`](NOTES.md) for the underlying reasoning.

---

## S1. "μs per second" bookkeeping

- **What it solves:** every CPU-fraction question (polling, interrupts, DMA).
- **When to use:** rates in events/s and costs in μs.
- **Why it works:** rate × cost(μs) gives microseconds of CPU per second; one second is 10⁶ μs, so
  `percent = (rate × cost in μs) / 10 000`. No unit conversion errors.
- **Example:** 250 interrupts/s × 40 μs = 10 000 μs/s → 10 000 / 10 000 = **1 %**. Another: 150 000 /s × 0.42 μs =
  63 000 μs/s → **6.3 %**.
- **Limitation:** costs given in cycles must first be converted: μs = cycles / (f in MHz).

## S2. Poll rate = 1 / interval, before anything else

- **What it solves:** polling fractions where the question gives a *period*.
- **When:** "polls every 20 ms" → write 50 polls/s immediately.
- **Why:** fraction = polls per second × cost per poll; the period is the inverse of the rate.
- **Example:** 20 ms, 50 μs/poll → 50 × 50 = 2500 μs/s.
- **Trap:** these polls happen every second even if only one event arrives — don't scale by the event count.

## S3. Ratios: cancel the common second

- **What it solves:** "ratio of polling to interrupt CPU use".
- **When:** both fractions refer to the same 1 s (or same interval).
- **Why:** each fraction = (μs per second)/10⁶, so the ratio equals the ratio of the μs-per-second numbers.
- **Example:** 2900 μs/s vs 1500 μs/s → 2900/1500 = 1.93.
- **Limitation:** both numerators must be in the same unit and per the same time base.

## S4. Max rate = budget / cost

- **What it solves:** "maximum interrupt rate for ≤ x % CPU".
- **When:** one source; or after subtracting other sources' fractions from x.
- **Why:** fraction = λ × c ≤ β ⇒ λ ≤ β / c.
- **Example:** 20 %, 25 μs → 0.2 / 25 μs = 8000 /s; with another source using 4 %, budget left 16 % → 6400 /s.
- **Trap:** using the cost without the entry/exit overhead; leaving out other devices.

## S5. Return address by adding sizes

- **What it solves:** "address pushed when an interrupt occurs during instruction X".
- **When:** external interrupt or trap, instruction list with byte-sized lengths.
- **Why:** the instruction completes, so the saved PC is the next-instruction address = address + length — or the target if X is a taken control transfer.
- **Example:** `ADD` at 1204 of length 6 → 1210; a taken `JMP 1200` → 1200.
- **Limitation:** for a fault (page fault, divide error) it is X's own address. If the listing is not shown (as in one mapped entry), you cannot compute it.

## S6. Ordering questions by two anchors

- **What it solves:** order-of-events options.
- **When:** list contains "finish instruction", "save status", "load new PC", "run ISR", "restore status".
- **Why:** (1) the current instruction finishes **first**; (2) the old PC/status must be saved **before** PC is overwritten; (3) restore is **last** after the ISR body. Any option violating one anchor is out.
- **Limitation:** assumes hardware-saved PC with a vectored/fixed ISR entry; if a question says the ISR saves the registers, treat that as part of the ISR body.

## S7. Active-request selection

- **What it solves:** which line wins with a mask.
- **When:** pending register and mask given as bit strings.
- **Why:** a masked request is ignored; compute `pending AND NOT mask` then pick the highest-priority set bit.
- **Example:** pending 0110 1101, mask 0100 0001 (1 = masked), IR0 highest → active 0010 1100 → **IR2** (without the mask it would have been IR0).
- **Trap:** forgetting to apply the mask first.

## S8. Cascade capacity

- **What it solves:** how many 8-input PICs for n sources.
- **When:** one master, k slaves, each slave on one master input.
- **Why:** each slave replaces one direct input by 8: lines = 8 + 7k.
- **Example:** n = 20 → 8 + 7k ≥ 20 → k = 2 → 3 chips.
- **Limitation:** single-level cascade only; chip with other input counts changes the constants.

## S9. Last finish in a contiguous busy period

- **What it solves:** "when does the last (lowest-priority) ISR finish / when does the main program resume?"
- **When:** no idle gap between the first arrival and the last finish (every later arrival happens before the CPU would have gone idle).
- **Why:** the CPU is always busy with some ISR, so the busy period lasts Σ lengths.
- **Example:** lengths 5, 4, 2 with arrivals 0, 2, 3 → CPU busy from 0 to 5+4+2 = 11, so the last finish = 11 (simulation confirms: finishes C = 5, B = 8, A = 11).
- **Limitation:** gives only the *last* finish, not intermediate ones; fails if the CPU idles in between.

## S10. Eliminate options with a single physical fact

- "Daisy chain": the grant is passed through devices, so **no CPU poll** → eliminates options that say the CPU polls all devices.
- "Vectored": the device/controller supplies an identifier → eliminates "common routine must search".
- "NMI": cannot be masked → eliminates options that say IF = 0 blocks NMI.
- "Memory-mapped I/O": ordinary load/store, no extra instructions, loses address space.

---

## Do NOT use

| Tempting shortcut | Why it fails (counterexample) |
|---|---|
| "Interrupts are always cheaper than polling." | A device producing 100 000 words/s: polling 0.6 μs/word = 6 % but 3 μs/interrupt = 30 % (NOTES E5). |
| "Add the sum of ISR lengths to get each ISR's finish." | Intermediate finishes depend on preemption order; only the last finish equals the sum (S9), and only without idle gaps. |
| "Priority = closer to CPU = lower number" with any convention. | The direction of "higher priority" is defined by the question; in the daisy chain "closest = highest" is a statement about **grant order**, not about numbers. |
| "Return address = interrupted instruction address + 4." | Valid only for fixed 4-byte instructions that fall through; fails for variable length, taken branches and faults. |
| "Wall-clock job time = work × (1 + fraction)." | Use work / (1 − fraction) when the fraction is a share of wall-clock time (6 % → ×1.0638, not ×1.06). |
| "Equal priority preempts / equal priority is simultaneous." | Preemption requires strictly higher priority; ties wait and obey the stated tie-break rule. |
| "Masked interrupt is lost." | Level-triggered or latched requests stay pending; edge-triggered duplicates may merge. |
