# B and B+ Trees — Practice Questions

Original practice for GATE CS. These questions are not from any GATE paper. Attempt the questions before reading the solutions.

Each numerical question states its own order convention. "At most P children" means an internal node stores at most P child pointers and therefore at most P − 1 keys. A leaf capacity is stated separately as a maximum number of keys. Unless the question relaxes it, every node except the root is at least half full, rounded up: a non-root internal node has at least ⌈P / 2⌉ children, and a non-root leaf has at least ⌈L / 2⌉ keys when L is its maximum. The root may contain less. The height used below is the number of nodes on a root-to-leaf path, counting both the root and the leaf.

## Level 1 — Conceptual

## Q1 — MCQ

Which statement is true of a B+ tree?

A. Every root-to-leaf path has the same number of nodes
B. Leaf nodes may sit at different depths after an insertion that splits only one leaf
C. An internal node has no key order; only the leaves are sorted
D. The height grows by one on every leaf split

---

## Q2 — MCQ

Which statement is true of a B+ tree index?

A. A separator copied up from a leaf split remains in the leaf as well as appearing in an ancestor
B. Internal nodes hold the data records, and leaves hold only pointers back to internal nodes
C. Leaves are not linked to sibling leaves
D. Two successful searches can end at different levels of the tree

---

## Q3 — MCQ

The usual minimum-occupancy rule of a B+ tree is relaxed for which node?

A. Only the root
B. Every leaf, including the root when the root is a leaf
C. Every non-root internal node
D. Only the leftmost leaf

---

## Q4 — NAT

An internal node has at most 6 children. How many children must a non-root internal node contain? ______

---

## Level 2 — Standard GATE Style

## Q5 — NAT

A leaf holds at most 5 keys. How many keys must a non-root leaf contain? ______

---

## Q6 — MCQ

In this question, a B-tree of order 5 has at most 5 children in a node. How many keys must a non-root node contain?

A. 1
B. 2
C. 3
D. 4

---

## Q7 — NAT

An internal node of a B+ tree is packed into a 512-byte block. A key is 12 bytes and a child pointer is 8 bytes. A node with n children stores n − 1 keys and n pointers, and nothing else. What is the largest legal value of n? ______

---

## Q8 — MSQ

A leaf of the same B+ tree stores 12-byte keys, 8-byte record pointers, and one extra 8-byte sibling pointer. The internal-node layout is the one in Q7. Which statements are true? Select all that apply.

A. An internal node can have 26 children
B. An internal node can have 27 children
C. A leaf can hold 25 keys
D. A leaf can hold 26 keys

---

## Level 3 — Multi-Step

Q9 and Q10 use one B+ tree. Each internal node has at most 5 children. Each leaf holds at most 4 keys. The tree stores 100 keys.

## Q9 — NAT

What is the minimum possible number of nodes on a root-to-leaf path? ______

---

## Q10 — MCQ

What is the maximum possible number of nodes on a root-to-leaf path?

A. 2
B. 3
C. 4
D. 5

---

## Q11 — MCQ

For the same limits, what is the minimum number of leaf nodes that can hold 100 keys?

A. 20
B. 25
C. 50
D. 100

---

## Level 4 — Tricky / Trap-Based

## Q12 — MCQ

Which statement is false?

A. In a B-tree, a search can stop at an internal node that stores a pointer to the matching record
B. In a B+ tree, the record pointer for a key is found at a leaf
C. In a B+ tree, every separator key in an internal node is stored together with that key's record pointer
D. Linked B+ tree leaves support a range scan that walks sideways across leaves

---

## Q13 — MSQ

A B+ tree has internal nodes of at most 5 children and leaves of at most 4 keys. A B-tree node may store a record pointer beside a key. Which statements are true? Select all that apply.

A. A non-root leaf contains at least 2 keys
B. A non-root internal node contains at least 3 children
C. The root must also be at least half full
D. A B-tree internal node can contain a pointer to a data record

---

## Q14 — NAT

Insert the keys 2, 4, 6, 8, 10, 12, 14, 16, in that order, into an empty B+ tree. A leaf holds at most 3 keys. An internal node holds at most 3 keys, hence at most 4 children. When a leaf overflows to 4 keys, the smaller 2 stay in the left leaf, the larger 2 go to the right leaf, and the first key of the right leaf is copied upward. If an internal node overflows to 4 keys, the third of those keys is moved up to the parent, the first two keys stay in the left node, and the last key stays in the right node. After the insertions, what is the largest key stored in the root? ______

---

## Level 5 — Challenge

The next two questions use a B+ tree whose internal nodes have at most 26 children and whose leaves hold at most 25 keys. It stores 1,000,000 keys. These capacities are the block-packing limits from Q7 and Q8; the questions do not depend on re-deriving the byte arithmetic.

