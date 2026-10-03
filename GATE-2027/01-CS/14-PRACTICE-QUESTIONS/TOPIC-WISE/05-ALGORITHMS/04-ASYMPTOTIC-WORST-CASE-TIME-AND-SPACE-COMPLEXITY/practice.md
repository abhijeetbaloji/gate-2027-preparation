# Asymptotic Worst-Case Time and Space Complexity — Practice Questions

Original practice for GATE CS. These questions are not from any GATE paper. Attempt the questions before reading the solutions.

## Level 1 — Conceptual

## Q1 — MCQ

Which relationship is true?

A. \(4^n = \Theta(2^n)\)

B. \(2^{n+1} = \Theta(2^n)\)

C. \(\log_2(n!) = \Theta(\log_2 n)\)

D. \((\log_2 n)^2 = \Theta(\log_2(n^2))\)

---

## Q2 — MSQ

Select all that apply. The functions are positive.

A. \(n = O(n^2)\) and \(n\) is not \(\Omega(n^2)\).

B. \(3n^2 + 5n + 7 = \Theta(n^2)\).

C. \(f = \Theta(g)\) implies \(g = \Theta(f)\), and \(f = O(g)\) implies \(g = O(f)\).

D. For any fixed base \(b > 1\), \(\log_b n = \Theta(\log_2 n)\).

---

## Q3 — NAT

The loop is

```
i = n
while i > 1:
    i = i // 2
```

How many iterations does it perform, as a \(\Theta\) class of \(n\)? Give the answer as one of 1, 2, or 3, where 1 means \(\Theta(1)\), 2 means \(\Theta(\log n)\), and 3 means \(\Theta(n)\).

---

## Q4 — MSQ

Select all that apply.

A. Worst-case time \(\Theta(n^2)\) means that the slowest input of size \(n\) costs on the order of \(n^2\), not less.

B. “The algorithm is \(O(n^2)\)” is a tight description of an algorithm whose worst case is \(\Theta(n)\).

C. Best-case \(\Theta(n)\) and worst-case \(\Theta(n^2)\) can both be true of one algorithm.

D. Average-case \(\Theta(n \log n)\) is an expectation under a stated input distribution. Amortised \(\Theta(1)\) is a total over a sequence of operations divided by the length of that sequence.

---

## Q5 — NAT

For \(n \ge 1\), the sum \(1 + 2 + \cdots + n\) is \(\Theta\) of which function? Answer \(1\) for \(\Theta(n)\), \(2\) for \(\Theta(n \log n)\), and \(3\) for \(\Theta(n^2)\).

---

## Level 2 — Standard GATE Style

## Q6 — MCQ

Solve \(T(n) = 2T(n/2) + n^2\), with \(T(1) = \Theta(1)\). The Master theorem applies with \(a = 2\), \(b = 2\). The solution is

A. \(\Theta(n \log n)\)

B. \(\Theta(n^2)\)

C. \(\Theta(n^2 \log n)\)

D. \(\Theta(n^3)\)

---

## Q7 — MCQ

Solve \(T(n) = 4T(n/2) + n^2\). State the Master case in the solution you rely on. The solution is

A. \(\Theta(n^2)\)

B. \(\Theta(n^2 \log n)\)

C. \(\Theta(n^4)\)

D. \(\Theta(n^{\log_2 4})\) with no extra logarithm, because \(f(n)\) is smaller than the critical power by a polynomial gap

---

## Q8 — MCQ

The nested loops are

```
for i = 1 to n:
    j = 1
    while j < n:
        j = j * 2
```

The body of the inner loop is \(\Theta(1)\). The total time is

A. \(\Theta(n)\)

B. \(\Theta(\log n)\)

C. \(\Theta(n \log n)\)

D. \(\Theta(n^2)\)

---

## Q9 — MSQ

Select all that apply. \(T(n) = T(n-1) + n\) and \(T(1) = \Theta(1)\).

A. The Master theorem applies with \(b = 1\).

