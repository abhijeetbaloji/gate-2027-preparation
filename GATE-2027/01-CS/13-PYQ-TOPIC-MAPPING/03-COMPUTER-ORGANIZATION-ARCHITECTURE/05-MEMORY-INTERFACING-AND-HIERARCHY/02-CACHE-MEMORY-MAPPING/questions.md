# GATE PYQs

## 2026

### Q.38

**Paper:** GATE 2026 CS-1 (forenoon)

**Question:**

The size of the physical address space of a processor is 2^{32} bytes. The capacity of a
cache memory unit is  2^{23} bytes. The cache block size is 128 bytes. The cache
memory unit can be built as a direct mapped cache or as a  𝐾-way set-associative
cache, where 𝐾= 2^{𝐿} and 𝐿∈{1, 2, 3}.  Let the length of the TAG field be 𝑀 bits
for the direct mapped cache, and 𝑁 bits for the set-associative cache.
Which one of the following options is true?

**Options:**

A. 𝑁= 𝑀+ 𝐿
B. 𝑁= 𝑀−𝐿
C. 𝑁= 𝑀+ 𝐾
D. 𝑁= 𝑀−𝐾

**Type:** MCQ

**Answer:** VERIFICATION REQUIRED

**Source:** GATE 2026 CS-1 (forenoon), `12-PYQ/2026/set-01/question-paper.pdf`

---

### Q.52

**Paper:** GATE 2026 CS-2 (afternoon)

**Question:**

Consider a system with a processor and a 4 KB direct mapped cache with block size
of 16 bytes. The system has a 16 MB physical memory. Four words P, Q, R, and S
are accessed by the processor in the same order 10 times. That is, there are a total
of 40 memory references in the sequence P, Q, R, S, P, Q, R, S,…
Assume that the cache memory is initially empty. The physical addresses of the
words are given below (1 word =1 byte).
P: 0x845B32, Q: 0x845B26, R: 0x845B36, S: 0x846B32
Which of the following statements is/are true?
Note: 1K=2^{10} and 1M=2^{20}

**Options:**

A. Every access to P results in a cache miss
B. Every access to R results in a cache hit
C. Every access to Q results in a cache miss
D. Except the first access to S, all subsequent accesses to S result in cache hits

**Type:** MCQ

**Answer:** VERIFICATION REQUIRED

**Source:** GATE 2026 CS-2 (afternoon), `12-PYQ/2026/set-02/question-paper.pdf`

---

### Q.53

**Paper:** GATE 2026 CS-2 (afternoon)

**Question:**

To keep track of free blocks in a file system, one of the two approaches is generally
used – using bitmaps (bit vectors) or using linked lists. Consider that the linked list
approach is used to keep track of free blocks in a file system. Assume that the disk
size is 16 GB, block size is 2 KB, and block numbers used are 32-bit long. A single
pointer of size 4 bytes is used in each block of the list to point to the next block of
the list. The number of blocks required to hold the free disk block numbers is
____________. (answer in integer)
Note: 1K=2^{10} and 1G=2^{30}

**Options:**

The paper does not print options for this numerical-answer question.

**Type:** NAT

**Answer:** VERIFICATION REQUIRED

**Source:** GATE 2026 CS-2 (afternoon), `12-PYQ/2026/set-02/question-paper.pdf`

---

### Q.56

**Paper:** GATE 2026 CS-2 (afternoon)

**Question:**

Consider a system with 1 MB physical memory and a word length of 1 byte. The
system uses a direct mapped cache, with block numbers starting from 0. The word
with physical address 0xA2C28 is mapped to the cache block number 176_{10}. The
maximum possible size of the cache (in KB) for this configuration is ___________.
(answer in integer)
Note: 1K=2^{10} and 1M=2^{20}

**Options:**

The paper does not print options for this numerical-answer question.

**Type:** NAT

**Answer:** VERIFICATION REQUIRED

**Source:** GATE 2026 CS-2 (afternoon), `12-PYQ/2026/set-02/question-paper.pdf`

---

## 2025

### Q.36

**Paper:** GATE 2025 CS-1

**Question:**

Consider a memory system with 1M bytes of main memory and 16K bytes of cache
memory. Assume that the processor generates 20-bit memory address, and the cache
block size is 16 bytes. If the cache uses direct mapping, how many bits will be
required to store all the tag values? [Assume memory is byte addressable, 1K=2^{10},
1M=2^{20}.]

**Options:**

A. 6 × 2^{10}
B. 8 × 2^{10}
C. 2^{12}
D. 2^{14}

**Type:** MCQ

**Answer:** VERIFICATION REQUIRED

**Source:** GATE 2025 CS-1, `12-PYQ/2025/set-01/question-paper.pdf`

---

### Q.53

**Paper:** GATE 2025 CS-1

**Question:**

A computer has a memory hierarchy consisting of two-level cache (L1 and L2) and
a main memory. If the processor needs to access data from memory, it first looks
into L1 cache. If the data is not found in L1 cache, it goes to L2 cache. If it fails to
get the data from L2 cache, it goes to main memory, where the data is definitely
available.  Hit rates  and  access times of various memory units are shown in the
figure. The average memory access time in nanoseconds (ns) is ________. (rounded
off to two decimal places)

**Options:**

The paper does not print options for this numerical-answer question.

**Type:** NAT

**Answer:** VERIFICATION REQUIRED

**Source:** GATE 2025 CS-1, `12-PYQ/2025/set-01/question-paper.pdf`

---

### Q.28

**Paper:** GATE 2025 CS-2

**Question:**

Which of the following is/are part of an Instruction Set Architecture of a processor?

**Options:**

A. The size of the cache memory
B. The clock frequency of the processor
C. The number of cache memory levels
D. The total number of registers

**Type:** MCQ

**Answer:** VERIFICATION REQUIRED

**Source:** GATE 2025 CS-2, `12-PYQ/2025/set-02/question-paper.pdf`

---

### Q.39

**Paper:** GATE 2025 CS-2

**Question:**

For a direct-mapped cache, 4 bits are used for the tag field and 12 bits are used to
index into a cache block. The size of each cache block is one byte. Assume that
there is no other information stored for each cache block.
Which ONE of the following is the CORRECT option for the sizes of the main
memory and the cache memory in this system (byte addressable), respectively?

