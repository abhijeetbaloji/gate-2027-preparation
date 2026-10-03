# GATE PYQs

## 2026

### Q.17

**Paper:** GATE 2026 CS-2 (afternoon)

**Question:**

In C runtime environment, which one of the following is stored in heap?

**Options:**

A. A static variable declared inside a function
B. An array of integers declared inside a function
C. A dynamically allocated array of integers created using malloc() function call
D. Return address of a function

**Type:** MCQ

**Answer:** VERIFICATION REQUIRED

**Source:** GATE 2026 CS-2 (afternoon), `12-PYQ/2026/set-02/question-paper.pdf`

---

### Q.32

**Paper:** GATE 2026 CS-2 (afternoon)

**Question:**

Consider an array 𝐴= [10, 7, 8,  19, 41, 35, 25, 31]. Suppose the merge sort
algorithm is executed on array  𝐴 to sort it in increasing order. The merge sort
algorithm will carry out a total of 7 merge operations.
A merge operation on sorted left array 𝐿 and sorted right array 𝑅 is said to be void
if the output of the merge operation is the elements of array  𝐿 followed by the
elements of array 𝑅.
The number of void merge operations among these 7 merge operations
is __________. (answer in integer)

**Options:**

The paper does not print options for this numerical-answer question.

**Type:** NAT

**Answer:** VERIFICATION REQUIRED

**Source:** GATE 2026 CS-2 (afternoon), `12-PYQ/2026/set-02/question-paper.pdf`

---

### Q.38

**Paper:** GATE 2026 CS-2 (afternoon)

**Question:**

Consider an array  𝐴 of integers of size  𝑛. The indices of  𝐴 run from  1 to 𝑛. An
algorithm is to be designed to check whether 𝐴 satisfies the condition given below.
∀𝑖, 𝑗∈{1, … , 𝑛−1} such that 𝑖> 𝑗, (𝐴[𝑖+ 1] −𝐴[𝑖]) > (𝐴[𝑗+ 1] −𝐴[𝑗])
Which one of the following gives the worst case time complexity of the fastest
algorithm that can be designed for the problem?

**Options:**

A. Θ(𝑛)
B. Θ(log(𝑛))
C. Θ(𝑛 log(𝑛))
D. Θ(𝑛^{2})

**Type:** MCQ

**Answer:** VERIFICATION REQUIRED

**Source:** GATE 2026 CS-2 (afternoon), `12-PYQ/2026/set-02/question-paper.pdf`

---

## 2025

### Q.33

**Paper:** GATE 2025 CS-1

**Question:**

The pseudocode of a function fun() is given below:
fun(int A[0,…,n-1]){
for i=0 to n-2
for j=0 to n-i-2
if (A[j]>A[j+1])
then swap A[j] and A[j+1]
}
Let 𝐴[0, … ,29] be an array storing 30 distinct integers in descending order. The
number of swap operations that will be performed, if the function fun() is called
with 𝐴[0, … ,29] as argument, is __________. (Answer in integer)

**Options:**

The paper does not print options for this numerical-answer question.

**Type:** NAT

**Answer:** VERIFICATION REQUIRED

**Source:** GATE 2025 CS-1, `12-PYQ/2025/set-01/question-paper.pdf`

---

### Q.41

**Paper:** GATE 2025 CS-2

**Question:**

An array 𝐴 of length 𝑛 with distinct elements is said to be bitonic if there is an index
1 ≤𝑖≤𝑛 such that 𝐴[1. . 𝑖] is sorted in the non-decreasing order and 𝐴[𝑖+ 1 . . 𝑛]
is sorted in the non-increasing order.
Which ONE of the following represents the best possible asymptotic bound for the
worst-case number of comparisons by an algorithm that searches for an element in
a bitonic array 𝐴?

**Options:**

A. Θ(𝑛)
B. Θ(1)
C. Θ(log^{2} 𝑛)
D. Θ(log 𝑛)

**Type:** MCQ

**Answer:** VERIFICATION REQUIRED

**Source:** GATE 2025 CS-2, `12-PYQ/2025/set-02/question-paper.pdf`

---

## 2024

### Q.17

**Paper:** GATE 2024 CS1

**Question:**

Given an integer array of size N, we want to check if the array is sorted (in either
ascending or descending order). An algorithm solves this problem by making a
single pass through the array and comparing each element of the array only with its
adjacent elements. The worst-case time complexity of this algorithm is

**Options:**

A. both Ο(𝑁) and Ω(𝑁)
B. Ο(𝑁) but not Ω(𝑁)
C. Ω(𝑁) but not Ο(𝑁)
D. neither Ο(𝑁) nor Ω(𝑁)

**Type:** MCQ

**Answer:** VERIFICATION REQUIRED

**Source:** GATE 2024 CS1, `12-PYQ/2024/set-01/question-paper.pdf`

