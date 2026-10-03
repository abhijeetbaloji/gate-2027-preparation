# GATE PYQs

## 2026

### Q.24

**Paper:** GATE 2026 CS-1 (forenoon)

**Question:**

Consider a hash table  𝑃[0, 1, … , 10]  that is initially empty. The hash table is
maintained using open addressing with linear probing. The hash function used is
ℎ(𝑥) = (𝑥+ 7) mod 11.
Consider the following sequence of insertions performed on 𝑃:
1, 13, 22, 15, 11, 24
Which of the following positions in the hash table is/are empty after these insertions
are performed?

**Options:**

A. 0
B. 10
C. 2
D. 1

**Type:** MCQ

**Answer:** VERIFICATION REQUIRED

**Source:** GATE 2026 CS-1 (forenoon), `12-PYQ/2026/set-01/question-paper.pdf`

---

### Q.30

**Paper:** GATE 2026 CS-2 (afternoon)

**Question:**

The keys 5, 28, 19, 15, 26, 33, 12, 17, 10 are inserted into a hash table using the
hash function ℎ(𝑘) = 𝑘 𝑚𝑜𝑑 9. The collisions are resolved by chaining. After all
the keys are inserted, the length of the longest chain is __________. (answer in
integer)

**Options:**

The paper does not print options for this numerical-answer question.

**Type:** NAT

**Answer:** VERIFICATION REQUIRED

**Source:** GATE 2026 CS-2 (afternoon), `12-PYQ/2026/set-02/question-paper.pdf`

---

### Q.46

**Paper:** GATE 2026 CS-2 (afternoon)

**Question:**

An index in a DBMS is said to be dense if an index entry appears for every
search-key value in the indexed file. Otherwise it is called a sparse index. Consider
the following two statements.
S1: A hash index must be a dense index
S2: A 𝐵^{+} tree index can be a sparse index
Which one of the following options is correct?

**Options:**

A. Both S1 and S2 are true
B. Both S1 and S2 are false
C. S1 is true and S2 is false
D. S1 is false and S2 is true

**Type:** MCQ

**Answer:** VERIFICATION REQUIRED

**Source:** GATE 2026 CS-2 (afternoon), `12-PYQ/2026/set-02/question-paper.pdf`

---

## 2025

### Q.65

**Paper:** GATE 2025 CS-1

**Question:**

In a double hashing scheme, ℎ_{1}(𝑘) = 𝑘 mod  11 and ℎ_{2}(𝑘) = 1 + (𝑘 mod  7) are
the auxiliary hash functions. The size 𝑚 of the hash table is 11. The hash function
for the  i-th probe in the open address table is  [ℎ_{1}(𝑘) + 𝑖 ℎ_{2}(𝑘)] mod  𝑚. The
following keys are inserted in the given order: 63, 50, 25, 79, 67, 24.
The slot at which key 24 gets stored is ___________. (Answer in integer)

**Options:**

The paper does not print options for this numerical-answer question.

**Type:** NAT

**Answer:** VERIFICATION REQUIRED

**Source:** GATE 2025 CS-1, `12-PYQ/2025/set-01/question-paper.pdf`

---

## 2024

### Q.26

**Paper:** GATE 2024 CS2

**Question:**

Which of the following file organizations is/are I/O efficient for the scan operation
in DBMS?

**Options:**

A. Sorted
B. Heap
C. Unclustered tree index
D. Unclustered hash index

**Type:** MCQ

**Answer:** VERIFICATION REQUIRED

**Source:** GATE 2024 CS2, `12-PYQ/2024/set-02/question-paper.pdf`

---

## 2022

### Q.16

**Paper:** GATE 2022 CS

**Question:**

Suppose we are given  n keys,  m hash table slots, and two simple uniform hash
functions  h_{1}  and  h_{2} . Further suppose our hashing scheme uses  h_{1}  for the odd keys
and  h_{2}  for the even keys. What is the expected number of keys in a slot?

**Options:**

A. m n
B. n m
C. 2n m
D. n 2m

**Type:** MCQ

**Answer:** VERIFICATION REQUIRED

**Source:** GATE 2022 CS, `12-PYQ/2022/question-paper.pdf`

---

### Q.38

**Paper:** GATE 2022 CS

**Question:**

Which one of the following statements is FALSE?

**Options:**

A. The TLB performs an associative search in parallel on all its valid entries using page number of incoming virtual address.
B. If the virtual address of a word given by CPU has a TLB hit, but the subsequent search for the word results in a cache miss, then the word will always be present in the main memory.
C. The memory access time using a given inverted page table is always same for all incoming virtual addresses.
D. In a system that uses hashed page tables, if two distinct virtual addresses V1 and V2 map to the same value while hashing, then the memory access time of these addresses will not be the same.

**Type:** MCQ

**Answer:** VERIFICATION REQUIRED

**Source:** GATE 2022 CS, `12-PYQ/2022/question-paper.pdf`

---

## 2020

### Q.23

**Paper:** GATE 2020 CS

**Question:**

Consider a double hashing scheme in which the primary hash function is
h,(k) = k mod 23, and the secondary hash function is h(k)=1+(k mod 19).
Assume that the table size is 23. Then the address returned by probe 1 in the probe
sequence (assume that the probe sequence begins at probe 0) for key value k = 90
is

**Options:**

The paper does not print options for this numerical-answer question.

**Type:** NAT

**Answer:** VERIFICATION REQUIRED

**Source:** GATE 2020 CS, `12-PYQ/2020/question-paper.pdf`

---

## 2015

### Q.50

**Paper:** GATE 2015 CS, 7 February Shift 2

**Question:**

Which one of the following hash functions on integers will distribute keys most uniformly over 10
buckets numbered 0 to 9 for i ranging from 0 to 2020?

