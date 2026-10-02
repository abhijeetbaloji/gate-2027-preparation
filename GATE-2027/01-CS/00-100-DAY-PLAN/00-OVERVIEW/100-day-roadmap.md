# 100-day roadmap — GATE 2027 CS

This is a study system, not a set of notes. The loop on every day is: learn, practice, PYQ, test when scheduled, analyse, revise, repeat.

## Sources used

1. Official CS syllabus: `GATE-2027/00-GATE-2027/official-syllabus/CS/syllabus.md` (GATE 2027, IIT Madras; syllabus PDF dated 6 July 2026 in the file record).
2. PYQ archive: `GATE-2027/01-CS/12-PYQ/` and its readme. The archive holds CS papers from 2007 through 2026. 2017 session 1 is missing. 2027 has not been held. Count of stored papers: 32.
3. PYQ topic-mapping folders: `GATE-2027/01-CS/13-PYQ-TOPIC-MAPPING/`. The folders follow the syllabus. They do not contain question lists or counts. This plan does not assign priority labels and does not claim a historical mark share for any CS section.
4. Exam pattern: `GATE-2027/00-GATE-2027/exam-pattern/CS/pattern.md` and `GATE-2027/00-GATE-2027/exam-pattern/general-question-pattern.md`.
5. General Aptitude syllabus PDF: https://gate2027.iitm.ac.in/static/doc/GATE2027_Syllabus/GA_GATE2027_Syllabus.pdf (checked 2 October 2026). GA is not transcribed inside the CS syllabus file. The pattern file records GA as 15 marks on the CS paper, so it is scheduled here.

## Official CS paper shape (used for full mocks and for MONTHLY-09 onward)

- 100 marks, 180 minutes, computer-based.
- 10 General Aptitude questions (15 marks: five of 1 mark and five of 2 marks) and 55 subject questions.
- Inside the 85-mark subject component, Engineering Mathematics is 13 marks and the remaining subject questions are 72 marks.
- The official pattern does not publish how many Engineering Mathematics questions make up those 13 marks, or how the 55 subject questions split between 1-mark and 2-mark items. This plan does not invent those counts.
- MCQ: 1/3 deducted for a wrong 1-mark choice; 2/3 deducted for a wrong 2-mark choice.
- MSQ and NAT: no negative marking and no partial credit.
- Question types: MCQ, MSQ, NAT. Abilities: recall, comprehension, application, analysis and synthesis.

Early alternate-day and weekly papers are 100-mark topical papers. They are not miniature copies of that 15/13/72 split, because most of the syllabus is still unstudied. The split begins when the syllabus is complete.

## What one day is allowed to hold

Assumed length of a full day: about 7 hours. If you have less time, cut new learning before you cut revision, PYQ, or a scheduled test.

| Kind of day | New learning | Practice | PYQ | Revision and mistakes | Test |
| --- | --- | --- | --- | --- | --- |
| Learning day (no 100-mark paper) | 150–180 minutes | 50 minutes | 50–70 minutes | about 45 minutes | None |
| Alternate-test day | 80–90 minutes | 25 minutes | Inside the paper; 20 minutes extra only if needed | 15 minutes after the paper | 90–120 minutes plus analysis |
| Weekly or monthly day | None | Redo misses | Inside the paper | Analysis 60–90 minutes | The scheduled paper |
| Full mock | None | The paper | The named archive paper | 20-minute log only | 180 minutes |
| Next day after a mock or after MONTHLY-09 | None | Redo misses | Older mixed papers, capped | Analysis, then a section sweep | None |

A day never opens two unrelated subjects as new work. A second block, when it exists, is the next clause of the same subject, or a short General Aptitude block.

## Phases

| Phase | Days | Job | New syllabus? |
| --- | --- | --- | --- |
| 1 | 1–28 | Foundation: discrete mathematics, Programming in C, linear data structures, digital logic, start of GA verbal and numerical computation | Yes |
| 2 | 29–56 | Rest of Engineering Mathematics, trees and graphs, algorithms, theory of computation | Yes |
| 3 | 57–83 | Computer organization, operating systems, databases, compiler design, computer networks, rest of GA | Yes. Last new clause is Day 83. |
| 4 | 84–90 | First full pass back over the syllabus, first two unseen mocks | No |
| 5 | 91–94 | Full cumulative paper, analysis, weak-area repair, third mock | No |
| 6 | 95–100 | Analysis, repair, fourth mock, final weekly, rapid revision | No |

Exit from Phase 3: every row in `subject-coverage.md` has a first day. Exit from Phase 4: two unseen papers have been sat and analysed. Exit from Phase 6: the mistake book has been through a final pass and TEST-026 is scored.

## Why this order

Dependencies from the official clauses, not from a generic CS curriculum:

- Discrete mathematics (logic, relations, graphs, counting, recurrences) comes before algorithms, theory of computation, and the parts of databases that use sets and functions.
- Programming in C and recursion come before arrays, stacks, queues, lists, trees, heaps, and graphs.
- Those structures come before searching, sorting, hashing, design techniques, traversals, spanning trees, and shortest paths.
- Boolean algebra and combinational circuits come before sequential circuits.
- Fixed-point and floating-point representation come before ALU and datapath reasoning in computer organization.
- Cache and the rest of the instruction path come before pipelining.
- Processes come before synchronization, deadlock, and scheduling. Memory management comes before the file-system block.
- ER-model and relational algebra come before SQL, normal forms, indexing, and transactions.
- Synchronization comes before transaction concurrency.
- Regular expressions and grammars come before lexical analysis and parsing. Parsing comes before syntax-directed translation, runtime environments, intermediate code, and data-flow analysis.
- Layering, switching, and the data link layer come before routing, IPv4, TCP, DNS, and HTTP.
- General Aptitude is started in Phase 1 and continued as short secondary blocks so it is not a last-week add-on. Permutations and combinations sit both in discrete counting and later as GA numerical items.

