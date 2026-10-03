# GATE PYQs

## 2026

### Q.23

**Paper:** GATE 2026 CS-1 (forenoon)

**Question:**

Let  𝑛 be an odd number greater than 100. Consider a binary minheap with
𝑛 elements stored in an array 𝑃 whose index starts from 1.
Which of the following indices of 𝑃 do/does NOT correspond to any leaf node of
the minheap?

**Options:**

A. 𝑛+ 1 2
B. 𝑛−1 2
C. 𝑛−3 2
D. 𝑛

**Type:** MCQ

**Answer:** VERIFICATION REQUIRED

**Source:** GATE 2026 CS-1 (forenoon), `12-PYQ/2026/set-01/question-paper.pdf`

---

## 2025

### Q.26

**Paper:** GATE 2025 CS-1

**Question:**

Which of the following statement(s) is/are TRUE for any binary search tree (BST)
having 𝑛 distinct integers?

**Options:**

A. The maximum length of a path from the root node to any other node is (𝑛−1).
B. An inorder traversal will always produce a sorted sequence of elements.
C. Finding an element takes 𝑂(log_{2} 𝑛) time in the worst case.
D. Every BST is also a Min-Heap.

**Type:** MCQ

**Answer:** VERIFICATION REQUIRED

**Source:** GATE 2025 CS-1, `12-PYQ/2025/set-01/question-paper.pdf`

---

### Q.35

**Paper:** GATE 2025 CS-1

**Question:**

The height of any rooted tree is defined as the maximum number of edges in the
path from the root node to any leaf node.
Suppose a Min-Heap 𝑇 stores 32 keys. The height of 𝑇 is _____________.
(Answer in integer)

**Options:**

The paper does not print options for this numerical-answer question.

**Type:** NAT

**Answer:** VERIFICATION REQUIRED

**Source:** GATE 2025 CS-1, `12-PYQ/2025/set-01/question-paper.pdf`

---

### Q.38

**Paper:** GATE 2025 CS-2

**Question:**

A meld operation on two instances of a data structure combines them into one single
instance of the same data structure. Consider the following data structures:
P: Unsorted doubly linked list with pointers to the head node and tail node
of the list.
Q: Min-heap implemented using an array.
R: Binary Search Tree.
Which ONE of the following options gives the worst-case time complexities for
meld operation on instances of size 𝑛 of these data structures?

**Options:**

A. P: Θ(1), Q: Θ(𝑛), R: Θ(𝑛)
B. P: Θ(1), Q: Θ(𝑛log 𝑛), R: Θ(𝑛)
C. P: Θ(𝑛), Q: Θ(𝑛log 𝑛), R: Θ(𝑛^{2})
D. P: Θ(1), Q: Θ(𝑛), R: Θ(𝑛log 𝑛)

**Type:** MCQ

**Answer:** VERIFICATION REQUIRED

**Source:** GATE 2025 CS-2, `12-PYQ/2025/set-02/question-paper.pdf`

---

### Q.45

**Paper:** GATE 2025 CS-2

**Question:**

Consider a stack data structure into which we can PUSH and POP records. Assume
that each record pushed in the stack has a positive integer key and that all keys are
distinct.
We wish to augment the stack data structure with an 𝑂(1) time MIN operation that
returns a pointer to the record with smallest key present in the stack
1)  without deleting the corresponding record, and
2)  without increasing the complexities of the standard stack operations.
Which one or more of the following approach(es) can achieve it?

**Options:**

A. Keep with every record in the stack, a pointer to the record with the smallest key below it.
B. Keep a pointer to the record with the smallest key in the stack.
C. Keep an auxiliary array in which the key values of the records in the stack are maintained in sorted order.
D. Keep a Min-Heap in which the key values of the records in the stack are maintained.

**Type:** MSQ

**Answer:** VERIFICATION REQUIRED

**Source:** GATE 2025 CS-2, `12-PYQ/2025/set-02/question-paper.pdf`

