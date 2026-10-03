# GATE PYQs

## 2026

### Q.37

**Paper:** GATE 2026 CS-1 (forenoon)

**Question:**

Consider a 2-bit saturating up/down counter that performs the saturating up count
when the input P is 0, and the saturating down count when P is 1. The Next State
table of the counter is as shown. The counter is built as a synchronous sequential
circuit using D flip-flops.
Input  Current  Next
State  State
𝑃  𝑄_{1}  𝑄_{0}  𝑄_{1}+  𝑄_{0}+
0  0  0  0  1
0  0  1  1  0
0  1  0  1  1
0  1  1  1  1
1  0  0  0  0
1  0  1  0  0
1  1  0  0  1
1  1  1  1  0
Which one of the following options corresponds to the expressions for the inputs of
the D flip-flops, 𝐷_{1} and 𝐷_{0}?

**Options:**

A. 𝐷_{1} = 𝑃 𝑄_{1} + 𝑃̅𝑄_{0} + 𝑄_{1}𝑄_{0}𝐷_{0} = 𝑃 𝑄_{0} + 𝑃̅ 𝑄_{1} + 𝑄_{1}𝑄_{0}̅̅̅
B. 𝐷_{1} = 𝑃̅ 𝑄_{1} + 𝑃̅𝑄_{0} + 𝑄_{1}𝑄_{0}𝐷_{0} = 𝑃̅ 𝑄_{0}̅̅̅ + 𝑃 ̅𝑄_{1} + 𝑄_{1}𝑄_{0}̅̅̅
C. 𝐷_{1} = 𝑃̅ 𝑄_{1}̅̅̅ + 𝑃 ̅𝑄_{0} + 𝑄_{1}𝑄_{0}𝐷_{0} = 𝑃̅ 𝑄_{0} + 𝑃̅ 𝑄_{1} + 𝑄_{1}𝑄_{0}̅̅̅
D. 𝐷_{1} = 𝑃 𝑄_{1}̅̅̅ + 𝑃̅ 𝑄_{0} + 𝑄_{1} 𝑄_{0}𝐷_{0} = 𝑃 𝑄_{0}̅̅̅ + 𝑃̅ 𝑄_{1} + 𝑄_{1}𝑄_{0}̅̅̅

**Type:** MCQ

**Answer:** VERIFICATION REQUIRED

**Source:** GATE 2026 CS-1 (forenoon), `12-PYQ/2026/set-01/question-paper.pdf`

---

### Q.60

**Paper:** GATE 2026 CS-1 (forenoon)

**Question:**

The EX stage of a pipelined processor performs the memory read operations for
LOAD instructions, and the operations for the arithmetic and logic instructions. Let
𝑡_{𝐸𝑋} denote the time taken by the EX stage to perform the operation for an instruction.
For each instruction type, the values of  𝑡_{𝐸𝑋} and M (the number of instructions of that
type in a sequence of 100 instructions for a program P), are given in the table below.
The duration of the pipeline clock cycle is 1 nanosecond. Assume that the latch time
for the interstage buffers in the pipeline is negligible.
Instruction  𝑡_{𝐸𝑋} in  𝑀
nanoseconds
LOAD  1.8  15
IMUL  1.5  10
IDIV  2.5  5
FADD  1.7  10
FSUB  1.7  5
FMUL  2.8  15
FDIV  3.2  5
All other  Less than  35
instructions  1.0
When program P is executed, the number of clock cycles for which the pipeline is
stalled due to structural hazards in the EX stage is ______. (answer in integer)

**Options:**

The paper does not print options for this numerical-answer question.

**Type:** NAT

**Answer:** VERIFICATION REQUIRED

**Source:** GATE 2026 CS-1 (forenoon), `12-PYQ/2026/set-01/question-paper.pdf`

---

### Q.57

**Paper:** GATE 2026 CS-2 (afternoon)

**Question:**

