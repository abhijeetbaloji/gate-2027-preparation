# Microprogrammed Control — Shortcuts

Only valid shortcuts. Derivations in [NOTES.md](NOTES.md); formulas in [FORMULAS.md](FORMULAS.md).

---

## S1. "None" costs one code: use ⌈log₂ (n+1)⌉, and spot the power-of-two trap

- **What it solves:** bits of an encoded field with an optional "assert nothing".
- **When:** a mutually exclusive group where a microinstruction may leave the group idle.
- **Why it works:** n signals + "none" = n + 1 codes.
- **Example:** n = 7 → 3 bits; n = 8 → 4 bits; n = 15 → 4; n = 16 → 5; n = 20 → 5.
- **Limitation:** if the question says exactly one is always selected (or the field is gated elsewhere, as ALU function is gated by an enable), use ⌈log₂ n⌉. Read the statement.

## S2. When n is just below a power of two, "+ none" is free

- **What it solves:** quick mental check. n + 1 ≤ 2ᵇ.
- **Why:** n = 2ᵇ − 1 plus "none" exactly fills 2ᵇ codes.
- **Example:** 15 signals + none → 16 codes → 4 bits (same as without none); 7 → 3.
- **Limitation:** works only at 2ᵇ − 1; at 2ᵇ the extra code forces one more bit.

## S3. CAR bits from N: find the bracketing power of two

- **What it solves:** ⌈log₂ N⌉ without a calculator.
- **How:** memorise 2⁶ = 64, 2⁷ = 128, 2⁸ = 256, 2⁹ = 512, 2¹⁰ = 1024. N = 29 → between 16 and 32 → 5. N = 400 → between 256 and 512 → 9. N = 1000 → 10.
- **Limitation:** exact powers (64) need exactly that many bits (6), not one more; 65 needs 7.

## S4. Saving = N × (difference in width), not the difference of totals

- **What it solves:** "how many bits does encoding save" with the same number of words.
- **Why:** N × W_h − N × W_v = N × (W_h − W_v); only the fields that changed matter (the next-address field cancels).
- **Example:** seven 6-way groups (one chosen per group): horizontal 42 signal bits vs encoded 7 × 3 = 21 → 21 bits/word saved; with 256 words → 5 376 bits.
- **Limitation:** only if both designs have the same N and the other fields are identical. If vertical needs more words, you must compute both totals.

## S5. Shared fetch counted once

- **What it solves:** the number of control-store words.
- **How:** N = fetch + Σ routines. If a quoted number "per instruction" already contains fetch, subtract it before summing.
- **Example:** fetch 5, routines 4, 4, 6, 3 (sum 17) → N = 22, not 4 × 5 + 17 = 37.
- **Limitation:** only if the machine really shares the fetch routine (the standard assumption; state it).

## S6. Mixed-format table: add the bit column, do not re-encode

- **What it solves:** a table listing fields with choices and bits.
- **How:** sum the given "bits" column; check each entry against ⌈log₂ choices⌉ only if the problem asks you to design the field.
- **Example:** 3 + 6 + 2 + 7 + 9 = 27 bits; with 128 words → 3 456 bits.
- **Limitation:** if the table's "bits" were not given, derive each field with S1 and keep simultaneous signals as 1 bit each.

## S7. Hardwired-vs-microprogrammed time = n_µ × t_µ − n_clk × T_clk

- **What it solves:** "how much longer is microprogrammed control".
- **Example:** 7 × 9 − 5 × 12 = 63 − 60 = 3 ns.
- **Limitation:** use exactly the time model in the question (access only vs access + decode + datapath; overlapped vs not).

## S8. Group count from conflicts: draw edges, not guesses

- **What it solves:** how many fields/bits are needed for given simultaneous pairs.
- **How:** edge = signals asserted together; groups = independent sets; for an even cycle two groups suffice (colour alternately).
- **Example:** 6-cycle on six signals → two groups of 3 → 2 + 2 = 4 bits.
- **Limitation:** for odd cycles/denser graphs you need more colours; brute-force small cases.

## S9. Loop count: body × iterations, test after decrement

- **What it solves:** microinstructions executed by a looping microroutine.
- **How:** total = fetch + setup + body × n + finish, where the loop runs n times if the branch-back test follows the decrement and exit is when the counter reaches zero.
- **Limitation:** a pre-test loop (test before body) runs the test one more time.

---

## Do NOT use

1. **"Vertical is always smaller in total."** Vertical words are narrower but there are more of them. Counter-example: 300 × 56 = 16 800 bits (horizontal) vs 410 × 31 = 12 710 bits (vertical) says vertical wins there, but with 520 vertical words of 34 bits you get 17 680 > 16 800. Compute both.
2. **"Horizontal width = number of signals."** Add next-address, condition-select and any sequencing mode bits.
3. **"Encoding a group costs log₂ n."** Use ⌈ ⌉ and add "none" when allowed.
4. **"Nanoprogramming always saves bits."** M = 512, W = 60, D = 500: 34 608 > 30 720.
5. **"CAR bits = next-address field bits = signal bits."** Only the first two coincide for a full absolute address; signal bits are unrelated.
6. **"Microprogrammed means slower by a fixed factor."** The gap depends on t_CS, decode, overlap and µ counts.
7. **"Encoded fields always combine across groups to ⌈log₂ of the product⌉."** Each group is independent; the sum of ceilings is what the format needs.
