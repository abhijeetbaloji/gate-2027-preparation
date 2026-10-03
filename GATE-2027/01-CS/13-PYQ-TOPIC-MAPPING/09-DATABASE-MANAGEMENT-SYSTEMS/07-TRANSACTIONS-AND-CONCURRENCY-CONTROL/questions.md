# GATE PYQs

## 2026

### Q.20

**Paper:** GATE 2026 CS-2 (afternoon)

**Question:**

Consider concurrent execution of two transactions 𝑇1 and 𝑇2 in a DBMS, both of
which access a data object 𝐴. For these two transactions to not conflict on 𝐴, which
one of the following statements must be true?

**Options:**

A. Both 𝑇1 and 𝑇2 only read 𝐴
B. 𝑇1 reads 𝐴 and 𝑇2 writes 𝐴
C. 𝑇1 writes 𝐴 and 𝑇2 reads 𝐴
D. Both 𝑇1 and 𝑇2 write 𝐴

**Type:** MCQ

**Answer:** VERIFICATION REQUIRED

**Source:** GATE 2026 CS-2 (afternoon), `12-PYQ/2026/set-02/question-paper.pdf`

---

## 2025

### Q.15

**Paper:** GATE 2025 CS-1

**Question:**

A schedule of three database transactions  𝑇_{1},  𝑇_{2}, and  𝑇_{3} is shown.  𝑅_{𝑖}(𝐴) and
𝑊_{𝑖}(𝐴) denote read and write of data item  𝐴 by transaction  𝑇_{𝑖}, 𝑖= 1,2,3. The
transaction  𝑇_{1} aborts at the end. Which other transaction(s) will be required to be
rolled back?
𝑅_{1}(𝑋)  𝑊_{1}(𝑌)  𝑅_{2}(𝑋)  𝑅_{2}(𝑌)  𝑅_{3}(𝑌) 𝐴𝐵𝑂𝑅𝑇(𝑇_{1})

**Options:**

A. Only 𝑇_{2}
B. Only 𝑇_{3}
C. Both 𝑇_{2} and 𝑇_{3}
D. Neither 𝑇_{2} nor 𝑇_{3}

**Type:** MCQ

**Answer:** VERIFICATION REQUIRED

**Source:** GATE 2025 CS-1, `12-PYQ/2025/set-01/question-paper.pdf`

---

### Q.27

**Paper:** GATE 2025 CS-2

**Question:**

An audit of a banking transactions system has found that on an earlier occasion, two
joint holders of account 𝐴 attempted simultaneous transfers of Rs. 10000 each from
account 𝐴 to account 𝐵.  Both transactions read the same value, Rs. 11000, as the
initial balance in 𝐴 and were allowed to go through. 𝐵 was credited Rs. 10000 twice.
𝐴 was debited only once and ended up with a balance of Rs. 1000.
Which of the following properties is/are certain to have been violated by the
system?

**Options:**

A. Atomicity
B. Consistency
C. Isolation
D. Durability

**Type:** MCQ

**Answer:** VERIFICATION REQUIRED

**Source:** GATE 2025 CS-2, `12-PYQ/2025/set-02/question-paper.pdf`

---

### Q.53

**Paper:** GATE 2025 CS-2

**Question:**

Consider the database transactions T1 and T2, and data items X and Y. Which of
the schedule(s) is/are conflict serializable?
Transaction T1
Transaction T2
R1(X)
W2(X)
W1(Y)
W2(Y)
R1(X)
COMMIT(T2)
W1(X)
COMMIT(T1)

**Options:**

A. R1(X), W2(X), W1(Y), W2(Y), R1(X), W1(X), COMMIT(T2), COMMIT(T1)
B. W2(X), R1(X), W2(Y), W1(Y), R1(X), COMMIT(T2), W1(X), COMMIT(T1)
C. R1(X), W1(Y), W2(X), W2(Y), R1(X), W1(X), COMMIT(T1), COMMIT(T2)
D. W2(X), R1(X), W1(Y), W2(Y), R1(X), COMMIT(T2), W1(X), COMMIT(T1)

