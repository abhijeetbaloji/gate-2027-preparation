# Memory Hierarchy Performance — SHORTCUTS

Only valid shortcuts. All examples are script-verified. Model assumptions are stated in each.

---

## S1. Hierarchical AMAT = hit time + miss ratio × (everything below)

- **What it solves:** any hierarchical single- or multi-level AMAT.
- **When:** the question says the lower level is consulted only after the upper level misses (or gives "hit time + miss penalty").
- **Why it works:** every reference pays T1; the fraction m1 that leaves L1 additionally pays the expected cost of the levels below, which has the same structure recursively.
- **Example:** 3 levels (1, 5, 30, 200 mem), h = 0.95 / 0.8 / 0.9 ⇒ innermost 30 + 0.1 × 200 = 50 ⇒ 5 + 0.2 × 50 = 15 ⇒ 1 + 0.05 × 15 = 1.75 ns.
- **Limit:** not for simultaneous access; hit ratios must be local.

## S2. Simultaneous = hierarchical − Σ T_i × P(miss through level i)

- **What it solves:** getting one model's answer from the other quickly.
- **When:** the two models are both of interest (ambiguous question, §4.2 of NOTES).
- **Why:** the simultaneous model never pays the failed lookup. One level: difference = m × T_c; two levels: m1 T1 + m1 m2 T2.
- **Example:** (T1, T2, mem) = (2, 20, 100), h = (0.9, 0.8): hierarchical 6.0, difference 0.1·2 + 0.1·0.2·20 = 0.6 ⇒ simultaneous 5.4. ✓
- **Limit:** only if both models use the same T_i values and the last level always hits.

## S3. Penalty form ↔ total-time form

- **What it solves:** switching between "penalty" and "total miss time".
- **When:** a question gives one and the formula needs the other.
- **Why:** hit time + m × P with P = T_miss_total − T_hit equals h·T_hit + m·T_miss_total.
- **Example:** hit 5, total miss 50, h = 0.8: 5 + 0.2 × 45 = 14 = 0.8 × 5 + 0.2 × 50. ✓
- **Limit:** do not confuse "miss penalty" with "total miss time"; read the wording.

## S4. Improvement per unit: ΔAMAT = Δm × P (or Δ(hit time))

- **What it solves:** "by how much does AMAT change if miss ratio changes".
- **When:** only the miss ratio (or only the penalty or hit time) changes.
- **Why:** AMAT is linear in each of T_c, m, P separately.
- **Example:** T_c = 2, P = 40, m 0.05 → 0.10 ⇒ ΔAMAT = 0.05 × 40 = 2 ns.
- **Limit:** not additive when two quantities change together (product term m × P).

## S5. Equal AMAT when m × P is the same

- **What it solves:** comparing a miss-ratio improvement with a penalty improvement.
- **When:** the hit time is the same in both designs.
- **Why:** AMAT = T_c + (m × P); the hit time is common.
- **Example:** (m, P) = (0.05, 40) vs (0.10, 20): both 2 ns of miss time ⇒ same AMAT (with T_c = 2: 4 ns).
- **Limit:** different hit times invalidate it.

## S6. Global ratio shortcut for 2 levels (hierarchical)

- **What it solves:** AMAT when global L2 miss ratio is given.
- **When:** data are m1 (L1 miss) and g2 (global L2 miss).
- **Why:** T = T1 + m1 T2 + g2 T3, no brackets needed.
- **Example:** m1 = 0.06, g2 = 0.015; T = 2, 12, 120 ⇒ 2 + 0.72 + 1.8 = 4.52 (equals 2 + 0.06(12 + 0.25 × 120)).
- **Limit:** do not multiply g2 by m1 again.

## S7. Cycles of penalty = ns × GHz

- **What it solves:** unit conversion.
- **When:** CPI questions with penalty in ns and clock in GHz.
- **Why:** cycles = time / period = time × frequency.
- **Example:** 40 ns × 2.5 GHz = 100 cycles. 75 ns at 0.8 ns clock: 93.75 → 94 cycles if whole cycles are required.
- **Limit:** apply ceiling only when the question says "whole number of cycles".

## S8. CPU slowdown from memory = stall fraction

- **What it solves:** speedup with perfect cache.
- **When:** CPI_base excludes miss stalls.
- **Why:** time ratio = CPI_eff / CPI_base.
- **Example:** CPI_base = 1.6, stalls 2.6 ⇒ 4.2 / 1.6 = 2.625; removing 60 % of misses: 4.2 / (1.6 + 1.04) = 1.59.
- **Limit:** same clock and IC in both machines.

## S9. Chips = total bits ÷ chip bits (when shapes divide)

- **What it solves:** chip count.
- **When:** the memory and chip dimensions divide evenly in both directions.
- **Why:** each bit of the memory comes from a unique chip bit.
- **Example:** 256 K × 16 from 32 K × 4 ⇒ (256 K · 16) / (32 K · 4) = 32 ✓.
- **Limit:** if the chip is wider than the system's data bus, or a dimension does not divide, use ⌈⌉ per dimension; and it does not give decoder sizes.

## S10. Decoder inputs = log₂(M / K)

- **What it solves:** decoder size.
- **When:** rows of chips, full decoding.
- **Why:** high-order bits not needed inside the chip select the row.
- **Example:** 64 K / 16 K = 4 rows ⇒ 2-to-4.
- **Limit:** the select bits may not be the top ones (NOTES §6.3).

## S11. Block start for non-top select bits = select value << position

- **What it solves:** the lowest address of each memory block.
- **When:** the decoder input bits are at A_p…A_q.
- **Why:** with every other bit 0, only the select bits contribute to the address.
- **Example:** select = A6A5: blocks 0,1,2,3 start at 0, 32, 64, 96.
- **Limit:** valid only if internal address bits are the remaining ones.

## S12. Refresh overhead = rows × t_row / T

- **What it solves:** % time lost.
- **When:** all chips refresh in parallel.
- **Why:** each refresh operation takes t_row of memory time; rows operations per period.
- **Example:** 4096 × 50 ns / 32 ms = 0.64 % ⇒ 99.36 % available.
- **Limit:** serial refresh multiplies by the number of serial groups.

## S13. Banks for full rate = ⌈t_m / t_b⌉

- **What it solves:** minimum number of interleaved banks.
- **When:** staggered starts, one-word bus.
- **Why:** a bank can be restarted after t_m; the bus consumes a word every t_b.
- **Example:** 60 ns / 15 ns = 4.
- **Limit:** stride patterns that skip banks need more or fewer; a prime bank count helps.

---

## Do NOT use

1. **"AMAT = h × T_cache + m × T_memory is always right."** It is the simultaneous model. For "first checks the cache then the memory" it is wrong by m × T_cache.
   Counterexample: T_c = 5, T_m = 50, h = 0.8: 14 vs 15.
2. **"Average of the hit times of I-cache and D-cache."** Weights are the access mix: 70 %/30 % of 2.8/3.7 gives 3.07, not 3.25.
3. **"Hit ratio = 1 − miss ratio of the next level."** The L2 hit ratio is conditional; the overall fraction served by L2 is m1 × h2.
4. **"Fewer misses ⇒ faster."** If the hit time or clock gets slower, the total time can get worse (Example 5.2 of NOTES with clock changes).
5. **"More banks always means more bandwidth."** Bandwidth saturates at the bus rate, and strides with large gcd defeat banks.
6. **"Block start address = block number × block size."** True only for top-bit select (contiguous) layouts.
7. **"Bandwidth = word size / access time."** For a burst it is block bytes / (first-word latency + remaining words); for repeated random accesses use the cycle time.
