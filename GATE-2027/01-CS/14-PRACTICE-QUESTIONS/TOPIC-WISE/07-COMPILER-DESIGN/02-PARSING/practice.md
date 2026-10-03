# Parsing — Practice Questions

Original practice for GATE CS. These questions are not from any GATE paper. Attempt the questions before reading the solutions.

## Level 1 — Conceptual

## Q1 — MCQ

An LR parser builds the parse by recognising handles. Which derivation does its sequence of reductions trace?

A. A leftmost derivation, from the start symbol toward the input
B. A leftmost derivation, from the input toward the start symbol
C. A rightmost derivation, in reverse
D. A rightmost derivation, from the start symbol toward the input

---

## Q2 — MSQ

Which of the following are bottom-up parsers? Select all that apply.

A. Shift-reduce parser
B. Recursive-descent predictive parser
C. LR parser
D. Table-driven LL(1) parser

---

## Q3 — MCQ

While computing FIRST and FOLLOW for a grammar whose start symbol is \(S\), where is the input end marker \(\$\) placed?

A. In FIRST(\(S\)), and nowhere else
B. In FOLLOW(\(S\))
C. In FOLLOW of every nonterminal
D. In neither FIRST nor FOLLOW; \(\$\) is used only by the lexer

---

## Q4 — MSQ

Which of the following grammars are left recursive? Select all that apply.

A. \(A \to A a \mid b\)
B. \(A \to a A \mid b\)
C. \(S \to A a,\quad A \to B b,\quad B \to S c \mid d\)
D. \(A \to a A b \mid c\)

---

## Q5 — MCQ

Which statement is true?

A. Every LL(1) grammar is unambiguous.
B. Every unambiguous context-free grammar is LL(1).
C. Every LR(1) grammar is LL(1).
D. Immediate left recursion does not prevent a grammar from being LL(1).

---

## Level 2 — Standard GATE Style

## Q6 — NAT

Consider the grammar with start symbol \(S\).

\[
\begin{align*}
S &\to P Q \\
P &\to p P \mid \varepsilon \\
Q &\to q Q \mid r
\end{align*}
\]

How many terminals are in FIRST(\(S\))? Do not count \(\varepsilon\). Enter an integer.

---

## Q7 — MCQ

For the grammar in Q6, FOLLOW(\(P\)) is

A. \(\{ q, r, \$ \}\)
B. \(\{ q, r \}\)
C. \(\{ p \}\)
D. \(\{ \$ \}\)

---

## Q8 — MSQ

For the grammar in Q6, which LL(1) parsing-table entries are correct? Select all that apply.

A. On nonterminal \(P\) and lookahead \(p\), expand \(P \to p P\).
B. On nonterminal \(P\) and lookahead \(q\), expand \(P \to \varepsilon\).
C. On nonterminal \(P\) and lookahead \(r\), expand \(P \to \varepsilon\).
D. On nonterminal \(Q\) and lookahead \(p\), expand \(Q \to q Q\).

---

## Q9 — MCQ

The grammar \(S \to S + S \mid S * S \mid \mathrm{id}\) is used with no precedence declared outside the grammar. How many distinct parse trees does \(\mathrm{id} + \mathrm{id} * \mathrm{id}\) have?

A. 1
B. 2
C. 3
D. 5

---

## Q10 — MCQ

The grammar below is not left recursive. \(C\) and \(D\) are nonterminals that do not derive \(\varepsilon\).

\[
S \to a b C \mid a b D \mid a e
\]

Which grammar is a full left-factoring of this grammar?

A. \(S \to a S_1,\quad S_1 \to b S_2 \mid e,\quad S_2 \to C \mid D\)
B. \(S \to a b S_1,\quad S_1 \to C \mid D \mid e\)
C. \(S \to a S_1 \mid e,\quad S_1 \to b C \mid b D\)
D. \(S \to a S_1,\quad S_1 \to b C \mid b D \mid e\)

---

## Q11 — MCQ

For \(S \to A B\), \(A \to a\), and \(B \to b\), one rightmost derivation is

\[
S \Rightarrow A B \Rightarrow A b \Rightarrow a b.
\]

In the right-sentential form \(A b\), the handle is

A. \(A\)
B. \(b\)
C. \(A b\)
D. \(S\)

---

## Level 3 — Multi-Step

## Q12 — NAT