A non-pipelined instruction execution unit that operates at 1.6 GHz clock takes an
average of 5 clock cycles to complete the execution of an instruction. To improve
the performance, the system was pipelined with a goal of achieving an average
throughput of one instruction per clock cycle. However, it could operate only at
1.2 GHz due to pipeline overheads. While executing a program in the pipelined
design, 30% of instructions encountered a stall of 2 cycles due to pipeline hazards.
The speed-up obtained by the pipelined design over the non-pipelined one for this
program is ___________. (rounded off to two decimal places)
Note: 1G=10^{9}

**Options:**

The paper does not print options for this numerical-answer question.

**Type:** NAT

**Answer:** VERIFICATION REQUIRED

**Source:** GATE 2026 CS-2 (afternoon), `12-PYQ/2026/set-02/question-paper.pdf`

---

## 2025

### Q.11

**Paper:** GATE 2025 CS-1

**Question:**

Suppose a program is running on a non-pipelined single processor computer system.
The computer is connected to an external device that can interrupt the processor
asynchronously. The processor needs to execute the interrupt service routine (ISR)
to serve this interrupt. The following steps (not necessarily in order) are taken by
the processor when the interrupt arrives:
(i)  The processor saves the content of the program counter.
(ii)  The program counter is loaded with the start address of the ISR.
(iii)  The processor finishes the present instruction.
Which ONE of the following is the CORRECT sequence of steps?

**Options:**

A. (iii), (i), (ii)
B. (i), (iii), (ii)
C. (i), (ii), (iii)
D. (iii), (ii), (i)

**Type:** MCQ

**Answer:** VERIFICATION REQUIRED

**Source:** GATE 2025 CS-1, `12-PYQ/2025/set-01/question-paper.pdf`

---

### Q.60

**Paper:** GATE 2025 CS-1

**Question:**

Consider the given sequential circuit designed using D-Flip-flops. The circuit is
initialized with some value (initial state). The number of distinct states the circuit
will go through before returning back to the initial state is _________ .  (Answer
in integer)

**Options:**

The paper does not print options for this numerical-answer question.

**Type:** NAT

**Answer:** VERIFICATION REQUIRED

**Source:** GATE 2025 CS-1, `12-PYQ/2025/set-01/question-paper.pdf`

---

### Q.34

**Paper:** GATE 2025 CS-2

**Question:**

In a 4-bit ripple counter, if the period of the waveform at the last flip-flop is 64
microseconds, then the frequency of the ripple counter in kHz is ________. (Answer
in integer)

**Options:**

The paper does not print options for this numerical-answer question.

**Type:** NAT

**Answer:** VERIFICATION REQUIRED

**Source:** GATE 2025 CS-2, `12-PYQ/2025/set-02/question-paper.pdf`

---

### Q.55

**Paper:** GATE 2025 CS-2

**Question:**

Given a computing system with two levels of cache (L1 and L2) and a main
memory. The first level (L1) cache access time is 1 nanosecond (ns) and the “hit
rate” for L1 cache is 90% while the processor is accessing the data from L1 cache.
Whereas, for the second level (L2) cache, the “hit rate” is 80% and the “miss
penalty” for transferring data from L2 cache to L1 cache is 10 ns. The “miss
penalty” for the data to be transferred from main memory to L2 cache is 100 ns.
Then the average memory access time in this system in nanoseconds is
___________ . (rounded off to one decimal place)
A 5-stage instruction pipeline has stage delays of 180, 250, 150, 170, and 250,
respectively, in nanoseconds. The delay of an inter-stage latch is 10 nanoseconds.

**Options:**

The paper does not print options for this numerical-answer question.

**Type:** NAT

**Answer:** VERIFICATION REQUIRED

**Source:** GATE 2025 CS-2, `12-PYQ/2025/set-02/question-paper.pdf`

---

## 2023

### Q.20

**Paper:** GATE 2023 CS

**Question:**

An algorithm has to store several keys generated by an adversary in a hash
table. The adversary is malicious who tries to maximize the number of collisions.
Let k be the number of keys, m be the number of slots in the hash table, and k > m.
Which one of the following is the best hashing strategy to counteract the adversary?

