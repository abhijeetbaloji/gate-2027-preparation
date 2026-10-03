# File Organization — Practice Questions

Original practice for GATE CS. These questions are not from any GATE paper. Attempt the questions before reading the solutions.

Records do not span blocks. The blocking factor is ⌊block size / record size⌋, and the number of blocks is the number of records divided by that factor, rounded up. When a question gives a search-cost formula, use that formula.

## Level 1 — Conceptual

## Q1 — MCQ

In a heap (unordered) file, a newly inserted record is placed

A. in sorted position according to the primary key, shifting later records if needed
B. in any block that has free record space, commonly the last block
C. in the block whose number equals the hash of the primary key
D. only in a new block, never in a partially filled block

---

## Q2 — MSQ

Which statements about a file sorted on a key K are true? Select all that apply.

A. An equality search on K can use binary search
B. An insertion always rewrites only the last block
C. A range query on K reads a contiguous run of blocks and can stop when K moves past the end of the range
D. Binary search on K examines about half the blocks on every probe

---

## Q3 — MCQ

A static hashed file, with the hash key as the search key, is a good physical design for

A. equality search on the hash key, and a poor one for a range query on that key
B. range query on the hash key, and a poor one for equality search
C. both equality and range search, because each bucket is kept sorted
D. neither, because every search reads every bucket

---

## Level 2 — Standard GATE Style

A sorted file holds 10,000 records. Each record is 128 bytes. Each block is 2,048 bytes. Records do not span blocks. Q4 and Q5 use this file.

## Q4 — NAT

How many blocks does the file occupy? ______

---

## Q5 — NAT

Take the worst-case number of block reads for a binary search to be ⌈log₂ b⌉, where b is the number of blocks. How many block reads is that for this file? ______

---

## Q6 — MCQ

The same records are instead stored as a heap of b blocks. Take the average number of block reads for a successful unique-key search to be ⌈b / 2⌉. What is that average?

A. 10
B. 16
C. 313
D. 625

---

## Level 3 — Multi-Step

## Q7 — NAT

A static hash file has 4,500 records and 150 buckets. The records are spread evenly, exactly 30 in each bucket. Each block holds 20 records. Every bucket is a chain of blocks, with one primary block and as many overflow blocks as the 30 records need. How many blocks does the file use in total? ______

---

## Q8 — MCQ

A query must return every record whose search key lies between two bounds. No index is available, only the file itself. Which organization avoids a full scan?

A. A heap file
B. A file sorted on that search key
C. A static hash file whose hash function is applied to that search key
D. A heap file stored on contiguous blocks

---

## Level 4 — Tricky / Trap-Based

## Q9 — MCQ

Each record is 100 bytes and each block is 512 bytes. Records do not span blocks. The blocking factor is

A. 5
B. 6
C. 4
D. 512

---

## Q10 — MSQ

Which statements are true? Select all that apply.

A. An unsuccessful equality search on a heap file can be forced to read every block
B. Binary search is valid on a heap file when the search key is not the insertion order
C. An equality search in a static hash file with overflow chains reads the chain of one bucket, not the other buckets
D. Inserting into a sorted file is always cheaper, in block writes, than inserting into a heap file

---

## Level 5 — Challenge

## Q11 — NAT

A static hash file must store 5,000 records with at most one block per bucket and no overflow. A block holds 20 records. The load factor must be at most 0.8, so a bucket holds at most 16 records. What is the minimum number of buckets? ______

---

## Q12 — MCQ

A file of 50,000 records, each 200 bytes, is stored in 4,096-byte blocks without spanning. It is sorted on the search key. Using ⌈log₂ b⌉ as the worst-case binary-search cost, how many block reads does a worst-case search take?

A. 12
B. 20
C. 1,250
D. 2,500

---

## Answer Key

| Q | Type | Answer |
|---|------|--------|
| 1 | MCQ | B |
| 2 | MSQ | A, C |
| 3 | MCQ | A |
| 4 | NAT | 625 |
| 5 | NAT | 10 |
| 6 | MCQ | C |
| 7 | NAT | 300 |
| 8 | MCQ | B |
| 9 | MCQ | A |
| 10 | MSQ | A, C |
| 11 | NAT | 313 |
| 12 | MCQ | A |

## Detailed Solutions

### Q1

Answer: B