---

### Q.41

**Paper:** GATE 2024 CS1

**Question:**

An array [82, 101, 90, 11, 111, 75, 33, 131, 44, 93] is heapified. Which one of the
following options represents the first three elements in the heapified array?

**Options:**

A. 82, 90, 101
B. 82, 11, 93
C. 131, 11, 93
D. 131, 111, 90

**Type:** MCQ

**Answer:** VERIFICATION REQUIRED

**Source:** GATE 2024 CS1, `12-PYQ/2024/set-01/question-paper.pdf`

---

### Q.33

**Paper:** GATE 2024 CS2

**Question:**

Consider the following C function definition.
int fX(char *a){
char *b = a;
while(*b)
b++;
return b - a;}
Which of the following statements is/are TRUE?

**Options:**

A. The function call fX(”abcd”) will always return a value Assuming a character array c is declared as char c[] = ”abcd” in main(),
B. the function call fX(c)will always return a value
C. The code of the function will not compile
D. Assuming a character pointer c is declared as char *c = ”abcd” in main(), the function call fX(c)will always return a value

**Type:** MCQ

**Answer:** VERIFICATION REQUIRED

**Source:** GATE 2024 CS2, `12-PYQ/2024/set-02/question-paper.pdf`

---

### Q.35

**Paper:** GATE 2024 CS2

**Question:**

Let  𝐴⁡be an array containing integer values. The distance of  𝐴 is defined as the
minimum number of elements in 𝐴 that must be replaced with another integer so
that the resulting array is sorted in non-decreasing order. The distance of the array
[2, 5, 3, 1, 4, 2, 6] is ___________

**Options:**

The paper does not print options for this numerical-answer question.

**Type:** NAT

**Answer:** VERIFICATION REQUIRED

**Source:** GATE 2024 CS2, `12-PYQ/2024/set-02/question-paper.pdf`

---

### Q.41

**Paper:** GATE 2024 CS2

**Question:**

Let 𝑀 be the 5-state NFA with 𝜖-transitions shown in the diagram below.
Which one of the following regular expressions represents the language accepted
by 𝑀 ?

**Options:**

A. ⁡(00)^{∗} ⁡+ ⁡1(11)^{∗}
B. ⁡0^{∗} + (1 + 0(00)^{∗})(11)^{∗}⁡
C. ⁡(00)^{∗} + (1 + (00)^{∗})(11)^{∗}⁡
D. ⁡0^{+} + 1(11)^{∗} + 0(11)^{∗}⁡ Consider an array X that contains n positive integers. A subarray of X is defined to

**Type:** MCQ

**Answer:** VERIFICATION REQUIRED

**Source:** GATE 2024 CS2, `12-PYQ/2024/set-02/question-paper.pdf`

---

### Q.42

**Paper:** GATE 2024 CS2

**Question:**

be a sequence of array locations with consecutive indices.
The C code snippet given below has been written to compute the length of the
longest subarray of X that contains at most two distinct integers. The code has two
missing expressions labelled (𝑃)⁡and (𝑄).
int first=0, second=0, len1=0, len2=0, maxlen=0;
for (int i=0; i < n; i++) {
if (X[i] == first) {
len2++; len1++;
} else if (X[i] == second) {
len2++;
len1 = ⁡⁡⁡⁡⁡(𝑃)⁡⁡⁡⁡⁡⁡⁡;
second = first;
} else {
len2 = ⁡⁡⁡⁡⁡(𝑄)⁡⁡⁡⁡⁡⁡;
len1 = 1; second = first;
}
if (len2 > maxlen) {
maxlen = len2;
}
first = X[i];
}
Which one of the following options gives the CORRECT missing expressions?
(Hint: At the end of the i-th iteration, the value of len1 is the length of the longest
subarray ending with X[i] that contains all equal values, and len2 is the length
of the longest subarray ending with X[i] that contains at most two distinct values.)

**Options:**

A. (𝑃) len1+1 (𝑄) len2+1
B. (𝑃) 1 (𝑄) len1+1
C. (𝑃) 1 (𝑄) len2+1
D. (𝑃) len2+1 (𝑄) len1+1

**Type:** MCQ

**Answer:** VERIFICATION REQUIRED

**Source:** GATE 2024 CS2, `12-PYQ/2024/set-02/question-paper.pdf`

---

## 2021

### Q.2

**Paper:** GATE 2021 CS Set-1

**Question:**

Let P be an array containing n integers. Let t be the lowest upper bound on the
number of comparisons of the array elements, required to find the minimum and
maximum values in an arbitrary array of n elements. Which one of the following
choices is correct?

**Options:**

A. |t > 2n -2
B. +>3 5|andt ≤2n-2 (0) t> n andt ≤3 5l
D. t > [logz(n)] andt ≤n GATE Graduate Aptitude Test in Engineering 2021 2021 Organising Institute - IIT Bombay

