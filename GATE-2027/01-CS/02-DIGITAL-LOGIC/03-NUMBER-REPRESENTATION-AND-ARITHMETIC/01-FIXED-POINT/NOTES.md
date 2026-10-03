# Fixed-Point Representation and Arithmetic

Fixed-point means the binary point is in a known place. Integers are the special case where the point sits at the right of the LSB. The mapped questions (see `PYQ.md`) are two’s-complement range and negation, overflow, sign extension, a Booth multiplication count, and one unsigned fraction with the point in the middle of the byte. Floating-point encoding is the next folder.

---

## 1. Three signed codes

An \(n\)-bit pattern is just \(n\) bits. The code says which integer it means.

**Unsigned.** Weights \(2^{n-1}, \ldots, 2^0\). Range \(0\) through \(2^n - 1\). Every pattern is a different value. There is no sign bit.

**Sign-magnitude.** The MSB is the sign, 1 meaning negative. The other \(n-1\) bits are the magnitude. Range \(-(2^{n-1}-1)\) through \(+(2^{n-1}-1)\). Both \(000\ldots 0\) and \(100\ldots 0\) mean zero. There are \(2^n\) patterns and \(2^n - 1\) distinct values.

**Ones’ complement.** Negating flips every bit. Range is the same as sign-magnitude, and there are again two zeros: \(000\ldots 0\) and \(111\ldots 1\). Addition uses **end-around carry**: a carry out of the MSB is added back into the LSB. That is required because the two zeros must behave as the same number, and because the bit-flip negation is off by one from two’s complement.

**Two’s complement.** Negating flips every bit and then adds 1, discarding any carry out of the MSB. Weights:

\[
-b_{n-1}\, 2^{n-1} + \sum_{i=0}^{n-2} b_i 2^i.
\]

Range \(-2^{n-1}\) through \(2^{n-1}-1\). One zero. Every pattern is a different integer, so an \(n\)-bit two’s-complement code has \(2^n\) values and a sign-magnitude code has \(2^n - 1\). Their difference is 1. That is the 2016 comparison of 16-bit codes.

| Code | Most negative | Most positive | Zeros | Distinct values |
|------|---------------|---------------|-------|----------------:|
| Unsigned | 0 | \(2^n-1\) | one (the number 0) | \(2^n\) |
| Sign-magnitude | \(-(2^{n-1}-1)\) | \(2^{n-1}-1\) | two | \(2^n-1\) |
| Ones’ complement | \(-(2^{n-1}-1)\) | \(2^{n-1}-1\) | two | \(2^n-1\) |
| Two’s complement | \(-2^{n-1}\) | \(2^{n-1}-1\) | one | \(2^n\) |

**Example, 4 bits.** \(1011\). Unsigned 11. Sign-magnitude \(-3\). Ones’ complement: flip of \(0100\) is \(1011\), so \(-4\). Two’s complement: \(-8+2+1 = -5\). The same bits are four different numbers. The stem has to name the code.

**Example, 6-bit \(-5\).** Magnitude \(000101\). Sign-magnitude \(100101\). Ones’ complement \(111010\). Two’s complement \(111011\).

**Most negative \(n\)-bit two’s-complement integer.** \(-2^{n-1}\). For 8 bits, \(-128\). For 7 bits, \(-64\). It is not \(-(2^{n-1}-1)\). That smaller-magnitude number is the ones’-complement extreme.

---

## 2. Why two’s-complement negation is “flip and add 1”

The pattern for \(x\) and the pattern for \(-x\) should sum to 0, modulo \(2^n\). Flipping bits produces \((2^n - 1) - x\), which is one less than a multiple of \(2^n\) minus \(x\). Adding 1 produces \(2^n - x\), which is \(-x\) modulo \(2^n\).

**The bit that has no partner.** \(-2^{n-1}\) is representable. \(+2^{n-1}\) is not: the positive side stops at \(2^{n-1}-1\). Negating the pattern \(100\ldots 0\) flips it to \(011\ldots 1\) and adds 1, which returns \(100\ldots 0\). The operation stays inside \(n\) bits and the pattern is unchanged. It still means \(-2^{n-1}\), not \(+2^{n-1}\).

**Patterns fixed by negation.** \(2x \equiv 0 \pmod{2^n}\), so \(x \equiv 0\) or \(x \equiv 2^{n-1}\). Exactly two \(n\)-bit patterns: all zeros, and the single 1 in the MSB. For \(n=8\), those are \(0\) and \(-128\).

---

## 3. Addition, and the two different overflows

Bit addition is identical for unsigned and two’s complement. The interpretation of the carry out is not.

