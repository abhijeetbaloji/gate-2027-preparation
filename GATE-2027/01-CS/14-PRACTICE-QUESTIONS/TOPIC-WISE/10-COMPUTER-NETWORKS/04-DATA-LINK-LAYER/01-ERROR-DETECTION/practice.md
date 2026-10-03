# Error Detection — Practice Questions

Original practice for GATE CS. These questions are not from any GATE paper. Attempt the questions before reading the solutions.

## Level 1 — Conceptual

## Q1 — MCQ

Even parity adds one bit so that the total number of 1s in the protected block, including the parity bit, is

A. even
B. odd
C. equal to the block length
D. equal to 1

---

## Q2 — MSQ

Select all that apply. A single even-parity bit over a block can

A. detect every error that flips an odd number of bits in the block
B. detect every error that flips exactly two bits in the block
C. detect a single-bit error
D. correct every two-bit error by itself, with no extra parity bits

---

## Q3 — NAT

The data bits are 1011001. One even-parity bit is appended. Enter that parity bit as the integer 0 or 1.

---

## Level 2 — Standard GATE Style

## Q4 — MCQ

A block uses even parity on each row and each column, including a parity bit on the parity column. One data bit is flipped in transit. The received row-parity and column-parity checks

A. fail only for the row and the column that contain the flipped bit, so their intersection locates it
B. all succeed, because two-dimensional parity ignores single-bit errors
C. fail for every row and every column
D. can detect the error but can never point at a single row

---

## Q5 — MCQ

A CRC generator polynomial has degree 4. The number of CRC bits appended to the data is

A. 2
B. 4
C. 8
D. 16

---

## Q6 — MSQ

Select all that apply. A CRC whose generator has degree \(r\), and at least two nonzero terms, can

A. detect every single-bit error
B. detect every burst error of length at most \(r\)
C. detect every possible error pattern of any length
D. be checked by dividing the received bit string by the same generator and expecting remainder 0

---

## Q7 — NAT

Data bits 10011101 are protected by the CRC generator 1011. The remainder that is appended is a 3-bit string. Enter that remainder as an integer (interpret the 3 bits as a binary number).

---

## Level 3 — Multi-Step

## Q8 — MCQ

Two 16-bit words, 0x4A3B and 0xB165, are covered by an Internet checksum: add them with end-around carry in 16 bits, then take the one’s complement. The checksum is

A. 0x045F
B. 0xFBA0
C. 0x0460
D. 0x04A3

---

## Q9 — MSQ

Select all that apply. Which statements about the Internet checksum are correct?

A. The addition uses one’s-complement end-around carry, not a throw-away carry.
B. The transmitted check field is the one’s complement of that sum.
C. A receiver that adds the data words and the checksum, with the same end-around carry, gets all 1s when there is no error.
D. The checksum is a CRC remainder for the generator \(x^{16}+x^{12}+x^5+1\).

---

## Q10 — NAT

Using the same words 0x4A3B and 0xB165 and the same Internet checksum, enter the checksum as a decimal integer.

---

## Level 4 — Tricky / Trap-Based

## Q11 — MCQ

The data 10011101 and generator 1011 produce CRC remainder 011, so the transmitted string is 10011101011. A student instead transmits 10011101000, leaving the three appended zeros in place. The receiver divides by 1011. What happens?

A. The remainder is 0, so the receiver accepts the string.
B. The remainder is not 0, so the receiver reports an error.
C. The receiver cannot run a CRC check unless the generator has degree 16.
D. The check passes because the data bits themselves are unchanged.

---

## Q12 — MSQ

Select all that apply. Which claims about error detection are true?

A. Even parity detects a two-bit error.
B. A CRC of degree \(r\) is guaranteed to detect every burst of length \(r+5\).
C. Flipping the single parity bit of an even-parity block is detected.
D. If a CRC generator divides the received string with a nonzero remainder, the receiver reports that an error was detected.

---

## Level 5 — Challenge

## Q13 — MCQ

Data bits are arranged as two rows of three bits, with even parity on every row and every column.

Row 1 data: 1 0 1. Row 2 data: 1 1 0.

The sender computes the parity bits. In transit, the only change is that row 1, column 2 flips from 0 to 1. The receiver’s failing checks identify which data bit?

A. Row 1, column 2
B. Row 2, column 2
C. Row 1, column 1
D. No row fails, so the error is invisible

---

## Q14 — MCQ

The Internet checksum of 0xABCD, 0x1234, and 0xEF01 is computed with 16-bit one’s-complement addition and a final complement. Which value is that checksum?

A. 0x52FC
B. 0xAD03
C. 0x52FD
D. 0xBE01

---

## Answer Key

| Q | Type | Answer |
|---|------|--------|
| 1 | MCQ | A |
| 2 | MSQ | A, C |
| 3 | NAT | 0 |
| 4 | MCQ | A |
| 5 | MCQ | B |
| 6 | MSQ | A, B, D |
| 7 | NAT | 3 |
| 8 | MCQ | A |
| 9 | MSQ | A, B, C |
| 10 | NAT | 1119 |
| 11 | MCQ | B |
| 12 | MSQ | C, D |
| 13 | MCQ | A |
| 14 | MCQ | A |

