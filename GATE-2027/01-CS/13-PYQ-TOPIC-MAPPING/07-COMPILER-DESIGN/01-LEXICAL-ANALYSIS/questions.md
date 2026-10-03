# GATE PYQs

## 2026

### Q.27

**Paper:** GATE 2026 CS-1 (forenoon)

**Question:**

Consider the following C statements:
char *str1 = "Hello;  /* Statement S1 */
char *str2 = "Hello;";  /* Statement S2 */
int *str3 = "Hello";  /* Statement S3 */
Which of the following options is/are correct?

**Options:**

A. S1 and S2 have syntactic errors
B. S2 has a lexical error and S3 has a syntactic error
C. S1 has a lexical error and S3 has a semantic error
D. S1 has a syntactic error and S3 has a semantic error

**Type:** MCQ

**Answer:** VERIFICATION REQUIRED

**Source:** GATE 2026 CS-1 (forenoon), `12-PYQ/2026/set-01/question-paper.pdf`

---

### Q.35

**Paper:** GATE 2026 CS-2 (afternoon)

**Question:**

A lexical analyzer uses the following token definitions
•  𝑙𝑒𝑡𝑡𝑒𝑟→[𝐴−𝑍𝑎−𝑧]
•  𝑑𝑖𝑔𝑖𝑡→[0 −9]
•  𝑖𝑑→𝑙𝑒𝑡𝑡𝑒𝑟 (𝑙𝑒𝑡𝑡𝑒𝑟 | 𝑑𝑖𝑔𝑖𝑡)*
•  𝑛𝑢𝑚𝑏𝑒𝑟→𝑑𝑖𝑔𝑖𝑡^{+}
•  𝑤𝑠→(𝑏𝑙𝑎𝑛𝑘 | 𝑡𝑎𝑏 | 𝑛𝑒𝑤𝑙𝑖𝑛𝑒)^{+}
For the string given below,
𝑥1  23𝑚𝑚  78  𝑦  7𝑧  𝑧𝑧5  14𝐴  8𝐻  𝐴𝑎𝑌𝑐𝐷
the number of tokens (excluding 𝑤𝑠) that will be produced by the lexical analyzer
is __________. (answer in integer)

**Options:**

The paper does not print options for this numerical-answer question.

**Type:** NAT

**Answer:** VERIFICATION REQUIRED

**Source:** GATE 2026 CS-2 (afternoon), `12-PYQ/2026/set-02/question-paper.pdf`

---

## 2018

### Q.37

**Paper:** GATE 2018 CS

**Question:**

A lexical analyzer uses the following patterns to recognize three tokens T_{1}, T_{2}, and T_{3} over
the alphabet {a,b,c}.
𝑇_{1}:  𝑎? (𝑏|𝑐)^{∗}𝑎
𝑇_{2}:  𝑏? (𝑎|𝑐)^{∗}𝑏
𝑇_{3}:  𝑐? (𝑏|𝑎)^{∗}𝑐
Note that ‘x?’ means 0 or 1 occurrence of the symbol x. Note also that the analyzer outputs
the token that matches the longest possible prefix.
If the string  𝑏𝑏𝑎𝑎𝑐𝑎𝑏𝑐 is processed by the analyzer, which one of the following is the
sequence of tokens it outputs?

**Options:**

A. 𝑇_{1}𝑇_{2}𝑇_{3}
B. 𝑇_{1}𝑇_{1}𝑇_{3}
C. 𝑇_{2}𝑇_{1}𝑇_{3}
D. 𝑇_{3}𝑇_{3}

**Type:** MCQ

**Answer:** VERIFICATION REQUIRED

**Source:** GATE 2018 CS, `12-PYQ/2018/question-paper.pdf`

---

## 2017

### Q.5

**Paper:** GATE 2017 CS Session 2

**Question:**

