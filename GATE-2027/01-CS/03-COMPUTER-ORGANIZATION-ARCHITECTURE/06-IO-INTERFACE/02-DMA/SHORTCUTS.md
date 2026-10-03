# DMA — Shortcuts

Only shortcuts that are exact under the stated assumptions. Background in [NOTES.md](NOTES.md); formulas in [FORMULAS.md](FORMULAS.md).

---

## 1. One-line rate: R = f × p × w (× 8 for bits)

- What it solves: "x MHz processor, y % of cycles used for DMA, w bytes per cycle, find the rate".
- When: DMA unit moves in one cycle; the percentage refers to the same cycle rate as f.
- Why it works: bus offers f cycles per second; p of them belong to DMA; each carries w bytes (NOTES 8.2).
- Example: f = 3 MHz, p = 1 %, w = 2 bytes: 3×10^6 × 0.01 × 2 × 8 = 480,000 bits/s (verified).
- Limitation / trap: if the unit takes k cycles divide by k; the percentage must refer to bus/processor cycles that really are the same.

## 2. Cancel the clock when the question gives a ratio

- What it solves: p = R/(f × w): the clock cancels if R and f use the same time unit; evaluate in the units given.
- Example: R = 6×10^6 B/s, bus cycle 40 ns moving 8 bytes: bus capacity = 8/40 ns = 2×10^8 B/s; p = 3 %. Quick check: R/w = 7.5×10^5 cycles/s against 2.5×10^7 offered = 3 %.
- Limitation: p > 1 means infeasible; do not report a "percentage" above 100.

## 3. Powers-of-two trick for count-register problems

- What it solves: number of bursts for a file of F KB with an m-bit count register and u-byte units.
- Rule: capacity per programming in KB = 2^(m−10) × u (valid for m ≥ 10); bursts = ⌈F / (2^(m−10) × u)⌉.
- Why it works: 2^m × u bytes divided by 2^10 gives KB with no 1024 arithmetic.
- Example: F = 600 KB, m = 12, u = 4: capacity 2^2 × 4 = 16 KB; 600/16 = 37.5; answer 38 (verified). F = 1000, m = 16, u = 1: capacity 64 KB; 15.625 -> 16.
- Limitation: ceiling always; for exact multiples state the 2^m vs 2^m − 1 convention (NOTES 4.3); for m < 10 revert to bytes.

## 4. Burst vs stealing bus-time ratio

- What it solves: how much longer the bus is occupied in cycle stealing than in burst.
- Rule: occupancy ratio = N(A + 1)/(A + N); for large N with A ≥ 0 it tends to A + 1.
- Example: N = 512, A = 2: 1536/514 = 2.99 (tends to 3).
- Limitation: assumes the same A for every acquisition and no device-limited waiting.

## 5. Max burst length from a latency limit

- Rule: N_max = ⌊L/T_b⌋ − A.
- Example: L = 1.5 µs, T_b = 60 ns, A = 2: ⌊25⌋ − 2 = 23.
- Limitation: if L/T_b is not an integer the floor is mandatory.

## 6. Break-even block size without trying values

- Rule: n_min = ⌊(S + C)/(c_int − c_st)⌋ + 1 (smallest whole n with DMA strictly cheaper).
- Example: S + C = 1200, c_int = 120, c_st = 1: 1200/119 = 10.08; n_min = 11 (n = 10: 1200 vs 1210; n = 11: 1320 vs 1211).
- Limitation: needs c_int > c_st; with a tie-allowed question ("not worse than") use the ceiling instead of floor + 1.

## 7. Slowdown from a stolen fraction

- Rule: new time = T_alone/(1 − p). Equivalent: extra time fraction = p/(1 − p).
- Example: p = 8 %: factor 1.087, extra 8.7 %, not 8 %.
- Limitation: assumes the CPU would use every cycle.

## 8. Keyword checks for statement questions

| Phrase in a statement | Valid reading |
|---|---|
| "cycle stealing ... one unit per stolen cycle" | consistent with the definition |
| "burst ... higher throughput than cycle stealing" | consistent when arbitration overhead is per acquisition (NOTES 7.3, 8.6) |
| "burst ... shorter CPU delay" | inconsistent: burst has the longer single stall |
| "both CPU and DMA drive the shared bus at the same instant" | inconsistent: one master at a time (NOTES 5.3) |
| "DMA means no interrupts" | inconsistent: completion interrupt remains |
| "daisy chain: position decides priority" | consistent |

- Limitation: "always/never/only" statements still need checking against the question's stated assumptions.

---

## Do NOT use

1. "Slowdown = p" as the CPU's extra time. Counterexample: p = 50 %: the CPU gets half the cycles, so the job takes 2× (extra 100 %), not 1.5×.
2. "Burst mode is the best mode" for a latency-bounded system: an 80-word burst of 50 ns cycles stalls the CPU for 4 µs; with a 1 µs limit it is unusable.
3. "Interrupt-driven I/O always wastes less CPU than polling": if ISR time exceeds the device period, the CPU cannot keep up; with an always-ready device polling does less work per byte.
4. "Bytes per programming = count register value": the unit size multiplies it (word units move 4 × as many bytes per count).
5. "Minimum acquisitions = ⌊file / capacity⌋": the leftover partial piece still needs a bus takeover, so use the ceiling.
6. "Percent of processor cycles = percent of bus cycles" unless the CPU and bus cycles are the same duration and the CPU uses a bus cycle every cycle.
