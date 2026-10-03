# Liveness Analysis — Practice Questions

Original practice for GATE CS. These questions are not from any GATE paper. Attempt the questions before reading the solutions.

A variable is live at a program point when some path from that point uses the variable before any redefinition. For a basic block \(B\),

- \(\mathrm{use}[B]\) is the set of variables used in \(B\) before any definition of that same variable in \(B\),
- \(\mathrm{def}[B]\) is the set of variables defined somewhere in \(B\),
- \(\mathrm{IN}[B] = \mathrm{use}[B] \cup (\mathrm{OUT}[B] - \mathrm{def}[B])\),
- \(\mathrm{OUT}[B]\) is the union of \(\mathrm{IN}[S]\) over the successors \(S\) of \(B\).

No variable is live on the exit edge of the procedure, so \(\mathrm{OUT}\) of a block that goes only to the procedure exit is empty. \(\mathrm{IN}[B]\) is the set live at the entry of \(B\). \(\mathrm{OUT}[B]\) is the set live at the exit of \(B\).

## Level 1 — Conceptual

## Q1 — MCQ

Liveness of variables is

A. a backward analysis: information flows from uses toward earlier definitions
B. a forward analysis: information flows from definitions toward later uses
C. another name for reaching definitions
D. computed by intersecting the live sets of the successors

---

## Q2 — MSQ

Select all that apply.

A. \(\mathrm{IN}[B] = \mathrm{use}[B] \cup (\mathrm{OUT}[B] - \mathrm{def}[B])\).
B. \(\mathrm{OUT}[B]\) is the union of \(\mathrm{IN}\) over the successors of \(B\).
C. If a block defines `x` before it uses `x`, that internal use does not by itself put `x` in \(\mathrm{use}[B]\).
D. The live set on the procedure-exit edge contains every variable of the procedure.

---

## Q3 — NAT

The control-flow graph has edges \(B_1 \to B_2\), \(B_1 \to B_3\), \(B_2 \to B_4\), and \(B_3 \to B_4\). Block \(B_4\) goes to the procedure exit.

```
B1: a = 1
    b = 2
B2: c = a + b
B3: c = a
B4: d = c + b
```

How many variables are live at the exit of \(B_4\)? Enter an integer.

---

## Level 2 — Standard GATE Style

## Q4 — MCQ

Using the graph and the blocks of Q3, the set of variables live at the exit of \(B_2\) is

A. \(\{ a, b \}\)
B. \(\{ b, c \}\)
C. \(\{ c \}\)
D. \(\{ a, b, c \}\)

---

## Q5 — MCQ

Using the graph and the blocks of Q3, the set of variables live at the entry of \(B_3\) is

A. \(\{ a \}\)
B. \(\{ a, b \}\)
C. \(\{ b, c \}\)
D. \(\emptyset\)

---

## Q6 — MCQ

Using the graph and the blocks of Q3, how many variables are live at the exit of \(B_1\)?

A. 0
B. 1
C. 2
D. 3

---

## Level 3 — Multi-Step

## Q7 — MSQ

A second graph has edges \(B_1 \to B_2\), \(B_2 \to B_2\), and \(B_2 \to B_3\). Block \(B_3\) goes to the procedure exit. The name `n` is not defined in these blocks.

```
B1: i = n
    s = 0
B2: s = s + i
    i = i - 1
B3: return s
```

Select all that apply.

A. `n` is live at the entry of \(B_1\).
B. `i` is live at the exit of \(B_1\).
C. `s` is live at the entry of \(B_3\).
D. `i` is live at the exit of \(B_3\).

---

## Q8 — NAT

Using the graph and the blocks of Q7, how many variables are live at the exit of \(B_2\)? Enter an integer.

---

## Level 4 — Tricky / Trap-Based

## Q9 — MCQ

Using the graph and the blocks of Q3, the set of variables live at the entry of \(B_1\) is

A. \(\{ a, b \}\)
B. \(\emptyset\)
C. \(\{ a \}\)
D. \(\{ b \}\)

---

## Q10 — MSQ

Using the graph and the blocks of Q3, which statements hold? Select all that apply.

A. `b` is live at the exit of \(B_2\), even though \(B_2\) does not use `b`.
B. `a` is live at the exit of \(B_2\).
C. `c` is live at the entry of \(B_4\).
D. `d` is live at the exit of \(B_4\).

---

## Level 5 — Challenge

## Q11 — NAT

