# Computer Organization & Architecture (GATE CS)

Study material for **Section 3** of the official GATE 2027 CS syllabus:

> Instruction set and addressing modes. Design of arithmetic and logic unit (ALU). Design of control unit – hardwired and microprogrammed. Memory interfacing and hierarchy: performance, cache memory mapping. I/O interface (interrupt and DMA). Instruction pipelining, pipeline hazards.

Official syllabus: [`../../00-GATE-2027/official-syllabus/CS/syllabus.md`](../../00-GATE-2027/official-syllabus/CS/syllabus.md)

---

## How to use this section

| File | Purpose | When to use |
|------|---------|-------------|
| `NOTES.md` | **Detailed learning notes** — learn the topic from scratch | First time studying, or after a long gap |
| `REVISION.md` | **Compressed revision sheet** — definitions, formulas, traps only | After you have already studied `NOTES.md` |
| `FORMULAS.md` | Formula reference with conditions and typical GATE use | Quick lookup while solving |
| `SHORTCUTS.md` | Valid shortcuts with when they work and when they fail | During timed practice |
| `PYQ.md` | Mapped previous-year questions (2007–2026) — concepts and methods only | After learning; solve from the original paper |
| `PRACTICE.md` | Multi-level GATE-style practice (not PYQs) | After `NOTES.md`, before or alongside PYQs |
| `MISTAKES.md` | Common traps + your personal mistake log | After every practice session |

**Important:** `NOTES.md` and `REVISION.md` serve different roles. Do not treat `REVISION.md` as a substitute for learning.

**Answers:** the PYQ mapping marks every answer "VERIFICATION REQUIRED". Topic `PYQ.md` files teach methods and patterns; they do not state official keys. Confirm answers from the original paper or an authoritative solution.

---

## Folder structure

| Folder | Syllabus block |
|--------|----------------|
| [`01-INSTRUCTION-SET/`](01-INSTRUCTION-SET/) | ISA, instruction formats, encoding, load/store, performance basics |
| [`02-ADDRESSING-MODES/`](02-ADDRESSING-MODES/) | Effective address, PC-relative, encoding interplay |
| [`03-ARITHMETIC-AND-LOGIC-UNIT/`](03-ARITHMETIC-AND-LOGIC-UNIT/) | Adders, ALU, datapath, multiplication/division |
| [`04-DESIGN-OF-CONTROL-UNIT/01-HARDWIRED/`](04-DESIGN-OF-CONTROL-UNIT/01-HARDWIRED/) | Hardwired control, micro-operations, timing |
| [`04-DESIGN-OF-CONTROL-UNIT/02-MICROPROGRAMMED/`](04-DESIGN-OF-CONTROL-UNIT/02-MICROPROGRAMMED/) | Control store, horizontal/vertical microinstructions |
| [`05-MEMORY-INTERFACING-AND-HIERARCHY/01-PERFORMANCE/`](05-MEMORY-INTERFACING-AND-HIERARCHY/01-PERFORMANCE/) | Hierarchy, AMAT, interleaving, chip interfacing |
| [`05-MEMORY-INTERFACING-AND-HIERARCHY/02-CACHE-MEMORY-MAPPING/`](05-MEMORY-INTERFACING-AND-HIERARCHY/02-CACHE-MEMORY-MAPPING/) | Cache organisations, tag/index, hit/miss, write policies |
| [`06-IO-INTERFACE/01-INTERRUPT/`](06-IO-INTERFACE/01-INTERRUPT/) | Polling, interrupts, priority, CPU-fraction numerics |
| [`06-IO-INTERFACE/02-DMA/`](06-IO-INTERFACE/02-DMA/) | DMA modes, bus arbitration, throughput |
| [`07-INSTRUCTION-PIPELINING/`](07-INSTRUCTION-PIPELINING/) | Ideal pipeline, speedup, stage timing |
| [`08-PIPELINE-HAZARDS/`](08-PIPELINE-HAZARDS/) | Structural/data/control hazards, forwarding, stalls |

---

## Recommended study order (dependencies)

```
Digital Logic (number representation) ──┐
                                        ├──► 01 Instruction Set ──► 02 Addressing Modes
                                        │              │
                                        │              └──► 03 ALU (datapath) ──► 04 Control Unit
                                        │                        (hardwired, then microprogrammed)
                                        │
                                        └──► 05 Memory Performance ──► 05 Cache Mapping
                                                      │
                                                      ├──► 07 Instruction Pipelining ──► 08 Pipeline Hazards
                                                      │
                                                      └──► 06 I/O (Interrupt, then DMA)
```