**Options:**

A. Division method, i.e., use the hash function h(k) = k mod m.
B. Multiplication method, i.e., use the hash function h(k) = ⌊m(kA −⌊kA⌋)⌋, where A is a carefully chosen constant.
C. Universal hashing method.
D. If k is a prime number, use Division method. Otherwise, use Multiplication method.

**Type:** MCQ

**Answer:** VERIFICATION REQUIRED

**Source:** GATE 2023 CS, `12-PYQ/2023/question-paper.pdf`

---

### Q.21

**Paper:** GATE 2023 CS

**Question:**

The output of a 2-input multiplexer is connected back to one of its inputs as shown
in the figure.
Multiplexer
0
Q
1
S
Match the functional equivalence of this circuit to one of the following options.

**Options:**

A. D Flip-flop
B. D Latch
C. Half-adder
D. Demultiplexer

**Type:** MCQ

**Answer:** VERIFICATION REQUIRED

**Source:** GATE 2023 CS, `12-PYQ/2023/question-paper.pdf`

---

### Q.22

**Paper:** GATE 2023 CS

**Question:**

Which one or more of the following need to be saved on a context switch from one
thread (T1) of a process to another thread (T2) of the same process?

**Options:**

A. Page table base register
B. Stack pointer
C. Program counter
D. General purpose registers

**Type:** MSQ

**Answer:** VERIFICATION REQUIRED

**Source:** GATE 2023 CS, `12-PYQ/2023/question-paper.pdf`

---

### Q.43

**Paper:** GATE 2023 CS

**Question:**

Consider a sequential digital circuit consisting of T flip-flops and D flip-flops as
shown in the figure. CLKIN is the clock input to the circuit. At the beginning,
Q1, Q2 and Q3 have values 0, 1 and 1, respectively.
T  D  T
Q  Q  Q
Q1  Q2  Q3
CLKIN
CLK  CLK  CLK
Which one of the given values of (Q1, Q2, Q3) can NEVER be obtained with this
digital circuit?

**Options:**

A. (0, 0, 1)
B. (1, 0, 0)
C. (1, 0, 1)
D. (1, 1, 1)

**Type:** MCQ

**Answer:** VERIFICATION REQUIRED

**Source:** GATE 2023 CS, `12-PYQ/2023/question-paper.pdf`

---

## 2021

### Q.28

**Paper:** GATE 2021 CS Set-1

**Question:**

Consider a 3-bit counter, designed using T flip-flops, as shown below:
Tр Q R
Clock
Pulse
P' Q'
Assuming the initial state of the counter given by PQR as 000, what are the next
three states?

**Options:**

A. | 011, 101, 000
B. 001, 010, 111
C. 011,101, 111
D. 001, 010, 000

**Type:** MCQ

**Answer:** VERIFICATION REQUIRED

**Source:** GATE 2021 CS Set-1, `12-PYQ/2021/set-01/question-paper.pdf`

---

### Q.46

**Paper:** GATE 2021 CS Set-1

**Question:**

Consider the following pseudocode, where S is a semaphore initialized to 5 in line#2
and counter is a shared variable initialized to 0 in line#1. Assume that the incre-
ment operation in line#7 is not atomic.
1. int counter = 0;
2. Semaphore S = init(5);
3. void parop(void)
4. €
5. wait(S);
6. wait(S);
7. countert+;
8. signal(S);
9. signal (S);
10.}
If five threads execute the function parop concurrently, which of the following
program behavior(s) is/are possible?

**Options:**

A. The value of counter is 5 after all the threads successfully complete the execution of parop
B. The value of counter is 1 after all the threads successfully complete the execution of parop.
C. The value of counter is 0 after all the threads successfully complete the execution of parop.
D. There is a deadlock involving all the threads. GATE Graduate Aptitude Test in Engineering 2021 2021 Organising Institute - IIT Bombay

**Type:** MCQ

**Answer:** VERIFICATION REQUIRED