**Type:** MCQ

**Answer:** VERIFICATION REQUIRED

**Source:** GATE 2025 CS-2, `12-PYQ/2025/set-02/question-paper.pdf`

---

## 2024

### Q.46

**Paper:** GATE 2024 CS1

**Question:**

Consider the following read-write schedule  𝑆 over three transactions
𝑇_{1}, 𝑇_{2}, and 𝑇_{3}, where the subscripts in the schedule indicate transaction IDs:
𝑆: 𝑟_{1}(𝑧); 𝑤_{1}(𝑧); 𝑟_{2}(𝑥); 𝑟_{3}(𝑦); 𝑤_{3}(𝑦); 𝑟_{2}(𝑦); 𝑤_{2}(𝑥); 𝑤_{2}(𝑦);
Which of the following transaction schedules is/are conflict equivalent to 𝑆 ?

**Options:**

A. 𝑇_{1}𝑇_{2}𝑇_{3}
B. 𝑇_{1}𝑇_{3}𝑇_{2}
C. 𝑇_{3}𝑇_{2}𝑇_{1}
D. 𝑇_{3}𝑇_{1}𝑇_{2}

**Type:** MCQ

**Answer:** VERIFICATION REQUIRED

**Source:** GATE 2024 CS1, `12-PYQ/2024/set-01/question-paper.pdf`

---

### Q.19

**Paper:** GATE 2024 CS2

**Question:**

324
Once the DBMS informs the user that a transaction has been successfully
completed, its effect should persist even if the system crashes before all its changes
are reflected on disk. This property is called

**Options:**

A. durability
B. atomicity
C. consistency
D. isolation

**Type:** MCQ

**Answer:** VERIFICATION REQUIRED

**Source:** GATE 2024 CS2, `12-PYQ/2024/set-02/question-paper.pdf`

---

## 2022

### Q.39

**Paper:** GATE 2022 CS

**Question:**

Let  R_{i} ( z)  and  W_{i} ( z)  denote read and write operations on a data element  z  by a
transaction  T_{i}  , respectively. Consider the schedule S with four transactions.
S:  R_{4} ( x )R_{2} ( x )R_{3} ( x )R_{1} ( y W)_{1} ( y W)_{2} ( x W)_{3} ( y )R_{4} ( y)
Which one of the following serial schedules is conflict equivalent to S?

**Options:**

A. T1 →T3→TA→T2
B. T1→TA→T3→T2
C. T4→T1→T3→T2
D. T3→Tı→TA→T2

**Type:** MCQ

**Answer:** VERIFICATION REQUIRED

**Source:** GATE 2022 CS, `12-PYQ/2022/question-paper.pdf`

---

## 2021

### Q.13

**Paper:** GATE 2021 CS Set-1

**Question:**

Suppose a database system crashes again while recovering from a previous crash.
Assume checkpointing is not done by the database either during the transactions
or during recovery.
Which of the following statements is/are correct?

**Options:**

A. The same undo and redo list will be used while recovering again.
B. The system cannot recover any further.
C. |All the transactions that are already undone and redone will not be recovered again.
D. The database will become inconsistent.

**Type:** MCQ

**Answer:** VERIFICATION REQUIRED

**Source:** GATE 2021 CS Set-1, `12-PYQ/2021/set-01/question-paper.pdf`

---

### Q.32

**Paper:** GATE 2021 CS Set-1

**Question:**

Let r;(z) and w;(z) denote read and write operations respectively on a data item z
by a transaction T;. Consider the following two schedules.
S1: T1(2) rI(У) T2(x) r2(У) W2(Y) W1(X)
S2: r1(2) r2(2) T2(y) W2(Y) TI(Y) W1(2)
Which one of the following options is correct?

**Options:**

A. S, is conflict serializable, and S2 is not conflict serializable.
B. Sı is not conflict serializable, and S2 is conflict serializable.
C. Both S1 and S2 are conflict serializable.
D. Neither S1 nor S2 is conflict serializable.

