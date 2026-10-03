# Binary Search Trees — Practice Questions

Original practice for GATE CS. These questions are not from any GATE paper. Attempt the questions before reading the solutions.

Keys are distinct. Every key in a node’s left subtree is smaller than the node’s key, and every key in its right subtree is larger. Height is the number of edges on a longest root-to-leaf path. The inorder successor of a key is the smallest key in the tree that is strictly larger than it. The inorder predecessor is the largest key that is strictly smaller.

When a node with two children is deleted, its key is replaced by its inorder successor, and that successor node is then deleted from the right subtree. The successor has no left child.

## Level 1 — Conceptual

## Q1 — MCQ

Keys are inserted into an empty BST in the order 8, 3, 10, 1, 6. The inorder traversal is

A. 1, 3, 6, 8, 10

B. 8, 3, 1, 6, 10

C. 1, 6, 3, 10, 8

D. 8, 3, 10, 1, 6

---

## Q2 — NAT

In the tree built in Q1, a search for 6 compares 6 with how many keys before it reports success?

---

## Q3 — NAT

The minimum key in the tree built in Q1 is ____.

---

## Q4 — MSQ

Select all that apply. Which sequences can be the inorder traversal of a BST on distinct keys?

A. 4, 2, 5, 1, 3

B. 1, 2, 3, 4, 5

C. 2, 4, 6, 8

D. 9, 7, 5

---

## Level 2 — Standard GATE Style

## Q5 — NAT

Keys are inserted into an empty BST in the order 5, 2, 7, 1, 3, 6, 8. The height of the resulting tree is ____.

---

## Q6 — NAT

The leaf 1 is deleted from the tree in Q5. How many nodes remain?

---

## Q7 — NAT

In the tree of Q5, before any deletion, the inorder successor of 3 is ____.

---

## Q8 — MCQ

Node 2 is deleted from the original tree of Q5, using the successor rule above. The preorder traversal after that deletion is

A. 5, 3, 1, 7, 6, 8

B. 5, 2, 1, 3, 7, 6, 8

C. 5, 1, 3, 7, 6, 8

D. 3, 1, 5, 7, 6, 8

---

## Q9 — MCQ

Which insertion order produces a BST that is a right spine of height 4?

A. 3, 1, 4, 2, 5

B. 1, 2, 3, 4, 5

C. 5, 4, 3, 2, 1

D. 3, 2, 4, 1, 5

---

## Q10 — NAT

In the tree of Q5, how many nodes have two children?

---

## Level 3 — Multi-Step

## Q11 — MCQ

Keys are inserted into an empty BST in the order 10, 5, 15, 3, 7, 12, 18. The root is then deleted by the successor rule. The preorder traversal is

A. 12, 5, 3, 7, 15, 18

B. 10, 5, 3, 7, 15, 12, 18

C. 15, 5, 3, 7, 12, 18

D. 12, 5, 3, 7, 15, 12, 18

---

## Q12 — MCQ

Which statement about the following tree is correct?

```text
      8
     / \
    3   10
     \
      9
```

A. It is a BST, because each node is larger than its left child and smaller than its right child.

B. It is not a BST, because 9 is in the left subtree of 8 and 9 is greater than 8.

C. It is a BST, because its inorder traversal is 3, 9, 8, 10.

D. It is not a BST, because 10 is greater than 8.

---

## Q13 — NAT

In the tree of Q11, before the root is deleted, the inorder successor of 7 is ____.

---

## Q14 — NAT

In the tree of Q5, a search for the absent key 9 compares 9 with how many stored keys before it falls off the tree?

---

## Level 4 — Tricky / Trap-Based

## Q15 — MSQ

Select all that apply.

A. The inorder traversal of a BST with distinct keys is strictly increasing.

B. The inorder traversal of a min-heap is always strictly increasing.

C. The root of a BST is always the minimum key.

D. The root of a min-heap is always the minimum key.

---

## Q16 — NAT

In the tree of Q11, before the deletion, the inorder predecessor of 7 is ____.

---

## Q17 — MSQ

Select all that apply. Which insertion orders produce the same BST?

A. 5, 3, 8, 7

B. 5, 8, 3, 7

C. 5, 8, 7, 3

D. 5, 7, 8, 3

---

## Level 5 — Challenge

## Q18 — NAT

