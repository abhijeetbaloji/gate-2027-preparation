# GATE PYQs

## 2026

### Q.54

**Paper:** GATE 2026 CS-1 (forenoon)

**Question:**

Consider a system that has a cache memory unit and a memory management unit
(MMU). The address input to the cache memory is a physical address. The MMU
has a translation lookaside buffer (TLB). Assume that when a page is evicted from
the main memory, the corresponding blocks in the cache are marked as invalid.
For a given memory reference, which of the following sequences of events can
NEVER happen?

**Options:**

A. TLB miss, Page table hit, Cache hit
B. TLB hit, Page table miss, Cache hit
C. TLB miss, Page table miss, Cache hit
D. TLB miss, Page table miss, Cache miss

**Type:** MCQ

**Answer:** VERIFICATION REQUIRED

**Source:** GATE 2026 CS-1 (forenoon), `12-PYQ/2026/set-01/question-paper.pdf`

---

### Q.54

**Paper:** GATE 2026 CS-2 (afternoon)

**Question:**

A system has a Translation Lookaside Buffer (TLB) that has a reach of 1 MB. TLB
reach is defined as the total amount of physical memory that can be accessed
through the TLB entries. The paging system uses pages of size 4 KB. The virtual
address space is 64 GB and physical address space is 1 GB. If each TLB entry stores
a 4-bit process id, page number, frame number, and a 2-bit control field, then the
size of the TLB (in bytes) is ___________. (answer in integer)
Note: 1K=2^{10}, 1M=2^{20}, 1G=2^{30}

**Options:**

The paper does not print options for this numerical-answer question.

**Type:** NAT

**Answer:** VERIFICATION REQUIRED

**Source:** GATE 2026 CS-2 (afternoon), `12-PYQ/2026/set-02/question-paper.pdf`

---

## 2025

### Q.14

**Paper:** GATE 2025 CS-1

**Question:**

Consider a demand paging memory management system with 32-bit logical
address, 20-bit physical address, and page size of 2048 bytes. Assuming that the
memory is byte addressable, what is the maximum number of entries in the page
table?

**Options:**

A. 2^{21}
B. 2^{20}
C. 2^{22}
D. 2^{24}

**Type:** MCQ

**Answer:** VERIFICATION REQUIRED

**Source:** GATE 2025 CS-1, `12-PYQ/2025/set-01/question-paper.pdf`

---

### Q.54

**Paper:** GATE 2025 CS-1

**Question:**

In optimal page replacement algorithm, information about all future page references
is available to the operating system (OS). A modification of the optimal page
replacement algorithm is as follows:
The OS correctly predicts only up to next 4 page references (including the current
page) at the time of allocating a frame to a page.
A process accesses the pages in the following order of page numbers:
1, 3, 2, 4, 2, 3, 1, 2, 4, 3, 1, 4.
If the system has three memory frames that are initially empty, the number of page
faults that will occur during execution of the process is ________ .  (Answer in
integer)

**Options:**

The paper does not print options for this numerical-answer question.

**Type:** NAT

**Answer:** VERIFICATION REQUIRED

**Source:** GATE 2025 CS-1, `12-PYQ/2025/set-01/question-paper.pdf`

---

### Q.47

**Paper:** GATE 2025 CS-2

**Question:**

Consider a demand paging system with three frames, and the following page
reference string: 1 2 3 4 5 4 1 6 4 5 1 3 2. The contents of the frames are as follows
initially and after each reference (from left to right):
initially  after
-  1* 2* 3* 4* 5* 4 1 6* 4 5 1* 3* 2*
-  1  1  1  1  1  1 1  6  6 6  6  6  2
-  -  2  2  4  4  4 4  4  4 4  1  1  1
-  -  -  3  3  5  5 5  5  5 5  5  3  3
The *-marked references cause page replacements.
Which one or more of the following could be the page replacement policy/policies
in use?

**Options:**

A. Least Recently Used page replacement policy
B. Least Frequently Used page replacement policy
C. Most Frequently Used page replacement policy
D. Optimal page replacement policy

**Type:** MSQ

**Answer:** VERIFICATION REQUIRED

**Source:** GATE 2025 CS-2, `12-PYQ/2025/set-02/question-paper.pdf`

---

### Q.58

**Paper:** GATE 2025 CS-2

**Question:**

