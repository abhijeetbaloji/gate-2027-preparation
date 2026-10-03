# Greedy — Practice

These are practice questions, not GATE questions.

### Level 1 — Concept

**1.** What two properties justify a greedy algorithm?

**2.** Why does sorting activities by increasing duration fail in general?

**3.** Why may fractional knapsack take a fraction of at most one item?

**4.** State the Huffman merge step.

**5.** Why is Dijkstra’s selection rule unsafe when an edge weight is negative?

### Level 2 — Standard

**6.** Activities `(start, finish)`: `(1, 4), (3, 5), (0, 6), (5, 7), (3, 9), (6, 10), (8, 11)`. How many does earliest-finish select?

**7.** Capacity 50, items `(w, v) = (10, 60), (20, 100), (30, 120)`. Fractional optimum? 0/1 optimum? Value of ratio-greedy if fractions are forbidden?

**8.** Coins `{1, 5, 10, 25}`, amount 40. How many coins does greedy use? Can two coins make 40?

**9.** Files of size 4, 2, 7, 3. Cost of always merging the two smallest current files?

**10.** Jobs `(profit, deadline)`: `(20, 2), (15, 2), (10, 1), (5, 3), (1, 3)`. Total profit of the standard greedy schedule?

### Level 3 — Multi-step

**11.** Coins `{1, 3, 4}`, amount 6. Greedy count, and DP values `C(0)` through `C(6)`?

**12.** Give three intervals where the shortest one is in no maximum-cardinality feasible set.

**13.** Huffman weights 1, 1, 2, 4. First merge, and the multiset of weights afterwards?

**14.** In the capacity-50 example, which step of the fractional swap proof needs a fraction?

**15.** Unit-time jobs, one machine, every job must run, objective minimum maximum lateness. Which order is the greedy rule?

### Level 4 — Trap-based

**16.** A rule matched the optimum on three inputs. Why is that not a proof?

**17.** One edge has weight `−5`; every other weight is positive. Which of Kruskal and Dijkstra remains correct?

**18.** Unordered activities, earliest-finish selection, answered as `Θ(n)`. What is missing?

**19.** Job P: profit 10, deadline 2. Job Q: profit 9, deadline 1. Compare “put the best job in the earliest slot” with “put it in the latest feasible slot”.

**20.** Frequencies 1, 1, 1, 3. Code length of the weight-3 symbol in a Huffman tree? Weighted external path length of the Huffman tree versus a tree in which every leaf has depth 2?

### Level 5 — Challenge

**21.** Prove that an earliest-finishing activity `g` can replace the earliest-finishing member of any optimal activity set without decreasing the size.

**22.** Argue that fractional knapsack has an optimum that takes a prefix of the ratio-sorted list, with only the last chosen item possibly fractional.

**23.** Show that no optimal coin combination for amount 6 with denominations `{1, 3, 4}` contains a 4.

**24.** Files 5, 5, 5, 5. Cost of the balanced merge sequence, and cost of the skewed sequence (always merge the newest result with a fresh 5). Why do they differ?

**25.** Intervals A `[0, 3)` value 10 and B `[2, 6)` value 100. What does earliest-finish select if it ignores values, and what is the optimal weighted selection?

---

## Answers and explanations

**1.** A greedy-choice property (some optimum contains the local choice) and optimal substructure (the remainder of that optimum solves the smaller instance).

**2.** A short interval can overlap two intervals that do not overlap each other. Taking the short one blocks both. Earliest finish has an exchange proof; shortest duration does not.

**3.** Capacity is filled from the best ratio downward. At most the residual capacity is left, and it is smaller than the next item, so only that item is split.

**4.** Remove the two lightest nodes, attach them to a parent whose weight is their sum, and put the parent back. Repeat until one node remains.

**5.** The algorithm treats the unsettled vertex of smallest tentative distance as finished. A negative edge can still reduce that distance, so the choice was not safe.

**6.** Three: `(1, 4)`, then `(5, 7)`, then `(8, 11)`.

**7.** Fractional 240. 0/1 optimum 220 (weights 20 and 30). Ratio greedy without fractions takes weights 10 and 20, value 160.

**8.** Three coins: 25 + 10 + 5. Two coins cannot: the pairs of denominations are 50, 35, 30, 25, 20, 15, 10, or 2, none of which is 40.

**9.** Merge 2 and 3 (cost 5), then 4 and 5 (cost 9), then 7 and 9 (cost 16). Total 30.

**10.** 40. Slot 2 gets profit 20, slot 1 gets profit 15, slot 3 gets profit 5. The profit-10 job needs slot 1, which is taken.

**11.** Greedy takes 4 + 1 + 1, three coins. `C = [0, 1, 2, 1, 1, 2, 2]`. Optimum `C(6) = 2` via 3 + 3.

**12.** `[0, 4)`, `[3, 5)`, `[4, 8)`. Durations 4, 2, and 4. The two long intervals are compatible. The short middle one meets both, so any set that contains it has size 1.

**13.** Merge the two 1s. Parent weight 2. Remaining weights: 2 (parent), 2, 4.

**14.** The improving swap moves a small amount of weight from a worse item onto a better item that still has unused fraction. The weight-30 item does not fit in the residual 20, so a 0/1 algorithm cannot take “a little” of it. It would have to drop the weight-10 item instead, which ratio order never does.

**15.** Earliest deadline first. Profit is not in the objective.

**16.** Optimality is a claim about every input. Three agreeing inputs do not rule out a fourth where the rule loses. You need an exchange argument, or a counterexample if you are rejecting the rule.

**17.** Kruskal remains correct. The cut property does not require positive weights. Dijkstra does not remain correct.

**18.** Sorting by finish time, `Θ(n log n)`, unless the question already sorted the activities.

**19.** Latest feasible slot: P goes to slot 2, Q goes to slot 1, total 19. Earliest slot for P fills slot 1 and leaves Q with nowhere to go, total 10.

**20.** The weight-3 symbol is a child of the root, code length 1. Huffman merges two 1s, then merges that node with the remaining 1, then merges with 3. Depths 3, 3, 2, and 1. Weighted path length `3·1 + 1·2 + 1·3 + 1·3 = 11`. All depths equal to 2 give weighted path length `2·(3+1+1+1) = 12`, which is worse.

**21.** Let `a` be the earliest-finishing member of an optimal set. Then `f_g ≤ f_a`. Every other chosen activity starts at or after `f_a`, so it also starts at or after `f_g`. Replacing `a` by `g` keeps the set feasible and the same size.

**22.** If a worse-ratio item has a positive amount while a better-ratio item is not full, shift weight toward the better ratio. Value does not decrease and capacity stays feasible. Continue until the taken set is a prefix of the ratio order.

**23.** A combination that uses a 4 has remainder 2. With these denominations, 2 is two 1s, so the combination has three coins. Two 3s make 6 with two coins and use no 4. Every optimum has size 2, so none contains a 4.

**24.** Balanced: merge two pairs (cost 10 + 10) and then the two results (cost 20), total 40. Skewed: `(5+5)=10`, `(10+5)=15`, `(15+5)=20`, total 45. They differ because each original file is paid once for every merge that contains it. In the skewed tree the first file sits in every merge, so it is counted three times. In the balanced tree each file is counted twice.

**25.** A finishes first, so earliest-finish selects A and then cannot select B. Value 10. The optimal weighted choice is B alone, value 100.
