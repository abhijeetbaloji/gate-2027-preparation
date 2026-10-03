# Tabular Method — Shortcuts

## 1. One-bit test before writing a dash

- **Solves.** Whether two labels combine.
- **When.** You are about to merge two rows of the table.
- **Why.** \(Px + Px' = P\) needs a single complemented variable. Two bit differences are not one use of that identity, and misaligned dashes are two different deleted variables.
- **Example.** \(0101\) and \(1101\) combine to \(-101\). \(0101\) and \(1010\) differ in three bits and do not combine.
- **Limit.** A pair that fails may still sit together inside a larger implicant built on a different route. The shortcut only rejects that pair.

## 2. Unticked means prime

- **Solves.** The prime count.
- **When.** Combining has stopped.
- **Why.** A ticked string is contained in a larger implicant, so it is not prime. An unticked string has no legal enlargement.
- **Example.** After a quad \(0--0\) is formed, each pair that produced it is ticked and is not an extra prime.
- **Limit.** Count the unticked strings at every stage, including unpaired minterms. Do not count only the largest stage.

## 3. Single mark means essential

- **Solves.** The essential-prime count.
- **When.** The chart is filled and only onset columns are present.
- **Why.** That minterm has no other prime, so every cover uses this row.
- **Example.** A minterm that paired with only one other minterm, and whose pair never grew, owns a private column.
- **Limit.** A prime can appear in every minimal cover without having a private minterm. The shortcut does not detect that stronger property. It also says nothing about don’t-care columns, which should not exist.

## 4. Don’t-care enlarges, then disappears

- **Solves.** Whether to include \(d(i)\) in the final term list.
- **When.** The onset cover is already complete without a prime that exists only because of don’t-cares.
- **Why.** The definition of “covers \(F\)” quantifies only over onset minterms.
- **Example.** A pair of a single onset minterm with a don’t-care may be the essential prime that covers that onset minterm. A group of only don’t-cares is a prime of a different function and is not required.
- **Limit.** Dropping a don’t-care prime is legal only after the onset columns are covered. Dropping it earlier can leave a 1 uncovered.
