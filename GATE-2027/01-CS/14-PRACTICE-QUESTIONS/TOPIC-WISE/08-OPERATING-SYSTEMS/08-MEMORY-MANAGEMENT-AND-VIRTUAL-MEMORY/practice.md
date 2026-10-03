# Memory Management and Virtual Memory — Practice Questions

Original practice for GATE CS. These questions are not from any GATE paper. Attempt the questions before reading the solutions.

Reference string R, used by the replacement questions that name it, is

```text
4, 1, 2, 4, 3, 2, 1, 5, 4, 2, 5, 3
```

All frames start empty. A fault occurs when the referenced page is not in a frame. FIFO replaces the page that has been resident longest. LRU replaces the page whose most recent use is furthest in the past. Optimal replaces the page whose next use is furthest in the future; a page that never appears again is the furthest. If several resident pages never appear again, Optimal replaces the one that was loaded earliest.

## Level 1 — Conceptual

## Q1 — MSQ

**Select all that apply.**

A. Pure paging wastes space inside the last allocated page of a region (internal fragmentation)
B. In the classical model, pure paging creates external fragmentation the way variable-size contiguous partitions do
C. Pure segmentation can leave external fragmentation between segments
D. Internal fragmentation is unused space inside a block that has already been allocated

---

## Q2 — MSQ

**Select all that apply.**

A. A TLB caches recent virtual-to-physical translations
B. A TLB hit can satisfy the translation without a memory read of the page table
C. A TLB stores the file's data blocks
D. After a context switch to a process with a different address space, old TLB entries must not be used as that process's translations

---

## Q3 — MCQ

Pure segmentation, with segments placed in variable-size holes, is prone to

A. external fragmentation
B. a page offset that is longer than the virtual address
C. Belady's anomaly on every reference string
D. a TLB that can hold only one segment table entry in total

---

## Q4 — MCQ

Thrashing means

A. the system spends most of its time paging, and the CPU does little useful work of the processes
B. the ready queue is empty because every process is CPU-bound
C. FIFO has just been replaced by Optimal
D. internal fragmentation has filled the disk

---

## Q5 — MSQ

**Select all that apply.**

Which replacement policies are free of Belady's anomaly (more frames never increase the fault count on a given string)?

A. LRU
B. Optimal
C. FIFO
D. A policy that replaces a random resident page

---

## Level 2 — Standard GATE Style

## Q6 — NAT

Reference string R is run with 3 frames under FIFO. The number of page faults is ____.

---

## Q7 — MCQ

Reference string R with 3 frames under LRU produces

A. 7 faults
B. 8 faults
C. 9 faults
D. 12 faults

---

## Q8 — MCQ

Reference string R with 3 frames under Optimal produces

A. 5 faults
B. 6 faults
C. 7 faults
D. 9 faults

---

## Q9 — MCQ

A virtual address is 32 bits and the page size is 4 KB. The page offset occupies

A. 10 bits
B. 12 bits
C. 20 bits
D. 32 bits

---

## Q10 — MCQ

With a 32-bit virtual address and a 4 KB page, the virtual page number occupies

A. 10 bits
B. 12 bits
C. 20 bits
D. 22 bits

---

## Q11 — NAT

A process uses 256 KB of paged virtual memory. The page size is 2 KB. The number of pages is ____.

---

## Level 3 — Multi-Step

## Q12 — NAT

A single-level page table is used. A TLB reference takes 10 ns and a memory reference takes 100 ns. The TLB hit ratio is 0.90. A hit costs a TLB reference plus one memory reference for the data. A miss costs a TLB reference, one memory reference for the page-table entry, and one memory reference for the data. The effective memory-access time, in nanoseconds, is ____.

---

## Q13 — MCQ

The times and the hit ratio are the same as in Q12, but the page table has two levels. A hit still costs a TLB reference plus the data reference. A miss costs a TLB reference, two memory references to walk the page tables, and one memory reference for the data. The effective access time is

A. 110 ns
B. 120 ns
C. 130 ns
D. 310 ns

---

## Q14 — MSQ

**Select all that apply.**

An inverted page table on this machine

A. has one entry per physical frame
B. stores one full conventional entry for every virtual page of every process, indexed only by virtual page number
C. is searched associatively or by hashing, rather than by using the virtual page number as a direct index into a per-process table of virtual-page size
D. grows with the number of frames, not with the size of the virtual address space