B. Unrolling gives \(T(n) = \Theta(n^2)\).

C. This is the shape of quicksort when every pivot is extreme, and of insertion sort’s worst case.

D. \(T(n) = T(n-1) + 1\) has the same solution.

---

## Q10 — MCQ

A doubling array copies every stored element into a new buffer whenever the buffer is full, and the buffer size doubles. Over \(n\) insertions starting from a constant capacity, the total number of element copies is strictly less than \(2n\). The correct pair of claims is

A. each insertion is \(O(1)\) in the worst case, and the amortised cost is \(O(n)\)

B. the amortised cost of an insertion is \(O(1)\), and some single insertion costs \(\Theta(n)\)

C. both the worst case and the amortised cost of every insertion are \(\Theta(n)\)

D. the \(O(1)\) claim is an average over random insertion values, not a bound on every sequence

---

## Q11 — MSQ

Select all that apply. Auxiliary space is memory beyond the input.

A. Iterative binary search uses \(\Theta(1)\) auxiliary memory.

B. Recursive binary search uses \(\Theta(\log n)\) stack space in the worst case.

C. The merge buffer of top-down merge sort is \(\Theta(1)\).

D. A recursion of depth \(d\) with \(\Theta(1)\) local variables uses \(\Theta(d)\) stack space.

---

## Level 3 — Multi-Step

## Q12 — MCQ

Solve \(T(n) = 8T(n/2) + n^2\). Compare \(f(n) = n^2\) with \(n^{\log_2 8}\). The solution is

A. \(\Theta(n^2)\)

B. \(\Theta(n^2 \log n)\)

C. \(\Theta(n^3)\)

D. \(\Theta(n^{\log_2 7})\)

---

## Q13 — MCQ

Solve \(T(n) = 2T(n/4) + n\). Check the regularity condition before using case 3. The solution is

A. \(\Theta(\sqrt{n})\)

B. \(\Theta(n)\)

C. \(\Theta(n \log n)\)

D. \(\Theta(n^2)\)

---

## Q14 — MSQ

Select all that apply. \(T(n) = T(n/3) + T(2n/3) + \Theta(n)\), with a constant base case.

A. The Master theorem applies directly with a single \(b\).

B. A recursion tree has \(\Theta(\log n)\) levels along the longer branch, and every level costs \(\Theta(n)\), so \(T(n) = \Theta(n \log n)\).

C. The solution is \(\Theta(n)\), because the two fractions sum to 1 and the non-recursive term is linear.

D. The same \(\Theta(n \log n)\) class is the solution of the even split \(T(n) = 2T(n/2) + \Theta(n)\).

---

## Q15 — MCQ

Which list is ordered from slowest growth to fastest growth?

A. \(\log n,\ n,\ n \log n,\ n^2,\ 2^n,\ n!\)

B. \(\log n,\ n \log n,\ n,\ n^2,\ n!,\ 2^n\)

C. \(n,\ \log n,\ n \log n,\ 2^n,\ n^2,\ n!\)

D. \(\log n,\ n,\ n^2,\ n \log n,\ 2^n,\ n!\)

---

## Q16 — MCQ

An integer \(N\) is the input, written in binary, so the input length is \(\Theta(\log N)\) bits. An algorithm tries every integer up to \(\sqrt{N}\). In terms of the bit length, that running time is

A. polynomial in the bit length

B. \(\Theta(\sqrt{N})\), and \(\sqrt{N}\) is polynomial in the bit length

C. exponential in the bit length

D. \(\Theta(\log N)\)

---

## Level 4 — Tricky / Trap-Based

## Q17 — MCQ

A solution claims \(T(n) = 2T(n/2) + n = \Theta(n)\), “because \(f(n) = n\) and case 3 returns \(\Theta(f(n))\)”. What is wrong?

A. Nothing; merge sort is linear.

B. Here \(\log_b a = 1\) and \(f(n) = \Theta(n^{\log_b a})\), so this is case 2, which adds a logarithm: \(\Theta(n \log n)\). Case 3 needs \(f\) to be polynomially larger than \(n^{\log_b a}\), plus regularity.

