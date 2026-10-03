# Cache Memory Mapping — Practice Questions

Original practice for GATE CS. These questions are not from any GATE paper. Attempt the questions before reading the solutions.

For a byte-addressable cache,

\[
\text{block offset} = \log_2(\text{block size in bytes})
\]

\[
\text{index} = \log_2(\text{number of sets})
\]

\[
\text{tag} = \text{address bits} - \text{index} - \text{block offset}
\]

A direct-mapped cache has one block per set. A fully associative cache has one set. Unless a question says otherwise, the cache starts empty and a 2-way set uses LRU.

## Level 1 — Conceptual

## Q1 — MCQ

In a direct-mapped cache, each memory block maps to

A. exactly one cache line  
B. any line in the cache  
C. any line in a set whose size is chosen at runtime  
D. a TLB entry rather than a cache line

---

## Q2 — NAT

A byte-addressable cache uses 32-byte blocks. How many block-offset bits are required?

---

## Q3 — MCQ

How many index bits does a fully associative cache use?

A. 0  
B. 1  
C. the number of tag bits  
D. the number of offset bits

---

## Q4 — NAT

A 4 KB cache has a 16-byte block. How many blocks does the cache contain? Use \(1\text{ KB} = 2^{10}\) bytes.

---

## Q5 — MCQ

The tag stored with a cache line is used to

A. decide which memory block currently occupies that line  
B. hold the block’s data bytes  
C. replace the block offset during an address calculation  
D. count the number of free page-table entries

---

## Level 2 — Standard GATE Style

## Q6 — NAT

A byte-addressable machine has 32-bit physical addresses. Its direct-mapped cache is 64 KB and its block is 64 bytes. How many tag bits are there? Use \(1\text{ KB} = 2^{10}\) bytes.

---

## Q7 — NAT

The cache in Q6 is rebuilt as 4-way set associative. Capacity, block size, and address length do not change. How many tag bits are there?

---

## Q8 — MCQ

Cache capacity, block size, and physical address length stay fixed. Changing the cache from direct-mapped to 4-way set associative changes the tag width by

A. 0 bits  
B. \(+1\) bit  
C. \(+2\) bits  
D. \(+4\) bits

---

## Q9 — NAT

The same 64 KB cache, 64-byte block, and 32-bit address are organized as fully associative. How many tag bits are there?

---

## Q10 — MSQ

A byte-addressable machine has 16-bit addresses. The cache is direct-mapped, holds 128 bytes, and uses an 8-byte block. Select all that apply.

A. The block offset is 3 bits.  
B. The index is 4 bits.  
C. The tag is 9 bits.  
D. Two addresses that differ only in the tag can map to the same line.

---

## Q11 — NAT

A word-addressable machine uses 20-bit word addresses. Its direct-mapped cache holds 256 words, with 4 words in each block. How many tag bits are there?

---

## Level 3 — Multi-Step

## Q12 — NAT

A direct-mapped cache has 8 lines and a block size of one word. Word-block references arrive in this order:

\[
0,\ 4,\ 8,\ 0,\ 4,\ 8,\ 12,\ 4
\]

The line is the block number modulo 8. How many references are hits?

---

## Q13 — NAT

A 2-way set-associative cache has 4 sets, one-word blocks, and LRU replacement. Block references arrive in this order:

\[
2,\ 6,\ 2,\ 10,\ 2,\ 6
\]

The set is the block number modulo 4. How many references are hits?

---

## Q14 — MCQ

One set of a 2-way LRU cache currently holds blocks 4 and 12. Block 12 was used more recently than block 4. The next reference is block 4, and the reference after that is block 20. Both 4 and 20 map to this set. Which block does the reference to 20 replace?

A. block 4  
B. block 12  
C. block 20  
D. either resident block, chosen at random

---

## Q15 — NAT