---

## Q15 — NAT

The virtual address is `0x2F3C` and the page size is 512 bytes. The virtual page number, as a decimal integer, is ____.

---

## Q16 — MCQ

For the address and page size in Q15, the page offset as a decimal integer is

A. 60
B. 316
C. 512
D. 47

---

## Level 4 — Tricky / Trap-Based

## Q17 — MCQ

FIFO is applied to the reference string

```text
1, 4, 6, 5, 1, 4, 3, 1, 4, 6, 5, 3
```

Frames start empty. Which statement is correct?

A. Three frames cause 9 faults and four frames cause 10 faults, so adding a frame increases the FIFO fault count
B. Three frames cause 10 faults and four frames cause 9 faults
C. Both frame counts cause 9 faults
D. Optimal replacement on this string also faults more often with four frames than with three

---

## Q18 — MSQ

**Select all that apply.**

A. Paging leaves internal fragmentation in a page that is only partly filled
B. Pure segmentation can suffer external fragmentation
C. Paging of the classical kind suffers external fragmentation among variable-size holes
D. Variable-size contiguous partitions suffer external fragmentation

---

## Q19 — MCQ

The page size is 512 bytes, so the offset field is 9 bits. Which statement is correct?

A. The offset value 512 can appear in that 9-bit field
B. The offset value 316 means the page's valid bit is 0
C. The valid/invalid bit belongs to the page-table entry. A legal offset is an integer from 0 through 511; 512 does not fit in 9 bits
D. The offset value 511 is illegal because it uses every bit of the field

---

## Level 5 — Challenge

## Q20 — NAT

Virtual addresses are 32 bits, the page size is 4 KB, and each page-table entry is 4 bytes. A process uses a contiguous 6 MB region that starts at virtual address 0. An inner page table is allocated only if at least one of its entries is needed, and each inner page table occupies one page. The outer page table occupies one page. The number of pages used to store this process's page tables is ____.

---

## Q21 — MCQ

For the page tables in Q20, the number of bytes occupied by those page-table pages is

A. 4096
B. 8192
C. 12288
D. 1536

---

## Q22 — MSQ

**Select all that apply.**

On reference string R with 3 frames,

A. FIFO causes 8 faults
B. LRU causes 9 faults
C. Optimal causes 7 faults
D. LRU causes fewer faults than FIFO

---

## Answer Key

| Q | Type | Answer |
|---|---|---|
| 1 | MSQ | A, C, D |
| 2 | MSQ | A, B, D |
| 3 | MCQ | A |
| 4 | MCQ | A |
| 5 | MSQ | A, B |
| 6 | NAT | 8 |
| 7 | MCQ | C |
| 8 | MCQ | C |
| 9 | MCQ | B |
| 10 | MCQ | C |
| 11 | NAT | 128 |
| 12 | NAT | 120 |
| 13 | MCQ | C |
| 14 | MSQ | A, C, D |
| 15 | NAT | 23 |
| 16 | MCQ | B |
| 17 | MCQ | A |
| 18 | MSQ | A, B, D |
| 19 | MCQ | C |
| 20 | NAT | 3 |
| 21 | MCQ | C |
| 22 | MSQ | A, B, C |

## Detailed Solutions

### Q1

Answer: A, C, D

A page is a fixed block. The unused tail of the last page is internal fragmentation. Classical paging places those fixed frames in any free frame, so it does not leave variable-size holes between allocations. A segment is a contiguous variable-size piece, and the holes between segments are external fragmentation. Internal fragmentation is space inside an allocated unit, which is the definition used in A and D.

### Q2

Answer: A, B, D

The TLB holds page-table translations, not file data. On a hit, the frame number comes from the TLB and the walk of the page table in memory is skipped. Entries installed for one address space must be flushed or tagged so that another process does not consume them.

### Q3

Answer: A

Segments occupy variable-length regions. After segments are freed, the free holes may be too small or too scattered for a new segment. That is external fragmentation. The offset of a segment is part of the address, not longer than the address. Belady's anomaly is a paging-replacement fact about FIFO, not a property of every segment reference. A TLB is not limited to one segment-table entry by the definition of segmentation.