**Type:** MCQ

**Answer:** VERIFICATION REQUIRED

**Source:** GATE 2021 CS Set-1, `12-PYQ/2021/set-01/question-paper.pdf`

---

### Q.32

**Paper:** GATE 2021 CS Set-2

**Question:**

Let S be the following schedule of operations of three transactions T1, T2 and Tg
in a relational database system:
R(Y), R1(X), R3(Z), R1(Y), Wi(X), R2(Z), W(Y), Rg(X), W3(Z)
Consider the statements P and Q below:
P: S is conflict-serializable.
Q: If T3 commits before T, finishes, then S is recoverable.
Which one of the following choices is correct?

**Options:**

A. Both P and Q are true.
B. P is true and Q is false.
C. P is false and Q is true.
D. Both P and Q are false.

**Type:** MCQ

**Answer:** VERIFICATION REQUIRED

**Source:** GATE 2021 CS Set-2, `12-PYQ/2021/set-02/question-paper.pdf`

---

## 2020

### Q.37

**Paper:** GATE 2020 CS

**Question:**

Consider a schedule of transactions T1 and T2:
RA RC WD WB Commit
RB WB RD WC Commit
Here, RX stands for "Read(X)" and WX stands for "Write(X)". Which one of the
following schedules is conflict equivalent to the above schedule?

**Options:**

A. RA RC WD WB Commit T2 RB WB RD WC Commit
B. RA RC WD WB Commit T2 RB WB RD WC Commit () T1 RA RC WD WB Commit T2 RB WB RD WC Commit
D. T1 RA RC WD WB Commit Tz RB WB RD WC Commit

**Type:** MCQ

**Answer:** VERIFICATION REQUIRED

**Source:** GATE 2020 CS, `12-PYQ/2020/question-paper.pdf`

---

## 2019

### Q.11

**Paper:** GATE 2019 CS (printed header Set-2)

**Question:**

Consider the following two statements about database transaction schedules:
Strict two-phase locking protocol generates conflict serializable schedules that
are also recoverable.
II. Timestamp-ordering concurrency control protocol with Thomas' Write Rule can
generate view serializable schedules that are not conflict serializable.
Which of the above statements is/are TRUE?

**Options:**

A. I only
B. II only
C. Both I and II
D. Neither I nor II

**Type:** MCQ

**Answer:** VERIFICATION REQUIRED

**Source:** GATE 2019 CS (printed header Set-2), `12-PYQ/2019/question-paper.pdf`

---

## 2017

### Q.44

**Paper:** GATE 2017 CS Session 2

**Question:**

Correct: 2 Wrong : 0
Two transactions T1 and T2 are given as
T1:r1(X)W1(X)r1(Y)W1(Y)
12:2w2)2ZW2Z)
where ri(V) denotes a read operation by transaction T; on a variable V and w;(V) denotes a write
operation by transaction T; on a variable V. The total number of conflict serializable schedules that
can be formed by T1 and Tz is

**Options:**

The paper does not print options for this numerical-answer question.

**Type:** NAT

**Answer:** VERIFICATION REQUIRED

**Source:** GATE 2017 CS Session 2, `12-PYQ/2017/set-02/question-paper.pdf`

---

## 2016

### Q.51

**Paper:** GATE 2016 CS-2

**Question:**

Consider the following database schedule with two transactions, T_{1} and T_{2}.
S = r_{2}(X); r_{1}(X); r_{2}(Y ); w_{1}(X); r_{1}(Y ); w_{2}(X); a_{1}; a_{2}
where r_{i}(Z) denotes a read operation by transaction T_{i} on a variable Z, w_{i}(Z) denotes a write
operation by T_{i} on a variable Z and a_{i} denotes an abort by transaction T_{i}.
Which one of the following statements about the above schedule is TRUE?

**Options:**

A. S is non-recoverable
B. S is recoverable, but has a cascading abort
C. S does not have a cascading abort
D. S is strict CS(Set B) 16/18

