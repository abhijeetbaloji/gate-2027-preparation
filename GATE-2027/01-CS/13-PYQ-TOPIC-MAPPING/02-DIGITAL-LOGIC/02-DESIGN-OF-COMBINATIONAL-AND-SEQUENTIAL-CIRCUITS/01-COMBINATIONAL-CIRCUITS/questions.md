# GATE PYQs

## 2026

### Q.59

**Paper:** GATE 2026 CS-2 (afternoon)

**Question:**

Consider the digital circuit shown below with two input lines A and B, two select
lines S0 and S1, and an output line Y. The blocks Q and M represent active high
2:4 decoder and 4-to-1 multiplexer, respectively. Out of 16 possible input
combinations, the number of combinations that produce Y=1 is ____________.
(answer in integer)
Note: One input combination is an instance of [A B S1 S0].

**Options:**

The paper does not print options for this numerical-answer question.

**Type:** NAT

**Answer:** VERIFICATION REQUIRED

**Source:** GATE 2026 CS-2 (afternoon), `12-PYQ/2026/set-02/question-paper.pdf`

---

## 2024

### Q.64

**Paper:** GATE 2024 CS1

**Question:**

Consider a digital logic circuit consisting of three 2-to-1 multiplexers M1, M2, and
M3 as shown below. X1 and X2 are inputs of M1. X3 and X4 are inputs of M2.
A, B, and C are select lines of M1, M2, and M3, respectively.
X1  0
Q1
X2  1 M1
S1
0
A  Y
M3
1
S3
X3  0
C
Q2
M2
X4  1
S2
B
For an instance of inputs  X1=1, X2=1, X3=0, and  X4=0, the number of
combinations of A, B, C that give the output Y=1 is _________

**Options:**

The paper does not print options for this numerical-answer question.

**Type:** NAT

**Answer:** VERIFICATION REQUIRED

**Source:** GATE 2024 CS1, `12-PYQ/2024/set-01/question-paper.pdf`

---

## 2023

### Q.42

**Paper:** GATE 2023 CS

**Question:**

A 4 kilobyte (KB) byte-addressable memory is realized using four 1 KB memory
blocks. Two input address lines (IA4 and IA3) are connected to the chip select
(CS) port of these memory blocks through a decoder as shown in the figure. The
remaining ten input address lines from IA11–IA0 are connected to the address
port of these blocks. The chip select (CS) is active high.
IA11 MSB
IA10
IA9
IA8  10-bit
IA7
IA6  1KB memory  1KB memory  1KB memory  1KB memory
IA5
IA2
IA1
IA0 LSB
Addr  Addr  Addr  Addr
Decoder  X1 CS  X2 CS  X3 CS  X4 CS
Q0
IA4  A1 Q1
IA3  A0 Q2
Q3
The input memory addresses (IA11–IA0), in decimal, for the starting locations
(Addr=0) of each block (indicated as X1, X2, X3, X4 in the figure) are among the
options given below. Which one of the following options is CORRECT?

**Options:**

A. (0, 1, 2, 3)
B. (0, 1024, 2048, 3072)
C. (0, 8, 16, 24)
D. (0, 0, 0, 0)

**Type:** MCQ

**Answer:** VERIFICATION REQUIRED

**Source:** GATE 2023 CS, `12-PYQ/2023/question-paper.pdf`

---

### Q.44

**Paper:** GATE 2023 CS

**Question:**

A Boolean digital circuit is composed using two 4-input multiplexers (M1 and M2)
and one 2-input multiplexer (M3) as shown in the figure. X0–X7 are the inputs of
the multiplexers M1 and M2 and could be connected to either 0 or 1. The select
lines of the multiplexers are connected to Boolean variables A, B and C as shown.
Multiplexer
X0  0
M1
X1  1
Q
X2  2
Multiplexer
X3  3 S1 S0  0
A  M3
C  Q
Multiplexer
X4  0  1 S
X5  1 M2
Q
X6  2
X7  3 S1 S0
A
C
B
Which one of the following set of values of (X0, X1, X2, X3, X4, X5, X6, X7) will
realise the Boolean function A + A.C + A.B.C?