**Type:** MCQ

**Answer:** VERIFICATION REQUIRED

**Source:** GATE 2021 CS Set-1, `12-PYQ/2021/set-01/question-paper.pdf`

---

### Q.9

**Paper:** GATE 2021 CS Set-1

**Question:**

Consider the following array.
23 32 45 69 72 738997
Which algorithm out of the following options uses the least number of comparisons
(among the array elements) to sort the above array in ascending order?

**Options:**

A. Selection sort
B. Mergesort
C. Insertion sort
D. | Quicksort using the last element as pivot

**Type:** MCQ

**Answer:** VERIFICATION REQUIRED

**Source:** GATE 2021 CS Set-1, `12-PYQ/2021/set-01/question-paper.pdf`

---

### Q.40

**Paper:** GATE 2021 CS Set-1

**Question:**

Define Rn to be the maximum amount earned by cutting a rod of length n meters
into one or more pieces of integer length and selling them. For i > 0, let p[i]
denote the selling price of a rod whose length is i meters. Consider the array of
prices:
p[1] = 1, p|2] = 5, p [3] = 8, p[4] = 9, p[5] = 10, p[6] = 17,p[7] = 18
Which of the following statements is/are correct about R-?

**Options:**

A. Rт =18
B. Ry = 19
C. R- is achieved by three different solutions.
D. R- cannot be achieved by a solution consisting of three pieces.

**Type:** MSQ

**Answer:** VERIFICATION REQUIRED

**Source:** GATE 2021 CS Set-1, `12-PYQ/2021/set-01/question-paper.pdf`

---

### Q.48

**Paper:** GATE 2021 CS Set-1

**Question:**

Consider the following ANSI C funetion:
int SimpleFunction(int Y[], int n, int x)
int total = Y[O], loopIndex;
for (loopIndex = 1; loopIndex <= n - 1; loopIndex++)
total = x * total + Y[loopIndex];
return total;
}
Let Z be an array of 10 elements with Z[i] =1, for all i such that 0 ≤ i ≤ 9. The
value returned by SimpleFunction(Z, 10, 2) is .

**Options:**

The paper does not print options for this numerical-answer question.

**Type:** NAT

**Answer:** VERIFICATION REQUIRED

**Source:** GATE 2021 CS Set-1, `12-PYQ/2021/set-01/question-paper.pdf`

---

### Q.8

**Paper:** GATE 2021 CS Set-2

**Question:**

What is the worst-case number ofarithmetic operations performed by recursive
binary search on a sorted array of size n?

**Options:**

A. L - {01}
B. LU {01}
C. {0,1)* - L
D. L.L GATE Graduate Aptitude Test in Engineering 2021 2021 Organising Institute - IIT Bombay

**Type:** MCQ

**Answer:** VERIFICATION REQUIRED

**Source:** GATE 2021 CS Set-2, `12-PYQ/2021/set-02/question-paper.pdf`

---

## 2019

### Q.20

**Paper:** GATE 2019 CS (printed header Set-2)

**Question:**

An array of 25 distinct elements is to be sorted using quicksort. Assume that the pivot
element is chosen uniformly at random. The probability that the pivot element gets placed in
the worst possible location in the first round of partitioning (rounded off to 2 decimal places)
1S

**Options:**

The paper does not print options for this numerical-answer question.

**Type:** NAT

**Answer:** VERIFICATION REQUIRED

**Source:** GATE 2019 CS (printed header Set-2), `12-PYQ/2019/question-paper.pdf`

---

## 2017

### Q.43

**Paper:** GATE 2017 CS Session 2

**Question:**

