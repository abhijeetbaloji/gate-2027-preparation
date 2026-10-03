# GATE PYQs

## 2026

### Q.33

**Paper:** GATE 2026 CS-1 (forenoon)

**Question:**

The height of a binary tree is the number of edges in the longest path from the root
to a leaf in the tree. The maximum possible height of a full binary tree with
23 nodes is _________. (answer in integer)

**Options:**

The paper does not print options for this numerical-answer question.

**Type:** NAT

**Answer:** VERIFICATION REQUIRED

**Source:** GATE 2026 CS-1 (forenoon), `12-PYQ/2026/set-01/question-paper.pdf`

---

### Q.62

**Paper:** GATE 2026 CS-1 (forenoon)

**Question:**

The following sequence corresponds to the preorder traversal of a binary search
tree 𝑇:
50, 25, 13, 40, 30, 47, 75, 60, 70, 80, 77
The position of the element 60 in the postorder traversal of 𝑇 is ______. (answer in
integer)
Note: The position begins with 1.

**Options:**

The paper does not print options for this numerical-answer question.

**Type:** NAT

**Answer:** VERIFICATION REQUIRED

**Source:** GATE 2026 CS-1 (forenoon), `12-PYQ/2026/set-01/question-paper.pdf`

---

### Q.12

**Paper:** GATE 2026 CS-2 (afternoon)

**Question:**

The set T represents various traversals over binary tree. The set S represents the
order of visiting nodes during a traversal.
T  S
I: Inorder  L: left subtree, node, right subtree
II: Preorder  M: node, left subtree, right subtree
III: Postorder N: left subtree, right subtree, node
Which one of the following is the correct match from T to S ?

**Options:**

A. I – L, II – M, III – N
B. I – M, II – L, III – N
C. I – N, II – M, III – L
D. I – L, II – N, III – M

**Type:** MCQ

**Answer:** VERIFICATION REQUIRED

**Source:** GATE 2026 CS-2 (afternoon), `12-PYQ/2026/set-02/question-paper.pdf`

---

## 2025

### Q.13

**Paper:** GATE 2025 CS-2

**Question:**

Consider a binary tree  𝑇 in which every node has either zero or two children.
Let 𝑛> 0 be the number of nodes in 𝑇.
Which ONE of the following is the number of nodes in 𝑇 that have exactly two
children?

**Options:**

A. 𝑛−2 2
B. 𝑛−1 2
C. 𝑛 2
D. 𝑛+ 1

**Type:** MCQ

**Answer:** VERIFICATION REQUIRED

**Source:** GATE 2025 CS-2, `12-PYQ/2025/set-02/question-paper.pdf`

---

## 2023

### Q.47

**Paper:** GATE 2023 CS

**Question:**

Consider the C function foo and the binary tree shown.
typedef struct node {
int val;^{10}
struct node *left, *right;
} node;_{5}  11
int foo(node *p) {
int retval;_{3}  8  13
if (p == NULL)
return 0;
else {
retval = p->val + foo(p->left) + foo(p->right);
printf("%d ", retval);
return retval;
}
}
When foo is called with a pointer to the root node of the given binary tree, what
will it print?

**Options:**

A. 3 8 5 13 11 10
B. 3 5 8 10 11 13
C. 3 8 16 13 24 50
D. 3 16 8 50 24 13

**Type:** MCQ

**Answer:** VERIFICATION REQUIRED

**Source:** GATE 2023 CS, `12-PYQ/2023/question-paper.pdf`

---

## 2021

### Q.4

**Paper:** GATE 2021 CS Set-1

**Question:**

Consider the following statements.
S1: The sequence of procedure calls corresponds to a preorder traversal
of the activation tree.
S2: The sequence of procedure returns corresponds to a postorder
traversal of the activation tree.
Which one of the following options is correct?

**Options:**

A. S, is true and Sa is false
B. Sı is false and Sa is true
C. S, is true and S2 is true
D. Sı is false and S2 is false GATE Graduate Aptitude Test in Engineering 2021 2021 Organising Institute - IIT Bombay

**Type:** MCQ

**Answer:** VERIFICATION REQUIRED

**Source:** GATE 2021 CS Set-1, `12-PYQ/2021/set-01/question-paper.pdf`

---

### Q.47

**Paper:** GATE 2021 CS Set-1

**Question:**

