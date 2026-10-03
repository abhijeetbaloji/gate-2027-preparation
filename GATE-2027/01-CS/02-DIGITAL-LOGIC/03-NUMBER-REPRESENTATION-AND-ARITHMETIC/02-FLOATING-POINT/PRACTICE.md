# Floating Point — Practice

Original questions. IEEE-754 single precision: 1 sign bit, 8 exponent bits, 23 fraction bits, bias 127 for normals. They are not previous-year questions.

## Level 1 — Conceptual

### Q1 — MCQ

The biased exponent stored for the normal number \(+1.0\) is

A. 0

B. 1

C. 127

D. 128

**Answer.** C

**Concept.** Bias places true exponent 0 at 127.

**Difficulty.** Level 1

**Solution.** \(+1 = 1.0 \times 2^0\). The stored field is \(0+127 = 127\). Field 0 is the zero/subnormal code, not the exponent of 1.

---

### Q2 — MSQ

Select all that apply.

A. `0x00000000` is \(+0\).

B. `0x80000000` is \(-0\).

C. `0x7F800000` is \(+\infty\).

D. `0x7F800000` is the largest finite single-precision number.

**Answer.** A, B, C

**Concept.** Reserved exponent fields.

**Difficulty.** Level 1

**Solution.** Exponent 0 and fraction 0 is zero; the sign bit still distinguishes \(+0\) and \(-0\). Exponent 255 and fraction 0 is infinity. The largest finite number has exponent 254 and a fraction of all 1s. `0x7F800000` is not finite.

---

## Level 2 — Standard GATE

### Q3 — NAT

The single-precision word `0xC0000000` has decimal value ______.

**Answer.** -2

**Concept.** Hex field split.

**Difficulty.** Level 2

**Solution.** `1100 0000 0000 …` Sign 1. Exponent `10000000` = 128. Fraction 0. Value \(-1.0 \times 2^{128-127} = -2\).

---

### Q4 — MCQ

The word `0x40400000` represents

A. 1.5

B. 2

C. 3

D. 4

**Answer.** C

**Concept.** Hidden 1 and a short fraction.

**Difficulty.** Level 2

**Solution.** `0100 0000 0100 …` Sign 0. Exponent `10000000` = 128, power \(2^1\). The fraction’s leading bit is 1, so the significand is \(1.1_2 = 1.5\). Value \(1.5 \times 2 = 3\).

---

## Level 3 — Multi-step

### Q5 — NAT

The biased exponent field of the normal number \(+0.5\) is ______.

**Answer.** 126

**Concept.** Normalise before biasing.

**Difficulty.** Level 3

**Solution.** \(0.5 = 1.0 \times 2^{-1}\). It is normal, not subnormal. Biased field \(-1 + 127 = 126\).

---

### Q6 — MCQ

The exact product \(2.0 \times 2.0\), encoded as a single-precision number, is

A. `0x40000000`

B. `0x40800000`

C. `0x41000000`

D. `0x40400000`

**Answer.** B

**Concept.** Product exponent \(E_1+E_2-127\).

**Difficulty.** Level 3

**Solution.** Each factor is \(1.0 \times 2^1\), biased exponent 128, word `0x40000000`. Product significand \(1.0\), unbiased exponents \(1+1=2\), biased field \(128+128-127 = 129\). That is \(1.0 \times 2^2 = 4\), word `0x40800000`. Option C is \(+8\) (exponent 130). Option D is \(+3\).

---

## Level 4 — Trap

### Q7 — MCQ

A student uses bias 128 and therefore stores biased field 131 for \(+8.0\), with sign 0 and fraction 0. Decoded with the real bias of 127, that pattern represents

A. 8

B. 16

C. 4

D. 32

**Answer.** B

**Concept.** A wrong bias scales the value by a power of two.

**Difficulty.** Level 4

**Solution.** \(+8 = 2^3\) should be stored as \(3+127 = 130\). Bias 128 stores \(3+128 = 131\). Decoding with 127 gives power \(131-127 = 4\), value \(2^4 = 16\). Fraction 0, so no further correction.

---

## Level 5 — Challenge

### Q8 — NAT

The word `0x00200000` is a positive subnormal. Its value is \(2^{-k}\). The positive integer \(k\) is ______.

**Answer.** 128

**Concept.** Subnormal power \(2^{-126}\) and no hidden 1.

**Difficulty.** Level 5

**Solution.** The exponent field is 0, so the normal formula does not apply. `0x00200000` sets bit 21 of the word. Fraction bit 22 would be weight \(2^{-1}\) in \(0.f\); bit 21 is weight \(2^{-2}\). Significand \(0.01_2 = 2^{-2}\). Subnormal scale \(2^{-126}\). Value \(2^{-2} \times 2^{-126} = 2^{-128}\).

**Trap.** Using a hidden 1, which would make this a normal with exponent 0, or using power \(2^{-127}\).
