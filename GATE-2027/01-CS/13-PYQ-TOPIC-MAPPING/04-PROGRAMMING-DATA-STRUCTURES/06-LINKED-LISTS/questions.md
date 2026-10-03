# GATE PYQs

## 2026

### Q.39

**Paper:** GATE 2026 CS-1 (forenoon)

**Question:**

Consider the following code snippet in C language that computes the number of
nodes in a non-empty singly linked list pointed to by the pointer variable head.
struct node{
int elt;
struct node *next;
};
int getListSize (struct node *head)
{
if( E1 ) return 1;
return E2;
}
Which one of the following options gives the correct replacements for the
expressions E1 and E2?

**Options:**

A. E1: head == NULL E2: 1 + getListSize(head)
B. E1: head->next == NULL E2: 1 + getListSize(head->next)
C. E1: head == NULL E2: 1 + getListSize(head->next)
D. E1: head->next == NULL E2: 1 + getListSize(head)

**Type:** MCQ

**Answer:** VERIFICATION REQUIRED

**Source:** GATE 2026 CS-1 (forenoon), `12-PYQ/2026/set-01/question-paper.pdf`

---

## 2025

### Q.62

**Paper:** GATE 2025 CS-1

**Question:**

Let LIST be a datatype for an implementation of linked list defined as follows:
typedef struct list {
int data;
struct list *next;
} LIST;
Suppose a program has created two linked lists, L1 and L2, whose contents are given
in the figure below (code for creating L1 and L2 is not provided here). L1 contains 9
nodes, and L2 contains 7 nodes.
Consider the following C program segment that modifies the list L1. The number of
nodes that will be there in L1 after the execution of the code segment is ________ .
(Answer in integer)
int find (int query, LIST *list) {
while (list != NULL){
if(list->data == query) return 1;
list = list->next;
}
return 0;
}
int main () {
… … …
ptr1=L1; ptr2=L2;
while (ptr1->next != NULL){
query = ptr1->next->data;
if (find (query, L2))
ptr1->next = ptr1->next->next;
else ptr1 = ptr1->next;
}
… … …
return 0;
}

**Options:**

The paper does not print options for this numerical-answer question.

**Type:** NAT

**Answer:** VERIFICATION REQUIRED

**Source:** GATE 2025 CS-1, `12-PYQ/2025/set-01/question-paper.pdf`

---

## 2023

### Q.13

**Paper:** GATE 2023 CS

**Question:**

Let SLLdel be a function that deletes a node in a singly-linked list given a pointer
to the node and a pointer to the head of the list. Similarly, let DLLdel be another
function that deletes a node in a doubly-linked list given a pointer to the node and
a pointer to the head of the list.
Let n denote the number of nodes in each of the linked lists. Which one of the
following choices is TRUE about the worst-case time complexity of SLLdel and
DLLdel?

**Options:**

A. SLLdel is O(1) and DLLdel is O(n)
B. Both SLLdel and DLLdel are O(log(n))
C. Both SLLdel and DLLdel are O(1)
D. SLLdel is O(n) and DLLdel is O(1)

**Type:** MCQ

**Answer:** VERIFICATION REQUIRED

**Source:** GATE 2023 CS, `12-PYQ/2023/question-paper.pdf`

---

## 2022

### Q.15

**Paper:** GATE 2022 CS

**Question:**

Consider the problem of reversing a singly linked list. To take an example, given
the linked list below,
the reversed linked list should look like
Which one of the following statements is TRUE about the time complexity of
algorithms that solve the above problem in  O(1)  space?

**Options:**

A. The best algorithm for the problem takes ( n) time in the worst case.
B. The best algorithm for the problem takes ( n log n) time in the worst case.
C. The best algorithm for the problem takes (n^{2}) time in the worst case.
D. It is not possible to reverse a singly linked list in O(1) space.

**Type:** MCQ

**Answer:** VERIFICATION REQUIRED

**Source:** GATE 2022 CS, `12-PYQ/2022/question-paper.pdf`

