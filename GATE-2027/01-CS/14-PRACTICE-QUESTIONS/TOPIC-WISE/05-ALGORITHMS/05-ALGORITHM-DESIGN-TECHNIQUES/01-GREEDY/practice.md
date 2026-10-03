# Greedy Algorithms — Practice Questions

Original practice for GATE CS. These questions are not from any GATE paper. Attempt the questions before reading the solutions.

## Level 1 — Conceptual

## Q1 — MCQ

Unweighted activity selection asks for the largest set of compatible intervals. The rule that has an exchange proof is

A. sort by increasing start time, then take every compatible activity

B. sort by increasing duration, then take every compatible activity

C. sort by increasing finish time, then take the next activity that starts at or after the finish of the last chosen activity

D. sort by decreasing finish time, then take the first activity

---

## Q2 — MSQ

Select all that apply.

A. A greedy algorithm is justified by a greedy-choice property: some optimal solution contains the locally chosen piece.

B. One input on which the rule succeeds is a proof that the rule succeeds on every input.

C. After the greedy piece is fixed, optimal substructure says that an optimal solution of the remainder completes an optimal solution of the original problem.

D. If the greedy-choice property fails, dynamic programming may still apply, because it tries the competing first choices and stores the winners.

---

## Q3 — MCQ

Fractional knapsack allows any fraction of an item. The safe order is

A. increasing weight

B. decreasing value, ignoring weight

C. decreasing value per unit weight, with at most one fractional item

D. the same ratio order used on the 0/1 problem, which is always optimal for indivisible items as well

---

## Q4 — MCQ

Huffman’s algorithm, on symbol frequencies, repeatedly merges

A. the two heaviest remaining nodes, and does not put the parent back into the heap

B. the two lightest remaining nodes, and inserts the parent, whose weight is the sum, back into the heap

C. the most frequent symbol with the least frequent symbol, once

D. symbols in alphabetical order

---

## Level 2 — Standard GATE Style

## Q5 — NAT

Activities, given as (name, start, finish), are

\[
(A,0,3),\ (B,1,4),\ (C,3,6),\ (D,2,8),\ (E,5,7),\ (F,6,9),\ (G,8,10).
\]

Finish time \(t\) is compatible with a later start of \(t\). What is the size of a maximum compatible set?

---

## Q6 — NAT

A fractional knapsack has capacity 15.

| Item | Weight | Value |
|------|-------:|------:|
| X | 6 | 30 |
| Y | 8 | 32 |
| Z | 5 | 15 |

What total value does the ratio rule achieve?

---

## Q7 — NAT

Jobs take one unit of time and earn their profit only if they finish in a slot at most their deadline. Slots are \(1, 2, 3\). Place each job, in decreasing order of profit, into the latest free slot that meets its deadline.

| Job | Profit | Deadline |
|-----|-------:|---------:|
| J1 | 40 | 2 |
| J2 | 15 | 1 |
| J3 | 35 | 1 |
| J4 | 20 | 2 |
| J5 | 10 | 3 |

What profit does the algorithm achieve?

---

## Q8 — MSQ

Select all that apply. Huffman codes for frequencies \(A:3,\ B:4,\ C:6,\ D:7,\ E:15\). The two lightest nodes are merged, the parent is reinserted, and ties are broken by taking the two nodes the binary heap returns first when equal weights are compared by the order they were created (A with B before any later tie).

A. The first merge combines A and B into a node of weight 7.

B. One optimal tree has E at depth 1 and A, B, C, D at depth 3.

C. The weighted external path length \(\sum \mathrm{freq}(s)\cdot\mathrm{depth}(s)\) equals 75.

D. Merging the two heaviest symbols first is the Huffman rule.

---

## Level 3 — Multi-Step

## Q9 — NAT

Files of sizes \(4, 6, 7, 9\) are merged. Merging two files of sizes \(a\) and \(b\) costs \(a+b\) and replaces them by one file of that size. The greedy rule always merges the two currently smallest files. What is the total cost?

---

## Q10 — NAT

Coin denominations are \(1, 4, 6\), and the amount is 8. Unlimited coins are allowed. The largest-first greedy rule uses how many coins?

---

## Q11 — MSQ

Select all that apply. A 0/1 knapsack has capacity 10. Items must be taken whole or not at all.

| Item | Weight | Value |
|------|-------:|------:|
| A | 6 | 30 |
| B | 5 | 20 |
| C | 5 | 20 |

A. Decreasing ratio takes only A, for value 30.

B. An optimal 0/1 packing has value 40.

C. The fractional rule on this instance is optimal for the 0/1 constraint.

