# Binary Heaps — Practice Questions

Original practice for GATE CS. These questions are not from any GATE paper. Attempt the questions before reading the solutions.

Unless a question says otherwise, heap positions are numbered from 1. For the node at index `i`, the parent is at `floor(i / 2)`, the left child is at `2i`, and the right child is at `2i + 1`. A min-heap stores the smaller key in the parent: the key at `i` is less than or equal to the keys at its children. A max-heap stores the larger key in the parent.

The array layout is the level order of a complete binary tree. Bottom-up build-heap starts at index `floor(n / 2)` and heapifies downward through index 1. An insertion places the new key at the next complete-tree position and sifts it upward. Extract-min on a min-heap removes index 1, moves the last key into index 1, shortens the heap by one, and heapifies index 1 downward.

## Level 1 — Conceptual

## Q1 — MCQ

The 1-based min-heap array, written without the unused index 0, is `2, 5, 3, 9, 6, 8`. Is this a min-heap?

A. Yes.

B. No, because 5 is greater than 3.

C. No, because 9 is greater than 6.

D. No, because the last key has no parent.

---

## Q2 — NAT

In a 1-based heap, the parent of the node at index 7 is at index ____.

---

## Q3 — NAT

A heap contains 10 keys. Its height, measured in edges, is ____.

---

## Q4 — MCQ

Which statement describes extract-min on a non-empty min-heap?

A. Delete the last leaf and leave the root unchanged.

B. Save the root, move the last key into the root, remove that last position, and heapify the root downward.

C. Sort the whole array and then delete index 1.

D. Swap the root with its right child and stop.

---

## Level 2 — Standard GATE Style

## Q5 — NAT

The min-heap contents are `2, 5, 3, 9, 6, 8`. The key 1 is inserted. After the upward sift, the key at index 3 is ____.

---

## Q6 — MCQ

Keys are inserted, in this order, into an empty min-heap: 5, 3, 8, 1. The resulting 1-based contents are

A. 1, 3, 8, 5

B. 1, 5, 8, 3

C. 1, 3, 5, 8

D. 5, 3, 8, 1

---

## Q7 — NAT

Bottom-up build-heap turns the 1-based array `3, 8, 5, 1, 9, 4` into a max-heap. The sum of the first two keys removed by extract-max is ____.

---

## Q8 — NAT

A heap contains 11 nodes. How many of them are leaves?

---

## Q9 — MCQ

In a 1-based heap, the children of the node at index 3 are at indices

A. 6 and 7

B. 4 and 5

C. 5 and 6

D. 3 and 4

---

## Level 3 — Multi-Step

## Q10 — MCQ

Bottom-up build-heap turns `9, 4, 7, 1, 2, 3, 6` into a min-heap. The resulting contents are

A. 1, 2, 3, 4, 9, 7, 6

B. 1, 2, 3, 9, 4, 7, 6

C. 1, 4, 3, 9, 2, 7, 6

D. 9, 4, 7, 1, 2, 3, 6

---

## Q11 — NAT

One extract-min is performed on the min-heap produced in Q10. The key then stored at index 2 is ____.

---

## Q12 — MCQ

The 1-based min-heap contents are `1, 3, 6, 14, 8, 11, 9`. The first three keys removed by extract-min are

A. 1, 3, 6

B. 1, 6, 3

C. 1, 3, 8

D. 9, 8, 6

---

## Q13 — MCQ

Repeated extract-min is applied to a min-heap until the heap is empty. Which statement is correct?

A. The extracted keys come out in non-decreasing order.

B. The extracted keys come out in the original level-order of the heap.

C. The extracted keys come out in non-increasing order.

D. Only the first extraction is the minimum; later extractions do not preserve heap order.

---

## Level 4 — Tricky / Trap-Based

## Q14 — MCQ

Using 1-based indexing, the left child of the node at index 5 is at index

A. 10

B. 11

C. 9

D. 6

---

## Q15 — MSQ

Keys 4, 2, 6, 1, 3 are inserted into an empty BST in that order. The resulting tree has the shape of a complete binary tree. Select all that apply.

A. The tree is a BST.

B. The tree is a min-heap.

C. The tree is a max-heap.

D. The tree is a complete binary tree.

---

## Q16 — MCQ

Bottom-up build-heap is applied to the 1-based array `5, 3, 8, 1, 2` to produce a min-heap. The resulting contents are

A. 1, 2, 8, 3, 5

B. 1, 2, 8, 5, 3

C. 1, 3, 2, 5, 8

D. 5, 3, 8, 1, 2

---

## Level 5 — Challenge

## Q17 — NAT

An empty min-heap receives insert 8, insert 4, insert 6, insert 1, insert 5, extract-min, insert 3, extract-min, in that order. The key then stored at index 2 is ____.

---

## Q18 — NAT

Start with the min-heap in Q12 and perform three extract-min operations. The key then stored at index 2 is ____.

## Answer Key

