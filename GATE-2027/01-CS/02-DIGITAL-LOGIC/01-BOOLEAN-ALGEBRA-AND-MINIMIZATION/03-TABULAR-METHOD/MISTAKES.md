# Tabular Method — Mistakes

### Common mistakes

| Mistake | What goes wrong | Correct rule |
|---------|-----------------|--------------|
| Distance-2 merge | A dash written over two bit changes | Combine only distance 1, dashes aligned |
| Don’t-care left out of the list | A larger prime missed | Don’t-cares participate in combining |
| Don’t-care column | An X is “covered” as if it were a 1 | Chart columns are onset minterms |
| Tick deletes the column | A combined minterm is dropped from the cover | Tick removes a prime candidate, not a column |
| Prime count used for essentials | 6 primes reported as 6 essentials | Essentials are single-mark columns |
| Essential used for “in every minimum” | A globally forced prime called essential | Essential means a private minterm |
| Dash read as a bit value | The string is decoded as an integer | Dash means the variable is absent |
| Minimal SOP used as the prime list | Redundant primes omitted from the count | The question’s noun decides the count |

### PYQ-shaped traps

- The mapped 2015 stem asks for the **total** number of prime implicants of a listed onset. That is the number of unticked strings, not the number of terms you would finally wire, except when every prime happens to be essential.
- The stem writes a sum, not the words “Quine–McCluskey.” The table is still the reliable way to count primes once a map circle is easy to under-count.
- No verified key is stored in the mapping. Recompute the table; do not memorise a number from an unmarked solution.

### Calculation slips

- Grouping by the integer value instead of by the number of 1s, then failing to compare adjacent buckets.
- Combining \(0101\) with \(0110\) because both have two 1s. They differ in two bits.
- Forgetting that the same quad can be reached by two pair-routes, and counting it twice.

### My Mistakes

| Date | Source | Question | Mistake | Root Cause | Correct Rule | Prevention |
|------|--------|----------|---------|------------|--------------|------------|
| | | | | | | |
