# Fixed Point — Practice

Original questions on range, two’s-complement value, overflow, sign extension, and Booth. They are not previous-year questions.

## Level 1 — Conceptual

### Q1 — MCQ

The range of a 5-bit two’s-complement integer is

A. \(-16\) to \(15\)

B. \(-15\) to \(15\)

C. \(-16\) to \(16\)

D. \(0\) to \(31\)

**Answer.** A

**Concept.** \(-2^{n-1}\) through \(2^{n-1}-1\).

**Difficulty.** Level 1

**Solution.** \(n=5\): \(-16\) through \(15\). Option B is the ones’-complement range. Option D is unsigned.

---

### Q2 — NAT

The most negative integer representable in 6-bit two’s complement is ______.

**Answer.** -32

**Concept.** The MSB weight.

**Difficulty.** Level 1

**Solution.** \(-2^{5} = -32\). The pattern is \(100000\). It is not \(-31\).

---

## Level 2 — Standard GATE

### Q3 — MCQ

The 4-bit pattern \(1101\), read as a two’s-complement integer, equals

A. \(-3\)

B. \(-5\)

C. \(13\)

D. \(-2\)

**Answer.** A

**Concept.** Negative MSB weight.

**Difficulty.** Level 2

**Solution.** \(-8 + 4 + 1 = -3\). Unsigned reading is 13. Ones’ complement of \(1101\) is the flip, which is a different code: flip of \(0010\) is \(1101\), so ones’ complement would be \(-2\).

---

### Q4 — NAT

Interpreted as an 8-bit two’s-complement integer, \(11110001\) equals ______.

**Answer.** -15

**Concept.** Flip and add 1.

**Difficulty.** Level 2

**Solution.** Flip \(00001110\), add 1, get \(00001111 = 15\). The value is \(-15\). Weight check: \(-128 + 64 + 32 + 16 + 1 = -15\).

---

## Level 3 — Multi-step

### Q5 — MSQ

Select all that apply. All additions are 4-bit. “Signed” means two’s complement.

A. \(0110 + 0011\) produces signed overflow.

B. \(1110 + 1110\) produces carry-out 1 and no signed overflow.

C. \(0111 + 0001\) produces signed overflow.

D. Signed overflow occurs when the carry into the sign equals the carry out of the sign.

**Answer.** A, B, C

**Concept.** Same-sign test versus carry-out.

**Difficulty.** Level 3

**Solution.** \(0110+0011 = 1001\). Both addends are positive and the stored sign is negative, so the signed sum overflows (\(6+3=9\), and 4-bit two’s complement stops at 7).

\(1110+1110 = 1100\) with carry-out 1. Both addends are negative and the stored sign stays negative: \(-2 + -2 = -4\), which fits. Carry-out 1 is not signed overflow.

\(0111+0001 = 1000\). Positive plus positive stored as a negative: \(7+1\) overflows.

Overflow is the case where the carry into the sign **differs** from the carry out. Option D states the opposite test.

**Trap.** Treating carry-out 1 as signed overflow. That rejects the correct addition \(-2 + -2\).

---

### Q6 — NAT

Booth’s algorithm multiplies by the 6-bit two’s-complement multiplier \(110100\). The imaginary bit below the LSB is 0. The number of addition and subtraction operations is ______.

**Answer.** 3

**Concept.** Count transitions, not 1-bits.

**Difficulty.** Level 3

**Solution.** Bits \(Q_5\ldots Q_0 = 110100\), \(Q_{-1}=0\).

| \(i\) | Pair | Action |
|------:|------|--------|
| 0 | 0, 0 | none |
| 1 | 0, 0 | none |
| 2 | 1, 0 | subtract |
| 3 | 0, 1 | add |
| 4 | 1, 0 | subtract |
| 5 | 1, 1 | none |

Three operations. The three 1-bits are not three operations; the top two 1s are a run and contribute only the subtract at \(i=4\).

---

## Level 4 — Trap

### Q7 — MCQ

Negating the 5-bit two’s-complement pattern \(10000\) by flipping all bits and adding 1, while keeping 5 bits, produces

A. \(10000\), which still represents \(-16\)

B. \(10000\), which represents \(+16\)

C. \(01111\), which represents \(+15\)

D. \(00000\)

**Answer.** A

**Concept.** The most negative value is its own negation inside this width.

**Difficulty.** Level 4

**Solution.** Flip \(01111\), add 1, get \(10000\). The pattern is unchanged and the only value it has in 5-bit two’s complement is \(-16\). \(+16\) needs a sixth bit.

---

## Level 5 — Challenge

### Q8 — NAT

The 6-bit two’s-complement integers \(+13\) and \(-18\) are added. The sum, as a decimal integer, is ______. The 6-bit width can represent the result.

**Answer.** -5

**Concept.** Add the patterns; the result fits, so the stored value is the true sum.

**Difficulty.** Level 5

**Solution.** \(+13 = 001101\). \(-18\): magnitude \(010010\), flip \(101101\), add 1, get \(101110\).

```
  001101
+ 101110
= 111011
```

Carry out is 0. \(111011 = -32 + 16 + 8 + 2 + 1 = -5\). And \(13 + (-18) = -5\), which lies between \(-32\) and \(31\), so there is no overflow to repair.

**Trap.** Reading \(111011\) as unsigned 59, or as sign-magnitude \(-27\).