Correct : 2 Wrong : 0
Consider the following snippet of a C program. Assume that swap (&x, &y) exchanges the
contents of x and y.
int main () {
int arrayl] = (3, 5, 1, 4, 6, 2ł;
int done = 0;
int i;
while (done == 0) {
done = 1;
for (i=0; i<=4; it+) {
if (arrayli] < array[itl])ł
swap (darraylil, darraylitl]);
done = 0;
for (i=5; i>=l; i--)
if (array[i] > array[i-l]) {
swap (&array[il, darray[i-l]);
done = 0;
}
printf("%d", array[3]);
}
The output of the program is

**Options:**

The paper does not print options for this numerical-answer question.

**Type:** NAT

**Answer:** VERIFICATION REQUIRED

**Source:** GATE 2017 CS Session 2, `12-PYQ/2017/set-02/question-paper.pdf`

---

## 2016

### Q.34

**Paper:** GATE 2016 CS-1

**Question:**

The following function computes the maximum value contained in an integer array p[] of size
n (n >= 1).
int max(int *p, int n) {
int a=0, b=n-1;
while (__________) {
if (p[a] <= p[b]) { a = a+1; }
else  { b = b-1; }
}
return p[a];
}
The missing loop condition is

**Options:**

A. a != n
B. b != 0
C. b > (a + 1)
D. b != a

**Type:** MCQ

**Answer:** VERIFICATION REQUIRED

**Source:** GATE 2016 CS-1, `12-PYQ/2016/set-01/question-paper.pdf`

---

### Q.46

**Paper:** GATE 2016 CS-2

**Question:**

A student wrote two context-free grammars G1 and G2 for generating a single C-like array
declaration. The dimension of the array is at least one. For example,
int a[10][3];
The grammars use D as the start symbol, and use six terminal symbols int ; id [ ] num.
Grammar G1  Grammar G2
D → int L;  D → int L;
L → id [E  L → id E
E → num]  E → E[num]
E → num][E  E → [num]
Which of the grammars correctly generate the declaration mentioned above?

**Options:**

A. Both G1 and G2
B. Only G1
C. Only G2
D. Neither G1 nor G2

**Type:** MCQ

**Answer:** VERIFICATION REQUIRED

**Source:** GATE 2016 CS-2, `12-PYQ/2016/set-02/question-paper.pdf`

---

## 2015

### Q.38

**Paper:** GATE 2015 CS, 7 February Shift 1

**Question:**

Consider the following C program segment.
while (first <= last)
if (array[middle] < search)
first = middle + 1;
else if (array[middle] == search)
found = TRUE;
else last = middle - 1;
middle = (first + last)/2;
if (first > last) notPresent = TRUE;
The cyclomatic complexity of the program segment is _
Correct Answer :

**Options:**

The paper does not print options for this numerical-answer question.

**Type:** NAT

**Answer:** VERIFICATION REQUIRED

**Source:** GATE 2015 CS, 7 February Shift 1, `12-PYQ/2015/set-01/question-paper.pdf`

---

### Q.47

**Paper:** GATE 2015 CS, 7 February Shift 2

**Question:**

Given below are some algorithms, and some algorithm design paradigms.
1. Dijkstra's Shortest Path i. Divide and Conquer
2. Floyd-Warshall algorithm to compute all ii. Dynamic Programming
paurs shortest path
3. Binary search on a sorted array iii. Greedy design
4. Backtracking search on a graph iv. Depth-first search
v. Breadth-first search
Match the above algorithms on the left to the corresponding design paradigm they follow.

**Options:**

A. 1-i, 2-1ii, 3-i, 4-v.
B. 1-iii, 2-iii, 3-i, 4-v.
C. 1-iii, 2-ii, 3-i, 4-iv.
D. 1-iїi, 2-ii, 3-i, 4-v.

**Type:** MCQ

**Answer:** VERIFICATION REQUIRED

**Source:** GATE 2015 CS, 7 February Shift 2, `12-PYQ/2015/set-02/question-paper.pdf`

---

### Q.48

**Paper:** GATE 2015 CS, 7 February Shift 2

**Question:**

A Young tableau is a 2D array of integers increasing from left to right and from top to bottom. Any
unfilled entries are marked with oo, and hence there cannot be any entry to the right of, or below a
0o. The following Young tableau consists of unique entries.
12 14
3 4 23
10 12 18 25
31| 00 00 00
When an element is removed from a Young tableau, other elements should be moved into its place
so that the resulting table is still a Young tableau (unfilled entries may be filled in with a oo). The
minimum number of entries (other than 1) to be shifted, to remove 1 from the given Young tableau
is
Correct Answer :

**Options:**

The paper does not print options for this numerical-answer question.

**Type:** NAT

**Answer:** VERIFICATION REQUIRED

**Source:** GATE 2015 CS, 7 February Shift 2, `12-PYQ/2015/set-02/question-paper.pdf`

---

### Q.49

**Paper:** GATE 2015 CS, 7 February Shift 2

**Question:**

Suppose you are provided with the following function declaration in the C programming language.
int partition (int all, int n);
The function treats the first element of a [] as a pivot, and rearranges the array so that all elements
less than or equal to the pivot is in the left part of the array, and all elements greater than the pivot
is in the right part. In addition, it moves the pivot so that the pivot is the last element of the left part.
The return value is the number of elements in the lett part.
The following partially given function in the C programming language is used to find the kth
smallest element in an array a [] of size n using the partition function. We assume k ≤ n.
int kth_smallest (int all, int n, int k)
int left_end = partition (a,n);
if ( left _end+1 ==k) {
return alleft_endl;
if ( left endt1 > k ) {
return kth _smallest( );
} else {
return kth_smallest( _ );
}
The mussing argument lists are respectively

**Options:**

A. (a, left _end, k) and latleft_ _endt1, n-left_end-1, k-left_end-1)
B. (a, left_end, k) and (a, n-left_end-1, k-left_end-1)
C. (atleft_endt1, n-left_end-1, k-left_end-1) and (a, left_end, k)
D. (a, n-lēft_end-1, k-left_end-1) and Ta, left_end, k)