A direct-mapped cache has a 32-bit byte address, a capacity of 32 KB, and a 32-byte block. Each line stores its tag and one valid bit. There is no dirty bit. How many metadata bits does the cache store? Use \(1\text{ KB} = 2^{10}\) bytes. Do not count data bits.

---

## Q16 — MSQ

Select all that apply.

A. A write-back cache needs a dirty bit for each block.  
B. Direct-mapped replacement does not consult an LRU stack.  
C. In a 4-way cache, an address has exactly four candidate lines, all in one set.  
D. Raising associativity from 1 to 4, with capacity and block size fixed, increases the number of index bits.

---

## Level 4 — Tricky / Trap-Based

## Q17 — NAT

A direct-mapped cache has 4 lines and a block size of 2 words. Word addresses arrive in this order:

\[
0,\ 1,\ 2,\ 3,\ 4,\ 1,\ 8,\ 9
\]

The block number is \(\lfloor \text{word} / 2 \rfloor\), and the line is the block number modulo 4. A miss loads the whole two-word block. How many references are hits?

---

## Q18 — NAT

A byte-addressable machine has 36-bit physical addresses. An 8-way set-associative cache is 16 KB and uses 64-byte blocks. How many tag bits does each line store? Use \(1\text{ KB} = 2^{10}\) bytes.

---

## Q19 — NAT

A byte-addressable machine has 32-bit addresses and a direct-mapped cache of 8 KB with 32-byte blocks. The byte address \(0\text{x00001F80}\) maps to which cache line number? Number the lines from 0. Use \(1\text{ KB} = 2^{10}\) bytes.

---

## Level 5 — Challenge

## Q20 — NAT

A direct-mapped cache has 4 one-word lines. The reference string

\[
1,\ 2,\ 5,\ 2
\]

is repeated three times, for 12 references in all. The line is the block number modulo 4. How many references are hits?

---

## Q21 — NAT

A 2-way set-associative cache is byte-addressable, with 32-bit addresses, an 8 KB capacity, and 64-byte blocks. Each line stores a tag, a valid bit, and a dirty bit. Each set stores one LRU bit. How many metadata bits are stored in total? Do not count data bits. Use \(1\text{ KB} = 2^{10}\) bytes.

---

## Q22 — NAT

A 2-way LRU cache has 2 sets and one-word blocks. References are

\[
0,\ 1,\ 2,\ 3,\ 0,\ 1,\ 4,\ 0
\]

The set index is the block number modulo 2. Every reference costs 1 cycle of hit time. Each miss costs 9 additional cycles. There is no overlap between references. Using

\[
\text{total cycles} = (\text{references}) \times 1 + (\text{misses}) \times 9
\]

what is the total number of cycles?

## Answer Key

| Q | Type | Answer |
|---|------|--------|
| 1 | MCQ | A |
| 2 | NAT | 5 |
| 3 | MCQ | A |
| 4 | NAT | 256 |
| 5 | MCQ | A |
| 6 | NAT | 16 |
| 7 | NAT | 18 |
| 8 | MCQ | C |
| 9 | NAT | 26 |
| 10 | MSQ | A, B, C, D |
| 11 | NAT | 12 |
| 12 | NAT | 1 |
| 13 | NAT | 2 |
| 14 | MCQ | B |
| 15 | NAT | 18432 |
| 16 | MSQ | A, B, C |
| 17 | NAT | 4 |
| 18 | NAT | 25 |
| 19 | NAT | 252 |
| 20 | NAT | 5 |
| 21 | NAT | 2880 |
| 22 | NAT | 53 |

## Detailed Solutions

### Q1

Answer: A

Direct mapping assigns each block to one line by using the index bits. Fully associative placement can use any line. A set-associative cache can use any line inside one fixed set, but the set size is part of the design, not a runtime choice.

### Q2

Answer: 5

\[
\log_2 32 = 5
\]

### Q3

Answer: A

A fully associative cache has a single set. There is no index field; the address splits into tag and block offset only.