The four statements are one straight-line block. No variable is live after statement (4).

```
(1) a = b + c
(2) d = a + 1
(3) a = d
(4) e = a
```

How many variables are live immediately after statement (2), before statement (3)? Enter an integer.

---

## Q12 — MCQ

Statement (4) of Q11 is replaced by `e = b`. No variable is live after the new statement (4). Which set is live immediately before statement (1)?

A. \(\{ b, c \}\)
B. \(\{ a, b, c \}\)
C. \(\{ b \}\)
D. \(\{ b, d \}\)

---

## Answer Key

| Q | Type | Answer |
| --- | --- | --- |
| 1 | MCQ | A |
| 2 | MSQ | A, B, C |
| 3 | NAT | 0 |
| 4 | MCQ | B |
| 5 | MCQ | B |
| 6 | MCQ | C |
| 7 | MSQ | A, B, C |
| 8 | NAT | 2 |
| 9 | MCQ | B |
| 10 | MSQ | A, C |
| 11 | NAT | 1 |
| 12 | MCQ | A |

## Detailed Solutions

### Q1

Answer: A

A use creates liveness, and that fact travels backward to every point that can reach the use without passing through a redefinition. The data-flow equations therefore read the successors’ IN sets to build OUT, which is a backward dependence. Reaching definitions travel forward from assignments to later program points. Intersecting successors would keep a variable live only when every successor needs it. Liveness uses union: one future use on any successor is enough.

### Q2

Answer: A, B, C

The displayed equation for IN is the standard one: upward-exposed uses are live on entry, and a variable live on exit stays live on entry unless the block defines it. OUT is a union because liveness is a “may” property along some path. If the block defines `x` and only afterward uses `x`, the use is satisfied by that definition. It is not an upward-exposed use, so it does not belong to \(\mathrm{use}[B]\). The procedure-exit edge carries the empty set in this problem. A variable that is defined and never used again is not live merely because it exists.

### Q3

Answer: 0

\(B_4\)’s only successor is the procedure exit, whose live set is empty. Nothing after `d = c + b` uses `d`, `c`, `b`, or `a`. The exit set has size 0. Liveness at the entry of \(B_4\) is a different point: `c` and `b` are used there, but the question asks for the exit.

### Q4

Answer: B

\(\mathrm{OUT}[B_4] = \emptyset\) and \(\mathrm{use}[B_4] = \{ b, c \}\), with \(\mathrm{def}[B_4] = \{ d \}\). Therefore

\[
\mathrm{IN}[B_4] = \{ b, c \}.
\]

\(B_2\)’s only successor is \(B_4\), so \(\mathrm{OUT}[B_2] = \{ b, c \}\). The variable `a` is used inside \(B_2\), not after it. The variable `c` is live on exit because \(B_4\) uses the `c` that \(B_2\) defined. Dropping `b` would be wrong: \(B_4\) uses `b`, and \(B_2\) does not define `b`.

### Q5

Answer: B

\(\mathrm{OUT}[B_3] = \mathrm{IN}[B_4] = \{ b, c \}\). Inside \(B_3\), `c = a` uses `a` and defines `c`, so \(\mathrm{use}[B_3] = \{ a \}\) and \(\mathrm{def}[B_3] = \{ c \}\).

\[
\mathrm{IN}[B_3] = \{ a \} \cup (\{ b, c \} - \{ c \}) = \{ a, b \}.
\]

The variable `b` is not mentioned in \(B_3\), but it is live on exit and is not defined in the block, so it remains live on entry. The variable `c` is defined before \(B_4\) reads it, so `c` is not live on entry to \(B_3\).

### Q6

Answer: C

From Q4 and Q5, \(\mathrm{IN}[B_2] = \{ a, b \}\) because \(B_2\) uses both and defines only `c`, and \(\mathrm{IN}[B_3] = \{ a, b \}\). The successors of \(B_1\) are \(B_2\) and \(B_3\), so

\[
\mathrm{OUT}[B_1] = \{ a, b \} \cup \{ a, b \} = \{ a, b \}.
\]

The exit of \(B_1\) has two live variables. Both are defined in \(B_1\), which matters for the entry of \(B_1\), not for this exit set.

### Q7

Answer: A, B, C

For \(B_3\), \(\mathrm{use} = \{ s \}\) and \(\mathrm{def} = \emptyset\), and the exit contributes nothing, so \(\mathrm{IN}[B_3] = \{ s \}\). Thus `s` is live at the entry of \(B_3\), and `i` is not live at the exit of \(B_3\).