**Type:** MCQ

**Answer:** VERIFICATION REQUIRED

**Source:** GATE 2015 CS, 7 February Shift 2, `12-PYQ/2015/set-02/question-paper.pdf`

---

### Q.63

**Paper:** GATE 2015 CS, 8 February Shift 1

**Question:**

3

Suppose c = (c[O], .., c[k - 1]) is an array of length k, where all the entries are from the set (0, 1).
For any positive integers a and n, consider the following pseudocode.
DOSOMETHING (c, a, n)
z+1
for i-0to k-1
do z- z' modn
if c[i] = 1
then z + (zxa) mod n
return z
If k = 4, c = (1,0, 1,1), a = 2 and n = 8, then the output of DOSOMETHING(c, a, n) is
Correct Answer :

**Options:**

The paper does not print options for this numerical-answer question.

**Type:** NAT

**Answer:** VERIFICATION REQUIRED

**Source:** GATE 2015 CS, 8 February Shift 1, `12-PYQ/2015/set-03/question-paper.pdf`

---

## 2014

### Q.41

**Paper:** GATE 2014 CS SET-1

**Question:**

Consider the following C function in which size is the number of elements in the array E:
int MyX(int *E, unsigned int size)
{
int Y = 0;
int Z;
int i, j, k;
CS01 (GATE 2014)  for(i = 0; i < size; i++)
Y = Y + E[i];
for(i = 0; i < size; i++)
for(j = i; j < size; j++)
{
Z = 0;
for(k = i; k <= j; k++)
Z = Z + E[k];
if (Z > Y)
Y = Z;
}
return Y;
}
The value returned by the function MyX is the

**Options:**

A. maximum possible sum of elements in any sub-array of array E.
B. maximum element in any sub-array of array E.
C. sum of the maximum elements in all possible sub-arrays of array E.
D. the sum of all the elements in the array E.

**Type:** MCQ

**Answer:** VERIFICATION REQUIRED

**Source:** GATE 2014 CS SET-1, `12-PYQ/2014/set-01/question-paper.pdf`

---

### Q.14

**Paper:** GATE 2014 CS SET-3

**Question:**

You have an array of n elements. Suppose you implement quicksort by always choosing the central
element of the array as the pivot. Then the tightest upper bound for the worst case performance is

**Options:**

A. ܱ(݊^{ଶ})
B. ܱ(݊log݊)
C. Θ(݊log݊)
D. ܱ(݊^{ଷ})

**Type:** MCQ

**Answer:** VERIFICATION REQUIRED

**Source:** GATE 2014 CS SET-3, `12-PYQ/2014/set-03/question-paper.pdf`

---

### Q.42

**Paper:** GATE 2014 CS SET-3

**Question:**

Consider the C function given below. Assume that the array  listA contains  n (> 0) elements,
sorted in ascending order.
int ProcessArray(int *listA, int x, int n)
{
int i, j, k;
i = 0;
j = n-1;
do {
CS03 (GATE 2014)  k = (i+j)/2;  if (x <= listA[k])
j = k-1;
if (listA[k] <= x)
i = k+1;
}while (i <= j);
if (listA[k] == x)
return(k);
else
return -1;
}
Which one of the following statements about the function ProcessArray is CORRECT?

**Options:**

A. It will run into an infinite loop when x is not in listA.
B. It is an implementation of binary search.
C. It will always find the maximum element in listA.
D. It will return −1 even when x is present in listA.

**Type:** MCQ

**Answer:** VERIFICATION REQUIRED

**Source:** GATE 2014 CS SET-3, `12-PYQ/2014/set-03/question-paper.pdf`

---

## 2013

### Q.39

**Paper:** GATE 2013 CS Booklet A

**Question:**

A certain computation generates two arrays  a  and  b such that  a[i]=f(i)for 0  ≤ i < n  and
b[i] = g (a[i] )for 0 ≤ i < n. Suppose this computation is decomposed into two concurrent processes
X and Y such that X computes the array a and Y computes the array b. The processes employ two
binary semaphores R and S, both initialized to zero. The array a is shared by the two processes. The
structures of the processes are shown below.
Process X:  Process Y:
private i;  private i;
for (i=0; i<n; i++) {  for (i=0; i<n; i++) {
a[i] = f(i);  EntryY(R, S);
ExitX(R, S);  b[i] = g(a[i]);
}  }
Which one of the following represents the CORRECT implementations of ExitX and EntryY?

**Options:**

A. ExitX(R, S) {
B. ExitX(R, S) { P(R); V(R); V(S); V(S); } } EntryY(R, S) { EntryY(R, S) { P(S); P(R); V(R); P(S); } }
C. ExitX(R, S) {
D. ExitX(R, S) { P(S); V(R); V(R); P(S); } } EntryY(R, S) { EntryY(R, S) { V(S); V(S); P(R); P(R); } }