---

## 2024

### Q.43

**Paper:** GATE 2024 CS1

**Question:**

Consider a binary min-heap containing 105 distinct elements. Let 𝑘 be the index (in
the underlying array) of the maximum element stored in the heap. The number of
possible values of 𝑘 is

**Options:**

A. 53
B. 52
C. 27
D. 1

**Type:** MCQ

**Answer:** VERIFICATION REQUIRED

**Source:** GATE 2024 CS1, `12-PYQ/2024/set-01/question-paper.pdf`

---

## 2023

### Q.12

**Paper:** GATE 2023 CS

**Question:**

Which one of the following sequences when stored in an array at locations
A[1], . . . , A[10] forms a max-heap?

**Options:**

A. 23, 17, 10, 6, 13, 14, 1, 5, 7, 12
B. 23, 17, 14, 7, 13, 10, 1, 5, 6, 12
C. 23, 17, 14, 6, 13, 10, 1, 5, 7, 15
D. 23, 14, 17, 1, 10, 13, 16, 12, 7, 5

**Type:** MCQ

**Answer:** VERIFICATION REQUIRED

**Source:** GATE 2023 CS, `12-PYQ/2023/question-paper.pdf`

---

### Q.46

**Paper:** GATE 2023 CS

**Question:**

Let A be a priority queue for maintaining a set of elements. Suppose A is
implemented using a max-heap data structure. The operation Extract-Max(A)
extracts and deletes the maximum element from A. The operation Insert(A,key)
inserts a new element key in A. The properties of a max-heap are preserved at the
end of each of these operations.
When A contains n elements, which one of the following statements about the worst
case running time of these two operations is TRUE?

**Options:**

A. runs in O(1) whereas Insert(A,key) runs in O(log(n)).
B. Both Extract-Max
C. Extract-Max
D. Extract-Max

**Type:** MCQ

**Answer:** VERIFICATION REQUIRED

**Source:** GATE 2023 CS, `12-PYQ/2023/question-paper.pdf`

---

## 2022

### Q.28

**Paper:** GATE 2022 CS

**Question:**

Suppose a binary search tree with 1000 distinct elements is also a complete binary
tree. The tree is stored using the array representation of binary heap trees. Assuming
that the array indices start with 0, the 3^{rd}  largest element of the tree is stored at
index_____________.

**Options:**

The paper does not print options for this numerical-answer question.

**Type:** NAT

**Answer:** VERIFICATION REQUIRED

**Source:** GATE 2022 CS, `12-PYQ/2022/question-paper.pdf`

---

## 2021

### Q.2

**Paper:** GATE 2021 CS Set-2

**Question:**

Let H be a binary min-heap consisting of n elements implemented as an array. What
is the worst case time complexity of an optimal algorithm to find the maximum
element in H?

**Options:**

A. |0(1)
B. e(logn)
C. e(n)
D. e(nlogn) GATE Graduate Aptitude Test in Engineering 2021 2021 Organising Institute - IIT Bombay

**Type:** MCQ

**Answer:** VERIFICATION REQUIRED

**Source:** GATE 2021 CS Set-2, `12-PYQ/2021/set-02/question-paper.pdf`

---

## 2020

### Q.47

**Paper:** GATE 2020 CS

**Question:**

Consider the array representation of a binary min-heap containing 1023 elements.
The minimum number of comparisons required to find the maximum in the heap

**Options:**

The paper does not print options for this numerical-answer question.

**Type:** NAT

**Answer:** VERIFICATION REQUIRED

**Source:** GATE 2020 CS, `12-PYQ/2020/question-paper.pdf`

---

## 2019

### Q.40

**Paper:** GATE 2019 CS (printed header Set-2)

**Question:**

Consider the following statements:
I. The smallest element in a max-heap is always at a leaf node
II. The second largest element in a max-heap is always a child of the root node
III. A max-heap can be constructed from a binary search tree in O(n) time
IV. A binary search tree can be constructed from a max-heap in O(n) time
Which of the above statements are TRUE?

