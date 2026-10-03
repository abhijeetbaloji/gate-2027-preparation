# Searching — Practice Questions

Original practice for GATE CS. These questions are not from any GATE paper. Attempt the questions before reading the solutions.

## Level 1 — Conceptual

## Q1 — MCQ

An unsorted array of \(n\) distinct integers will be used for exactly one membership query and then discarded. In the comparison model, the worst-case cost of the best strategy is

A. \(\Theta(1)\)

B. \(\Theta(\log n)\)

C. \(\Theta(n)\)

D. \(\Theta(n \log n)\)

---

## Q2 — MSQ

Select all that apply. Iterative binary search is run on a sorted array of \(n\) keys, using the closed interval \([\mathrm{lo}, \mathrm{hi}]\) and \(\mathrm{mid} = \mathrm{lo} + (\mathrm{hi} - \mathrm{lo}) // 2\).

A. The running-time recurrence is \(T(n) = T(\lfloor n/2 \rfloor) + \Theta(1)\), which solves to \(\Theta(\log n)\).

B. The iterative version uses \(\Theta(\log n)\) auxiliary memory.

C. The best case is \(\Theta(1)\), when the first middle key equals the target.

D. If the array is not sorted, the same code still returns a correct index whenever the key is present.

---

## Q3 — NAT

In the comparison model, each test has two outcomes. What is the minimum number of comparisons required in the worst case to decide which of 15 sorted positions holds a key, or that the key is absent?

---

## Level 2 — Standard GATE Style

## Q4 — NAT

The sorted array is \([3, 8, 14, 19, 25, 31, 40]\), indexes starting at 0. Binary search looks for 25 with \(\mathrm{mid} = \mathrm{lo} + (\mathrm{hi} - \mathrm{lo}) // 2\) and the interval closed. How many middle probes are performed until 25 is found?

---

## Q5 — NAT

The sorted array is \([1, 4, 4, 4, 4, 9]\). How many times does the key 4 occur? Compute it as the gap between the first and last occurrence, not by a linear scan.

---

## Q6 — MCQ

Linear search scans from the left. The key is present and equally likely to sit in any of the \(n\) positions. The expected number of comparisons is

A. \(n\)

B. \((n+1)/2\)

C. \(\lceil \log_2 (n+1) \rceil\)

D. \(n/2\) for every positive integer \(n\), with no rounding

---

## Q7 — MSQ

Select all that apply. Jump search runs on a sorted array of \(n = 400\) keys. The block length \(m\) is chosen to minimise the bound \(n/m + m\).

A. The minimising block length is \(m = 20\).

B. At that block length the bound \(n/m + m\) equals 40.

C. The worst-case time is \(\Theta(\log n)\).

D. Auxiliary memory is \(\Theta(1)\).

---

## Level 3 — Multi-Step

## Q8 — NAT

A distinct-key sorted array was rotated to \([9, 12, 15, 2, 5, 7]\). Search for 5. At each step the half whose endpoints are in order is the sorted half, and the search keeps the half that can contain the key. Use \(\mathrm{mid} = \mathrm{lo} + (\mathrm{hi} - \mathrm{lo}) // 2\) and indexes from 0. How many middle probes are made until 5 is found?

---

## Q9 — NAT

A predicate \(P(x)\) is false for every integer \(x\) with \(x^2 < 50\) and true for every integer \(x\) with \(x^2 \ge 50\). Binary search is used on the answer range \(1 \le x \le 100\). What is the smallest \(x\) for which \(P(x)\) is true?

---

## Q10 — MCQ

Ternary search minimises a unimodal function on \(n\) points by evaluating two interior points and discarding one third of the domain. The recurrence is \(T(n) = T(2n/3) + \Theta(1)\). The solution is

A. \(\Theta(n)\)

B. \(\Theta(\log n)\)

C. \(\Theta(n \log n)\)

D. \(\Theta(\log \log n)\)

---

## Level 4 — Tricky / Trap-Based

## Q11 — MCQ

Which statement about interpolation search is correct?

A. Its worst-case cost is \(O(\log \log n)\) on every numeric array.

B. Under a uniform key model the expected cost is \(O(\log \log n)\), and the worst case is \(\Theta(n)\).

C. Its worst-case cost is \(\Theta(\log n)\) on every input, because each probe halves the interval.

D. It is always faster than binary search, including on skewed keys.

---

## Q12 — MSQ

Select all that apply.

A. The call stack of recursive binary search is \(\Theta(\log n)\) in the worst case.

B. On a rotated array that may contain duplicate keys, the “sorted half” test always discards half of the remaining interval.

C. If the key is absent, the expected linear-search cost is \((n+1)/2\).

D. If the key is absent, a left-to-right linear search examines all \(n\) keys.

---

## Level 5 — Challenge

## Q13 — NAT

A sorted array has \(n = 1024\) keys. The standard closed-interval binary search halves the range at every probe. How many probes does it use in the worst case? Use the bound \(\lfloor \log_2 n \rfloor + 1\).

---

## Q14 — MCQ

A static unsorted array holds \(n\) distinct keys. Then \(q\) membership queries arrive, with \(q\) growing and \(1 \ll q \ll n\). Comparisons are the cost. Which statement is true?

A. Sorting once and then binary-searching every query is \(\Theta(n \log n + q \log n)\) in the worst case, and this is asymptotically cheaper than \(q\) separate linear scans.

B. A hash function fixed before the queries are chosen answers every query in worst-case \(\Theta(1)\) time.

C. For \(q = 1\), sorting and then searching improves the worst-case bound below \(\Theta(n)\).

D. Binary search on the original unsorted array is \(\Theta(\log n)\) in the worst case.

## Answer Key

| Q | Type | Answer |
|---|------|--------|
| 1 | MCQ | C |
| 2 | MSQ | A, C |
| 3 | NAT | 4 |
| 4 | NAT | 3 |
| 5 | NAT | 4 |
| 6 | MCQ | B |
| 7 | MSQ | A, B, D |
| 8 | NAT | 2 |
| 9 | NAT | 8 |
| 10 | MCQ | B |
| 11 | MCQ | B |
| 12 | MSQ | A, D |
| 13 | NAT | 11 |
| 14 | MCQ | A |

## Detailed Solutions

### Q1

Answer: C

Nothing is known about order, so a comparison cannot discard an unseen element. Linear search looks at every key in the worst case and stops when it finds the target, which is \(\Theta(n)\). Sorting first costs \(\Theta(n \log n)\) and is then thrown away after one query, so it is a worse worst-case strategy. Binary search is not valid until the array is sorted.

### Q2

Answer: A, C

(A) is the binary-search recurrence. There are \(\Theta(\log n)\) constant-time probes, so \(T(n) = \Theta(\log n)\). (B) is false for the iterative form: only a few indexes are stored, so auxiliary memory is \(\Theta(1)\). The \(\Theta(\log n)\) stack belongs to the recursive form. (C) is true: if \(A[\mathrm{mid}]\) equals the key on the first probe, the search returns immediately. (D) is false. The step that throws away a side uses sorted order. On an unsorted array that step can discard the only copy of the key.

### Q3

Answer: 4

There are 16 possibilities: the key is in one of 15 positions, or it is absent. Each comparison has two answers, so a decision tree of height \(h\) distinguishes at most \(2^h\) possibilities. The smallest \(h\) with \(2^h \ge 16\) is \(h = 4\), which is \(\lceil \log_2 (15 + 1) \rceil = 4\).

### Q4

Answer: 3

Start with \(\mathrm{lo} = 0\), \(\mathrm{hi} = 6\).

| Probe | lo | hi | mid | \(A[\mathrm{mid}]\) | Action |
|------:|---:|---:|----:|--------------------:|--------|
| 1 | 0 | 6 | 3 | 19 | \(19 < 25\), set \(\mathrm{lo} = 4\) |
| 2 | 4 | 6 | 5 | 31 | \(31 > 25\), set \(\mathrm{hi} = 4\) |
| 3 | 4 | 4 | 4 | 25 | found |

The invariant is that if 25 occurs, it lies in \([\mathrm{lo}, \mathrm{hi}]\). Each miss moves an endpoint past the rejected middle, so the interval shrinks. Three probes.

### Q5

Answer: 4

The first-occurrence search records a match and continues left. It stops at index 1. The last-occurrence search records a match and continues right. It stops at index 4. The count is \(4 - 1 + 1 = 4\). Ordinary binary search would be allowed to return any of the indexes 1, 2, 3, or 4, so one equality test does not give the count. Both bound searches are still \(\Theta(\log n)\).

### Q6

Answer: B

If the key is at the first position, one comparison is used; if it is at the last, \(n\) comparisons are used. Averaging the uniform positions gives

\[
\frac{1 + 2 + \cdots + n}{n} = \frac{n+1}{2}.
\]

Option (D) drops the \(+1/2\). For odd \(n\) the two expressions differ. The formula needs the key to be present. An absent key always costs \(n\) comparisons.

### Q7

Answer: A, B, D

Jumps of length \(m\) cost about \(n/m\), and the final block costs at most \(m\). For positive \(m\), \(n/m + m\) is minimised at \(m = \sqrt{n}\). Here \(\sqrt{400} = 20\), and \(400/20 + 20 = 40\). That is \(\Theta(\sqrt{n})\), not \(\Theta(\log n)\). Binary search is the logarithmic algorithm. Only indexes are stored, so extra memory is \(\Theta(1)\). Thus (A), (B), and (D) hold, and (C) does not.

### Q8

Answer: 2

| Probe | lo | hi | mid | \(A[\mathrm{mid}]\) | Sorted half and decision |
|------:|---:|---:|----:|--------------------:|--------------------------|
| 1 | 0 | 5 | 2 | 15 | Left side \([9, 12, 15]\) is sorted, and 5 is not between 9 and 15, so \(\mathrm{lo} = 3\) |
| 2 | 3 | 5 | 4 | 5 | found |

With distinct keys, at least one side of the middle is still fully sorted, because the single rotation cut can lie in only one side. The key is kept only if it lies between that side’s endpoints. Two probes.

### Q9

Answer: 8

\(7^2 = 49 < 50\) and \(8^2 = 64 \ge 50\). Feasibility is monotonic: every integer larger than 8 also works, and every integer smaller than 8 fails. Binary search on that predicate therefore returns 8. A search of an array of squares is unnecessary; the unknown is the numeric boundary.

### Q10

Answer: B

Here \(a = 1\) and \(b = 3/2\), so \(\log_b a = 0\). The non-recursive cost \(f(n) = \Theta(1) = \Theta(n^{\log_b a})\). Master case 2, with the log power \(k = 0\), adds one logarithm: \(T(n) = \Theta(\log n)\). The base \(3/2\) changes the constant hidden by \(\Theta\), because \(\log_{3/2} n = \Theta(\log n)\). Unrolling gives the same picture: each step keeps a \(2/3\) fraction, and \(\Theta(\log n)\) steps reduce the domain to a constant.

### Q11

Answer: B

The probe index estimates where the key would lie if values increased linearly. Under a uniform model that guess lands close to the key, and the expected number of probes is \(O(\log \log n)\). On skewed data the interval can shrink by only one index, which is \(\Theta(n)\). The \(O(\log \log n)\) bound is not a worst-case bound, and a single probe need not discard half of the range, so interpolation search is not a substitute for binary search unless uniformity is given.

### Q12

Answer: A, D

(A) is true: each recursive call handles one half, and the depth is the number of halvings. (B) is false. Duplicate neighbours can make both sides look identical, so one comparison may be unable to discard half of the array. The logarithmic worst-case claim needs distinct keys, or an extra rule for ties. (C) is false: \((n+1)/2\) is the expectation only when the key is present and uniform over the positions. (D) is true: a miss has no place to stop early, so all \(n\) keys are compared.

### Q13

Answer: 11

\(\log_2 1024 = 10\), so \(\lfloor \log_2 1024 \rfloor + 1 = 11\). The range lengths fall through \(1024, 512, \ldots, 1\), which is 11 probes when the key is in the last cell examined or is absent. This matches the comparison lower bound up to a small constant: \(\lceil \log_2 (1024 + 1) \rceil = 11\) as well, since \(2^{10} = 1024 < 1025 \le 2^{11}\).

### Q14

Answer: A

Sorting costs \(\Theta(n \log n)\) once. Each later binary search is \(\Theta(\log n)\), so \(q\) queries cost \(\Theta(n \log n + q \log n)\). Fresh linear scans cost \(\Theta(qn)\). For \(1 \ll q \ll n\) the sort-once bound is the smaller one, because \(n \log n + q \log n = o(qn)\). (B) fails by the pigeonhole principle: a fixed hash known to an adversary can send every query into one long chain, and the worst case is linear in the chain. (C) fails because one query does not repay the sort: \(\Theta(n \log n)\) is worse than one scan of \(\Theta(n)\). (D) fails because discarding a side is valid only after the array is sorted.