D. The failure shows that “sort by \(v_i/w_i\)” does not have the greedy-choice property for indivisible items.

---

## Level 4 — Tricky / Trap-Based

## Q12 — MCQ

Intervals \(P = [1,4]\), \(Q = [3,5]\), and \(R = [4,7]\) are compatible when one finishes at or before the next starts. Shortest-duration greedy considers the shortest interval first and then keeps later intervals only if they are compatible with those already chosen. Earliest-finish greedy sorts by finish time. Which statement is correct?

A. Both rules return a maximum set, of size 2.

B. Shortest-duration greedy returns only \(Q\), size 1, while a maximum set is \(\{P, R\}\), size 2.

C. Earliest-finish greedy returns only \(Q\).

D. No compatible pair exists.

---

## Q13 — MSQ

Select all that apply.

A. Kruskal and Prim remain correct if some edge weights are negative. The cut property never divides by a weight.

B. Dijkstra’s selection of the unsettled vertex of smallest tentative distance remains correct if some edge weight is negative.

C. “Greedy never works when a number is negative” is false for minimum spanning trees and true as a warning about Dijkstra.

D. A minimum spanning tree is a shortest-path tree: the unique path in the tree between two vertices is a minimum-weight path in the graph.

---

## Q14 — MCQ

Job sequencing with deadlines and profits, for unit-time jobs, sorts by

A. increasing deadline, because earliest-deadline-first maximises profit

B. decreasing profit, and then places a job in the latest free slot that is still at most its deadline

C. decreasing profit, and then places a job in the earliest free slot

D. increasing duration, although every duration is 1

---

## Level 5 — Challenge

## Q15 — MCQ

A weighted matroid is a hereditary family of independent sets that also has the exchange property: if \(|A| < |B|\) and both sets are independent, some element of \(B \setminus A\) can be added to \(A\). The greedy algorithm adds the heaviest element that preserves independence. Which statement is correct?

A. This greedy rule produces a maximum-weight independent set for every weight function exactly on matroids. Kruskal’s algorithm is this rule on the graphic matroid of acyclic edge sets.

B. Every optimisation problem whose description contains the word “maximum” is a matroid, so every greedy rule is optimal.

C. 0/1 knapsack is this matroid, which is why the ratio rule is optimal.

D. Fractional knapsack is optimal only because its feasible sets form a matroid. The ratio exchange is not a separate argument.

---

## Q16 — MSQ

Select all that apply. Activity selection is stated on an unsorted list of \(n\) intervals, and the objective is the number of compatible activities, not their values.

A. Including the sort, the earliest-finish algorithm is \(\Theta(n \log n)\).

B. If the list is already sorted by finish time, the scan is \(\Theta(n)\).

C. The same earliest-finish rule maximises total value when each activity has an arbitrary value.

D. Sorting by start time, or by duration, can reject an optimal set. The exchange proof uses the earliest finish, not those other keys.

## Answer Key

| Q | Type | Answer |
|---|------|--------|
| 1 | MCQ | C |
| 2 | MSQ | A, C, D |
| 3 | MCQ | C |
| 4 | MCQ | B |
| 5 | NAT | 3 |
| 6 | NAT | 65 |
| 7 | NAT | 85 |
| 8 | MSQ | A, B, C |
| 9 | NAT | 52 |
| 10 | NAT | 3 |
| 11 | MSQ | A, B, D |
| 12 | MCQ | B |
| 13 | MSQ | A, C |
| 14 | MCQ | B |
| 15 | MCQ | A |
| 16 | MSQ | A, B, D |

## Detailed Solutions

### Q1

Answer: C

Sort so that \(f_1 \le f_2 \le \cdots \le f_n\), take the first activity, and then take the next activity whose start is at least the finish of the last choice. The exchange proof uses that finish order. Let \(g\) be an earliest finisher and let \(a\) be the activity that finishes first in some optimal set. Then \(f_g \le f_a\). Replacing \(a\) by \(g\) stays feasible, because every other chosen activity starts at or after \(f_a\) and hence at or after \(f_g\), and the set size does not fall. Start time and duration do not give this comparison. Decreasing finish time takes the activity that blocks the largest remainder of the day.

### Q2

Answer: A, C, D

The greedy-choice property is an existence claim about every input, proved by exchange or by a cut argument, not by a single successful example. A rule can succeed on ten inputs and fail on the eleventh. Once the first piece is fixed, the rest of an optimal solution must solve the remaining instance; that is optimal substructure, which greedy shares with dynamic programming. Dynamic programming differs by computing the competing choices. If no proof eliminates them, they have to be tried. That is why 0/1 knapsack and weighted interval scheduling move to a table.