### Q4

Answer: 256

\[
\frac{4 \times 2^{10}}{16} = \frac{4096}{16} = 256
\]

### Q5

Answer: A

The index selects the line or set. The tag distinguishes which of the many memory blocks that share that index is actually present. Data live in the data array, and the offset selects a byte inside the block.

### Q6

Answer: 16

\[
\text{offset} = \log_2 64 = 6
\]

\[
\text{blocks} = \frac{64 \times 2^{10}}{64} = 1024, \quad \text{index} = \log_2 1024 = 10
\]

\[
\text{tag} = 32 - 10 - 6 = 16
\]

### Q7

Answer: 18

The 1024 blocks are grouped into \(1024 / 4 = 256\) sets.

\[
\text{index} = \log_2 256 = 8
\]

\[
\text{tag} = 32 - 8 - 6 = 18
\]

### Q8

Answer: C

Four-way associativity divides the number of sets by 4, so the index loses \(\log_2 4 = 2\) bits. Those two bits join the tag. The offset is unchanged because the block size is unchanged. The tag therefore grows by 2.

### Q9

Answer: 26

A fully associative organization has no index.

\[
\text{tag} = 32 - \log_2 64 = 32 - 6 = 26
\]

There are 1024 tags to compare, but each tag is 26 bits.

### Q10

Answer: A, B, C, D

\[
\text{offset} = \log_2 8 = 3
\]

\[
\text{lines} = 128 / 8 = 16, \quad \text{index} = \log_2 16 = 4
\]

\[
\text{tag} = 16 - 4 - 3 = 9
\]

Addresses with the same index and offset, but different tags, compete for one line, so D is true. The block is 8 bytes, not 16, so E is false.

### Q11

Answer: 12

The address already names words, so the offset counts words inside a block.

\[
\text{offset} = \log_2 4 = 2
\]

\[
\text{blocks} = 256 / 4 = 64, \quad \text{index} = \log_2 64 = 6
\]

\[
\text{tag} = 20 - 6 - 2 = 12
\]

### Q12

Answer: 1

| Reference | Line = block mod 8 | Result | Line contents |
|---|---|---|---|
| 0 | 0 | miss | line 0 = 0 |
| 4 | 4 | miss | line 4 = 4 |
| 8 | 0 | miss | line 0 = 8 |
| 0 | 0 | miss | line 0 = 0 |
| 4 | 4 | hit | line 4 = 4 |
| 8 | 0 | miss | line 0 = 8 |
| 12 | 4 | miss | line 4 = 12 |
| 4 | 4 | miss | line 4 = 4 |

Only the fifth reference hits. Hits = 1.

### Q13

Answer: 2

Every listed block has residue 2 modulo 4, so all of them use set 2. LRU order is shown with the most recently used block on the right.

| Reference | Result | Set 2 after the reference |
|---|---|---|
| 2 | miss | [2] |
| 6 | miss | [2, 6] |
| 2 | hit | [6, 2] |
| 10 | miss, replaces 6 | [2, 10] |
| 2 | hit | [10, 2] |
| 6 | miss, replaces 10 | [2, 6] |

Hits = 2.

### Q14

Answer: B

The hit on block 4 makes 4 most recently used and leaves 12 least recently used. The miss on block 20 therefore replaces 12. LRU does not choose at random, and the incoming block is not already resident.

### Q15

Answer: 18432

\[
\text{offset} = \log_2 32 = 5
\]

\[
\text{blocks} = \frac{32 \times 2^{10}}{32} = 1024, \quad \text{index} = 10
\]

\[
\text{tag} = 32 - 10 - 5 = 17
\]

Each line stores 17 tag bits and 1 valid bit.

\[
1024 \times (17 + 1) = 1024 \times 18 = 18432
\]

### Q16

Answer: A, B, C

