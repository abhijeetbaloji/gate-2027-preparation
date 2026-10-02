# Engineering Mathematics PYQ mapping

## 1. Scope

This folder maps GATE CS previous-year questions to the official GATE 2027 CS Engineering Mathematics syllabus.

A question is mapped only when it belongs to one of these syllabus lines:

- Discrete Mathematics: propositional and first order logic; sets; relations; functions; partial orders and lattices; monoids; groups; graphs (connectivity, matching, colouring); combinatorics (counting, recurrence relations, generating functions).
- Linear Algebra: matrices; determinants; system of linear equations; eigenvalues and eigenvectors; LU decomposition.
- Calculus: limits; continuity and differentiability; maxima and minima; mean value theorem; integration.
- Probability and Statistics: random variables; uniform, normal, exponential, Poisson, and binomial distributions; mean, median, mode, and standard deviation; conditional probability; Bayes theorem.

General Aptitude is not mapped. Digital Logic, Computer Organization and Architecture, Programming and Data Structures, Algorithms, Theory of Computation, Compiler Design, Operating Systems, Databases, and Computer Networks are not mapped.

A recurrence is mapped only when the stem does not present it as the running time of an algorithm. Graph questions are mapped only for connectivity, matching, or colouring, or when the asked quantity is a count under combinatorics.

## 2. Years covered

2026, 2025, 2024, 2023, 2022, 2021, 2020, 2019, 2018, 2017, 2016, 2015, 2014, 2013, 2012, 2011, 2010, 2009, 2008, 2007.

Papers were read newest first. Where a year has more than one stored CS paper, each stored paper was checked.

## 3. Official syllabus reference

`GATE-2027/00-GATE-2027/official-syllabus/CS/syllabus.md`, Section 1: Engineering Mathematics.

Topic and subtopic names in the mapping tables are taken from that section. No extra syllabus category was added.

## 4. Total Engineering Mathematics PYQs mapped

- Mapped rows: **299**
- Distinct questions: **278**

The distinct count treats the four 2013 booklets as one question set. Those booklets print the same Engineering Mathematics questions in different orders, so they contribute 28 rows and 7 distinct questions.

## 5. Coverage by year

Counts are mapped rows. For 2013, the row count is four times the distinct-question count.

| Year | Mapped rows |
|------|-------------|
| 2026 | 18 |
| 2025 | 18 |
| 2024 | 21 |
| 2023 | 9 |
| 2022 | 11 |
| 2021 | 20 |
| 2020 | 9 |
| 2019 | 10 |
| 2018 | 11 |
| 2017 | 10 |
| 2016 | 17 |
| 2015 | 30 |
| 2014 | 32 |
| 2013 | 28 (7 distinct questions, four booklets) |
| 2012 | 8 |
| 2011 | 8 |
| 2010 | 7 |
| 2009 | 9 |
| 2008 | 12 |
| 2007 | 11 |

## 6. Coverage by topic

Mapped rows, including each 2013 booklet.

| Topic | Rows |
|-------|------|
| Discrete Mathematics | 147 |
| Linear Algebra | 52 |
| Calculus | 39 |
| Probability and Statistics | 61 |

### Coverage by subtopic

| Topic | Subtopic | Rows |
|-------|----------|------|
| Discrete Mathematics | Combinatorics: counting | 17 |
| Discrete Mathematics | Combinatorics: generating functions | 4 |
| Discrete Mathematics | Combinatorics: recurrence relations | 16 |
| Discrete Mathematics | Functions | 10 |
| Discrete Mathematics | Graphs: colouring | 9 |
| Discrete Mathematics | Graphs: connectivity | 7 |
| Discrete Mathematics | Graphs: matching | 2 |
| Discrete Mathematics | Groups | 17 |
| Discrete Mathematics | Monoids | 2 |
| Discrete Mathematics | Partial orders and lattices | 5 |
| Discrete Mathematics | Propositional and first order logic | 41 |
| Discrete Mathematics | Relations | 11 |
| Discrete Mathematics | Sets | 6 |
| Linear Algebra | Determinants | 11 |
| Linear Algebra | Eigenvalues and eigenvectors | 23 |
| Linear Algebra | LU decomposition | 3 |
| Linear Algebra | Matrices | 6 |
| Linear Algebra | System of linear equations | 9 |
| Calculus | Continuity and differentiability | 13 |
| Calculus | Integration | 13 |
| Calculus | Limits | 8 |
| Calculus | Maxima and minima | 3 |
| Calculus | Mean value theorem | 2 |
| Probability and Statistics | Bayes theorem | 3 |
| Probability and Statistics | Binomial distribution | 2 |
| Probability and Statistics | Conditional probability | 16 |
| Probability and Statistics | Exponential distribution | 1 |
| Probability and Statistics | Mean | 11 |
| Probability and Statistics | Normal distribution | 1 |
| Probability and Statistics | Poisson distribution | 5 |
| Probability and Statistics | Random variables | 7 |
| Probability and Statistics | Standard deviation | 3 |
| Probability and Statistics | Uniform distribution | 12 |

