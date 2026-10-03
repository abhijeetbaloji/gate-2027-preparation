# Trees — Practice Questions

Original practice for GATE CS. These questions are not from any GATE paper. Attempt the questions before reading the solutions.

Height is the number of edges on a longest path from the root to a leaf. A single node has height 0. In these questions, a **full** binary tree means every node has 0 or 2 children. A **complete** binary tree means every level except possibly the last is completely filled, and the nodes on the last level are as far left as possible. Inorder visits left subtree, node, right subtree. Preorder visits node, left, right. Postorder visits left, right, node. Level order visits nodes level by level, left to right.

## Level 1 — Conceptual

## Q1 — MCQ

The minimum possible height of a binary tree with 7 nodes is

A. 1

B. 2

C. 3

D. 6

---

## Q2 — NAT

A non-empty full binary tree has 8 leaves. How many nodes does it have in total?

---

## Q3 — MCQ

For the tree below, the inorder traversal is

```text
      1
     / \
    2   3
   / \
  4   5
```

A. 4, 2, 5, 1, 3

B. 1, 2, 4, 5, 3

C. 4, 5, 2, 3, 1

D. 1, 2, 3, 4, 5

---

## Q4 — NAT

How many leaves does the tree in Q3 have?

---

## Level 2 — Standard GATE Style

## Q5 — NAT

The height of the tree in Q3 is ____.

---

## Q6 — MCQ

Which traversal of the tree in Q3 produces 1, 2, 4, 5, 3?

A. inorder

B. preorder

C. postorder

D. the reverse of inorder

---

## Q7 — NAT

The maximum number of nodes in a binary tree of height 3 is ____.

---

## Q8 — MCQ

The minimum number of nodes in a binary tree of height 3 is

A. 3

B. 4

C. 7

D. 8

---

## Q9 — MCQ

A binary tree has preorder `6, 2, 1, 4, 8, 7` and inorder `1, 2, 4, 6, 7, 8`. Its postorder traversal is

A. 1, 4, 2, 7, 8, 6

B. 1, 2, 4, 7, 8, 6

C. 6, 2, 8, 1, 4, 7

D. 4, 1, 2, 7, 8, 6

---

## Q10 — NAT

In the tree of Q9, how many nodes have exactly one child?

---

## Level 3 — Multi-Step

## Q11 — MCQ

The level order of the tree below is

```text
        3
      /   \
     7     6
    / \     \
   2   5     8
      /
     4
```

A. 3, 7, 6, 2, 5, 8, 4

B. 2, 7, 4, 5, 3, 6, 8

C. 2, 4, 5, 7, 8, 6, 3

D. 3, 7, 2, 5, 4, 6, 8

---

## Q12 — NAT

What is the maximum number of leaves a binary tree with 10 nodes can have?

---

## Q13 — MCQ

The number of distinct binary-tree shapes with exactly 3 nodes is

A. 3

B. 4

C. 5

D. 6

---

## Q14 — MSQ

Select all that apply. For the tree drawn in Q11:

A. Its height is 3.

B. It has 4 leaves.

C. Exactly two nodes have two children.

D. Exactly two nodes have one child.

---

## Level 4 — Tricky / Trap-Based

## Q15 — MCQ

Consider this tree.

```text
      1
     / \
    2   3
   / \ /
  4  5 6
```

Which description is correct, using the definitions at the top of this set?

A. It is both complete and full.

B. It is complete but not full.

C. It is full but not complete.

D. It is neither complete nor full.

---

## Q16 — MCQ

For the tree in Q3, the reverse of the preorder sequence is 3, 5, 4, 2, 1. Which statement is correct?

A. That reversed sequence is the postorder of this tree.

B. Reversing preorder produces postorder for every binary tree.

C. For this tree, the reversed preorder differs from the postorder.

D. Reversing inorder produces preorder for every binary tree.

---

## Q17 — NAT

