# Theory of Computation (GATE CS)

Study material for Section 6 of the official GATE 2027 CS syllabus:

Regular expressions and finite automata. Context-free grammars and push-down automata. Regular and context-free languages, pumping lemma. Turing machines and undecidability.

Syllabus source: `../../00-GATE-2027/official-syllabus/CS/syllabus.md`.

## How to use this section

| File | Purpose | When to use |
|------|---------|-------------|
| `NOTES.md` | Learn the topic: definitions, why the rule holds, worked constructions | First study |
| `REVISION.md` | Short sheet | After the notes, and again before a test |
| `FORMULAS.md` | Equivalences, closure tables, construction rules, theorem conditions | Lookup while solving |
| `SHORTCUTS.md` | Checks that are valid only in a stated situation | Timed practice, after you know why they hold |
| `PYQ.md` | What the mapped papers actually asked | After the notes. Solve from the original paper |
| `PRACTICE.md` | Original questions, five levels, with solutions | Beside the past papers. These are not past-paper questions |
| `MISTAKES.md` | Common traps, plus an empty log | After every practice session |

`REVISION.md` is not a substitute for `NOTES.md`.

A second set of original questions already lives in `../14-PRACTICE-QUESTIONS/TOPIC-WISE/06-THEORY-OF-COMPUTATION/`. The `PRACTICE.md` files here are a further set, written from the same patterns, not a copy of that folder and not a copy of the PYQs.

## Folders

The names below are the syllabus lines, in the order already created.

| Folder | Syllabus fragment |
|--------|-------------------|
| `01-REGULAR-EXPRESSIONS/` | Regular expressions (and the string/language algebra every later topic uses) |
| `02-FINITE-AUTOMATA/` | Finite automata |
| `03-CONTEXT-FREE-GRAMMARS/` | Context-free grammars |
| `04-PUSH-DOWN-AUTOMATA/` | Push-down automata |
| `05-REGULAR-LANGUAGES/` | Regular languages |
| `06-CONTEXT-FREE-LANGUAGES/` | Context-free languages |
| `07-PUMPING-LEMMA/` | Pumping lemma |
| `08-TURING-MACHINES/` | Turing machines |
| `09-UNDECIDABILITY/` | Undecidability |

No unofficial topic folder was added. Complexity classes (P, NP) are not a TOC syllabus line. A few mapped stems mention NP; they are listed as mapping noise in `09-UNDECIDABILITY/PYQ.md`.

## Order

Study in this dependency order, even though the folder numbers put languages after the machines that accept them.

1. Regular expressions. Alphabets, strings, `∅` vs `{ε}`, reading an RE, Arden, Thompson.
2. Finite automata. DFA / NFA / ε-NFA, subset construction, distinguishability, minimization. This is the highest-volume PYQ folder.
3. Regular languages. What “regular” means, closure, Myhill–Nerode, regular grammars. You already have the machines; this folder is the algebra of the family.
4. Pumping lemma (regular half first). A necessary condition only. Use it after you can write a DFA, not instead of one.
5. Context-free grammars. Derivations, parse trees, ambiguity, Chomsky normal form (the `2n−1` step count).
6. Push-down automata. The machine for CFGs. Final state vs empty stack; DPDA vs NPDA.
7. Context-free languages. Closure (union yes, intersection no, intersection-with-regular yes). Nested vs crossed dependencies.
8. Pumping lemma (CFL half). The `uvwxy` window. Revisit `{a^n b^n c^n}` here.
9. Turing machines. Decides vs recognizes. Recursive vs RE.
10. Undecidability. Reductions and the standard table by model. Rice’s theorem for properties of `L(M)`.

Finite automata and regular languages share constructions; so do CFGs and PDAs. If a PYQ asks “min DFA states”, stay in folder 02. If it asks “is this regular?”, stay in folder 05. If it asks both, do the construction in 02 and the classification in 05.

## How PYQs and practice fit together

Past papers for 2007–2026 are in `../12-PYQ/`. Topic extracts are in `../13-PYQ-TOPIC-MAPPING/06-THEORY-OF-COMPUTATION/`. Each topic `PYQ.md` points at that folder.

The mapping is usable and uneven:

- Finite automata, regular languages, CFGs, and undecidability have many recognizable stems. The notes are built from those patterns: min DFA sizes, NFA-to-DFA bounds, closure yes/no, grammar counting, the decidability table.
- Push-down automata and pumping lemma have almost no clean mapped construction questions. Depth there comes from the existing practice file and from CFL/undecidability stems that need a PDA or a pumping argument.
- Several stored blocks are compilers, architecture, probability, or NP-completeness. Each `PYQ.md` lists those separately. They are not counted as TOC evidence.
- The four 2013 booklets repeat the same questions. Priority counts distinct questions, not booklet reprints.
- Year headings inside several `questions.md` files can disagree with the `Paper` line. Topic `PYQ.md` files follow `Paper`.
- Every stored answer field seen for this subject is `VERIFICATION REQUIRED`. These notes do not invent official keys. Work the paper.

`TOPIC-PRIORITY.md` and `PYQ-COVERAGE.md` record the counts under that rule. `FORMULA-INDEX.md` links every formula sheet.

## Suggested study flow

1. Read `NOTES.md` and work the constructions, including the reason for each conversion and each closure.
2. Check `FORMULAS.md` and `SHORTCUTS.md`.
3. Solve this folder’s `PRACTICE.md` from Level 1 through Level 5.
4. Solve the matching file under `14-PRACTICE-QUESTIONS`.
5. Solve the recognizable rows in `PYQ.md` from the linked paper. Log misses in `MISTAKES.md`.
6. Revise from `REVISION.md`.

## Construction and proof questions

GATE TOC is not a definition quiz. The stems that keep returning ask you to *do* something.

| Job | What to write first | Folder |
|-----|---------------------|--------|
| Min DFA size | The information a state must remember; then pairwise distinguishable strings | 02, 05 |
| NFA → DFA bound | Powersets `≤ 2^n`; 1-state is possible; `k ≥ n` is not forced | 02 |
| Which RE / which language of a DFA | Short accepted and rejected strings; `ε` first | 01, 02 |
| Regular or not | DFA / RE / finite, or infinitely many distinguishable prefixes | 05 |
| Language of a CFG | What each production adds to the letter counts | 03 |
| CFL or not | One stack / nested pairs, or a crossed pair / three equal counts | 06, 04 |
| Pumping | Fix `p`, pick one long `s`, defeat **every** legal split | 07 |
| Decides vs recognizes | Halt on every input, or only accept the yes-instances | 08 |
| Decidable? | Name the model first, then the property; do not copy a TM fact onto a DFA | 09 |
| Reduction | “If *this* were decidable, *that* known-undecidable problem would be too” | 09 |

For a construction: draw the machine or the grammar, then test `ε`, a shortest member, and a just-illegal string. For a proof that a language is not regular / not CFL: the pumping lemma is the usual written argument; Myhill–Nerode (distinguishable prefixes) is faster when the prefixes are obvious. For decidability: a single algorithm sketch (reachability, generating variables, minimization) or a single reduction sketch is enough. Do not quote Rice on a syntactic property such as “exactly five states”.