**Type:** MCQ

**Answer:** VERIFICATION REQUIRED

**Source:** GATE 2013 CS Booklet A, `12-PYQ/2013/set-01/question-paper.pdf`

---

### Q.34

**Paper:** GATE 2013 CS Booklet B

**Question:**

A certain computation generates two arrays  a  and  b such that  a[i]=f(i)for 0  ≤ i < n  and
b[i] = g (a[i] )for 0 ≤ i < n. Suppose this computation is decomposed into two concurrent processes
X and Y such that X computes the array a and Y computes the array b. The processes employ two
binary semaphores R and S, both initialized to zero. The array a is shared by the two processes. The
structures of the processes are shown below.
Process X:  Process Y:
private i;  private i;
for (i=0; i<n; i++) {  for (i=0; i<n; i++) {
a[i] = f(i);  EntryY(R, S);
ExitX(R, S);  b[i] = g(a[i]);
}  }
Which one of the following represents the CORRECT implementations of ExitX and EntryY?

**Options:**

A. ExitX(R, S) {
B. ExitX(R, S) { P(R); V(R); V(S); V(S); } } EntryY(R, S) { EntryY(R, S) { P(S); P(R); V(R); P(S); } }
C. ExitX(R, S) {
D. ExitX(R, S) { P(S); V(R); V(R); P(S); } } EntryY(R, S) { EntryY(R, S) { V(S); V(S); P(R); P(R); } } CS-B 7/20 2013COMPUTER SCIENCE & INFORMATION TECH. - CS

**Type:** MCQ

**Answer:** VERIFICATION REQUIRED

**Source:** GATE 2013 CS Booklet B, `12-PYQ/2013/set-02/question-paper.pdf`

---

### Q.47

**Paper:** GATE 2013 CS Booklet B

**Question:**

What is the logical translation of the following statement?
“None of my friends are perfect.”

**Options:**

A. ∃ x (F ( x)∧ ¬ P ( x))
B. ∃ x (¬ F ( x)∧ P ( x))
C. ∃ x (¬ F ( x)∧ ¬ P ( x))
D. ¬∃ x (F ( x)∧ P ( x)) CS-B 10/20 2013COMPUTER SCIENCE & INFORMATION TECH. - CS Common Data Questions Common Data for Questions 48 and 49: The procedure given below is required to find and replace certain characters inside an input character string supplied in array A. The characters to be replaced are supplied in array oldc, while their respective replacement characters are supplied in array newc. Array A has a fixed length of five characters, while arrays oldc and newc contain three characters each. However, the procedure is flawed. void find_and_replace (char *A, char *oldc, char *newc) { for (int i=0; i<5; i++) for (int j=0; j<3; j++) if (A[i] == oldc[j]) A[i] = newc[j]; } The procedure is tested with the following four test cases. (1) oldc = “abc”, newc = “dab” (2) oldc = “cde”, newc = “bcd” (3) oldc = “bca”, newc = “cda” (4) oldc = “abc”, newc = “bac”

**Type:** MCQ

**Answer:** VERIFICATION REQUIRED

**Source:** GATE 2013 CS Booklet B, `12-PYQ/2013/set-02/question-paper.pdf`

---

### Q.49

**Paper:** GATE 2013 CS Booklet B

**Question:**

If array A is made to hold the string “abcde”, which of the above four test cases will be successful
in exposing the flaw in this procedure?

**Options:**

A. None
B. 2 only
C. 3 and 4 only
D. 4 only Common Data for Questions 50 and 51: The following code segment is executed on a processor which allows only register operands in its instructions. Each instruction can have atmost two source operands and one destination operand. Assume that all variables are dead after this code segment. c = a + b; d = c * a; e = c + a; x = c * c; if (x > a) { y = a * a; } else { d = d * d; e = e * e; }

**Type:** MCQ

**Answer:** VERIFICATION REQUIRED

**Source:** GATE 2013 CS Booklet B, `12-PYQ/2013/set-02/question-paper.pdf`

---

### Q.45

**Paper:** GATE 2013 CS Booklet C

**Question:**

A certain computation generates two arrays  a  and  b such that  a[i]=f(i)for 0  ≤ i < n  and
b[i] = g (a[i] )for 0 ≤ i < n. Suppose this computation is decomposed into two concurrent processes
X and Y such that X computes the array a and Y computes the array b. The processes employ two
binary semaphores R and S, both initialized to zero. The array a is shared by the two processes. The
structures of the processes are shown below.
Process X:  Process Y:
private i;  private i;
for (i=0; i<n; i++) {  for (i=0; i<n; i++) {
a[i] = f(i);  EntryY(R, S);
ExitX(R, S);  b[i] = g(a[i]);
}  }
Which one of the following represents the CORRECT implementations of ExitX and EntryY?