**Unsigned overflow.** The true sum does not fit when the carry out of the MSB is 1. The stored \(n\) bits are the sum modulo \(2^n\).

**Two’s-complement overflow.** The true signed sum does not fit when the two operands have the same sign and the sum bit has the opposite sign. Equivalently, the carry **into** the sign bit differs from the carry **out of** the sign bit.

**Why those match.** A carry into the sign that does not leave the sign flips the sign bit. A carry that both enters and leaves does not flip it. Opposite-sign operands cannot overflow: their sum lies strictly between them.

**Worked rows, 4-bit.**

| Add | Bits | \(C_{out}\) | Carry into sign | Signed reading | Overflow? |
|-----|------|------------:|----------------:|----------------|-----------|
| \(5+4\) | \(0101+0100=1001\) | 0 | 1 | \(5+4=9\), stored \(-7\) | yes |
| \((-3)+(-3)\) | \(1101+1101=1010\) | 1 | 1 | \(-6\), stored \(-6\) | no |
| \((-1)+1\) | \(1111+0001=0000\) | 1 | 1 | \(0\) | no |
| \(7+1\) | \(0111+0001=1000\) | 0 | 1 | \(8\) stored as \(-8\) | yes |

\(C_{out}=1\) is not signed overflow. In the second row the carry out is 1 and the signed result is correct. In the first row the carry out is 0 and the signed result is wrong.

**Ones’ complement addition.** Add, then if there is a carry out, add 1 to the LSB. \(0101+1101 = 10010\). End-around turns that into \(0010 + 1? \) The five-bit sum \(10010\) means carry 1 and bits \(0010\). Adding the carry back gives \(0011\). Check: \(5 + (-2) = 3\), and \(1101\) is the ones’ complement of \(0010\), which is \(-2\). Result \(0011 = 3\).

---

## 4. Subtraction, shifts, sign extension

**Subtract \(B\) from \(A\)** in two’s complement by adding the two’s complement of \(B\). One circuit does add and subtract; the subtract path inverts \(B\) and sets the carry into the LSB.

**Logical left shift** by \(k\) multiplies an unsigned value by \(2^k\), until bits fall off the top.

**Arithmetic right shift** copies the sign into the vacated MSB. It divides a two’s-complement value by \(2^k\) and rounds toward \(-\infty\) (the discarded bits are the remainder, and the sign fill makes \(-1 \gg 1\) stay \(-1\), namely \(1111 \to 1111\)).

**Arithmetic left shift** multiplies by \(2^k\) when the signed result still fits. If a bit shifted into the sign differs from the old sign, the product overflowed. The 2010 stem asks for the two’s-complement pattern of \(8P\) given \(P\). That is an arithmetic left shift by 3, and the question is whether you keep \(n\) bits or report the shifted field the stem defines. Do the shift on the given hex; do not convert to decimal and back unless you keep every bit the stem keeps.

**Sign extension** copies the MSB into every new high bit. It preserves the two’s-complement value. It does not preserve an unsigned value, and it is not “insert zeros.” The 5-bit pattern \(10110\) is \(-2^4 + 4 + 2 = -10\). Extended to 8 bits it is \(11110110\), still \(-10\). Zero-fill would produce \(00010110 = +22\).

---

## 5. A binary point that is not at the LSB

The 2018 stem uses eight bits \(b_7 b_6 b_5 b_4 b_3 . b_2 b_1 b_0\), unsigned, \(b_7\) the MSB. The point is between \(b_3\) and \(b_2\), so three bits are fractional.

\[
\text{value} = \sum_{i=0}^{7} b_i \, 2^{i-3}.
\]

Equivalently, read all eight bits as an integer \(N\) and divide by \(2^3 = 8\).

**Why.** Moving the point three places left divides the integer reading by 8. A 1 at \(b_2\) is worth \(2^{-1}\), a 1 at \(b_0\) is worth \(2^{-3}\), a 1 at \(b_3\) is worth \(2^0\).

**Example.** \(00101.100\) is integer \(N = 0101100_2 = 44\), value \(44/8 = 5.5\). Bitwise: \(4+1+0.5 = 5.5\).

This is not a floating-point number. The point does not move, and there is no exponent field.

---

## 6. Booth multiplication

Booth multiplies two’s-complement integers by scanning the multiplier from the LSB. Append an imaginary bit \(Q_{-1} = 0\). At bit position \(i\), look at the pair \((Q_i, Q_{i-1})\):

| \(Q_i\) | \(Q_{i-1}\) | Action before the arithmetic shift |
|--------:|------------:|-------------------------------------|
| 0 | 0 | none |
| 0 | 1 | add the multiplicand \(M\) |
| 1 | 0 | subtract \(M\) |
| 1 | 1 | none |