## Q15 — NAT

What is the minimum possible number of nodes on a root-to-leaf path? ______

---

## Q16 — MCQ

What is the maximum possible number of nodes on a root-to-leaf path?

A. 4
B. 5
C. 6
D. 7

---

## Answer Key

| Q | Type | Answer |
|---|------|--------|
| 1 | MCQ | A |
| 2 | MCQ | A |
| 3 | MCQ | A |
| 4 | NAT | 3 |
| 5 | NAT | 3 |
| 6 | MCQ | B |
| 7 | NAT | 26 |
| 8 | MSQ | A, C |
| 9 | NAT | 3 |
| 10 | MCQ | C |
| 11 | MCQ | B |
| 12 | MCQ | C |
| 13 | MSQ | A, B, D |
| 14 | NAT | 14 |
| 15 | NAT | 5 |
| 16 | MCQ | C |

## Detailed Solutions

### Q1

Answer: A

A B+ tree is height-balanced. Every leaf is at the same depth, so every root-to-leaf path has the same number of nodes. A split replaces one node by two at the same level and may push a separator upward; it does not put one leaf deeper than another. B therefore fails. Keys inside every node, internal or leaf, are kept in sorted order, so C fails. The height grows only when a split propagates all the way through the current root and a new root is created. An ordinary leaf split does not do that, so D fails.

### Q2

Answer: A

On a leaf split, the middle separator is copied into the parent and also stays in the right leaf, because every record key lives in exactly one leaf. Ancestors store copies used only for routing.

B swaps the two levels and describes neither a B+ tree nor a B-tree accurately. C is false because the leaf chain is what makes a range scan cheap. D contradicts Q1: every successful search ends at a leaf, and all leaves have the same depth.

### Q3

Answer: A

Non-root nodes are created by splits that hand each sibling at least the minimum occupancy, and merges or redistributions restore that minimum. The root is allowed to be under-full. A leaf root may hold a single key, and an internal root may have only two children, even when ⌈P / 2⌉ is larger than 2.

B and C apply the root's exemption to nodes that must stay half full. D has no special role in the occupancy rule; the leftmost leaf obeys the same minimum as every other non-root leaf.

### Q4

Answer: 3

The maximum number of children is P = 6. A non-root internal node has at least ⌈6 / 2⌉ = 3 children. It therefore stores at least 2 keys. The answer requested is the child count, 3, not the key count.

### Q5

Answer: 3

The leaf maximum is L = 5. A non-root leaf has at least ⌈5 / 2⌉ = 3 keys. Rounding 2.5 down to 2 is the error. The root, if it is still a single leaf, may hold fewer than 3 keys; the question excludes the root.

### Q6

Answer: B

Order 5 is defined here as at most 5 children, so a node holds at most 4 keys. A non-root node has at least ⌈5 / 2⌉ = 3 children and therefore at least 3 − 1 = 2 keys.

A is the root's possible key count, not the non-root minimum. C is the minimum number of children, one larger than the minimum number of keys. D is the maximum number of keys.

### Q7

Answer: 26

The inequality is (n − 1) · 12 + n · 8 ≤ 512, which simplifies to 20n − 12 ≤ 512, so 20n ≤ 524 and n ≤ 26.2. The largest integer n is 26.

Check the endpoints. For n = 26, the node stores 25 keys and 26 pointers: 25 · 12 + 26 · 8 = 300 + 208 = 508 ≤ 512. For n = 27: 26 · 12 + 27 · 8 = 312 + 216 = 528 > 512. So 27 does not fit.

### Q8

Answer: A, C

A is the result of Q7. B is the 528-byte node that does not fit.

A leaf with k keys uses k · (12 + 8) + 8 = 20k + 8 bytes. For k = 25, 500 + 8 = 508 ≤ 512. For k = 26, 520 + 8 = 528 > 512. C is true and D is false. Forgetting the sibling pointer would appear to allow k = 25 still, since 25 · 20 = 500, but it would also make k = 26 look legal at 520 if someone both drops the sibling pointer and mis-compares with 512. With the sibling pointer included, 26 does not fit.

### Q9

Answer: 3

Pack every node as full as possible.

- 1 level, a leaf root: at most 4 keys. Too small.
- 2 levels: the root has at most 5 leaf children, and each leaf has at most 4 keys, for 20 keys. Still below 100.
- 3 levels: at most 5 · 5 = 25 leaves, times 4 keys, which is exactly 100.

The minimum path length is 3. A tree of path length 2 cannot store 100 keys under these maxima.

### Q10

Answer: C

Minimum occupancy makes the tree as tall as possible. A non-root internal node has at least ⌈5 / 2⌉ = 3 children. A non-root leaf has at least ⌈4 / 2⌉ = 2 keys. The root, once it is internal, has at least 2 children.

