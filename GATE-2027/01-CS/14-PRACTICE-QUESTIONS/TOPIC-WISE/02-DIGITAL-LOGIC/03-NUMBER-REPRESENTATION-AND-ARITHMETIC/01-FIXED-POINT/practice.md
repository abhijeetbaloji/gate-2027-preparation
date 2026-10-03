# Fixed-Point Representation and Arithmetic — Practice Questions

Original practice for GATE CS. These questions are not from any GATE paper. Attempt the questions before reading the solutions.

## Level 1 — Conceptual

## Q1 — MCQ

The range of an 8-bit unsigned integer is

A. 0 to 255

B. 0 to 256

C. \(-128\) to 127

D. \(-127\) to 127

---

## Q2 — MSQ

Select all that apply. Which of the following 6-bit patterns represent the value \(-5\)?

A. Sign-magnitude \(100101\)

B. Ones' complement \(111010\)

C. Two's complement \(111011\)

D. Two's complement \(100101\)

---

## Q3 — NAT

The most negative integer representable in 7-bit two's complement is ______.

---

## Q4 — MCQ

The 4-bit two's-complement pattern \(1011\) has decimal value

A. \(-5\)

B. \(-3\)

C. \(11\)

D. \(-4\)

---

## Level 2 — Standard GATE Style

## Q5 — MCQ

The 4-bit two's-complement addition \(0101 + 0100\) produces

A. bits \(1001\), carry-out 0, and signed overflow

B. bits \(1001\), carry-out 0, and no signed overflow

C. bits \(1001\), carry-out 1, and signed overflow

D. bits \(0111\), with no signed overflow

---

## Q6 — NAT

Interpreted as an 8-bit two's-complement integer, the pattern \(11000011\) has decimal value ______.

---

## Q7 — MSQ

Select all that apply. For 6-bit ones' complement representation,

A. the set of representable values is symmetric about zero

B. both \(000000\) and \(111111\) represent zero

C. exactly 63 distinct numeric values are representable

D. the most negative representable value is \(-32\)

---

## Q8 — MCQ

In 4-bit ones' complement, with end-around carry, \(0101 + 1101\) equals

A. \(0011\)

B. \(0010\)

C. the five-bit sum \(10010\), which is already the final ones'-complement result

D. \(1111\)

---

## Level 3 — Multi-Step

## Q9 — MCQ

The 4-bit two's-complement addition \(1101 + 1101\) produces

A. bits \(1010\), carry-out 1, and no signed overflow

B. bits \(1010\), carry-out 1, and signed overflow

C. bits \(1010\), carry-out 0, and signed overflow

D. bits \(0110\), carry-out 1, and no signed overflow

---

## Q10 — NAT

In 6-bit two's complement, the sum of \(+14\) and \(-19\) has decimal value ______.

---

## Q11 — MSQ

Select all that apply. The 5-bit two's-complement pattern \(10110\) is sign-extended to 8 bits.

A. The 8-bit pattern is \(11110110\).

B. The 8-bit pattern still represents \(-10\).

C. The 8-bit pattern is \(10010110\).

D. Sign extension copies the original sign bit into every new high-order bit.

---

## Level 4 — Tricky / Trap-Based

## Q12 — MSQ

Select all that apply. All additions below are 4-bit two's complement.

A. \(0111 + 0001\) produces signed overflow.

B. \(1111 + 0001\) produces carry-out 1 and no signed overflow.

C. \(1100 + 1011\) produces carry-out 1 and signed overflow.

D. Signed overflow occurs exactly when the carry into the sign bit equals the carry out of the sign bit.

---

## Q13 — NAT

The two's-complement negation procedure (invert every bit, then add 1, keeping 5 bits) is applied to the 5-bit pattern \(10110\). The resulting pattern, read as a 5-bit two's-complement integer, has decimal value ______.

---

## Q14 — MCQ

The same negation procedure, now keeping 4 bits, is applied to \(1000\). The result is

A. \(1000\), which still represents \(-8\)

B. \(1000\), which represents \(+8\)

C. \(0111\), which represents \(+7\)

D. \(0000\), which represents \(0\)

---

## Level 5 — Challenge

## Q15 — NAT

How many 8-bit patterns are unchanged by two's-complement negation (invert every bit, add 1, and discard the carry out of the eighth bit)? ______.

---

## Q16 — MCQ

Which addition does not cause signed overflow in 5-bit two's complement?

A. \(01001 + 00111\)

B. \(10001 + 10001\)

C. \(01101 + 10010\)

D. \(01111 + 00001\)

## Answer Key