A computer system supports a logical address space of 2^{32} bytes. It uses two-level
hierarchical paging with a page size of 4096 bytes. A logical address is divided into
a  𝑏-bit index to the outer page table, an offset within the page of the inner page
table, and an offset within the desired page. Each entry of the inner page table uses
eight bytes. All the pages in the system have the same size.
The value of 𝑏 is ___________ . (Answer in integer)

**Options:**

The paper does not print options for this numerical-answer question.

**Type:** NAT

**Answer:** VERIFICATION REQUIRED

**Source:** GATE 2025 CS-2, `12-PYQ/2025/set-02/question-paper.pdf`

---

## 2024

### Q.24

**Paper:** GATE 2024 CS2

**Question:**

Which of the following tasks is/are the responsibility/responsibilities of the memory
management unit (MMU) in a system with paging-based memory management?

**Options:**

A. Allocate a new page table for a newly created process
B. Translate a virtual address to a physical address using the page table
C. Raise a trap when a virtual address is not found in the page table Raise a trap when a process tries to write to a page marked with read-only
D. permission in the page table

**Type:** MCQ

**Answer:** VERIFICATION REQUIRED

**Source:** GATE 2024 CS2, `12-PYQ/2024/set-02/question-paper.pdf`

---

### Q.64

**Paper:** GATE 2024 CS2

**Question:**

Consider a 32-bit system with 4 KB page size and page table entries of size 4 bytes
each. Assume 1 KB = 2^{10} bytes. The OS uses a 2-level page table for memory
management, with the page table containing an outer page directory and an inner
page table. The OS allocates a page for the outer page directory upon process
creation. The OS uses demand paging when allocating memory for the inner page
table, i.e., a page of the inner page table is allocated only if it contains at least one
valid page table entry.
An active process in this system accesses 2000 unique pages during its execution,
and none of the pages are swapped out to disk. After it completes the page accesses,
let X denote the minimum and Y denote the maximum number of pages across the
two levels of the page table of the process.
The value of X+Y is ________

**Options:**

The paper does not print options for this numerical-answer question.

**Type:** NAT

**Answer:** VERIFICATION REQUIRED

**Source:** GATE 2024 CS2, `12-PYQ/2024/set-02/question-paper.pdf`

---

## 2023

### Q.23

**Paper:** GATE 2023 CS

**Question:**

Which one or more of the following options guarantee that a computer system will
transition from user mode to kernel mode?

**Options:**

A. Function Call
B. malloc Call
C. Page Fault
D. System Call

**Type:** MSQ

**Answer:** VERIFICATION REQUIRED

**Source:** GATE 2023 CS, `12-PYQ/2023/question-paper.pdf`

---

## 2022

### Q.64

**Paper:** GATE 2022 CS

**Question:**

Consider a demand paging system with four page frames (initially empty) and LRU
page replacement policy. For the following page reference string
7,2,7,3,2,5,3,4,6,7,7,1,5,6,1
the page fault rate, defined as the ratio of number of page faults to the number of
memory accesses (rounded off to one decimal place) is_________.

**Options:**

The paper does not print options for this numerical-answer question.

**Type:** NAT

**Answer:** VERIFICATION REQUIRED

**Source:** GATE 2022 CS, `12-PYQ/2022/question-paper.pdf`

---

## 2021

### Q.11

**Paper:** GATE 2021 CS Set-1

**Question:**

In the context of operating systems, which of the following statements is/are correct
with respect to paging?

**Options:**

A. Paging helps solve the issue of external fragmentation.
B. Page size has no impact on internal fragmentation.
C. | Paging incurs memory overheads.
D. Multi-level paging is necessary to support pages of different sizes.

**Type:** MCQ

**Answer:** VERIFICATION REQUIRED

**Source:** GATE 2021 CS Set-1, `12-PYQ/2021/set-01/question-paper.pdf`

---

## 2020

### Q.11

**Paper:** GATE 2020 CS

**Question:**

Consider allocation of memory to a new process. Assume that none of the existing
holes in the memory will exactly fit the process's memory requirement. Hence, a
new hole of smaller size will be created if allocation is made in any of the existing
holes. Which one of the following statements is TRUE?

**Options:**

A. The hole created by first fit is always larger than the hole created by next fit.
B. The hole created by worst fit is always larger than the hole created by first fit. () The hole created by best fit is never larger than the hole created by first fit.
D. The hole created by next fit is never larger than the hole created by best fit.

