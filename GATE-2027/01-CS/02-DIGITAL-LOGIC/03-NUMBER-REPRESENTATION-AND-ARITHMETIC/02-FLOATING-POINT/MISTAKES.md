# Floating Point — Mistakes

### Common mistakes

| Mistake | What goes wrong | Correct rule |
|---------|-----------------|--------------|
| Bias 128 | Every normal is off by a factor of two | Single-precision bias is 127 |
| Hidden 1 on every encoding | Subnormals and the exponent-0 formula get a leading 1 | Hidden 1 only for exponents 1 through 254 |
| \(E=255\) in the normal formula | Infinity reported as \(2^{128}\) | Fraction 0 means infinity; nonzero fraction means NaN |
| Largest finite | `0x7F800000` chosen | That is \(+\infty\). Largest finite has exponent 254 |
| \(-0\) | `0x80000000` read as a large negative | Exponent 0, fraction 0, sign 1 is \(-0\) |
| Smallest positive | \(2^{-127}\) or \(2^{-149}\) called the smallest normal | Smallest normal is \(2^{-126}\). \(2^{-149}\) is the smallest positive subnormal |
| Product exponents | \(E_1+E_2\) stored | Store \(E_1+E_2-127\), then adjust if the significand is at least 2 |
| Alignment direction | The larger number shifted | Shift the smaller significand right |
| Equal sum, equal exponents | “Exact integer sum” used to skip alignment | \(1.5+2.5=4\) still has exponent difference 1 |
| Fraction includes the hidden 1 | 24 fraction bits written into the word | 23 stored fraction bits |

### PYQ-shaped traps

- Hex words in recent papers are field puzzles. Split sign, exponent, and fraction before multiplying or adding in decimal.
- “Closest decimal” still starts from the exact binary value. Rounding is the last step, and only when the fraction is not a short dyadic rational the stem already matches.
- Comparing several encodings: a positive beats a negative, infinity beats every finite, and a NaN is not ordered as a magnitude.
- A sum of two exactly representable numbers can be exactly representable and still require an alignment shift.
- One mapped row is about floating-point **registers in an instruction format**. That is not an IEEE value.

### Calculation slips

- Reading the exponent from the wrong hex digits after the sign bit crosses a nibble boundary. `0xC0` is sign 1 and the top of the exponent; it is not “exponent = C0”.
- Forgetting to normalise a significand sum that reached \(10.0_2\).
- Treating subnormal power as \(2^{0-127}\).

### My Mistakes

| Date | Source | Question | Mistake | Root Cause | Correct Rule | Prevention |
|------|--------|----------|---------|------------|--------------|------------|
| | | | | | | |