**Source:** GATE 2021 CS Set-1, `12-PYQ/2021/set-01/question-paper.pdf`

---

### Q.28

**Paper:** GATE 2021 CS Set-2

**Question:**

Suppose we want to design a synchronous circuit that processes a string of 0's
and I's. Given a string, it produces another string by replacing the first 1 in any
subsequence of consecutive 1's by a 0. Consider the following example.
Input sequence: 00100011000011100
Output sequence: 00000001000001100
A Mealy Machine is a state machine where both the next state and the output are
functions of the present state and the current input.
The above mentioned circuit can be designed as a two-state Mealy machine. The
states in the Mealy machine can be represented using Boolean values 0 and 1. We
denote the current state, the next state, the next incoming bit, and the output bit
of the Mealy machine by the variables s, t, b and y respectively.
Assume the initial state of the Mealy machine is 0.
What are the Boolean expressions corresponding to t and y in terms of s and b?

**Options:**

A. t=s+Ъ y = sb
B. t =b y =sb
C. t =b y =sb
D. t=s+b y =sb GATE Graduate Aptitude Test in Engineering 2021 2021 Organising Institute - IIT Bombay

**Type:** MCQ

**Answer:** VERIFICATION REQUIRED

**Source:** GATE 2021 CS Set-2, `12-PYQ/2021/set-02/question-paper.pdf`

---

## 2018

### Q.21

**Paper:** GATE 2018 CS

**Question:**

Consider the following C program:
#include <stdio.h>
int counter = 0;
int calc (int a, int b) {
int c;
counter++;
if (b==3) return (a*a*a);
else {
c = calc(a, b/3);
return (c*c*c);
}
}
int main (){
calc(4, 81);
printf ("%d", counter);
}
The output of this program is _____.

**Options:**

The paper does not print options for this numerical-answer question.

**Type:** NAT

**Answer:** VERIFICATION REQUIRED

**Source:** GATE 2018 CS, `12-PYQ/2018/question-paper.pdf`

---

### Q.22

**Paper:** GATE 2018 CS

**Question:**

Consider the sequential circuit shown in the figure, where both flip-flops used are positive
edge-triggered D flip-flops.
in  out
D  Q  D  Q
clock
The number of states in the state transition diagram of this circuit that have a transition back
to the same state on some value of “in” is _____.

**Options:**

The paper does not print options for this numerical-answer question.

**Type:** NAT

**Answer:** VERIFICATION REQUIRED

**Source:** GATE 2018 CS, `12-PYQ/2018/question-paper.pdf`

---

## 2017

### Q.7

**Paper:** GATE 2017 CS Session 2

**Question:**

Correct : 1 Wrong:-0.33
Which of the following is/are shared by all the threads in a process?
I. Program counter
II. Stack
III. Address space
IV. Registers

**Options:**

A. Iand II only
B. III only
C. IV only
D. III and IV only

**Type:** MCQ

**Answer:** VERIFICATION REQUIRED

**Source:** GATE 2017 CS Session 2, `12-PYQ/2017/set-02/question-paper.pdf`

---

### Q.42

**Paper:** GATE 2017 CS Session 2

**Question:**

Correct: 2 Wrong:-0.66
The next state table of a 2-bit saturating up-counter is given below.
01 lo Qt
0 1
1 0
1 0
1 1 1
The counter is built as a synchronous sequential circuit using T flip-flops. The expressions for T1
and To are

**Options:**

A. T1 = Q1lo, To = Q1l0
B. T1 = 010o, To = Q1 + Q0
C. T1=Q1+Q0To=Q1+Õ
D. T1 = Q1lo, To= lI + lo

**Type:** MCQ

**Answer:** VERIFICATION REQUIRED

**Source:** GATE 2017 CS Session 2, `12-PYQ/2017/set-02/question-paper.pdf`

---

## 2016

### Q.8

**Paper:** GATE 2016 CS-1

**Question:**

We want to design a synchronous counter that counts the sequence 0-1-0-2-0-3 and then
repeats. The minimum number of J-K flip-flops required to implement this counter is

