# Syntax-Directed Translation — Practice Questions

Original practice for GATE CS. These questions are not from any GATE paper. Attempt the questions before reading the solutions.

In these questions, an attribute written on the left-hand nonterminal is synthesized. An attribute written on a symbol of the right-hand side is inherited. A definition is S-attributed when every attribute is synthesized. It is L-attributed when every inherited attribute of a symbol \(X_j\) on a right-hand side depends only on inherited attributes of the left-hand nonterminal and on attributes of the symbols to the left of \(X_j\).

## Level 1 — Conceptual

## Q1 — MCQ

In an annotated parse tree, an attribute of a node that is computed from attributes of that node’s children is

A. an inherited attribute
B. a synthesized attribute
C. a lookahead token
D. a lexical attribute of the parent only

---

## Q2 — MSQ

Which statements about S-attributed definitions are true? Select all that apply.

A. Every attribute is synthesized.
B. The attributes can be evaluated while a bottom-up parser reduces.
C. An inherited attribute of a left sibling may be defined from a right sibling.
D. Every S-attributed definition is also L-attributed.

---

## Q3 — MCQ

An inherited attribute of a node is normally computed from

A. attributes of that node’s children only
B. attributes of the parent and of the siblings to its left
C. attributes of the sibling to its right only
D. the object code, after register allocation

---

## Q4 — MCQ

Which traversal always respects the dependencies of an L-attributed definition?

A. A depth-first left-to-right walk that computes a node’s inherited attributes before visiting its children, and the node’s synthesized attributes after the children return
B. A right-to-left walk that visits the rightmost child first
C. Any topological order, including orders that read a right sibling before a left sibling
D. A postorder walk that ignores inherited attributes

---

## Level 2 — Standard GATE Style

## Q5 — MCQ

The semantic rule attached to \(T \to \mathbf{num}\) is \(T.\mathrm{val} = \mathbf{num}.\mathrm{lexval}\). The attribute \(T.\mathrm{val}\) is

A. synthesized, and the rule is both S-attributed and L-attributed
B. inherited from \(\mathbf{num}\)
C. synthesized, but the rule is not L-attributed
D. neither synthesized nor inherited

---

## Q6 — NAT

The grammar gives \(*\) higher precedence than \(+\), and both operators associate to the left.

\[
\begin{align*}
E &\to E_1 + T & \{ E.\mathrm{val} = E_1.\mathrm{val} + T.\mathrm{val} \} \\
E &\to T & \{ E.\mathrm{val} = T.\mathrm{val} \} \\
T &\to T_1 * F & \{ T.\mathrm{val} = T_1.\mathrm{val} * F.\mathrm{val} \} \\
T &\to F & \{ T.\mathrm{val} = F.\mathrm{val} \} \\
F &\to \mathbf{num} & \{ F.\mathrm{val} = \mathbf{num}.\mathrm{val} \}
\end{align*}
\]

What integer is \(E.\mathrm{val}\) at the root of \(2 + 3 * 4\)? Enter an integer.

---

## Q7 — MSQ

The rules below type a comma-separated list. The procedure \(\mathrm{add}(\mathrm{id}, t)\) writes the type \(t\) into the symbol-table entry of \(\mathrm{id}\).

\[
\begin{align*}
D &\to T\, L & \{ L.\mathrm{type} = T.\mathrm{type} \} \\
T &\to \mathbf{int} & \{ T.\mathrm{type} = \mathrm{int} \} \\
T &\to \mathbf{float} & \{ T.\mathrm{type} = \mathrm{float} \} \\
L &\to L_1,\ \mathrm{id} & \{ L_1.\mathrm{type} = L.\mathrm{type};\ \mathrm{add}(\mathrm{id}, L.\mathrm{type}) \} \\
L &\to \mathrm{id} & \{ \mathrm{add}(\mathrm{id}, L.\mathrm{type}) \}
\end{align*}
\]

Select all that apply.

A. \(T.\mathrm{type}\) is synthesized.
B. \(L.\mathrm{type}\) is inherited.
C. The definition is S-attributed.
D. The definition is L-attributed.

---

## Q8 — MCQ

Using the definition in Q7, how many symbol-table insertions does the declaration \(\mathbf{float}\ a,\ b,\ c\) perform?

A. 1
B. 2
C. 3
D. 4

---

## Level 3 — Multi-Step

## Q9 — NAT

Evaluate the attributes below. The value printed is \(A.\mathrm{s}\).