Linear algebra and calculus are official Engineering Mathematics clauses. They are placed in Phase 2 as a continuous mathematics block after the probability start, before the algorithm block, so the 13-mark mathematics section is not left to the end. They are not treated as hidden prerequisites for topics the CS syllabus does not connect to them.

Out-of-syllabus prerequisites are not added. Pointers appear only as part of Programming in C, because the listed data structures are implemented in that language.

## Day budget by section

Days are not split evenly. A day is counted if it opens at least one clause of that section. Combined days are counted once here and named in the day file.

| Section | First-study days | Why this amount of time |
| --- | --- | --- |
| Engineering Mathematics | 1–5, 8–9, 11–13, 29, 31–33, 36–39 | Official 13-mark block, and discrete mathematics feeds later sections. Distributions share a day with summary statistics because they are one syllabus paragraph. |
| General Aptitude | Secondary blocks on 11, 12, 13, 26, 31, 37, 53, 55, 59, 83 | Official 15 marks. Short blocks from Phase 1 onward, then every cumulative paper. |
| Programming and Data Structures | 15–19, 41, 43 | C and linear structures before trees. Trees share a day with BST. Heaps share a day with graph representation. |
| Digital Logic | 22–27 | Minimization is split across two days because the syllabus names three methods. Fixed-point and floating-point are split because both are numerical. |
| Algorithms | 44–47, 50–51 | Dynamic programming and shortest paths get learning days. Searching, sorting, and hashing share one test day, with hashing redone on the Day 48 consolidation. |
| Theory of Computation | 52–55 | Automata, grammars, pumping lemma, then machines and undecidability, in that order. |
| Computer Organization and Architecture | 57–59, 61 | Pipeline shares a day with I/O. Pipeline gets the longer block. |
| Operating System | 64–67 | Synchronization and deadlock share a day. Virtual memory gets the longer share of the memory and file-system day. |
| Databases | 68–69, 71–73 | Normal forms, indexing, and transactions each get their own day. |
| Compiler Design | 74–75, 78 | The syllabus groups lexical analysis with parsing, and groups the three data-flow analyses together. |
| Computer Networks | 79, 81–83 | Layering and data link share a day. Routing and IPv4 share a day. TCP gets a test day. DNS and HTTP close the syllabus. |

## Spaced return

A clause is opened once, then:

1. The next learning day revisits it for about 25 minutes.
2. The next alternate, weekly, or monthly paper includes it in the cumulative slice.
3. A named older-return block (about 20 minutes) cycles through clauses that are already open. The anchor is written on each day.
4. Phase 4–6 sweep whole sections again.
5. The final ten days use the mistake book rather than new headings.

No section ends when its first-study days end. Later days name it again. The sample return days are in `subject-coverage.md`.

## Tests

The calendar is every other day, with two deliberate exceptions so that a 3-hour paper is not followed by another 100-mark paper, and so that the day before a weekly paper can be used for revision.

- Even days are 100-mark alternate papers, except the consolidation days 6, 20, 34, 48, 62, 76, and 90, the weekly days 14, 28, 42, 56, 84, and 98, the monthly days 10, 30, 40, 60, 70, and 80, the mock days 86, 88, 94, and 96, and Day 92.
- Day 92 is the analysis of MONTHLY-09. It does not add a second paper.
- Odd days are learning or analysis days, except weekly or monthly papers on Days 7, 21, 35, 49, 63, 77, and 91.
- Weeks 3, 7, 10, and 13 close with the monthly paper instead of a second weekly paper.

Counts:

- Alternate-day papers: TEST-001 through TEST-026 (Day 100 is TEST-026).
- Weekly papers: WEEKLY-01 through WEEKLY-10.
- Monthly cumulative papers: MONTHLY-01 through MONTHLY-09.
- Unseen full mocks: MOCK-01 through MOCK-04.

Mark mix moves from mostly recent to mostly cumulative. The exact mix is on each `test-target.md` and in `test-strategy.md`.

## PYQ policy

Recent papers are used while a clause is new, so the current pattern is seen early. Older papers are used for recurrence during consolidation and during Phases 4–6.

Held out for timed mocks, and not to be opened early:

- MOCK-01, Day 86: 2024 set-02
- MOCK-02, Day 88: 2025 set-02
- MOCK-03, Day 94: 2026 set-02
- MOCK-04, Day 96: 2023

Reserve if one of those papers is already familiar: 2017 set-02, 2016 set-01.

Daily PYQ is a timed selection of matching questions, not a promise of a fixed count. The archive is not tagged by topic.

## Final ten days (91–100)

No new clauses.

- Day 91: full cumulative paper, official 15/13/72 shape, 180 minutes.
- Day 92: analysis and databases plus networks.
- Day 93: weak-area repair from the tracker.
- Day 94: unseen 2026 set-02.
- Day 95: analysis and repair.
- Day 96: unseen 2023 paper.
- Day 97: analysis and repair.
- Day 98: full-syllabus weekly.
- Day 99: mistake-book and formula sweep. Formulas come from your own sheet.
- Day 100: 90-minute mixed 100-mark paper, then a short close. No new heading.

## How to start

1. Pick the calendar date for Day 1 and write it on that day's plan. The plan is relative; it is not pinned to 2 October 2026. GATE 2027 exam dates in the important-dates file are 6–7, 13–14, and 20–21 February 2027, and those dates can change.
2. Keep one mistake book, physical or digital, outside this folder.
3. Fill `daily-tracker.md` at the end of the day. Leave future scores blank.
4. After each weekly or monthly paper, write the adjustment before the next block.