Subtopics with no mapped question:

- Probability and Statistics: Median
- Probability and Statistics: Mode

2011 Booklet A Q.33 asks about the mean, the median, the mode, and the standard deviation together. It is filed once, under Mean, and marked AMBIGUOUS.


## 7. Uncertain or ambiguous classifications

12 mapped rows are marked `AMBIGUOUS` in the topic file. The note in that file states why.

- 2025 CS-2 Q.64 → Probability and Statistics / Uniform distribution. The asked quantity is the probability of a uniformly chosen square-invariant quadratic. The sample space is defined by a complex-polynomial condition, which is not a named Engineering Mathematics topic.
- 2024 CS1 Q.52 → Discrete Mathematics / Monoids. Asks whether two binary operators are associative and whether one distributes over the other. Identity and inverses are not stated, and distributivity is not a monoid axiom.
- 2021 CS Set-2 Q.37 → Linear Algebra / Matrices. Asks the maximum number of pairwise orthogonal nonzero vectors in R^10. Orthogonality and dimension are linear algebra, but the stem does not use matrices, determinants, linear systems, eigenvalues, or LU decomposition.
- 2015 7 February, Shift 1 Q.40 → Discrete Mathematics / Monoids. A binary operator on {0,1} is defined by a truth table, and the question asks whether it is commutative and associative. That is also a Boolean operator, which sits next to Digital Logic.
- 2015 7 February, Shift 1 Q.41 → Calculus / Integration. The PDF asks for the sum from x=1 to 99 of 1/(x(x+1)). It is a finite sum, not an integral. Integration is the nearest listed calculus topic and is not what the question asks.
- 2014 SET-3 Q.16 → Discrete Mathematics / Sets. Asks whether Sigma-star and its power set are countable. The objects are formal languages, so the question also sits in Theory of Computation.
- 2014 SET-3 Q.48 → Probability and Statistics / Random variables. Mutually exclusive events A and B partition the sample space, and the maximum of P(A)P(B) is asked. None of the named distributions or summary statistics is the object.
- 2013 Booklet A Q.1 → Discrete Mathematics / Groups. Same question in all four 2013 booklets, with a different question number in each booklet. Only commutativity and associativity are asked.
- 2013 Booklet B Q.25 → Discrete Mathematics / Groups. Same question in all four 2013 booklets, with a different question number in each booklet. Only commutativity and associativity are asked.
- 2013 Booklet C Q.12 → Discrete Mathematics / Groups. Same question in all four 2013 booklets, with a different question number in each booklet. Only commutativity and associativity are asked.
- 2013 Booklet D Q.14 → Discrete Mathematics / Groups. Same question in all four 2013 booklets, with a different question number in each booklet. Only commutativity and associativity are asked.
- 2011 Booklet A Q.33 → Probability and Statistics / Mean. One question asks which claim about the mean, median, mode, and standard deviation of a linearly transformed sequence is incorrect. Those four statistics are separate syllabus lines.

Some other rows are marked OK and still carry a note, because a formula, matrix, or graph is in the PDF and the text extract is incomplete. Those notes name the PDF as the authoritative copy. They are not a second classification.

### Mathematics questions checked and not mapped

These were read and left out because they are outside the GATE 2027 Engineering Mathematics lines above. This list is the record of those omissions. It is not a ranking.