Keys are inserted into an empty BST in the order 20, 10, 30, 5, 15, 12, 18, 13. Node 10 is then deleted by the successor rule. The key that replaces 10 as the left child of 20 is ____.

---

## Q19 — NAT

How many distinct BSTs can be formed from the key set `{1, 2, 3}`?

---

## Q20 — NAT

The preorder traversal of a BST is `7, 4, 2, 5, 12, 9`. The inorder successor of 5 is ____.

## Answer Key

| Q | Type | Answer |
|---|------|--------|
| 1 | MCQ | (A) |
| 2 | NAT | 3 |
| 3 | NAT | 1 |
| 4 | MSQ | (B), (C) |
| 5 | NAT | 2 |
| 6 | NAT | 6 |
| 7 | NAT | 5 |
| 8 | MCQ | (A) |
| 9 | MCQ | (B) |
| 10 | NAT | 3 |
| 11 | MCQ | (A) |
| 12 | MCQ | (B) |
| 13 | NAT | 10 |
| 14 | NAT | 3 |
| 15 | MSQ | (A), (D) |
| 16 | NAT | 5 |
| 17 | MSQ | (A), (B), (C) |
| 18 | NAT | 12 |
| 19 | NAT | 5 |
| 20 | NAT | 7 |

## Detailed Solutions

### Q1

Answer: (A)

Insert 8 as the root. Then 3 goes left of 8, and 10 goes right of 8. Then 1 goes left of 3, and 6 goes right of 3.

```text
      8
     / \
    3   10
   / \
  1   6
```

Inorder visits keys from smallest to largest: 1, 3, 6, 8, 10. Option (B) is preorder. A BST inorder sequence is sorted, so any sequence that is not sorted can be rejected immediately.

### Q2

Answer: 3

The search starts at 8. Since 6 is smaller, it goes left to 3. Since 6 is larger, it goes right to 6 and stops. The three comparisons are with 8, 3, and 6.

### Q3

Answer: 1

The minimum is the leftmost node. From 8 the path goes to 3 and then to 1. The minimum is 1. The maximum would be the rightmost node, 10.

### Q4

Answer: (B), (C)

Inorder of a BST on distinct keys lists those keys in increasing order. (B) and (C) are strictly increasing, so each is the inorder sequence of the BST obtained by inserting those keys in an order that builds some valid tree; the sequence itself is fixed once the set is fixed. (A) is not sorted. (D) is strictly decreasing. Neither (A) nor (D) can be a BST inorder traversal.

### Q5

Answer: 2

The insertions produce

```text
      5
     / \
    2   7
   / \ / \
  1  3 6  8
```

Every leaf is two edges below the root. The height is 2.

### Q6

Answer: 6

The original tree has 7 nodes. Deleting the leaf 1 unlinks that one node and leaves the other six. Node 2 then has only the right child 3.

### Q7

Answer: 5

Node 3 has no right subtree. Its successor is the lowest ancestor for which 3 lies in the left subtree. The parent of 3 is 2, and 3 is the right child of 2, so 2 is not the successor. The parent of 2 is 5, and 2 is the left child of 5. The successor is 5. The inorder sequence 1, 2, 3, 5, 6, 7, 8 confirms that 5 follows 3.

### Q8

Answer: (A)

Node 2 has two children. The successor is the minimum of its right subtree, which is 3. Node 3 is a leaf. Copying 3 into the place occupied by 2 and deleting the leaf 3 produces

```text
      5
     / \
    3   7
   /   / \
  1   6   8
```

Preorder is 5, 3, 1, 7, 6, 8. The inorder sequence remains sorted: 1, 3, 5, 6, 7, 8. Option (C) drops the key 3, and option (D) changes the root.

### Q9

Answer: (B)

Inserting 1, 2, 3, 4, 5 in that order sends every new key to the right child of the current rightmost node. The tree is a right spine with four edges, so its height is 4. Order (C) produces a left spine of height 4, not a right spine. Orders (A) and (D) both have height 2.

### Q10

Answer: 3

In the drawing for Q5, nodes 5, 2, and 7 each have two children. The other four nodes are leaves. The count is 3.

### Q11

Answer: (A)

The tree before deletion is

```text
       10
      /  \
     5    15
    / \   / \
   3  7  12  18
```

The successor of 10 is the minimum of the right subtree, which is 12. Node 12 is a leaf, so it is removed after its key replaces 10. Node 15 keeps its right child 18 and loses its left child.

