# File Systems — Practice Questions

Original practice for GATE CS. These questions are not from any GATE paper. Attempt the questions before reading the solutions.

## Level 1 — Conceptual

## Q1 — MCQ

Contiguous allocation of a file's disk blocks provides

A. direct access to a logical block from the starting block number, and it can suffer external fragmentation
B. immunity to external fragmentation, with no direct access
C. a pointer stored inside every data block as the only way to find the next block
D. an inode that never records a starting block

---

## Q2 — MSQ

**Select all that apply.**

A typical inode (or equivalent file-control block) stores

A. the file length
B. pointers to the file's data blocks
C. owner and permission bits
D. the directory name of the file

---

## Q3 — MCQ

A directory entry's main job is to

A. map a file name to an inode number (or another file identifier)
B. hold every data block of the file
C. replace the free-space bitmap
D. store the file's byte contents in the directory slot itself

---

## Level 2 — Standard GATE Style

## Q4 — NAT

An inode has 6 direct block pointers, 1 single-indirect pointer, and 1 double-indirect pointer. The block size is 512 bytes. A block pointer is 4 bytes. No triple indirect pointer is used. The maximum file size, in bytes, is ____.

---

## Q5 — MCQ

In classical linked allocation, each data block contains a pointer to the next block, and the directory stores the first block. Access to logical block \(k\), counting from 0,

A. follows \(k\) pointers from the start of the file
B. jumps to block \(k\) by adding \(k\) to the start block, as in contiguous allocation
C. reads only the inode's \(k\)-th direct pointer
D. is completed by one random read of a FAT, even though this scheme has no FAT

---

## Q6 — MCQ

A directory contains 40 entries. Each entry is 32 bytes. Disk blocks are 512 bytes. The directory itself is stored in whole blocks. The number of blocks required for the directory is

A. 1
B. 2
C. 3
D. 40

---

## Q7 — MCQ

Indexed allocation, with the index separate from the data blocks,

A. supports direct lookup of block \(k\) through the index, and data blocks need not be physically contiguous
B. requires the data blocks to occupy one contiguous run
C. stores the file name in every index entry
D. cannot represent a file longer than one block

---

## Level 3 — Multi-Step

## Q8 — NAT

A file is stored contiguously and starts at disk block 40. The block size is 1024 bytes. The byte at file offset 10000 (the first byte of the file has offset 0) lies in physical disk block ____.

---

## Q9 — MCQ

The inode is already in memory. The byte to be read is reached only through a double-indirect pointer: the inode points at a double-indirect block, that block points at a single-indirect block, and that block points at the data block. The number of additional disk reads needed to bring that data block into memory is

A. 1
B. 2
C. 3
D. 4

---

## Q10 — MSQ

**Select all that apply.**

A. With a FAT, the link to the next block lives in the table, so a data block can be filled entirely with file data
B. A linked scheme that stores the next-block pointer inside the data block reduces the number of data bytes in that block
C. Contiguous allocation places a next-block pointer in every data block
D. Indexed allocation gathers block pointers into index blocks instead of chaining those pointers through the data blocks

---

## Level 4 — Tricky / Trap-Based

## Q11 — MSQ

**Select all that apply.**

A. Contiguous allocation can suffer external fragmentation
B. Linked allocation can use any free block for the next piece of a file, so it does not need a single contiguous run
C. The last data block of a block-allocated file can be partly empty (internal fragmentation)
D. A directory entry contains the entire byte contents of the file

---

## Q12 — MCQ

A file is created and has link count 1. One extra hard link is created, and one symbolic link is created. The file's link count is then

A. 1
B. 2
C. 3
D. 4

---

## Level 5 — Challenge

## Q13 — NAT

Blocks are 1024 bytes. An inode has 12 direct pointers and one single-indirect pointer. A block pointer is 4 bytes, so an indirect block holds 256 pointers. The double-indirect range is not needed for this offset. File offset 200000 (byte 0 is the start of the file) falls inside a data block reached from that single-indirect pointer. The offset of this byte within its data block is ____.

---

## Q14 — MSQ

**Select all that apply.**

Use the inode layout and the file offset from Q13.

A. Offset 200000 lies in the single-indirect region, beyond the 12 direct blocks
B. The pointer used inside the single-indirect block is the pointer at index 183, counting the first pointer as index 0
C. The byte's offset within its data block is 320
D. Offset 200000 lies in one of the 12 direct blocks

---

## Answer Key

| Q | Type | Answer |
|---|---|---|
| 1 | MCQ | A |
| 2 | MSQ | A, B, C |
| 3 | MCQ | A |
| 4 | NAT | 8457216 |
| 5 | MCQ | A |
| 6 | MCQ | C |
| 7 | MCQ | A |
| 8 | NAT | 49 |
| 9 | MCQ | C |
| 10 | MSQ | A, B, D |
| 11 | MSQ | A, B, C |
| 12 | MCQ | B |
| 13 | NAT | 320 |
| 14 | MSQ | A, B, C |

