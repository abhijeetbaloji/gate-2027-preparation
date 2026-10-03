# Floating-Point Representation and Arithmetic — Practice Questions

Original practice for GATE CS. These questions are not from any GATE paper. Attempt the questions before reading the solutions.

Throughout, IEEE-754 single precision means 1 sign bit, 8 exponent bits and 23 fraction bits. The exponent bias of a normal number is 127. A normal encoding with biased field \(E\) and fraction \(f\) has value

\[
(-1)^s \times (1.f)_2 \times 2^{E - 127},
\]

where \(1 \le E \le 254\).

## Level 1 — Conceptual

## Q1 — NAT

The exponent bias used by IEEE-754 single-precision normal numbers is ______.

---

## Q2 — MSQ

Select all that apply.

A. The format uses 1 sign bit, 8 exponent bits and 23 fraction bits.

B. A normal number has a hidden leading 1 in its significand.

C. Exponent field 255 with fraction 0 represents an infinity.

D. Exponent field 255 with a nonzero fraction represents a finite number larger than \(2^{128}\).

---

## Q3 — MCQ

The biased exponent field stored for the normal number \(+1.0\) is

A. 0

B. 126

C. 127

D. 128

---

## Level 2 — Standard GATE Style

## Q4 — MCQ

The biased exponent field stored for the normal number \(+6.5\) is

A. 127

B. 128

C. 129

D. 130

---

## Q5 — NAT

The IEEE-754 single-precision pattern \(0\text{xC0A00000}\) has decimal value ______.

---

## Q6 — MSQ

Select all that apply.

A. \(0\text{x00000000}\) is \(+0\).

B. \(0\text{x80000000}\) is \(-0\).

C. \(0\text{x7F800000}\) is \(+\infty\).

D. \(0\text{x7F800000}\) is the largest finite single-precision number.

---

## Q7 — MCQ

The value of the single-precision pattern \(0\text{xBE000000}\) is

A. \(-0.125\)

B. \(-0.25\)

C. \(-1.25\)

D. \(-0.5\)

---

## Level 3 — Multi-Step

## Q8 — NAT

The biased exponent field stored for the normal number \(+16.0\) is ______.

---

## Q9 — MCQ

The exact product \(3.0 \times 5.0\), encoded as a single-precision number, is

A. \(0\text{x41700000}\)

B. \(0\text{x40F00000}\)

C. \(0\text{x41E00000}\)

D. \(0\text{x40400000}\)

---

## Q10 — MSQ

Select all that apply. The sum \(1.5 + 2.5\) is formed in single precision. Both summands and the sum are exactly representable.

A. The mathematical sum is 4.

B. The encoding of the sum is \(0\text{x40800000}\).

C. The two summands already have the same exponent, so no alignment shift is required.

D. The biased exponent of \(2.5\) is larger than the biased exponent of \(1.5\).

---

## Level 4 — Tricky / Trap-Based

## Q11 — NAT

The smallest positive normalized single-precision value equals \(2^{-k}\). The positive integer \(k\) is ______.

---

## Q12 — MCQ

A student uses bias 128 instead of 127 and therefore stores the biased field 132 for \(+16.0\), with sign 0 and fraction 0. Decoded with the real bias of 127, that bit pattern represents

A. 32

B. 16

C. 8

D. 64

---

## Level 5 — Challenge

## Q13 — NAT

The pattern \(0\text{x00000001}\) is a positive subnormal number. Its value is \(2^{-k}\). The positive integer \(k\) is ______.

A subnormal has exponent field 0 and a nonzero fraction. It does not use a hidden 1. Its significand is \((0.f)_2\), and the power of two is \(2^{-126}\), the same power as the smallest normal exponent.

---

## Q14 — MSQ

Select all that apply.

A. \(0\text{x00800000}\) is the smallest positive normal and equals \(2^{-126}\).

B. \(0\text{x00400000}\) is a positive subnormal and equals \(2^{-127}\).

C. \(0\text{x00400000}\) is a normal number whose unbiased exponent is \(-127\).

D. Every positive subnormal is strictly smaller than every positive normal.

## Answer Key

| Q | Type | Answer |
|---|------|--------|
| 1 | NAT | 127 |
| 2 | MSQ | A, B, C |
| 3 | MCQ | C |
| 4 | MCQ | C |
| 5 | NAT | -5 |
| 6 | MSQ | A, B, C |
| 7 | MCQ | A |
| 8 | NAT | 131 |
| 9 | MCQ | A |
| 10 | MSQ | A, B, D |
| 11 | NAT | 126 |
| 12 | MCQ | A |
| 13 | NAT | 149 |
| 14 | MSQ | A, B, D |

