# GATE PYQs

## 2026

### Q.43

**Paper:** GATE 2026 CS-1 (forenoon)

**Question:**

Consider a relational database schema with two relations 𝑅(𝑃, 𝑄) and 𝑆(𝑋, 𝑌).
Let  𝐸 = {⟨𝑢⟩∣∃𝑣 ∃𝑤  ⟨𝑢, 𝑣⟩∈𝑅 ∧ ⟨𝑣, 𝑤⟩ ∈𝑆}  be a tuple relational calculus
expression.
Which one of the following relational algebraic expressions is equivalent to 𝐸 ?

**Options:**

A. 𝛱_{𝑃}(𝑅⋈𝑅.𝑃=𝑆.𝑋 𝑆)
B. 𝛱_{𝑃}(𝑆⋈𝑆.𝑋=𝑅.𝑄 𝑅)
C. 𝛱_{𝑃}(𝑅⋈𝑅.𝑃=𝑆.𝑌 𝑆)
D. 𝛱_{𝑃}(𝑆⋈𝑆.𝑌=𝑅.𝑄 𝑅)

**Type:** MCQ

**Answer:** VERIFICATION REQUIRED

**Source:** GATE 2026 CS-1 (forenoon), `12-PYQ/2026/set-01/question-paper.pdf`

---

## 2008

### Q.15

**Paper:** GATE 2008 CS

**Question:**

Which of the following tuple relational calculus expression(s) is/are equivalent to Vt e r(P(t))?
I. -3 te r(P(t)
II. 3 te r(P(t))
III. -3 te r(→P(t))
IV. 3te r(→P(t)

**Options:**

A. Ionly
B. II only
C. III only
D. IIl and IV only

**Type:** MCQ

**Answer:** VERIFICATION REQUIRED

**Source:** GATE 2008 CS, `12-PYQ/2008/question-paper.pdf`

---

## 2007

### Q.60

**Paper:** GATE 2007 CS

**Question:**

Consider the relation employee(name, sex, supervisorName) with name as the key.
supervisorName gives the name of the supervisor of the employee under
consideration. What does the following Tuple Relational Calculus query produce?
{e.name | employee(e) ^
(Vx)[ - employee(x) V x.supervisorName = e.name V x.sex = "male"])

**Options:**

A. Names of employees with a male supervisor.
B. Names of employees with no immediate male subordinates.
C. Names of employees with no immediate female subordinates:
D. Names of employees with a female supervisor.

**Type:** MCQ

**Answer:** VERIFICATION REQUIRED

**Source:** GATE 2007 CS, `12-PYQ/2007/question-paper.pdf`

---
