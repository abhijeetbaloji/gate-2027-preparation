# Memory Hierarchy Performance — MISTAKES

Typical errors for this topic, with the fix. The "My Mistakes" table at the end is for you; it is intentionally empty.
See [`NOTES.md`](NOTES.md) for the correct treatment and [`PRACTICE.md`](PRACTICE.md) for questions that exercise each trap.

---

## 1. Conceptual confusions

| # | Mistake | Why wrong | Fix |
|---|---|---|---|
| C1 | "Associativity removes all misses except compulsory." | Capacity misses remain when the working set exceeds the cache (also in a fully associative cache). | Remember the three C's (NOTES §1.3). |
| C2 | "A smaller block gives better spatial locality / lower miss rate." | Smaller blocks capture less spatial locality; they only reduce the *penalty* and the number of useless bytes. | NOTES §1.4. |
| C3 | "Write-through needs a dirty bit." | Memory is always current; nothing to write back on eviction. | NOTES §4.7 table. |
| C4 | "A write buffer cuts the amount of memory writes." | It hides latency; traffic is unchanged. | Practice Q18. |
| C5 | "A read miss never writes memory." | In write-back caches the victim may be dirty. | NOTES §4.7. |
| C6 | Treating access time and cycle time as the same. | Cycle time ≥ access time; the rate is 1 / cycle time. | Practice Q3. |
| C7 | "Inclusion needs write-through / higher associativity." | These are design means, not logical requirements; the necessary part is L2 ≥ L1 in capacity (plus block size) and a mechanism to keep the contents nested. | NOTES §1.5. |
| C8 | "AMAT tells the worst-case time of an access." | AMAT is an average over many references. | State the meaning in the answer. |
| C9 | "More interleaved banks always means higher bandwidth." | The bus rate and the stride pattern limit it. | NOTES §3.3–3.4. |
| C10 | Mixing up "hit ratio of L2 as quoted" (local) with the fraction of all references served by L2. | The local ratio is conditional on an L1 miss. | NOTES §4.4. |

## 2. Formula mistakes

| # | Mistake | Fix |
|---|---|---|
| F1 | Using hit and miss ratios the wrong way round: T_c + h × P. | Penalty is multiplied by the **miss** ratio. |
| F2 | Applying the simultaneous formula to a hierarchical statement (or vice versa). | Read the wording (NOTES §4.2). The gap is m × T_c for one level. |
| F3 | Using the miss **time** (a total) as a **penalty** (an extra): T_c + m × Y with Y already containing T_c. | Total: h·X + m·Y; penalty: T_c + m·P. |
| F4 | Evaluating nested AMAT outside-in or dropping a bracket. | Innermost bracket first. |
| F5 | Multiplying the global L2 miss ratio by m1 again. | g2 already contains m1. |
| F6 | CPI: applying the data miss ratio to all instructions, or leaving out the fetch stalls. | stalls = 1 × m_I × P_I + (ld/st fraction) × m_D × P_D. |
| F7 | Burst: P = W × t_next (or W × t_first). | P = t_first + (W − 1) × t_next. |
| F8 | Write-back penalty without the dirty probability. | P = P_fetch + d × P_wb. |
| F9 | Chip count: forgetting the width dimension (columns) or the row dimension. | chips = ⌈M/K⌉ × ⌈W/N⌉. |
| F10 | Refresh overhead with chips instead of rows. | rows × t_row / period. |
| F11 | EAT with TLB: omitting the data access after translation, or counting k + 1 reads on a TLB hit. | hit: t_tlb + t_m; miss: t_tlb + (k+1) t_m. |

## 3. Numerical / calculation mistakes

| # | Mistake | Fix |
|---|---|---|
| N1 | ns vs cycles: using a penalty of 40 ns as 40 cycles at 2.5 GHz (it is 100). | cycles = ns × GHz. |
| N2 | Bits vs bytes: 64-bit word treated as 64 bytes → block with 4 words instead of 32. | W = block bytes / word bytes. |
| N3 | K = 1000 for sizes or K = 1024 for rates (MHz, MB/s). | Sizes binary, rates decimal unless told. |
| N4 | Off-by-one: W instead of W − 1 subsequent words; rounds ⌈B/m⌉ instead of B/m. | Check with a tiny case (B = 2). |
| N5 | µs vs ms in refresh (e.g., 204.8 µs / 32 ms = 0.64 %, not 6.4 %). | Write both in seconds. |
| N6 | Ceiling forgotten (⌈93.75⌉ = 94 cycles) or applied when not requested. | Apply only if "whole cycles" is stated. |
| N7 | Rounding of the answer: hit ratio 0.9167 rounded to 0.92 vs 0.91. | Round to the precision asked and check the condition. |
| N8 | Percent not converted (92 % used as 92). | Convert to 0.92 first. |
| N9 | Weighting a mix as 1/3, 1/3, 1/3 rather than by counts (170/200, 30/200). | Counts over total. |
| N10 | Quadratic root: choosing the negative one or one above 1. | Probabilities lie in [0, 1]; verify by substitution. |

