# Floating-Point Representation and Arithmetic

A floating-point number stores a sign, a significand, and an exponent, so the binary point moves. GATE CS questions in the mapping are IEEE-754 **single precision**: decode a hex word, compare specials, add or multiply two exact values, and know what the extreme patterns mean. The integer codes are in the fixed-point folder. The stored answers in the mapping are `VERIFICATION REQUIRED`, so the numbers below are the standard encoding rules applied to small examples, not official keys.

---

## 1. The single-precision word

Thirty-two bits:

| Field | Bits | Width |
|-------|------|------:|
| Sign \(s\) | 31 | 1 |
| Biased exponent \(E\) | 30–23 | 8 |
| Fraction \(f\) | 22–0 | 23 |

Hex is the easiest way to see the fields. `0xC0A00000` is `1100 0000 1010 0000 0000 0000 0000 0000`.

- Sign = 1.
- Next 8 bits = `10000001` = 129.
- Fraction = `010` followed by zeros, so \(f = 2^{-2}\).

**Bias.** For a normal number the stored exponent is the true power plus 127.

\[
\text{unbiased} = E - 127, \qquad 1 \le E \le 254.
\]

**Why 127, not 128.** Eight bits can hold 0 through 255. Reserving 0 and 255 for specials leaves 1 through 254. The bias is chosen so that true exponent 0, the power of \(1.0\), sits in the middle of that range: \(0 + 127 = 127\). A bias of 128 shifts every normal number by a factor of two. Using 128 on a machine that decodes with 127 does not “almost” work; it doubles the value.

**Normal value.**

\[
(-1)^s \times (1.f)_2 \times 2^{E-127}.
\]

The leading 1 is hidden. It is not stored, because every normal significand is at least 1 and less than 2, so the bit above the fraction is always 1. Storing it would waste a bit.

**Example.** `0xC0A00000`. Sign negative, \(E=129\), power \(2^{2}\), significand \(1.01_2 = 1.25\). Value \(-1.25 \times 4 = -5\).

**Example.** \(+6.5 = 110.1_2 = 1.101_2 \times 2^2\). Biased exponent \(129 = 10000001_2\). Fraction `101` then zeros. The word is `0 10000001 10100000000000000000000` = `0x40D00000`.

**Example.** \(+1.0\) has \(E=127\) and fraction 0: `0x3F800000`. \(+2.0\) has \(E=128\): `0x40000000`.

---

## 2. Special patterns

| Exponent field | Fraction | Meaning |
|----------------|----------|---------|
| 0 | 0 | \(\pm 0\), sign bit kept |
| 0 | nonzero | subnormal, no hidden 1 |
| 1–254 | anything | normal |
| 255 | 0 | \(\pm \infty\) |
| 255 | nonzero | NaN |

**Why the reserved exponents exist.** If every field were a normal number, there would be no encoding left for overflow, for underflow gradual to zero, or for an invalid result. All-ones and all-zeros are those leftover codes. They are not “the largest finite exponent plus one” in the normal formula. Plugging \(E=255\) into \(2^{E-127}\) is a mistake; that field is infinity or NaN.

| Word | Value |
|------|-------|
| `0x00000000` | \(+0\) |
| `0x80000000` | \(-0\) |
| `0x7F800000` | \(+\infty\) |
| `0xFF800000` | \(-\infty\) |
| `0x7F800001` | NaN (any nonzero fraction with exponent 255) |

\(+\infty\) is larger than every finite float. A NaN does not compare as larger than a number.

**Smallest positive normal.** \(E=1\), fraction 0: \(1.0 \times 2^{1-127} = 2^{-126}\). The word is `0x00800000`.

**Largest finite.** \(E=254\), fraction all 1s: \((2 - 2^{-23}) \times 2^{127}\). Exponent 255 with fraction 0 is infinity, which is not finite. The mapped “largest among these encodings” questions are decided by sign first, then by this table, then by exponent, then by fraction.

---

## 3. Subnormals

