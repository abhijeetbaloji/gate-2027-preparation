# Floating Point — Formulas

Single precision only, unless a stem names another width. Reasons are in `NOTES.md`.

| Formula | Meaning | Condition |
|---------|---------|-----------|
| \((-1)^s (1.f)_2 2^{E-127}\) | Normal value | Exponent field \(E\) from 1 to 254. Leading 1 is not stored |
| \((-1)^s (0.f)_2 2^{-126}\) | Subnormal value | \(E=0\), fraction nonzero. No hidden 1 |
| Bias 127 | Stored exponent of a normal | True power 0 is stored as 127. Not 128 |
| \(2^{-126}\) | Smallest positive normal | \(E=1\), fraction 0, word `0x00800000` |
| \(2^{-149}\) | Smallest positive subnormal | \(E=0\), only the fraction LSB set. \(2^{-23}\times 2^{-126}\) |
| \((2-2^{-23})2^{127}\) | Largest finite single | \(E=254\), fraction all 1s. \(E=255\) is not this formula |
| \(E_1+E_2-127\) | Biased exponent of a product, before normalising | Both operands normal. If the significand product is \(\ge 2\), add 1 more |
| Sign of a product | XOR of sign bits | Independent of the exponents |

**Example.** \(+6.5 = 1.101_2 \times 2^2\). Biased field \(129\). Encoding `0x40D00000`.

**Example.** Product of \(1.5\) (\(E=127\), significand \(1.1_2\)) and \(4\) (\(E=129\), significand \(1.0_2\)) has biased exponent \(127+129-127 = 129\) and significand \(1.1_2\). Value 6. Word `0x40C00000`.

**Example.** `0x00400000` has exponent field 0 and the leading fraction bit set. Subnormal value \(\frac12 \times 2^{-126} = 2^{-127}\).

Specials, not plugged into the normal formula: exponent 0 and fraction 0 is zero; exponent 255 and fraction 0 is infinity; exponent 255 and nonzero fraction is NaN.