**Options:**

A. 64 KB and 4 KB
B. 128 KB and 16 KB
C. 64 KB and 8 KB
D. 128 KB and 6 KB

**Type:** MCQ

**Answer:** VERIFICATION REQUIRED

**Source:** GATE 2025 CS-2, `12-PYQ/2025/set-02/question-paper.pdf`

---

## 2024

### Q.16

**Paper:** GATE 2024 CS1

**Question:**

A user starts browsing a webpage hosted at a remote server. The browser opens a
single TCP connection to fetch the entire webpage from the server. The webpage
consists of a top-level index page with multiple embedded image objects. Assume
that all caches (e.g., DNS cache, browser cache) are all initially empty. The
following packets leave the user’s computer in some order.
(i)  HTTP GET request for the index page
(ii)  DNS request to resolve the web server’s name to its IP address
(iii)  HTTP GET request for an image object
(iv)  TCP SYN to open a connection to the web server
Which one of the following is the CORRECT chronological order (earliest in time
to latest) of the packets leaving the computer ?

**Options:**

A. (iv), (ii), (iii), (i)
B. (ii), (iv), (iii), (i)
C. (ii), (iv), (i), (iii)
D. (iv), (ii), (i), (iii)

**Type:** MCQ

**Answer:** VERIFICATION REQUIRED

**Source:** GATE 2024 CS1, `12-PYQ/2024/set-01/question-paper.pdf`

---

### Q.53

**Paper:** GATE 2024 CS1

**Question:**

Consider two set-associative cache memory architectures:  WBC, which uses the
write back policy, and WTC, which uses the write through policy. Both of them use
the LRU (Least Recently Used) block replacement policy. The cache memory is
connected to the main memory. Which of the following statements is/are TRUE?

**Options:**

A. A read miss in WBC never evicts a dirty block A read miss in WTC never triggers a write back operation of a cache block to
B. main memory
C. A write hit in WBC can modify the value of the dirty bit of a cache block A write miss in WTC always writes the victim cache block to main memory
D. before loading the missed block to the cache

**Type:** MCQ

**Answer:** VERIFICATION REQUIRED

**Source:** GATE 2024 CS1, `12-PYQ/2024/set-01/question-paper.pdf`

---

## 2023

### Q.52

**Paper:** GATE 2023 CS

**Question:**

Suppose in a web browser, you click on the www.gate-2023.in URL. The browser
cache is empty. The IP address for this URL is not cached in your local host, so
a DNS lookup is triggered (by the local DNS server deployed on your local host)
over the 3-tier DNS hierarchy in an iterative mode. No resource records are cached
anywhere across all DNS servers.
Let RTT denote the round trip time between your local host and DNS servers
in the DNS hierarchy. The round trip time between the local host and the web
server hosting www.gate-2023.in is also equal to RTT. The HTML file associated
with the URL is small enough to have negligible transmission time and negligible
rendering time by your web browser, which references 10 equally small objects on
the same web server.
Which of the following statements is/are CORRECT about the minimum elapsed
time between clicking on the URL and your browser fully rendering it?

**Options:**

A. 7 RTTs, in case of non-persistent HTTP with 5 parallel TCP connections.
B. 5 RTTs, in case of persistent HTTP with pipelining.
C. 9 RTTs, in case of non-persistent HTTP with 5 parallel TCP connections.
D. 6 RTTs, in case of persistent HTTP with pipelining.

**Type:** MCQ

**Answer:** VERIFICATION REQUIRED

**Source:** GATE 2023 CS, `12-PYQ/2023/question-paper.pdf`

---

### Q.62

**Paper:** GATE 2023 CS

**Question:**

Consider a database of fixed-length records, stored as an ordered file. The database
has 25,000 records, with each record being 100 bytes, of which the primary key
occupies 15 bytes. The data file is block-aligned in that each data record is fully
contained within a block. The database is indexed by a primary index file, which
is also stored as a block-aligned ordered file. The figure below depicts this indexing
scheme.
Data File
Primary Key  Other Fields
(15 Bytes)  (85 Bytes)
Index File
Block Anchor Block
Primary Key Pointer
Suppose the block size of the file system is 1024 bytes, and a pointer to a block
occupies 5 bytes. The system uses binary search on the index file to search for a
record with a given key. You may assume that a binary search on an index file of
b blocks takes ⌈log_{2} b⌉ block accesses in the worst case.
Given a key, the number of block accesses required to identify the block in the data
file that may contain a record with the key, in the worst case, is  .

**Options:**

The paper does not print options for this numerical-answer question.

**Type:** NAT

**Answer:** VERIFICATION REQUIRED

**Source:** GATE 2023 CS, `12-PYQ/2023/question-paper.pdf`

---

### Q.64

**Paper:** GATE 2023 CS

**Question:**

An 8-way set associative cache of size 64 KB (1 KB = 1024 bytes) is used in a
system with 32-bit address. The address is sub-divided into TAG, INDEX, and
BLOCK OFFSET.
The number of bits in the TAG is  .

**Options:**

The paper does not print options for this numerical-answer question.

**Type:** NAT

**Answer:** VERIFICATION REQUIRED

**Source:** GATE 2023 CS, `12-PYQ/2023/question-paper.pdf`

---

## 2022

### Q.24

**Paper:** GATE 2022 CS

**Question:**

Let WB and WT be two set associative cache organizations that use LRU algorithm
for cache block replacement. WB is a write back cache and WT is a write through
cache. Which of the following statements is/are FALSE?

**Options:**

A. Each cache block in WB and WT has a dirty bit.
B. Every write hit in WB leads to a data transfer from cache to main memory.
C. Eviction of a block from WT will not lead to data transfer from cache to main memory.
D. A read miss in WB will never lead to eviction of a dirty block from WB.

**Type:** MCQ

**Answer:** VERIFICATION REQUIRED

**Source:** GATE 2022 CS, `12-PYQ/2022/question-paper.pdf`

---

### Q.33

**Paper:** GATE 2022 CS

**Question:**