---

## 2020

### Q.16

**Paper:** GATE 2020 CS

**Question:**

What is the worst case time complexity of inserting n elements into an empty
linked list, if the linked list needs to be maintained in sorted order?

**Options:**

A. 0(n)
B. 0(nlogn) () 0(n2)
D. 0(1)

**Type:** MCQ

**Answer:** VERIFICATION REQUIRED

**Source:** GATE 2020 CS, `12-PYQ/2020/question-paper.pdf`

---

## 2018

### Q.3

**Paper:** GATE 2018 CS

**Question:**

A queue is implemented using a non-circular singly linked list. The queue has a head pointer
and a tail pointer, as shown in the figure. Let n denote the number of nodes in the queue. Let
enqueue be implemented by inserting a new node at the head, and  dequeue be
implemented by deletion of a node from the tail.
head  tail
Which one of the following is the time complexity of the most time-efficient implementation
of enqueue and dequeue, respectively, for this data structure?

**Options:**

A. θ(1), θ(1)
B. θ(1), θ(n)
C. θ(n), θ(1)
D. θ(n), θ(n)

**Type:** MCQ

**Answer:** VERIFICATION REQUIRED

**Source:** GATE 2018 CS, `12-PYQ/2018/question-paper.pdf`

---

## 2017

### Q.13

**Paper:** GATE 2017 CS Session 2

**Question:**

Correct: 1 Wrong:-0.33
A circular queue has been implemented using a singly linked list where each node consists of a
value and a single pointer pointing to the next node. We maintain exactly two external pointers
FRONT and REAR pointing to the front node and the rear node of the queue, respectively. Which of
the following statements is/are CORRECT for such a circular queue, so that insertion and deletion
operations can be performed in O(1) time?
I. Next pointer of front node points to the rear node.
II. Next pointer of rear node points to the front node.

**Options:**

A. I only
B. II only
C. Both I and II
D. Neither I nor II

**Type:** MCQ

**Answer:** VERIFICATION REQUIRED

**Source:** GATE 2017 CS Session 2, `12-PYQ/2017/set-02/question-paper.pdf`

---

## 2016

### Q.15

**Paper:** GATE 2016 CS-2

**Question:**

N items are stored in a sorted doubly linked list. For a delete operation, a pointer is provided
to the record to be deleted. For a decrease-key operation, a pointer is provided to the record on
which the operation is to be performed.
An algorithm performs the following operations on the list in this order: Θ(N) delete, O(log N)
insert, O(log N) find, and Θ(N) decrease-key. What is the time complexity of all these
operations put together?

**Options:**

A. O(log^{2} N)
B. O(N)
C. O(N^{2})
D. Θ(N^{2} log N)

**Type:** MCQ

**Answer:** VERIFICATION REQUIRED

**Source:** GATE 2016 CS-2, `12-PYQ/2016/set-02/question-paper.pdf`

---

## 2008

### Q.62

**Paper:** GATE 2008 CS

**Question:**

The following C function takes a singly-linked list of integers as a parameter and rearranges the
elements of the list. The function is called with the list containing the integers 1,2,3,4,5,6, 7 in the
given order. What will be the contents of the list after the function completes execution?
struct node {
int value;
struct node *next;
} :
void rearrange (struct node *list){
struct node *p, *q;
int temp;
if (!list | !list -> next) return;
p = list; q = list -> next;
while (q) (
temp = p -> value; P -> value = q -> value;
q -> value = temp; p = q -> next;
q = p ? p -> next : 0;
}

**Options:**

A. 1,2,3,4,5,6,7
B. 2,1,4,3,6,5,7
C. 1,3,2,5,4,7,6
D. 2,3,4,5,6,7,1 12/24 2008 MAIN PAPER -CS

**Type:** MCQ

**Answer:** VERIFICATION REQUIRED

**Source:** GATE 2008 CS, `12-PYQ/2008/question-paper.pdf`

---