Write-back must know whether a replaced block has been modified. Direct mapping has only one legal line, so LRU is unnecessary. A 4-way set gives four candidates. Increasing associativity from 1 to 4 reduces the number of sets and therefore reduces, rather than increases, the index width. A fully associative cache has an empty index. D is false.

### Q17

Answer: 4

| Word | Block | Line | Result |
|---|---|---|---|
| 0 | 0 | 0 | miss, loads words 0 and 1 |
| 1 | 0 | 0 | hit |
| 2 | 1 | 1 | miss, loads words 2 and 3 |
| 3 | 1 | 1 | hit |
| 4 | 2 | 2 | miss |
| 1 | 0 | 0 | hit; block 0 is still present |
| 8 | 4 | 0 | miss, replaces block 0 and loads words 8 and 9 |
| 9 | 4 | 0 | hit |

Hits = 4.

### Q18

Answer: 25

\[
\text{offset} = \log_2 64 = 6
\]

\[
\text{blocks} = \frac{16 \times 2^{10}}{64} = 256
\]

\[
\text{sets} = 256 / 8 = 32, \quad \text{index} = \log_2 32 = 5
\]

\[
\text{tag} = 36 - 5 - 6 = 25
\]

### Q19

Answer: 252

\[
\text{lines} = \frac{8 \times 2^{10}}{32} = 256
\]

The line number of a direct-mapped cache is

\[
\left\lfloor \frac{\text{address}}{\text{block size}} \right\rfloor \bmod (\text{number of lines})
\]

\[
0\text{x1F80} = 8064
\]

\[
\left\lfloor \frac{8064}{32} \right\rfloor \bmod 256 = 252 \bmod 256 = 252
\]

The field split gives the same line: offset 5, index 8, and the index bits of \(0\text{x1F80}\) are \(11111100_2 = 252\).

### Q20

Answer: 5

Lines are block modulo 4. The trace is:

| Step | Block | Line | Result |
|---|---|---|---|
| 1 | 1 | 1 | miss |
| 2 | 2 | 2 | miss |
| 3 | 5 | 1 | miss, replaces 1 |
| 4 | 2 | 2 | hit |
| 5 | 1 | 1 | miss, replaces 5 |
| 6 | 2 | 2 | hit |
| 7 | 5 | 1 | miss, replaces 1 |
| 8 | 2 | 2 | hit |
| 9 | 1 | 1 | miss, replaces 5 |
| 10 | 2 | 2 | hit |
| 11 | 5 | 1 | miss, replaces 1 |
| 12 | 2 | 2 | hit |

Block 2 stays in line 2 for the whole string. Blocks 1 and 5 alternately displace each other in line 1. Hits = 5.

### Q21

Answer: 2880

\[
\text{offset} = \log_2 64 = 6
\]

\[
\text{blocks} = \frac{8 \times 2^{10}}{64} = 128
\]

\[
\text{sets} = 128 / 2 = 64, \quad \text{index} = 6
\]

\[
\text{tag} = 32 - 6 - 6 = 20
\]

One line stores \(20 + 1 + 1 = 22\) metadata bits. A set stores two lines and one LRU bit:

\[
2 \times 22 + 1 = 45
\]

\[
64 \times 45 = 2880
\]

### Q22

Answer: 53

Set 0 receives the even blocks and set 1 receives the odd blocks. LRU order has the most recently used block on the right.

Set 0:

| Block | Result | Set after reference |
|---|---|---|
| 0 | miss | [0] |
| 2 | miss | [0, 2] |
| 0 | hit | [2, 0] |
| 4 | miss, replaces 2 | [0, 4] |
| 0 | hit | [4, 0] |

Set 1:

| Block | Result | Set after reference |
|---|---|---|
| 1 | miss | [1] |
| 3 | miss | [1, 3] |
| 1 | hit | [3, 1] |

The eight references produce 3 hits and \(8 - 3 = 5\) misses.

\[
8 \times 1 + 5 \times 9 = 8 + 45 = 53
\]