## Detailed Solutions

### Q1

Answer: A

If a file starts at block \(b\), logical block \(k\) is physical block \(b+k\). That is direct access. The file occupies one run of blocks, so free space broken into holes that are each too small for a new file is external fragmentation. Linked allocation is the scheme that puts a pointer in each data block. The starting block can be recorded in the inode or the directory; contiguity does not forbid recording it.

### Q2

Answer: A, B, C

The inode holds size, ownership, permissions, timestamps, and the block-pointer structure. The file's name lives in a directory entry that points at the inode. Two names can share one inode (hard links), which is why the name is not stored in the inode.

### Q3

Answer: A

The directory maps a name to an identifier, classically an inode number. The data blocks hang off the inode. The free-space bitmap is a separate structure. Putting the file bytes in the directory slot would make the directory the file, which is not how these entries work.

### Q4

Answer: 8457216

Pointers per indirect block:

\[
512 / 4 = 128.
\]

Data blocks addressed:

\[
6 + 128 + 128^2 = 6 + 128 + 16384 = 16518.
\]

Maximum size:

\[
16518 \times 512 = 8457216\ \text{bytes}.
\]

Check: \(16518 \times 512 = 16518 \times (500 + 12) = 8259000 + 198216 = 8457216\).

### Q5

Answer: A

The only locator stored with the file is the first block. Logical block \(k\) is reached by walking \(k\) next-block pointers, so the cost grows with \(k\). Adding \(k\) to a start block is contiguous allocation. A direct pointer in an inode is indexed allocation. A FAT would allow a table lookup, but the scheme in the question has the pointer inside the block and has no FAT.

### Q6

Answer: C

Directory bytes: \(40 \times 32 = 1280\).

\[
1280 / 512 = 2.5,
\]

so the directory occupies 3 blocks. Two blocks hold only 1024 bytes, which is short of 1280. Forty would be one block per entry.

### Q7

Answer: A

The index block (or the inode's pointer array) stores the address of logical block \(k\) in slot \(k\). Those data blocks can sit anywhere on the disk, so the file is not one contiguous run and external fragmentation of a growing contiguous run does not apply. Names stay in directories. Multi-level index pointers exist precisely so that a file can exceed one data block.

### Q8

Answer: 49

Block index of offset 10000:

\[
\lfloor 10000 / 1024 \rfloor = 9, \quad 10000 \bmod 1024 = 784.
\]

The 784 is the offset inside the block. The physical block is

\[
40 + 9 = 49.
\]

### Q9

Answer: C

The inode is cached, so it is not a disk read. The remaining reads are:

1. the double-indirect block,
2. the single-indirect block it names,
3. the data block.

That is 3 disk reads. Counting the inode again would make 4. Stopping after the two index blocks would leave the data block unread.

### Q10

Answer: A, B, D

A FAT entry holds the next-block number, so the on-disk data block does not spend bytes on that pointer. An in-block link does spend those bytes, and the usable payload is smaller than the block size. Contiguous allocation uses a start block and a length; it does not chain pointers through the data. Indexed allocation puts the pointers in the index.

### Q11

Answer: A, B, C

Contiguous files need a run of free blocks and therefore suffer external fragmentation. Linked allocation takes any free block as the successor, so the file's blocks need not form one run. Any scheme that allocates whole blocks can leave the last block partly unused; that leftover is internal fragmentation. The directory entry holds the name and the inode number, not the file's bytes.

### Q12

Answer: B

Creation sets the link count to 1. A hard link is another directory entry for the same inode, so the count becomes 2. A symbolic link is a separate inode whose contents are a path; it does not increment the target's link count. The count stays 2. Counting the symbolic link as a third name of the same inode is the trap.

### Q13

Answer: 320

Twelve direct blocks cover

\[
12 \times 1024 = 12288\ \text{bytes}
\]

(offsets 0 through 12287). Offset 200000 is past that region:

\[
200000 - 12288 = 187712.
\]

The single-indirect region covers the next \(256 \times 1024 = 262144\) bytes, through offset \(12288 + 262144 - 1 = 274431\). Offset 200000 is inside that region. The position within the region splits as

\[
\lfloor 187712 / 1024 \rfloor = 183, \quad 187712 \bmod 1024 = 320,
\]

because \(183 \times 1024 = 187392\) and \(187712 - 187392 = 320\). The byte sits 320 bytes into its data block.

### Q14

Answer: A, B, C

Direct blocks end at offset 12287, so 200000 is not in a direct block. It is in the single-indirect region, at pointer index 183, with offset 320 inside the data block, as computed in Q13. The double-indirect region would begin only at offset 274432.
