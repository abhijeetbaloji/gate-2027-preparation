# Transactions and Concurrency Control — Practice Questions

Original practice for GATE CS. These questions are not from any GATE paper. Attempt the questions before reading the solutions.

In a schedule, rᵢ(X) is a read of item X by transaction Tᵢ, wᵢ(X) is a write, cᵢ is a commit, and aᵢ is an abort. Two operations conflict when they belong to different transactions, they use the same item, and at least one of them is a write. The precedence graph has an edge Tᵢ → Tⱼ when an operation of Tᵢ precedes and conflicts with an operation of Tⱼ. A schedule is conflict serializable when that graph is acyclic. xlᵢ and ulᵢ are exclusive lock and unlock by Tᵢ.

## Level 1 — Conceptual

## Q1 — MCQ

Which pair of operations conflicts?

A. r₁(A) and r₂(A)
B. r₁(A) and w₂(B)
C. w₁(A) and w₂(A)
D. r₁(A) and w₁(A)

---

## Q2 — MCQ

A schedule is conflict serializable if and only if

A. its precedence graph has no cycle
B. every pair of operations conflicts
C. every transaction commits
D. it contains no blind write

---

## Q3 — MSQ

Which statements match the ACID properties? Select all that apply.

A. Atomicity: either all of a transaction's updates are installed, or none are
B. Isolation: the effect of concurrent committed transactions matches some serial execution of those transactions
C. Durability: an update that has not been committed must survive a crash
D. Consistency: a transaction run by itself preserves the database's integrity constraints

---

## Q4 — MSQ

The operations occur in this order: r₁(A), r₂(A), w₁(A), w₂(B), w₁(B). Which pairs conflict? Select all that apply.

A. r₁(A) and r₂(A)
B. r₂(A) and w₁(A)
C. w₂(B) and w₁(B)
D. w₁(A) and w₂(B)

---

## Q5 — MCQ

Which statement is true of basic two-phase locking?

A. A transaction may acquire a new lock after it has released a lock
B. Every schedule allowed by basic two-phase locking has an acyclic precedence graph
C. Basic two-phase locking cannot deadlock
D. Every exclusive lock must be held until the transaction commits

---

## Level 2 — Standard GATE Style

## Q6 — MCQ

Consider S: r₁(X), r₂(Y), w₁(Y), w₂(X).

A. S is conflict serializable in the order T₁ then T₂
B. S is conflict serializable in the order T₂ then T₁
C. S is not conflict serializable
D. S has no conflicting pair

---

## Q7 — MCQ

Consider S: r₁(A), w₁(A), r₂(A), w₂(B), r₃(B), w₃(C).

A. S is not conflict serializable
B. S is conflict serializable only in the order T₁, T₂, T₃
C. S is conflict serializable only in the order T₃, T₂, T₁
D. S is conflict serializable in both T₁, T₂, T₃ and T₃, T₂, T₁

---

## Q8 — NAT

How many edges are in the precedence graph of the schedule in Q7? ______

---

## Q9 — MCQ

A schedule is recoverable when

A. whenever Tᵢ reads a value written by Tⱼ, Tⱼ commits before Tᵢ commits
B. whenever Tᵢ reads a value written by Tⱼ, Tⱼ commits before that read
C. every transaction in the schedule commits
D. the precedence graph is acyclic

---

## Q10 — MSQ

Which statements are true? Select all that apply.

A. Under basic two-phase locking, a transaction may release a lock before it commits
B. Under strict two-phase locking, every exclusive lock is held until commit or abort
C. Strict two-phase locking prevents deadlock
D. Every schedule allowed by strict two-phase locking is cascadeless

---

## Q11 — NAT

Consider w₁(X), r₂(X), r₃(X), a₁. T₂ and T₃ have not committed. How many transactions other than T₁ must be rolled back because they read X from T₁? ______

---

## Level 3 — Multi-Step

## Q12 — MCQ

Consider S: w₁(X), r₂(X), c₂, c₁.

