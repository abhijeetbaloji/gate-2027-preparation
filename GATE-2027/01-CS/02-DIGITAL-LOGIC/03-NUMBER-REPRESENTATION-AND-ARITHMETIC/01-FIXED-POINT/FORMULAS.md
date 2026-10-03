# Fixed Point — Formulas

Reasons are in `NOTES.md`.

## Ranges

| Formula | Meaning | Condition |
|---------|---------|-----------|
| \(0 \ldots 2^n-1\) | Unsigned range | \(n\) bits |
| \(-2^{n-1} \ldots 2^{n-1}-1\) | Two’s-complement range | \(n\) bits, one zero |
| \(-(2^{n-1}-1) \ldots 2^{n-1}-1\) | Sign-magnitude and ones’ complement | Two patterns for zero; \(2^n-1\) distinct values |
| \(2^n - (2^n - 1) = 1\) | (two’s-complement count) minus (sign-magnitude count) | Same \(n\). This is the 16-bit comparison |

## Value and negation

| Formula | Meaning | Condition |
|---------|---------|-----------|
| \(-b_{n-1}2^{n-1} + \sum_{i=0}^{n-2} b_i 2^i\) | Two’s-complement value | Bit \(n-1\) is the sign |
| Flip, then add 1 | Negation | Discard the carry past bit \(n-1\). Pattern \(100\ldots 0\) is unchanged |
| \(N / 2^f\) | Fixed-point value | \(N\) is the integer formed by all bits, \(f\) bits are fractional, unsigned unless stated |

**Example.** 4-bit \(1011 = -8+2+1 = -5\). 6-bit two’s complement of \(-5\) is \(111011\).

## Overflow and carry

| Test | Detects | Condition |
|------|---------|-----------|
| Carry out of MSB \(= 1\) | Unsigned overflow | \(n\)-bit sum |
| Carry into sign \(\neq\) carry out of sign | Two’s-complement overflow | Equivalent: same-sign operands, opposite-sign result |
| End-around: add MSB carry into the LSB | Ones’-complement correction | Not used for two’s complement |

**Example.** 4-bit \(0101+0100 = 1001\), carry out 0, carry into the sign 1. Signed overflow: the stored pattern reads as \(-7\), while \(5+4=9\). Unsigned, the same bits are 9, which is inside \(0\ldots 15\), and the carry out is 0, so there is no unsigned overflow. The two tests disagree on this row.

## Booth

| Pair \(Q_i, Q_{i-1}\) | Operation | Condition |
|-----------------------|-----------|-----------|
| 00, 11 | no add or subtract | \(Q_{-1}=0\) at the start |
| 01 | add multiplicand | Then arithmetic right shift |
| 10 | subtract multiplicand | Shifts are not counted as add/sub |

The number of add/sub operations equals the number of indices \(i\) with \(Q_i \neq Q_{i-1}\).
