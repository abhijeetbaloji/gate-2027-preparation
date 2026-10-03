# GATE PYQs

## 2026

### Q.18

**Paper:** GATE 2026 CS-2 (afternoon)

**Question:**

Consider the following two statements about interrupt handling mechanisms in a
CPU.
S1: In non-vectored interrupt mechanism, it usually takes more time to start the
Interrupt Service Routine (ISR) when compared to that in a vectored interrupt
mechanism.
S2: In daisy-chain interrupt mechanism, the CPU polls all the input devices
individually to determine the source of the interrupt.
Which one of the following options is correct with respect to S1 and S2 ?

**Options:**

A. Both S1 and S2 are true
B. Both S1 and S2 are false
C. S1 is true and S2 is false
D. S1 is false and S2 is true

**Type:** MCQ

**Answer:** VERIFICATION REQUIRED

**Source:** GATE 2026 CS-2 (afternoon), `12-PYQ/2026/set-02/question-paper.pdf`

---

## 2024

### Q.40

**Paper:** GATE 2024 CS1

**Question:**

Consider the following two threads T1 and T2 that update two shared variables
a and b. Assume that initially a = b = 1. Though context switching between
threads can happen at any time, each statement of T1 or T2 is executed atomically
without interruption.
T1  T2
a = a + 1;  b = 2 * b;
b = b + 1;  a = 2 * a;
Which one of the following options lists all the possible combinations of values of
a and b after both T1 and T2 finish execution?

**Options:**

A. (a = 4, b = 4); (a = 3, b = 3); (a = 4, b = 3)
B. (a = 3, b = 4); (a = 4, b = 3); (a = 3, b = 3)
C. (a = 4, b = 4); (a = 4, b = 3); (a = 3, b = 4)
D. (a = 2, b = 2); (a = 2, b = 3); (a = 3, b = 4)

**Type:** MCQ

**Answer:** VERIFICATION REQUIRED

**Source:** GATE 2024 CS1, `12-PYQ/2024/set-01/question-paper.pdf`

---

### Q.25

**Paper:** GATE 2024 CS2

**Question:**

Consider a process P running on a CPU. Which one or more of the following events
will always trigger a context switch by the OS that results in process P moving to a
non-running state (e.g., ready, blocked)?

**Options:**

A. P makes a blocking system call to read a block of data from the disk
B. P tries to access a page that is in the swap space, triggering a page fault
C. An interrupt is raised by the disk to deliver data requested by some other process
D. A timer interrupt is raised by the hardware

**Type:** MSQ

**Answer:** VERIFICATION REQUIRED

**Source:** GATE 2024 CS2, `12-PYQ/2024/set-02/question-paper.pdf`

---

## 2023

### Q.34

**Paper:** GATE 2023 CS

**Question:**

A keyboard connected to a computer is used at a rate of 1 keystroke per second.
The computer system polls the keyboard every 10 ms (milli seconds) to check for
a keystroke and consumes 100 μs (micro seconds) for each poll. If it is determined
after polling that a key has been pressed, the system consumes an additional 200
μs to process the keystroke. Let T_{1} denote the fraction of a second spent in polling
and processing a keystroke.
In an alternative implementation, the system uses interrupts instead of polling.
An interrupt is raised for every keystroke. It takes a total of 1 ms for servicing an
interrupt and processing a keystroke. Let T_{2} denote the fraction of a second spent
in servicing the interrupt and processing a keystroke.
The ratio T_{1} is  . (Rounded offto one decimal place)
T_{2}

**Options:**

The paper does not print options for this numerical-answer question.

**Type:** NAT

**Answer:** VERIFICATION REQUIRED

**Source:** GATE 2023 CS, `12-PYQ/2023/question-paper.pdf`

---

## 2018

### Q.9

**Paper:** GATE 2018 CS

**Question:**

The following are some events that occur after a device controller issues an interrupt while
process L is under execution.
(P) The processor pushes the process status of L onto the control stack.
(Q) The processor finishes the execution of the current instruction.
(R) The processor executes the interrupt service routine.
(S) The processor pops the process status of L from the control stack.
(T) The processor loads the new PC value based on the interrupt.
Which one of the following is the correct order in which the events above occur?

**Options:**

A. QPTRS
B. PTRSQ
C. TRPQS
D. QTPRS

**Type:** MCQ

**Answer:** VERIFICATION REQUIRED

**Source:** GATE 2018 CS, `12-PYQ/2018/question-paper.pdf`

---

## 2013

### Q.28

**Paper:** GATE 2013 CS Booklet A

**Question:**

Consider the following sequence of micro-operations.
MBR ← PC
MAR ← X
PC ← Y
Memory ← MBR
Which one of the following is a possible operation performed by this sequence?

**Options:**

A. Instruction fetch
B. Operand fetch
C. Conditional branch
D. Initiation of interrupt service