| Q | Type | Answer |
|---|------|--------|
| 1 | MCQ | A |
| 2 | MSQ | A, B, C |
| 3 | NAT | -64 |
| 4 | MCQ | A |
| 5 | MCQ | A |
| 6 | NAT | -61 |
| 7 | MSQ | A, B, C |
| 8 | MCQ | A |
| 9 | MCQ | A |
| 10 | NAT | -5 |
| 11 | MSQ | A, B, D |
| 12 | MSQ | A, B, C |
| 13 | NAT | 10 |
| 14 | MCQ | A |
| 15 | NAT | 2 |
| 16 | MCQ | C |

## Detailed Solutions

### Q1

Answer: **A**

Eight bits give \(2^8 = 256\) codes, namely the integers 0 through 255. The upper endpoint is \(2^8 - 1\), not \(2^8\). Options (C) and (D) are signed ranges: (C) is 8-bit two's complement, and (D) is 8-bit sign-magnitude or ones' complement.

### Q2

Answer: **A, B, C**

The positive magnitude is \(000101\).

- Sign-magnitude flips only the sign bit: \(100101\).
- Ones' complement flips every bit: \(111010\).
- Two's complement adds one to the ones' complement: \(111011\).

Option (D) reuses the sign-magnitude pattern and calls it two's complement. That pattern is \(+5\) with the sign bit set, which in two's complement is \(-27\), not \(-5\). Check: \(111011_2 = 59\), and \(59 - 64 = -5\).

### Q3

Answer: **-64**

An \(n\)-bit two's-complement integer runs from \(-2^{n-1}\) to \(2^{n-1} - 1\). For \(n = 7\) the lower end is \(-2^6 = -64\), and the upper end is 63. Answering \(-63\) uses the ones'-complement or sign-magnitude endpoint. Answering \(-128\) uses eight bits.

### Q4

Answer: **A**

Invert \(1011\) to get \(0100\), then add 1 to get \(0101 = +5\). The original pattern is therefore \(-5\). Equivalently, a pattern with the sign bit set has value \(-8 + 2 + 1 = -5\).

Option (B), \(-3\), is the pattern \(1101\). Option (C) reads the bits as unsigned. Option (D), \(-4\), is \(1100\). Stopping after the invert and forgetting to add 1 produces \(0100 = 4\) as the magnitude and tempts the answer \(-4\).

### Q5

Answer: **A**

\(0101_2 + 0100_2 = 1001_2\), and the sum fits in four bits, so the carry-out is 0. The operands are \(+5\) and \(+4\). Their true sum is \(+9\), which is outside the 4-bit two's-complement range \(-8\) through \(+7\). The stored pattern \(1001\) means \(-7\). Both operands are positive and the result is negative, so this is signed overflow.

Carry-out 0 does not mean "no overflow". Here the carry into the sign bit is 1 and the carry out of the sign bit is 0. Overflow is the XOR of those two carries, which is 1. Option (B) looks only at the carry-out. Option (D) is the true mathematical sum with its overflow bit discarded, not the four stored bits.

### Q6

Answer: **-61**

\(11000011_2 = 195\) as an unsigned byte. With the sign bit set, the two's-complement value is \(195 - 256 = -61\). The invert-and-add check: the complement of \(11000011\) is \(00111100\), plus 1 is \(00111101 = 61\), so the original value is \(-61\). Answering 195 ignores the sign. Answering \(-67\) inverts the bits and forgets the final \(+1\): \(00111100 = 60\), and \(60\) is not the magnitude.

### Q7

Answer: **A, B, C**

Ones' complement represents every magnitude from 0 through \(2^{5} - 1 = 31\) with either sign. The positive and negative ranges therefore match, which is (A). The all-zero and all-one words are \(+0\) and \(-0\), two encodings of the same number. Distinct values run from \(-31\) to \(+31\), which is 63 numbers. There are 64 patterns and one duplicated value.

The most negative value is \(-31\), not \(-32\). The extra negative code \(-2^{n-1}\) belongs to two's complement. That is why (D) is false for this representation even though it would be true for 6-bit two's complement.

### Q8

Answer: **A**

\(1101\) is the ones' complement of \(0010\), so the addition is \(+5 + (-2)\). The raw binary sum is \(10010_2\). The end-around step adds the carry-out back into the low nibble:

\[
0010 + 1 = 0011.
\]

The result is \(+3\), as expected. Option (B) stops before the end-around addition and is short by 1. Option (C) treats a ones'-complement adder as an ordinary five-bit adder. Option (D) is the ones' complement of zero, not the sum.

### Q9

Answer: **A**

\(1101\) means \(-3\). Then \(-3 + (-3) = -6\), and \(-6\) in four bits is \(1010\). The raw sum is \(11010_2\), so the stored nibble is \(1010\) and the carry-out is 1.

Both operands are negative and the stored result is negative, so there is no signed overflow. The carry into the sign is 1 and the carry out of the sign is 1; their XOR is 0. Carry-out 1 is not by itself an overflow. It would be the unsigned indication that \(13 + 13\) does not fit in four bits. Signed overflow is a different predicate, and it is false here because \(-6\) fits.