A. S is recoverable and cascadeless
B. S is recoverable but not cascadeless
C. S is not recoverable, and S is conflict serializable
D. S is not conflict serializable

---

## Q13 — MCQ

Consider S: w₁(X), r₂(X), w₂(Y), c₁, c₂.

A. S is not recoverable
B. S is recoverable but not cascadeless
C. S is cascadeless but not recoverable
D. S is strict

---

## Q14 — MCQ

Consider S: w₁(X), w₂(X), c₂, c₁. There is no read.

A. S is not recoverable
B. S is recoverable but not cascadeless
C. S is cascadeless but not strict
D. S is strict

---

## Q15 — MSQ

Consider S: r₁(X), w₂(X), w₁(X), w₃(X). Which statements are true? Select all that apply.

A. S is conflict serializable
B. S is view serializable
C. The final write of X is by T₃
D. T₁ reads the value written by T₂

---

## Q16 — NAT

Consider S: r₁(A), w₁(E), w₂(A), r₃(E), w₂(B), w₃(C), r₄(B), r₄(C). How many distinct serial orders are consistent with the precedence graph of S? ______

---

## Level 4 — Tricky / Trap-Based

## Q17 — MCQ

Again consider S: r₁(X), w₂(X), w₁(X), w₃(X).

A. S is both conflict serializable and view serializable
B. S is view serializable and not conflict serializable
C. S is conflict serializable and not view serializable
D. S is neither conflict serializable nor view serializable

---

## Q18 — MCQ

Consider S: w₁(X), r₂(X), c₁, c₂.

A. S is neither recoverable nor cascadeless
B. S is recoverable but not cascadeless
C. S is cascadeless but not recoverable
D. S is both recoverable and cascadeless

---

## Q19 — MSQ

A lock manager produces this schedule. Every lock is exclusive.

xl₁(Q), w₁(Q), ul₁(Q), xl₂(Q), w₂(Q), ul₂(Q), c₂, c₁

Which statements are true? Select all that apply.

A. The schedule is allowed by basic two-phase locking
B. The schedule is allowed by strict two-phase locking
C. The schedule is conflict serializable
D. The schedule is strict: it contains no write of an uncommitted value

---

## Level 5 — Challenge

## Q20 — NAT

Consider S: r₁(A), w₂(A), r₂(B), w₃(B), r₃(C), w₁(C). How many edges are in the precedence graph of S? ______

---

## Q21 — NAT

Consider w₁(X), r₂(X), w₂(Y), r₃(Y), a₁. No transaction has committed before the abort. Cascading rollback is used. How many transactions roll back, counting T₁? ______

---

## Q22 — MSQ

A counter starts at 40. Two clerks run the transaction "read the counter, subtract 1, write the counter". Both read 40 before either writes. Both write 39. Two sales occurred, and the stored counter is 39. A serial execution of the two sales would have stored 38. Which statements are true? Select all that apply.

A. The interleaved outcome is not the outcome of either serial order
B. Isolation does not hold; this is a lost update
C. Durability does not hold, because the value 39 was written
D. Atomicity does not hold, because each clerk wrote only part of a subtraction

---

## Answer Key

| Q | Type | Answer |
|---|------|--------|
| 1 | MCQ | C |
| 2 | MCQ | A |
| 3 | MSQ | A, B, D |
| 4 | MSQ | B, C |
| 5 | MCQ | B |
| 6 | MCQ | C |
| 7 | MCQ | B |
| 8 | NAT | 2 |
| 9 | MCQ | A |
| 10 | MSQ | A, B, D |
| 11 | NAT | 2 |
| 12 | MCQ | C |
| 13 | MCQ | B |
| 14 | MCQ | C |
| 15 | MSQ | B, C |
| 16 | NAT | 2 |
| 17 | MCQ | B |
| 18 | MCQ | B |
| 19 | MSQ | A, C |
| 20 | NAT | 3 |
| 21 | NAT | 3 |
| 22 | MSQ | A, B |