When \(E=0\) and \(f \neq 0\),

\[
(-1)^s \times (0.f)_2 \times 2^{-126}.
\]

There is no hidden 1. The power is \(2^{-126}\), the same power as the smallest normal, not \(2^{-127}\) and not \(2^{0-127}\).

**Why that power.** The smallest normal is \(1.0 \times 2^{-126}\). The next numbers downward should sit just below it, with significands \(0.111\ldots\), \(0.110\ldots\), down to one bit. Using \(2^{-126}\) places the largest subnormal at \((1 - 2^{-23}) \times 2^{-126}\), immediately below \(2^{-126}\). Using the formula \(2^{0-127}\) would leave a gap.

**Smallest positive subnormal.** Fraction LSB only, `0x00000001`:

\[
2^{-23} \times 2^{-126} = 2^{-149}.
\]

**A midpoint subnormal.** `0x00400000` sets fraction bit 22, the highest fraction bit, and the exponent field is 0. Significand \(0.1_2 = 1/2\). Value \(2^{-1} \times 2^{-126} = 2^{-127}\). It is not a normal number, and its unbiased exponent is not \(-127\) in the normal sense: normals do not use exponent field 0.

`0x00800000` is the smallest positive **normal**, \(2^{-126}\). Every positive subnormal is strictly smaller than every positive normal.

---

## 4. Comparing and decoding quickly

1. If the exponent is 255, stop: infinity or NaN. Do not compute \(2^{128}\).
2. If the exponent is 0, use the subnormal formula, or recognise zero.
3. Otherwise write \(1.f \times 2^{E-127}\) and apply the sign.
4. Among positive normals, the larger biased exponent wins. Equal exponents: the larger fraction wins.
5. A negative number is smaller than every positive number, including \(+0\).

**Worked comparison.** `0x3F800000` is \(+1\). `0x40000000` is \(+2\). `0xBF800000` is \(-1\) (same fields as \(+1\), sign set). Order: \(-1 < +1 < +2\).

---

## 5. Addition

Addition cannot add the fraction bits until the exponents match.

1. If either operand is NaN, the result is NaN. Infinity plus the opposite infinity is NaN. Infinity plus a finite number is that infinity.
2. Put the larger-magnitude exponent on the result tentatively.
3. Shift the smaller significand **right** by the difference of unbiased exponents. Bits that shift past the fraction are where rounding will look; they are not free to ignore if the stem asks about an inexact sum.
4. Add or subtract the significands according to the signs. Subtraction is addition of the opposite sign.
5. Normalise. A sum \(\ge 2\) shifts right and increments the exponent. A sum \(< 1\) shifts left and decrements the exponent, unless the exponent would fall below the normal range, in which case the result is subnormal or zero.
6. Round, then normalise again if rounding produced a carry out of the significand.

**Why the shift is right, not left.** The larger exponent is the coarser scale. To write both numbers in units of \(2^{E_{\text{large}}-127}\), the smaller number must lose low-order bits, which is a right shift.

**Exact example.** \(1.5 + 2.5\).

- \(1.5 = 1.1_2 \times 2^0\), biased exponent 127.
- \(2.5 = 1.01_2 \times 2^1\), biased exponent 128.
- Difference 1. Shift 1.5’s significand right by 1 at exponent 128: \(0.11_2\).
- Add \(1.01_2 + 0.11_2 = 10.00_2 = 2\).
- Normalise: \(1.0_2 \times 2^2\). Biased exponent 129. Word of \(+4\) is `0x40800000`.

The mathematical sum is 4, and 4 is exactly representable. The exponents were **not** equal, so an alignment shift was required. Both facts can be true together.

---

## 6. Multiplication