A cache memory that has a hit rate of 0.8 has an access latency 10 ns and miss
penalty 100 ns. An optimization is done on the cache to reduce the miss rate.
However, the optimization results in an increase of cache access latency to 15 ns,
whereas the miss penalty is not affected. The minimum hit rate (rounded off to two
decimal places) needed after the optimization such that it should not increase the
average memory access time is _____________.

**Options:**

The paper does not print options for this numerical-answer question.

**Type:** NAT

**Answer:** VERIFICATION REQUIRED

**Source:** GATE 2022 CS, `12-PYQ/2022/question-paper.pdf`

---

### Q.35

**Paper:** GATE 2022 CS

**Question:**

Consider the resolution of the domain name www.gate.org.in by a DNS
resolver. Assume that no resource records are cached anywhere across the DNS
servers and that iterative query mechanism is used in the resolution. The number
of DNS query-response pairs involved in completely resolving the domain name
is_____________.

**Options:**

The paper does not print options for this numerical-answer question.

**Type:** NAT

**Answer:** VERIFICATION REQUIRED

**Source:** GATE 2022 CS, `12-PYQ/2022/question-paper.pdf`

---

### Q.54

**Paper:** GATE 2022 CS

**Question:**

Consider a system with 2 KB direct mapped data cache with a block size of 64 bytes.
The system has a physical address space of 64 KB and a word length of 16 bits.
During the execution of a program, four data words P, Q, R, and S are accessed in
that order 10 times (i.e., PQRSPQRS…). Hence, there are 40 accesses to data cache
altogether. Assume that the data cache is initially empty and no other data words are
accessed by the program. The addresses of the first bytes of P, Q, R, and S are
0xA248, 0xC28A, 0xCA8A, and 0xA262, respectively. For the execution of the
above program, which of the following statements is/are TRUE with respect to the
data cache?

**Options:**

A. Every access to S is a hit.
B. Once P is brought to the cache it is never evicted.
C. At the end of the execution only R and S reside in the cache.
D. Every access to R evicts Q from the cache.

**Type:** MCQ

**Answer:** VERIFICATION REQUIRED

**Source:** GATE 2022 CS, `12-PYQ/2022/question-paper.pdf`

---

## 2021

### Q.22

**Paper:** GATE 2021 CS Set-1

**Question:**

Consider a computer system with a byte-addressable primary memory of size
232 bytes. Assume the computer system has a direct-mapped cache of size 32 KB
(1 KB = 21º bytes), and each cache block is of size 64 bytes.
The size of the tag field is — bits.

**Options:**

The paper does not print options for this numerical-answer question.

**Type:** NAT

**Answer:** VERIFICATION REQUIRED

**Source:** GATE 2021 CS Set-1, `12-PYQ/2021/set-01/question-paper.pdf`

---

### Q.18

**Paper:** GATE 2021 CS Set-2

**Question:**

If r and y are two decimal digits and (0.1101)2 = (0.8ry5)10, the decimal value of
x +y is
9.19 Consider a set-associative cache of size 2KB (1KB = 21° bytes) with cache block
size of 64 bytes. Assume that the cache is byte-addressable and a 32-bit address is
used for accessing the cache. If the width of the tag field is 22 bits, the associativity
of the cache is
GATE Graduate Aptitude Test in Engineering 2021
2021 Organising Institute - IIT Bombay

**Options:**

The paper does not print options for this numerical-answer question.

**Type:** NAT

**Answer:** VERIFICATION REQUIRED

**Source:** GATE 2021 CS Set-2, `12-PYQ/2021/set-02/question-paper.pdf`

---

## 2020

### Q.21

**Paper:** GATE 2020 CS

**Question:**

A direct mapped cache memory of 1 MB has a block size of 256 bytes. The cache
has an access time of 3 ns and a hit rate of 94%. During a cache miss, it takes
20 ns to bring the first word of a block from the main memory, while each
subsequent word takes 5 ns. The word size is 64 bits. The average memory access
time in ns (round off to 1 decimal place) is

**Options:**

The paper does not print options for this numerical-answer question.

**Type:** NAT

**Answer:** VERIFICATION REQUIRED

**Source:** GATE 2020 CS, `12-PYQ/2020/question-paper.pdf`

---

### Q.24

**Paper:** GATE 2020 CS

**Question:**

Consider the following grammar.
S → aSB|d
B →b
The number of reduction steps taken by a bottom-up parser while accepting the
string aaadbbb is
Assume that you have made a request for a web page through your web browser
to a web server. Initially the browser cache is empty. Further, the browser is
configured to send HTTP requests in non-persistent mode. The web page contains
text and five very small images. The minimum number of TCP connections
required to display the web page completely in your browser is
Q26 - Q55 carry two marks each.

**Options:**

The paper does not print options for this numerical-answer question.

**Type:** NAT

**Answer:** VERIFICATION REQUIRED

**Source:** GATE 2020 CS, `12-PYQ/2020/question-paper.pdf`

---

### Q.30

**Paper:** GATE 2020 CS

**Question:**

A computer system with a word length of 32 bits has a 16 MB byte-addressable
main memory and a 64 KB, 4-way set associative cache memory with a block size
of 256 bytes. Consider the following four physical addresses represented in
hexadecimal notation.
A1 = 0x42C8A4, A2 =0x546888, A3 = 0x6A289C, A4 = 0x5E4880
Which one of the following is TRUE?

**Options:**

A. Al and A4 are mapped to different cache sets.
B. A2 and A3 are mapped to the same cache set. () A3 and A4 are mapped to the same cache set.
D. Al and A3 are mapped to the same cache set.

**Type:** MCQ

**Answer:** VERIFICATION REQUIRED

**Source:** GATE 2020 CS, `12-PYQ/2020/question-paper.pdf`

---

## 2019

### Q.1

**Paper:** GATE 2019 CS (printed header Set-2)

**Question:**

A certain processor uses a fully associative cache of size 16 kB. The cache block size is 16
bytes. Assume that the main memory is byte addressable and uses a 32-bit address. How
many bits are required for the Tag and the Index fields respectively in the addresses generated
by the processor?

**Options:**

