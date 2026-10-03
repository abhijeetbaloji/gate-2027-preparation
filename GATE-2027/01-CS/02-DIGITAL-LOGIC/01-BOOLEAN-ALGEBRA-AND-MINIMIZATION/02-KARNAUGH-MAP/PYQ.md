# Karnaugh Map — Previous Year Questions

Question text stays in the mapping file. Year headings in that file do not always match the `Paper` line; this page follows `Paper`. Stored answers are `VERIFICATION REQUIRED`. The maps themselves are only partly recovered from the PDF text, so this page does not recompute an official key from a broken figure.

Mapping file: `../../../13-PYQ-TOPIC-MAPPING/02-DIGITAL-LOGIC/01-BOOLEAN-ALGEBRA-AND-MINIMIZATION/02-KARNAUGH-MAP/questions.md`

Papers: `../../../12-PYQ/`.

## What the recognizable stems test

Four stored blocks are K-map questions.

- GATE 2025 CS-2 Q.43 (MSQ). A 4-variable map is given. More than one expression may equal \(F\). The check is cell by cell, and “equal” is not the same as “minimal.”
- GATE 2017 CS Session 2 Q.28 (MCQ). Minterm list plus don’t-cares, and the asked form is a **minimum product of sums**. Group the 0s, or minimize \(F'\) and complement. The options in the extract are visually corrupted; use the paper.
- GATE 2012 CS Q.30 (MCQ). A drawn map with X as don’t-care. Minimal form. Redundant products show up as extra options.
- GATE 2008 CS Q.5 (MCQ). Same pattern: drawn map, X as don’t-care, minimal form. The option text in the extract is not reliable enough to grade from.

Many other minimal-SOP stems, including don’t-care lists and essential-prime counts, are stored under algebraic technique. They are solved with this map. See that topic’s `PYQ.md`.

## Row that is not a K-map

| Paper | Question | Why it is not this topic |
|-------|----------|--------------------------|
| GATE 2011 CS | Q.43 | Direct-mapped cache tag size |

## Coverage gap

The mapping has no K-map stem for 2026, 2024, 2023, 2022, 2021, 2020, 2019, 2018, 2016, 2015, 2014, 2013, 2010, 2009, or 2007. The tabular-method file has the 2015 prime-implicant count. Absence from this file is not a claim that no other paper showed a map.

| Paper | Question | Type | Pattern |
|-------|----------|------|---------|
| GATE 2025 CS-2 | Q.43 | MSQ | Which expressions match a drawn map |
| GATE 2017 CS Session 2 | Q.28 | MCQ | Minimum POS with don’t-cares |
| GATE 2012 CS | Q.30 | MCQ | Minimal form of a map with X |
| GATE 2008 CS | Q.5 | MCQ | Minimal form of a map with X |