| Q | Type | Answer |
|---|------|--------|
| 1 | MCQ | (A) |
| 2 | NAT | 3 |
| 3 | NAT | 3 |
| 4 | MCQ | (B) |
| 5 | NAT | 2 |
| 6 | MCQ | (A) |
| 7 | NAT | 17 |
| 8 | NAT | 6 |
| 9 | MCQ | (A) |
| 10 | MCQ | (A) |
| 11 | NAT | 4 |
| 12 | MCQ | (A) |
| 13 | MCQ | (A) |
| 14 | MCQ | (A) |
| 15 | MSQ | (A), (D) |
| 16 | MCQ | (A) |
| 17 | NAT | 5 |
| 18 | NAT | 9 |

## Detailed Solutions

### Q1

Answer: (A)

Check every parent against its own children. Index 1 holds 2, and its children are 5 and 3; both are at least 2. Index 2 holds 5, and its children are 9 and 6; both are at least 5. Index 3 holds 3, and its only child in this six-key heap is 8, which is at least 3. The array is a min-heap. The keys 5 and 3 are siblings, not a parent and a child, so `5 > 3` does not violate the heap property.

### Q2

Answer: 3

The parent index is `floor(7 / 2) = 3`. The children of index 3 are `2*3 = 6` and `2*3 + 1 = 7`, which confirms that 7 is the right child of 3.

### Q3

Answer: 3

A heap is a complete binary tree. Its height is `floor(log2 n)`. For `n = 10`, `2^3 = 8 <= 10` and `2^4 = 16 > 10`, so the height is 3 edges. The last level is not full, but the longest root-to-leaf path still has three edges.

### Q4

Answer: (B)

Extract-min returns the root, which is the smallest key. The last position is the one that disappears so that the tree stays complete. Its key is moved to the root and then sifted down by swapping with the smaller child until the heap property holds. Deleting the last leaf without moving it would remove an arbitrary key. Sorting the array is a different procedure from one heap extraction.

### Q5

Answer: 2

The new key is placed at index 7. Its parent, index 3, holds 3, which is greater than 1, so they swap. Index 3 now holds 1 and index 7 holds 3. The parent of index 3 is index 1, which holds 2, and `2 > 1`, so they swap. The array is `1, 5, 2, 9, 6, 8, 3`. Index 3 holds 2.

### Q6

Answer: (A)

- Insert 5: `5`
- Insert 3: 3 sifts above 5, giving `3, 5`
- Insert 8: 8 stays at index 3, giving `3, 5, 8`
- Insert 1: 1 swaps with index 2, giving `3, 1, 8, 5`, then swaps with index 1, giving `1, 3, 8, 5`

The result is 1, 3, 8, 5.

### Q7

Answer: 17

The array is `3, 8, 5, 1, 9, 4`, with `n = 6`. Heapify downward from index 3.

Index 3 holds 5, and its child at index 6 holds 4. Since 5 is larger, the max-heap property already holds there.

Index 2 holds 8. Its children are 1 and 9. The larger child is 9, so 8 and 9 swap. The array is `3, 9, 5, 1, 8, 4`. Index 5 is a leaf.

Index 1 holds 3. Its children are 9 and 5. Swap 3 with 9: `9, 3, 5, 1, 8, 4`. At index 2, the children are 1 and 8, so 3 swaps with 8: `9, 8, 5, 1, 3, 4`.

The first extract-max returns 9 and moves 4 to the root. Sifting `4, 8, 5, 1, 3` swaps 4 with 8 and then stops, because 4 is at least its new children 1 and 3. The heap is `8, 4, 5, 1, 3`. The second extract-max returns 8. The sum is `9 + 8 = 17`.

### Q8

Answer: 6

In a 1-based heap of `n` nodes, the leaves occupy indices `floor(n / 2) + 1` through `n`. For `n = 11`, those indices are 6 through 11, which is 6 leaves. The same count is `ceil(n / 2) = 6`.

### Q9

Answer: (A)

The left child is `2 * 3 = 6`, and the right child is `7`. Indices 4 and 5 are the children of index 2. The 0-based child formula `2i + 1` and `2i + 2` is a different numbering and is not the formula used here.

### Q10

Answer: (A)

The array is `9, 4, 7, 1, 2, 3, 6`. Heapify from index `floor(7 / 2) = 3` down to 1.

Index 3 holds 7. Its children are 3 and 6, so 7 swaps with 3. The array is `9, 4, 3, 1, 2, 7, 6`.

Index 2 holds 4. Its children are 1 and 2, so 4 swaps with 1. The array is `9, 1, 3, 4, 2, 7, 6`.

Index 1 holds 9. Its children are 1 and 3, so 9 swaps with 1. The array is `1, 9, 3, 4, 2, 7, 6`. Index 2 must be sifted again: its children are 4 and 2, so 9 swaps with 2. The array is `1, 2, 3, 4, 9, 7, 6`. Index 5 is a leaf.