**Options:**

A. (1, 1, 0, 0, 1, 1, 1, 0)
B. (1, 1, 0, 0, 1, 1, 0, 1)
C. (1, 1, 0, 1, 1, 1, 0, 0)
D. (0, 0, 1, 1, 0, 1, 1, 1)

**Type:** MCQ

**Answer:** VERIFICATION REQUIRED

**Source:** GATE 2023 CS, `12-PYQ/2023/question-paper.pdf`

---

## 2022

### Q.40

**Paper:** GATE 2022 CS

**Question:**

Consider a digital display system (DDS) shown in the figure that displays the
contents of register X. A 16-bit code word is used to load a word in X, either from
S or from R. S is a 1024-word memory segment and R is a 32-word register file.
Based on the value of mode bit M, T selects an input word to load in X. P and Q
interface with the corresponding bits in the code word to choose the addressed word.
Which one of the following represents the functionality of P, Q, and T?
Code Word
M  S-address  R-address
P  Q
S  R
T
X  DDS

**Options:**

A. P is 10:1 multiplexer; Q is 5:1 multiplexer; T is 2:1 multiplexer
B. P is 10:2^{10} decoder; Q is 5:2^{5} decoder; T is 2:1 encoder
C. P is 10:2^{10} decoder; Q is 5:2^{5} decoder; T is 2:1 multiplexer
D. P is 1:10 de-multiplexer; Q is 1:5 de-multiplexer; T is 2:1 multiplexer

**Type:** MCQ

**Answer:** VERIFICATION REQUIRED

**Source:** GATE 2022 CS, `12-PYQ/2022/question-paper.pdf`

---

## 2020

### Q.19

**Paper:** GATE 2020 CS

**Question:**

A multiplexer is placed between a group of 32 registers and an accumulator to
regulate data movement such that at any given point in time the content of only
one register will move to the accumulator. The minimum number of select lines
needed for the multiplexer is

**Options:**

The paper does not print options for this numerical-answer question.

**Type:** NAT

**Answer:** VERIFICATION REQUIRED

**Source:** GATE 2020 CS, `12-PYQ/2020/question-paper.pdf`

---

### Q.20

**Paper:** GATE 2020 CS

**Question:**

If there are m input lines and n output lines for a decoder that is used to uniquely
address a byte addressable 1 KB RAM, then the minimum value of m + n is

**Options:**

The paper does not print options for this numerical-answer question.

**Type:** NAT

**Answer:** VERIFICATION REQUIRED

**Source:** GATE 2020 CS, `12-PYQ/2020/question-paper.pdf`

---

## 2016

### Q.30

**Paper:** GATE 2016 CS-1

**Question:**

Consider the two cascaded 2-to-1 multiplexers as shown in the figure.
R
0  0  2−to−1  0  2−to−1  X
R  1  MUX  1  MUX
s  s
P  Q
The minimal sum of products form of the output X is

**Options:**

A. P¯ Q¯ + PQR
B. PQ¯ + QR
C. PQ + P¯ QR¯
D. Q¯ R¯ + PQR

**Type:** MCQ

**Answer:** VERIFICATION REQUIRED

**Source:** GATE 2016 CS-1, `12-PYQ/2016/set-01/question-paper.pdf`

---

## 2015

### Q.65

**Paper:** GATE 2015 CS, 7 February Shift 2

**Question:**

A half adder is implemented with XOR and AND gates. A full adder is implemented with two half
adders and one OR gate. The propagation delay of an XOR gate is twice that of an AND/OR gate.
The propagation delay of an AND/OR gate 1s 1.2 mucroseconds. A 4-bit mpple-carry binary adder 1s
implemented by using four full adders. The total propagation time of this 4-bit binary adder in
microseconds is
Correct Answer:
19.2

**Options:**

The paper does not print options for this numerical-answer question.