### Q4

Answer: A

Thrashing is a page-fault storm: processes do not keep their working sets resident, so the CPU repeatedly handles faults instead of running user instructions. An empty ready queue of CPU-bound processes would mean the opposite, a shortage of CPU work without saying anything about paging. Replacing FIFO by Optimal is a policy choice. Internal fragmentation does not fill the disk with faults.

### Q5

Answer: A, B

LRU and Optimal are stack algorithms: the set of pages kept with \(n\) frames is a subset of the set kept with \(n+1\) frames, so extra frames do not add faults. FIFO does not have that property; Q17 is a concrete case. Random replacement has no such guarantee either.

### Q6

Answer: 8

FIFO, 3 frames. The left end of each list is the oldest resident page.

| Reference | Result | Frames |
|---|---|---|
| 4 | fault | 4 |
| 1 | fault | 4, 1 |
| 2 | fault | 4, 1, 2 |
| 4 | hit | 4, 1, 2 |
| 3 | fault | 1, 2, 3 |
| 2 | hit | 1, 2, 3 |
| 1 | hit | 1, 2, 3 |
| 5 | fault | 2, 3, 5 |
| 4 | fault | 3, 5, 4 |
| 2 | fault | 5, 4, 2 |
| 5 | hit | 5, 4, 2 |
| 3 | fault | 4, 2, 3 |

Faults: 4, 1, 2, 3, 5, 4, 2, 3. Count = 8.

### Q7

Answer: C

LRU, 3 frames. The right end is the most recently used page.

| Reference | Result | Frames (oldest → newest) |
|---|---|---|
| 4 | fault | 4 |
| 1 | fault | 4, 1 |
| 2 | fault | 4, 1, 2 |
| 4 | hit | 1, 2, 4 |
| 3 | fault | 2, 4, 3 |
| 2 | hit | 4, 3, 2 |
| 1 | fault | 3, 2, 1 |
| 5 | fault | 2, 1, 5 |
| 4 | fault | 1, 5, 4 |
| 2 | fault | 5, 4, 2 |
| 5 | hit | 4, 2, 5 |
| 3 | fault | 2, 5, 3 |

Faults: 4, 1, 2, 3, 1, 5, 4, 2, 3. Count = 9.

### Q8

Answer: C

Optimal, 3 frames.

- 4, 1, 2 fill the frames (3 faults). The later 4 hits.
- At 3, the future uses are: 1 at the upcoming 1, 2 at the upcoming 2, and 4 only at the 4 that follows 5. Replace 4. Frames become 1, 2, 3.
- 2 and 1 hit.
- At 5, 1 never returns, while 2 returns at the later 2 and 3 returns at the final 3. Replace 1. Frames become 2, 3, 5.
- At 4, the next uses are 2 (soon), 5 (soon), and 3 (only at the end). Replace 3. Frames become 2, 5, 4.
- 2 and 5 hit.
- At the final 3, none of 2, 5, or 4 returns. The earliest loaded among them is 2. Replace 2.

Faults: 4, 1, 2, 3, 5, 4, 3. Count = 7.

### Q9

Answer: B

\[
4\ \text{KB} = 2^{12}\ \text{bytes},
\]

so the offset is 12 bits. A 1 KB page would use 10 bits. 20 bits is the page-number field, not the offset.

### Q10

Answer: C

The virtual page number is the rest of the 32-bit address:

\[
32 - 12 = 20\ \text{bits}.
\]

### Q11

Answer: 128

\[
256\ \text{KB} / 2\ \text{KB} = 128\ \text{pages}.
\]

### Q12

Answer: 120

Hit time: \(10 + 100 = 110\) ns. Miss time: \(10 + 100 + 100 = 210\) ns.

\[
0.90 \times 110 + 0.10 \times 210 = 99 + 21 = 120\ \text{ns}.
\]

### Q13

Answer: C

The hit time is still 110 ns. A two-level miss reads two page-table levels and then the data:

\[
10 + 100 + 100 + 100 = 310\ \text{ns}.
\]

\[
0.90 \times 110 + 0.10 \times 310 = 99 + 31 = 130\ \text{ns}.
\]

110 ns ignores misses. 120 ns is the single-level result from Q12. 310 ns is the miss penalty alone.