C. The recurrence is case 1, so the solution is \(\Theta(n^{\log_2 2}) = \Theta(n)\) only after an extra \(\log n\) is removed.

D. The Master theorem cannot be applied to equal subproblem sizes.

---

## Q18 — MSQ

Select all that apply.

A. \(2^{n+1}\) and \(2^n\) differ by the constant factor 2, so they are \(\Theta\) of each other.

B. \(4^n / 2^n = 2^n\) is unbounded, so \(4^n\) is not \(\Theta(2^n)\).

C. \(\log_2(n^2) = 2 \log_2 n\), so \(\log_2(n^2) = \Theta(\log n)\).

D. \((\log_2 n)^2 = 2 \log_2 n\).

---

## Q19 — MCQ

Consider \(f(n) = n / \log_2 n\) and the recurrence \(T(n) = 2T(n/2) + f(n)\) for \(n \ge 2\). Which conclusion is justified?

A. Case 1 applies, because \(f(n) = O(n^{1-\varepsilon})\) for some \(\varepsilon > 0\).

B. Case 2 in the basic form \(f(n) = \Theta(n^{\log_b a})\) applies, so \(T(n) = \Theta(n \log n)\).

C. The polynomial gap required by case 1 is missing, and \(f(n)\) is not \(\Theta(n^{\log_b a})\) either, so neither case 1 nor the basic case 2 applies off the shelf.

D. Case 3 applies, because \(f(n) = \Omega(n^{1+\varepsilon})\) for some \(\varepsilon > 0\).

---

## Level 5 — Challenge

## Q20 — MCQ

The change of variables \(n = 2^m\) and \(S(m) = T(2^m)\) is used on \(T(n) = 2T(\sqrt{n}) + \Theta(\log n)\). After solving the recurrence for \(S\), \(T(n)\) is

A. \(\Theta(\log n)\)

B. \(\Theta(\log n \cdot \log \log n)\)

C. \(\Theta(n \log n)\)

D. \(\Theta(\sqrt{n})\)

---

## Q21 — MCQ

A binary counter starts at 0 and is incremented \(n\) times. Bit \(i\), counting from 0 at the least significant bit, flips once every \(2^i\) increments. The total number of bit flips over the \(n\) increments is strictly less than \(2n\). Which statement follows?

A. Every increment flips \(\Theta(\log n)\) bits in the worst case, so the amortised cost is \(\Theta(\log n)\).

B. One increment can flip every bit, and the amortised cost per increment is still \(\Theta(1)\).

C. The amortised bound requires the incremented value to be random.

D. The total is \(\Theta(n \log n)\), because there are \(\log n\) bits and each increment touches all of them.

---

## Q22 — MSQ

Select all that apply. Space and the word “in-place” are read in the usual GATE sense: auxiliary memory beyond the input, with the recursion stack counted when the algorithm is recursive.

A. Balanced quicksort uses \(\Theta(\log n)\) stack space. The degenerate pivot chain uses \(\Theta(n)\) stack space.

B. Merge sort’s auxiliary buffer is \(\Theta(n)\) even when the recursion stack is only \(\Theta(\log n)\).

C. Breadth-first search on an adjacency-list graph uses a queue that can hold \(\Theta(V)\) vertices.

D. An adjacency matrix of a graph uses \(\Theta(V + E)\) memory.

## Answer Key

| Q | Type | Answer |
|---|------|--------|
| 1 | MCQ | B |
| 2 | MSQ | A, B, D |
| 3 | NAT | 2 |
| 4 | MSQ | A, C, D |
| 5 | NAT | 3 |
| 6 | MCQ | B |
| 7 | MCQ | B |
| 8 | MCQ | C |
| 9 | MSQ | B, C |
| 10 | MCQ | B |
| 11 | MSQ | A, B, D |
| 12 | MCQ | C |
| 13 | MCQ | B |
| 14 | MSQ | B, D |
| 15 | MCQ | A |
| 16 | MCQ | C |
| 17 | MCQ | B |
| 18 | MSQ | A, B, C |
| 19 | MCQ | C |
| 20 | MCQ | B |
| 21 | MCQ | B |
| 22 | MSQ | A, B, C |