## Detailed Solutions

### Q1

Answer: **127**

The single-precision exponent field has 8 bits. For normal numbers the all-zero and all-ones fields are reserved, leaving biased codes 1 through 254. The bias is \(2^{8-1} - 1 = 127\), so those codes represent unbiased exponents \(-126\) through \(+127\). Using 128 shifts every power by one. Using 126 does the same in the other direction.

### Q2

Answer: **A, B, C**

The field widths \(1 + 8 + 23 = 32\) are the single-precision layout. A normal significand is \(1.f\), and the leading 1 is hidden: it is not stored in the 23 fraction bits. Exponent field \(255 = 11111111_2\) with fraction 0 is infinity; the sign bit chooses \(+\infty\) or \(-\infty\).

The same exponent field with a nonzero fraction is NaN, not a finite magnitude. There is no finite single-precision number at or above \(2^{128}\). The largest finite unbiased exponent is \(+127\).

### Q3

Answer: **C**

\(1.0 = 1.0 \times 2^0\). The unbiased exponent is 0, so the stored field is \(0 + 127 = 127 = 01111111_2\). The full word is \(0\text{x3F800000}\).

Option (A) is the reserved all-zero exponent, used by zeros and subnormals, not by \(1.0\). Option (B) is the encoding of \(0.5 = 2^{-1}\), whose field is \(127 - 1 = 126\). Option (D) is the encoding of \(2.0\).

### Q4

Answer: **C**

\(6.5 = 110.1_2 = 1.101_2 \times 2^2\). The unbiased exponent is 2, so the biased field is \(2 + 127 = 129\). The fraction begins \(101\), and the word is \(0\text{x40D00000}\).

Option (D), 130, is the off-by-one from using bias 128: \(2 + 128 = 130\). That field actually encodes \(2^{130-127} = 2^3 = 8\) times a significand, not the exponent of 6.5. Option (B) would be correct for an unbiased exponent of 1, which is the normalization of 3 or of 2.5, not of 6.5. Option (A) is the field for an unbiased exponent of 0.

### Q5

Answer: **-5**

Split \(0\text{xC0A00000} = 1100\,0000\,1010\,0000\,0000\,0000\,0000\,0000_2\).

- Sign bit 1, so the value is negative.
- Exponent field \(10000001_2 = 129\). Unbiased exponent \(129 - 127 = 2\).
- Fraction \(010\ldots_2\), so the significand is \(1.01_2 = 1.25\).

The magnitude is \(1.25 \times 2^2 = 5\), and the signed value is \(-5\). Using bias 128 instead produces unbiased exponent \(129 - 128 = 1\) and the wrong magnitude \(1.25 \times 2 = 2.5\).

### Q6

Answer: **A, B, C**

Exponent field 0 and fraction 0 encode zero. The sign bit still distinguishes \(+0\) from \(-0\), so \(0\text{x00000000}\) and \(0\text{x80000000}\) are the two zeros. Exponent field 255 and fraction 0 encode infinity, so \(0\text{x7F800000}\) is \(+\infty\).

It is not the largest finite value. The largest finite encoding has exponent field 254, not 255, and fraction all 1s. Its unbiased exponent is \(254 - 127 = 127\). Treating the infinity code as a large finite number ignores the reserved exponent.

### Q7

Answer: **A**

\(0\text{xBE000000} = 1011\,1110\,0000\ldots_2\).

- Sign bit 1.
- Exponent field \(01111100_2 = 124\).
- Fraction 0, so the significand is exactly \(1.0\).

The unbiased exponent is \(124 - 127 = -3\). The value is \(-2^{-3} = -0.125\).

Option (B) is \(-2^{-2}\). It is what the same fraction gives if the unbiased exponent is taken to be \(-2\) instead of \(-3\), a one-step bias error. Option (D) is \(-2^{-1}\), the value for biased field 126. Option (C) invents a nonzero fraction that is not present; the low 23 bits of this word are 0.

### Q8

Answer: **131**

\(16 = 10000_2 = 1.0 \times 2^4\). The biased field is \(4 + 127 = 131 = 10000011_2\), and the word is \(0\text{x41800000}\).

The two nearby wrong answers are 132, from bias 128, and 130, from adding 4 to 126. Both are one away from the bias definition \(2^{k-1} - 1\). The stored field is the unbiased exponent plus 127, not plus 126 and not plus 128.

### Q9

Answer: **A**

