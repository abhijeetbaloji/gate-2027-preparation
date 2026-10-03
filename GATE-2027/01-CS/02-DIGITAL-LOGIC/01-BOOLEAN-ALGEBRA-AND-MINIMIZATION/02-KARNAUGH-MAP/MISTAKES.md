# Karnaugh Map — Mistakes

### Common mistakes

| Mistake | What goes wrong | Correct rule |
|---------|-----------------|--------------|
| Binary column order | \(01\) drawn next to \(10\) | Gray order \(00, 01, 11, 10\) |
| Group of 6 or 3 | One circle around a non-subcube | Only \(2^k\) cells |
| Forgotten wrap | Corners left as four pairs | \(m_0, m_2, m_8, m_{10}\) is one quad |
| X treated as a required 1 | Extra products kept only to cover X | X need not be covered |
| X treated as a hard 0 | A larger group rejected | X may be inside the group |
| Required 0 inside an octet | \(C'\) circled across a 0 | A 0 forbids the group |
| Prime called essential | Every circle kept | Essential means a 1 has no second prime |
| SOP rule used on 0s | POS literal complemented backwards | In a 0-group, complement the variable that is constantly 1 |
| Minimal form assumed unique | One cover reported as the only answer | Cyclic maps have several minimal covers |
| Hazard circle kept in a minimum-literal answer | Consensus term counted as necessary | It preserves the function and is optional unless the stem asks for a hazard-free sum |

### PYQ-shaped traps

- A drawn X is a don’t-care, not a 1 and not a third logic value that must appear in the expression.
- “Which expressions represent \(F\)?” can accept a non-minimal sum. “Minimal form” cannot.
- POS options that look alike in a bad scan still differ by which variable is complemented. Evaluate one 0-cell.
- The same minterm list is often filed under algebraic technique. The map is still the method.

### Calculation slips

- Minterm number read with \(D\) as the MSB. The weight follows the order stated in the stem.
- A pair combined across a two-bit change because the cells looked nearby in a non-Gray sketch.
- Literal count: a group of 4 on a 4-variable map contributes 2 literals, not 4.

### My Mistakes

| Date | Source | Question | Mistake | Root Cause | Correct Rule | Prevention |
|------|--------|----------|---------|------------|--------------|------------|
| | | | | | | |