## Detailed Solutions

### Q1

Answer: A

Even parity makes the number of 1s even. Odd parity makes it odd. The parity bit is not required to equal the block length or to be the only 1 in the block.

### Q2

Answer: A, C

One parity bit is a parity check on the whole block. Any odd number of flips, including one flip, changes the parity and is detected. Exactly two flips preserve even parity, so B is not detected. A single parity bit has no way to point at which bits flipped, so it does not correct a two-bit error. D is false.

### Q3

Answer: 0

1011001 contains four 1s, which is already even. The even-parity bit is 0. Appending 1 would make five 1s and would be the odd-parity choice.

### Q4

Answer: A

A single flipped data bit ruins exactly one row parity and exactly one column parity. The failing row and failing column cross at the damaged bit. B is wrong because the checks do fail. C would describe a much larger corruption. D denies the column check, which is what gives the position along the row.

### Q5

Answer: B

The number of CRC bits equals the degree of the generator. Degree 4 means four check bits. The other options are unrelated powers of two.

### Q6

Answer: A, B, D

A generator with two or more terms does not divide \(x^i\), so every single-bit error is detected. Every burst of length at most \(r\) is also detected for a degree-\(r\) generator. The receiver appends nothing further: it divides the received string, including the CRC field, and a valid string produces remainder 0. C is false. Some long error patterns are exact multiples of the generator and are invisible to that CRC.

### Q7

Answer: 3

Append three zeros: 10011101000. Divide by 1011 using XOR.

- 10011101000 XOR 1011 shifted to bit 0 gives 00101101000.
- The next 1 is at bit 2. XOR 1011 there gives 00000001000.
- The next 1 is at bit 7. XOR 1011 there gives 00000000011.

The remainder is 011 binary, which is the integer 3. The transmitted string is 10011101011. Dividing that string by 1011 leaves remainder 000.

### Q8

Answer: A

\[
\texttt{0x4A3B} + \texttt{0xB165} = \texttt{0xFBA0}
\]

The sum fits in 16 bits, so there is no end-around carry. The one’s complement flips every bit:

\[
\texttt{0xFFFF} - \texttt{0xFBA0} = \texttt{0x045F}
\]

B is the sum before the complement. C is that complement plus one, which would be a two’s-complement step. D is a fragment of the first word.

### Q9

Answer: A, B, C

Internet checksum arithmetic folds the carry back into the low bits, and the field stored in the packet is the complement of the folded sum. Adding that complement back in produces 0xFFFF when the words are intact. For these two words, \(\texttt{0xFBA0} + \texttt{0x045F} = \texttt{0xFFFF}\). D names the CRC-16-CCITT generator. The Internet checksum is not that CRC.

### Q10

Answer: 1119

From the previous addition, the checksum is 0x045F.

\[
\texttt{0x045F} = 4 \times 256 + 5 \times 16 + 15 = 1024 + 80 + 15 = 1119
\]

Sending the uncomplemented sum 0xFBA0 would be the decimal value 64416, which is not the checksum field.

### Q11

Answer: B

The zeros were only a placeholder so the division had room for a degree-3 remainder. The value that makes the whole string divisible by 1011 is 011, not 000. Dividing 10011101000 by 1011 leaves remainder 011, which is not 0, so the check fails. C invents a degree requirement. D is the trap: unchanged data bits are not enough if the check field is the wrong three bits.

### Q12

Answer: C, D

A two-bit flip keeps even parity, so A is false. A degree-\(r\) CRC is guaranteed for bursts of length up to \(r\), not up to \(r+5\), so B is false. Flipping only the parity bit changes the count of 1s and is detected. A nonzero CRC remainder is exactly the receiver’s error signal, so D is true.

### Q13

Answer: A

Even parity bits at the sender:

- Row 1 data 1 0 1 has two 1s, so the row parity bit is 0.
- Row 2 data 1 1 0 has two 1s, so the row parity bit is 0.
- Column parities of the data columns are 0, 1, and 1. The parity column’s parity bit is 0.

After row 1, column 2 flips, row 1 data is 1 1 1. Its parity bit is still 0, so row 1 fails. Column 2 is now 1 and 1, with parity bit 1, so that column fails. Row 2 still checks, and columns 1 and 3 still check. The unique failing row and failing column meet at row 1, column 2. The error is not invisible, and it does not point at row 2 or at column 1.

### Q14

Answer: A

\[
\texttt{0xABCD} + \texttt{0x1234} = \texttt{0xBE01}
\]

\[
\texttt{0xBE01} + \texttt{0xEF01} = \texttt{0x1AD02}
\]

End-around carry: \(\texttt{0xAD02} + 1 = \texttt{0xAD03}\).

\[
\texttt{0xFFFF} - \texttt{0xAD03} = \texttt{0x52FC}
\]

B is the folded sum before complementing. C is one larger than the checksum. D is the sum of only the first two words. Check: \(\texttt{0xAD03} + \texttt{0x52FC} = \texttt{0xFFFF}\).