### Q3

Answer: C

Sort by decreasing \(v_i / w_i\). Fill whole items until the next item does not fit, then take the fraction of it that fills the residual capacity. At most one item is fractional. The exchange is: if a packing still contains some weight of a worse ratio while a better ratio is available, moving that weight onto the better ratio raises the value and stays inside the capacity. The fraction is essential. The same order on indivisible items can miss the optimum, as Q11 shows.

### Q4

Answer: B

The two least frequent symbols are siblings at the deepest level of some optimal prefix code. If a rarer symbol sat deeper than a more frequent one, swapping them would not increase \(\sum \mathrm{freq}\cdot\mathrm{depth}\). Merge those two lightest nodes, give the parent weight equal to the sum, and put the parent back into the heap so that later merges can compare it with original symbols. Merging the two heaviest nodes builds a deep code for the frequent symbols, which is the wrong direction.

### Q5

Answer: 3

Sorted by finish time: \(A(3),\ B(4),\ C(6),\ E(7),\ D(8),\ F(9),\ G(10)\).

- Take \(A\), which finishes at 3.
- \(B\) starts at 1, before 3. Skip.
- \(C\) starts at 3. Take it. It finishes at 6.
- \(E\) starts at 5, and \(D\) starts at 2. Skip both.
- \(F\) starts at 6. Take it. It finishes at 9.
- \(G\) starts at 8, before 9. Skip.

The set \(\{A, C, F\}\) has size 3. No set of size 4 exists. Any selection that keeps both \(C\) and \(E\) overlaps on \([5,6]\), and after \(F\) finishes at 9 the only later activity, \(G\), has already started. Replacing \(C\) by \(E\) yields \(\{A, E, G\}\), which also has size 3, so the optimum value is unique even though the optimum set is not. The algorithm’s set is optimal.

### Q6

Answer: 65

Ratios: \(X\) is \(30/6 = 5\), \(Y\) is \(32/8 = 4\), \(Z\) is \(15/5 = 3\).

- Take all of \(X\): value 30, weight 6, residual capacity 9.
- Take all of \(Y\): value 32, weight 8, residual capacity 1.
- Take \(1/5\) of \(Z\): value \(15/5 = 3\).

The total is \(30 + 32 + 3 = 65\). The last item is the only fraction. Swapping any weight off \(X\) onto a lower ratio would lose value, which is why the ratio order is safe for the fractional problem.

### Q7

Answer: 85

Decreasing profit order is J1 (40), J3 (35), J4 (20), J2 (15), J5 (10).

- J1 has deadline 2. The latest legal free slot is 2. Place J1 there.
- J3 has deadline 1. Slot 1 is free. Place J3 there.
- J4 has deadline 2. Slots 2 and 1 are full, and slot 3 is after the deadline. Reject J4.
- J2 has deadline 1. Slot 1 is full. Reject J2.
- J5 has deadline 3. Slot 3 is free. Place J5 there.

The schedule is J3, J1, J5, and the profit is \(40 + 35 + 10 = 85\). Replacing J3 by J4 would drop the profit to \(40 + 20 + 10 = 70\). The latest-slot rule is what left slot 1 open for J3; putting J1 into slot 1 would have blocked the only slot J3 can use.

### Q8

Answer: A, B, C

The heap starts as \(A:3,\ B:4,\ C:6,\ D:7,\ E:15\).

- Merge A and B into a node \(P\) of weight 7. The multiset is \(C:6,\ D:7,\ P:7,\ E:15\).
- Merge C with D into \(Q\) of weight 13. The multiset is \(P:7,\ Q:13,\ E:15\).
- Merge \(P\) with \(Q\) into \(R\) of weight 20. Then merge \(R\) with E.

One resulting tree has E on one side of the root and the subtree of weight 20 on the other, so E has depth 1. Inside that subtree, \(P\) and \(Q\) each add a level, and A, B, C, D are one level below them, at depth 3. The weighted path length is

\[
15\cdot 1 + 3\cdot 3 + 4\cdot 3 + 6\cdot 3 + 7\cdot 3 = 15 + 9 + 12 + 18 + 21 = 75.
\]

The same 75 is the sum of the internal-node weights \(7 + 13 + 20 + 35\), because each leaf is counted once for every internal node above it. Merging heaviest symbols first is not the algorithm.

### Q9

Answer: 52

This is the same tree shape as Huffman, with file size in place of frequency, and the cost is the sum of the file sizes created by the merges.

- Merge 4 and 6, cost 10. The sizes are now \(7, 9, 10\).
- Merge 7 and 9, cost 16. The sizes are now \(10, 16\).
- Merge 10 and 16, cost 26.