**Type:** MCQ

**Answer:** VERIFICATION REQUIRED

**Source:** GATE 2016 CS-2, `12-PYQ/2016/set-02/question-paper.pdf`

---

## 2015

### Q.31

**Paper:** GATE 2015 CS, 7 February Shift 2

**Question:**

Consider the following transaction involving two bank accounts x and y.
read (x); x := x - 50; write(x); read(y); y:= y + 50; write(y)
The constraint that the sum of the accounts x and y should remain constant is that of

**Options:**

A. Atomicity
B. Consistency
C. Isolation
D. Durability

**Type:** MCQ

**Answer:** VERIFICATION REQUIRED

**Source:** GATE 2015 CS, 7 February Shift 2, `12-PYQ/2015/set-02/question-paper.pdf`

---

### Q.51

**Paper:** GATE 2015 CS, 8 February Shift 1

**Question:**

Consider the following partialSchedule Sinvolving two transactions T1 and T2. Only the read and
the write operations have been shown. The read operation on data item P is denoted by read(P) and
the write operation on data item P is denoted by write(P).
Tıme Transaction-id
instance T1 T2
1 read(A)
2 write(A)
3 read(C)
4 write(C)
5 read(B)
6 write(B)
7 read(A)
8 commit
9 read(B)
Schedule S
Suppose that the transaction T1 fails immediately after time instance 9. Which one of the following
statements is correct?

**Options:**

A. T2 must be aborted and then both T1 and T2 must be re-started to ensure transaction atomicity
B. Schedule S 1s non-recoverable and cannot ensure transaction atomicity
C. Only T2 must be aborted and then re-started to ensure transaction atomicity
D. Schedule S'is recoverable and can ensure atomicity and nothing else needs to be done

**Type:** MCQ

**Answer:** VERIFICATION REQUIRED

**Source:** GATE 2015 CS, 8 February Shift 1, `12-PYQ/2015/set-03/question-paper.pdf`

---

## 2014

### Q.29

**Paper:** GATE 2014 CS SET-1

**Question:**

Consider the following four schedules due to three transactions (indicated by the subscript) using
read and write on a data item x, denoted by r(x) and w(x) respectively. Which one of them is
conflict serializable?

**Options:**

A. r_{1}(x); r_{2}(x); w_{1}(x); r_{3}(x); w_{2}(x) CS01 (GATE 2014)^{
B. }r_{2}(x);r_{1}(x);w_{2}(x);r_{3}(x);w_{1}(x)
C. r_{3}(x);r_{2}(x);r_{1}(x);w_{2}(x);w_{1}(x)
D. r_{2}(x);w_{2}(x);r_{3}(x);r_{1}(x);w_{1}(x)

**Type:** MCQ

**Answer:** VERIFICATION REQUIRED

**Source:** GATE 2014 CS SET-1, `12-PYQ/2014/set-01/question-paper.pdf`

---

### Q.29

**Paper:** GATE 2014 CS SET-2

**Question:**

Consider the following schedule S of transactions T1, T2, T3, T4:
T1  T2  T3  T4
Reads(X)
Writes(X)
Commit
Writes(X)
Commit
Writes(Y)
Reads(Z)
Commit
Reads(X)
Reads(Y)
Commit
Which one of the following statements is CORRECT?

**Options:**

A. S is conflict-serializable but not recoverable
B. S is not conflict-serializable but is recoverable
C. S is both conflict-serializable and recoverable
D. S is neither conflict-serializable nor is it recoverable

**Type:** MCQ

**Answer:** VERIFICATION REQUIRED

**Source:** GATE 2014 CS SET-2, `12-PYQ/2014/set-02/question-paper.pdf`

---

### Q.29

**Paper:** GATE 2014 CS SET-3

**Question:**