Then arithmetic-shift the partial product and \(Q\) one place to the right, including the sign. Repeat once per multiplier bit.

**Why it works.** A run of 1s from bit \(a\) through bit \(b-1\) equals \(2^b - 2^a\). Booth subtracts at the top of the run (the \(10\) transition, reading toward the MSB) and adds at the bottom (the \(01\) transition). Isolated 1s are a run of length 1: one subtract and one add, which is the ordinary \(2^{i+1} - 2^i = 2^i\). The algorithm never needs a separate sign fix, because the final shift is arithmetic and the MSB transition is included.

**How many additions and subtractions.** Each \(01\) is one addition. Each \(10\) is one subtraction. \(00\) and \(11\) are free. The count is the number of positions where \(Q_i \neq Q_{i-1}\), including \(Q_{-1}=0\). It depends on the multiplier, not on the multiplicand.

**Example.** Multiplier \(0110\), so bits from the LSB with the extra 0 are pairs \((0,0), (1,0), (1,1), (0,1)\) if the bits are \(q_3 q_2 q_1 q_0 = 0110\) and we examine \(i=0,1,2,3\):

| \(i\) | \(Q_i\) | \(Q_{i-1}\) | Action |
|------:|--------:|------------:|--------|
| 0 | 0 | 0 | none |
| 1 | 1 | 0 | subtract |
| 2 | 1 | 1 | none |
| 3 | 0 | 1 | add |

Two arithmetic operations. A string of identical bits costs none, except that a leading 1 next to the appended story still counts: \(1000\) with \(Q_{-1}=0\) has a single \(10\) at the LSB and a \(10\)? \(q=1000\), pairs \((0,0),(0,0),(0,0),(1,0)\): one subtraction. Value \(-8\) times \(M\) in 4-bit two’s complement, and Booth’s one subtraction of \(M\) placed at that weight, followed by shifts, produces \(-8M\).

The 2025 stem gives two 16-bit vectors and asks for the total number of addition and subtraction operations. Scan the multiplier only. Do not scan the multiplicand. Do not count the shifts.

---

## 7. Solving procedure

1. Name the code before converting. The same bits change value when the code changes.
2. For a decimal to two’s complement: if the number is negative, encode the magnitude, flip, add 1, and keep \(n\) bits.
3. For a pattern to decimal in two’s complement: if the MSB is 0, convert unsigned. If it is 1, either use the negative weight or flip-and-add-1 and attach a minus sign.
4. For overflow, compare the two signs with the result sign, or compare the carry into the sign with the carry out. Do not use \(C_{out}\) alone.
5. For \(kP\) when \(k\) is a power of two, shift. Check that the signed result still fits if the register width is fixed.
6. For Booth, write \(Q_{-1}=0\) and mark every \(01\) and \(10\).
7. For a printed binary point, convert by dividing the integer reading by \(2^{f}\), where \(f\) is the number of fractional bits.

---

## 8. Traps

| Trap | Correction |
|------|------------|
| Most negative 8-bit value \(-127\) | Two’s complement goes to \(-128\) |
| Two zeros in two’s complement | Only ones’ complement and sign-magnitude have two zeros |
| \(C_{out}=1\) means signed overflow | Overflow is carry-in-sign \(\neq\) carry-out-sign |
| Negating \(1000\) yields \(+8\) | In 4 bits it yields \(1000\), still \(-8\) |
| Sign extension inserts 0s | It copies the sign bit |
| Logical right shift of a negative value | That is not division. Arithmetic shift fills with the sign |
| Booth scans both operands | Only the multiplier, plus the extra 0, decides add versus subtract |
| End-around carry in two’s complement | End-around is ones’ complement. Two’s complement keeps the carry out as the unsigned-overflow bit and does not add it back |
| \(X-Y\) for the two 16-bit codes | \(2^{16} - (2^{16}-1) = 1\), not 0 and not 2 |

---

## 9. Connections

- **Combinational adders.** The full adder’s \(C_{out}\) is the unsigned carry. Signed overflow needs one extra XOR of the carry into the sign and the carry out of the sign.
- **Sequential counters.** A binary up counter’s state is an unsigned integer, or a two’s-complement integer, depending on the question. Wrap from \(1111\) to \(0000\) is overflow if the bits were signed and the counter was not saturating.
- **Floating point.** The fraction field of an IEEE number is fixed-point in the sense that its point is just after the hidden 1. The exponent then moves that point. The integer codes on this page do not have an exponent.