**Options:**

A. I, II and III
B. I, II and IV
C. I, III and IV
D. II, III and IV

**Type:** MCQ

**Answer:** VERIFICATION REQUIRED

**Source:** GATE 2019 CS (printed header Set-2), `12-PYQ/2019/question-paper.pdf`

---

## 2018

### Q.46

**Paper:** GATE 2018 CS

**Question:**

The number of possible min-heaps containing each value from {1, 2, 3, 4, 5, 6, 7}exactly once
is _____.

**Options:**

The paper does not print options for this numerical-answer question.

**Type:** NAT

**Answer:** VERIFICATION REQUIRED

**Source:** GATE 2018 CS, `12-PYQ/2018/question-paper.pdf`

---

## 2017

### Q.3

**Paper:** GATE 2017 CS Session 2

**Question:**

Correct : 1 Wrong : -0.33
Match the algorithms with their time complexities:
Algorithm Time complexity
(P) Towers of Hanoi with n disks (i) 0(n2)
(Q) Binary search given n sorted numbers (11) ©(n logn)
(R) Heap sort given n numbers at the worst case (iii) 0(2")
(S) Addition of two n X n matrices (iv) 0(logn)

**Options:**

A. P → (111), Q → (iv). R → (i), S → (11)
B. P → (iv), Q → (iiii), R → (i), S → (ii)
C. P → (i11). Q → (iv), R → (ii), S → (1)
D. P → (iv), Q → (iii), R → (ii), S → (i)

**Type:** MCQ

**Answer:** VERIFICATION REQUIRED

**Source:** GATE 2017 CS Session 2, `12-PYQ/2017/set-02/question-paper.pdf`

---

## 2016

### Q.37

**Paper:** GATE 2016 CS-1

**Question:**

An operator delete(i) for a binary heap data structure is to be designed to delete the item in
the i-th node. Assume that the heap is implemented in an array and i refers to the i-th index
of the array. If the heap tree has depth d (number of edges on the path from the root to the
farthest leaf), then what is the time complexity to re-fix the heap efficiently after the removal
of the element?

**Options:**

A. O(1)
B. O(d) but not O(1)
C. O(2^{d}) but not O(d)
D. O(d 2^{d}) but not O(2^{d})

**Type:** MCQ

**Answer:** VERIFICATION REQUIRED

**Source:** GATE 2016 CS-1, `12-PYQ/2016/set-01/question-paper.pdf`

---

### Q.34

**Paper:** GATE 2016 CS-2

**Question:**

A complete binary min-heap is made by including each integer in [1, 1023] exactly once.
The depth of a node in the heap is the length of the path from the root of the heap to that
node. Thus, the root is at depth 0. The maximum depth at which integer 9 can appear is

**Options:**

The paper does not print options for this numerical-answer question.

**Type:** NAT

**Answer:** VERIFICATION REQUIRED

**Source:** GATE 2016 CS-2, `12-PYQ/2016/set-02/question-paper.pdf`

---

## 2015

### Q.37

**Paper:** GATE 2015 CS, 7 February Shift 1

**Question:**

160

Consider a max heap, represented by the array: 40, 30, 20, 10, 15, 16, 17, 8, 4.
Array Index
Value
Now consider that a value 35 is inserted into this heap. After insertion, the new heap is

**Options:**

A. 40, 30, 20, 10, 15, 16, 17, 8, 4, 35
B. 40, 35, 20, 10, 30, 16, 17, 8, 4, 15
C. 40, 30, 20, 10, 35, 16, 17, 8, 4, 15
D. 40, 35, 20, 10, 15, 16, 17, 8, 4, 30 4 D

**Type:** MCQ

**Answer:** VERIFICATION REQUIRED

**Source:** GATE 2015 CS, 7 February Shift 1, `12-PYQ/2015/set-01/question-paper.pdf`

---

### Q.60

**Paper:** GATE 2015 CS, 7 February Shift 1

**Question:**

An algorithm performs (logN)find operations, Ninsert operations, (logN)/2delete
operations, and (1og N) decrease-key operations on a set of data items with keys drawn from a
linearly ordered set. For a delete operation, a pointer is provided to the record that must be deleted.
For the decrease-key operation, a pointer is provided to the record that has its key decreased. Which
one of the following data structures is the most suited for the algorithm to use, if the goal is to
achieve the best total asymptotic complexity considering all the operations?

**Options:**

A. Unsorted array
B. Min-heap
C. Sorted array
D. Sorted doubly linked list

**Type:** MCQ

**Answer:** VERIFICATION REQUIRED

**Source:** GATE 2015 CS, 7 February Shift 1, `12-PYQ/2015/set-01/question-paper.pdf`

---

### Q.22

**Paper:** GATE 2015 CS, 7 February Shift 2

**Question:**

Consider a complete binary tree where the left and the right subtrees of the root are max-heaps. The
lower bound for the number of operations to convert the tree to a heap is

**Options:**

A. 2(logn)
B. 2(n)
C. 2(nlogn)
D. 2(n2) 2 $ B 3. % C 4. D

**Type:** MCQ

**Answer:** VERIFICATION REQUIRED

**Source:** GATE 2015 CS, 7 February Shift 2, `12-PYQ/2015/set-02/question-paper.pdf`

---

### Q.30

**Paper:** GATE 2015 CS, 8 February Shift 1

**Question:**

Consider the following array of elements.
(89, 19, 50, 17, 12, 15, 2, 5, 7, 11, 6, 9, 100)
The minimum number of interchanges needed to convert it into a max-heap is

**Options:**

A. 4
B. 5
C. 2
D. 3

**Type:** MCQ

**Answer:** VERIFICATION REQUIRED

**Source:** GATE 2015 CS, 8 February Shift 1, `12-PYQ/2015/set-03/question-paper.pdf`

---

## 2014

### Q.12

**Paper:** GATE 2014 CS SET-2

**Question:**

A priority queue is implemented as a Max-Heap. Initially, it has 5 elements. The level-order
traversal of the heap is:  10, 8, 5, 3, 2. Two new elements 1 and 7 are inserted into the heap in that
order. The level-order traversal of the heap after the insertion of the elements is:

**Options:**

A. 10, 8, 7, 3, 2, 1, 5
B. 10, 8, 7, 2, 3, 1, 5
C. 10, 8, 7, 1, 2, 3, 5
D. 10, 8, 7, 5, 3, 2, 1 CS02 (GATE 2014)

**Type:** MCQ

**Answer:** VERIFICATION REQUIRED

**Source:** GATE 2014 CS SET-2, `12-PYQ/2014/set-02/question-paper.pdf`

---

## 2013

### Q.30

**Paper:** GATE 2013 CS Booklet A

**Question:**

The number of elements that can be sorted in Θ(log n) time using heap sort is

**Options:**

A. Θ(1)
B. Θ (_{log} n )
C. Θ  log n 
D. Θ(log n)  log log n  CS-A 6/20 2013COMPUTER SCIENCE & INFORMATION TECH. - CS

**Type:** MCQ

**Answer:** VERIFICATION REQUIRED

**Source:** GATE 2013 CS Booklet A, `12-PYQ/2013/set-01/question-paper.pdf`

---

### Q.43

**Paper:** GATE 2013 CS Booklet B

**Question:**

The number of elements that can be sorted in Θ(log n) time using heap sort is

**Options:**

A. Θ(1)
B. Θ (_{log} n )
C. Θ  log n 
D. Θ(log n)  log log n 

**Type:** MCQ

**Answer:** VERIFICATION REQUIRED

**Source:** GATE 2013 CS Booklet B, `12-PYQ/2013/set-02/question-paper.pdf`

---

### Q.32

**Paper:** GATE 2013 CS Booklet C

**Question:**

The number of elements that can be sorted in Θ(log n) time using heap sort is

**Options:**

A. Θ(1)
B. Θ (_{log} n )
C. Θ  log n 
D. Θ(log n)  log log n  CS- C 7/20 2013COMPUTER SCIENCE & INFORMATION TECH. - CS

**Type:** MCQ

**Answer:** VERIFICATION REQUIRED

**Source:** GATE 2013 CS Booklet C, `12-PYQ/2013/set-03/question-paper.pdf`

---

### Q.41

**Paper:** GATE 2013 CS Booklet D

**Question:**

The number of elements that can be sorted in Θ(log n) time using heap sort is

**Options:**

A. Θ(1)
B. Θ (_{log} n )
C. Θ  log n 
D. Θ(log n)  log log n 

**Type:** MCQ

**Answer:** VERIFICATION REQUIRED

**Source:** GATE 2013 CS Booklet D, `12-PYQ/2013/set-04/question-paper.pdf`

---

## 2011

### Q.23

**Paper:** GATE 2011 CS Booklet A

**Question:**

A max-heap is a heap where the value of each parent is greater than or equal to the value of its
children. Which of the following is a max-heap?

**Options:**

B. 10 5 U
D. 10

**Type:** MCQ

**Answer:** VERIFICATION REQUIRED

**Source:** GATE 2011 CS Booklet A, `12-PYQ/2011/question-paper.pdf`

---

## 2009

### Q.58

**Paper:** GATE 2009 CS

**Question:**

Suppose that the sliding window protocol is used with the sender window size of 2' , where is the
number of bits identified in the earlier part and acknowledgements are always piggy backed. After
sending 2' frames, what is the minimum time the sender will have to wait before starting transmission
of the next frame? (Identify the closest choice ignoring the frame processing time.)

**Options:**

A. 16ms
B. 18ms
C. 20ms
D. 22ms 2009 CS Statement for Linked Answer Questions 59 and 60: Consider a binary max-heap implemented using an array.

**Type:** MCQ

**Answer:** VERIFICATION REQUIRED

**Source:** GATE 2009 CS, `12-PYQ/2009/question-paper.pdf`

---

### Q.59

**Paper:** GATE 2009 CS

**Question:**

Which one of the following array represents a binary max-heap ?

**Options:**

A. ( 25, 12, 16, 13, 10, 8, 14 }
B. ( 25, 14, 13, 16, 10, 8, 12 }
C. { 25, 14, 16, 13, 10, 8, 12 }
D. ( 25, 14, 12, 13, 10, 8, 16 }

**Type:** MCQ

**Answer:** VERIFICATION REQUIRED

**Source:** GATE 2009 CS, `12-PYQ/2009/question-paper.pdf`

---

## 2008

### Q.47

**Paper:** GATE 2008 CS

**Question:**

We have a binary heap on n elements and wish to insert n more elements (not necessarily one after
another) into this heap. The total time required for this is

**Options:**

A. © (logn)
B. ®(n)
C. ©(nlogn)
D. ©(n')

**Type:** MCQ

**Answer:** VERIFICATION REQUIRED

**Source:** GATE 2008 CS, `12-PYQ/2008/question-paper.pdf`

---

## 2007

### Q.47

**Paper:** GATE 2007 CS

**Question:**

Consider the process of inserting an element into a Max Heap, where the Max Heap is
represented by an array. Suppose we perform a binary search on the path from the
new leaf to the root to find the position for the newly inserted element, the number of
comparisons performed is:

**Options:**

A. ©(log, n)
B. O(log, l0g, n)
C. O(n)
D. O(nlog, n)

**Type:** MCQ

**Answer:** VERIFICATION REQUIRED

**Source:** GATE 2007 CS, `12-PYQ/2007/question-paper.pdf`

---