### Q14

Answer: A, C, D

An inverted table has a slot per frame, because the physical memory, not the virtual space, is what the table is indexed by. Finding a virtual page means searching that frame table, commonly with hashing. Its size follows the frame count. A direct array with one slot per virtual page is the ordinary per-process page table, not the inverted table.

### Q15

Answer: 23

512 bytes is \(2^9\), so the offset is the low 9 bits.

\[
\texttt{0x2F3C} = 12092, \quad 512 \times 23 = 11776, \quad 12092 - 11776 = 316.
\]

The page number is 23. In hex, \(12092 = \texttt{0x2E00} + \texttt{0x13C}\), and \(\texttt{0x2F3C} \gg 9 = 23\).

### Q16

Answer: B

The remainder computed in Q15 is the offset 316. Using an 8-bit offset (as if the page were 256 bytes) yields offset \(0x3C = 60\) and page \(0x2F = 47\). 512 is the page size, which is one past the largest legal offset.

### Q17

Answer: A

FIFO with 3 frames (oldest at the left):

| Reference | Result | Frames |
|---|---|---|
| 1 | fault | 1 |
| 4 | fault | 1, 4 |
| 6 | fault | 1, 4, 6 |
| 5 | fault | 4, 6, 5 |
| 1 | fault | 6, 5, 1 |
| 4 | fault | 5, 1, 4 |
| 3 | fault | 1, 4, 3 |
| 1 | hit | 1, 4, 3 |
| 4 | hit | 1, 4, 3 |
| 6 | fault | 4, 3, 6 |
| 5 | fault | 3, 6, 5 |
| 3 | hit | 3, 6, 5 |

Fault count = 9.

FIFO with 4 frames:

| Reference | Result | Frames |
|---|---|---|
| 1 | fault | 1 |
| 4 | fault | 1, 4 |
| 6 | fault | 1, 4, 6 |
| 5 | fault | 1, 4, 6, 5 |
| 1 | hit | 1, 4, 6, 5 |
| 4 | hit | 1, 4, 6, 5 |
| 3 | fault | 4, 6, 5, 3 |
| 1 | fault | 6, 5, 3, 1 |
| 4 | fault | 5, 3, 1, 4 |
| 6 | fault | 3, 1, 4, 6 |
| 5 | fault | 1, 4, 6, 5 |
| 3 | fault | 4, 6, 5, 3 |

Fault count = 10. The extra frame increased the FIFO fault count. That is Belady's anomaly.

Optimal on this string faults 7 times with 3 frames and 6 times with 4 frames, so Optimal moves in the other direction. LRU faults 10 times with 3 frames and 8 times with 4 frames, and also does not show the anomaly.

### Q18

Answer: A, B, D

A partly used page wastes space inside the page: internal fragmentation. Segments and variable-size partitions are contiguous variable blocks, so freed pieces become holes that may not satisfy the next request: external fragmentation. Classical paging avoids that hole problem by using fixed frames.

### Q19

Answer: C

A 9-bit field stores 0 through 511. The value 512 needs a tenth bit, so it is not an offset of a 512-byte page. The valid/invalid bit says whether the page-table entry names a resident frame. It does not tag a particular legal offset, and a full 9-bit pattern such as 511 is a legal offset (the last byte of the page).

### Q20

Answer: 3

One page is 4 KB, so the process occupies

\[
6 \times 1024 \times 1024 / 4096 = 1536\ \text{pages}.
\]

A page-table page holds \(4096 / 4 = 1024\) entries and therefore describes 1024 virtual pages (4 MB). The 1536 pages need two inner page tables: one full table of 1024 entries and one table for the remaining 512 entries. The outer table is one more page. Pages used for page tables: \(1 + 2 = 3\).

### Q21

Answer: C

\[
3 \times 4096 = 12288\ \text{bytes}.
\]

4096 would be a single page table page. 8192 would be two. 1536 is the number of data pages, not a byte count of the tables.

### Q22

Answer: A, B, C

Q6, Q7, and Q8 count 8 FIFO faults, 9 LRU faults, and 7 Optimal faults on R with 3 frames. LRU's count is higher than FIFO's on this string, so the last claim is false. LRU is often better across a workload; it is not fewer on every individual string.
