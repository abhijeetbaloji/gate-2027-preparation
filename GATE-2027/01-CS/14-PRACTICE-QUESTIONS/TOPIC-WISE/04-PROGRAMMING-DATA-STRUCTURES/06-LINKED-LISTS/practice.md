# Linked Lists — Practice Questions

Original practice for GATE CS. These questions are not from any GATE paper. Attempt the questions before reading the solutions.

A singly linked node has a key and a `next` pointer. A doubly linked node also has a `prev` pointer. Unless a question says the list is circular, the last node’s `next` pointer is NULL, and the list is reached through a head pointer.

## Level 1 — Conceptual

## Q1 — NAT

The list `10 → 20 → 30 → NULL` contains how many nodes?

---

## Q2 — MCQ

A new node is inserted at the front of a non-empty singly linked list. The new node’s `next` pointer and the head pointer are both updated. How many of those two pointer writes are required?

A. 1

B. 2

C. 3

D. 4

---

## Q3 — MCQ

In a singly linked list with only a head pointer, the time to reach the node at position `i`, counting the head as position 1, is

A. `Θ(1)`

B. `Θ(i)`

C. `Θ(log i)`

D. `Θ(i log i)`

---

## Q4 — MCQ

Deleting the last node of a singly linked list of `n` nodes, when the only external pointer is the head, takes

A. `Θ(1)` time

B. `Θ(n)` time

C. `Θ(log n)` time

D. `Θ(n log n)` time

---

## Level 2 — Standard GATE Style

## Q5 — NAT

How many nodes in `5 → 1 → 5 → 2 → 5` store the key 5?

---

## Q6 — NAT

The list `1 → 2 → 3 → 4` is reversed by the usual pointer-reversal loop. After the reversal, the key in position 2, counting the new head as position 1, is ____.

---

## Q7 — MCQ

Floyd’s cycle check moves a slow pointer one node at a time and a fast pointer two nodes at a time, both starting at the head. If the two pointers meet on a node, which conclusion is correct?

A. The list is empty.

B. The list contains a cycle.

C. The keys are sorted.

D. The list contains no cycle.

---

## Q8 — NAT

A new node is inserted immediately after a given node in a doubly linked list. The given node is not the last node. How many pointer fields, among `next` and `prev` fields, are written to splice the new node in?

---

## Level 3 — Multi-Step

## Q9 — NAT

The list `1 → 2 → 3` is concatenated in front of the list `4 → 5` by making the node 3 point at the node 4. The length of the resulting list is ____.

---

## Q10 — MCQ

`head` in `main` points at a non-empty list. The call is `del_first(head)`.

```c
void del_first(struct Node *head) {
    if (head != NULL)
        head = head->next;
}
```

Which statement is correct?

A. After the call, the caller’s `head` points at the old second node.

B. The caller’s `head` is unchanged, because the function receives a copy of the pointer.

C. The function frees every node.

D. The function reverses the list.

---

## Q11 — NAT

The sorted list `1 → 4 → 9` receives the key 6 in the unique position that keeps the list sorted. The 1-based position of 6 after insertion is ____.

---

## Level 4 — Tricky / Trap-Based

## Q12 — MSQ

`n` points at a newly created node whose key is already set. Select all that apply. Which functions make the caller’s head point at `n`, with `n` followed by the old list?

A. ```c
void A(struct Node **head, struct Node *n) {
    n->next = *head;
    *head = n;
}
```

B. ```c
void B(struct Node **head, struct Node *n) {
    *head = n;
    n->next = *head;
}
```

C. ```c
void C(struct Node *head, struct Node *n) {
    n->next = head;
    head = n;
}
```

D. ```c
void D(struct Node **head, struct Node *n) {
    struct Node *old = *head;
    n->next = old;
    *head = n;
}
```

---

## Q13 — MCQ

A circular singly linked list contains the nodes 1, 2, and 3. The `next` pointer of 3 points back at 1, and there is no NULL pointer. A loop that starts at 1 and continues while the current pointer is not NULL

A. visits three nodes and stops

B. does not terminate

C. visits one node and stops

D. is rejected because a circular list cannot be represented in C

---

## Q14 — NAT

In the list `8 → 6 → 4 → 2`, the node immediately after the node whose key is 6 is deleted. The sum of the keys that remain is ____.

---

## Level 5 — Challenge

## Q15 — NAT

This function reverses a non-empty NULL-terminated singly linked list and returns the new head.

```c
struct Node *reverse(struct Node *h) {
    struct Node *p = h, *q = NULL, *r;
    while (p != NULL) {
        r = q;
        q = p;
        p = p->next;
        q->next = r;
    }
    return q;
}
```

The input list is `7 → 3 → 9 → 1`. The key of the second node in the returned list is ____.

---

## Q16 — NAT

Two sorted NULL-terminated lists, `1 → 4 → 8` and `2 → 3 → 9`, are merged into one sorted list. The sum of the keys in the merged list is ____.

## Answer Key

| Q | Type | Answer |
|---|------|--------|
| 1 | NAT | 3 |
| 2 | MCQ | (B) |
| 3 | MCQ | (B) |
| 4 | MCQ | (B) |
| 5 | NAT | 3 |
| 6 | NAT | 3 |
| 7 | MCQ | (B) |
| 8 | NAT | 4 |
| 9 | NAT | 5 |
| 10 | MCQ | (B) |
| 11 | NAT | 3 |
| 12 | MSQ | (A), (D) |
| 13 | MCQ | (B) |
| 14 | NAT | 16 |
| 15 | NAT | 9 |
| 16 | NAT | 27 |

