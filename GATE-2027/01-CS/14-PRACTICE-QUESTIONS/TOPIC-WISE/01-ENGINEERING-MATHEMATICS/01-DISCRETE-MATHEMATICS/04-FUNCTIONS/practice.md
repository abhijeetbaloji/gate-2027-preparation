# Functions — Practice Questions

Original practice for GATE CS. These questions are not from any GATE paper. Attempt the questions before reading the solutions.

## Level 1 — Conceptual

## Q1 — MCQ

A function \(f: A \rightarrow B\) is a relation from \(A\) to \(B\) such that

A. every element of \(A\) is related to exactly one element of \(B\)
B. every element of \(B\) is related to exactly one element of \(A\)
C. every element of \(A\) is related to at least two elements of \(B\)
D. some element of \(A\) may be related to no element of \(B\)

---

## Q2 — MSQ

Let \(f: \mathbb{Z} \rightarrow \mathbb{Z}\) be defined by \(f(n) = n^{2}\). Which statements are true?

Select all that apply.

A. \(f\) is injective.
B. \(f\) is not injective.
C. \(f\) is surjective.
D. \(f\) is not surjective.

---

## Q3 — MCQ

Let \(A\) be a finite set and let \(f: A \rightarrow A\). Which statement is true?

A. If \(f\) is injective, then \(f\) is surjective.
B. If \(f\) is injective, then \(f\) is not surjective.
C. \(f\) may be injective without being surjective.
D. If \(f\) is surjective, then the image of \(f\) is a proper subset of \(A\).

---

## Q4 — MCQ

Thirteen laptops are each assigned to one of five labs. The minimum possible number of laptops in the most crowded lab is

A. \(2\)
B. \(3\)
C. \(5\)
D. \(13\)

---

## Level 2 — Standard GATE Style

## Q5 — NAT

Let \(|A| = 4\) and \(|B| = 3\). Enter the number of functions from \(A\) to \(B\).

---

## Q6 — MCQ

The number of injective functions from a set with \(3\) elements to a set with \(6\) elements is

A. \(18\)
B. \(120\)
C. \(216\)
D. \(0\)

---

## Q7 — MSQ

Let \(f: A \rightarrow B\) and \(g: B \rightarrow C\) be functions. Which statements are true for all such \(f\) and \(g\)?

Select all that apply.

A. If \(f\) and \(g\) are injective, then \(g \circ f\) is injective.
B. If \(f\) and \(g\) are surjective, then \(g \circ f\) is surjective.
C. \(g \circ f = f \circ g\).
D. If \(g \circ f\) is injective, then \(f\) is injective.

---

## Q8 — MCQ

The number of bijections from a set with \(4\) elements to itself is

A. \(16\)
B. \(24\)
C. \(256\)
D. \(4\)

---

## Level 3 — Multi-Step

## Q9 — NAT

Enter the number of surjective functions from a set with \(4\) elements to a set with \(3\) elements.

---

## Q10 — MCQ

Define \(f, g: \mathbb{R} \rightarrow \mathbb{R}\) by \(f(x) = x + 3\) and \(g(x) = 2x\). The function \((g \circ f) - (f \circ g)\) equals

A. the constant function \(3\)
B. the constant function \(-3\)
C. the constant function \(6\)
D. the function \(2x + 6\)

---

## Q11 — MSQ

Which equalities are true?

Select all that apply.

A. \(\lfloor -1.7 \rfloor = -2\)
B. \(\lceil -1.7 \rceil = -1\)
C. \(\lfloor -1.7 \rfloor = -1\)
D. \(\lfloor 4 \rfloor = 4\)

---

## Level 4 — Tricky / Trap-Based

## Q12 — MCQ

Let \(|A| = 2\) and \(|B| = 5\). The number of functions from \(A\) to \(B\) is

A. \(32\)
B. \(25\)
C. \(10\)
D. \(7\)

---

## Q13 — MSQ

Let \(A = \{1,2,3\}\), \(B = \{a,b,c,d\}\), and define \(f: A \rightarrow B\) by \(f(1) = a\), \(f(2) = b\), and \(f(3) = a\). Which statements are true?

Select all that apply.

A. \(f\) is injective.
B. \(f\) is not injective.
C. The image of \(f\) equals the codomain \(B\).
D. The image of \(f\) is \(\{a,b\}\).

---

## Q14 — NAT

Enter the number of injective functions from a set with \(5\) elements to a set with \(3\) elements.

---

## Level 5 — Challenge

## Q15 — MCQ

Let \(f: A \rightarrow B\) and \(g: B \rightarrow C\) be functions between nonempty sets, and suppose \(g \circ f\) is bijective. Which statement must be true?

