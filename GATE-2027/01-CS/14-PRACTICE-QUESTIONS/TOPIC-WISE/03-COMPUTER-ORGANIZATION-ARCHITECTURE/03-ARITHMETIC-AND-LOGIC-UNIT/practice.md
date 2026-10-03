# Arithmetic and Logic Unit — Practice Questions

Original practice for GATE CS. These questions are not from any GATE paper. Attempt the questions before reading the solutions.

## Level 1 — Conceptual

## Q1 — MCQ

A full adder has inputs \(A\), \(B\), and \(C_{in}\). Which expression is its sum bit?

A. \(AB + C_{in}\)  
B. \(A \oplus B \oplus C_{in}\)  
C. \(A + B + C_{in}\)  
D. \(\overline{A \oplus B \oplus C_{in}}\)

---

## Q2 — MCQ

The zero flag is set when

A. the result is zero  
B. the result is negative  
C. the carry out of the MSB is 1  
D. signed overflow occurs

---

## Q3 — NAT

A ripple-carry adder adds two 8-bit numbers and is built only from full adders, one per bit. How many full adders does it contain?

---

## Level 2 — Standard GATE Style

## Q4 — MCQ

An 8-bit two’s-complement ALU adds \(0\text{x7F}\) and \(0\text{x01}\). The flags are sign \(S\), zero \(Z\), carry-out \(C\), and overflow \(V\). Overflow is carry-into-MSB XOR carry-out-of-MSB. Which flags equal 1?

A. only \(Z\)  
B. only \(S\) and \(V\)  
C. \(S\), \(Z\), and \(C\)  
D. only \(C\)

---

## Q5 — NAT

Each full adder produces its carry in 2 gate delays and its sum in 3 gate delays. One gate delay is 1 ns. In a 16-bit ripple-carry adder, the carry ripples through the first 15 adders and the MSB sum is then formed. What is the worst-case delay, in nanoseconds?

---

## Q6 — MSQ

Select all that apply to integer addition flags.

A. Adding two positive two’s-complement numbers and obtaining a negative result means signed overflow.  
B. Adding two negative two’s-complement numbers and obtaining a non-negative result means signed overflow.  
C. Carry-out of the MSB always means signed overflow.  
D. Signed overflow occurs when the carry into the MSB differs from the carry out of the MSB.

---

## Q7 — MCQ

An ALU operation is selected by a 4-bit control field. How many distinct operations can that field select?

A. 4  
B. 8  
C. 15  
D. 16

---

## Level 3 — Multi-Step

## Q8 — NAT

An 8-bit ALU subtracts by adding the two’s complement. It computes \(5 - 13\). The stored carry flag is the raw carry out of that addition, not an inverted borrow. What is the unsigned integer value of the 8-bit result?

---

## Q9 — MCQ

\(A = 1100_2\) and \(B = 1010_2\). The 4-bit result of \(A\) XOR \(B\) is

A. \(1000_2\)  
B. \(1110_2\)  
C. \(0110_2\)  
D. \(0010_2\)

---

## Q10 — NAT

An 8-bit two’s-complement ALU adds the signed values 100 and 50. Interpret the 8-bit result as a signed integer. The result is ______.

---

## Level 4 — Tricky / Trap-Based

## Q11 — NAT

A sequential shift-and-add multiplier multiplies two 16-bit unsigned numbers. Each of the 16 iterations adds, taking 5 ns, and then shifts, taking 2 ns. Those steps are in series. A combinational array multiplier produces the same product in 40 ns. How many nanoseconds slower is the sequential multiplier?

---

## Q12 — MSQ

An 8-bit ALU adds \(0\text{xFF}\) and \(0\text{x01}\). \(S\) is the MSB of the stored result, \(Z\) is the zero flag, \(C\) is the carry out, and \(V\) is carry-into-MSB XOR carry-out. Select all that apply.

A. \(Z = 1\)  
B. \(C = 1\)  
C. \(V = 1\)  
D. \(S = 0\)

---

## Level 5 — Challenge

## Q13 — NAT

A 32-bit adder is built from eight 4-bit carry-lookahead sections and a second-level lookahead.

- Section propagate and generate are ready 5 ns after the operands.
- The second-level lookahead produces every section carry-in 10 ns after those section propagate and generate signals.
- Once a section has its carry-in, it produces all four sum bits 12 ns later.
- The adder’s own carry-in is available at time 0, but every section carry used on the critical path comes from the second-level lookahead.

What is the worst-case delay until every sum bit is ready, in nanoseconds?

---

## Q14 — MCQ

A 64-bit ALU supports addition, subtraction, AND, OR, XOR, and set-on-less-than. After a subtraction performed by adding the two’s complement, \(C = 1\) means an unsigned borrow, \(S\) is the result sign, and \(V\) is signed overflow. Which comparison is correct?

A. Unsigned less-than uses only \(Z\), and signed less-than uses only \(S\).  
B. Unsigned less-than uses \(V\), and signed less-than uses \(C\).  
C. Signed less-than uses \(S \oplus V\), and unsigned less-than uses \(C\).  
D. Both comparisons use only the zero flag.

