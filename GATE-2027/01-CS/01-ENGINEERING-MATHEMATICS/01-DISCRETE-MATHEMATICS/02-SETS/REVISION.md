# Sets — Quick Revision (Cheat Sheet)

## Core definitions
- \(a \in A\): element; \(A \subseteq B\): every element of A in B; \(A \subset B\): proper subset.
- \(\emptyset\): no elements; subset of every set; **not** element of every set.
- \(|A|\): cardinality (finite in GATE).

## Power set
- \(\mathcal{P}(A)\) = all subsets; \(|\mathcal{P}(A)| = 2^{|A|}\).
- Proper subsets of \(n\)-set: \(2^n - 1\) (exclude A itself).
- \(\mathcal{P}(\emptyset)=\{\emptyset\}\), size 1.

## Operations
- \(A \cup B\), \(A \cap B\), \(A - B\), \(A^c\) (w.r.t. universe U).
- \(A - B = A \cap B^c\). Disjoint: \(A \cap B = \emptyset\).
- \(A \triangle B = (A-B)\cup(B-A)\).

## De Morgan
- \((A \cup B)^c = A^c \cap B^c\)
- \((A \cap B)^c = A^c \cup B^c\)

## Inclusion–exclusion
- 2 sets: \(|A \cup B| = |A|+|B|-|A \cap B|\)
- 3 sets: singles − pairwise + triple
- \(|A^c| = |U| - |A|\)

## Cartesian product
- \(A \times B = \{(a,b)\}\); \(|A \times B| = |A|\cdot|B|\)
- Relation ⊆ \(A \times B\); function = special relation

## Traps (1-line)
- \(\in\) vs \(\subseteq\); \(\{1\}\) vs \(1\)
- Complement needs universe U
- \(\mathcal{P}(\{\emptyset\})\) has 2 elements
- Subsets containing fixed x: \(2^{n-1}\) from n-set
- Venn: read region carefully (only A, not A∩B)