A heap has no key order to maintain. The file manager writes the record into free space, and the usual free space is the last block, or a newly allocated block when the last block is full. It does not shift records to open a sorted slot, so A is the sorted-file policy. C is static hashing. D wastes space; a partially filled last block is exactly where a heap insert prefers to go.

### Q2

Answer: A, C

Sorted order on K makes binary search correct, and it makes a range a contiguous segment: find the first qualifying key and scan forward until the key passes the upper bound.

B is false. An insertion in the middle of the key order must open a slot. That can shift records through many later blocks, which is why heap insertion is cheaper. D is false. Each binary-search probe halves the remaining span. It does not read half the file at every step. The whole search is about ⌈log₂ b⌉ block reads, which is Q5.

### Q3

Answer: A

The hash function sends equal keys to one bucket, so an equality search reads that bucket and its overflow chain. Consecutive key values are scattered across buckets, so a range query cannot stop after a local scan. It degenerates toward reading every bucket.

B reverses the two workloads. C would require an order-preserving organization; a typical hash does not keep a global key order. D is the cost of a heap scan, not of hashing.

### Q4

Answer: 625

The blocking factor is ⌊2048 / 128⌋ = 16 records per block. The number of blocks is ⌈10000 / 16⌉ = ⌈625⌉ = 625. There is no partially filled extra block, because 10,000 is divisible by 16.

### Q5

Answer: 10

Here b = 625. Because 2^9 = 512 and 2^10 = 1024, log₂ 625 is between 9 and 10. The ceiling is 10. A successful or unsuccessful binary search reads at most 10 blocks under the formula in the question. It does not read 625 blocks, and it does not read 16 blocks merely because that is the blocking factor.

### Q6

Answer: C

The heap still has b = 625 blocks. ⌈625 / 2⌉ = ⌈312.5⌉ = 313.

A is the binary-search cost from Q5, not the heap average. B is the blocking factor. D is a full scan, which is the worst case for a successful heap search and the cost of an unsuccessful one, not the stated average.

### Q7

Answer: 300

Each bucket holds 30 records and each block holds 20, so a bucket needs ⌈30 / 20⌉ = 2 blocks: one primary block and one overflow block. There are 150 buckets, and 150 · 2 = 300 blocks.

Using only the primary blocks gives 150 and ignores overflow. Dividing 4,500 by 20 gives 225 blocks if the file were a packed heap with no empty slots inside buckets. Even distribution still leaves 10 empty record slots in the second block of each bucket, so the hash file uses 300 blocks, not 225.

### Q8

Answer: B

On a file sorted by the search key, the qualifying records occupy a contiguous run. The search finds the first block of that run and reads only through the last. A heap has no such run, whether or not its blocks are contiguous on disk, so A and D still scan the file. A static hash scatters keys that are close in value, so the bounds do not identify a small set of buckets.

### Q9

Answer: A

⌊512 / 100⌋ = 5. Five records occupy 500 bytes, and the remaining 12 bytes cannot hold another 100-byte record when spanning is forbidden.

B rounds 5.12 up to 6. Six records would need 600 bytes and do not fit. C drops a record that does fit. D is the block size, not the number of records.

### Q10

Answer: A, C

If the key is absent, a heap search has no stopping signal short of the last block. In the worst case it reads every block. A hash equality search computes one bucket number and follows only that chain. Other buckets cannot contain the key if the hash function is the one used at insertion.

B is false. Binary search needs the file to be ordered by the search key. Insertion order is a different order, so a heap is not a binary-search structure. D is false. A heap appends a record to free space, often one block write. A sorted file may shift a large suffix of the file. Sorted search is the cheap direction; sorted insertion is the expensive one.

### Q11

Answer: 313

The load-factor cap allows ⌊0.8 · 20⌋ = 16 records in a bucket. At least ⌈5000 / 16⌉ buckets are required. 16 · 312 = 4,992, which is short of 5,000, so 312 buckets are not enough. 16 · 313 = 5,008, which covers 5,000 records. The minimum is 313.

### Q12

Answer: A

The blocking factor is ⌊4096 / 200⌋ = 20. The number of blocks is ⌈50000 / 20⌉ = 2,500. Because 2^11 = 2,048 and 2^12 = 4,096, log₂ 2500 lies strictly between 11 and 12, and the ceiling is 12.

B is the blocking factor. C is half of 2,500, the shape of an average heap search, not a binary search. D is every block, the worst-case heap scan.