\[
\begin{align*}
S &\to A & \{ A.\mathrm{i} = 2 \} \\
A &\to B\, C & \{ B.\mathrm{i} = A.\mathrm{i};\ C.\mathrm{i} = B.\mathrm{s};\ A.\mathrm{s} = C.\mathrm{s} \} \\
B &\to b & \{ B.\mathrm{s} = B.\mathrm{i} + 3 \} \\
C &\to c & \{ C.\mathrm{s} = C.\mathrm{i} \times 2 \}
\end{align*}
\]

What integer is printed? Enter an integer.

---

## Q10 — MSQ

For the definition in Q9, which statements hold? Select all that apply.

A. \(B.\mathrm{i}\) is inherited.
B. \(B.\mathrm{s}\) is synthesized.
C. \(C.\mathrm{i}\) depends on a symbol to the right of \(C\).
D. The definition is L-attributed.

---

## Q11 — MCQ

Replace only the rule for \(A \to B\, C\) in Q9 by

\[
\{ B.\mathrm{i} = C.\mathrm{s};\ C.\mathrm{i} = A.\mathrm{i};\ A.\mathrm{s} = B.\mathrm{s} \}.
\]

What is true of the revised rule?

A. It is still L-attributed, because both \(B.\mathrm{i}\) and \(C.\mathrm{i}\) are inherited attributes.
B. It is not L-attributed, because the inherited attribute \(B.\mathrm{i}\) depends on \(C\), which lies to the right of \(B\).
C. It is S-attributed, because \(A.\mathrm{s}\) is computed from \(B.\mathrm{s}\).
D. It uses only synthesized attributes.

---

## Level 4 — Tricky / Trap-Based

## Q12 — MCQ

Consider the single rule

\[
R \to A\, B \quad \{ B.\mathrm{i} = R.\mathrm{i} - 1;\ A.\mathrm{i} = B.\mathrm{i};\ R.\mathrm{s} = A.\mathrm{i} + 1 \}.
\]

Which classification is correct?

A. The rule is S-attributed.
B. The rule is L-attributed but not S-attributed.
C. The rule is neither S-attributed nor L-attributed.
D. The rule is S-attributed but not L-attributed.

---

## Q13 — MSQ

Consider the single rule

\[
P \to C\, D \quad \{ P.\mathrm{s} = C.\mathrm{s} + D.\mathrm{s};\ D.\mathrm{i} = C.\mathrm{s} + 2 \}.
\]

Select all that apply.

A. \(P.\mathrm{s}\) is synthesized.
B. \(D.\mathrm{i}\) is inherited.
C. The rule is L-attributed.
D. The rule is S-attributed.

---

## Q14 — NAT

Each digit is multiplied by the same inherited scale. This is not a place-value interpretation. The digit values in the input \(d\, d\, d\) are 2, then 1, then 4.

\[
\begin{align*}
S &\to L & \{ L.\mathrm{scale} = 3;\ S.\mathrm{val} = L.\mathrm{val} \} \\
L &\to d\, L_1 & \{ L_1.\mathrm{scale} = L.\mathrm{scale};\ L.\mathrm{val} = d.\mathrm{v} \times L.\mathrm{scale} + L_1.\mathrm{val} \} \\
L &\to \varepsilon & \{ L.\mathrm{val} = 0 \}
\end{align*}
\]

What integer is \(S.\mathrm{val}\)? Enter an integer.

---

## Level 5 — Challenge

## Q15 — MCQ

The dependency graph of an attribute grammar contains a cycle through \(A.\mathrm{s}\) and \(B.\mathrm{i}\). Which statement follows?

A. Any evaluation order still computes the same values.
B. No evaluation order respects every dependency.
C. The definition must be S-attributed.
D. A bottom-up parser can evaluate the attributes during reductions.

---

## Q16 — NAT