## Answer Key

| Q | Type | Answer |
|---|------|--------|
| 1 | MCQ | B |
| 2 | MCQ | A |
| 3 | NAT | 8 |
| 4 | MCQ | B |
| 5 | NAT | 33 |
| 6 | MSQ | A, B, D |
| 7 | MCQ | D |
| 8 | NAT | 248 |
| 9 | MCQ | C |
| 10 | NAT | -106 |
| 11 | NAT | 72 |
| 12 | MSQ | A, B, D |
| 13 | NAT | 27 |
| 14 | MCQ | C |

## Detailed Solutions

### Q1

Answer: B

A full adder sums three bits. The sum is 1 when an odd number of inputs are 1, which is \(A \oplus B \oplus C_{in}\). The carry is the majority function, not the sum.

### Q2

Answer: A

The zero flag tests whether every result bit is 0. Sign, carry, and overflow are separate flags.

### Q3

Answer: 8

Each of the 8 bits has its own full adder. The least significant carry-in is 0 for a plain addition, but that adder is still a full adder.

### Q4

Answer: B

\[
0\text{x7F} + 0\text{x01} = 0\text{x80} = 10000000_2
\]

The MSB is 1, so \(S = 1\). The result is not zero, so \(Z = 0\). There is no carry out of bit 7, so \(C = 0\). The lower 7 bits are \(1111111 + 0000001\), which generates a carry into the MSB, so

\[
V = 1 \oplus 0 = 1
\]

Signed interpretation: \(127 + 1\) should be 128, which is not representable in 8-bit two’s complement. The stored bit pattern is \(-128\). Only \(S\) and \(V\) are 1.

### Q5

Answer: 33

Fifteen carry steps reach the MSB, and that adder then forms its sum.

\[
15 \times 2 + 3 = 33 \text{ ns}
\]

### Q6

Answer: A, B, D

Signed overflow is detected from the sign of the result when the operands have the same sign, and equivalently from \(C_{in,MSB} \oplus C_{out}\). Carry-out by itself is the unsigned overflow indication. Two’s-complement overflow can occur with \(C = 0\), as in Q4, so C is false.

### Q7

Answer: D

A 4-bit field has \(2^4 = 16\) encodings.

### Q8

Answer: 248

The two’s complement of 13 is

\[
(\sim 00001101_2) + 1 = 11110011_2
\]

\[
\begin{align*}
&\ 00000101 \\
+&\ 11110011 \\
=&\ 11111000
\end{align*}
\]

There is no carry out. The bit pattern \(11111000_2\) equals \(128 + 64 + 32 + 16 + 8 = 248\) as an unsigned integer. As a signed value it is \(248 - 256 = -8\), and \(5 - 13 = -8\), so \(V = 0\).

### Q9

Answer: C

XOR is 1 only where the bits differ.

\[
\begin{align*}
A &= 1100 \\
B &= 1010 \\
A \oplus B &= 0110
\end{align*}
\]

AND would be \(1000_2\) and OR would be \(1110_2\).

### Q10

Answer: -106

\[
\begin{align*}
100 &= 01100100_2 \\
50 &= 00110010_2 \\
\text{sum} &= 10010110_2 = 150
\end{align*}
\]

The pattern \(10010110_2\) has MSB 1. Its signed value is

\[
150 - 256 = -106
\]

The lower bits generate a carry into the MSB and there is no carry out, so \(V = 1\). That matches the sign error: \(100 + 50 = 150\) is outside the signed range \(-128\) to \(127\).

### Q11

Answer: 72

One sequential iteration takes \(5 + 2 = 7\) ns, and there are 16 iterations.

\[
16 \times 7 = 112 \text{ ns}
\]

\[
112 - 40 = 72 \text{ ns}
\]

### Q12

Answer: A, B, D

\[
0\text{xFF} + 0\text{x01} = 1\,00000000_2
\]

The stored 8 bits are \(00000000_2\), so \(S = 0\) and \(Z = 1\). The ninth bit makes \(C = 1\). The carry into the MSB is also 1, so

\[
V = 1 \oplus 1 = 0
\]

Signed check: \(-1 + 1 = 0\), which fits. Unsigned check: \(255 + 1 = 256\), which does not fit in 8 bits. C is the false statement.

### Q13

Answer: 27

Section propagate and generate signals are ready at 5 ns. The second-level unit then takes 10 ns, so every section carry-in is ready at

\[
5 + 10 = 15 \text{ ns}
\]

The slowest sums need another 12 ns.

\[
15 + 12 = 27 \text{ ns}
\]

Section 0 can start from the external carry-in at time 0 and finishes earlier. The critical path is a later section waiting for the second-level carry.

### Q14

Answer: C

For two’s-complement subtraction, signed \(A < B\) is true when the result is negative for a reason other than overflow, which is \(S \oplus V\). With the problem’s convention that \(C = 1\) means unsigned borrow, unsigned \(A < B\) is exactly \(C = 1\). The zero flag distinguishes equality. It does not by itself distinguish the direction of an inequality.
