# Runtime Environments — Practice Questions

Original practice for GATE CS. These questions are not from any GATE paper. Attempt the questions before reading the solutions.

## Level 1 — Conceptual

## Q1 — MCQ

A language allows recursive procedures. Where are the activation records of those calls allocated?

A. In the code segment, one record per procedure name
B. On a control stack, one record per live call
C. Only in the symbol table
D. In a single static slot that every call of that procedure reuses

---

## Q2 — MSQ

Which of the following can be fields of a procedure activation record? Select all that apply.

A. The return address
B. A control link to the caller’s activation record
C. An access link to the activation of the textually enclosing procedure
D. The machine code of the callee

---

## Q3 — MCQ

Under call-by-value, what does the callee receive?

A. A copy of the argument; assigning to the formal does not change the caller’s variable
B. The address of the caller’s variable, so every assignment to the formal updates that variable
C. A thunk that re-evaluates the argument expression on every use
D. The caller’s name for the argument, resolved with dynamic scope

---

## Level 2 — Standard GATE Style

## Q4 — NAT

The parameter is passed by value. What is the value of \(a\) after the call returns? Enter an integer.

```
int a = 2;
void f(int x) { x = x + a; a = a + x; }
f(a);
```

---

## Q5 — MCQ

The same procedure as in Q4 is used, but \(x\) is passed by reference. What is \(a\) after `f(a)` returns?

A. 2
B. 4
C. 6
D. 8

---

## Q6 — MSQ

The program is

```
int x = 1;
void p() { print(x); }
void q() { int x = 2; p(); }
q();
```

`p` and `q` are nested directly in the scope that declares the outer `x`. Select all that apply.

A. Under static scoping the printed value is 1.
B. Under dynamic scoping the printed value is 2.
C. Under static scoping the printed value is 2.
D. An access link is the usual way to find a statically enclosing activation.

---

## Level 3 — Multi-Step

## Q7 — MCQ

The stack grows toward lower addresses. The frame pointer FP addresses the dynamic link. Moving toward lower addresses, the record then holds an access link (4 bytes), local `x` (4 bytes), and local `y` (4 bytes).

How many bytes below FP does local `y` begin?

A. 4
B. 8
C. 12
D. 16

---

## Q8 — MSQ

Procedures `A` and `C` are nested directly in `main`. Procedure `B` is nested directly in `A`. The live call chain, from oldest to newest, is

\[
\mathrm{main} \to A \to C \to B.
\]

`B` is executing. Select all that apply.

A. The stack holds one activation of `A` and one activation of `B`.
B. The dynamic link of `B` points to the activation of `C`.
C. The access link of `B` points to the activation of `C`.
D. The access link of `B` points to the activation of `A`.

---

## Level 4 — Tricky / Trap-Based

## Q9 — MCQ

Call-by-copy-restore copies the actual into the formal when the call begins, and copies the formal back into the actual when the call returns. Starting from `a = 5`, what is `a` after the call?

```
void f(int x) { a = 10; x = x + 1; }
f(a);
```

A. 5
B. 6
C. 10
D. 11

---

## Q10 — MSQ

Select all that apply.

A. Call-by-name re-evaluates the argument expression at each use of the formal.
B. Call-by-value evaluates the argument once, before the body runs.
C. Under call-by-reference the formal is an alias of the actual variable.
D. Call-by-name and call-by-value produce the same result for every procedure.

---

## Level 5 — Challenge

## Q11 — NAT

Both calls pass `x` by value. What is `a` when `main` finishes? Enter an integer.

```
int a = 4;
void f(int x) { x = x + 1; a = a + x; }
void main() { f(a); f(a); }
```

---

## Q12 — MCQ

Use the nesting and the call chain of Q8. A variable of `main` is not local to `B` or to `A`. How many access-link hops from the active `B` reach the activation of `main`?

A. 1
B. 2
C. 3
D. 4

---

## Answer Key

| Q | Type | Answer |
| --- | --- | --- |
| 1 | MCQ | B |
| 2 | MSQ | A, B, C |
| 3 | MCQ | A |
| 4 | NAT | 6 |
| 5 | MCQ | D |
| 6 | MSQ | A, B, D |
| 7 | MCQ | C |
| 8 | MSQ | A, B, D |
| 9 | MCQ | B |
| 10 | MSQ | A, B, C |
| 11 | NAT | 19 |
| 12 | MCQ | B |

## Detailed Solutions

### Q1

Answer: B

Recursion can have several live calls of one procedure, each with its own locals, parameters, and return address. Those activation records are pushed on the control stack and popped on return. A single static slot cannot hold two recursive activations. The code segment stores the instructions, which do not change per call. The symbol table stores declaration-time information, not the live frame.

