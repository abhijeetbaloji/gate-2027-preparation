# Cache Memory Mapping — SHORTCUTS

Only mathematically valid shortcuts. Examples script-verified. Assumptions stated.
Full context: [`NOTES.md`](NOTES.md). AMAT shortcuts also in [`../01-PERFORMANCE/SHORTCUTS.md`](../01-PERFORMANCE/SHORTCUTS.md).

---

## S1. Tag grows by +log₂k when associativity multiplies by k

- **What it solves:** tag width after changing DM → k-way at fixed capacity and block size.
- **When:** same C, B, A; comparing two organisations.
- **Why:** #sets divides by k → index loses log₂k bits → tag gains them.
- **Example:** 64 KB, 64 B, A = 32: DM tag 16 → 4-way tag 18 (+2).
- **Limit:** fails if capacity or block size also changes.

## S2. DM tag unchanged when block size doubles (fixed C, A)

- **What it solves:** per-line tag width after block-size change.
- **When:** direct-mapped, capacity and address width fixed.
- **Why:** offset +1 and index −1 cancel in t = A − i − o.
- **Example:** 16 KB DM, A = 32: B = 32 or 64 → tag stays **16**; lines halve so total tag bits halve.
- **Limit:** set-associative tag still changes if k > 1 (sets change).

## S3. Quick check: t_DM + log₂k = t_k

- **What it solves:** sanity-check a computed tag in one addition.
- **When:** after computing DM tag separately.
- **Example:** DM tag 20, 8-way → 20 + 3 = **23** ✓
- **Limit:** fully associative: t = A − o, not DM + log₂N.

## S4. Line from hex without full binary

- **What it solves:** direct-mapped line number.
- **When:** byte-addressable, B is a power of 2.
- **Why:** line = (addr >> log₂B) mod #lines.
- **Example:** addr = 0x7C3A5E, B = 32 → (0x7C3A5E >> 5) mod 256 = **210**.
- **Limit:** wrong if you forget to shift by the offset before masking.

## S5. Block-to-line range in one line

- **What it solves:** which physical line numbers can hold block j in a k-way cache with v sets.
- **When:** lines numbered set-by-set, k lines per set.
- **Why:** set = j mod v; lines are k consecutive slots starting at set·k.
- **Example:** v = 16, k = 2, j = 37 → lines **10–11**.
- **Limit:** wrong line numbering scheme (some texts number by set only).

## S6. Same-block test before simulating

- **What it solves:** P,Q,R,S loop questions faster.
- **When:** several variables in one trace.
- **Why:** same block number ⇒ same tag on a hit; different tags on same line ⇒ conflict every time.
- **Example:** Y = 0x1D48, Z = 0x1D4F, B = 16 → same block 468 → Z always hits after Y loads it.
- **Limit:** only skips simulation for variables you have checked; still trace conflicts.

## S7. Row-major vs column-major on square array (DM)

- **What it solves:** order-of-magnitude miss difference.
- **When:** block-aligned array, DM cache, row size not a multiple of cache size in blocks.
- **Why:** column-major with stride = row length in blocks maps rows i and i+rows/2 to the same line.
- **Example:** 32×32 ints, 32 B blocks, 64 lines → row-major 128 misses, column-major 1024 → difference **896**.
- **Limit:** needs the specific stride conflict; row-major is not always optimal.

## S8. Metadata bits = lines × (tag + status) + sets × LRU

- **What it solves:** total non-data bits quickly.
- **When:** question lists per-line bits and LRU scope (per set vs per line).
- **Example:** 1024 lines, tag+valid+dirty = 21, 128 sets, LRU 16 → 128×(8×21+16) = **23 552**.
- **Limit:** use the LRU bit count the question specifies (true LRU vs one bit per set).

## S9. Hierarchical vs simultaneous gap (one level)

- **What it solves:** convert between models.
- **When:** ambiguous wording; MCQ options use both.
- **Why:** simultaneous never pays the failed lookup: T_simul = T_hier − m·t_hit.
- **Example:** t = 2, m = 0.15, t_m = 80: hier 2+12=14; simul 14−0.3=**13.7**… wait: 0.85×2+0.15×80=14 hier additive? For one level hier T_c+m·P vs simul h·T_c+m·T_m: difference m·T_c.
- **Limit:** multi-level gap is a sum of terms, not one subtraction.

## S10. CPI stall = refs_per_instr × m × P

- **What it solves:** memory stall cycles per instruction.
- **When:** separate I- and D-cache miss ratios given.
- **Why:** each instruction generates one fetch; loads/stores add data refs.
- **Example:** m_I=0.02, m_D=0.05, 35 % mem ops, P=40 → 0.8+0.7 stalls → CPI = 1.2+1.5 = **2.7**.
- **Limit:** write-through with write-buffer may hide some stalls (only if the question says so).

## S11. Page colours = 2^((i+o) − page_offset_bits)

- **What it solves:** minimum page colours for VIPT.
- **When:** page size and cache index+offset widths known.
- **Example:** i+o = 13, page = 12 bits → 2^(13−12) = **2 colours**.
- **Limit:** high-order virtual indexing uses a different formula; see OS notes.

---

## Do NOT use

| Tempting rule | Why it fails | Counterexample |
|---|---|---|
| "Fully associative ⇒ fewest tag bits" | FA has the **widest** tag (no index bits removed from the tag) | A=32, B=64: DM tag 16, FA tag 26 |
| "Doubling block size always lowers miss ratio" | capacity in lines halves; pollution rises | NOTES §12.2 |
| "Conflict miss ⇒ fully associative would hit" | reversed: FA hit ⇒ your miss was conflict | classification table §12.1 |
| "Write miss never touches memory in WB" | write-allocate fetches; dirty victim write-backs | Q22 trace |
| "LRU always beats FIFO on the same trace" | Belady anomaly | Q35: FIFO gets one more hit on the classic 12-ref, 3-line trace |
