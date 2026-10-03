# Fixed Point — Revision

## Ranges, \(n\) bits

| Code | Range | Distinct values |
|------|-------|----------------:|
| Unsigned | \(0 \ldots 2^n-1\) | \(2^n\) |
| Sign-magnitude | \(-(2^{n-1}-1) \ldots 2^{n-1}-1\) | \(2^n-1\) (two zeros) |
| Ones’ complement | same as sign-magnitude | \(2^n-1\) (two zeros) |
| Two’s complement | \(-2^{n-1} \ldots 2^{n-1}-1\) | \(2^n\) (one zero) |

8-bit two’s complement: \(-128\) to \(127\). The pattern \(10000000\) is \(-128\).

## Value of a two’s-complement pattern

\[
-b_{n-1}2^{n-1} + \sum_{i<n-1} b_i 2^i.
\]

Negation: flip every bit, add 1, drop the carry out of the MSB. Negating \(100\ldots 0\) returns \(100\ldots 0\).

## Overflow

Same bit sum for unsigned and two’s complement.

- Unsigned overflow: carry out of the MSB is 1.
- Signed overflow: carry into the sign differs from carry out of the sign. Same as “operands’ signs match, result sign differs.”

\(C_{out}=1\) is not signed overflow.

Ones’ complement: add the end-around carry back into the LSB.

## Shifts and extension

- Arithmetic right shift fills the MSB with the sign.
- Left shift by \(k\) multiplies by \(2^k\) when the result fits.
- Sign extension copies the sign into new high bits. It preserves a two’s-complement value.

## Binary point

If \(f\) bits lie to the right of the point, value \(= N / 2^f\), where \(N\) is the integer reading of all bits. Unsigned unless the stem says otherwise.

## Booth

Append \(Q_{-1}=0\). Scan the multiplier only.

| \(Q_i Q_{i-1}\) | Action |
|-----------------|--------|
| 00 or 11 | none |
| 01 | add \(M\) |
| 10 | subtract \(M\) |

Then arithmetic shift right. Add/sub count = number of positions with \(Q_i \neq Q_{i-1}\).

## Traps

\(-127\) as the 8-bit minimum. Two’s complement having two zeros. Sign extension with zeros. Booth count taken from the multiplicand. End-around carry used on a two’s-complement sum.