The total is \(10 + 16 + 26 = 52\). Merging 4 with 6 and then 7 with 10, before touching 9, costs \(10 + 17 + 26 = 53\), which is worse. The optimal cost need not come from a unique tree, but every deviation from “two smallest” in this instance raised the total.

### Q10

Answer: 3

The largest coin that fits in 8 is 6. The residual 2 is two 1s. Greedy uses \(6 + 1 + 1\), which is 3 coins. The rule has no exchange proof on this denomination set. Two 4s make 8 with 2 coins, so 3 is not optimal. The general algorithm is the coin dynamic program, not largest-first. Canonical systems such as powers of a base are a special case where the greedy choice does have a proof; this set is not one of them.

### Q11

Answer: A, B, D

Ratios: A is 5, and B and C are 4. Greedy takes A, weight 6, and the residual capacity 4 admits neither B nor C. The value is 30. Taking B and C uses weight 10 and value 40, which is feasible and better. The fractional version of this knapsack could fill the residual 4 with a fraction of B and would be justified by the ratio swap. Once fractions are forbidden, that swap can leave the knapsack, and the first choice of A is not part of any optimal solution. The greedy-choice property fails.

### Q12

Answer: B

Durations are \(P:3\), \(Q:2\), \(R:3\). Shortest-duration greedy takes \(Q\) first. Both \(P\) and \(R\) overlap \(Q\), so the algorithm stops at size 1. The set \(\{P, R\}\) is compatible because \(P\) finishes at 4 and \(R\) starts at 4, and it has size 2. Earliest-finish order is \(P\) (finish 4), \(Q\) (finish 5), \(R\) (finish 7). It takes \(P\), rejects \(Q\), and takes \(R\). The earliest-finish rule returns the optimum. Shortest duration does not, because a short interval in the middle can block two intervals that would have sat on either side.

### Q13

Answer: A, C

The cut property says that a lightest edge leaving a set that the current forest does not yet touch is safe to add. The proof replaces another crossing edge by this one and compares weights by \(\le\). A negative weight is allowed and, when it does not close a cycle, it only helps the sum. Dijkstra’s proof needs the opposite sign condition. The unsettled vertex of smallest tentative distance is final only because every edge on the unused tail of a competing path has weight at least 0. A negative tail can repair a path that looked worse at the cut, after Dijkstra has already finalised the vertex. So (A) and (C) are true and (B) is false. (D) is false for a different reason: an MST minimises the sum of selected edges, not the path between a given pair. On the triangle with weights 5, 6, and 9, the MST uses 5 and 6, total 11, and the tree path between the endpoints of the unused edge has weight 11, which is worse than the direct edge of weight 9.

### Q14

Answer: B

The objective is profit, so the jobs are considered from the most profitable to the least. The deadline is only a feasibility limit. Placing the chosen job in the latest legal slot keeps earlier slots free for a job whose deadline is tighter; Q7 is the worked case. Earliest-deadline-first is the greedy rule for a different objective, minimising maximum lateness when every job must run. It does not select a maximum-profit subset. Earliest-slot placement of a high-profit job can occupy the only slot a slightly less profitable, tighter job can use.

### Q15

Answer: A

On a matroid, the hereditary property and the exchange property are exactly what the greedy exchange needs. Adding the heaviest element that preserves independence produces a maximum-weight independent set for every weight function, and this characterises matroids among hereditary families. Kruskal is that algorithm: independent sets are the acyclic subsets of edges, and “heaviest” becomes “lightest” after the weights are negated, or the edges are scanned lightest first with the same independence test. The word “maximum” in a problem statement does not create a matroid. 0/1 knapsack does not have this exchange property for the family of feasible packs, and Q11 is a concrete failure of a natural greedy rule. Fractional knapsack is optimal because of the ratio swap, which is a different proof about a continuous capacity, not because its feasible sets were checked against the matroid axioms.

### Q16

Answer: A, B, D

The scan that accepts or rejects each interval is linear, but an unsorted list must be sorted by finish time first. Comparison sorting is \(\Theta(n \log n)\), and it dominates. If the question already supplies finish order, the sort is not charged and the scan is \(\Theta(n)\). Values break the exchange. A low-value activity that finishes first can be swapped into an optimal set while the objective, now a sum of values, falls. Weighted interval scheduling is a dynamic program: after sorting by finish time, each activity is either skipped or taken together with the latest compatible predecessor. Start order and duration order fail even in the unweighted problem, as Q1 and Q12 record. The comparison \(f_g \le f_a\) is specifically a comparison of finish times.
