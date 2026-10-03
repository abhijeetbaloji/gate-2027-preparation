# GATE PYQs

## 2026

### Q.40

**Paper:** GATE 2026 CS-1 (forenoon)

**Question:**

Let 𝑃 be the set of all integers from 1 to 15. Consider any order of insertion of the
elements of 𝑃 into a binary search tree that creates a complete binary tree.
Which one of the following elements can NEVER be the third element that is
inserted?

**Options:**

A. 4
B. 2
C. 10
D. 5

**Type:** MCQ

**Answer:** VERIFICATION REQUIRED

**Source:** GATE 2026 CS-1 (forenoon), `12-PYQ/2026/set-01/question-paper.pdf`

---

### Q.49

**Paper:** GATE 2026 CS-2 (afternoon)

**Question:**

Consider a binary search tree (BST) with 𝑛 leaf nodes (𝑛> 0). Given any node 𝑉,
the key present in the node is denoted as 𝑉𝑎𝑙(𝑉). All the keys present in the given
BST are distinct. The keys belong to the set of real numbers.
For a node 𝑉, let 𝑆𝑢𝑐(𝑉) denote the node that is its inorder successor. If a node 𝑉
does not have an inorder successor, then  𝑆𝑢𝑐(𝑉) is  𝑁𝑈𝐿𝐿. As there are no
duplicates, if 𝑆𝑢𝑐(𝑉) is not 𝑁𝑈𝐿𝐿,  then 𝑉𝑎𝑙(𝑉) < 𝑉𝑎𝑙(𝑆𝑢𝑐(𝑉)).
Corresponding to every leaf node 𝐿_{𝑖} that has a non-NULL 𝑆𝑢𝑐(𝐿_{𝑖}), a new key 𝑘_{𝑖}
with the following property is to be inserted into the BST.
𝑉𝑎𝑙(𝐿_{𝑖}) < 𝑘_{𝑖} < 𝑉𝑎𝑙(𝑆𝑢𝑐(𝐿_{𝑖}))
Let 𝐾 represent the list of all such new keys to be inserted into the BST.
Which of the following statements is/are true?

**Options:**

A. 𝐾 cannot have any duplicates
B. 𝐾 will have at least one element
C. After inserting all keys from 𝐾, the height of the BST can increase at most by one
D. Number of nodes in the BST will double after inserting all keys from 𝐾

**Type:** MCQ

**Answer:** VERIFICATION REQUIRED

**Source:** GATE 2026 CS-2 (afternoon), `12-PYQ/2026/set-02/question-paper.pdf`

---

## 2025

### Q.12

**Paper:** GATE 2025 CS-1

**Question:**

Which ONE of the following statements is FALSE regarding the symbol table?

**Options:**

A. Symbol table is responsible for keeping track of the scope of variables.
B. Symbol table can be implemented using a binary search tree.
C. Symbol table is not required after the parsing phase.
D. Symbol table is created during the lexical analysis phase.

**Type:** MCQ

**Answer:** VERIFICATION REQUIRED

**Source:** GATE 2025 CS-1, `12-PYQ/2025/set-01/question-paper.pdf`

---

### Q.43

**Paper:** GATE 2025 CS-1

**Question:**

Let 𝐺(𝑉, 𝐸) be an undirected and unweighted graph with 100 vertices. Let 𝑑(𝑢, 𝑣)
denote the number of edges in a shortest path between vertices 𝑢 and 𝑣 in 𝑉. Let the
maximum value of 𝑑(𝑢, 𝑣), 𝑢, 𝑣∈𝑉 such that 𝑢≠𝑣, be 30. Let 𝑇 be any breadth-
first-search tree of 𝐺. Which ONE of the given options is CORRECT for every such
graph 𝐺?

**Options:**

A. The height of 𝑇 is exactly 15.
B. The height of 𝑇 is exactly 30.
C. The height of 𝑇 is at least 15.
D. The height of 𝑇 is at least 30.

**Type:** MCQ

**Answer:** VERIFICATION REQUIRED