A chain of three nodes has one leaf and two edges on the path from the root to that leaf. One book defines height as the number of nodes on a longest root-to-leaf path, so it would call this height 3. Under the edge definition used in this set, the height is ____.

---

## Level 5 — Challenge

## Q18 — MCQ

Do the preorder and postorder sequences of a binary tree always determine one unique binary tree?

A. Yes. Those two sequences fix every parent-child link.

B. No. Preorder `1, 2` and postorder `2, 1` arise both when 2 is the left child of 1 and when 2 is the right child of 1.

C. Yes. The first preorder key and the last postorder key name the root, and that split always fixes the rest of the tree.

D. Yes whenever both sequences contain more than two keys.

---

## Q19 — NAT

A complete binary tree has 20 nodes. How many nodes lie on its deepest level?

---

## Q20 — NAT

Every node of a binary tree has two child fields. In the tree drawn in Q11, how many of those fields are NULL?

## Answer Key

| Q | Type | Answer |
|---|------|--------|
| 1 | MCQ | (B) |
| 2 | NAT | 15 |
| 3 | MCQ | (A) |
| 4 | NAT | 3 |
| 5 | NAT | 2 |
| 6 | MCQ | (B) |
| 7 | NAT | 15 |
| 8 | MCQ | (B) |
| 9 | MCQ | (A) |
| 10 | NAT | 1 |
| 11 | MCQ | (A) |
| 12 | NAT | 5 |
| 13 | MCQ | (C) |
| 14 | MSQ | (A), (C), (D) |
| 15 | MCQ | (B) |
| 16 | MCQ | (C) |
| 17 | NAT | 2 |
| 18 | MCQ | (B) |
| 19 | NAT | 5 |
| 20 | NAT | 8 |

## Detailed Solutions

### Q1

Answer: (B)

Seven nodes fill three levels: 1 node, then 2, then 4. The longest root-to-leaf path has two edges, so the minimum height is 2. A single chain of 7 nodes has height 6, which is the maximum, not the minimum.

### Q2

Answer: 15

In a full binary tree every node has 0 or 2 children, so there is no node with one child. If `L` is the number of leaves and `I` is the number of nodes with two children, the relation is `L = I + 1`. Here `L = 8`, so `I = 7`. The total is `8 + 7 = 15`. Equivalently, a full binary tree with `L` leaves has `2L - 1` nodes.

### Q3

Answer: (A)

Inorder walks the left subtree, then the node, then the right subtree. The left subtree of 1 produces 4, 2, 5. Then 1 is visited. The right subtree is the leaf 3. The sequence is 4, 2, 5, 1, 3.

### Q4

Answer: 3

The leaves are 4, 5, and 3. Node 2 has two children, and node 1 has two children. The leaf count is 3.

### Q5

Answer: 2

The longest root-to-leaf paths are 1–2–4 and 1–2–5. Each contains two edges. The height is 2. Counting the three nodes on that path would give a different convention; this set counts edges.

### Q6

Answer: (B)

The sequence starts with the root 1, then the entire left subtree 2, 4, 5, then the right subtree 3. That is node, left, right: preorder. Inorder was computed in Q3, and postorder is 4, 5, 2, 3, 1.

### Q7

Answer: 15

A binary tree of height 3 can fill every position through level 3. The level sizes are 1, 2, 4, and 8. The total is `2^(3+1) - 1 = 15`.

### Q8

Answer: (B)

Height 3 means some root-to-leaf path has exactly three edges, so that path contains four nodes. A chain of four nodes achieves height 3 and uses no extra nodes. Fewer than four nodes cannot contain a path of three edges.

### Q9

Answer: (A)

The first preorder key, 6, is the root. In the inorder sequence, keys before 6 are the left subtree and keys after 6 are the right subtree. The left keys are 1, 2, 4, and the right keys are 7, 8.

The next preorder keys are 2, 1, 4 for the left and 8, 7 for the right. In the left piece, 2 is the root, 1 is its left child, and 4 is its right child. In the right piece, 8 is the root and 7 is its left child.