**Type:** MCQ

**Answer:** VERIFICATION REQUIRED

**Source:** GATE 2020 CS, `12-PYQ/2020/question-paper.pdf`

---

### Q.53

**Paper:** GATE 2020 CS

**Question:**

Consider a paging system that uses 1-level page table residing in main memory
and a TLB for address translation. Each main memory access takes 100 ns and
TLB lookup takes 20 ns. Each page transfer to/from the disk takes 5000 ns.
Assume that the TLB hit ratio is 95%, page fault rate is 10%. Assume that for
20% of the total page faults, a dirty page has to be written back to disk before the
required page is read in from disk. TLB update time is negligible. The average
memory access time in ns (round off to 1 decimal places) is _

**Options:**

The paper does not print options for this numerical-answer question.

**Type:** NAT

**Answer:** VERIFICATION REQUIRED

**Source:** GATE 2020 CS, `12-PYQ/2020/question-paper.pdf`

---

## 2019

### Q.33

**Paper:** GATE 2019 CS (printed header Set-2)

**Question:**

Assume that in a certain computer, the vittual addresses are 64 bits long and the physical
addresses are 48 bits long. The memory is word addressible. The page size is 8 kB and the
word size is 4 bytes. The Translation Look-aside Buffer (TLB) in the address translation path
has 128 valid entries. At most how many distinct virtual addresses can be translated without
any TLB miss?

**Options:**

A. 16×210
B. 256×2°
C. 4x220
D. 8×22°

**Type:** MCQ

**Answer:** VERIFICATION REQUIRED

**Source:** GATE 2019 CS (printed header Set-2), `12-PYQ/2019/question-paper.pdf`

---

## 2018

### Q.10

**Paper:** GATE 2018 CS

**Question:**

Consider a process executing on an operating system that uses demand paging. The average
time for a memory access in the system is  M units if the corresponding memory page is
available in memory, and  D units if the memory access causes a page fault. It has been
experimentally measured that the average time taken for a memory access in the process is
X units.
Which one of the following is the correct expression for the page fault rate experienced by
the process?

**Options:**

A. (D – M) / (X – M)
B. (X – M) / (D – M)
C. (D – X) / (D – M)
D. (X – M) / (D – X)

**Type:** MCQ

**Answer:** VERIFICATION REQUIRED

**Source:** GATE 2018 CS, `12-PYQ/2018/question-paper.pdf`

---

## 2016

### Q.49

**Paper:** GATE 2016 CS-1

**Question:**

Consider a computer system with ten physical page frames. The system is provided with
an access sequence (a_{1}, a_{2},..., a_{20}, a_{1}, a_{2},..., a_{20}), where each a_{i} is a distinct virtual page
number. The difference in the number of page faults between the last-in-first-out page
replacement policy and the optimal page replacement policy is  .
CS(Set A)  15/17

**Options:**

The paper does not print options for this numerical-answer question.

**Type:** NAT

**Answer:** VERIFICATION REQUIRED

**Source:** GATE 2016 CS-1, `12-PYQ/2016/set-01/question-paper.pdf`

---

### Q.20

**Paper:** GATE 2016 CS-2

**Question:**

In which one of the following page replacement algorithms it is possible for the page fault rate
to increase even when the number of allocated frames increases?

**Options:**

A. LRU (Least Recently Used)
B. OPT (Optimal Page Replacement)
C. MRU (Most Recently Used)
D. FIFO (First In First Out) CS(Set B) 5/18

**Type:** MCQ

**Answer:** VERIFICATION REQUIRED

**Source:** GATE 2016 CS-2, `12-PYQ/2016/set-02/question-paper.pdf`

---

## 2015

### Q.57

**Paper:** GATE 2015 CS, 7 February Shift 1

**Question:**

10

Consider a main memory with five page frames and the following sequence of page references: 3,
8, 2, 3, 9, 1, 6, 3, 8, 9, 3, 6, 2, 1, 3. Which one of the following is true with respect to page
replacement policies First In First Out (FIFO) and Least Recently Used (LRU)?

**Options:**

A. Both incur the same number of page faults
B. FIFO incurs 2 more page faults than LRU
C. LRU incurs 2 more page faults than FIFO
D. FIFO incurs 1 more page faults than LRU D

**Type:** MCQ

**Answer:** VERIFICATION REQUIRED