**Options:**

A. h(i) = i2 mod 10
B. h(i) = i mod 10
C. h(i) = (11 * i2) mod 10
D. h(i) = (12 * i) mod 10

**Type:** MCQ

**Answer:** VERIFICATION REQUIRED

**Source:** GATE 2015 CS, 7 February Shift 2, `12-PYQ/2015/set-02/question-paper.pdf`

---

### Q.22

**Paper:** GATE 2015 CS, 8 February Shift 1

**Question:**

199

Given a hash table T with 25 slots that stores 2000 elements, the load factor a for T is
Correct Answer :

**Options:**

The paper does not print options for this numerical-answer question.

**Type:** NAT

**Answer:** VERIFICATION REQUIRED

**Source:** GATE 2015 CS, 8 February Shift 1, `12-PYQ/2015/set-03/question-paper.pdf`

---

## 2014

### Q.40

**Paper:** GATE 2014 CS SET-1

**Question:**

Consider a hash table with 9 slots. The hash function is h(k) = k mod 9. The collisions are
resolved by chaining.  The following 9 keys are inserted in the order: 5, 28, 19, 15, 20, 33, 12, 17,
10.  The maximum, minimum, and average chain lengths in the hash table, respectively, are

**Options:**

A. 3, 0, and 1
B. 3, 3, and 3
C. 4, 0, and 1
D. 3, 0, and 2

**Type:** MCQ

**Answer:** VERIFICATION REQUIRED

**Source:** GATE 2014 CS SET-1, `12-PYQ/2014/set-01/question-paper.pdf`

---

### Q.40

**Paper:** GATE 2014 CS SET-3

**Question:**

Consider a hash table with 100 slots. Collisions are resolved using chaining. Assuming simple
uniform hashing, what is the probability that the first 3 slots are unfilled after the first 3 insertions?

**Options:**

A. (97 × 97 × 97)/1003
B. (99 × 98 × 97)/1003
C. (97 × 96 × 95)/1003
D. (97 × 96 × 95)/(3! x 1003)

**Type:** MCQ

**Answer:** VERIFICATION REQUIRED

**Source:** GATE 2014 CS SET-3, `12-PYQ/2014/set-03/question-paper.pdf`

---

## 2011

### Q.39

**Paper:** GATE 2011 CS Booklet A

**Question:**

Consider a relational table r with sufficient number of records, having attributes A,, Az, .... A, and
let 1 ≤P ≤n. Two queries Q1 and Q2 are given below.
Ql: TA1, (04,= (r)) where c is a constant
Q2: T.A (O,5A,5r, (r)) where c, and ez are constants
The database can be configured to do ordered indexing on A, or hashing on Ap. Which of the
following statements is TRUE?

**Options:**

A. Ordered indexing will always outperform hashing for both queries
B. Hashing will always outperform ordered indexing for both queries
C. Hashing Will outperform ordered indexing on Q1, but not on Q2
D. Hashing will outperform ordered indexing on Q2, but not on Ql CS-A 10/20 2011 CS

**Type:** MCQ

**Answer:** VERIFICATION REQUIRED

**Source:** GATE 2011 CS Booklet A, `12-PYQ/2011/question-paper.pdf`

---

## 2010

### Q.50

**Paper:** GATE 2010 CS

**Question:**

What is the minimurn possible weight of a spanning tree I' in this graph such ehat vertex () is a leaf
node in the tree T?

**Options:**

A. 7
B. 8 (0)=
C. 9
D. 10 12/25 2010 Linked Answer Questions Scatement for Linked Answer Questions 52 and 53: A hash table of length 10 uses open addressing with hash function h(k) = k mod /0, and linedl robing. After inserting 6 values into an empty hash table, the table is as shown below 2 42 3 23 4 34 5 52 6 46 8

**Type:** MCQ

**Answer:** VERIFICATION REQUIRED

**Source:** GATE 2010 CS, `12-PYQ/2010/question-paper.pdf`

---

### Q.53

**Paper:** GATE 2010 CS

**Question:**

How many different insertion sequences of the key values using the same hash function and linear
probing will result in the hash table shown above?

**Options:**

A. 4
B. 3
C. 2
D. 1

**Type:** MCQ

**Answer:** VERIFICATION REQUIRED

**Source:** GATE 2010 CS, `12-PYQ/2010/question-paper.pdf`

---

## 2009

### Q.36

**Paper:** GATE 2009 CS

**Question:**

The keys 12, 18, 13, 2, 3, 23, 5 and 15 are inserted into an initially empty hash table of length 10 using
open addressing with hash function h(k) = k mod 10 and linear probing. What is the resultant hash
table ?

**Options:**

D. 0 0 0 2 12 12 12,2 23 13 13 13, 3, 23 2 15 5 3 5,15 6 23 5 18 8 18 8 18 18 9 15 2009 CS

**Type:** NAT

**Answer:** VERIFICATION REQUIRED

**Source:** GATE 2009 CS, `12-PYQ/2009/question-paper.pdf`

---

## 2007

### Q.40

**Paper:** GATE 2007 CS

**Question:**

Consider a hash table of size seven, with starting index zero, and a hash function
(3x+4) mod 7. Assuming the hash table is initially empty, which of the foilowing is
the contents of the table when the sequence 1,3,8,10 is inserted into the table using
closed hashing? Note that - denotes an empty location in the table.

**Options:**

A. 8,-, -, -, -, -,10
B. 1,8,10, -, -,-,3
C. 1,-,-,-,-,-,3
D. 1,10,8, -, -, -,3 S/121 Food/06-CS-2 CS - 9/24

**Type:** MCQ

**Answer:** VERIFICATION REQUIRED

**Source:** GATE 2007 CS, `12-PYQ/2007/question-paper.pdf`

---