1. Result sign is the XOR of the signs.
2. Add the unbiased exponents. In biased arithmetic that is \((E_1 - 127) + (E_2 - 127)\), then add 127 back: \(E_1 + E_2 - 127\).
3. Multiply the significands, including the hidden 1s.
4. The product of two numbers in \([1, 2)\) lies in \([1, 4)\). If it is \(\ge 2\), shift right once and add 1 to the exponent.
5. Overflow to infinity if the exponent cannot be stored as a normal or if the rules say so. Underflow to subnormal or zero on the other side.

**Example.** \(1.5 \times 4\).

- \(1.5 = 1.1_2 \times 2^0\), \(E=127\).
- \(4 = 1.0_2 \times 2^2\), \(E=129\).
- Sign positive. Unbiased exponents \(0+2=2\), biased \(129\).
- Significands \(1.1_2 \times 1.0_2 = 1.1_2\), already in range.
- Value \(1.1_2 \times 2^2 = 6\). Fraction `100…`, exponent 129: `0x40C00000`.

**Bias slip.** Adding the biased exponents and forgetting to subtract 127 doubles the exponent error: \(127+129 = 256\), not 129. The stored field is 8 bits; 256 does not fit. The correction is part of the algorithm, not an optional rounding step.

---

## 7. What recent papers are doing

The mapped stems are almost all single-precision hex:

- Decode one word to a decimal, sometimes rounded to two places when the fraction is not a short binary.
- Add or multiply two or three register values given in hex, and match the result word or a property of it.
- Choose the largest encoding, which requires the special-case table before any magnitude comparison.
- Name the smallest positive normalised number, which is \(2^{-126}\), not \(2^{-127}\) and not \(2^{-149}\).

A question that only needs the sign, the exponent, and whether the fraction is zero can be answered without expanding all 23 bits. A question that asks for a decimal needs the fraction expanded, or a bound if the stem says “closest.”

Instruction-format questions that mention floating-point **registers** are computer organisation. One such row is in the mapping file and is not an IEEE decode.

---

## 8. Solving procedure

1. Split the 32-bit pattern into 1 / 8 / 23. Hex digits help: the sign is the top bit of the first hex digit.
2. If \(E \in \{0, 255\}\), use the special table and stop.
3. Write the power \(E-127\) and the significand \(1.f\).
4. For a sum, align, then add, then normalise.
5. For a product, XOR signs, add unbiased exponents, multiply significands, normalise once if the product significand is at least 2.
6. To rebuild the word, bias the exponent, write the fraction **without** the leading 1, and convert to hex.
7. Check the result against a nearby power of two. \(+6\) must sit between `0x40C00000` (\(4 \times 1.5\)) and `0x41000000` (\(+8\)).

---

## 9. Traps

| Trap | Correction |
|------|------------|
| Bias 128 | Single-precision bias is 127 |
| Hidden 1 on a subnormal | Subnormals use \(0.f\) and power \(2^{-126}\) |
| \(E=255\) fed into the normal formula | Infinity or NaN |
| `0x7F800000` called the largest finite | It is \(+\infty\). Largest finite has exponent 254 |
| `0x80000000` called a large negative | It is \(-0\) |
| Smallest positive normal \(2^{-127}\) or \(2^{-149}\) | Normal minimum is \(2^{-126}\). \(2^{-149}\) is the smallest positive subnormal |
| Biased exponents added and stored | Subtract one bias: \(E_1+E_2-127\) |
| Alignment the wrong way | Shift the **smaller** significand right |
| Equal mathematical sum means equal exponents | \(1.5\) and \(2.5\) sum exactly to 4 and still need a one-bit alignment |
| Fraction bits include the hidden 1 | 23 stored bits; the leading 1 is extra |

---

## 10. Connections

- **Fixed point.** The fraction is a fixed-point field. The exponent is what fixed point does not have. Two’s-complement overflow and IEEE overflow are different tests.
- **Combinational circuits.** A floating-point adder is an align shifter, an integer significand adder, a normalise shifter, and a rounder. The adder equations from the combinational notes are the significand step.
- **Computer organisation.** Register-transfer questions about floating-point registers are not this encoding. The encoding is what those registers contain when the stem actually gives an IEEE word.