A. \(f\) is surjective and \(g\) is injective.
B. \(f\) is injective and \(g\) is surjective.
C. Both \(f\) and \(g\) are bijective.
D. \(g\) is injective and \(f\) is surjective.

---

## Q16 — NAT

Enter the number of surjective functions from a set with \(5\) elements to a set with \(3\) elements.

---

## Answer Key

| Q | Type | Answer |
|---|------|--------|
| 1 | MCQ | A |
| 2 | MSQ | B, D |
| 3 | MCQ | A |
| 4 | MCQ | B |
| 5 | NAT | 81 |
| 6 | MCQ | B |
| 7 | MSQ | A, B, D |
| 8 | MCQ | B |
| 9 | NAT | 36 |
| 10 | MCQ | A |
| 11 | MSQ | A, B, D |
| 12 | MCQ | B |
| 13 | MSQ | B, D |
| 14 | NAT | 0 |
| 15 | MCQ | B |
| 16 | NAT | 150 |

## Detailed Solutions

### Q1

Answer: A

A function \(f: A \rightarrow B\) assigns to each domain element exactly one codomain element. As a set of pairs, every \(a \in A\) occurs as the first coordinate of exactly one pair.

B describes a bijection from \(B\) to \(A\), or a function \(B \rightarrow A\) that is bijective. An ordinary function \(A \rightarrow B\) may miss elements of \(B\) and may send two inputs to the same output, so elements of \(B\) need not have exactly one preimage.

C describes a relation that is multi-valued. A function forbids two different outputs for the same input.

D describes a partial map. In the GATE definition used here, a function on \(A\) is total: every element of the domain has an output.

### Q2

Answer: B, D

Injective means \(f(n_{1}) = f(n_{2})\) forces \(n_{1} = n_{2}\). Here \(f(2) = 4 = f(-2)\) and \(2 \neq -2\), so \(f\) is not injective. A is false and B is true.

Surjective onto \(\mathbb{Z}\) means every integer is a square of some integer. The integer \(-1\) is negative, and \(n^{2} \ge 0\) for every \(n \in \mathbb{Z}\), so \(-1\) has no preimage. Thus \(f\) is not surjective. C is false and D is true. The image is the set of perfect squares, a proper subset of the codomain \(\mathbb{Z}\).

On an infinite codomain, failing injectivity and failing surjectivity are separate facts. This example fails both, for different reasons: a pair of opposite inputs, and a negative output that is never attained.

### Q3

Answer: A

Let \(|A| = n\), with \(n\) finite. If \(f: A \rightarrow A\) is injective, distinct inputs have distinct outputs, so the image has \(n\) elements. The image is a subset of \(A\), and the only \(n\)-element subset of an \(n\)-element set is \(A\) itself. Therefore the image equals the codomain, and \(f\) is surjective. On a finite set of equal domain and codomain, injective, surjective, and bijective are equivalent.

B reverses the theorem. A permutation of a finite set is both injective and surjective.

C is true for some functions between infinite sets, such as \(n \mapsto 2n\) on \(\mathbb{Z}\), but it is false for every finite self-map. The question asks which statement is true in the finite setting given.

D contradicts the definition of surjective. If \(f\) is surjective, the image equals \(A\), so the image is not a proper subset of \(A\).

### Q4

Answer: B

This is the pigeonhole principle on a function from a set of \(13\) laptops to a set of \(5\) labs. If every lab received at most \(2\) laptops, the total would be at most \(5 \cdot 2 = 10\), which is less than \(13\). So some lab receives at least \(3\).

The bound \(3\) is achievable: the sizes \(3,3,3,2,2\) sum to \(13\). The minimum possible size of the most crowded lab is therefore
\[
\lceil 13/5 \rceil = \lceil 2.6 \rceil = 3.
\]

A is \(\lfloor 13/5 \rfloor = 2\). That is a possible size of some lab, but it is not forced as the maximum, and a maximum of \(2\) cannot accommodate \(13\) laptops. C is the number of labs. D is the total number of laptops, which would be the maximum in one lab only in the extreme assignment that leaves the other labs empty. The question asks for the minimum possible value of that maximum.

### Q5

Answer: 81

Each of the \(4\) domain elements independently chooses one of \(3\) outputs. The number of functions \(A \rightarrow B\) is
\[
|B|^{|A|} = 3^{4} = 81.
\]
The exponent is the domain size, because the choices are indexed by inputs. The swapped power \(4^{3} = 64\) counts functions from a \(3\)-element set to a \(4\)-element set. The product \(4 \cdot 3 = 12\) counts neither functions nor the full set of input-output choices.

### Q6

Answer: B