- Numerical methods: Newton-Raphson, bisection, secant method, trapezoidal rule, Simpson's rule. Examples include 2012 Q.28, the trapezoidal-rule question in each 2013 booklet, 2014 SET-2 Q.40 and Q.46, 2014 SET-3 Q.46, 2015 Shift 2 Q.51, 2015 8 February Shift 1 Q.36, 2008 Q.21 and Q.22, 2010 Q.2.
- Vector-space dimension that is not one of the five linear-algebra lines: 2014 SET-3 Q.5 (dimension of an intersection of subspaces).
- Graph questions other than connectivity, matching, and colouring: planarity and faces, isomorphism, line graphs, Eulerian circuits, graphic degree sequences, and the handshaking lemma. Examples include 2012 Q.17 and Q.26, the handshaking-lemma question and the line-graph question in each 2013 booklet, 2014 SET-1 Q.52, 2014 SET-2 Q.3 and Q.51, 2014 SET-3 Q.52, 2015 Shift 1 Q.44, 2015 Shift 2 Q.61, 2016 CS-2 Q.28, 2017 Session 2 Q.23, 2007 Q.4 and Q.23, 2008 Q.23, 2009 Q.3, 2010 Q.1 and Q.28, 2011 Q.17.
- Minimum spanning trees, shortest paths, and graph traversals, including 2021 CS Set-1 Q.16 (number of edges in a connected planar graph with eight vertices and five faces) and Q.36 (diameter defined using shortest paths).
- Recurrences stated as the running time of an algorithm, including Towers of Hanoi execution time (2012 Q.16) and Master-theorem questions tied to an algorithm's time complexity.
- Number theory that is not counting, groups, or a named probability model: divisor counts such as 2014 SET-2 Q.49 and 2015 Shift 2 Q.14, and modular powers such as 2016 CS-2 Q.29 and 2019 Q.21 and Q.54.
- Probability used inside a Computer Networks question, including slotted LAN and ALOHA collision probabilities (2007 Q.65, 2015 Shift 1 Q.39, 2021 CS Set-2 Q.54).
- Huffman coding and matrix-chain multiplication, which are algorithm questions.
- General Aptitude questions that use probability or averages, including 2012 Q.63 and Q.64 and the General Aptitude block Q.56–Q.65 in each 2013 booklet.

## 8. Missing or unavailable papers

- 2017 Session 1 (CS-1, 11 February 2017, forenoon) is not in `GATE-2027/01-CS/12-PYQ/`. The archive note says the official file is not a readable PDF. Those questions were not reconstructed.
- 2027 has not been conducted.
- Years 2008 through 2026 other than 2017 Session 1 have the CS papers listed in `GATE-2027/01-CS/12-PYQ/README.md`. Each of those stored papers was checked.
- 2010 Q.12 and Q.24 have no readable stem in the text layer. The visible options are not mathematical, and those two questions were not mapped.
- 2011 has two questions whose printed numbers are missing in OCR, between Q.8 and Q.10 and between Q.31 and Q.33. Neither is Engineering Mathematics. The card-probability question is printed as Q.34 and is mapped.

## 9. Validation status

- [x] 2026 checked (CS-1 and CS-2)
- [x] 2025 checked (CS-1 and CS-2)
- [x] 2024 checked (CS1 and CS2)
- [x] 2023 checked
- [x] 2022 checked
- [x] 2021 checked (Set-1 and Set-2)
- [x] 2020 checked
- [x] 2019 checked (one CS paper; the printed header says Set-2)
- [x] 2018 checked
- [x] 2017 checked (Session 2 only; Session 1 is unavailable)
- [x] 2016 checked (CS-1 and CS-2)
- [x] 2015 checked (three shifts)
- [x] 2014 checked (SET-1, SET-2, and SET-3)
- [x] 2013 checked (booklets A, B, C, and D)
- [x] 2012 checked
- [x] 2011 checked
- [x] 2010 checked
- [x] 2009 checked
- [x] 2008 checked
- [x] 2007 checked

- [x] Every mapped row has a source path under `GATE-2027/01-CS/12-PYQ/`
- [x] Every mapped row has a year and a question number taken from the stored paper
- [x] Every mapped row uses a topic and subtopic from the official GATE 2027 CS Engineering Mathematics syllabus
- [x] A question is mapped once inside a single paper. The 2013 booklets repeat the same seven questions at different numbers; each booklet row points at that booklet's PDF
- [x] General Aptitude and the other nine CS syllabus sections are not given mapping rows
- [x] Out-of-syllabus mathematics that was seen is listed in section 7 rather than dropped without a note

Text was taken from the PDF text layer where that layer exists. Papers with no usable text layer were read with optical character recognition, and selected pages were checked against the PDF when the transcription was incomplete. The PDF remains the authoritative copy.