Correct: 1 Wrong:-0.33
Match the following according to input (from the left column) to the compiler phase (in the right
column) that processes it:
(P) Syntax tree (1) Code generator
(Q) Character stream (ii) Syntax analyzer
(R) Intermediate representation (iii) Semantic analyzer
(S) Token stream (iv) Lexical analyzer

**Options:**

A. P → (i1), Q → (111), R → (iv), S → (i)
B. P → (ii), Q → (i), R → (iii), S → (iv)
C. P → (111), Q → (iv), R → (1), S → (ii)
D. P → (i). Q → (iv), R → (ii), S → (iii)

**Type:** MCQ

**Answer:** VERIFICATION REQUIRED

**Source:** GATE 2017 CS Session 2, `12-PYQ/2017/set-02/question-paper.pdf`

---

## 2016

### Q.54

**Paper:** GATE 2016 CS-1

**Question:**

.
For a host machine that uses the token bucket algorithm for congestion control, the token
bucket has a capacity of 1 megabyte and the maximum output rate is 20 megabytes per second.
Tokens arrive at a rate to sustain output at a rate of 10 megabytes per second. The token bucket
is currently full and the machine needs to send 12 megabytes of data. The minimum time
required to transmit the data is  seconds.

**Options:**

The paper does not print options for this numerical-answer question.

**Type:** NAT

**Answer:** VERIFICATION REQUIRED

**Source:** GATE 2016 CS-1, `12-PYQ/2016/set-01/question-paper.pdf`

---

## 2014

### Q.26

**Paper:** GATE 2014 CS SET-1

**Question:**

Consider a token ring network with a length of 2 km having 10 stations including a monitoring
station. The propagation speed of the signal is  2 × 10_{଼}  m/s and the token transmission time is
ignored. If each station is allowed to hold the token for 2 µsec, the minimum time for which the
monitoring station should wait (in µsec)before assuming that the token is lost is _______.

**Options:**

The paper does not print options for this numerical-answer question.

**Type:** NAT

**Answer:** VERIFICATION REQUIRED

**Source:** GATE 2014 CS SET-1, `12-PYQ/2014/set-01/question-paper.pdf`

---

### Q.25

**Paper:** GATE 2014 CS SET-2

**Question:**

In tthe diagram shown beloww, L1 is an EEthernet LAN and L2 is a Token-Rinng LAN.  An IP packet
origginates fromm sender S annd traverses to R, as shoown.  The linnks within eeach ISP andd across the
twoo ISPs, are  all point-to--point opticaal links.  Thhe initial vaalue of the TTTL field is 32.  The
maxximum possiible value off the TTL fieeld when R reeceives the ddatagram is ______________.

**Options:**

The paper does not print options for this numerical-answer question.

**Type:** NAT

**Answer:** VERIFICATION REQUIRED

**Source:** GATE 2014 CS SET-2, `12-PYQ/2014/set-02/question-paper.pdf`

---

## 2008

### Q.58

**Paper:** GATE 2008 CS

**Question:**

A computer on a 10Mbps network is regulated by a token bucket. The token bucket is filled at a
rate of 2Mbps. It is initially filled to capacity with 16 Megabits. What is the maximum duration for
which the computer can transmit at the full 10Mbps?

**Options:**

A. 1.6 seconds
B. 2 seconds
C. 5 seconds
D. 8 seconds

**Type:** MCQ

**Answer:** VERIFICATION REQUIRED

**Source:** GATE 2008 CS, `12-PYQ/2008/question-paper.pdf`

---

## 2007

### Q.66

**Paper:** GATE 2007 CS

**Question:**

In a token ring network the transmission speed is 10' bps and the propagation speed is
200 metres/us. The 1-bit delay in this network is equivalent to:

**Options:**

A. 500 metres of cable.
B. 200 metres of cable.
C. 20 metres of cable.
D. 50 metres of cable.

**Type:** MCQ

**Answer:** VERIFICATION REQUIRED

**Source:** GATE 2007 CS, `12-PYQ/2007/question-paper.pdf`

---