## 4. PYQ-derived traps

These describe the *kind* of trap in question types that really exist in the mapping (newest → oldest). No official answers are given or implied.

| Year / Q# | Question kind | Trap pattern |
|---|---|---|
| 2025 Q.53 (CS-1) | Two-level AMAT from a figure | local vs global hit rates; read the access times as access times of each level (hierarchical wording). Figure not in the mapping. |
| 2024 Q.53 (CS1), 2022 Q.24 | WB / WT statements | "dirty victim" on a read miss; dirty bit presence; write-hit transfers; "TRUE" vs "FALSE" in the question stem. |
| 2022 Q.33 | Minimum hit rate | compare AMATs, not hit rates; rounding up. |
| 2020 Q.21 | Block-fill penalty | 64-bit word = 8 B; W − 1; whether the hit time is added. |
| 2019 Q.45 | Bandwidth | which stages are serial; MHz → period; units ×10^6. |
| 2017 Q.29 | Miss rates from AMAT | which cache has the larger miss rate (ratio direction); model. |
| 2017 Q.45 | I/D/L2 mix | weights; shared L2; referred-word-first wording. |
| 2016 Q.50 | Size from a curve (figure missing) | strict inequality; which model. |
| 2015 Q.18 | Basic AMAT | totals vs penalty. |
| 2014 Q.44 (Set-3) | Read/write/fetch mix | counts as weights; write hit and write miss times differ. |
| 2014 Q.43 (Set-2) | Block size | "smaller block ⇒ lower penalty" vs "better locality". |
| 2010 Q.48–49 | Block transfers between levels | different block sizes per level; sequential moves; bus width. |
| 2008 Q.35 | Inclusion | necessary vs sufficient/design choices. |
| 2025 CS-2 Q.55 (unmapped), 2024 CS1 Q.56 (pipeline folder), 2018 Q.23 (unmapped), 2023 Q.42 / 2020 Q.20 (DL folder) | AMAT penalty form, CPI stalls, refresh %, decoder/memory blocks | see NOTES §4.3, §5, §6.4, §6.3 |

## 5. Examination-time mistakes

1. Starting the arithmetic before writing down the model (hierarchical/simultaneous) and the units.
2. Not reading "per instruction" vs "per reference"; "all references" vs "reads only".
3. Trusting the first-glance product: 0.05 × 80 is 4, not 0.4.
4. In MCQs, accepting the first matching option; the distractors are usually the other model's value or an off-by-one.
5. In MSQs, skipping the options that need a careful definition (dirty bit, inclusion).
6. For NAT: rounding intermediate values (use the exact fraction until the end).
7. Not checking the limit (AMAT lower than the L1 hit time is impossible; probability above 1 is impossible).

## 6. How to check yourself

- [ ] Did I write the model and the units? Are my hit ratios local or global?
- [ ] Does AMAT lie between T1 and the full serial path?
- [ ] Penalty or total time? Did I add the hit time exactly once (hierarchical) or not at all (totals)?
- [ ] W − 1 for the burst; W = bytes ÷ word bytes.
- [ ] ns → cycles with the clock; ceiling only if required.
- [ ] CPI_eff ≥ CPI_base; the fetch included; data fraction used for D.
- [ ] Interfacing: rows × columns, low bits to chips, high bits to decoder, select bits where they actually are.
- [ ] Refresh: rows × t / period (units consistent).
- [ ] Re-derive the answer a second way (events table) if time allows.

---

## My Mistakes

| Date | Source | Question | Mistake | Root cause | Fix / Rule |
|---|---|---|---|---|---|
|  |  |  |  |  |  |
|  |  |  |  |  |  |
|  |  |  |  |  |  |