Consider a dynamic hashing approach for 4-bit integer keys:
1. There is a main hash table of size 4.
2. The 2 least significant bits of a key is used to index into the main hash table.
3. Initially, the main hash table entries are empty.
4. Thereafter, when more keys are hashed into it, to resolve collisions, the set of
all keys corresponding to a main hash table entry is organized as a binary tree
that grows on demand.
5. First, the 3rd least significant bit is used to divide the keys into left and right
6. To resolve more collisions, each node of the binary tree is further sub-divided
into left and right subtrees based on the 4* least significant bit.
7. A split is done only if it is needed, i.e., only when there is a collision.
Consider the following state of the hash table.
00 01 10
empty 0 0
Which of the following sequences of key insertions can cause the above state of the
hash table (assume the keys are in decimal notation)?

**Options:**

A. 5, 9, 4, 13, 10, 7
B. 9, 5, 10, 6, 7, 1
C. 10, 9, 6, 7, 5, 13
D. 9, 5, 13, 6, 10, 14 GATE Graduate Aptitude Test in Engineering 2021 2021 Organising Institute - IIT Bombay

**Type:** MCQ

**Answer:** VERIFICATION REQUIRED

**Source:** GATE 2021 CS Set-1, `12-PYQ/2021/set-01/question-paper.pdf`

---

### Q.16

**Paper:** GATE 2021 CS Set-2

**Question:**

Consider a complete binary tree with 7 nodes. Let A denote the set of first 3
elements obtained by performing Breadth-First Search (BFS) starting from the
root. Let B denote the set of first 3 elements obtained by performing Depth-First
Search (DFS) starting from the root.
The value of |A - B is -
9.17 Consider the following deterministic finite automaton (DFA).
0,1
start →O 0 Op 0,1
1 0,1
The number of strings of length 8 accepted by the above automaton is

**Options:**

The paper does not print options for this numerical-answer question.

**Type:** NAT

**Answer:** VERIFICATION REQUIRED

**Source:** GATE 2021 CS Set-2, `12-PYQ/2021/set-02/question-paper.pdf`

---

## 2019

### Q.46

**Paper:** GATE 2019 CS (printed header Set-2)

**Question:**

Let T be a full binary tree with 8 leaves. (A full binary tree has every level full.) Suppose
two leaves a and b of Tare chosen uniformly and independently at random. The expected
value of the distance between a and b in T (i.e., the number of edges in the unique path
between a and b) is (rounded off to 2 decimal places)

**Options:**

The paper does not print options for this numerical-answer question.

**Type:** NAT

**Answer:** VERIFICATION REQUIRED

**Source:** GATE 2019 CS (printed header Set-2), `12-PYQ/2019/question-paper.pdf`

---

## 2018

### Q.20

**Paper:** GATE 2018 CS

**Question:**

The postorder traversal of a binary tree is 8,9,6,7,4,5,2,3,1. The inorder traversal of the same
tree is 8,6,9,4,7,2,5,1,3. The height of a tree is the length of the longest path from the root to
any leaf. The height of the binary tree above is ______.

**Options:**

The paper does not print options for this numerical-answer question.

**Type:** NAT

**Answer:** VERIFICATION REQUIRED

**Source:** GATE 2018 CS, `12-PYQ/2018/question-paper.pdf`

---

## 2016

### Q.11

**Paper:** GATE 2016 CS-2

**Question:**

Breadth First Search (BFS) is started on a binary tree beginning from the root vertex. There is
a vertex t at a distance four from the root. If t is the n-th vertex in this BFS traversal, then the
maximum possible value of n is  .

**Options:**

The paper does not print options for this numerical-answer question.

**Type:** NAT

**Answer:** VERIFICATION REQUIRED

**Source:** GATE 2016 CS-2, `12-PYQ/2016/set-02/question-paper.pdf`

---

### Q.36

**Paper:** GATE 2016 CS-2

**Question:**

Consider the following New-order strategy for traversing a binary tree:
• Visit the root;
• Visit the right subtree using New-order;
• Visit the left subtree using New-order;
The New-order traversal of the expression tree corresponding to the reverse polish expression
3 4 * 5 - 2 ˆ 6 7 * 1 + - is given by:

**Options:**

A. + - 1 6 7 * 2 ˆ 5 - 3 4 *
B. - + 1 * 6 7 ˆ 2 - 5 * 3 4
C. - + 1 * 7 6 ˆ 2 - 5 * 4 3
D. 1 7 6 * + 2 5 4 3 * - ˆ -

**Type:** MCQ

**Answer:** VERIFICATION REQUIRED