## Detailed Solutions

### Q1

Answer: C

The two writes name different transactions and the same item, so they conflict. The edge in a schedule would run from whichever write happens first to the other.

A is a pair of reads. Reads do not conflict, and two readers may be ordered either way in a conflict-equivalent serial schedule. B uses different items, so the operations commute. D is one transaction; conflict is defined between different transactions. A transaction's own read and write are ordered by its program, not by the precedence graph.

### Q2

Answer: A

Conflict serializability is exactly acyclicity of the precedence graph. A topological order of that graph is a conflict-equivalent serial order.

B would make almost every schedule fail and is not the definition. C is about completion, not about conflicts; an uncommitted schedule can still have an acyclic graph. D is false because a blind write can participate in a conflict, and it can also be the reason a schedule is view serializable without being conflict serializable, as in Q17. Absence of blind writes is not the test.

### Q3

Answer: A, B, D

Atomicity is all-or-nothing installation of a transaction's updates. Isolation asks that concurrency be indistinguishable from some serial order of the committed transactions. Consistency, as a transaction property, says that a correct transaction run alone takes a consistent database to a consistent database.

C reverses durability. Durability says that a committed update survives a crash. An uncommitted update must not be treated as durable; if the transaction aborts or the system crashes before commit, that update is undone.

### Q4

Answer: B, C

r₂(A) and w₁(A) are different transactions, the same item, and one write. They conflict, with the earlier read before the later write. w₂(B) and w₁(B) are two writes of B, so they conflict as well. In this schedule the edge would be T₂ → T₁ on B, because w₂(B) is written first.

A is two reads of A. D uses A in one operation and B in the other. Different items do not conflict, even though both operations are writes.

### Q5

Answer: B

Basic two-phase locking has a growing phase of lock acquisitions followed by a shrinking phase of releases. A transaction does not acquire a lock after its first release. Schedules that obey this protocol are conflict serializable, so the precedence graph is acyclic.

A is the opposite of the two-phase rule. C is false: two transactions can each hold a lock the other needs, and the protocol does not by itself prevent that deadlock. D is strict two-phase locking, which keeps exclusive locks until commit or abort. Basic two-phase locking may release an exclusive lock earlier, during the shrinking phase.

### Q6

Answer: C

On Y, r₂(Y) precedes w₁(Y), so the graph has T₂ → T₁. On X, r₁(X) precedes w₂(X), so the graph has T₁ → T₂. The two edges form a cycle. S is not conflict serializable, in either serial order.

A and B each ignore one of the two edges. D is false because both cross pairs contain a write. The reads do not conflict with each other, since they touch different items, but each read conflicts with the other transaction's write.

### Q7

Answer: B

Conflicting pairs:

- w₁(A) precedes r₂(A), so T₁ → T₂
- w₂(B) precedes r₃(B), so T₂ → T₃

No operation follows w₃(C), and the earlier operations on A and B do not add another edge. The graph is the chain T₁ → T₂ → T₃. It is acyclic, and the only topological order is T₁, T₂, T₃.

A would be right if any edge ran backward. C is the reverse chain, which contradicts both edges. D would require T₂ and T₃ to be unordered, but w₂(B) before r₃(B) orders them.

### Q8

Answer: 2

The edges are only T₁ → T₂ on A and T₂ → T₃ on B. Writes and reads of different items do not create edges, and w₃(C) conflicts with nothing later in the schedule. Counting a read-read edge, or an edge into T₃ from T₁, overcounts.

### Q9

Answer: A

Recoverability constrains commit order. If Tᵢ used a value produced by Tⱼ, then Tᵢ must not commit until Tⱼ has committed. Otherwise Tⱼ could abort after Tᵢ had already committed, and the read could not be undone.

B is the stronger cascadeless condition: the writer commits before the read, so the read is not dirty and an abort cannot cascade. C is not required for the definition; a schedule can be recoverable and still contain an active transaction, as long as the commit-order rule is respected by those who do commit. D is conflict serializability. Q12 is conflict serializable and not recoverable, so the two properties are independent.