Minimum keys at path length h:

- h = 3: at least 2 · 3 = 6 leaves, times 2 keys, which is 12. Maximum is 100, so 100 keys fit.
- h = 4: at least 2 · 3 · 3 = 18 leaves, times 2 keys, which is 36. Still at most the full-tree maximum 5^3 · 4 = 500, so 100 keys fit.
- h = 5: at least 2 · 3^3 = 54 leaves, times 2 keys, which is 108. That already exceeds 100, so a legal tree of 100 keys cannot be this tall.

The maximum path length is 4. B is the minimum from Q9. D is the illegal height whose minimum occupancy is 108 keys.

### Q11

Answer: B

The fewest leaves is obtained by filling leaves completely: ⌈100 / 4⌉ = 25. That packing is achievable at the minimum height of Q9, because 25 leaves are exactly 5 parents with 5 children each, under one root. The parent level has 5 nodes, which is within the root's maximum of 5 children.

A divides 100 by 5, the internal fanout, and never looks at the leaf capacity. C uses the minimum leaf occupancy, ⌈100 / 2⌉ = 50, which is the largest number of leaves, not the smallest. D is one key per leaf, below the legal minimum for non-root leaves.

### Q12

Answer: C

C is the false statement. In a B+ tree the internal separator is a copy used for routing. The record pointer sits in the leaf. Internal nodes do not carry a record pointer for every separator.

A is true of a classical B-tree: keys and their record pointers can occupy internal nodes, so a search may finish before a leaf. B is the B+ tree search rule. D is why the leaf chain exists. The trap is to describe a B-tree's internal record pointers as if they were part of a B+ tree.

### Q13

Answer: A, B, D

Leaf maximum 4 gives a non-root minimum of ⌈4 / 2⌉ = 2 keys. A holds. Internal maximum 5 gives a non-root minimum of ⌈5 / 2⌉ = 3 children. B holds. A classical B-tree stores record pointers in internal nodes as well as in leaves. D holds.

C is false. The root is the node excused from the half-full rule. Requiring the root to be half full would make a one-key tree illegal and would change the height bounds in Q10.

### Q14

Answer: 14

Leaf overflow always splits 4 sorted keys into 2 and 2, and the copied separator is the first key of the right leaf.

- Insert 2, 4, 6. One leaf: [2, 4, 6].
- Insert 8. The leaf [2, 4, 6, 8] splits into [2, 4] and [6, 8]. Copy 6. The root is [6].
- Insert 10. The right leaf becomes [6, 8, 10].
- Insert 12. [6, 8, 10, 12] splits into [6, 8] and [10, 12]. Copy 10. The root becomes [6, 10]. Leaves: [2, 4], [6, 8], [10, 12].
- Insert 14. The rightmost leaf becomes [10, 12, 14].
- Insert 16. [10, 12, 14, 16] splits into [10, 12] and [14, 16]. Copy 14. The root becomes [6, 10, 14].

The root keys are 6, 10, and 14. It holds exactly 3 keys, so the internal-node split rule is never used. The largest root key is 14. The leaves are [2, 4], [6, 8], [10, 12], and [14, 16].

### Q15

Answer: 5

Use maximum fanout. A path of h nodes has at most 26^(h − 1) leaves, and each leaf holds at most 25 keys.

- h = 4: 26^3 · 25 leaves' worth of keys. 26^2 = 676 and 26^3 = 17,576, then 17,576 · 25 = 439,400. That is less than 1,000,000.
- h = 5: 26^4 · 25 = 17,576 · 26 · 25 = 456,976 · 25 = 11,424,400, which is at least 1,000,000.

The shortest legal path has 5 nodes. Stopping at 4 leaves 439,400 keys of capacity unused and cannot store the file.

### Q16

Answer: C

Minimum fanout is ⌈26 / 2⌉ = 13 children for a non-root internal node, and ⌈25 / 2⌉ = 13 keys for a non-root leaf. An internal root has at least 2 children. The minimum number of keys at path length h is 2 · 13^(h − 2) · 13 = 2 · 13^(h − 1) for h ≥ 2.

- h = 6: 13^2 = 169, 13^3 = 2,197, and 13^4 = 28,561. Minimum leaves = 2 · 13^(6 − 2) = 57,122. Minimum keys = 57,122 · 13 = 742,586, which is at most 1,000,000. A tree this tall can still be thin enough.
- h = 7: minimum leaves = 2 · 13^5 = 2 · 371,293 = 742,586, and minimum keys = 742,586 · 13 = 9,653,618, which is more than 1,000,000.

The tallest legal path has 6 nodes. A is below even the minimum height. B is the minimum height from Q15, not the maximum. D is the first height whose minimum occupancy already exceeds the file.