The built heap is 1, 2, 3, 4, 9, 7, 6. Option (B) is what successive insertion of the same keys produces. Build-heap and insertion can both be correct heaps without being the same array. This question asks for the bottom-up procedure.

### Q11

Answer: 4

Extract-min removes 1 and moves the last key, 6, to the root. The remaining keys before the downward sift are `6, 2, 3, 4, 9, 7`.

Index 1 holds 6. Its smaller child is 2, at index 2, so they swap: `2, 6, 3, 4, 9, 7`. Index 2 holds 6, and its smaller child is 4, at index 4, so they swap: `2, 4, 3, 6, 9, 7`. Index 4 is now a leaf. The key at index 2 is 4.

### Q12

Answer: (A)

Bottom-up heapify is not needed; the given array is already the heap. Its root is 1.

Extract 1, move 9 to the root, and sift `9, 3, 6, 14, 8, 11`. The smaller child of 9 is 3, so they swap. Then 9 is greater than its child 8, so they swap. The heap is `3, 8, 6, 14, 9, 11`.

Extract 3, move 11 to the root, and sift `11, 8, 6, 14, 9`. The smaller child of 11 is 6, so they swap, and the heap is `6, 8, 11, 14, 9`.

Extract 6. The first three removed keys are 1, 3, and 6. Reading the original level order would suggest 1, 3, 6 as well at the start, but the third original level-order key is already 6 only by coincidence of this heap. The sift above shows why 8 is not removed third: after 1 and 3 leave, 6 is promoted to the root ahead of 8.

### Q13

Answer: (A)

Each extract-min returns the current root, and the downward heapify restores a min-heap on the keys that remain. The next root is therefore the minimum of what is left. The output is the keys in non-decreasing order. It is not the original level order, and the later roots are minima of the remaining keys rather than arbitrary leftovers. This is the heap contribution to heap sort: the sorted order is the sequence of extractions. The question does not ask for a separate sorting algorithm.

### Q14

Answer: (A)

The 1-based left-child index is `2 * 5 = 10`. The right child is 11. The formula `2i + 1` is the left child in a 0-based array. Using it on a 1-based index 5 produces 11, which is the right child, not the left child. The off-by-one comes from mixing the two numberings.

### Q15

Answer: (A), (D)

The BST insertions produce

```text
      4
     / \
    2   6
   / \
  1   3
```

Every level above the last is full, and the last level is packed to the left, so the shape is complete. The search-tree links are also correct, so it is a BST. It is not a min-heap, because the root 4 is greater than its child 2. It is not a max-heap, because the root 4 is smaller than its child 6. A complete BST shape does not make the parent keys a heap.

### Q16

Answer: (A)

Heapify the array `5, 3, 8, 1, 2` from index 2.

Index 2 holds 3. Its children are 1 and 2, so 3 swaps with 1. The array is `5, 1, 8, 3, 2`.

Index 1 holds 5. Its children are 1 and 8, so 5 swaps with 1. The array is `1, 5, 8, 3, 2`. Index 2 must be sifted: its children are 3 and 2, so 5 swaps with 2. The array is `1, 2, 8, 3, 5`.

The bottom-up result is 1, 2, 8, 3, 5. Inserting 5, then 3, then 8, then 1, then 2 one at a time produces the different min-heap `1, 2, 8, 5, 3`. Both satisfy the heap property. The procedure named in the question is bottom-up build-heap, so the array is the first of those two.

### Q17

Answer: 5

- Insert 8: `8`
- Insert 4: `4, 8`
- Insert 6: `4, 8, 6`
- Insert 1: `1, 4, 6, 8`
- Insert 5: 5 stays under 4, giving `1, 4, 6, 8, 5`

Extract-min removes 1 and moves 5 to the root. Sifting swaps 5 with 4 and stops. The heap is `4, 5, 6, 8`.

Insert 3. It swaps with 5 and then with 4, giving `3, 4, 6, 8, 5`.

Extract-min removes 3 and moves 5 to the root. Sifting swaps 5 with 4. The child of that new index-2 position is 8, and `5 <= 8`, so the sift stops. The heap is `4, 5, 6, 8`. Index 2 holds 5.

Several different min-heaps can be built from the remaining keys `{4, 5, 6, 8}`. The operations above fix this particular one. The root must be 4 in every min-heap of these keys, but the key at index 2 depends on the sifts.

### Q18

Answer: 9

Continue from the trace in Q12. After removing 1 and 3, the heap is `6, 8, 11, 14, 9`.

Extract 6 and move the last key, 9, to the root. The array before sifting is `9, 8, 11, 14`. The smaller child of 9 is 8, so they swap, giving `8, 9, 11, 14`. Index 2 now holds 9, and its only remaining child is 14. Since `9 <= 14`, the sift stops.

Index 2 holds 9. The root is 8, the minimum of the four keys that remain, but index 2 is not determined by that fact alone.