**Type:** NAT

**Answer:** VERIFICATION REQUIRED

**Source:** GATE 2015 CS, 7 February Shift 2, `12-PYQ/2015/set-02/question-paper.pdf`

---

## 2014

### Q.45

**Paper:** GATE 2014 CS SET-1

**Question:**

Conssider the 4-to--1 multiplexer with two select lines ܵ_{ଵ} aand ܵ_{଴} given bbelow.
The mminimal sum-of-products form of the BBoolean expreession for the output F of thhe multiplexeer is

**Options:**

A. PQ + QR + PÕR
B. PQ + PQŘ + PQR + PÕR
C. PQR + PQR + QR + PQR
D. ത

**Type:** MCQ

**Answer:** VERIFICATION REQUIRED

**Source:** GATE 2014 CS SET-1, `12-PYQ/2014/set-01/question-paper.pdf`

---

### Q.44

**Paper:** GATE 2014 CS SET-2

**Question:**

If the associativity of a processor cache is doubled while keeping the capacity and block size
unchanged, which one of the following is guaranteed to be NOT affected?

**Options:**

A. Width of tag comparator
B. Width of set index decoder
C. Width of way selection multiplexor
D. Width of processor to main memory data bus

**Type:** MCQ

**Answer:** VERIFICATION REQUIRED

**Source:** GATE 2014 CS SET-2, `12-PYQ/2014/set-02/question-paper.pdf`

---

## 2013

### Q.5

**Paper:** GATE 2013 CS Booklet A

**Question:**

In the following truth table, V = 1 if and only if the input is valid.
Inputs  Outputs
D_{0} D_{1} D_{2} D_{3} X_{0} X_{1} V
0  0  0  0  x  x  0
1  0  0  0  0  0  1
x  1  0  0  0  1  1
x x 1 0 1 0 1
x  x  x  1  1  1  1
What function does the truth table represent?

**Options:**

A. Priority encoder
B. Decoder
C. Multiplexer
D. Demultiplexer

**Type:** MCQ

**Answer:** VERIFICATION REQUIRED

**Source:** GATE 2013 CS Booklet A, `12-PYQ/2013/set-01/question-paper.pdf`

---

### Q.46

**Paper:** GATE 2013 CS Booklet A

**Question:**

A RAM chip has a capacity of 1024 words of 8 bits each (1K × 8). The number of 2 × 4 decoders
with enable line needed to construct a 16K × 16 RAM from 1K × 8 RAM is

**Options:**

A. 4
B. 5
C. 6
D. 7

**Type:** MCQ

**Answer:** VERIFICATION REQUIRED

**Source:** GATE 2013 CS Booklet A, `12-PYQ/2013/set-01/question-paper.pdf`

---

### Q.21

**Paper:** GATE 2013 CS Booklet B

**Question:**

In the following truth table, V = 1 if and only if the input is valid.
Inputs  Outputs
D_{0} D_{1} D_{2} D_{3} X_{0} X_{1} V
0  0  0  0  x  x  0
1 0 0 0 0 0 1
x  1  0  0  0  1  1
x  x  1  0  1  0  1
x x x 1 1 1 1
What function does the truth table represent?

**Options:**

A. Priority encoder
B. Decoder
C. Multiplexer
D. Demultiplexer

**Type:** MCQ

**Answer:** VERIFICATION REQUIRED

**Source:** GATE 2013 CS Booklet B, `12-PYQ/2013/set-02/question-paper.pdf`

---

### Q.27

**Paper:** GATE 2013 CS Booklet B

**Question:**

A RAM chip has a capacity of 1024 words of 8 bits each (1K × 8). The number of 2 × 4 decoders
with enable line needed to construct a 16K × 16 RAM from 1K × 8 RAM is

**Options:**

A. 4
B. 5
C. 6
D. 7

**Type:** MCQ

**Answer:** VERIFICATION REQUIRED

**Source:** GATE 2013 CS Booklet B, `12-PYQ/2013/set-02/question-paper.pdf`