**Type:** MCQ

**Answer:** VERIFICATION REQUIRED

**Source:** GATE 2013 CS Booklet A, `12-PYQ/2013/set-01/question-paper.pdf`

---

### Q.45

**Paper:** GATE 2013 CS Booklet B

**Question:**

Consider the following sequence of micro-operations.
MBR ← PC
MAR ← X
PC ← Y
Memory ← MBR
Which one of the following is a possible operation performed by this sequence?

**Options:**

A. Instruction fetch
B. Operand fetch
C. Conditional branch
D. Initiation of interrupt service

**Type:** MCQ

**Answer:** VERIFICATION REQUIRED

**Source:** GATE 2013 CS Booklet B, `12-PYQ/2013/set-02/question-paper.pdf`

---

### Q.34

**Paper:** GATE 2013 CS Booklet C

**Question:**

Consider the following sequence of micro-operations.
MBR ← PC
MAR ← X
PC ← Y
Memory ← MBR
Which one of the following is a possible operation performed by this sequence?

**Options:**

A. Instruction fetch
B. Operand fetch
C. Conditional branch
D. Initiation of interrupt service

**Type:** MCQ

**Answer:** VERIFICATION REQUIRED

**Source:** GATE 2013 CS Booklet C, `12-PYQ/2013/set-03/question-paper.pdf`

---

### Q.39

**Paper:** GATE 2013 CS Booklet D

**Question:**

Consider the following sequence of micro-operations.
MBR ← PC
MAR ← X
PC ← Y
Memory ← MBR
Which one of the following is a possible operation performed by this sequence?

**Options:**

A. Instruction fetch
B. Operand fetch
C. Conditional branch
D. Initiation of interrupt service

**Type:** MCQ

**Answer:** VERIFICATION REQUIRED

**Source:** GATE 2013 CS Booklet D, `12-PYQ/2013/set-04/question-paper.pdf`

---

## 2011

### Q.11

**Paper:** GATE 2011 CS Booklet A

**Question:**

A computer handles several interrupt sources of which the following are relevant for this question.
• Interrupt from CPU temperature sensor (raises interrupt if CPU temperature is too high)
• Interrupt from Mouse (raises interrupt if the mouse is moved or a button is pressed)
• Interrupt from Keyboard (raises interrupt when a key is pressed or released)
• Interrupt from Hard Disk (raises interrupt when a disk read is completed)
Which one of these will be handled at the HIGHEST priority?

**Options:**

A. Interrupt from Hard Disk
B. Interrupt from Mouse
C. Interrupt from Keyboard
D. Interrupt from CPU temperature sensor CS-A 3/20 2011 CS

**Type:** MCQ

**Answer:** VERIFICATION REQUIRED

**Source:** GATE 2011 CS Booklet A, `12-PYQ/2011/question-paper.pdf`

---

## 2009

### Q.8

**Paper:** GATE 2009 CS

**Question:**

A CPU generally handles an interrupt by executing an interrupt service routine

**Options:**

A. as soon as an interrupt is raised.
B. by checking the interrupt register at the end of fetch cycle.
C. by checking the interrupt register after finishing the execution of the current instruction.
D. by checking the interrupt register at fixed time intervals.

**Type:** MCQ

**Answer:** VERIFICATION REQUIRED

**Source:** GATE 2009 CS, `12-PYQ/2009/question-paper.pdf`

---

## 2008

### Q.64

**Paper:** GATE 2008 CS

**Question:**

Which of the following statements about synchronous and asynchronous 1/O is NOT true?

**Options:**

A. An ISR is invoked on completion of 1/O in synchronous I/O but not in asynchronous I/O
B. In both synchronous and asynchronous 1/0, an ISR (Interrupt Service Routine) is invoked after completion of the I/O
C. A process making a synchronous I/O call waits until I/O is complete, but a process making an asynchronous I/O call does not wait for completion of the I/O
D. In the case of synchronous l/O, the process waiting for the completion of 1/0 is woken up by the ISR that is invoked after the completion of I/O

**Type:** MCQ

**Answer:** VERIFICATION REQUIRED

**Source:** GATE 2008 CS, `12-PYQ/2008/question-paper.pdf`

---

## 2007

### Q.73

**Paper:** GATE 2007 CS

**Question:**

Assume that the memory is byte addressable and the word size is 32 bits. If an
interrupt occurs during the execution of the instruction "INC R3", what return address
will be pushed on to the stack?

**Options:**

A. 1005
B. 1020
C. 1024
D. 1040 CS - 18/24 Common Data for Questions 74, 75: Consider the following Finite State Automaton:

**Type:** MCQ

**Answer:** VERIFICATION REQUIRED

**Source:** GATE 2007 CS, `12-PYQ/2007/question-paper.pdf`

---