**Source:** GATE 2016 CS-2, `12-PYQ/2016/set-02/question-paper.pdf`

---

## 2015

### Q.15

**Paper:** GATE 2015 CS, 7 February Shift 1

**Question:**

The height of a tree is the length of the longest root-to-leaf path in it. The maximum and minimum
number of nodes in a binary tree of height 5 are

**Options:**

A. 63 and 6, respectively
B. 64 and 5, respectively
C. 32 and 6, respectively
D. 31 and 5, respectively

**Type:** MCQ

**Answer:** VERIFICATION REQUIRED

**Source:** GATE 2015 CS, 7 February Shift 1, `12-PYQ/2015/set-01/question-paper.pdf`

---

### Q.23

**Paper:** GATE 2015 CS, 7 February Shift 2

**Question:**

A binary tree T has 20 leaves. The number of nodes in T having two children is
Correct Answer :

**Options:**

The paper does not print options for this numerical-answer question.

**Type:** NAT

**Answer:** VERIFICATION REQUIRED

**Source:** GATE 2015 CS, 7 February Shift 2, `12-PYQ/2015/set-02/question-paper.pdf`

---

### Q.21

**Paper:** GATE 2015 CS, 8 February Shift 1

**Question:**

Ouestion Type : NAT
Consider a binary tree T that has 200 leaf nodes. Then, the number of nodes in T that have exactly
two children are
Correct Answer :

**Options:**

The paper does not print options for this numerical-answer question.

**Type:** NAT

**Answer:** VERIFICATION REQUIRED

**Source:** GATE 2015 CS, 8 February Shift 1, `12-PYQ/2015/set-03/question-paper.pdf`

---

## 2007

### Q.12

**Paper:** GATE 2007 CS

**Question:**

The maximum number of nodes in a binary tree of height h is: The height of a binary tree is the maximum number of edges in any root to leaf nath.

**Options:**

A. 2"-1
B. 2--1
C. 2*+1-1
D. 2*+1

**Type:** MCQ

**Answer:** VERIFICATION REQUIRED

**Source:** GATE 2007 CS, `12-PYQ/2007/question-paper.pdf`

---

### Q.13

**Paper:** GATE 2007 CS

**Question:**

The maximum number of binary trees that can be formed with three unlabeled nodes

**Options:**

A. 1
B. 5
C. 4
D. 3

**Type:** MCQ

**Answer:** VERIFICATION REQUIRED

**Source:** GATE 2007 CS, `12-PYQ/2007/question-paper.pdf`

---

### Q.39

**Paper:** GATE 2007 CS

**Question:**

The inorder and preorder traversal of a binary tree are
dbeafcgandabde c fg, respectively.
The postorder traversal of the binary tree is

**Options:**

A. debfgca
B. edbgfca
C. edbfgca
D. defgbca

**Type:** MCQ

**Answer:** VERIFICATION REQUIRED

**Source:** GATE 2007 CS, `12-PYQ/2007/question-paper.pdf`

---

### Q.43

**Paper:** GATE 2007 CS

**Question:**

A complete n-ary tree is a tree in which each node has n children or no children. Let /
be the number of internal nodes and L be the number of leavés in a complete n-ary
tree. If L = 41, and I =10, what is the value of n?

**Options:**

A. 3
B. 4
C. 5
D. 6

**Type:** MCQ

**Answer:** VERIFICATION REQUIRED

**Source:** GATE 2007 CS, `12-PYQ/2007/question-paper.pdf`

---

### Q.46

**Paper:** GATE 2007 CS

**Question:**

Consider the following C program segment where CellNode represents a node in a
binary tree:
struct CellNode {
struct CellNode *leftChild;
struct CellNode *rightChild; int element;
int GetValue (struct CellNode *ptr) {
int value = 0;
if (ptr != NULL)
if ((ptr->leftChild == NULL) &&
(ptr->rightChild == NULL))
value = 1;
else
value = value + GetValue (ptı->leftChild)
+ GetValue (ptr->rightChild);
return (value);
The value returned by GetValue when a pointer to the root of a binary tree is passed
as its argument is:

**Options:**

A. the number of nodes in the tree.
B. the number of internal nodes in the tree.
C. the number of leaf nodes in the tree.
D. the height of the tree.

**Type:** MCQ

**Answer:** VERIFICATION REQUIRED

**Source:** GATE 2007 CS, `12-PYQ/2007/question-paper.pdf`

---
