# Divide and Conquer — Mistakes

### Common GATE Traps

| Trap | What goes wrong | Correct rule | Prevention |
|------|-----------------|--------------|------------|
| Merge sort `Θ(n)` | Case 2 loses its log | `2T(n/2) + Θ(n) = Θ(n log n)` | Equal level costs times `log n` levels |
| Sorted quicksort | Called the best case for an endpoint pivot | That input is the worst case: `T(n) = T(n−1) + Θ(n)` | Name the pivot |
| Master on a chain | `T(n−1) + n` forced into case 2 | Unroll arithmetic series, `Θ(n²)` | Master needs `n/b` |
| Uneven split | Master applied to `T(n/3)+T(2n/3)+n` | Tree argument: still `Θ(n log n)`, but not by plugging one `b` | Draw the long branch |
| Binary search recurrence | Written `2T(n/2)` | Only the half that can hold the key is solved: `T(n/2)+Θ(1)` | The discard step is the point |
| Closest pair | Combine called `Θ(n)` while each call sorts by y | Fresh y-sorts give `Θ(n log² n)` | Ask whether y-order is merged or rebuilt |
| Strip pairs | Every pair in the strip compared | Only `O(1)` later y-neighbours per point | The packing argument is the linearity |
| Strassen vs chain | `n^{log2 7}` used for parenthesisation | Strassen multiplies two matrices; chain order is `Θ(n³)` DP | Count how many matrices are input |
| Karatsuba | Four recursive products | Three products; the cross term is built from sums | The fourth product is the one that was eliminated |
| Max subarray | Only the crossing sum computed | Left and right recursions are required; or use Kadane in `Θ(n)` | A segment can lie entirely on one side |
| Quickselect | Worst case stated `Θ(n)` | Expected `Θ(n)`; worst `Θ(n²)`. Worst-case linear is median of medians | Say “expected” or “median of medians” |
| Inversions | A quadratic pair loop inside merge | Each merge emits the count in linear time | `r` left keys charge `r` when a right key is emitted |

### My Mistakes

Record your own errors after practice and past papers. Do not pre-fill this table.

| Date | Source | Question | Mistake | Root Cause | Correct Rule | Prevention |
|------|--------|----------|---------|-----------|--------------|------------|
| | | | | | | |