A. 24 bits and 0 bits
B. 28 bits and 4 bits
C. 24 bits and 4 bits
D. 28 bits and 0 bits

**Type:** MCQ

**Answer:** VERIFICATION REQUIRED

**Source:** GATE 2019 CS (printed header Set-2), `12-PYQ/2019/question-paper.pdf`

---

### Q.42

**Paper:** GATE 2019 CS (printed header Set-2)

**Question:**

The index node (inode) of a Unix-like file system has 12 direct, one single-indirect and one
double-indirect pointers. The disk block size is 4 kB, and the disk block address is 32-bits
long. The maximum possible file size is (rounded off to 1 decimal place)
cS 10/15

**Options:**

The paper does not print options for this numerical-answer question.

**Type:** NAT

**Answer:** VERIFICATION REQUIRED

**Source:** GATE 2019 CS (printed header Set-2), `12-PYQ/2019/question-paper.pdf`

---

### Q.45

**Paper:** GATE 2019 CS (printed header Set-2)

**Question:**

A certain processor deploys a single-level cache. The cache block size is 8 words and the
word size is 4 bytes. The memory system uses a 60-MHz clock. To service a cache miss, the
memory controller first takes 1 cycle to accept the starting address of the block, it then takes
3 cycles to fetch all the eight words of the block, and finally transmits the words of the
requested block at the rate of 1 word per cycle. The maximum bandwidth for the memory
system when the program running on the processor issues a series of read operations is
x 106 bytes/sec.

**Options:**

The paper does not print options for this numerical-answer question.

**Type:** NAT

**Answer:** VERIFICATION REQUIRED

**Source:** GATE 2019 CS (printed header Set-2), `12-PYQ/2019/question-paper.pdf`

---

## 2018

### Q.34

**Paper:** GATE 2018 CS

**Question:**

The size of the physical address space of a processor is  2^{𝑃} bytes. The word length is
2^{𝑊} bytes. The capacity of cache memory is  2^{𝑁} bytes. The size of each cache block is
2^{𝑀} words. For a 𝐾-way set-associative cache memory, the length (in number of bits) of the
tag field is

**Options:**

A. 𝑃−𝑁− log_{2} 𝐾
B. 𝑃−𝑁+ log_{2} 𝐾
C. 𝑃−𝑁−𝑀−𝑊− log_{2} 𝐾
D. 𝑃−𝑁−𝑀−𝑊+ log_{2} 𝐾

**Type:** MCQ

**Answer:** VERIFICATION REQUIRED

**Source:** GATE 2018 CS, `12-PYQ/2018/question-paper.pdf`

---

## 2017

### Q.29

**Paper:** GATE 2017 CS Session 2

**Question:**

Correct: 2 Wrong:-0.66
In a two-level cache system, the access times of L1 and Lz caches are 1 and 8 clock cycles.
respectively. The miss penalty from the Lz cache to main memory is 18 clock cycles. The miss rate
of Ly cache is twice that of Lz. The average memory access time (AMAT) of this cache system is 2
cycles. The miss rates of Ly and Lz respectively are:

**Options:**

A. 0.111 and 0.056
B. 0.056 and 0.111
C. 0.0892 and 0.1784
D. 0.1784 and 0.0892

**Type:** MCQ

**Answer:** VERIFICATION REQUIRED

**Source:** GATE 2017 CS Session 2, `12-PYQ/2017/set-02/question-paper.pdf`

---

### Q.45

**Paper:** GATE 2017 CS Session 2

**Question:**

Correct: 2 Wrong : 0
The read access times and the hit ratios for different caches in a memory hierarchy are as given
below.
Cache Read access time Hit ratio
(in nanoseconds)
I-cache 2 0.8
D-cache 2 0.9
L2-cache 8 0.9
The read access time of main memory is 90 nanoseconds. Assume that the caches use the referred-
word-first read policy and the write back policy. Assume that all the caches are direct mapped
caches. Assume that the dirty bit is always 0 for all the blocks in the caches. In execution of a
program, 60% of memory reads are for instruction fetch and 40% are for memory operand fetch.
The average read access time in nanoseconds (up to 2 decımal places) 1s

**Options:**

The paper does not print options for this numerical-answer question.

**Type:** NAT

**Answer:** VERIFICATION REQUIRED

**Source:** GATE 2017 CS Session 2, `12-PYQ/2017/set-02/question-paper.pdf`

---

### Q.49

**Paper:** GATE 2017 CS Session 2

**Question:**

Correct: 2 Wrong : 0
In a Bt tree, if the search-key value is 8 bytes long. the block size is 512 bytes and the block
pointer size is 2 bytes, then the maximum order of the B+ tree is

**Options:**

The paper does not print options for this numerical-answer question.

**Type:** NAT

**Answer:** VERIFICATION REQUIRED

**Source:** GATE 2017 CS Session 2, `12-PYQ/2017/set-02/question-paper.pdf`

---

### Q.53

**Paper:** GATE 2017 CS Session 2

**Question:**

Correct: 2 Wrong : 0
Consider a machine with a byte addressable main memory of 232 bytes divided into blocks of size
32 bytes. Assume that a direct mapped cache having 512 cache lines is used with this machine. The
size of the tag field in bits is

**Options:**

The paper does not print options for this numerical-answer question.

**Type:** NAT

**Answer:** VERIFICATION REQUIRED

**Source:** GATE 2017 CS Session 2, `12-PYQ/2017/set-02/question-paper.pdf`

---

## 2016

### Q.32

**Paper:** GATE 2016 CS-2

**Question:**

The width of the physical address on a machine is 40 bits. The width of the tag field in a 512
KB 8-way set associative cache is  bits.
CS(Set B)  8/18

**Options:**

The paper does not print options for this numerical-answer question.

**Type:** NAT

**Answer:** VERIFICATION REQUIRED

**Source:** GATE 2016 CS-2, `12-PYQ/2016/set-02/question-paper.pdf`

---

### Q.50

**Paper:** GATE 2016 CS-2

**Question:**