**Practical path for GATE numerics:**

1. **01 Instruction Set** + **02 Addressing Modes** — encoding and EA skills used everywhere.
2. **05 Performance** + **05 Cache** — highest PYQ density; budget the most time here.
3. **07 Pipelining** + **08 Hazards** — second-highest density; always state forwarding and register-file assumptions.
4. **03 ALU** + **04 Control** — thinner mapped PYQ evidence; syllabus-driven depth from practice files.
5. **06 Interrupt** then **06 DMA** — fraction/rate arithmetic; read interrupt before DMA.

Cross-subject bridges (not owned here): fixed/floating representation → [`../02-DIGITAL-LOGIC/`](../02-DIGITAL-LOGIC/); virtual memory/TLB → [`../08-OPERATING-SYSTEMS/08-MEMORY-MANAGEMENT-AND-VIRTUAL-MEMORY/`](../08-OPERATING-SYSTEMS/08-MEMORY-MANAGEMENT-AND-VIRTUAL-MEMORY/).

---

## How to use PYQs + practice + notes

1. Read `NOTES.md` for the topic — work through every worked example.
2. Skim `FORMULAS.md` and `SHORTCUTS.md`.
3. Solve `PRACTICE.md` Level 1–3, then 4–5 (answers are under each question).
4. Open `PYQ.md` — note the pattern; solve from the linked paper in [`../12-PYQ/`](../12-PYQ/) (do not rely on mapping text alone; figures and tables are often missing).
5. Log errors in `MISTAKES.md` under **My Mistakes**.
6. Before the exam, revise using `REVISION.md` only.

Existing topic-wise practice (168 questions, separate answer style): [`../14-PRACTICE-QUESTIONS/TOPIC-WISE/03-COMPUTER-ORGANIZATION-ARCHITECTURE/`](../14-PRACTICE-QUESTIONS/TOPIC-WISE/03-COMPUTER-ORGANIZATION-ARCHITECTURE/). Each topic folder's `NOTES.md` includes a coverage map to that file.

---

## Numerical problem-solving strategy (COA)

1. **Write assumptions first:** byte vs word addressable; hierarchical vs simultaneous AMAT; RF-A vs RF-B register timing; forwarding on/off; branch resolved in which stage.
2. **Draw the address split** (offset | index | tag) before any cache question.
3. **Use consistent units:** ns for time, bits for tag storage, bytes for capacity unless the question says otherwise. 1 K = 2¹⁰.
4. **Pipeline:** total cycles = (k + N − 1) + stalls; never use N × k for a pipelined machine.
5. **Check both AMAT models** when a question gives only access times and MCQ options — hierarchical and simultaneous answers often differ.
6. **Re-derive** — do not memorise final numbers; opcode-space fractions and stall tables are pattern-based.
7. **End with a sanity check:** hit ratio ≤ 1, CPI ≥ ideal, tag bits + index + offset = address width.

---

## Master files

| File | Purpose |
|------|---------|
| [`TOPIC-PRIORITY.md`](TOPIC-PRIORITY.md) | Study priority from mapped PYQ evidence |
| [`PYQ-COVERAGE.md`](PYQ-COVERAGE.md) | Year-wise and topic-wise PYQ coverage, gaps, mapping noise |
| [`FORMULA-INDEX.md`](FORMULA-INDEX.md) | Cross-topic index into every `FORMULAS.md` |

## Related folders

- PYQ archive: [`../12-PYQ/`](../12-PYQ/)
- PYQ topic mapping: [`../13-PYQ-TOPIC-MAPPING/03-COMPUTER-ORGANIZATION-ARCHITECTURE/`](../13-PYQ-TOPIC-MAPPING/03-COMPUTER-ORGANIZATION-ARCHITECTURE/)
- Practice questions: [`../14-PRACTICE-QUESTIONS/TOPIC-WISE/03-COMPUTER-ORGANIZATION-ARCHITECTURE/`](../14-PRACTICE-QUESTIONS/TOPIC-WISE/03-COMPUTER-ORGANIZATION-ARCHITECTURE/)