### Q10

Answer: A, B, D

Basic two-phase locking allows the shrinking phase to begin before commit, so a lock, including a shared lock, can be released early. A holds. Strict two-phase locking keeps every exclusive lock until commit or abort, which prevents another transaction from reading or overwriting a dirty value. B holds. A schedule with no dirty read is cascadeless, so D holds.

C is false. Strict two-phase locking still waits for locks. Two transactions can deadlock by acquiring exclusive locks in opposite orders. The protocol does not include a deadlock-prevention rule such as wait-die.

### Q11

Answer: 2

Both r₂(X) and r₃(X) read the value written by T₁, and T₁ then aborts. That value is dirty. Cascading rollback must undo T₂ and T₃ as well. The question excludes T₁, so the count is 2. If either reader had read X only after c₁, it would not be part of the cascade. Neither read is in that position.

### Q12

Answer: C

The only conflict is w₁(X) before r₂(X), which is the edge T₁ → T₂. The graph is acyclic, so S is conflict serializable in the order T₁ then T₂.

T₂ read X from T₁ and committed at c₂ before c₁. If T₁ later aborted, T₂'s committed read could not be undone. S is not recoverable. It is also not cascadeless, because the read happened before c₁. A and B claim recoverability that the commit order destroys. D claims a cycle that is not in the graph. Conflict serializability does not imply recoverability.

### Q13

Answer: B

T₂ reads X from T₁ before c₁, so the read is dirty. S is not cascadeless and not strict. T₁ does commit at c₁ before T₂ commits at c₂, so the recoverability rule is satisfied. There is no other read-from pair. w₂(Y) writes a new item and nobody reads Y.

A ignores c₁ before c₂. C is impossible for any schedule: a cascadeless schedule has no dirty read, so the recoverability obligation is vacuously satisfied or is satisfied even earlier. This schedule is not cascadeless anyway. D requires that nobody read or overwrite T₁'s X before c₁. The read r₂(X) already violates that.

### Q14

Answer: C

Nobody reads X. Cascadelessness only forbids reading an uncommitted write, so it holds. Recoverability also only constrains readers of another transaction's write. With no such reader, c₂ before c₁ does not by itself make the schedule unrecoverable.

Strictness forbids a write of an item that still holds another transaction's uncommitted write. w₂(X) overwrites w₁(X) before c₁, so S is not strict. A dirty write is allowed in a cascadeless schedule and forbidden in a strict one.

A applies the commit-order test without a read-from edge. B would be right for Q13, where there is a dirty read. D ignores the overwrite.

### Q15

Answer: B, C

Conflicts on X:

- r₁(X) before w₂(X) gives T₁ → T₂
- w₂(X) before w₁(X) gives T₂ → T₁
- w₁(X) before w₃(X) gives T₁ → T₃
- w₂(X) before w₃(X) gives T₂ → T₃

The cycle T₁ → T₂ → T₁ means S is not conflict serializable. A is false.

View equivalence uses three checks. The only read is r₁(X), and it precedes every write, so T₁ reads the initial value of X. In the serial order T₁, T₂, T₃, T₁ is first and also reads the initial value. No transaction reads a value written by T₂ or by T₁. The last write of X in S is w₃(X), and T₃ is also last in that serial order, so the final write agrees. S is view equivalent to T₁, T₂, T₃ and is view serializable. B and C are true.

D is false because r₁(X) occurs before w₂(X). T₁ never reads T₂'s write. The writes of T₂ and T₁ are blind: nobody reads them. That is why view equivalence can ignore the T₁/T₂ cycle that conflict serializability cannot ignore.

### Q16

Answer: 2

Conflicts and edges:

- r₁(A) before w₂(A) gives T₁ → T₂
- w₁(E) before r₃(E) gives T₁ → T₃
- w₂(B) before r₄(B) gives T₂ → T₄
- w₃(C) before r₄(C) gives T₃ → T₄