### Q10

Answer: **-5**

The 6-bit two's complement of 19 is the invert of \(010011\), which is \(101100\), plus 1, which is \(101101\). Add the representation of 14:

\[
001110 + 101101 = 111011.
\]

There is no carry out of the sixth bit. The pattern \(111011\) has sign bit 1, so its value is \(59 - 64 = -5\). This matches \(14 - 19\). The missing carry-out is not a signed overflow: the operands have opposite signs, and \(-5\) fits in \(-32\) through \(+31\).

### Q11

Answer: **A, B, D**

\(10110\) has sign bit 1 and value \(-16 + 4 + 2 = -10\). Sign extension copies that 1 into the three new high bits, giving \(11110110\). Copying the sign preserves the value: the new weight of the sign is \(-128\), and the three inserted 1s contribute \(64 + 32 + 16 = 112\), so the change in place value is \(-128 + 112 = -16\), which cancels the old sign weight. The 8-bit word still means \(-10\).

Option (C) writes a leading 1, then zeros, then the old low bits. That is not sign extension. It means \(-128 + 16 + 4 + 2 = -106\).

### Q12

Answer: **A, B, C**

- \(0111 + 0001 = 1000\). The values are \(+7 + 1 = +8\), stored as \(-8\). Carry-out is 0. The sign changed from positive to negative, so overflow is real.
- \(1111 + 0001 = 0000\) with carry-out 1. The values are \(-1 + 1 = 0\), which is correct. No overflow. A carry-out occurred because the unsigned reading \(15 + 1\) crossed 16.
- \(1100 + 1011 = 0111\) with carry-out 1. The values are \(-4 + (-5) = -9\), stored as \(+7\). Two negatives produced a positive, so overflow is real even though a carry-out is present.

Overflow is the XOR of the carry into the sign and the carry out of the sign. It occurs when those carries differ, not when they are equal. Option (D) states the complementary condition and would declare the overflowing cases safe and the safe case \(1111 + 0001\) unsafe.

### Q13

Answer: **10**

The pattern \(10110\) is \(-16 + 4 + 2 = -10\). Invert it to \(01001\), then add 1 to get \(01010 = +10\). Negation is legal here because \(+10\) fits in five bits. The value of the resulting pattern is \(+10\), not a negative number: the procedure produces the representation of the additive inverse, and the inverse of a negative value is positive.

Inverting without the final \(+1\) leaves \(01001 = 9\), which is neither \(+10\) nor the two's-complement result. The same off-by-one appears whenever the magnitude is recovered by inversion alone.

### Q14

Answer: **A**

Invert \(1000\) to get \(0111\), then add 1 to get \(1000\) again. The procedure returns the same pattern. In 4-bit two's complement that pattern means \(-8\), not \(+8\). The integer \(+8\) is not in the range \(-8\) through \(+7\). This is the one nonzero value whose negation cannot be represented; the modular result wraps to itself because \(-(-8) = 8 \equiv -8 \pmod{16}\).

Option (C) is the invert step before adding 1. Option (B) reads a sign bit of 1 as if the remaining bits were an unsigned magnitude of 8. Sign-magnitude would do that; two's complement does not.

### Q15

Answer: **2**

Negation leaves a pattern \(x\) fixed when \(2x \equiv 0 \pmod{256}\), so \(x \equiv 0\) or \(x \equiv 128 \pmod{256}\). The two patterns are \(00000000\), whose value is 0, and \(10000000\), whose value is \(-128\).

The second fixed point is the case of Q14 extended to eight bits. The integer equation \(x = -x\) has only the solution 0, but the 8-bit adder implements arithmetic modulo 256. Under that modulus \(-128\) is its own additive inverse, because \(128\) is not a representable positive value and \(10000000 + 10000000\) wraps to \(00000000\). Answering 1 counts only zero and misses the minimum representable value.

### Q16

Answer: **C**

The 5-bit range is \(-16\) through \(+15\).

- (A) \(+9 + 7 = +16\), stored as \(10000 = -16\). Positive plus positive gives negative: overflow.
- (B) \(-15 + (-15) = -30\), stored as \(00010 = +2\) with carry-out 1. Negative plus negative gives positive: overflow.
- (C) \(+13 + (-14) = -1\), stored as \(11111\). The operands have opposite signs, so overflow is impossible. The stored result equals the true sum.
- (D) \(+15 + 1 = +16\), stored as \(10000 = -16\). Overflow, and the carry-out is 0.

The safe addition is the one whose operands disagree in sign. Carry-out is 1 only in (B), which is nevertheless an overflow. Carry-out is 0 in (A) and (D), which also overflow.
