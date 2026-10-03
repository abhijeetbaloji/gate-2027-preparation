# Floating Point — Shortcuts

## 1. Split the hex before any arithmetic

- **Solves.** Decoding a single-precision word.
- **When.** The stem gives 8 hex digits.
- **Why.** The fields are fixed: top bit sign, next 8 bits biased exponent, last 23 bits fraction. The normal formula applies only for exponents 1 through 254.
- **Example.** `0xC0A00000` is sign 1, exponent `10000001` = 129, fraction `01`. Value \(-1.25 \times 2^{2} = -5\).
- **Limit.** Exponent `11111111` is infinity or NaN. Do not compute \(2^{255-127}\).

## 2. Positive normals sort by exponent, then fraction

- **Solves.** “Which encoding is largest?” among ordinary positive numbers.
- **When.** Signs are 0 and exponents are not 0 or 255.
- **Why.** The hidden significand is in \([1, 2)\), so a larger power of two dominates any fraction difference. Inside one power, the fraction is an ordinary unsigned comparison.
- **Example.** Exponent 129 beats exponent 128 regardless of the fractions. Equal exponents: the larger fraction bits win.
- **Limit.** A negative sign reverses the order. Exponent 255 with fraction 0 is \(+\infty\), larger than every finite encoding. A NaN is not a contestant in “largest number.”

## 3. Powers of two are fraction zero

- **Solves.** Encoding \(2^k\) and recognising it in a word.
- **When.** The value is a power of two inside the normal range, \(-126 \le k \le 127\).
- **Why.** \(2^k = 1.0 \times 2^k\), so the fraction is all zeros and the biased field is \(k+127\).
- **Example.** \(+16 = 2^4\) has biased exponent 131 and word `0x41800000`. \(+1\) is `0x3F800000`.
- **Limit.** \(2^{-126}\) is the smallest normal, word `0x00800000`, exponent field 1. \(2^{-127}\) is **not** that word; with a zero fraction it cannot be written as a normal, and `0x00400000` is the subnormal \(2^{-127}\).

## 4. Product exponents add, then lose one bias

- **Solves.** The exponent field of an exact product of two normals.
- **When.** You do not need a decimal expansion, only the result word or its exponent.
- **Why.** \((E_1-127)+(E_2-127)\) is the true power. Adding 127 stores it. Multiplying two hidden-1 significands may produce a 2, which adds one more to the exponent and shifts the fraction.
- **Example.** \(1.5 \times 4\) has biased exponent \(127+129-127=129\) and significand \(1.1_2\), word `0x40C00000`.
- **Limit.** Adding the biased fields and storing the sum uses the bias twice. If the significand product is at least 2, the shortcut without the extra +1 is off by a factor of two.

## 5. Alignment shifts the smaller operand

- **Solves.** Whether an addition needs a shift, and which way.
- **When.** Two normals are added or subtracted.
- **Why.** Both numbers must be written at the larger exponent. That divides the smaller significand by \(2^{\Delta E}\), a right shift.
- **Example.** \(1.5\) (exponent 127) added to \(2.5\) (exponent 128) shifts \(1.1_2\) right by one, adds to \(1.01_2\), and normalises \(10.00_2\) into \(1.0 \times 2^2\).
- **Limit.** A right shift can discard fraction bits. If the stem’s sum is not exact, those bits are the rounding problem. “The decimal sum is an integer” does not imply “the exponents were equal.”