The printed instructions of \(B_2\) are the only ones that contribute uses and definitions. `s = s + i` uses `s` and `i` before either is defined in the block. `i = i - 1` defines `i` and also uses `i`, but that use comes after the use in `s = s + i`, so `i` is already an upward-exposed use. Thus \(\mathrm{use}[B_2] = \{ s, i \}\) and \(\mathrm{def}[B_2] = \{ s, i \}\). Then

\[
\mathrm{IN}[B_2] = \{ s, i \} \cup (\mathrm{OUT}[B_2] - \{ s, i \}) = \{ s, i \},
\]

whatever OUT is. The successors of \(B_2\) are \(B_2\) and \(B_3\), so \(\mathrm{OUT}[B_2] = \{ s, i \} \cup \{ s \} = \{ s, i \}\). Therefore \(\mathrm{OUT}[B_1] = \mathrm{IN}[B_2] = \{ s, i \}\), and `i` is live at the exit of \(B_1\).

\(B_1\) uses `n` in `i = n` and defines `i` and `s`. 

\[
\mathrm{IN}[B_1] = \{ n \} \cup (\{ s, i \} - \{ s, i \}) = \{ n \}.
\]

So `n` is live at the entry of \(B_1\). D is the exit of the return block, which is empty.

### Q8

Answer: 2

The fixed point computed in Q7 is \(\mathrm{OUT}[B_2] = \{ s, i \}\). Both `s` and `i` are used again on the back edge: the next iteration reads them in `s = s + i` before defining them. The return path needs only `s`, but the union with the back edge also keeps `i`. The set has size 2.

### Q9

Answer: B

Q6 gives \(\mathrm{OUT}[B_1] = \{ a, b \}\). Both variables are defined in \(B_1\), and neither is used before its definition: `a = 1` and `b = 2` have constant right-hand sides. So \(\mathrm{use}[B_1] = \emptyset\) and \(\mathrm{def}[B_1] = \{ a, b \}\).

\[
\mathrm{IN}[B_1] = \emptyset \cup (\{ a, b \} - \{ a, b \}) = \emptyset.
\]

The set live at the exit is not the set live at the entry. A definition before any use kills the variable for the entry, even when later blocks use the new value. Reporting \(\{ a, b \}\) swaps the two ends of the block.

### Q10

Answer: A, C

From Q4, \(\mathrm{OUT}[B_2] = \{ b, c \}\). The instruction `c = a + b` uses `a` and defines `c`; it does not leave `a` live, and it does not use `b` after the block. The reason `b` is live at the exit is the use `d = c + b` in \(B_4\). A use in a successor is enough. That is A, and it is why B is false.

\(\mathrm{IN}[B_4] = \{ b, c \}\), so `c` is live at the entry of \(B_4\). At the exit of \(B_4\) the live set is empty: `d` is defined and never used. D confuses a definition with a later use.

### Q11

Answer: 1

Move backward from the empty set after statement (4).

- Statement (4), `e = a`, uses `a` and defines `e`. Immediately before (4), `a` is live and `e` is not.
- Statement (3), `a = d`, defines `a` before that use, and it uses `d`. The incoming `a` is killed. Immediately before (3), which is immediately after (2), the live set is \(\{ d \}\).
- Statement (2) uses `a`, but that point is before the point the question asks about.

No other variable is used between statement (2) and a definition. In particular `a` is dead after (2) because (3) redefines `a` before (4) reads it. The earlier uses of `b` and `c` are already behind this point. Exactly one variable, `d`, is live.

### Q12

Answer: A

The new statement (4) is `e = b`. Walk backward from the empty set after (4).

- Before (4): \(\{ b \}\), because `e = b` uses `b`.
- Statement (3) defines `a` and uses `d`. It does not define `b`, so before (3) the live set is \(\{ b, d \}\).
- Statement (2) defines `d` and uses `a`. It kills `d` and adds `a`, so before (2) the live set is \(\{ a, b \}\).
- Statement (1) defines `a` and uses `b` and `c`. It kills `a` and adds `c`. Before (1) the live set is \(\{ b, c \}\).

The variable `a` is not live on entry: its first occurrence is a definition. The variable `d` is defined in (2) before it is used in (3). The variable `b` is live on entry both because (1) uses it and because (4) uses it with no intervening definition. The variable `c` is live on entry because (1) uses it. The set is \(\{ b, c \}\).