**Options:**

The paper does not print options for this numerical-answer question.

**Type:** NAT

**Answer:** VERIFICATION REQUIRED

**Source:** GATE 2016 CS-1, `12-PYQ/2016/set-01/question-paper.pdf`

---

## 2015

### Q.21

**Paper:** GATE 2015 CS, 7 February Shift 1

**Question:**

Consider a 4-bit Johnson counter with an initial value of 0000. The counting sequence of this
counter is
(А) 0, 1, 3, 7, 15, 14, 12, 8, 0 (B) 0, 1, 3, 5, 7, 9, 11, 13, 15, 0
(С) 0, 2, 4, 6, 8, 10, 12, 14, 0 (D) 0, 8, 12, 14, 15, 7, 3, 1, 0

**Options:**

The options could not be read from the local paper. The PDF listed in Source is the authoritative copy.

**Type:** MCQ

**Answer:** VERIFICATION REQUIRED

**Source:** GATE 2015 CS, 7 February Shift 1, `12-PYQ/2015/set-01/question-paper.pdf`

---

### Q.53

**Paper:** GATE 2015 CS, 7 February Shift 1

**Question:**

12

A positive edge-triggered D flip-flop is connected to a positive edge-triggered JK flip-flop as
follows. The Q output of the D flip-flop is connected to both the J and K inputs of the JK flip-flop,
while the Q output of the JK flip-flop is connected to the input of the D flip-flop. Initially, the
output of the D flip-flop is set to logic one and the output of the JK flip-flop is cleared. Which one
of the following is the bit sequence (including the initial state) generated at the Q output of the JK
flip-flop when the flip-flops are connected to a free-running common clock? Assume that J=K =1
is the toggle mode and J = K = 0 is the state-holding mode of the JK flip-flop. Both the flip-flops
have non-zero propagation delays.

**Options:**

A. 0110110...
B. 0100100...
C. 011101110...
D. 011001100... 2% B 3.% c 4. D

**Type:** MCQ

**Answer:** VERIFICATION REQUIRED

**Source:** GATE 2015 CS, 7 February Shift 1, `12-PYQ/2015/set-01/question-paper.pdf`

---

### Q.17

**Paper:** GATE 2015 CS, 7 February Shift 2

**Question:**

The minimum number of JK flip-flops required to construct a synchronous counter with the count
sequence (0,0,1,1,2,2,3,3,0,0,....) is _
Correct Answer:

**Options:**

The paper does not print options for this numerical-answer question.

**Type:** NAT

**Answer:** VERIFICATION REQUIRED

**Source:** GATE 2015 CS, 7 February Shift 2, `12-PYQ/2015/set-02/question-paper.pdf`

---

### Q.51

**Paper:** GATE 2015 CS, 7 February Shift 2

**Question:**

The secant method is used to find the root of an equation f(x) = 0. It is started from two distinct
estimates Xa and xb for the root. It is an iterative procedure involving linear interpolation to a root.
The iteration stops if f(xb) is very small and then xb 1s the solution. The procedure is given below.
Observe that there is an expression which is missing and is marked by ?. Which is the suitable
expression that is to be put in place of ? so that it follows all steps of the secant method?
Secant
Initialize: Xar Xbr &, N //€ = convergence indicator
// N= maximum no. of iterations
1n=1j)
1 = 0
while (i < Nand Ifbl > €) do
i=i+ 1 // update counter
Xt= ? / missing expression for
/ intermediate value
Xа = Xb // reset xa
Xb = Xt // reset xb
1b=1xb) / function value at new x
end while
if & then / loop is terminated with i=N
write "Non-convergence"
else
write "return xo"
end if

**Options:**

A. xb-(fb-f(xa))fb/(xb-xa)
B. xa - (fa-f (Xa)) fa / (Xb-Xa) )xb-xb-2a) 1b/1b-1xa))
D. Xa- (xb-xa) fa/ (fb-f(xa))

**Type:** MCQ