## Detailed Solutions

### Q1

Answer: B

\(2^{n+1} = 2 \cdot 2^n\). A positive constant factor does not change \(\Theta\), so \(2^{n+1} = \Theta(2^n)\). \(4^n = (2^2)^n = 2^{2n}\), and \(4^n / 2^n = 2^n\) grows, so \(4^n\) is not \(\Theta(2^n)\). Stirling gives \(\log_2(n!) = \Theta(n \log n)\), not \(\Theta(\log n)\). Finally \(\log_2(n^2) = 2 \log_2 n\), while \((\log_2 n)^2\) grows strictly faster than \(\log n\). They are not the same expression.

### Q2

Answer: A, B, D

For \(n \ge 1\), \(n \le 1 \cdot n^2\), so \(n = O(n^2)\). There is no constant \(c > 0\) such that \(n \ge c n^2\) for every large \(n\), so \(n\) is not \(\Omega(n^2)\). For the quadratic, \(3n^2 \le 3n^2 + 5n + 7 \le 15n^2\) when \(n \ge 1\), which is the two-constant definition of \(\Theta(n^2)\). Theta is symmetric. Big-O is not: \(n = O(n^2)\) does not give \(n^2 = O(n)\). A change of logarithm base divides by the constant \(\log_2 b\), so every fixed base produces the same \(\Theta\) class. That cancellation is not valid inside an exponent.

### Q3

Answer: 2

The counter runs through \(\lfloor \log_2 n \rfloor\) halvings before it drops to 1. The number of iterations is \(\Theta(\log n)\), which is code 2. A loop that adds a constant, such as \(j = j + 2\), is linear. Multiplying or dividing the counter by a constant greater than 1 is logarithmic.

### Q4

Answer: A, C, D

Worst-case \(\Theta(n^2)\) sandwiches the maximum, over inputs of size \(n\), between two constant multiples of \(n^2\). A bare \(O(n^2)\) is only an upper bound. It is true of an algorithm that is actually \(\Theta(n)\), and it is the wrong choice when the question asks for a tight bound. Insertion sort is a standard example of (C): a sorted array is \(\Theta(n)\), and a reversed array is \(\Theta(n^2)\). Average-case needs a distribution, often uniform over permutations. Amortised cost needs no distribution. It bounds the total cost of a sequence and then divides by the number of operations. A doubling array is the usual example: the total is linear, so the amortised cost is constant, while one insertion still copies the whole array.

### Q5

Answer: 3

The closed form is \(n(n+1)/2\). For \(n \ge 1\), \(n^2/2 \le n(n+1)/2 \le n^2\), so the sum is \(\Theta(n^2)\). Code 3. The same sum is the comparison count of selection sort and the shift count of insertion sort on a reversed array.

### Q6

Answer: B

Here \(a = 2\), \(b = 2\), and \(\log_b a = 1\). The driving function \(f(n) = n^2\) is \(\Omega(n^{1+\varepsilon})\) with \(\varepsilon = 1\). Regularity: \(a f(n/b) = 2 \cdot (n/2)^2 = n^2/2 \le c n^2\) with \(c = 1/2 < 1\). Case 3 says the root dominates, and \(T(n) = \Theta(n^2)\). In the tree, level \(i\) costs \(n^2 / 2^i\). That geometric series sums to less than \(2n^2\).

### Q7

Answer: B

Now \(a = 4\), \(b = 2\), and \(\log_b a = 2\). Then \(f(n) = n^2 = \Theta(n^{\log_b a})\). This is case 2 with log power \(k = 0\), so

\[
T(n) = \Theta(n^2 \log n).
\]