---

### Q.8

**Paper:** GATE 2013 CS Booklet C

**Question:**

In the following truth table, V = 1 if and only if the input is valid.
Inputs  Outputs
D_{0} D_{1} D_{2} D_{3} X_{0} X_{1} V
0  0  0  0  x  x  0
1  0  0  0  0  0  1
x  1  0  0  0  1  1
x  x  1  0  1  0  1
x  x  x  1  1  1  1
What function does the truth table represent?

**Options:**

A. Priority encoder
B. Decoder
C. Multiplexer
D. Demultiplexer

**Type:** MCQ

**Answer:** VERIFICATION REQUIRED

**Source:** GATE 2013 CS Booklet C, `12-PYQ/2013/set-03/question-paper.pdf`

---

### Q.38

**Paper:** GATE 2013 CS Booklet C

**Question:**

A RAM chip has a capacity of 1024 words of 8 bits each (1K × 8). The number of 2 × 4 decoders
with enable line needed to construct a 16K × 16 RAM from 1K × 8 RAM is

**Options:**

A. 4
B. 5
C. 6
D. 7 CS- C 8/20 2013COMPUTER SCIENCE & INFORMATION TECH. - CS

**Type:** MCQ

**Answer:** VERIFICATION REQUIRED

**Source:** GATE 2013 CS Booklet C, `12-PYQ/2013/set-03/question-paper.pdf`

---

### Q.18

**Paper:** GATE 2013 CS Booklet D

**Question:**

In the following truth table, V = 1 if and only if the input is valid.
Inputs  Outputs
D_{0} D_{1} D_{2} D_{3} X_{0} X_{1} V
0  0  0  0  x  x  0
1  0  0  0  0  0  1
x 1 0 0 0 1 1
x  x  1  0  1  0  1
x  x  x  1  1  1  1
What function does the truth table represent?

**Options:**

A. Priority encoder
B. Decoder
C. Multiplexer
D. Demultiplexer

**Type:** MCQ

**Answer:** VERIFICATION REQUIRED

**Source:** GATE 2013 CS Booklet D, `12-PYQ/2013/set-04/question-paper.pdf`

---

### Q.35

**Paper:** GATE 2013 CS Booklet D

**Question:**

A RAM chip has a capacity of 1024 words of 8 bits each (1K × 8). The number of 2 × 4 decoders
with enable line needed to construct a 16K × 16 RAM from 1K × 8 RAM is

**Options:**

A. 4
B. 5
C. 6
D. 7

**Type:** MCQ

**Answer:** VERIFICATION REQUIRED

**Source:** GATE 2013 CS Booklet D, `12-PYQ/2013/set-04/question-paper.pdf`

---

## 2011

### Q.46

**Paper:** GATE 2011 CS Booklet A

**Question:**

Database table by name Loan_Records is given below.
Borrower Bank_Manager Loan_Amount
Ramesh Sunderajan 10000.00
Suresh Ramgopal 5000.00
Mahesh Sunderajan 7000.00
What is the output of the following SQL query?
SELECT count(*)
FROM (
(SELECT Borrower, Bank_Manager FROM Loan_Records) AS S
NATURAL JOIN
(SELECT Bank_Manager, Loan_Amount FROM Loan_Records) AS T
);

**Options:**

A. 3
B. 9
C. 5
D. 6 CS-A 12/20 2011 CS

**Type:** MCQ

**Answer:** VERIFICATION REQUIRED

**Source:** GATE 2011 CS Booklet A, `12-PYQ/2011/question-paper.pdf`

---

## 2007

### Q.8

**Paper:** GATE 2007 CS

**Question:**

How many 3-to-8 line decoders with an enable input are needed to construct a 6-to-64
line decoder without using any other logic gates?

**Options:**

A. 7
B. 8
C. 9
D. 10

**Type:** MCQ

**Answer:** VERIFICATION REQUIRED

**Source:** GATE 2007 CS, `12-PYQ/2007/question-paper.pdf`

---
