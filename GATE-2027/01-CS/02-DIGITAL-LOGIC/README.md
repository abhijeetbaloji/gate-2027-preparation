# Digital Logic (GATE CS)

Study material for Section 2 of the official GATE 2027 CS syllabus:

Boolean algebra and minimization (algebraic technique, Karnaugh map, tabular method). Design of combinational and sequential circuits. Number representation and arithmetic (fixed and floating point).

Syllabus source: `../../00-GATE-2027/official-syllabus/CS/syllabus.md`.

## How to use this section

| File | Purpose | When to use |
|------|---------|-------------|
| `NOTES.md` | Learn the topic: definitions, why the rule holds, worked steps | First study |
| `REVISION.md` | Short sheet | After the notes, and again before a test |
| `FORMULAS.md` | Rules with the condition that makes them true | Lookup while solving |
| `SHORTCUTS.md` | Checks that are valid only in a stated situation | Timed practice, after you know why they hold |
| `PYQ.md` | What the mapped papers actually asked | After the notes. Solve from the original paper |
| `PRACTICE.md` | Original questions, five levels, with solutions | Beside the past papers. These are not past-paper questions |
| `MISTAKES.md` | Common traps, plus an empty log | After every practice session |

`REVISION.md` is not a substitute for `NOTES.md`.

A second set of original questions already lives in `../14-PRACTICE-QUESTIONS/TOPIC-WISE/02-DIGITAL-LOGIC/`. The `PRACTICE.md` files here are a further set, written from the same patterns, not a copy of that folder and not a copy of the PYQs.

## Folders

The names below are the syllabus lines, in the order already created.

| Folder | Syllabus line |
|--------|----------------|
| `01-BOOLEAN-ALGEBRA-AND-MINIMIZATION/01-ALGEBRAIC-TECHNIQUE/` | Algebraic technique |
| `01-BOOLEAN-ALGEBRA-AND-MINIMIZATION/02-KARNAUGH-MAP/` | Karnaugh map |
| `01-BOOLEAN-ALGEBRA-AND-MINIMIZATION/03-TABULAR-METHOD/` | Tabular method |
| `02-DESIGN-OF-COMBINATIONAL-AND-SEQUENTIAL-CIRCUITS/01-COMBINATIONAL-CIRCUITS/` | Combinational circuits |
| `02-DESIGN-OF-COMBINATIONAL-AND-SEQUENTIAL-CIRCUITS/02-SEQUENTIAL-CIRCUITS/` | Sequential circuits |
| `03-NUMBER-REPRESENTATION-AND-ARITHMETIC/01-FIXED-POINT/` | Fixed-point representation and arithmetic |
| `03-NUMBER-REPRESENTATION-AND-ARITHMETIC/02-FLOATING-POINT/` | Floating-point representation and arithmetic |

## Order

The dependency order is the 100-day plan’s order (days 22–27 in `../00-100-DAY-PLAN/`):

1. Algebraic technique. Identities, minterms, XOR, De Morgan, self-dual functions.
2. Karnaugh map. The same minimization, by grouping. Do this before trusting a long algebraic simplification.
3. Tabular method. Prime-implicant counts when a picture is unreliable.
4. Combinational circuits. Adders, muxes, decoders, encoders. They are Boolean functions in a package.
5. Sequential circuits. Flip-flops and counters. The next-state logic is the combinational topic.
6. Fixed point. Two’s complement, overflow, Booth. The adder’s carry-out is not signed overflow; that distinction needs both topics.
7. Floating point. IEEE-754 single precision. The fraction is a fixed-point field with an exponent beside it.

## How PYQs and practice fit together

Past papers for 2007–2026 are in `../12-PYQ/`. Topic extracts are in `../13-PYQ-TOPIC-MAPPING/02-DIGITAL-LOGIC/`. Each topic `PYQ.md` points at that folder.

The mapping is usable and uneven:

- Many stems are real Digital Logic questions. The notes are built from those patterns: minimal SOP, essential primes, mux and decoder trees, flip-flop traces, Johnson and saturating counters, two’s-complement overflow, Booth transition counts, IEEE-754 hex.
- Some stored blocks are parsers, caches, pipelines, databases, or similar. Each `PYQ.md` lists those separately. They are not counted as evidence for this subject.
- Year headings inside several `questions.md` files disagree with the `Paper` line. The topic `PYQ.md` files follow `Paper`.
- Every stored answer field seen for this subject is `VERIFICATION REQUIRED`. These notes do not invent official keys. Work the paper.

`TOPIC-PRIORITY.md` and `PYQ-COVERAGE.md` record the counts under that rule. `FORMULA-INDEX.md` links every formula sheet.

## Suggested study flow

1. Read `NOTES.md` and work the examples, including the reason for each identity.
2. Check `FORMULAS.md` and `SHORTCUTS.md`.
3. Solve this folder’s `PRACTICE.md` from Level 1 through Level 5.
4. Solve the matching file under `14-PRACTICE-QUESTIONS`.
5. Solve the recognizable rows in `PYQ.md` from the linked paper. Log misses in `MISTAKES.md`.
6. Revise from `REVISION.md`.