An injection from a set of \(m\) elements to a set of \(n\) elements exists only when \(m \le n\), and the count is the falling factorial
\[
P(n,m) = \frac{n!}{(n-m)!} = n(n-1)\cdots(n-m+1).
\]
Here \(m = 3\) and \(n = 6\), so
\[
P(6,3) = 6 \cdot 5 \cdot 4 = 120.
\]
The first input has \(6\) allowed outputs, the second has \(5\) remaining outputs, and the third has \(4\).

A is \(6 \cdot 3 = 18\), which multiplies the two cardinalities once and does not shrink the pool of outputs. C is \(6^{3} = 216\), the number of all functions, including those that repeat an output. D would be correct only if the domain were larger than the codomain. Here \(3 \le 6\), so injections exist.

### Q7

Answer: A, B, D

A is true. Suppose \((g \circ f)(a_{1}) = (g \circ f)(a_{2})\). Injectivity of \(g\) forces \(f(a_{1}) = f(a_{2})\), and injectivity of \(f\) then forces \(a_{1} = a_{2}\).

B is true. Take \(c \in C\). Surjectivity of \(g\) supplies \(b \in B\) with \(g(b) = c\). Surjectivity of \(f\) supplies \(a \in A\) with \(f(a) = b\). Then \((g \circ f)(a) = c\).

D is true even without any hypothesis on \(g\) beyond \(g \circ f\) being injective. If \(f(a_{1}) = f(a_{2})\), apply \(g\) to both sides to get \((g \circ f)(a_{1}) = (g \circ f)(a_{2})\), and injectivity of the composition forces \(a_{1} = a_{2}\).

C is false. The composite \(f \circ g\) is not even defined from the stated types unless \(C \subseteq A\) in the appropriate way: \(g\) outputs an element of \(C\), while \(f\) expects an element of \(A\). Even when \(A = B = C = \mathbb{R}\), \(f(x) = x + 3\), and \(g(x) = 2x\), one composite is \(2x + 6\) and the other is \(2x + 3\). Composition is not commutative.

### Q8

Answer: B

A bijection from a finite set to itself is a permutation of that set. For a set with \(4\) elements the number of permutations is
\[
4! = 4 \cdot 3 \cdot 2 \cdot 1 = 24.
\]
Equivalently, it is the injection count \(P(4,4) = 4!\), since domain and codomain have the same finite size and every injection is then a bijection.

A is \(4^{2} = 16\), which is neither \(4!\) nor \(4^{4}\). C is \(4^{4} = 256\), the number of all self-maps, most of which repeat a value and miss another. D is the size of the set, not the number of ways to permute it.

### Q9

Answer: 36

The inclusion–exclusion formula for the number of surjections from an \(m\)-element set onto an \(n\)-element set is
\[
\sum_{i=0}^{n} (-1)^{i} \binom{n}{i} (n-i)^{m}.
\]
Here \(m = 4\) and \(n = 3\). Also \(0^{4} = 0\) because the exponent is positive.

\begin{align*}
i = 0 &\colon \binom{3}{0} 3^{4} = 1 \cdot 81 = 81, \\
i = 1 &\colon -\binom{3}{1} 2^{4} = -3 \cdot 16 = -48, \\
i = 2 &\colon \binom{3}{2} 1^{4} = 3 \cdot 1 = 3, \\
i = 3 &\colon -\binom{3}{3} 0^{4} = -1 \cdot 0 = 0.
\end{align*}
Add the terms:
\[
81 - 48 + 3 + 0 = 36.
\]
The first term \(81\) counts all functions. Each later term corrects for functions that miss at least a chosen set of outputs. Using the injection count \(P(3,4)\) is invalid because \(4 > 3\), and that count is \(0\), while surjections from a larger domain onto a smaller codomain can exist. Forgetting the sign of the \(i = 1\) term would add \(48\) instead of subtracting it.

### Q10

Answer: A

Composition applies the right-hand function first:
\begin{align*}
(g \circ f)(x) &= g(f(x)) = g(x+3) = 2(x+3) = 2x+6, \\
(f \circ g)(x) &= f(g(x)) = f(2x) = 2x+3.
\end{align*}
Subtract pointwise:
\[
(g \circ f)(x) - (f \circ g)(x) = (2x+6) - (2x+3) = 3.
\]
The difference is the constant function \(3\).

B is the result of subtracting in the opposite order, \((f \circ g) - (g \circ f) = -3\). The question fixes the order \(g \circ f\) minus \(f \circ g\). C is the constant term of \(g \circ f\) before \(f \circ g\) is subtracted. D is \(g \circ f\) itself, not the difference of the two composites.

### Q11

Answer: A, B, D

The floor \(\lfloor x \rfloor\) is the greatest integer less than or equal to \(x\). The ceiling \(\lceil x \rceil\) is the least integer greater than or equal to \(x\).