Case 1 would need a polynomial gap below \(n^2\), which is not present. Option (D) is the case-1 answer and it drops the logarithm that equal level costs produce. The tree has \(\Theta(\log n)\) levels, and every level costs \(\Theta(n^2)\).

### Q8

Answer: C

For each of the \(n\) values of \(i\), the inner counter doubles until it reaches \(n\). That takes \(\Theta(\log n)\) iterations, independent of \(i\). The product is \(\Theta(n \log n)\). The loop is not \(\Theta(n^2)\): the inner bound is multiplicative, not an index running up to \(i\) or \(n\) one step at a time.

### Q9

Answer: B, C

The Master theorem needs \(b > 1\), a genuine shrinkage by a constant factor. Subtracting 1 is not that form, so (A) is false. Unrolling writes \(T(n) = n + (n-1) + \cdots + 1 + \Theta(1) = \Theta(n^2)\). That sum is exactly the bad quicksort split and the worst-case shift work of insertion sort. Replacing the added \(n\) by 1 produces \(n\) constant terms, which is \(\Theta(n)\), so (D) is false.

### Q10

Answer: B

Copies occur at capacities \(1, 2, 4, \ldots\), and the last incomplete block does not exceed \(n\). The series \(n + n/2 + n/4 + \cdots\) is strictly less than \(2n\). Dividing by \(n\) insertions gives amortised \(O(1)\). The insertion that finds the buffer full copies every live element, so that one operation is \(\Theta(n)\) in the worst case. Both sentences are true, and neither replaces the other. The argument never randomises the inserted values. It holds for every sequence.

### Q11

Answer: A, B, D

Iterative binary search stores a constant number of indexes. The recursive version stores one frame per halving, and the deepest chain has \(\Theta(\log n)\) frames. Merge sort writes a second array of length \(n\); the stack is only an additional \(\Theta(\log n)\). In general, frames that are alive at the same time are the current root-to-leaf path of the recursion, so the auxiliary stack is proportional to the depth when each frame is constant size.

### Q12

Answer: C

\(\log_2 8 = 3\), so the critical power is \(n^3\). The driving function \(n^2\) is \(O(n^{3-\varepsilon})\) for \(\varepsilon = 1\). Case 1: the leaves dominate, and \(T(n) = \Theta(n^3)\). There is no extra logarithm, because the level costs grow geometrically toward the leaves rather than staying equal. The exponent \(\log_2 7\) belongs to a different recurrence, seven subproblems, which is Strassen’s matrix product rather than this one.

### Q13

Answer: B

Here \(a = 2\), \(b = 4\), and \(\log_4 2 = 1/2\). The driving function \(n\) is \(\Omega(n^{1/2 + \varepsilon})\) for \(\varepsilon = 1/2\). Regularity: \(a f(n/b) = 2 \cdot (n/4) = n/2 \le (1/2) f(n)\). Case 3 applies, and \(T(n) = \Theta(n)\). The root work dominates the two quarter-size subproblems. The answer is not the leaf contribution \(\Theta(\sqrt{n})\), which would be case 1.

### Q14

Answer: B, D

The two subproblems use different fractions, so there is no single \(b\) to plug into the Master theorem. Draw the tree. The longer child keeps a \(2/3\) fraction, and the depth of that branch is \(\Theta(\log n)\) because \((2/3)^d n\) reaches a constant when \(d = \Theta(\log n)\). A short induction on the tree shows that the non-recursive costs on one level still add to \(\Theta(n)\): the fractions on any cut of the tree sum to 1. Equal costs on \(\Theta(\log n)\) levels give \(\Theta(n \log n)\). The even split \(2T(n/2) + \Theta(n)\) is Master case 2 and lands in the same class, with a different constant. Option (C) would be right for \(T(n) = T(n/2) + \Theta(n)\), a single halving chain whose geometric series is dominated by the root.

### Q15

Answer: A