**Answer:** VERIFICATION REQUIRED

**Source:** GATE 2015 CS, 7 February Shift 2, `12-PYQ/2015/set-02/question-paper.pdf`

---

### Q.54

**Paper:** GATE 2015 CS, 7 February Shift 2

**Question:**

13

Consider a processor with byte-addressable memory. Assume that all registers, including Program
Counter (PC) and Program Status Word (PSW), are of size 2 bytes. A stack in the main memory is
implemented from memory location (0100)16 and it grows upward. The stack pointer (SP) points to
the top element of the stack. The current value of SP is (016E) 16. The CALL instruction is of two
words, the first word is the op-code and the second word is the starting address of the subroutine
(one word = 2 bytes). The CALL instruction is implemented as follows:
• Store the current value of PC in the stack
• Store the value of PSW register in the stack
• Load the starting address of the subroutine in PC
The content of PC just before the fetch of a CALL instruction is (5FAO) 16. After execution of the
CALL instruction, the value of the stack pointer is

**Options:**

A. (016A) 16
B. (016C) 16
C. (0170) 16
D. (0172) 16

**Type:** MCQ

**Answer:** VERIFICATION REQUIRED

**Source:** GATE 2015 CS, 7 February Shift 2, `12-PYQ/2015/set-02/question-paper.pdf`

---

## 2014

### Q.7

**Paper:** GATE 2014 CS SET-2

**Question:**

Let  = 2^{௡}. A circuit is built by giving the output of an  -bit binary counter as input to an
-to-2^{௡} bit decoder. This circuit is equivalent to a

**Options:**

A. ݇ -bit binary up counter.
B. ݇ -bit binary down counter. CS02 (GATE 2014)^{
C. } ݇ -bit ring counter.
D. ݇ -bit Johnson counter.

**Type:** MCQ

**Answer:** VERIFICATION REQUIRED

**Source:** GATE 2014 CS SET-2, `12-PYQ/2014/set-02/question-paper.pdf`

---

### Q.8

**Paper:** GATE 2014 CS SET-3

**Question:**

Consider the following combinational function block involving four Boolean variables x, y, a,
b  where x, a, b  are inputs and y is the output.
f (x, y, a, b)
{
if (x is 1) y = a;
else y = b;
}
Which one of the following digital logic blocks is the most suitable for implementing this function?

**Options:**

A. Full adder
B. Priority encoder
C. Multiplexor
D. Flip-flop

**Type:** MCQ

**Answer:** VERIFICATION REQUIRED

**Source:** GATE 2014 CS SET-3, `12-PYQ/2014/set-03/question-paper.pdf`

---

### Q.45

**Paper:** GATE 2014 CS SET-3

**Question:**

CS03 (GATE 2014)
Thee above syynchronous  sequential  circuit built using JJK flip-flopps is initiaalized with
ଶ ଵ ଴ = 0000. The state seequence for this circuit ffor the next 33 clock cycles  is

**Options:**

A. ) 001, 010, 0011
B. ) 111, 110, 1101
C. ) 100, 110, 1111
D. ) 100, 011, 0001

**Type:** MCQ

**Answer:** VERIFICATION REQUIRED

**Source:** GATE 2014 CS SET-3, `12-PYQ/2014/set-03/question-paper.pdf`

---

## 2011

### Q.51

**Paper:** GATE 2011 CS Booklet A

**Question:**

If all the flip-flops were reset to 0 at power on, what is the total number of distinct outputs (states)
represented by PQR generated by the counter?

**Options:**