For \(x = -1.7\), the integers surrounding it are \(-2\) and \(-1\), with \(-2 < -1.7 < -1\). The greatest integer still at most \(-1.7\) is \(-2\), so A is true. The least integer still at least \(-1.7\) is \(-1\), so B is true.

C uses truncation toward zero. That operation sends \(-1.7\) to \(-1\), but floor moves away from zero on negative non-integers. Since \(-1 > -1.7\), \(-1\) is not less than or equal to \(-1.7\), and it is not the floor.

D is true because \(4\) is already an integer, and \(\lfloor n \rfloor = n\) for every integer \(n\). The same identity holds for the ceiling of an integer.

### Q12

Answer: B

The number of functions from \(A\) to \(B\) is \(|B|^{|A|}\):
\[
5^{2} = 25.
\]
Each of the two inputs chooses one of five outputs.

A is \(2^{5} = 32\), which swaps the base and the exponent and counts functions from a five-element set to a two-element set. C is \(5 \cdot 2 = 10\), a single product of the cardinalities rather than a power. D is \(5 + 2 = 7\), the sum of the cardinalities.

### Q13

Answer: B, D

The values \(f(1)\) and \(f(3)\) are both \(a\), while \(1 \neq 3\). A function that sends two domain elements to the same codomain element is not injective. A is false and B is true.

The image is the set of values actually attained:
\[
\{f(1), f(2), f(3)\} = \{a, b, a\} = \{a,b\}.
\]
D is true. The codomain is \(\{a,b,c,d\}\). Since \(c\) and \(d\) are missed, the image is a proper subset of the codomain, and C is false. Surjectivity would require the image to equal \(B\). Containing the image inside \(B\) is true of every function into \(B\), and it is not the surjective condition.

### Q14

Answer: 0

An injective function from a finite set \(A\) to a finite set \(B\) can exist only when \(|A| \le |B|\). Each input consumes a distinct output, so there must be at least as many outputs as inputs. Here \(|A| = 5\) and \(|B| = 3\), and \(5 > 3\). The injection count is defined to be \(0\) in this case:
\[
P(3,5) = 0.
\]
The power \(3^{5} = 243\) counts all functions, almost all of which repeat an output. The factorial \(5! = 120\) counts permutations of the domain, which would be functions from a five-element set to itself, not into a three-element set.

### Q15

Answer: B

Since \(g \circ f\) is bijective, it is injective and surjective.

Injectivity of the composition forces injectivity of \(f\). If \(f(a_{1}) = f(a_{2})\), then \(g(f(a_{1})) = g(f(a_{2}))\), so \(a_{1} = a_{2}\) because \(g \circ f\) is injective.

Surjectivity of the composition forces surjectivity of \(g\). For any \(c \in C\) there is an \(a \in A\) with \(g(f(a)) = c\), and then \(f(a)\) is an element of \(B\) that \(g\) sends to \(c\).

Thus \(f\) is injective and \(g\) is surjective.

The two maps need not be bijective. Take \(A = \{1\}\), \(B = \{1,2\}\), and \(C = \{1\}\), with \(f(1) = 1\), \(g(1) = 1\), and \(g(2) = 1\). Then \(g \circ f: A \rightarrow C\) sends \(1\) to \(1\), so it is bijective. But \(f\) misses \(2\), so \(f\) is not surjective, and \(g(1) = g(2)\), so \(g\) is not injective. This single example eliminates A, C, and D. Option A asks for a surjective \(f\) and an injective \(g\). Option D swaps those demands. Option C asks for both maps to be bijective. None of those claims survives the example, while B matches the proof above.

### Q16

Answer: 150

Use inclusion–exclusion with domain size \(m = 5\) and codomain size \(n = 3\). First compute the powers: \(3^{5} = 243\), \(2^{5} = 32\), \(1^{5} = 1\), and \(0^{5} = 0\).

\begin{align*}
i = 0 &\colon \binom{3}{0} 3^{5} = 243, \\
i = 1 &\colon -\binom{3}{1} 2^{5} = -3 \cdot 32 = -96, \\
i = 2 &\colon \binom{3}{2} 1^{5} = 3, \\
i = 3 &\colon -\binom{3}{3} 0^{5} = 0.
\end{align*}
Add the signed terms:
\[
243 - 96 + 3 + 0 = 150.
\]
The \(243\) functions include maps whose image has size \(1\) or \(2\). Subtracting the maps that miss at least one named output, and then adding back the maps that were subtracted too often, leaves only the maps whose image is all three outputs.

The injection formula does not apply: \(P(3,5) = 0\) because five inputs cannot receive distinct outputs from a three-element codomain. Surjections are still possible because outputs may be reused. The two-codomain shortcut \(2^{5} - 2 = 30\) answers a different problem, surjections onto a two-element set, and it is not the three-element count.