A file system uses an in-memory cache to cache disk blocks. The miss rate of the cache is
shown in the figure. The latency to read a block from the cache is 1 ms and to read a block
from the disk is 10 ms. Assume that the cost of checking whether a block exists in the cache
is negligible. Available cache sizes are in multiples of 10 MB.
90
80
70
Miss rate (%) 60
50
40
30
20
10
0
0 10 20 30 40 50 60 70 80 90
Cache size (MB)
The smallest cache size required to ensure an average read latency of less than 6 ms is
MB.

**Options:**

The paper does not print options for this numerical-answer question.

**Type:** NAT

**Answer:** VERIFICATION REQUIRED

**Source:** GATE 2016 CS-2, `12-PYQ/2016/set-02/question-paper.pdf`

---

## 2015

### Q.18

**Paper:** GATE 2015 CS, 7 February Shift 2

**Question:**

Assume that for a certain processor, a read request takes 50 nanoseconds on a cache miss and 5
nanoseconds on a cache hit. Suppose while running a program, it was observed that 80% of the
processor's read requests result in a cache hit. The average read access time in nanoseconds is
Correct Answer :

**Options:**

The paper does not print options for this numerical-answer question.

**Type:** NAT

**Answer:** VERIFICATION REQUIRED

**Source:** GATE 2015 CS, 7 February Shift 2, `12-PYQ/2015/set-02/question-paper.pdf`

---

### Q.34

**Paper:** GATE 2015 CS, 8 February Shift 1

**Question:**

28

Consıder a machine with a byte addressable main memory of 2° bytes, block size of 16 bytes and a
direct mapped cache having 2" cache lines. Let the addresses of two consecutive bytes in main
memory be (E201F)16 and (E2020)16. What are the tag and cache line address (in hex) for main
memory address (E201F)16?

**Options:**

A. E, 201
B. F, 201
C. E, E20
D. 2, 01F

**Type:** MCQ

**Answer:** VERIFICATION REQUIRED

**Source:** GATE 2015 CS, 8 February Shift 1, `12-PYQ/2015/set-03/question-paper.pdf`

---

### Q.39

**Paper:** GATE 2015 CS, 8 February Shift 1

**Question:**

4.

Consider a B+ tree in which the search key is 12 bytes long, block size is 1024 bytes, record pointer
is 10 bytes long and block pointer is 8 bytes long. The maximum number of keys that can be
accommodated in each non-leaf node of the tree is
Correct Answer :

**Options:**

The paper does not print options for this numerical-answer question.

**Type:** NAT

**Answer:** VERIFICATION REQUIRED

**Source:** GATE 2015 CS, 8 February Shift 1, `12-PYQ/2015/set-03/question-paper.pdf`

---

## 2014

### Q.44

**Paper:** GATE 2014 CS SET-1

**Question:**

An aaccess sequennce of cache bblock addressees is of lengthh N and contaains n uniquee block addressses.
The nnumber of unnique block adddresses betwween two conssecutive accesses to the saame block adddress
is boounded abovee by k. What is the miss raatio if the acccess sequencee is passed thhrough a cachhe of
assocciativity A ≥ kk exercising lleast-recentlyy-used replaceement policy??

**Options:**

A. nn/N
B. 1/NN
C. 1/A
D. k/n CS01 (GATE 2014)

**Type:** MCQ

**Answer:** VERIFICATION REQUIRED

**Source:** GATE 2014 CS SET-1, `12-PYQ/2014/set-01/question-paper.pdf`

---

### Q.9

**Paper:** GATE 2014 CS SET-2

**Question:**

A 4-way set-associative cache memory unit with a capacity of 16 KB is built using a block size of 8
words. The word length is 32 bits. The size of the physical address space is 4 GB. The number of
bits for the TAG field is _____

**Options:**

The paper does not print options for this numerical-answer question.

**Type:** NAT

**Answer:** VERIFICATION REQUIRED

**Source:** GATE 2014 CS SET-2, `12-PYQ/2014/set-02/question-paper.pdf`

---

### Q.20

**Paper:** GATE 2014 CS SET-2

**Question:**

A FAT (file allocation table) based file system is being used and the total overhead of each entry in
the FAT is 4 bytes in size. Given a 100 x 10^{6}  bytes disk on which the file system is stored and data
block size is 10^{3} bytes, the maximum size of a file that can be stored on this disk in units of 10^{6}
bytes is ____________.

**Options:**

The paper does not print options for this numerical-answer question.

**Type:** NAT

**Answer:** VERIFICATION REQUIRED

**Source:** GATE 2014 CS SET-2, `12-PYQ/2014/set-02/question-paper.pdf`

---

### Q.30

**Paper:** GATE 2014 CS SET-2

**Question:**

Consider a join (relation algebra) between relations r(R)and s(S) using the nested loop method.
There are 3 buffers each of size equal to disk block size, out of which one buffer is reserved for
intermediate results. Assuming size(r(R))<size(s(S)), the join will have fewer number of
disk block accesses if

**Options:**

A. relation r(R) is in the outer loop.
B. relation s(S) is in the outer loop.
C. join selection factor between r(R) and s(S) is more than 0.5. CS02 (GATE 2014)
D. join selection factor between r(R) and s(S) is less than 0.5.

**Type:** MCQ

**Answer:** VERIFICATION REQUIRED

**Source:** GATE 2014 CS SET-2, `12-PYQ/2014/set-02/question-paper.pdf`

---

### Q.43

**Paper:** GATE 2014 CS SET-2

**Question:**

In designing a computer’s cache system, the cache block (or cache line) size is an important
parameter.  Which one of the following statements is correct in this context?

**Options:**

A. A smaller block size implies better spatial locality
B. A smaller block size implies a smaller cache tag and hence lower cache tag overhead
C. A smaller block size implies a larger cache tag and hence lower cache hit time
D. A smaller block size incurs a lower cache miss penalty

**Type:** MCQ

**Answer:** VERIFICATION REQUIRED

**Source:** GATE 2014 CS SET-2, `12-PYQ/2014/set-02/question-paper.pdf`

---

### Q.44

**Paper:** GATE 2014 CS SET-3

**Question:**

