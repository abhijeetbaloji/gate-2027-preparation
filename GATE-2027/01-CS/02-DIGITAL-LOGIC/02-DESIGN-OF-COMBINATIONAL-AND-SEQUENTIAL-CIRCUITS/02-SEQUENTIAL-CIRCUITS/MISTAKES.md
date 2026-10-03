# Sequential Circuits — Mistakes

### Common mistakes

| Mistake | What goes wrong | Correct rule |
|---------|-----------------|--------------|
| JK equation sign | \(KQ\) written instead of \(K'Q\) | \(Q^+ = JQ' + K'Q\) |
| SR hold | \(S=R=1\) used as hold | NOR latch hold is \(S=R=0\); \(S=R=1\) is forbidden |
| JK toggle forbidden | \(J=K=1\) avoided | That input complements \(Q\) |
| Output symbols as states | Repeated 0s counted once | Different successors are different states |
| Johnson length | \(2^n\) or \(n\) | Main cycle length \(2n\) |
| Ring length | \(2n\) | One-hot cycle length \(n\) |
| All \(T=1\) | Called a binary counter | Binary up uses \(T_i =\) AND of lower \(Q\) |
| Hold added to period | Clock stretched to “fix” hold | Hold uses minimum delay; period uses maximum delay |
| MSB period | Used as the clock period | MSB period is \(2^n\) clock periods on a binary counter |
| Same-edge update | Next \(Q\) used to compute the other \(D\) on that edge | Both excitations use the pre-edge state |
| D excitation don’t-care | \(D\) left as X | \(D\) equals the required next state |

### PYQ-shaped traps

- Saturating counters hold at the end code. The excitation there is hold, so a T input is 0, not 1.
- “Frequency of the ripple counter” must be read against the waveform the stem names. The MSB and the clock differ by \(2^n\).
- A sequence such as \(0\text{-}1\text{-}0\text{-}2\text{-}0\text{-}3\) needs a state per visit when the next symbol differs. The minimum JK count is \(\lceil \log_2 N \rceil\) for that \(N\).
- Distinct states reached from the given initial state can be fewer than \(2^k\). Reset to 0, then walk the cycle. Do not assume the counter uses every code.
- A multiplexer with its output fed back is a latch while the select stays at the feedback input. It is not an edge-triggered flip-flop.

### Calculation slips

- Toggling a bit whose \(T\) is 0.
- Forgetting \(Q'\) when \(J=1\) and \(Q=1\): toggle depends on the present \(Q\).
- Setup inequality reversed, so a long logic delay is treated as helpful.

### My Mistakes

| Date | Source | Question | Mistake | Root Cause | Correct Rule | Prevention |
|------|--------|----------|---------|------------|--------------|------------|
| | | | | | | |