\(3 = 1.1_2 \times 2^1\) and \(5 = 1.01_2 \times 2^2\), so the exact product is 15. Then

\[
15 = 1111_2 = 1.111_2 \times 2^3.
\]

The biased exponent is \(3 + 127 = 130 = 10000010_2\), and the fraction begins \(111\). The word is

\[
0\,10000010\,11100000000000000000000_2 = 0\text{x41700000}.
\]

Option (D) is the encoding of 3.0 itself, \(0\text{x40400000}\). Option (B) has exponent field 129 and fraction \(111\), so it is \(1.111_2 \times 2^2 = 7.75\). Option (C) has exponent field 131 and fraction \(110\), so it is \(1.11_2 \times 2^4 = 28\).

### Q10

Answer: **A, B, D**

\(1.5 = 1.1_2 \times 2^0\), with biased exponent 127. \(2.5 = 1.01_2 \times 2^1\), with biased exponent 128. The second exponent is larger, so (D) is true and (C) is false. Alignment shifts 1.5 one place right relative to exponent 1, producing \(0.11_2 \times 2^1\). Adding the significands gives

\[
1.01_2 + 0.11_2 = 10.00_2 = 1.0_2 \times 2^1,
\]

which normalizes to \(1.0 \times 2^2 = 4\). The biased field of 4 is \(2 + 127 = 129\), and the word is \(0\text{x40800000}\). The sum is exact in single precision; this particular addition needs no rounding.

### Q11

Answer: **126**

The smallest biased field that still means a normal number is 1, not 0. Field 0 is reserved for zero and subnormals. The corresponding unbiased exponent is \(1 - 127 = -126\). With the smallest normal fraction, which is 0, the value is \(1.0 \times 2^{-126}\).

Answering 127 applies \(0 - 127\) and treats the reserved field as a normal exponent. Answering 149 gives the smallest positive subnormal, which is a different encoding: exponent field 0, hidden bit 0, and only the last fraction bit set. The smallest normal is larger than every subnormal.

### Q12

Answer: **A**

The correct field for \(16 = 2^4\) is \(4 + 127 = 131\). Bias 128 produces \(4 + 128 = 132\). Decode that incorrect field with the real rule:

\[
132 - 127 = 5, \qquad 1.0 \times 2^5 = 32.
\]

The wrong bias does not merely label 16 incorrectly inside an otherwise private code. The bits 132 are a legal normal encoding of a different number, 32. The one-count error in the bias becomes a factor-of-two error in the value. Option (B) would be right only if the decoder used the same wrong bias the student used. The hardware decoder uses 127.

### Q13

Answer: **149**

The word \(0\text{x00000001}\) has sign 0, exponent field 0 and fraction bit 0 set in the \(2^{-23}\) place only. Because the exponent field is 0, the hidden bit is 0 rather than 1, and the power is \(2^{-126}\) rather than \(2^{0 - 127}\).

\[
(0.f)_2 \times 2^{-126} = 2^{-23} \times 2^{-126} = 2^{-149}.
\]

Two off-by-one readings give a different power. Applying the normal formula anyway produces \((1 + 2^{-23}) \times 2^{-127}\), which is about \(2^{-127}\), not \(2^{-149}\). Keeping the subnormal significand but still subtracting the bias from a stored 0 produces \(2^{-23} \times 2^{-127} = 2^{-150}\). The subnormal power is fixed at \(-126\), one larger than \(0 - 127\), which is why the last-bit subnormal is \(2^{-149}\) and not \(2^{-150}\).

### Q14

Answer: **A, B, D**

\(0\text{x00800000}\) has exponent field 1 and fraction 0. That is the smallest normal code, and its value is \(1.0 \times 2^{1 - 127} = 2^{-126}\).

\(0\text{x00400000}\) has exponent field 0, so it is not normal. Its leading fraction bit is 1, and the other fraction bits are 0, so

\[
(0.1)_2 \times 2^{-126} = 2^{-1} \times 2^{-126} = 2^{-127}.
\]

The value \(2^{-127}\) is real, but the unbiased exponent \(-127\) is not a normal exponent. Normal unbiased exponents stop at \(-126\). Option (C) takes a numerical coincidence and turns it into a normal encoding. The coincidence is that half of \(2^{-126}\) equals \(2^{-127}\). A normal decoding of some other field is not what these bits are.

Every positive subnormal uses exponent field 0 and is at most \((1 - 2^{-23}) \times 2^{-126}\), which is strictly below the smallest positive normal \(2^{-126}\). So every positive subnormal is strictly smaller than every positive normal.
