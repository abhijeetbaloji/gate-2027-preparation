# Combinational Circuits — Previous Year Questions

Question text stays in the mapping file. This page follows the `Paper` line when a year heading disagrees with it. Stored answers are `VERIFICATION REQUIRED`. Figures are not reconstructed here.

Mapping file: `../../../13-PYQ-TOPIC-MAPPING/02-DIGITAL-LOGIC/02-DESIGN-OF-COMBINATIONAL-AND-SEQUENTIAL-CIRCUITS/01-COMBINATIONAL-CIRCUITS/questions.md`

Papers: `../../../12-PYQ/`.

## Recognizable combinational stems

| Paper | Question | Type | Pattern |
|-------|----------|------|---------|
| GATE 2026 CS-2 | Q.59 | NAT | Decoder plus 4-to-1 mux; count of input combinations with a stated output |
| GATE 2024 CS1 | Q.64 | NAT | Three 2-to-1 muxes; a count over the input space |
| GATE 2023 CS | Q.44 | MCQ | Two 4-input muxes and one 2-input mux |
| GATE 2016 CS-1 | Q.30 | MCQ | Two cascaded 2-to-1 muxes; minimal SOP of the output |
| GATE 2015 CS, 7 February Shift 2 | Q.65 | NAT | Half-adder and full-adder delays along a carry path |
| GATE 2014 CS SET-1 | Q.45 | MCQ | Minimal SOP of a 4-to-1 mux with given data |
| GATE 2013 CS (four booklets) | Booklet A Q.5, B Q.21, C Q.8, D Q.18 | MCQ | Same encoder-style truth table with a valid bit \(V\). Four printings, one question |
| GATE 2007 CS | Q.8 | MCQ | How many 3-to-8 decoders with enable build a 6-to-64 decoder, no other gates |

The four 2013 booklet rows are one distinct question.

## Decoder or mux used inside a memory question

These stems are in the file. The block is a decoder or a mux; the quantity asked is a memory parameter. They are listed so the mapping is not over-counted as pure logic design.

| Paper | Question | What is asked |
|-------|----------|----------------|
| GATE 2023 CS | Q.42 | Chip select of 1 KB blocks through a decoder |
| GATE 2022 CS | Q.40 | Display path that loads a register; the extract is a system diagram, not a gate equation |
| GATE 2020 CS | Q.19 | Mux between 32 registers and an accumulator |
| GATE 2020 CS | Q.20 | Decoder address lines for a 1 KB RAM; minimum \(m+n\) |
| GATE 2013 CS (four booklets) | A Q.46, B Q.27, C Q.38, D Q.35 | How many \(2\times 4\) decoders build a \(16K \times 16\) RAM from \(1K \times 8\) chips. One question, four printings |

## Rows that are not combinational logic

| Paper | Question | Why it is not this topic |
|-------|----------|--------------------------|
| GATE 2014 CS SET-2 | Q.44 | Cache associativity |
| GATE 2011 CS | Q.46 | A database table |

## Gap

No recognizable adder, mux, or decoder stem is stored here for 2025, 2021, 2019, 2018, 2017, 2012, 2010, 2009, or 2008. A 2007 mux-size question (one mux and one inverter for a function of \(n\) variables) is stored under sequential circuits. Absence from this file is not a claim about the papers.