The memory access time is 1 nanosecond for a read operation with a hit in cache, 5 nanoseconds
for a read operation with a miss in cache, 2 nanoseconds for a write operation with a hit in cache
and 10 nanoseconds for a write operation with a miss in cache. Execution of a sequence of
instructions involves 100 instruction fetch operations, 60 memory operand read operations and 40
memory operand write operations. The cache hit-ratio is 0.9.  The average memory access time (in
nanoseconds) in executing the sequence of instructions is  __________.

**Options:**

The paper does not print options for this numerical-answer question.

**Type:** NAT

**Answer:** VERIFICATION REQUIRED

**Source:** GATE 2014 CS SET-3, `12-PYQ/2014/set-03/question-paper.pdf`

---

## 2013

### Q.20

**Paper:** GATE 2013 CS Booklet A

**Question:**

In a k-way set associative cache, the cache is divided into v sets, each of which consists of k lines.
The lines of a set are placed in sequence one after another. The lines in set s are sequenced before
the lines in set (s+1). The main memory blocks are numbered 0 onwards. The main memory block
numbered j must be mapped to any one of the cache lines from

**Options:**

A. (j mod v) * k to (j mod v) * k + (k-1)
B. (j mod v) to (j mod v) + (k-1)
C. (j mod k) to (j mod k) + (v-1)
D. (j mod k) * v to (j mod k) * v + (v-1)

**Type:** MCQ

**Answer:** VERIFICATION REQUIRED

**Source:** GATE 2013 CS Booklet A, `12-PYQ/2013/set-01/question-paper.pdf`

---

### Q.53

**Paper:** GATE 2013 CS Booklet A

**Question:**

What is the minimum number of page colours needed to guarantee that no two synonyms map to
different sets in the processor cache of this computer?

**Options:**

A. 2
B. 4
C. 8
D. 16 Statement for Linked Answer Questions 54 and 55: Relation R has eight attributes ABCDEFGH. Fields of R contain only atomic values. F={CH→G, A→BC, B→CFH, E→A, F→EG} is a set of functional dependencies (FDs) so that F^{+} is exactly the set of FDs that hold for R.

**Type:** MCQ

**Answer:** VERIFICATION REQUIRED

**Source:** GATE 2013 CS Booklet A, `12-PYQ/2013/set-01/question-paper.pdf`

---

### Q.6

**Paper:** GATE 2013 CS Booklet B

**Question:**

In a k-way set associative cache, the cache is divided into v sets, each of which consists of k lines.
The lines of a set are placed in sequence one after another. The lines in set s are sequenced before
the lines in set (s+1). The main memory blocks are numbered 0 onwards. The main memory block
numbered j must be mapped to any one of the cache lines from

**Options:**

A. (j mod v) * k to (j mod v) * k + (k-1)
B. (j mod v) to (j mod v) + (k-1)
C. (j mod k) to (j mod k) + (v-1)
D. (j mod k) * v to (j mod k) * v + (v-1)

**Type:** MCQ

**Answer:** VERIFICATION REQUIRED

**Source:** GATE 2013 CS Booklet B, `12-PYQ/2013/set-02/question-paper.pdf`

---

### Q.55

**Paper:** GATE 2013 CS Booklet B

**Question:**

What is the minimum number of page colours needed to guarantee that no two synonyms map to
different sets in the processor cache of this computer?

**Options:**

A. 2
B. 4
C. 8
D. 16 CS-B 12/20 2013COMPUTER SCIENCE & INFORMATION TECH. - CS General Aptitude (GA) Questions

**Type:** MCQ

**Answer:** VERIFICATION REQUIRED

**Source:** GATE 2013 CS Booklet B, `12-PYQ/2013/set-02/question-paper.pdf`

---

### Q.18

**Paper:** GATE 2013 CS Booklet C

**Question:**

In a k-way set associative cache, the cache is divided into v sets, each of which consists of k lines.
The lines of a set are placed in sequence one after another. The lines in set s are sequenced before
the lines in set (s+1). The main memory blocks are numbered 0 onwards. The main memory block
numbered j must be mapped to any one of the cache lines from

**Options:**

A. (j mod v) * k to (j mod v) * k + (k-1)
B. (j mod v) to (j mod v) + (k-1)
C. (j mod k) to (j mod k) + (v-1)
D. (j mod k) * v to (j mod k) * v + (v-1)

**Type:** MCQ

**Answer:** VERIFICATION REQUIRED

**Source:** GATE 2013 CS Booklet C, `12-PYQ/2013/set-03/question-paper.pdf`

---

### Q.53

**Paper:** GATE 2013 CS Booklet C

**Question:**

What is the minimum number of page colours needed to guarantee that no two synonyms map to
different sets in the processor cache of this computer?

**Options:**

A. 2
B. 4
C. 8
D. 16 Statement for Linked Answer Questions 54 and 55: Relation R has eight attributes ABCDEFGH. Fields of R contain only atomic values. F={CH→G, A→BC, B→CFH, E→A, F→EG} is a set of functional dependencies (FDs) so that F^{+} is exactly the set of FDs that hold for R.

**Type:** MCQ

**Answer:** VERIFICATION REQUIRED

**Source:** GATE 2013 CS Booklet C, `12-PYQ/2013/set-03/question-paper.pdf`

---

### Q.8

**Paper:** GATE 2013 CS Booklet D

**Question:**

In a k-way set associative cache, the cache is divided into v sets, each of which consists of k lines.
The lines of a set are placed in sequence one after another. The lines in set s are sequenced before
the lines in set (s+1). The main memory blocks are numbered 0 onwards. The main memory block
numbered j must be mapped to any one of the cache lines from

**Options:**

A. (j mod v) * k to (j mod v) * k + (k-1)
B. (j mod v) to (j mod v) + (k-1)
C. (j mod k) to (j mod k) + (v-1)
D. (j mod k) * v to (j mod k) * v + (v-1)

**Type:** MCQ

**Answer:** VERIFICATION REQUIRED

**Source:** GATE 2013 CS Booklet D, `12-PYQ/2013/set-04/question-paper.pdf`

---

### Q.55

**Paper:** GATE 2013 CS Booklet D

**Question:**

What is the minimum number of page colours needed to guarantee that no two synonyms map to
different sets in the processor cache of this computer?