**Source:** GATE 2025 CS-1, `12-PYQ/2025/set-01/question-paper.pdf`

---

### Q.35

**Paper:** GATE 2025 CS-2

**Question:**

Suppose the values  10, −4, 15, 30, 20, 5, 60, 19 are inserted in that order into an
initially empty binary search tree. Let  𝑇 be the resulting binary search tree.
The number of edges in the path from the node containing 19 to the root node of 𝑇
is ___________. (Answer in integer)

**Options:**

The paper does not print options for this numerical-answer question.

**Type:** NAT

**Answer:** VERIFICATION REQUIRED

**Source:** GATE 2025 CS-2, `12-PYQ/2025/set-02/question-paper.pdf`

---

## 2024

### Q.39

**Paper:** GATE 2024 CS2

**Question:**

You are given a set  𝑉 of distinct integers. A binary search tree  𝑇 is created by
inserting all elements of  𝑉 one by one, starting with an empty tree. The tree  𝑇
follows the convention that, at each node, all values stored in the left subtree of the
node are smaller than the value stored at the node. You are not aware of the sequence
in which these values were inserted into 𝑇, and you do not have access to 𝑇.
Which one of the following statements is TRUE?

**Options:**

A. Inorder traversal of 𝑇 can be determined from 𝑉
B. Root node of 𝑇 can be determined from 𝑉
C. Preorder traversal of 𝑇 can be determined from 𝑉
D. Postorder traversal of 𝑇 can be determined from 𝑉

**Type:** MCQ

**Answer:** VERIFICATION REQUIRED

**Source:** GATE 2024 CS2, `12-PYQ/2024/set-02/question-paper.pdf`

---

## 2021

### Q.10

**Paper:** GATE 2021 CS Set-1

**Question:**

A binary search tree T contains n distinet elements. What is the time complexity
of picking an element in T that is smaller than the maximum element in T?

**Options:**

A. e(nlogn)
B. e(n)
C. e(logn)
D. 0(1) GATE Graduate Aptitude Test in Engineering 2021 2021 Organising Institute - IIT Bombay

**Type:** MCQ

**Answer:** VERIFICATION REQUIRED

**Source:** GATE 2021 CS Set-1, `12-PYQ/2021/set-01/question-paper.pdf`

---

## 2020

### Q.5

**Paper:** GATE 2020 CS

**Question:**

The preorder traversal of a binary search tree is 15, 10, 12, 11, 20, 18, 16, 19.
Which one of the following is the postorder traversal of the tree?

**Options:**

A. 10, 11, 12, 15, 16, 18, 19, 20
B. 11, 12, 10, 16, 19, 18, 20, 15
C. 20, 19, 18, 16, 15, 12, 11, 10
D. 19, 16, 18, 20, 11, 12, 10, 15

**Type:** MCQ

**Answer:** VERIFICATION REQUIRED

**Source:** GATE 2020 CS, `12-PYQ/2020/question-paper.pdf`

---

### Q.6

**Paper:** GATE 2020 CS

**Question:**

What is the worst case time complexity of inserting n? elements into an AVL-tree
with n elements initially?

**Options:**

A. 0(n*)
B. 0(n2)
C. 0(n2l0g n)
D. 0(n3)

**Type:** MCQ

**Answer:** VERIFICATION REQUIRED

**Source:** GATE 2020 CS, `12-PYQ/2020/question-paper.pdf`

---

### Q.41

**Paper:** GATE 2020 CS

**Question:**

In a balanced binary search tree with n elements, what is the worst case time
complexity of reporting all elements in range [a, b]? Assume that the number of
reported elements is k.

**Options:**

A. 0(logn)
B. 0(logn + k)
C. 0 (k logn)
D. 0(nlogk)

**Type:** MCQ

**Answer:** VERIFICATION REQUIRED

**Source:** GATE 2020 CS, `12-PYQ/2020/question-paper.pdf`

---

## 2018

### Q.30

**Paper:** GATE 2018 CS

**Question:**