The augmented grammar below is parsed with the canonical collection of LR(0) sets of items. \(S'\) is the new start symbol.

\[
\begin{align*}
S' &\to S \\
S &\to X X \\
X &\to x X \mid y
\end{align*}
\]

How many LR(0) states are in the collection? Enter an integer.

---

## Q13 — MCQ

For the grammar in Q12, which statement is true?

A. The grammar is LR(0).
B. An SLR(1) parser for the grammar has a shift/reduce conflict.
C. The grammar is ambiguous.
D. The grammar is not LR(1).

---

## Q14 — MSQ

For the grammar in Q12, let \(I_0\) be the closure of \(\{ S' \to \cdot S \}\). Select all that apply.

A. GOTO(\(I_0\), \(X\)) contains the item \(S \to X \cdot X\).
B. GOTO(\(I_0\), \(y\)) contains the item \(X \to y \cdot\).
C. GOTO(\(I_0\), \(x\)) contains the item \(X \to x \cdot X\).
D. GOTO(\(I_0\), \(S\)) contains the item \(S \to X X \cdot\).

---

## Q15 — NAT

Using the LR(0) automaton of the grammar in Q12, a shift-reduce parser reads the input \(xyxy\). How many reduce moves does it make before accepting? Enter an integer.

---

## Q16 — MCQ

Consider this grammar.

\[
\begin{align*}
S &\to A a \\
A &\to b A \mid \varepsilon
\end{align*}
\]

Which description of its LL(1) table is correct?

A. On lookahead \(b\), expand \(A \to b A\); on lookahead \(a\), expand \(A \to \varepsilon\). There is no conflict.
B. On lookahead \(b\), expand \(A \to \varepsilon\); on lookahead \(a\), expand \(A \to b A\).
C. Both productions of \(A\) are entered in the cell \((A, a)\).
D. FOLLOW(\(A\)) contains \(\$\), so \(A \to \varepsilon\) is also entered on \(\$\).

---

## Level 4 — Tricky / Trap-Based

## Q17 — MCQ

For the grammar

\[
\begin{align*}
S &\to A a \\
A &\to b A \mid \varepsilon
\end{align*}
\]

a computation puts nothing in FOLLOW(\(S\)), on the grounds that \(S\) never appears on a right-hand side. Which set is actually FOLLOW(\(S\))?

A. \(\emptyset\)
B. \(\{ a \}\)
C. \(\{ \$ \}\)
D. \(\{ a, \$ \}\)

---

## Q18 — MSQ

Consider the grammar

\[
\begin{align*}
S &\to A a \\
A &\to B b \\
B &\to S c \mid d
\end{align*}
\]

Select all that apply.

A. The grammar is immediately left recursive.
B. The grammar is indirectly left recursive.
C. The two productions of \(B\) have a common terminal prefix, so left factoring applies directly to them.
D. \(\mathrm{FIRST}(S c) \cap \mathrm{FIRST}(d)\) is nonempty, so the grammar is not LL(1).

---

## Q19 — MSQ

Consider the grammar

\[
\begin{align*}
S &\to a A d \mid b B d \mid a B e \mid b A e \\
A &\to c \\
B &\to c
\end{align*}
\]

Select all that apply.

A. An SLR(1) parser has a reduce/reduce conflict.
B. The conflicting LR(0) state contains both \(A \to c \cdot\) and \(B \to c \cdot\).
C. FOLLOW(\(A\)) = FOLLOW(\(B\)) = \(\{ d, e \}\).
D. The grammar is ambiguous.

---

## Level 5 — Challenge

## Q20 — NAT

For the grammar in Q19, an SLR(1) parser reports a reduce/reduce conflict on how many distinct lookahead terminals? Enter an integer.

---

## Q21 — MCQ

Consider the grammar

\[
\begin{align*}
S &\to L \# R \mid R \\
L &\to @ R \mid n \\
R &\to L
\end{align*}
\]

Which statement is true?

A. An SLR(1) parser has a shift/reduce conflict on \(\#\), and the grammar is still LR(1).
B. Both the SLR(1) parser and the canonical LR(1) parser have a reduce/reduce conflict.
C. The grammar is LR(0).
D. The grammar is LL(1).

---

## Q22 — MSQ

Select all that apply.

A. Every LR(0) grammar is SLR(1).
B. Every SLR(1) grammar is LALR(1).
C. Every LALR(1) grammar is canonical LR(1).
D. Every canonical LR(1) grammar is LL(1).

---

## Answer Key

| Q | Type | Answer |
| --- | --- | --- |
| 1 | MCQ | C |
| 2 | MSQ | A, C |
| 3 | MCQ | B |
| 4 | MSQ | A, C |
| 5 | MCQ | A |
| 6 | NAT | 3 |
| 7 | MCQ | B |
| 8 | MSQ | A, B, C |
| 9 | MCQ | B |
| 10 | MCQ | A |
| 11 | MCQ | B |
| 12 | NAT | 7 |
| 13 | MCQ | A |
| 14 | MSQ | A, B, C |
| 15 | NAT | 5 |
| 16 | MCQ | A |
| 17 | MCQ | C |
| 18 | MSQ | B, D |
| 19 | MSQ | A, B, C |
| 20 | NAT | 2 |
| 21 | MCQ | A |
| 22 | MSQ | A, B, C |

## Detailed Solutions

### Q1

Answer: C

A bottom-up parser shifts tokens until the right-hand side of a production sits on top of the stack as a handle, then reduces that handle to the nonterminal on the left. The handle of a right-sentential form is the right-hand side introduced by the last step of a rightmost derivation. Replaying the reductions from the input back to the start symbol therefore reconstructs a rightmost derivation in reverse. It is not a leftmost derivation. LL parsers are the ones that expand leftmost nonterminals.

### Q2

Answer: A, C

A shift-reduce parser and an LR parser build the tree from the leaves upward by shifting and reducing. A recursive-descent parser and a table-driven LL(1) parser expand the start symbol toward the input, so they are top-down. Predictive and LL(1) are not bottom-up methods.

### Q3

Answer: B

By definition, FOLLOW(\(S\)) contains the end marker \(\$\), because the start symbol is followed by the end of the input. The marker is not a member of FIRST(\(S\)) unless the grammar’s own terminals include it, which it does not. It is not added to the FOLLOW set of every nonterminal; a nonterminal receives \(\$\) only if it can appear at the end of some derivation from \(S\). The lexer never sees \(\$\). It is a parser convention.

### Q4

Answer: A, C

Grammar A has the immediate left recursion \(A \Rightarrow A a\). Grammar C has the indirect cycle \(S \Rightarrow A a \Rightarrow B b a \Rightarrow S c b a\), so a nonterminal derives a sentential form that starts with itself. Grammar B is immediately right recursive: the recursive occurrence of \(A\) is at the right end. Grammar D is neither left nor right recursive in the one-sided sense; the recursive \(A\) is strictly inside \(a\) and \(b\). Only A and C are left recursive.

### Q5

Answer: A

If a grammar is LL(1), each (nonterminal, lookahead) pair selects at most one production, so each string has at most one leftmost derivation. An LL(1) grammar is therefore unambiguous. The converse is false: many unambiguous grammars have left recursion, common prefixes, or conflicts that one token cannot resolve. LR(1) is a larger class than LL(1); the grammar of Q21 is LR(1) and not LL(1). Immediate left recursion always makes FIRST of the recursive production intersect FIRST of the other alternatives, or else the left-recursive nonterminal is unproductive, so it destroys the LL(1) property for any grammar that derives a terminal string.

### Q6

Answer: 3

\(P\) is nullable because of \(P \to \varepsilon\). FIRST(\(P\)) = \(\{ p \}\). FIRST(\(Q\)) = \(\{ q, r \}\), and \(Q\) is not nullable. Because \(P\) is nullable,

\[
\mathrm{FIRST}(S) = \mathrm{FIRST}(P) \cup \mathrm{FIRST}(Q) = \{ p, q, r \}.
\]

The set contains 3 terminals.

### Q7

Answer: B

\(P\) occurs only in \(S \to P Q\) and in \(P \to p P\). In \(S \to P Q\), everything in FIRST(\(Q\)) follows \(P\). Since \(Q\) is not nullable, FOLLOW(\(S\)) is not copied into FOLLOW(\(P\)). In \(P \to p P\), the occurrence of \(P\) is at the end, so FOLLOW(\(P\)) is copied into itself and adds nothing new. FOLLOW(\(S\)) = \(\{ \$ \}\), but that does not reach \(P\). Therefore FOLLOW(\(P\)) = \(\{ q, r \}\). The end marker is not in FOLLOW(\(P\)).

### Q8

Answer: A, B, C

FIRST(\(p P\)) = \(\{ p \}\), so cell \((P, p)\) holds \(P \to p P\). The production \(P \to \varepsilon\) is used on every lookahead in FOLLOW(\(P\)) = \(\{ q, r \}\). Both B and C are correct, and these sets are disjoint from \(\{ p \}\), so the row is LL(1). FIRST(\(Q\)) = \(\{ q, r \}\). Lookahead \(p\) is not in FIRST(\(Q\)) and \(Q\) is not nullable, so cell \((Q, p)\) is empty. D is not a table entry.

### Q9

Answer: B

The two operators are introduced by separate productions, and either production may be the root. The two trees are

- \(S \Rightarrow S + S\), with the right \(S\) rewritten by \(S * S\), giving \((\mathrm{id} + (\mathrm{id} * \mathrm{id}))\);
- \(S \Rightarrow S * S\), with the left \(S\) rewritten by \(S + S\), giving \(((\mathrm{id} + \mathrm{id}) * \mathrm{id})\).

No third shape exists: there are only two internal operators and the grammar has no other productions that could associate them. The grammar is ambiguous, which is why the count is greater than 1. Ordinary precedence is not present in this grammar, so both trees are legal.

### Q10

Answer: A

The three alternatives share the terminal prefix \(a\). Factoring \(a\) out leaves \(S \to a S_1\) and \(S_1 \to b C \mid b D \mid e\). The first two alternatives of \(S_1\) still share \(b\). Factoring \(b\) out leaves \(S_1 \to b S_2 \mid e\) and \(S_2 \to C \mid D\). That is option A, and the resulting FIRST sets \(\{ b \}\) and \(\{ e \}\), then \(\{ \mathrm{FIRST}(C) \}\) and \(\{ \mathrm{FIRST}(D) \}\), are disjoint.

Option B keeps \(e\) as an alternative of a nonterminal that was introduced only after \(ab\), so it generates \(abe\), which the original grammar does not generate. Option C drops the original alternative \(a e\) as a string that starts with \(a\), and it generates a bare \(e\). Option D factors \(a\) but leaves the common prefix \(b\) unfactored, so it is not a full left-factoring: \(S_1\) still has two productions whose FIRST sets both contain \(b\).

### Q11

Answer: B

The step \(A B \Rightarrow A b\) replaces \(B\) by \(b\), and that \(B\) was the rightmost nonterminal. The handle in \(A b\) is the right-hand side \(b\), to be reduced by \(B \to b\). The symbol \(A\) is not a handle yet; it is reduced only in the later step \(A b \Rightarrow a b\) after \(b\) has already been reduced in the forward rightmost derivation. Equivalently, in the bottom-up order the first reduction of the sentential form \(A b\) is \(b\) to \(B\).

### Q12

Answer: 7

\(I_0 = \mathrm{CLOSURE}(\{ S' \to \cdot S \})\) is

\[
S' \to \cdot S,\quad S \to \cdot X X,\quad X \to \cdot x X,\quad X \to \cdot y.
\]

The distinct GOTO states are:

| State | How it is reached | Items |
| --- | --- | --- |
| \(I_1\) | GOTO(\(I_0\), \(X\)) | \(S \to X \cdot X,\ X \to \cdot x X,\ X \to \cdot y\) |
| \(I_2\) | GOTO(\(I_0\), \(x\)) | \(X \to x \cdot X,\ X \to \cdot x X,\ X \to \cdot y\) |
| \(I_3\) | GOTO(\(I_0\), \(y\)) | \(X \to y \cdot\) |
| \(I_4\) | GOTO(\(I_0\), \(S\)) | \(S' \to S \cdot\) |
| \(I_5\) | GOTO(\(I_2\), \(X\)) | \(X \to x X \cdot\) |
| \(I_6\) | GOTO(\(I_1\), \(X\)) | \(S \to X X \cdot\) |

GOTO(\(I_1\), \(x\)) and GOTO(\(I_2\), \(x\)) return \(I_2\). GOTO(\(I_1\), \(y\)) and GOTO(\(I_2\), \(y\)) return \(I_3\). No further states appear. The collection has the seven states \(I_0\) through \(I_6\).

### Q13

Answer: A

Every completed item sits in a state by itself: \(X \to y \cdot\) in \(I_3\), \(X \to x X \cdot\) in \(I_5\), \(S \to X X \cdot\) in \(I_6\), and \(S' \to S \cdot\) in \(I_4\). None of those states also has a dot in front of a terminal, and no state has two completed items. An LR(0) parser may therefore reduce in those states on every terminal without colliding with a shift or with another reduction. The grammar is LR(0). It is consequently SLR(1), LALR(1), LR(1), and unambiguous. B, C, and D are false.

### Q14

Answer: A, B, C

From the collection in Q12, GOTO(\(I_0\), \(X\)) = \(I_1\) contains \(S \to X \cdot X\). GOTO(\(I_0\), \(y\)) = \(I_3\) contains \(X \to y \cdot\). GOTO(\(I_0\), \(x\)) = \(I_2\) contains \(X \to x \cdot X\). GOTO(\(I_0\), \(S\)) = \(I_4\) contains only \(S' \to S \cdot\). The item \(S \to X X \cdot\) is in \(I_6 = \mathrm{GOTO}(I_1, X)\), not in GOTO(\(I_0\), \(S\)). D is false.

### Q15

Answer: 5

The deterministic parse of \(xyxy\), writing state numbers on the stack, is:

| Stack after the move | Move |
| --- | --- |
| \(0\) | start |
| \(0\, x\, 2\) | shift \(x\) |
| \(0\, x\, 2\, y\, 3\) | shift \(y\) |
| \(0\, x\, 2\, X\, 5\) | reduce \(X \to y\) |
| \(0\, X\, 1\) | reduce \(X \to x X\) |
| \(0\, X\, 1\, x\, 2\) | shift \(x\) |
| \(0\, X\, 1\, x\, 2\, y\, 3\) | shift \(y\) |
| \(0\, X\, 1\, x\, 2\, X\, 5\) | reduce \(X \to y\) |
| \(0\, X\, 1\, X\, 6\) | reduce \(X \to x X\) |
| \(0\, S\, 4\) | reduce \(S \to X X\), then accept |

The five reductions are \(X \to y\), \(X \to x X\), \(X \to y\), \(X \to x X\), and \(S \to X X\). There are four shifts, one per input symbol.

### Q16

Answer: A

\(A\) is nullable, FIRST(\(A\)) = \(\{ b \}\), and the terminal \(a\) follows \(A\) in \(S \to A a\), so FOLLOW(\(A\)) = \(\{ a \}\). FIRST(\(S\)) = \(\{ a, b \}\) and FOLLOW(\(S\)) = \(\{ \$ \}\). The production \(A \to b A\) is entered only on \(b\). The production \(A \to \varepsilon\) is entered only on FOLLOW(\(A\)) = \(\{ a \}\). Those lookaheads are disjoint, so there is no conflict. Option B swaps the lookaheads. Option C invents a conflict on \(a\). Option D is wrong because \(\$\) follows \(S\), not \(A\): after \(A\) is reduced, the next input symbol is \(a\), and only after \(S \to A a\) is reduced does \(\$\) follow \(S\).

### Q17

Answer: C

FOLLOW of the start symbol contains \(\$\) by definition, whether or not \(S\) occurs on a right-hand side. Here \(S\) does not occur on a right-hand side, and no other terminal is copied into FOLLOW(\(S\)), so FOLLOW(\(S\)) = \(\{ \$ \}\). The terminal \(a\) follows \(A\), not \(S\). Leaving FOLLOW(\(S\)) empty omits the end marker and makes the accept action, and every \(\varepsilon\)-production that should see \(\$\), impossible to place.

### Q18

Answer: B, D

No production has its own left-hand nonterminal as the first symbol of the right-hand side, so the left recursion is not immediate. It is indirect:

\[
S \Rightarrow A a \Rightarrow B b a \Rightarrow S c b a.
\]

The productions of \(B\) are \(B \to S c\) and \(B \to d\). Their right-hand sides begin with the different grammar symbols \(S\) and \(d\). There is no common terminal prefix to factor, so left factoring does not apply to that pair. The grammar is still not LL(1). The only terminal derivations start with \(d\), because \(B \Rightarrow d\) is the only way to leave the cycle. Thus FIRST(\(S\)) = FIRST(\(A\)) = FIRST(\(B\)) = \(\{ d \}\), and FIRST(\(S c\)) = \(\{ d \}\) meets FIRST(\(d\)) = \(\{ d \}\). The two productions of \(B\) both want lookahead \(d\). The repair this grammar needs is elimination of the indirect left recursion, not left factoring.

### Q19

Answer: A, B, C

\(A\) stands immediately before \(d\) in \(S \to a A d\) and immediately before \(e\) in \(S \to b A e\), so FOLLOW(\(A\)) = \(\{ d, e \}\). The same two terminals follow \(B\): \(d\) from \(S \to b B d\) and \(e\) from \(S \to a B e\). So C is true.

After the parser shifts \(a\) or \(b\), the next symbol is \(c\), and closure of both \(A \to \cdot c\) and \(B \to \cdot c\) puts both productions in one LR(0) state. Shifting \(c\) produces a state whose only items are

\[
A \to c \cdot, \qquad B \to c \cdot.
\]

SLR reduces \(A \to c\) on FOLLOW(\(A\)) and \(B \to c\) on FOLLOW(\(B\)). Both sets are \(\{ d, e \}\), so on \(d\) and on \(e\) the parser has two reductions and no shift. That is a reduce/reduce conflict, and B describes that state.

The four strings \(acd\), \(bcd\), \(ace\), and \(bae\) each have one derivation. For example, \(acd\) can use only \(S \to a A d\) with \(A \to c\); the alternative \(S \to a B e\) ends in \(e\). The grammar is unambiguous, so D is false. Canonical LR(1) separates the two contexts: after \(a\), the item \(A \to c \cdot\) carries lookahead \(d\) and \(B \to c \cdot\) carries lookahead \(e\); after \(b\), the lookaheads are swapped. Those are different LR(1) states, and each lookahead selects one reduction. SLR cannot see that distinction because it uses FOLLOW sets instead of item lookaheads.

### Q20

Answer: 2

The reduce/reduce conflict of Q19 occurs on exactly the two lookaheads \(d\) and \(e\). No other terminal is in FOLLOW(\(A\)) or FOLLOW(\(B\)). The SLR automaton does not have a shift/reduce conflict in that state, because the dot is at the end of both items.

Merging the two LR(1) states that share the core \(\{ A \to c \cdot,\ B \to c \cdot \}\) unions the lookaheads and produces the same reduce/reduce conflict, so the grammar is not LALR(1) either. It is canonical LR(1). The integer asked for is the number of SLR lookaheads that conflict, which is 2.

### Q21

Answer: A

FIRST(\(L\)) = \(\{ @, n \}\) and \(R \to L\), so FIRST(\(R\)) = \(\{ @, n \}\). The two productions of \(S\) both have FIRST set \(\{ @, n \}\). The grammar is not LL(1), and D is false.

In the LR(0) collection, the state reached by reading an \(L\) from the start state contains both

\[
S \to L \cdot \# R \qquad \text{and} \qquad R \to L \cdot.
\]

There is a shift on \(\#\). FOLLOW(\(R\)) also contains \(\#\): \(R \to L\) copies FOLLOW(\(L\)) into FOLLOW(\(R\)), and \(S \to L \# R\) puts \(\#\) in FOLLOW(\(L\)). The completed item \(R \to L \cdot\) is therefore an SLR reduction on \(\#\), in the same state that shifts \(\#\). That is a shift/reduce conflict, so the grammar is not LR(0) and not SLR(1). C is false.

Canonical LR(1) puts the lookahead \(\$\) on the item that came from \(S \to \cdot R\), and it shifts \(\#\) from the item \(S \to L \cdot \# R\). The reduction \(R \to L\) is not offered on \(\#\). The LR(1) automaton has 14 states and no conflicts, so the grammar is LR(1). The same cores give an LALR(1) automaton with 10 states and no conflicts. There is no reduce/reduce conflict in either automaton, so B is false. The language is unambiguous: an \(L\) followed by \(\#\) begins \(S \to L \# R\), and a lone \(L\)-form is \(S \to R\).

### Q22

Answer: A, B, C

LR(0) places a reduction on every terminal. If that already causes no conflict, then restricting the reduction to FOLLOW, which is what SLR(1) does, cannot create a conflict. Every LR(0) grammar is SLR(1). Every SLR(1) grammar is LALR(1), and every LALR(1) grammar is canonical LR(1): each class keeps the grammars of the previous class and adds grammars whose conflicts need sharper lookaheads. The inclusions are proper. Q12 is LR(0). Q21 is LR(1) and LALR(1) but not SLR(1). Q19 is canonical LR(1) but not LALR(1) and not SLR(1).

LL(1) is not a superset of LR(1). The grammar in Q21 is LR(1) and is not LL(1), because FIRST(\(L \# R\)) and FIRST(\(R\)) both equal \(\{ @, n \}\). D is false.
