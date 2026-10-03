# Finite Automata — Shortcuts

Each shortcut below is a valid rule, not a guess. The limitation line says exactly where it stops working. Theory: [NOTES.md](NOTES.md).

## 1. Name the memory, then count

- **Solves:** “minimum number of states in a DFA for `L`”.
- **When:** `L` is a local pattern, a count, a residue, or a product of those.
- **Why:** Myhill–Nerode classes *are* that memory.
- **Example:** ends with `01` → remember the longest suffix that is a prefix of `01` → `{ε, 0, 01}` → 3.
- **Limitation:** if two candidate memories can be merged, you still owe a distinguishing continuation; do not stop at “I drew `n` states”.

## 2. Ends-with / contains templates

- **Ends with `w`, `|w| = m`:** `m + 1` complete states (the prefixes of `w`).
- **Contains `w`:** also `m + 1`, with the last prefix an accepting sink.
- **Why:** KMP-style suffix-prefix function; overlaps change the *target* of an arc, never the number of prefixes.
- **Example:** ends with `01` is 3; contains `001` is 4; ends with `011` is 4.
- **Limitation:** “starts with `w`” needs an extra dead sink on the first mismatch (`m + 2` typically). Unary languages may not have a mismatch.

## 3. Distinguish `ε`, `0`, `01` for ends-with-`01`

- **Solves:** proving the 3-state machine is minimal, and killing wrong language options.
- **Why:** `01 ∈ L`, `ε ∉ L`, `0 ∉ L`; `0 · 1 ∈ L` while `ε · 1 ∉ L`.
- **Same pattern for any “ends with `ab`”:** the three prefixes of `ab` are pairwise distinguishable.
- **Limitation:** for “contains `01`” the accepting sink is distinguished by `z = ε`, but `ε` and `0` are still distinguished by `z = 1`. Count stays 3; the *arcs* from the accept state differ (they stay in the sink).

## 4. Product of independent moduli

- **Solves:** “`#a ≡ r (mod m)` and `#b ≡ s (mod n)`”.
- **Rule:** min complete DFA has `m n` states over `{a, b}` (or `{0, 1}`).
- **Why:** every pair of residues is reachable, and `a^{m-i} b^{n-j}` distinguishes `(i, j)`.
- **Example:** `#0` divisible by 3 and `#1` divisible by 5 → 15.
- **Limitation:** one counter used twice (e.g. `#a ≡ 0 (mod 2)` *and* `#a ≡ 1 (mod 3)`) is a *single* `lcm(2, 3) = 6` counter, not a 2×3 product of two letter-counts. “Even but not divisible by 3” is this latter case: still 6, accept `{2, 4} mod 6`.

## 5. `2^n` is an upper bound, 1 is possible

- **Solves:** “an `n`-state NFA; which numbers can / cannot be the min DFA size `k`”.
- **Rules that are always safe:** `k ≤ 2^n`; `k = 1` is possible (`∅` or `Σ*`); `k > 2^n` is impossible; `k ≥ n` is **not** forced.
- **Example:** `n = 6` → `k ≤ 64`. 32 and 1 can occur; 65 and 128 cannot.
- **Limitation:** “can occur” is existential over all `n`-state NFAs. A *given* NFA may have a much smaller `k`; you must run reachable-subset construction (and minimise) to know *its* `k`.

## 6. Dead state on “exactly `k`” and on “no `k` in a row”

- **Exactly `k` ones, complete DFA:** `k + 2` (counts `0…k` plus a `≥ k+1` reject sink).
- **No `k` consecutive ones, complete DFA:** `k + 1` (trailing counts `0…k−1` plus a `k`-run reject sink).
- **Why:** an illegal prefix is reachable, so the complete machine must keep a dead state, and it is distinguishable from every still-legal state (`z` that would have finished a legal count / a shorter run of ones).
- **Example:** exactly two `1`s → 4; no three consecutive `1`s → 4.
- **Limitation:** “at least `k` ones” has no reject sink (`k + 1`). An incomplete DFA can omit the sink; GATE counts the complete one.

## 7. Last-`k`-bits vs first-`k`-positions

- **`k`-th from the end:** DFA `2^k`, NFA `k + 1`.
- **`k`-th from the start:** DFA `k + 2` (waiting states, then a yes-sink and a no-sink).
- **Why:** the future still depends on bits you have already forgotten only in the from-the-end case, so you must store all `k`-bit windows.
- **Example:** third from the end is `1` → 8; third symbol is `1` → 5.
- **Limitation:** strings shorter than `k` are rejected in both; the start-position machine needs two sinks, the end-position machine does not use a separate dead state (every window is legal).

## 8. One-state check before answering “2”

- **Solves:** RE-defined languages that look like `Σ*`.
- **Rule:** the only 1-state complete DFAs are `∅` and `Σ*`. If `ε` is out and some nonempty string is in (or vice versa), the answer is at least 2.
- **Example:** `(0+1)*(0+1)(0+1)* = Σ+` → 2.
- **Limitation:** `{ε}` is also 2 states (accepting start plus a dead sink), not 1.

## 9. Short-string filter for DFA ↔ language / RE

- **Solves:** “which language / which RE does this DFA accept” when a figure is given.
- **When:** always, as the first pass.
- **Why:** one disagreement kills an option. Test `ε`, length 1, length 2, a string that should just enter the claimed pattern, and a string that just violates it.
- **Limitation:** surviving the filter is not a proof; if two options remain, trace a loop twice or compare ends-with vs contains.

## 10. NFA complement: determinize first

- **Solves:** “complement of the language of this NFA”.
- **Rule:** never flip `F` on the NFA. Convert to a complete DFA, then flip.
- **Example:** unary NFA for `a+` → complement `{ε}`.
- **Limitation:** if the NFA already happens to be a complete DFA, flipping `F` is legal — because it *is* a DFA.
