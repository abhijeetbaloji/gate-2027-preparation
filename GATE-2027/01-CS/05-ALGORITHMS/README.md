# Algorithms (GATE CS)

Study material for Section 5 of the official GATE 2027 CS syllabus.

Searching, sorting, hashing. Asymptotic worst-case time and space complexity. Algorithm design techniques: greedy, dynamic programming and divide-and-conquer. Graph traversals, minimum spanning trees, shortest paths.

## How to use this section

| File | Purpose | When to use |
|------|---------|-------------|
| `NOTES.md` | Learning notes: definitions, reasons, worked steps, complexity | First study of a topic |
| `REVISION.md` | Short sheet: rules, bounds, traps | After the notes, and again before a test |
| `FORMULAS.md` | Bounds and recurrences with the condition that makes them true | Lookup while solving |
| `SHORTCUTS.md` | Checks that are valid only in a stated situation | Timed practice, after you know why they hold |
| `PYQ.md` | Mapped previous-year questions | After the notes. Solve from the original paper |
| `PRACTICE.md` | Practice questions at five levels, with explanations | Before or beside past papers. These are not past-paper questions |
| `MISTAKES.md` | Common traps, plus an empty log for your own errors | After every practice session |

`REVISION.md` is not a substitute for `NOTES.md`.

## How the folders are organised

The folder names are the syllabus lines, in the order already created. Nothing here renames them.

| Folder | Syllabus line |
|--------|----------------|
| `01-SEARCHING/` | Searching |
| `02-SORTING/` | Sorting |
| `03-HASHING/` | Hashing |
| `04-ASYMPTOTIC-WORST-CASE-TIME-AND-SPACE-COMPLEXITY/` | Asymptotic worst-case time and space complexity |
| `05-ALGORITHM-DESIGN-TECHNIQUES/01-GREEDY/` | Greedy |
| `05-ALGORITHM-DESIGN-TECHNIQUES/02-DYNAMIC-PROGRAMMING/` | Dynamic programming |
| `05-ALGORITHM-DESIGN-TECHNIQUES/03-DIVIDE-AND-CONQUER/` | Divide-and-conquer |
| `06-GRAPH-TRAVERSALS/` | Graph traversals |
| `07-MINIMUM-SPANNING-TREES/` | Minimum spanning trees |
| `08-SHORTEST-PATHS/` | Shortest paths |

Heaps and graph representations are also used here. As data structures they sit under Programming and Data Structures. These notes use them only to explain sorting, traversals, spanning trees, and shortest paths.

## How PYQs are linked

Past papers for 2007–2026 are stored in `../12-PYQ/`. Topic rows, when they exist, are stored in `../13-PYQ-TOPIC-MAPPING/05-ALGORITHMS/`. Each topic `PYQ.md` points at that folder and lists only rows that are actually mapped.

The Algorithms mapping folders do not yet contain `pyq-mapping.md` files. The Engineering Mathematics mapping states that Algorithms is not mapped. Because of that, the tables in `PYQ.md` are empty. Question numbers are not guessed. `PYQ-COVERAGE.md` records the same fact.

## Suggested study flow

1. Read `NOTES.md` and work the examples, including the reason for each complexity bound.
2. Check `FORMULAS.md` and `SHORTCUTS.md`.
3. Solve `PRACTICE.md` from Level 1 through Level 5.
4. When a mapping file exists, solve those questions from the linked paper and log misses in `MISTAKES.md`.
5. Revise from `REVISION.md`.

## Master files

- `TOPIC-PRIORITY.md` — what the repository can and cannot say about priority
- `PYQ-COVERAGE.md` — year-wise and topic-wise mapping status
- `FORMULA-INDEX.md` — links to every topic formula sheet

## Related folders

- Official syllabus: `../../00-GATE-2027/official-syllabus/CS/syllabus.md`
- 100-day plan: `../00-100-DAY-PLAN/` (Algorithms is scheduled on days 44–47 and 50–51)
- PYQ archive: `../12-PYQ/`
- PYQ topic mapping: `../13-PYQ-TOPIC-MAPPING/05-ALGORITHMS/`