Let G be a simple undirected graph. Let  T_{D} be a depth first search tree of G. Let T_{B} be a
breadth first search tree of G.  Consider the following statements.
(I)  No edge of G is a cross edge with respect to T_{D}.  (A cross edge in G is between two
nodes neither of which is an ancestor of the other in T_{D}.)
(II)  For every edge (u,v) of G, if u is at depth i  and v is at depth  j in T_{B}, then |𝑖−𝑗| = 1.
Which of the statements above must necessarily be true?

**Options:**

A. I only
B. II only
C. Both I and II
D. Neither I nor II

**Type:** MCQ

**Answer:** VERIFICATION REQUIRED

**Source:** GATE 2018 CS, `12-PYQ/2018/question-paper.pdf`

---

## 2017

### Q.36

**Paper:** GATE 2017 CS Session 2

**Question:**

Correct: 2 Wrong :-0.66
The pre-order traversal of a binary search tree is given by 12, 8, 6, 2, 7, 9, 10, 16, 15, 19, 17, 20.
Then the post-order traversal of this tree is:
(А) 2, 6, 7,8, 9, 10, 12, 15, 16, 17, 19,20 (B) 2,7,6, 10, 9,8, 15, 17, 20, 19, 16, 12

**Options:**

C. 7,2, 6, 8, 9, 10, 20, 17, 19, 15, 16, 12
D. 7,6, 2, 10, 9, 8, 15, 16, 17, 20, 19, 12

**Type:** MCQ

**Answer:** VERIFICATION REQUIRED

**Source:** GATE 2017 CS Session 2, `12-PYQ/2017/set-02/question-paper.pdf`

---

## 2016

### Q.40

**Paper:** GATE 2016 CS-2

**Question:**

The number of ways in which the numbers 1, 2, 3, 4, 5, 6, 7 can be inserted in an empty binary
search tree, such that the resulting tree has height 6, is  .
Note: The height of a tree with a single node is 0.
CS(Set B)  11/18

**Options:**

The paper does not print options for this numerical-answer question.

**Type:** NAT

**Answer:** VERIFICATION REQUIRED

**Source:** GATE 2016 CS-2, `12-PYQ/2016/set-02/question-paper.pdf`

---

## 2015

### Q.17

**Paper:** GATE 2015 CS, 7 February Shift 1

**Question:**

Which of the following is/are correct inorder traversal sequence(s) of binary search tree(s)?
I. 3, 5, 7, 8, 15, 19, 25
IT. 5, 8, 9, 12, 10, 15, 25
2,7, 10, 8, 14, 16, 20
IV. 4, 6, 7, 9 18, 20, 25

**Options:**

A. I and IV only
B. II and II only
C. IIand IV only
D. II only

**Type:** MCQ

**Answer:** VERIFICATION REQUIRED

**Source:** GATE 2015 CS, 7 February Shift 1, `12-PYQ/2015/set-01/question-paper.pdf`

---

### Q.35

**Paper:** GATE 2015 CS, 7 February Shift 1

**Question:**

-5

What are the worst-case complexities of insertion and deletion of a key in a binary search tree?

**Options:**

A. 0(1ogn) for both insertion and deletion
B. e(n) for both insertion and deletion
C. e(n) for insertion and e(logn) for deletion
D. e(logn) for insertion and O(n) for deletion 4 $ D

**Type:** MCQ

**Answer:** VERIFICATION REQUIRED

**Source:** GATE 2015 CS, 7 February Shift 1, `12-PYQ/2015/set-01/question-paper.pdf`

---

### Q.27

**Paper:** GATE 2015 CS, 8 February Shift 1

**Question:**

While inserting the elements 71, 65, 84, 69, 67, 83 in an empty binary search tree (BST) in the
sequence shown, the element in the lowest level is

**Options:**

A. 65
B. 67
C. 69
D. 83 Options : 2.VB 3. % C 4. % D

**Type:** MCQ

**Answer:** VERIFICATION REQUIRED

**Source:** GATE 2015 CS, 8 February Shift 1, `12-PYQ/2015/set-03/question-paper.pdf`

---

## 2014

### Q.39