Consider the transactions T1, T2, and T3 and the schedules S1 and S2 given below.
T1: r1(X); r1(Z); w1(X); w1(Z)
T2: r2(Y); r2(Z); w2(Z)
T3: r3(Y); r3(X); w3(Y)
S1: r1(X); r3(Y); r3(X); r2(Y); r2(Z); w3(Y); w2(Z); r1(Z); w1(X); w1(Z)
S2: r1(X); r3(Y); r2(Y); r3(X); r1(Z); r2(Z); w3(Y); w1(X); w2(Z); w1(Z)
Which one of the following statements about the schedules is TRUE?

**Options:**

A. Only S1 is conflict-serializable.
B. Only S2 is conflict-serializable.
C. Both S1 and S2 are conflict-serializable.
D. Neither S1 nor S2 is conflict-serializable.

**Type:** MCQ

**Answer:** VERIFICATION REQUIRED

**Source:** GATE 2014 CS SET-3, `12-PYQ/2014/set-03/question-paper.pdf`

---

## 2012

### Q.27

**Paper:** GATE 2012 CS Booklet A

**Question:**

Consider the following transactions with data items P and Q initialized to zero:
T_{1} :read (P);
read (Q);
if  P = 0 then Q := Q + 1 ;
write (Q).
T_{2} : read (Q);
read (P);
if  Q = 0 then P := P + 1 ;
write (P).
Any non-serial interleaving of T_{1} and T_{2} for concurrent execution leads to

**Options:**

A. a serializable schedule
B. a schedule that is not conflict serializable
C. a conflict serializable schedule
D. a schedule for which a precedence graph cannot be drawn

**Type:** MCQ

**Answer:** VERIFICATION REQUIRED

**Source:** GATE 2012 CS Booklet A, `12-PYQ/2012/question-paper.pdf`

---

## 2010

### Q.42

**Paper:** GATE 2010 CS

**Question:**

Consider the following schedule for transactions TI. T2 and T3:
I1 I2 I3
Read ( X)
Read (Y)
Read (Y)
Write (Y)
Write (X)
Write (X)
Read (X)
Wrile (X)
Which one of the schedules below is the correct serialization of the above?

**Options:**

A. TI → T3 → T2
B. T2 → T1 → T3
C. T2 → T3 → T1
D. T3 → T1 → T2

**Type:** MCQ

**Answer:** VERIFICATION REQUIRED

**Source:** GATE 2010 CS, `12-PYQ/2010/question-paper.pdf`

---

## 2009

### Q.43

**Paper:** GATE 2009 CS

**Question:**

2009
Consider two transactions Ty and T2, and four schedules S1, S2, S3, S4 of T, and T2 as given below :
T;:R,[x] W,[x] W,[y]
[½:R,[x] R‚[y]W½[y]
S,:R,[x] R,[x] R,[y] W‚[x] W‚[y] W¿[y]
S¿:R‚[x] R‚[x] R‚[y] W‚[x] W¿[y] W‚[y]
S3 : R[0] W[0]R[x] m[][y] [y]
S4: Rz[x] R‚[y] R,[x] W,[x] W,[y] W½[y]
Which of the above schedules are conflict-serializable ?

**Options:**

A. Sı and S2
B. S2 and S3
C. S3 only
D. S4 only

**Type:** MCQ

**Answer:** VERIFICATION REQUIRED

**Source:** GATE 2009 CS, `12-PYQ/2009/question-paper.pdf`

---

## 2007

### Q.64

**Paper:** GATE 2007 CS

**Question:**

Consider the following schedules involving two transactions. Which one of the
following statements is TRUE?
SI: r(X); r(Y); r2(X); г2(Y); W2(Y); WI(X)
S2: ri(X); r2(X); r2(Y); wz(Y); rı(Y); wi(X)

**Options:**

A. Both Sj and S2 are conflict serializable.
B. S, is conflict serializable and S2 is not conflict serializable.
C. S, is not conflict serializable and S2 is conflict serializable.
D. Both S, and S2 are not conflict serializable.

**Type:** MCQ

**Answer:** VERIFICATION REQUIRED

**Source:** GATE 2007 CS, `12-PYQ/2007/question-paper.pdf`

---