```text
      6
     / \
    2   8
   / \ /
  1  4 7
```

Postorder visits left, right, then the node: 1, 4, 2, then 7, 8, then 6. The sequence is 1, 4, 2, 7, 8, 6. Preorder and inorder together fix this tree because the keys are distinct: each root splits its inorder interval into a unique left part and right part.

### Q10

Answer: 1

In the tree constructed in Q9, node 8 has a left child and no right child. Every other node has either two children or none. The count is 1.

### Q11

Answer: (A)

Level order reads one level at a time, from left to right. Level 0 is 3. Level 1 is 7, 6. Level 2 is 2, 5, 8. Level 3 is 4. The sequence is 3, 7, 6, 2, 5, 8, 4. Option (B) is inorder, option (C) is postorder, and option (D) is preorder.

### Q12

Answer: 5

A binary tree with `n` nodes has `n - 1` edges. If `k` nodes are internal, they provide at most `2k` child edges, so `2k >= n - 1` and `k >= 5` when `n = 10`. The number of leaves is `n - k <= 5`. Five leaves are achievable: four internal nodes have two children and one internal node has one child, giving `2*4 + 1 = 9` edges. The maximum is 5. A full shape is impossible for an even number of nodes, since a full binary tree has an odd number of nodes.

### Q13

Answer: (C)

There are five shapes:

- the root’s left child has a left child
- the root’s left child has a right child
- the root has two children
- the root’s right child has a left child
- the root’s right child has a right child

The count is the Catalan number `C_3 = 5`. Here the nodes are unlabeled, so only the shape matters.

### Q14

Answer: (A), (C), (D)

The longest path is 3–7–5–4, with three edges, so the height is 3. The leaves are 2, 4, and 8, so there are three leaves, not four. Nodes 3 and 7 have two children. Nodes 5 and 6 have one child: 5 has only 4, and 6 has only 8. (A), (C), and (D) are true.

### Q15

Answer: (B)

Every level above the last is full, and the last level occupies the leftmost three positions. The tree is complete. It is not full: node 3 has one child, namely 6. A full tree would give 3 either no children or both children. Completeness does not imply the full-node condition, and the full-node condition does not imply completeness.

### Q16

Answer: (C)

Preorder of the Q3 tree is 1, 2, 4, 5, 3. Its reverse is 3, 5, 4, 2, 1. Postorder is 4, 5, 2, 3, 1. Those sequences differ, so (A) and (B) are false. Reversing inorder 4, 2, 5, 1, 3 gives 3, 1, 5, 2, 4, which is not preorder, so (D) is false as a claim about every binary tree. The correct statement is (C).

### Q17

Answer: 2

The path contains the root, one internal node, and the leaf. The number of edges on it is 2, so the height in this set is 2. The other book counts the three nodes and reports 3. The two answers describe the same chain; they come from different definitions. The numerical answer required here is the edge count.

### Q18

Answer: (B)

Both candidate trees have preorder 1, 2: the root is visited first, and the only other node is visited next whether it hangs on the left or the right. Both have postorder 2, 1: the child is finished before the root. Knowing the root does not say which side the child is on. Preorder together with inorder would separate the two trees, because the inorder position of 2 relative to 1 shows the side. Preorder together with postorder does not.

### Q19

Answer: 5

The largest complete tree of height 3 has `2^4 - 1 = 15` nodes, filling levels 0 through 3. The 20-node complete tree therefore has height 4, because `floor(log2 20) = 4`. Its deepest level contains the 5 nodes beyond those 15. The capacity of that level is 16, but only 5 positions are occupied, starting from the left.

### Q20

Answer: 8

The drawn tree has 7 nodes and therefore 6 edges. Each node has two child fields, giving 14 fields. Each edge fills one field, so `14 - 6 = 8` fields are NULL. The same count is `n + 1 = 8` for any binary tree with `n` nodes: every node except the root is the target of one child pointer, and the remaining child fields are NULL.