A logarithm grows slower than every positive power of \(n\), so \(\log n\) precedes \(n\). Multiplying by another \(\log n\) still leaves \(n \log n = o(n^2)\). Every polynomial is \(o(2^n)\), and \(n! / c^n \to \infty\) for every fixed \(c\), so \(n!\) follows \(2^n\). The increasing order is \(\log n,\ n,\ n \log n,\ n^2,\ 2^n,\ n!\).

### Q16

Answer: C

The input length is the number of bits, \(b = \Theta(\log_2 N)\), so \(N = 2^{\Theta(b)}\) and \(\sqrt{N} = 2^{\Theta(b)/2}\). Time polynomial in the value \(N\) is exponential in the number of bits. Calling \(\sqrt{N}\) polynomial is correct only if \(N\) itself is the size parameter. The question fixes the size as the bit length.

### Q17

Answer: B

For \(a = b = 2\), the critical power is \(n^1\). The driving function is \(\Theta(n)\), not polynomially larger, so case 3 does not apply. Regularity is not the missing piece; the case test already failed. Case 2 adds one logarithm and produces \(\Theta(n \log n)\). That is merge sort. Writing \(\Theta(n)\) drops the \(\Theta(\log n)\) equal-cost levels of the recursion tree.

### Q18

Answer: A, B, C

(A), (B), and (C) are the three identities from Q1, stated in the direction that makes them true. (D) rewrites a square of a logarithm as if it were the logarithm of a square. The identity \(\log(n^2) = 2 \log n\) moves the 2 outside the logarithm. It does not turn \((\log n)^2\) into \(2 \log n\). The square grows faster than \(\log n\) and slower than every \(n^\varepsilon\).

### Q19

Answer: C

The critical power is \(n^{\log_2 2} = n\). Case 1 needs \(f(n) = O(n^{1-\varepsilon})\) for some fixed \(\varepsilon > 0\). But \(n / \log n\) is not bounded by a constant times \(n^{1-\varepsilon}\), because \(n^\varepsilon / \log n \to \infty\). Basic case 2 needs \(f(n) = \Theta(n)\), and \(n / \log n\) is \(o(n)\). Case 3 needs a polynomial gap above \(n\), and \(n / \log n\) is smaller than \(n\), not larger. The recurrence sits between the textbook cases. A finer case-2 form that allows a negative power of \(\log n\) can be derived from the tree, but it is not any of the three claims (A), (B), or (D).

### Q20

Answer: B

Set \(n = 2^m\) and \(S(m) = T(2^m)\). Then \(\sqrt{n} = 2^{m/2}\) and \(\log n = \Theta(m)\), so

\[
S(m) = 2S(m/2) + \Theta(m).
\]

For this recurrence \(a = 2\), \(b = 2\), \(\log_b a = 1\), and \(f(m) = \Theta(m) = \Theta(m^{\log_b a})\). Case 2 gives \(S(m) = \Theta(m \log m)\). Substitute back: \(m = \log_2 n\) and \(\log m = \Theta(\log \log n)\), hence \(T(n) = \Theta(\log n \cdot \log \log n)\).

### Q21

Answer: B

Bit 0 flips every increment, bit 1 flips every second increment, and bit \(i\) flips every \(2^i\) increments. Over \(n\) increments the total is at most \(n + n/2 + n/4 + \cdots < 2n\). The amortised cost is therefore \(\Theta(1)\) per increment. A single increment of a string of 1-bits flips every bit, so the worst case of one operation is \(\Theta(\log n)\) when the counter has \(\Theta(\log n)\) bits. The total bound does not need randomness, and it is not \(\Theta(n \log n)\), because most bits flip rarely.

### Q22

Answer: A, B, C

Quicksort’s stack is the recursion depth: \(\Theta(\log n)\) when pivots stay balanced, and \(\Theta(n)\) when each pivot peels off one key. Merge sort’s buffer is a second copy of the \(n\) keys regardless of that stack. A breadth-first queue holds a whole level; on a star that level has \(\Theta(V)\) leaves. An adjacency matrix stores a \(V \times V\) table, which is \(\Theta(V^2)\) memory, not \(\Theta(V+E)\). The linear size belongs to adjacency lists.