**Paper:** GATE 2014 CS SET-3

**Question:**

Suppose we have a balanced binary search tree ܶ  holding  numbers.  We are given two
numbers  ܮ and  ܪ and wish to sum up all the numbers in ܶ  that lie between  ܮ and  ܪ.
Suppose there are  such numbers in  .  If the tightest upper bound  on the time to
compute the sum is ܱ(݊^{௔} log^{௕} + ݉^{௖} log^{ௗ} ), the value of  + 10ܾ+ 100ܿ+ 1000݀  is
____.

**Options:**

The paper does not print options for this numerical-answer question.

**Type:** NAT

**Answer:** VERIFICATION REQUIRED

**Source:** GATE 2014 CS SET-3, `12-PYQ/2014/set-03/question-paper.pdf`

---

## 2013

### Q.7

**Paper:** GATE 2013 CS Booklet A

**Question:**

Which one of the following is the tightest upper bound that represents the time complexity of
inserting an object into a binary search tree of n nodes?

**Options:**

A. O(1)
B. O(log n)
C. O(n)
D. O(n log n) CS-A 2/20 2013COMPUTER SCIENCE & INFORMATION TECH. - CS

**Type:** MCQ

**Answer:** VERIFICATION REQUIRED

**Source:** GATE 2013 CS Booklet A, `12-PYQ/2013/set-01/question-paper.pdf`

---

### Q.43

**Paper:** GATE 2013 CS Booklet A

**Question:**

The preorder traversal sequence of a binary search tree is 30, 20, 10, 15, 25, 23, 39, 35, 42. Which
one of the following is the postorder traversal sequence of the same tree?

**Options:**

A. 10, 20, 15, 23, 25, 35, 42, 39, 30
B. 15, 10, 25, 23, 20, 42, 35, 39, 30
C. 15, 20, 10, 23, 25, 42, 35, 39, 30
D. 15, 10, 23, 25, 20, 35, 42, 39, 30

**Type:** MCQ

**Answer:** VERIFICATION REQUIRED

**Source:** GATE 2013 CS Booklet A, `12-PYQ/2013/set-01/question-paper.pdf`

---

### Q.19

**Paper:** GATE 2013 CS Booklet B

**Question:**

Which one of the following is the tightest upper bound that represents the time complexity of
inserting an object into a binary search tree of n nodes?

**Options:**

A. O(1)
B. O(log n)
C. O(n)
D. O(n log n)

**Type:** MCQ

**Answer:** VERIFICATION REQUIRED

**Source:** GATE 2013 CS Booklet B, `12-PYQ/2013/set-02/question-paper.pdf`

---

### Q.30

**Paper:** GATE 2013 CS Booklet B

**Question:**

The preorder traversal sequence of a binary search tree is 30, 20, 10, 15, 25, 23, 39, 35, 42. Which
one of the following is the postorder traversal sequence of the same tree?

**Options:**

A. 10, 20, 15, 23, 25, 35, 42, 39, 30
B. 15, 10, 25, 23, 20, 42, 35, 39, 30
C. 15, 20, 10, 23, 25, 42, 35, 39, 30
D. 15, 10, 23, 25, 20, 35, 42, 39, 30

**Type:** MCQ

**Answer:** VERIFICATION REQUIRED

**Source:** GATE 2013 CS Booklet B, `12-PYQ/2013/set-02/question-paper.pdf`

---

### Q.6

**Paper:** GATE 2013 CS Booklet C

**Question:**

Which one of the following is the tightest upper bound that represents the time complexity of
inserting an object into a binary search tree of n nodes?

**Options:**

A. O(1)
B. O(log n)
C. O(n)
D. O(n log n)

**Type:** MCQ

**Answer:** VERIFICATION REQUIRED

**Source:** GATE 2013 CS Booklet C, `12-PYQ/2013/set-03/question-paper.pdf`

---

### Q.41

**Paper:** GATE 2013 CS Booklet C

**Question:**

The preorder traversal sequence of a binary search tree is 30, 20, 10, 15, 25, 23, 39, 35, 42. Which
one of the following is the postorder traversal sequence of the same tree?