```text
       12
      /  \
     5    15
    / \     \
   3  7     18
```

Preorder is 12, 5, 3, 7, 15, 18. Option (D) still contains 12 in the old place as well as in the root, which would duplicate a key.

### Q12

Answer: (B)

The local parent-child comparisons all hold: 3 is left of 8, 9 is right of 3, and 10 is right of 8. The BST rule is stronger. Every key in the left subtree of 8 must be smaller than 8. The key 9 is in that left subtree and is greater than 8, so the tree is not a BST. Its inorder sequence is 3, 9, 8, 10, which is not sorted. The comparison between 10 and 8 has the correct direction and is not the defect.

### Q13

Answer: 10

Node 7 has no right child. It is the right child of 5, and 5 is the left child of 10. The first ancestor that has this node in its left subtree is 10. The inorder sequence 3, 5, 7, 10, 12, 15, 18 shows 10 immediately after 7.

### Q14

Answer: 3

The search compares 9 with 5 and goes right, compares 9 with 7 and goes right, then compares 9 with 8 and goes right. The right child of 8 is empty, so the search stops. It made three key comparisons. The missing child is not a stored key and is not counted.

### Q15

Answer: (A), (D)

(A) is the inorder property of a BST. (D) is the min-heap root property: the minimum occupies the root, whatever the inorder sequence of the heap’s tree shape happens to be. (B) is false. A min-heap only orders each parent with its children; an inorder walk can visit a right child before a later left descendant and need not be sorted. (C) is false. The BST minimum is the leftmost node, and the root is the minimum only when it has no left subtree.

### Q16

Answer: 5

Node 7 has no left subtree, so the predecessor is not found by walking left. Node 7 is the right child of 5, which means 5 is the nearest ancestor smaller than 7. The predecessor is 5. The inorder sequence places 5 immediately before 7. The key 3 is smaller than 7, but it is not the closest smaller key. The key 10 is the successor, not the predecessor.

### Q17

Answer: (A), (B), (C)

Orders (A), (B), and (C) all produce

```text
    5
   / \
  3   8
     /
    7
```

In (A), 3 and 8 are attached directly to 5, and 7 goes left of 8. In (B) and (C), 8 is attached before 3, but 3 still goes left of 5, and 7 still goes left of 8. The relative order of keys that end up in different branches does not change the tree.

Order (D) inserts 7 before 8. Then 7 becomes the right child of 5, and 8 becomes the right child of 7:

```text
    5
   / \
  3   7
       \
        8
```

That is a different BST. Its preorder is 5, 3, 7, 8 rather than 5, 3, 8, 7.

### Q18

Answer: 12

The insertions produce

```text
        20
       /  \
     10    30
    /  \
   5    15
       /  \
     12    18
       \
        13
```

Node 10 has two children. Its successor is the leftmost key in the right subtree: 12. Node 12 has a right child, 13, and no left child. The key 12 is copied into the node that held 10. Deleting the old successor node promotes 13 into the left-child position previously occupied by 12.

```text
        20
       /  \
     12    30
    /  \
   5    15
       /  \
     13    18
```

The left child of 20 is now 12. The inorder sequence stays 5, 12, 13, 15, 18, 20, 30. Replacing 10 by its right child 15 would be the one-child deletion rule, and it would drop the key 5’s relationship incorrectly if it were applied here; 10 has two children, so the successor rule is the one that applies.

### Q19

Answer: 5

The root may be 1, 2, or 3.

- If the root is 1, both remaining keys are in the right subtree. Those two keys form 2 BSTs.
- If the root is 3, both remaining keys are in the left subtree. Those two keys form 2 BSTs.
- If the root is 2, the left subtree is the single node 1 and the right subtree is the single node 3. That is 1 BST.

The total is `2 + 2 + 1 = 5`. This is the Catalan number `C_3`.

### Q20

Answer: 7

Inserting the preorder keys from left to right rebuilds the BST. The first key, 7, is the root. The following keys that are smaller than 7 are the left subtree, and the first later key that is larger starts the right subtree.

```text
      7
     / \
    4   12
   / \  /
  2  5 9
```

Node 5 has no right subtree. It is the right child of 4, and 4 is the left child of 7, so the successor is 7. The sorted inorder sequence is 2, 4, 5, 7, 9, 12, which places 7 immediately after 5. For distinct keys, the preorder sequence determines the BST: the root is first, and each later key goes to the unique vacant BST position.