### Q2

Answer: A, B, C

The return address says where the call resumes. The control link, also called the dynamic link, points at the caller’s frame so the stack can be popped. The access link, also called the static link, points at the current activation of the textually enclosing procedure so a nested procedure can read non-local variables. The callee’s machine code lives in the code segment and is shared by every activation. It is not stored in the frame.

### Q3

Answer: A

Call-by-value evaluates the actual once and copies the result into the formal. Later assignments to the formal change that copy. Passing the address is call-by-reference. Re-evaluating the expression on every use is call-by-name. Dynamic scope is a rule for free variables, not a parameter-passing mode.

### Q4

Answer: 6

The actual `a` is 2, so the formal `x` starts as a copy of 2. The assignment `x = x + a` uses the global `a`, which is still 2, and writes the local: \(x = 2 + 2 = 4\). The assignment `a = a + x` writes the global: \(a = 2 + 4 = 6\). When `f` returns, the local `x` is discarded and is not copied back. The global `a` remains 6.

### Q5

Answer: D

Reference makes `x` an alias of `a`. The first assignment `x = x + a` is `a = a + a`, so `a` becomes \(2 + 2 = 4\). The second assignment `a = a + x` reads that same location twice: \(a = 4 + 4 = 8\). The call-by-value result 6 is not the reference result, because the first assignment already changed the caller’s variable.

### Q6

Answer: A, B, D

Static scope binds the free `x` in `p` to the `x` declared in the textually enclosing scope, which is the outer `x` with value 1. The local `x` in `q` is a different variable, even though `q` called `p`. Dynamic scope binds the free `x` to the nearest declaration on the call chain. That declaration is `q`’s `x`, with value 2. An access link implements the static nesting used by A: from `p` it points at the outer frame, not at `q`. C swaps the static answer.

### Q7

Answer: C

From FP toward lower addresses the layout is:

| Address | Field | Size |
| --- | --- | --- |
| FP | dynamic link | |
| FP − 4 | access link | 4 bytes |
| FP − 8 | local `x` | 4 bytes |
| FP − 12 | local `y` | 4 bytes |

Local `y` begins 4 + 4 + 4 = 12 bytes below FP. The return address, which this question places above FP, does not affect the distance down to `y`.

### Q8

Answer: A, B, D

The stack, from oldest to newest, is `main`, `A`, `C`, `B`. There is one frame for `A` and one frame for `B`, so A is true. The dynamic link records the caller. `C` called `B`, so B’s dynamic link points at `C`. The access link records textual nesting, not the caller. `B` is declared inside `A`, so B’s access link points at `A` even though `C` performed the call. It does not point at `C`.

### Q9

Answer: B

Copy-restore is not reference and not plain value. At the call, `x` receives a copy of 5. The body then sets the global `a` to 10 and sets the local `x` to \(5 + 1 = 6\). On return the formal is written back into the actual, so `a` becomes 6. The assignment `a = 10` is overwritten by that write-back. Call-by-reference would alias `x` with `a`, giving `a = 10` and then `a = 11`. Call-by-value would leave `a` at 10, because the local `x = 6` would not be copied back. The copy-restore result is 6.

### Q10

Answer: A, B, C

Call-by-name passes a thunk: each use of the formal evaluates the actual expression in the caller’s environment. Call-by-value evaluates once and copies. Call-by-reference passes an address, so the formal and the actual name the same location. D is false. A classic difference is an argument with a side effect, or a formal that is used more than once: call-by-name repeats the effect, and call-by-value does not. The program in Q9 is a related witness that value and copy-restore already disagree; name and value disagree as well whenever a use of the formal must see a later change to a variable mentioned in the actual.

### Q11

Answer: 19

Both calls use value, so each formal starts as a copy of the current global `a` and is not written back.

- First call: `x` starts at 4, then `x = 5`, then `a = 4 + 5 = 9`.
- Second call: `x` starts at 9, then `x = 10`, then `a = 9 + 10 = 19`.

The second call sees the global updated by the first call. It does not see the first call’s local `x`.

### Q12

Answer: B

Access links follow textual parents. `B` is nested in `A`, and `A` is nested in `main`, so the chain is

\[
B \xrightarrow{\text{access}} A \xrightarrow{\text{access}} \mathrm{main}.
\]

That is two hops. The dynamic call chain `main → A → C → B` has three caller links, but the question asks for access links. `C` is not on B’s static chain: `C` called `B`, yet `B`’s parent is `A`. Counting the call chain instead of the nesting chain produces the trap answer 3.