The operator \(\#\) has lower precedence than \(\%\). Both associate to the left. The rules are the same shape as in Q6, with \(\#\) in place of \(+\) and \(\%\) in place of \(*\): a \(\#\) node adds its children’s values, and a \(\%\) node multiplies them.

What integer is stored at the root of \(6 \# 4 \% 2 \# 5\)? Enter an integer.

---

## Answer Key

| Q | Type | Answer |
| --- | --- | --- |
| 1 | MCQ | B |
| 2 | MSQ | A, B, D |
| 3 | MCQ | B |
| 4 | MCQ | A |
| 5 | MCQ | A |
| 6 | NAT | 14 |
| 7 | MSQ | A, B, D |
| 8 | MCQ | C |
| 9 | NAT | 10 |
| 10 | MSQ | A, B, D |
| 11 | MCQ | B |
| 12 | MCQ | C |
| 13 | MSQ | A, B, C |
| 14 | NAT | 21 |
| 15 | MCQ | B |
| 16 | NAT | 19 |

## Detailed Solutions

### Q1

Answer: B

A synthesized attribute moves information up the tree: the semantic rule is attached to the production at that node and names an attribute of the production’s left-hand side, using attributes of the children. An inherited attribute moves information down or across the tree and is attached to a symbol on the right-hand side. A lookahead is a parsing token, not a node attribute computed from children.

### Q2

Answer: A, B, D

S-attributed means there are no inherited attributes at all, so A is true and C is false. C describes a dependence that only an inherited attribute can have. During a bottom-up parse, the children of a node have already been reduced before the parent is reduced, so every synthesized attribute of the parent can be computed at the reduction. That is B. If there are no inherited attributes, the L-attributed restriction on inherited attributes holds vacuously. Every S-attributed definition is L-attributed, so D is true.

### Q3

Answer: B

The semantic rule that computes an inherited attribute of a symbol sits on the production in which that symbol appears on the right-hand side. For the definition to be L-attributed, the rule may read the parent’s inherited attributes and the attributes of symbols already visited to the left. It may not read a right sibling. Computing an attribute only from children is the synthesized case. Register allocation is unrelated.

### Q4

Answer: A

An L-attributed definition is exactly the class that a depth-first left-to-right traversal can evaluate: on the way down, the inherited attributes of the next child depend only on information already known; on the way up, synthesized attributes are combined. A right-to-left walk would need the opposite sibling restriction. An arbitrary order can read a right sibling too early. A postorder walk computes synthesized attributes, but it does not pass inherited attributes down before the children are visited.

### Q5

Answer: A

The rule computes \(T.\mathrm{val}\), an attribute of the left-hand side, from the child’s lexical value. That is a synthesized attribute. The production has no inherited attribute, so this rule is S-attributed and therefore also L-attributed. The terminal \(\mathbf{num}\) does not inherit \(T.\mathrm{val}\); the dependence points from the child up to \(T\).

### Q6

Answer: 14

The grammar forces \(*\) to be recognized inside \(T\) and \(+\) to be recognized inside \(E\), so \(3 * 4\) is one \(T\). Left recursion is not needed to see the value, because there is only one \(+\):

\[
E.\mathrm{val} = 2 + (3 \times 4) = 2 + 12 = 14.
\]

A right-associative reading \( (2 + 3) * 4 = 20 \) is not a parse of this grammar.

### Q7

Answer: A, B, D

\(T.\mathrm{type}\) is computed by the productions \(T \to \mathbf{int}\) and \(T \to \mathbf{float}\), which assign an attribute of the left-hand side. It is synthesized. \(L.\mathrm{type}\) is assigned in \(D \to T\, L\) and in \(L \to L_1,\ \mathrm{id}\), both times as an attribute of a symbol on the right-hand side. It is inherited. Because an inherited attribute exists, the definition is not S-attributed.

It is L-attributed. In \(D \to T\, L\), \(L.\mathrm{type}\) depends on \(T.\mathrm{type}\), and \(T\) is to the left of \(L\). In \(L \to L_1,\ \mathrm{id}\), \(L_1.\mathrm{type}\) depends on the inherited attribute \(L.\mathrm{type}\) of the parent. The identifier is a terminal and receives no inherited attribute. No inherited attribute depends on a symbol to its right.

### Q8

Answer: C

The declaration is \(T = \mathbf{float}\) followed by the list \(a,\ b,\ c\). The list productions call \(\mathrm{add}\) once per identifier: once in the base production for the leftmost identifier, and once in each application of \(L \to L_1,\ \mathrm{id}\). Three identifiers produce three insertions, all with type \(\mathrm{float}\), because the inherited \(L.\mathrm{type}\) is copied unchanged down the list.

### Q9

Answer: 10

The only legal order is the L-attributed one.

- \(A.\mathrm{i} = 2\), then \(B.\mathrm{i} = A.\mathrm{i} = 2\).
- \(B.\mathrm{s} = 2 + 3 = 5\).
- \(C.\mathrm{i} = B.\mathrm{s} = 5\).
- \(C.\mathrm{s} = 5 \times 2 = 10\).
- \(A.\mathrm{s} = C.\mathrm{s} = 10\).

The printed value is 10. Using \(C\) before \(B.\mathrm{s}\) is known would read an uncomputed attribute.

### Q10

Answer: A, B, D

\(B.\mathrm{i}\) is assigned by the parent production \(A \to B\, C\), so it is inherited. \(B.\mathrm{s}\) is assigned by \(B \to b\), so it is synthesized. \(C.\mathrm{i} = B.\mathrm{s}\) reads \(B\), which is to the left of \(C\), not to the right. The dependencies match the L-attributed restriction: \(B.\mathrm{i}\) uses the parent’s inherited attribute \(A.\mathrm{i}\), and \(C.\mathrm{i}\) uses the left sibling’s synthesized attribute. D is true and C is false.

### Q11

Answer: B

\(B.\mathrm{i} = C.\mathrm{s}\) defines an inherited attribute of \(B\) from \(C.\mathrm{s}\). On the right-hand side \(B\, C\), the symbol \(C\) stands to the right of \(B\). An L-attributed definition forbids that dependence, so the rule is not L-attributed. It is also not S-attributed: \(B.\mathrm{i}\) and \(C.\mathrm{i}\) are inherited. Computing the synthesized attribute \(A.\mathrm{s}\) from a child does not cancel the illegal inherited dependence. The mere presence of inherited attributes is not what breaks the L-attributed condition; the rightward dependence does.

### Q12

Answer: C

\(A.\mathrm{i}\) and \(B.\mathrm{i}\) are attributes of right-hand symbols, so they are inherited. The rule is not S-attributed, which removes A and D. For the L-attributed test, look at each inherited attribute in left-to-right order. \(A\) is the first right-hand symbol. Its attribute is set by \(A.\mathrm{i} = B.\mathrm{i}\). That reads \(B\), the symbol to the right of \(A\). The dependence is illegal even though \(B.\mathrm{i} = R.\mathrm{i} - 1\), taken alone, would have been a legal use of the parent’s inherited attribute. One illegal dependence is enough: the rule is neither S-attributed nor L-attributed. The tempting classification “L-attributed but not S-attributed” would be right for a left-to-right copy such as \(B.\mathrm{i} = A.\mathrm{s}\), and it is wrong here because the copy runs from right to left.

### Q13

Answer: A, B, C

\(P.\mathrm{s}\) is an attribute of the left-hand side, computed from the children, so it is synthesized. \(D.\mathrm{i}\) is an attribute of a right-hand symbol, so it is inherited. \(D.\mathrm{i} = C.\mathrm{s} + 2\) reads \(C\), which is to the left of \(D\), and reads no right sibling. The rule is L-attributed. It is not S-attributed, because \(D.\mathrm{i}\) is inherited. D is false.

### Q14

Answer: 21

The grammar is right recursive, so the leftmost digit is the outermost \(d\). The scale 3 is copied unchanged into every \(L\). From the inside outward:

- the empty list contributes \(0\);
- the digit 4 contributes \(4 \times 3 + 0 = 12\);
- the digit 1 contributes \(1 \times 3 + 12 = 15\);
- the digit 2 contributes \(2 \times 3 + 15 = 21\).

Equivalently, each of 2, 1, and 4 is multiplied by 3 and the products are added: \(6 + 3 + 12 = 21\). A place-value reading \(2 \times 100 + 1 \times 10 + 4 = 214\) is a different attribute grammar. Nothing in these rules multiplies the scale by 10.

### Q15

Answer: B

Attribute evaluation is possible only if the dependency graph is acyclic, because each attribute must be computed after the attributes it reads. A cycle means some attribute depends, directly or indirectly, on itself, so no order satisfies every edge. S-attributed definitions have acyclic dependencies from children to parents; a cycle shows that this definition is not in that easy class. A bottom-up parser evaluates synthesized attributes at reductions and cannot solve a cycle by reducing.

### Q16

Answer: 19

Inside a \(T\)-like factor, \(\%\) is computed before \(\#\). The unique parse is

\[
(6 \# (4 \% 2)) \# 5.
\]

The inner product is \(4 \times 2 = 8\). The left sum is \(6 + 8 = 14\). The root sum is \(14 + 5 = 19\). Left association is what places the second \(\#\) at the root. Swapping the precedence to \((6 \# 4) \% (2 \# 5)\) is not a parse of this grammar.