There is no edge between T₂ and T₃. T₁ must be first and T₄ must be last. The two legal orders are T₁, T₂, T₃, T₄ and T₁, T₃, T₂, T₄. The count is 2. Any order with T₄ earlier, or with T₂ or T₃ before T₁, contradicts an edge.

### Q17

Answer: B

The precedence graph has the cycle T₁ → T₂ → T₁ shown in Q15, so S is not conflict serializable. The same solution shows that S is view equivalent to the serial order T₁, T₂, T₃, because T₁ reads the initial value, no other read needs a writer, and T₃ performs the final write. S is view serializable and not conflict serializable.

A misses the cycle. C is impossible: every conflict serializable schedule is view serializable, because agreeing on the order of every conflicting pair is a stronger condition than agreeing on initial reads, read-from pairs, and final writes. This schedule is not an example of C anyway. D misses the serial order that matches the view.

### Q18

Answer: B

r₂(X) reads T₁'s write before c₁, so the read is dirty and S is not cascadeless. c₁ occurs before c₂, so T₁ commits before the reader commits and S is recoverable.

A would be the classification of Q12, where c₂ comes first. C names a combination that cannot occur. Cascadeless schedules are recoverable, because a writer that commits before the read has certainly committed before the reader's commit. This schedule is not cascadeless in any case. D would require the read to follow c₁. Moving r₂(X) to after c₁ would make that option true; the schedule as written does not.

### Q19

Answer: A, C

T₁ acquires its only lock, uses it, and releases it, with no later acquisition. T₂ does the same. Both transactions are two-phase, so basic two-phase locking allows the schedule. The only conflict is w₁(Q) before w₂(Q), giving T₁ → T₂. The graph is acyclic and the only serial order is T₁ then T₂. A and C hold.

B fails because both exclusive locks are released before the owning transaction commits. Strict two-phase locking would keep xl₁(Q) until c₁, and T₂ could not lock Q in between. D fails because w₂(Q) overwrites a value written by T₁ while T₁ is still uncommitted. The schedule contains a dirty write, so it is not strict, which is consistent with the early unlock.

### Q20

Answer: 3

The conflicting pairs are:

- r₁(A) before w₂(A), edge T₁ → T₂
- r₂(B) before w₃(B), edge T₂ → T₃
- r₃(C) before w₁(C), edge T₃ → T₁

Those are three edges, and they form a cycle. The schedule is not conflict serializable. It is also not view serializable: T₁ must precede T₂ to read the initial value of A, T₂ must precede T₃ to read the initial value of B, and T₃ must precede T₁ to read the initial value of C. No serial order satisfies all three. The question asks only for the edge count, which is 3. Missing the wrap-around edge on C produces 2 and hides the cycle.

### Q21

Answer: 3

T₁ aborts after writing X. T₂ has read that uncommitted X, so T₂ rolls back. T₃ has read Y, which T₂ wrote after reading the bad X, so T₃ rolls back as well. Counting T₁, T₂, and T₃ gives 3.

Stopping at T₂ forgets that a transaction which read a value from a transaction that is itself rolling back must also roll back. The schedule would have been cascadeless only if r₂(X) had waited for c₁, in which case an abort of T₁ would not have involved T₂ or T₃.

### Q22

Answer: A, B

Run alone, each sale changes 40 to 39 and is a consistent single-seat sale. Run serially, the second sale reads 39 and writes 38. The interleaving loses one subtraction: both clerks write 39, and one sale disappears. The result matches neither serial order. That is a lost update, and isolation does not hold. A and B are true.

C is false. Durability is about a committed value surviving a crash. The anomaly is that the committed value is the wrong one, not that a committed value was lost in a failure. D is false. Each clerk's transaction performed its whole read-subtract-write. Nothing was left half installed inside one transaction. The missing seat is the effect of interleaving two complete transactions, which is an isolation failure rather than an atomicity failure.