**Options:**

A. ExitX(R, S) {
B. ExitX(R, S) { P(R); V(R); V(S); V(S); } } EntryY(R, S) { EntryY(R, S) { P(S); P(R); V(R); P(S); } }
C. ExitX(R, S) {
D. ExitX(R, S) { P(S); V(R); V(R); P(S); } } EntryY(R, S) { EntryY(R, S) { V(S); V(S); P(R); P(R); } } CS- C 10/20 2013COMPUTER SCIENCE & INFORMATION TECH. - CS

**Type:** MCQ

**Answer:** VERIFICATION REQUIRED

**Source:** GATE 2013 CS Booklet C, `12-PYQ/2013/set-03/question-paper.pdf`

---

### Q.50

**Paper:** GATE 2013 CS Booklet C

**Question:**

If array A is made to hold the string “abcde”, which of the above four test cases will be successful
in exposing the flaw in this procedure?

**Options:**

A. None
B. 2 only
C. 3 and 4 only
D. 4 only

**Type:** MCQ

**Answer:** VERIFICATION REQUIRED

**Source:** GATE 2013 CS Booklet C, `12-PYQ/2013/set-03/question-paper.pdf`

---

### Q.28

**Paper:** GATE 2013 CS Booklet D

**Question:**

A certain computation generates two arrays  a  and  b such that  a[i]=f(i)for 0  ≤ i < n  and
b[i] = g (a[i] )for 0 ≤ i < n. Suppose this computation is decomposed into two concurrent processes
X and Y such that X computes the array a and Y computes the array b. The processes employ two
binary semaphores R and S, both initialized to zero. The array a is shared by the two processes. The
structures of the processes are shown below.
Process X:  Process Y:
private i;  private i;
for (i=0; i<n; i++) {  for (i=0; i<n; i++) {
a[i] = f(i);  EntryY(R, S);
ExitX(R, S);  b[i] = g(a[i]);
}  }
Which one of the following represents the CORRECT implementations of ExitX and EntryY?

**Options:**

A. ExitX(R, S) {
B. ExitX(R, S) { P(R); V(R); V(S); V(S); } } EntryY(R, S) { EntryY(R, S) { P(S); P(R); V(R); P(S); } }
C. ExitX(R, S) {
D. ExitX(R, S) { P(S); V(R); V(R); P(S); } } EntryY(R, S) { EntryY(R, S) { V(S); V(S); P(R); P(R); } }

**Type:** MCQ

**Answer:** VERIFICATION REQUIRED

**Source:** GATE 2013 CS Booklet D, `12-PYQ/2013/set-04/question-paper.pdf`

---

### Q.47

**Paper:** GATE 2013 CS Booklet D

**Question:**

Determine the maximum length of the cable (in km) for transmitting data at a rate of 500 Mbps in
an Ethernet LAN with frames of size 10,000 bits. Assume the signal speed in the cable to be
2,00,000 km/s.

**Options:**

A. 1
B. 2
C. 2.5
D. 5 CS- D 10/20 2013COMPUTER SCIENCE & INFORMATION TECH. - CS Common Data Questions Common Data for Questions 48 and 49: The procedure given below is required to find and replace certain characters inside an input character string supplied in array A. The characters to be replaced are supplied in array oldc, while their respective replacement characters are supplied in array newc. Array A has a fixed length of five characters, while arrays oldc and newc contain three characters each. However, the procedure is flawed. void find_and_replace (char *A, char *oldc, char *newc) { for (int i=0; i<5; i++) for (int j=0; j<3; j++) if (A[i] == oldc[j]) A[i] = newc[j]; } The procedure is tested with the following four test cases. (1) oldc = “abc”, newc = “dab” (2) oldc = “cde”, newc = “bcd” (3) oldc = “bca”, newc = “cda” (4) oldc = “abc”, newc = “bac”

**Type:** MCQ

**Answer:** VERIFICATION REQUIRED

**Source:** GATE 2013 CS Booklet D, `12-PYQ/2013/set-04/question-paper.pdf`

---

### Q.48

**Paper:** GATE 2013 CS Booklet D

**Question:**

If array A is made to hold the string “abcde”, which of the above four test cases will be successful
in exposing the flaw in this procedure?

**Options:**

A. None
B. 2 only
C. 3 and 4 only
D. 4 only

**Type:** MCQ

**Answer:** VERIFICATION REQUIRED

**Source:** GATE 2013 CS Booklet D, `12-PYQ/2013/set-04/question-paper.pdf`

---

## 2011

### Q.25

**Paper:** GATE 2011 CS Booklet A

**Question:**