**Options:**

A. 10, 20, 15, 23, 25, 35, 42, 39, 30
B. 15, 10, 25, 23, 20, 42, 35, 39, 30
C. 15, 20, 10, 23, 25, 42, 35, 39, 30
D. 15, 10, 23, 25, 20, 35, 42, 39, 30

**Type:** MCQ

**Answer:** VERIFICATION REQUIRED

**Source:** GATE 2013 CS Booklet C, `12-PYQ/2013/set-03/question-paper.pdf`

---

### Q.20

**Paper:** GATE 2013 CS Booklet D

**Question:**

Which one of the following is the tightest upper bound that represents the time complexity of
inserting an object into a binary search tree of n nodes?

**Options:**

A. O(1)
B. O(log n)
C. O(n)
D. O(n log n) CS- D 4/20 2013COMPUTER SCIENCE & INFORMATION TECH. - CS

**Type:** MCQ

**Answer:** VERIFICATION REQUIRED

**Source:** GATE 2013 CS Booklet D, `12-PYQ/2013/set-04/question-paper.pdf`

---

### Q.32

**Paper:** GATE 2013 CS Booklet D

**Question:**

The preorder traversal sequence of a binary search tree is 30, 20, 10, 15, 25, 23, 39, 35, 42. Which
one of the following is the postorder traversal sequence of the same tree?

**Options:**

A. 10, 20, 15, 23, 25, 35, 42, 39, 30
B. 15, 10, 25, 23, 20, 42, 35, 39, 30
C. 15, 20, 10, 23, 25, 42, 35, 39, 30
D. 15, 10, 23, 25, 20, 35, 42, 39, 30

**Type:** MCQ

**Answer:** VERIFICATION REQUIRED

**Source:** GATE 2013 CS Booklet D, `12-PYQ/2013/set-04/question-paper.pdf`

---

## 2012

### Q.5

**Paper:** GATE 2012 CS Booklet A

**Question:**

The worst case running time to search for an element in a balanced binary search tree with n2^{n}
elements is

**Options:**

A. Θ (n log n)
B. Θ (n2^{n})
C. Θ (n)
D. Θ (log n) CS-A 2/20 2012 COMPUTER SCIENCE & INFORMATION TECH. – CS

**Type:** MCQ

**Answer:** VERIFICATION REQUIRED

**Source:** GATE 2012 CS Booklet A, `12-PYQ/2012/question-paper.pdf`

---

## 2011

### Q.29

**Paper:** GATE 2011 CS Booklet A

**Question:**

We are given a set of n distinct elements and an unlabeled binary tree with n nodes. In how many
ways can we populate the tree with the given set so that it becomes a binary search tree?

**Options:**

A. 0
B. 1
C. n!
D. it. ''C„

**Type:** MCQ

**Answer:** VERIFICATION REQUIRED

**Source:** GATE 2011 CS Booklet A, `12-PYQ/2011/question-paper.pdf`

---

## 2009

### Q.37

**Paper:** GATE 2009 CS

**Question:**

What is the maximum height of any AVL-tree with 7 nodes ? Assume that the height of a tree with a
single node is 0.

**Options:**

A. 2
B. 3
C. 4
D. 5

**Type:** MCQ

**Answer:** VERIFICATION REQUIRED

**Source:** GATE 2009 CS, `12-PYQ/2009/question-paper.pdf`

---

## 2008

### Q.46

**Paper:** GATE 2008 CS

**Question:**

You are given the postorder traversal, P, of a binary search tree on the n elements 1,2,...,n. You
have to determine the unique binary search tree that has P as its postorder traversal. What is the
time complexity of the most efficient algorithm for doing this?

**Options:**

A. O(logn)
B. O(n)
C. ©(nlogn)
D. none of the above, as the tree cannot be uniquely determined.

**Type:** MCQ

**Answer:** VERIFICATION REQUIRED

**Source:** GATE 2008 CS, `12-PYQ/2008/question-paper.pdf`

---