A. 3
B. 4
C. 5
D. 6 CS-A 14/20 2011 CS Linked Answer Questions Statement for Linked Answer Questions 52 and 53: Consider a network with five nodes, N1 to N5, as shown below. NS 3 (N2) 4 6 (N4 2 N3 The network uses a Distance Vector Routing protocol. Once the routes have stabilized, the distance vectors at different nodes are as following. N1: (0, 1,7, 8, 4) N2: (1, 0, 6, 7, 3) N3: (7, 6, 0, 2, 6) N4: (8, 7,2, 0, 4) Each distance vector is the distance of the best known path at that instance to nodes, N1 to N5, where the N5: (4,3, 6, 4, 0) nodes to change only that entry in their distance vectors.

**Type:** MCQ

**Answer:** VERIFICATION REQUIRED

**Source:** GATE 2011 CS Booklet A, `12-PYQ/2011/question-paper.pdf`

---

## 2010

### Q.22

**Paper:** GATE 2010 CS

**Question:**

What is the appropriate pairing of ilems in che two columns listing various activities encountered in a software life cycle?
P. Requirements Caplure 1. Module Development and Inlegration
Q.Design 2. Domain Analysis 3. Structural and Behavioral Modeling
R. Impleientation 4. Performance Tuning
S. Maintenance

**Options:**

A. P-3 Q-2 R.t $.1
B. P-2 Q-3R-1$4
C. P-3Q-2R-LS4
D. P-2 Q-3R-4S-1

**Type:** MCQ

**Answer:** VERIFICATION REQUIRED

**Source:** GATE 2010 CS, `12-PYQ/2010/question-paper.pdf`

---

## 2009

### Q.27

**Paper:** GATE 2009 CS

**Question:**

/ Given the following state table of an FSM with two states A and B, one input and one output :
Present State A Present State B Input Next State A Next State B Output
0 0 0 0 1
1 0 0 0
1
0
1 0 1
1 1 0 0 1
If the initial state is A = 0, B = 0, what is the minimum length of an input string which will take
the machine to the state A = 0, B = 1 with Output = 1?

**Options:**

A. 3
B. 4
C. 5
D. 6

**Type:** MCQ

**Answer:** VERIFICATION REQUIRED

**Source:** GATE 2009 CS, `12-PYQ/2009/question-paper.pdf`

---

### Q.47

**Paper:** GATE 2009 CS

**Question:**

2009
While opening a TCP connection, the initial sequence number is to be derived using a time-of-day
(ToD) clock that keeps running even when the host is down. The low order 32 bits of the counter of the
ToD clock is to be used for the initial sequence numbers. The clock counter increments once per
millisecond. The maximum packet lifetime is given to be 64s.
Which one of the choices given below is closest to the minimum permissible rate at which sequence
numbers used for packets of a connection can increase ?

**Options:**

A. 0.015/s
B. 0.064/s
C. 0.135/s
D. 0.327/s

**Type:** MCQ

**Answer:** VERIFICATION REQUIRED

**Source:** GATE 2009 CS, `12-PYQ/2009/question-paper.pdf`

---

## 2007

### Q.34

**Paper:** GATE 2007 CS

**Question:**

Suppose only one multiplexer and one inverter are allowed to be used to implement
any Boolean function of n variables. What is the minimum size of the multiplexer
needed?

**Options:**

A. 6, 3
B. 10,4
C. 6,4
D. 10,5 The control signal functions of a 4-bit binary counter are given below (where X is

**Type:** MCQ

**Answer:** VERIFICATION REQUIRED

**Source:** GATE 2007 CS, `12-PYQ/2007/question-paper.pdf`

---

### Q.36

**Paper:** GATE 2007 CS

**Question:**

"don't care"):
Clear Clock Load Count Function
1 X X Clear to 0
0 X 0 0 No change
0 1 X Load input
0 1 Count next
The counter is connected as follows:
A4 A3 A2 AI
Count=1
Clear 4-bit counter Load=0
Clock
Inputs
Assume that the counter and gate delays are negligible. If the counter starts at 0, then 0 0 1
it cycles through the following sequence:

**Options:**

A. 0, 3,4
B. 0, 3, 4, 5
C. 0, 1, 2, 3, 4
D. 0, 1, 2, 3, 4, 5 CS - 8/24

**Type:** MCQ

**Answer:** VERIFICATION REQUIRED

**Source:** GATE 2007 CS, `12-PYQ/2007/question-paper.pdf`

---