## Detailed Solutions

### Q1

Answer: 3

The nodes store 10, 20, and 30. The NULL pointer terminates the list and is not a node. The length is 3.

### Q2

Answer: (B)

Let the old head be `H`. The new node’s `next` pointer must be set to `H`, and the head pointer must then be set to the new node. Those are two writes. Doing only one of them either loses the old list or fails to publish the new head. An empty list is the special case in which the new `next` pointer is NULL, but this question starts with a non-empty list and still needs both writes.

### Q3

Answer: (B)

From the head, the only way forward is to follow `next` once per node. Reaching position `i` follows `i - 1` links, which is `Θ(i)`. A singly linked list does not support jumping to an arbitrary position in constant time.

### Q4

Answer: (B)

The last node can be unlinked only after the traversal has found its predecessor. With only the head pointer, finding that predecessor inspects `Θ(n)` nodes. A pointer to the last node, or a doubly linked list with such a pointer, would make the deletion `Θ(1)`, but that extra pointer is not given.

### Q5

Answer: 3

The keys are 5, 1, 5, 2, and 5. The key 5 occurs in the first, third, and fifth nodes, so the count is 3.

### Q6

Answer: 3

Pointer reversal makes each node point at the node that previously preceded it. The old tail becomes the head. The list becomes `4 → 3 → 2 → 1`. Position 1 is 4, and position 2 is 3.

### Q7

Answer: (B)

In a NULL-terminated list with no cycle, the fast pointer reaches NULL and the walk stops. If there is a cycle, both pointers eventually remain inside that cycle, and the faster pointer gains one step per iteration relative to the slower one, so they meet. A meeting is therefore evidence of a cycle. It says nothing about the order of the keys.

### Q8

Answer: 4

Let the given node be `P`, and let `S` be `P->next`, which exists because `P` is not last. The new node `N` needs `N->next = S` and `N->prev = P`. The old neighbors must also turn toward `N`: `S->prev = N` and `P->next = N`. Those are four pointer writes. Setting `P->next` before saving `S` would lose the rest of the list, so the old successor is read before that write.

### Q9

Answer: 5

The first list contributes 3 nodes and the second contributes 2. Connecting 3 to 4 does not allocate or delete a node, so the length is 5. The head of the result is the node 1.

### Q10

Answer: (B)

The parameter `head` is a copy of the pointer value stored in `main`. Assigning to that parameter changes the copy inside `del_first` and does not change the variable in `main`. The caller’s head still points at the original first node. Updating the caller requires either a `struct Node **` parameter, with an assignment through it, or a returned pointer that `main` stores back into its head variable. The function also does not free a node or rewrite any `next` pointer.

### Q11

Answer: 3

The sorted order is `1 → 4 → 6 → 9`. The new key is after 1 and 4, so its 1-based position is 3. The insertion point is the first node whose key is greater than 6, and the new node is placed before that node.

### Q12

Answer: (A), (D)

(A) saves the old head in `n->next` and then publishes `n`. (D) does the same thing with an explicit temporary. Both leave the caller’s head at `n`, followed by the old list.

(B) publishes `n` first. The assignment `n->next = *head` then stores `n` into `n->next`, because `*head` is already `n`. The new node forms a one-node cycle, and the old list is no longer reachable from the head.

(C) receives `head` by value. It correctly points `n` at the old list, but `head = n` updates only the function’s copy. The caller’s head variable does not change.

### Q13

Answer: (B)

The continuation test asks whether the current pointer is NULL. In this circular list every `next` pointer refers to a node, so the test never fails and the loop does not terminate. A circular traversal needs a different stop: for example, walk until the next step would return to the starting node, and count that start only once. The three-node circle itself is a valid C structure.

### Q14

Answer: 16

The node after 6 is 4. Deleting 4 leaves `8 → 6 → 2`. The remaining sum is `8 + 6 + 2 = 16`. Deleting 6 itself would leave `8 → 4 → 2`, whose sum is 14. The question deletes the successor, not the node that was used to find it.

### Q15

Answer: 9

The loop walks `p` down the old list. At each node, `q` becomes that node and its `next` pointer is turned around to the previous node, saved in `r`.

- Start: `q` is NULL and `p` is 7.
- Process 7: `q` becomes 7, `p` becomes 3, and `7->next` becomes NULL.
- Process 3: `q` becomes 3, `p` becomes 9, and `3->next` becomes 7.
- Process 9: `q` becomes 9, `p` becomes 1, and `9->next` becomes 3.
- Process 1: `q` becomes 1, `p` becomes NULL, and `1->next` becomes 9.

The returned head is 1, and the list is `1 → 9 → 3 → 7`. The second key is 9.

### Q16

Answer: 27

Merge by always taking the smaller current head. The choices are 1 (from the first list), 2, 3 (from the second), 4, 8 (from the first), and 9 (from the second). The merged list is `1 → 2 → 3 → 4 → 8 → 9`. The sum is `1 + 2 + 3 + 4 + 8 + 9 = 27`. Every key of both inputs appears once.