**Source:** GATE 2015 CS, 7 February Shift 1, `12-PYQ/2015/set-01/question-paper.pdf`

---

### Q.19

**Paper:** GATE 2015 CS, 7 February Shift 2

**Question:**

14

A computer system implements a 40-bit virtual address, page size of 8 kilobytes, and a 128-entry
translation look-aside buffer (TLB) organized into 32 sets each having four ways. Assume that the
TLB tag does not store any process id. The minimum length of the TLB tag in bits is _
Correct Answer:

**Options:**

The paper does not print options for this numerical-answer question.

**Type:** NAT

**Answer:** VERIFICATION REQUIRED

**Source:** GATE 2015 CS, 7 February Shift 2, `12-PYQ/2015/set-02/question-paper.pdf`

---

### Q.41

**Paper:** GATE 2015 CS, 7 February Shift 2

**Question:**

4.

Consıder six memory partitions of sizes 200 KB, 400 KB, 600 KB, 500 KB, 300 KB and 250 KB,
where KB refers to kilobyte. These partitions need to be allotted to four processes of sizes 357 KB,
210 KB, 468 KB and 491 KB in that order. If the best fit algorithm is used, which partitions are
NOT allotted to any process?

**Options:**

A. 200 KB and 300 KB
B. 200 KB and 250 KB
C. 250 KB and 300 KB
D. 300 KB and 400 KB

**Type:** MCQ

**Answer:** VERIFICATION REQUIRED

**Source:** GATE 2015 CS, 7 February Shift 2, `12-PYQ/2015/set-02/question-paper.pdf`

---

## 2014

### Q.33

**Paper:** GATE 2014 CS SET-1

**Question:**

Assume that there are 3 page frames which are initially empty. If the page reference string is 1, 2, 3,
4, 2, 1, 5, 3, 2, 4, 6, the number of page faults using the optimal replacement policy is__________.

**Options:**

The paper does not print options for this numerical-answer question.

**Type:** NAT

**Answer:** VERIFICATION REQUIRED

**Source:** GATE 2014 CS SET-1, `12-PYQ/2014/set-01/question-paper.pdf`

---

### Q.33

**Paper:** GATE 2014 CS SET-2

**Question:**

A computer  has twenty physical page frames which contain pages numbered 101 through 120.
Now a program accesses the pages numbered 1, 2, …, 100 in that order, and repeats the access
sequence THRICE. Which one of the following page replacement policies experiences the same
number of page faults as the optimal page replacement policy for this program?

**Options:**

A. Least-recently-used
B. First-in-first-out
C. Last-in-first-out
D. Most-recently-used

**Type:** MCQ

**Answer:** VERIFICATION REQUIRED

**Source:** GATE 2014 CS SET-2, `12-PYQ/2014/set-02/question-paper.pdf`

---

### Q.20

**Paper:** GATE 2014 CS SET-3

**Question:**

A system uses 3 page frames for storing process pages in main memory. It uses the Least Recently
Used (LRU) page replacement policy. Assume that all the page frames are initially empty. What is
the total number of page faults that will occur while processing the page reference string given
below?
4,  7,  6,  1,  7,  6,  1,  2,  7,  2

**Options:**

The paper does not print options for this numerical-answer question.

**Type:** NAT

**Answer:** VERIFICATION REQUIRED

**Source:** GATE 2014 CS SET-3, `12-PYQ/2014/set-03/question-paper.pdf`

---

### Q.33

**Paper:** GATE 2014 CS SET-3

**Question:**

Consider a paging hardware with a TLB. Assume that the entire page table and all the pages are  in
the physical memory. It takes 10 milliseconds to search the TLB and 80 milliseconds to access the
physical memory. If the TLB hit ratio is 0.6, the effective memory access time (in milliseconds) is
_________.

**Options:**

The paper does not print options for this numerical-answer question.

**Type:** NAT

**Answer:** VERIFICATION REQUIRED

**Source:** GATE 2014 CS SET-3, `12-PYQ/2014/set-03/question-paper.pdf`

---

## 2012

### Q.42

**Paper:** GATE 2012 CS Booklet A

**Question:**

Consider the virtual page reference string
1,  2,  3,  2,  4,  1,  3,  2,  4,  1
on a demand paged virtual memory system running on a computer system that has main memory
size of 3 page frames which are initially empty. Let LRU, FIFO and OPTIMAL denote the number
of page faults under the corresponding page replacement policy. Then