An algorithm to find the length of the longest monotonically increasing sequence of numbers in an
array A[O:n-1] is given below.
Let L, denote the length of the longest monotonically increasing sequence starting at index i in
the array.
Initialize L,-1 =1.
Forall i such that0≤ i ≤n-2
L,=. JI+L if Ali]<A[i+1]
1 Otherwise
Finally the length of the longest monotonically increasing sequence is Max (4o, 4....,Ln-1).
Which of the following statements is TRUE?

**Options:**

B. The algorithm us a dynanic prperaimaing peadiranch and bound paradiem
C. The algorithm has a non-linear polynomial complexity and uses branch and bound paradiem
D. The algorithm uses divide and conquer paradigm. CS-A 6/20 2011 CS

**Type:** MCQ

**Answer:** VERIFICATION REQUIRED

**Source:** GATE 2011 CS Booklet A, `12-PYQ/2011/question-paper.pdf`

---

## 2009

### Q.54

**Paper:** GATE 2009 CS

**Question:**

The values of ((i,j) could be obtained by dynamic programming based on the correct recursive
definition of ((i,j) of the form given above, using an array L[M,N], where M = m + 1 and
N = n + 1, such that L[i,İ] = ((i,j).
Which one the following statements would be TRUE regarding the dynamic programming solution for
the recursive definition of ((i,j)?

**Options:**

A. All elements of L should be initialized to 0 for the values of ((i,j) to be properly computed.
B. The values of I(i, j) may be computed in a row major order or column major order of L[M, N].
C. The values of ((i,j) cannot be computed in either row major order or column major order of L[M,N] .
D. L[p, q] needs to be computed before L[r, s] if either p‹r or g‹s. 12/16 2009 Common Data for Questions 55 and 56: Consider the following relational schema : Suppliers(sid: integer, sname:string, city:string, street:string) Parts(pid:integer, pname:string, color:string) Catalog(sid:integer, pid:integer, cost:real)

**Type:** MCQ

**Answer:** VERIFICATION REQUIRED

**Source:** GATE 2009 CS, `12-PYQ/2009/question-paper.pdf`

---

## 2008

### Q.40

**Paper:** GATE 2008 CS

**Question:**

The minimum number of comparisons required to determine if an integer appears more than n /2
times in a sorted array of n integers is

**Options:**

A. O(n)
B. O(logn)
C. O(log' n)
D. O(1)

**Type:** MCQ

**Answer:** VERIFICATION REQUIRED

**Source:** GATE 2008 CS, `12-PYQ/2008/question-paper.pdf`

---

### Q.79

**Paper:** GATE 2008 CS

**Question:**

The value of x, is

**Options:**

A. 5
B. 7
C. 8
D. 16 Statement for Linked Answer Questions 80 and 81: The subset-sum problem is defined as follows. Given a set of n positive integers, S ={a,,az,a,.....a„), and a positive integer W, is there a subset of S whose elements sum to W? A dynamic program for solving this problem uses a 2-dimensional Boolean array, X, with n rows and W+1 columns. X[i,j]. I≤i≤n, 0≤ j ≤W, is TRUE if and only if there is a subset of {a,,az,...,a,) whose elements sum to j.

**Type:** MCQ

**Answer:** VERIFICATION REQUIRED

**Source:** GATE 2008 CS, `12-PYQ/2008/question-paper.pdf`

---

### Q.81

**Paper:** GATE 2008 CS

**Question:**

Which entry of the array X, if TRUE, implies that there is a subset whose elements sum to W?

**Options:**

A. X[1,W]
B. X [n,0]
C. x [»,W]
D. X[n-l,n] 17/24 2008 MAIN PAPER - CS Statement for Linked Answer Questions 82 and 83: Consider the following ER diagram M R1 R2 N

**Type:** MCQ

**Answer:** VERIFICATION REQUIRED

**Source:** GATE 2008 CS, `12-PYQ/2008/question-paper.pdf`

---

### Q.83

**Paper:** GATE 2008 CS

**Question:**

Which of the following is a correct attribute set for one of the tables for the correct answer to the
above question?

**Options:**

A. (M1, M2, M3, P1}
B. (M1, P1, N1, N2}
C. (M1, P1, N1)
D. (MI, P1} Statement for Linked Answer Questions 84 and 85: Consider the following C program that attempts to locate an element x in an array Y [ ] using binary search. The program is erroneous. 1. f (int Y[10], int x) { 2. int i, j, k; 3. i = 0; j = 9; 4. do { 5. k = (i+j)/2; 6. if (Y[k] < x) i = k; else j = k; 7. ) while ((Y[k] != x) && (i < j)); 8. if (Y[k] == x) printf("x is in the array"); 9. else printf("x is not in the array"); 10. }

**Type:** MCQ

**Answer:** VERIFICATION REQUIRED

**Source:** GATE 2008 CS, `12-PYQ/2008/question-paper.pdf`

---