**Options:**

A. 2
B. 4
C. 8
D. 16 CS- D 12/20 2013COMPUTER SCIENCE & INFORMATION TECH. - CS General Aptitude (GA) Questions

**Type:** MCQ

**Answer:** VERIFICATION REQUIRED

**Source:** GATE 2013 CS Booklet D, `12-PYQ/2013/set-04/question-paper.pdf`

---

## 2012

### Q.53

**Paper:** GATE 2012 CS Booklet A

**Question:**

The appropriate entries for E1, E2, and E3 are

**Options:**

A. E1: S  aAbB, A  S
B. E1: S  aAbB, S   E2: S  bAaB, B  S E2: S  bAaB, S   E3: B  S E3: S  
C. E1: S  aAbB, S  
D. E1: A  S, S   E2: S  bAaB, S   E2: B  S, S   E3: B  S E3: B  S Statement for Linked Answer Questions 54 and 55: A computer has a 256 KByte, 4-way set associative, write back data cache with block size of 32 Bytes. The processor sends 32 bit addresses to the cache controller. Each cache tag directory entry contains, in addition to address tag, 2 valid bits, 1 modified bit and 1 replacement bit.

**Type:** MCQ

**Answer:** VERIFICATION REQUIRED

**Source:** GATE 2012 CS Booklet A, `12-PYQ/2012/question-paper.pdf`

---

### Q.54

**Paper:** GATE 2012 CS Booklet A

**Question:**

The number of bits in the tag field of an address is

**Options:**

A. 11
B. 14
C. 16
D. 27

**Type:** MCQ

**Answer:** VERIFICATION REQUIRED

**Source:** GATE 2012 CS Booklet A, `12-PYQ/2012/question-paper.pdf`

---

### Q.55

**Paper:** GATE 2012 CS Booklet A

**Question:**

The size of the cache tag directory is

**Options:**

A. 160 Kbits
B. 136 Kbits
C. 40 Kbits
D. 32 Kbits CS-A 15/20 2012 COMPUTER SCIENCE & INFORMATION TECH. – CS General Aptitude (GA) Questions

**Type:** MCQ

**Answer:** VERIFICATION REQUIRED

**Source:** GATE 2012 CS Booklet A, `12-PYQ/2012/question-paper.pdf`

---

## 2010

### Q.47

**Paper:** GATE 2010 CS

**Question:**

Suppose computers A and B have IP addresses 10.105.L.113 and 10.105.1.91 respeclively and they
should belong to the same nerwork? both use the same netmask N. Which of the valucs of N given below should not be used if A and B

**Options:**

A. 255.255.255.0
B. 255.255.255.128
C. 255.255.255.192
D. 255.255.255.224 11/24 2010 Common Data Questions Common Dala for Questions 48 and 49: A compuler syslem has an LI cache, an L2 cache. and a main memory unit connected as shown below: The block size in LI cache is 4 words. The block size in 1.2 cache is 16 words. The memory access times are 2 nanoseconds. 20 nanoseconds and 200 nanoscconds for LI cache..L2 cache and main memory unis respectively. Data Bus 1.2 Dala Bus Main Cache LI Cache Memory 4 words 4 words

**Type:** MCQ

**Answer:** VERIFICATION REQUIRED

**Source:** GATE 2010 CS, `12-PYQ/2010/question-paper.pdf`

---

### Q.48

**Paper:** GATE 2010 CS

**Question:**

When there is a miss in L1 cache and a hit in 1.2 cache, a block is transferred from L2 cache to
LI cache. What is the time taken for this transfur?

**Options:**

A. 2 nanoseconds
B. 20 nanoseconds
C. 22 nanoseconds
D. 88 nanoseconds

**Type:** MCQ

**Answer:** VERIFICATION REQUIRED

**Source:** GATE 2010 CS, `12-PYQ/2010/question-paper.pdf`

---

### Q.49

**Paper:** GATE 2010 CS

**Question:**

When there is a miss in both LI cache and L2 cachc. first a block is transferred fromn main inemory
10 12 cache, and then a block is transferred from L2 cache to LI cache. What is the lola) time taken
for ilsese transfers?

**Options:**

A. 222 nanoseconds
B. 888 nanoseconds
C. 902 nanoseconds (1)) 968 nanoseconds Common Data for Questions 50 and 51: onsider a complete undirected graph with vertex set (0.1.2.3,4). Entry W. in the matrix W below is the reight of the edge (iil 01814} 0 12 4 9 w= 8 12 0 7 3 (49 3 20) 7 0

**Type:** MCQ

**Answer:** VERIFICATION REQUIRED

**Source:** GATE 2010 CS, `12-PYQ/2010/question-paper.pdf`

---

## 2009

### Q.29

**Paper:** GATE 2009 CS

**Question:**

Consider a 4-way set associative cache (initially empty) with total 16 cache blocks. The main
memory consists of 256 blocks and the request for memory blocks is in the following order :
0, 255, 1, 4, 3, 8, 133, 159, 216, 129, 63, 8, 48, 32, 73, 92, 155.
Which one of the following memory block will NOT be in cache if LRU replacement policy is used ?

**Options:**

A. 3
B. 8
C. 129
D. 216

**Type:** MCQ

**Answer:** VERIFICATION REQUIRED

**Source:** GATE 2009 CS, `12-PYQ/2009/question-paper.pdf`

---

## 2008

### Q.35

**Paper:** GATE 2008 CS

**Question:**

For inclusion to hold between two cache levels L1 and L2 in a multi-level cache hierarchy, which
of the following are necessary?
I. L1 must be a write-through cache
II. L2 must be a write-through cache
III. The associativity of L2 must be greater than that of L1
IV. The L2 cache must be at least as large as the L1 cache

**Options:**

A. IV only
B. 1 and IV only
C. 1, III and IV only
D. I, II, III and IV 6/24 2008 MAIN PAPER-CS

**Type:** MCQ

**Answer:** VERIFICATION REQUIRED

**Source:** GATE 2008 CS, `12-PYQ/2008/question-paper.pdf`

---

### Q.70

**Paper:** GATE 2008 CS

**Question:**