**Options:**

A. OPTIMAL < LRU < FIFO
B. OPTIMAL < FIFO < LRU
C. OPTIMAL = LRU
D. OPTIMAL = FIFO

**Type:** MCQ

**Answer:** VERIFICATION REQUIRED

**Source:** GATE 2012 CS Booklet A, `12-PYQ/2012/question-paper.pdf`

---

## 2011

### Q.20

**Paper:** GATE 2011 CS Booklet A

**Question:**

Let the page fault service time be 10 ms in a computer with average memory access time being
20 ns. If one page fault is generated for every 10° memory accesses, what is the effective acces:
time for the memory?

**Options:**

A. 21 ns
B. 30 ns
C. 23 ns
D. 35 ns

**Type:** MCQ

**Answer:** VERIFICATION REQUIRED

**Source:** GATE 2011 CS Booklet A, `12-PYQ/2011/question-paper.pdf`

---

## 2010

### Q.24

**Paper:** GATE 2010 CS

**Question:**

A system uses FIFO policy lor page roplacemem. ln has 4 page frames with no pages loaded to bogin with. Thesysem firstaccesses 100 distinet pages in some order und then accesses the sume
100 puges but now in the reverso order. Horw many page faults will occur?

**Options:**

A. 19 (13) 192 (1') 197
D. 195 325

**Type:** MCQ

**Answer:** VERIFICATION REQUIRED

**Source:** GATE 2010 CS, `12-PYQ/2010/question-paper.pdf`

---

## 2009

### Q.9

**Paper:** GATE 2009 CS

**Question:**

In which one of the following page replacement policies, Belady's anomaly may occur?

**Options:**

A. FIFO
B. Optimal
C. LRU
D. MRU

**Type:** MCQ

**Answer:** VERIFICATION REQUIRED

**Source:** GATE 2009 CS, `12-PYQ/2009/question-paper.pdf`

---

### Q.34

**Paper:** GATE 2009 CS

**Question:**

A multilevel page table is preferred in comparison to a single level page table for translating virtual
address to physical address because

**Options:**

A. it reduces the memory access time to read or write a memory location.
B. it helps to reduce the size of page table needed to implement the virtual address space of a process.
C. it is required by the translation lookaside buffer.
D. it helps to reduce the number of page faults in page replacement algorithms.

**Type:** MCQ

**Answer:** VERIFICATION REQUIRED

**Source:** GATE 2009 CS, `12-PYQ/2009/question-paper.pdf`

---

## 2007

### Q.56

**Paper:** GATE 2007 CS

**Question:**

A virtual memory system uses First In First Out (FIFO) page replacement policy and
allocates a fixed number of frames to a process. Consider the following statements:
P: Increasing the number of page frames allocated to a process sometimes increases
the page fault rate.
Q: Some programs do not exhibit locality of reference.
Which one of the following is TRUE?

**Options:**

A. Both P and Q are true, and Q is the reason for P.
B. Both P and Q are true, but Q is not the reason for P.
C. P is false, but Q is true.
D. Both P and Q are false.

**Type:** MCQ

**Answer:** VERIFICATION REQUIRED

**Source:** GATE 2007 CS, `12-PYQ/2007/question-paper.pdf`

---

### Q.82

**Paper:** GATE 2007 CS

**Question:**

If optimal page replacement policy is used, how many page faults occur for the above
reference string?

**Options:**

A. 7
B. 8
C. 9
D. 10

**Type:** MCQ

**Answer:** VERIFICATION REQUIRED

**Source:** GATE 2007 CS, `12-PYQ/2007/question-paper.pdf`

---

### Q.83

**Paper:** GATE 2007 CS

**Question:**

Least Recently Used (LRU) page replacement policy is a practical approximation to
optimal page replacement. For the above reference string, how many more page faults
occur with LRU than with the optimal page replacement policy?

**Options:**

A. 0
B. 1
C. 2
D. 3 CS - 20/24 Statement for Linked Answer Questions 84 & 85: Suppose that a robot is placed on the Cartesian plane. At each step it is allowed to move either one unit up or one unit right, i.e., if it is at (i, j) then it can move to either (i +1,j) or (i,j +1).

**Type:** MCQ

**Answer:** VERIFICATION REQUIRED

**Source:** GATE 2007 CS, `12-PYQ/2007/question-paper.pdf`

---