Consider a file of 16384 records. Each record is 32 bytes long and its key field is of size 6 bytes.
The file is ordered on a non-key field, and the file organization is unspanned. The file is stored in a
file system with block size 1024 bytes, and the size of a block pointer is 10 bytes. If the secondary
index is built on the key field of the file, and a multi-level index scheme is used to store the
secondary index, the number of first-level and second-level blocks in the multi-level index are
respectively

**Options:**

A. 8 and 0
B. 128 and 6
C. 256 and 4
D. 512 and 5 2008 Common Data Questions MAIN PAPER - CS Common Data for Questions 71,72 and 73: Consider a machine with a 2-way set associative data cache of size 64 Kbytes and block size 16 bytes. The cache is managed using 32 bit virtual addresses and the page size is 4 Kbytes. A program to be run on this machine begins as follows: double ARR [1024] [1024]; int i, ji /* Initialize array ARR to 0.0 */ for (i = 0; i < 1024; i++) for (j = 0; j < 1024; j++) ARR [i] [j] = 0.0; The size of double is 8Bytes. Array ARR is located in memory starting at the beginning of virtual page OxFF000 and stored in row major order. The cache is initially empty and no pre-fetching is done. The only data memory references made by the program are those to array ARR.

**Type:** MCQ

**Answer:** VERIFICATION REQUIRED

**Source:** GATE 2008 CS, `12-PYQ/2008/question-paper.pdf`

---

### Q.71

**Paper:** GATE 2008 CS

**Question:**

The total size of the tags in the cache directory is

**Options:**

A. 32 Kbits
B. 34 Kbits
C. 64 Kbits
D. 68 Kbits

**Type:** MCQ

**Answer:** VERIFICATION REQUIRED

**Source:** GATE 2008 CS, `12-PYQ/2008/question-paper.pdf`

---

### Q.72

**Paper:** GATE 2008 CS

**Question:**

Which of the following array elements has the same cache index as ARR [O] [O]?

**Options:**

A. ARR [0] [4]
B. ARR [4] [0]
C. ARR [0] [5]
D. ARR [5] [0]

**Type:** MCQ

**Answer:** VERIFICATION REQUIRED

**Source:** GATE 2008 CS, `12-PYQ/2008/question-paper.pdf`

---

### Q.73

**Paper:** GATE 2008 CS

**Question:**

The cache hit ratio for this initialization loop is

**Options:**

A. 0%
B. 25%
C. 50%
D. 75% 15/24 2008 MAIN PAPER -CS Common Data for Questions 74 and 75: Consider the following C functions: int f1 ( int n ) if (n == 0 || n == 1) return n; else return (2*f1(n-1) + 3*f1(n-2)); int f2 ( int n ) int i; int X[N], Y[N]. Z[N); X[0] = [0]=2[]=; x[1] = 1; Y[1] = 2; Z[1] = 3; for (i = 2; i <= n; i++){| X[i] = Y[i-1] + Z[i-2];| Y[i] = 2 * X[i]; Z[i] = 3 * X[i]; } return X[n]; }

**Type:** MCQ

**Answer:** VERIFICATION REQUIRED

**Source:** GATE 2008 CS, `12-PYQ/2008/question-paper.pdf`

---

## 2007

### Q.10

**Paper:** GATE 2007 CS

**Question:**

Consider a 4-way set associative cache consisting of 128 lines with a line size of 64
words. The CPU generates a 20-bit address of a word in main memory. The number
of bits in the TAG, LINE and WORD fields are respectively:

**Options:**

A. 9, 6, 5
B. 7,7,6
C. 7,5, 8
D. 9,5, 6

**Type:** MCQ

**Answer:** VERIFICATION REQUIRED

**Source:** GATE 2007 CS, `12-PYQ/2007/question-paper.pdf`

---

### Q.63

**Paper:** GATE 2007 CS

**Question:**

The order of a leaf node in a B'-tree is the maximum number of (value, data record
pointer) pairs it can hold. Given that the block size is 1K bytes, data record pointer is
7 bytes long, the value field is 9 bytes long and a block pointer is 6 bytes long, what
is the order of the leaf node?

**Options:**

A. 63
B. 64 67
D. 68

**Type:** MCQ

**Answer:** VERIFICATION REQUIRED

**Source:** GATE 2007 CS, `12-PYQ/2007/question-paper.pdf`

---

### Q.79

**Paper:** GATE 2007 CS

**Question:**

For the correct answer string to Q.78, how many derivation trees are there?

**Options:**

A. 1
B. 2
C. 3
D. 4 Statement for Linked Answer Questions 80 & 81: Consider a machine with a byte addressable main memory of 2'° bytes. Assume that a direct mapped data cache consisting of 32 lines of 64 bytes each is used in the system. A 50 x 50 two-dimensional array of bytes is stored in the main memory starting from memory location 1100H. Assume that the data cache is initially empty. The complete array is accessed twice. Assume that the contents of the data cache do not change in between the two accesses.

**Type:** MCQ

**Answer:** VERIFICATION REQUIRED

**Source:** GATE 2007 CS, `12-PYQ/2007/question-paper.pdf`

---

### Q.80

**Paper:** GATE 2007 CS

**Question:**

How many data cache misses will occur in total?

**Options:**

A. 48
B. 50
C. 56
D. 59

**Type:** MCQ

**Answer:** VERIFICATION REQUIRED

**Source:** GATE 2007 CS, `12-PYQ/2007/question-paper.pdf`

---

### Q.81

**Paper:** GATE 2007 CS

**Question:**

Which of the following lines of the data cache will be replaced by new blocks in
accessing the array for the second time?

**Options:**

A. line 4 to line 11
B. line 4 to line 12
C. line 0 to line 7
D. line 0 to line 8 Statement for Linked Answer Questions 82 & 83: A process has been allocated 3 page frames. Assume that none of the pages of the process are available in the memory initially. The process makes the following sequence of page references (reference string): 1, 2, 1, 3, 7, 4, 5, 6, 3, 1

**Type:** MCQ

**Answer:** VERIFICATION REQUIRED

**Source:** GATE 2007 CS, `12-PYQ/2007/question-paper.pdf`

---
