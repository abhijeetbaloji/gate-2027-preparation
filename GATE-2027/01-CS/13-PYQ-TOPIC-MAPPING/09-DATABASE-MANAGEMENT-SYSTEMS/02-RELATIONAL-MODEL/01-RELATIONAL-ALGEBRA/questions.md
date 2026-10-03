# GATE PYQs

## 2022

### Q.25

**Paper:** GATE 2022 CS

**Question:**

Consider the following three relations in a relational database.
Employee( eId , Name),  Brand (bId ,bName),  Own( eId ,bId)
Which of the following relational algebra expressions return the set of  eIds
who own all the brands?

**Options:**

A. _{eId} (_{eId} ,bId (Own) / _{bId} (Brand))
B.  (Own) − ( (Own)× (Brand)) − (Own) eId eId eId bId eId ,bId
C. _{eId} (_{eId} ,bId (Own) / _{bId} (Own))
D.  ( (Own)× (Own)) /  (Brand) eId eId bId bId

**Type:** MCQ

**Answer:** VERIFICATION REQUIRED

**Source:** GATE 2022 CS, `12-PYQ/2022/question-paper.pdf`

---

## 2021

### Q.27

**Paper:** GATE 2021 CS Set-1

**Question:**

The following relation records the age of 500 employees of a company, where empNo
(indicating the employee number) is the key:
empAge(empNo, age)
Consider the following relational algebra expression:
IempNo(empAge X (age>agel) PempNo1, agel (empAge))
What does the above expression generate?

**Options:**

A. Employee numbers of only those employees whose age is the maximum.
B. Employee numbers of only those employees whose age is more than the age of exactly one other employee.
C. Employee numbers of all employees whose age is not the minimum.
D. Employee numbers of all employees whose age is the minimum. GATE Graduate Aptitude Test in Engineering 2021 2021 Organising Institute - IIT Bombay

**Type:** MCQ

**Answer:** VERIFICATION REQUIRED

**Source:** GATE 2021 CS Set-1, `12-PYQ/2021/set-01/question-paper.pdf`

---

## 2019

### Q.55

**Paper:** GATE 2019 CS (printed header Set-2)

**Question:**

Consider the following relations P(X,Y,Z), Q(X,Y,T) and R(Y,V).
P Q R
T Y
XI Y1 X2 YI 2 Y1 V1
X1 Y1 Z2 XI Y2 5 Y3 V2
X2 Y2 Z2 XI 6 Y2 V3
X2 Y4 ZA X3 73 1 Y2 V2
How many tuples will be returned by the following relational algebra query?
П(PYERY 1avava (PXR))- (CeraRrneTsD)(0XR))
Answer:

**Options:**

The paper does not print options for this numerical-answer question.

**Type:** NAT

**Answer:** VERIFICATION REQUIRED

**Source:** GATE 2019 CS (printed header Set-2), `12-PYQ/2019/question-paper.pdf`

---

## 2014

### Q.30

**Paper:** GATE 2014 CS SET-3

**Question:**

Consider the relational schema given below, where eId of the relation dependent is a foreign
key referring to empId of the relation employee. Assume that every employee has at least one
associated dependent in the dependent relation.
employee (empId, empName, empAge)
dependent(depId, eId, depName, depAge)
Consider the following relational algebra query:
∏empId(employee)-∏empId(employee⋈_{(}empId = eID)∧(empAge≤ depAge)dependent)
The above query evaluates to the set of empIds of employees whose age is greater than that of

**Options:**

A. some dependent.
B. all dependents.
C. some of his/her dependents.
D. all of his/her dependents.

**Type:** MCQ

**Answer:** VERIFICATION REQUIRED

**Source:** GATE 2014 CS SET-3, `12-PYQ/2014/set-03/question-paper.pdf`

---

## 2012

### Q.50

**Paper:** GATE 2012 CS Booklet A

**Question:**

How many tuples does the result of the following relational algebra expression contain? Assume
that the schema of A∪B is the same as that of A.
(A∪B) ⋈ A.Id > 40 ∧ C.Id < 15 _{C}

**Options:**

A. 7
B. 4
C. 5
D. 9

**Type:** MCQ

**Answer:** VERIFICATION REQUIRED

**Source:** GATE 2012 CS Booklet A, `12-PYQ/2012/question-paper.pdf`

---

## 2010

### Q.43

**Paper:** GATE 2010 CS

**Question:**

The fallowing functional dependencies hold for relations R(A, B, C) and S(B, D. E):
B →+ А,
1→C
The relation R contains 200 tuples and the rolation S contains 100 tuples. What is the maximum
number of tuples possible in the natural join RIX.S?

**Options:**

A. 100
B. 200
C. 300
D. 200 • HN24

**Type:** MCQ

**Answer:** VERIFICATION REQUIRED

**Source:** GATE 2010 CS, `12-PYQ/2010/question-paper.pdf`

---

## 2007

### Q.59

**Paper:** GATE 2007 CS

**Question:**

Information about a collection of students is given by the relation studinfo(studld,
name, sex). The relation enroll(studld, courseld) gives which student has enrolled for
at least one female student. What does the following relational algebra expression (or taken) what course(s). Assume that every course is taken by at least one male and
represent?
IIcourseld ((IIstudia(Osex = "female*(studInfo)) x Icourseld(enroll)) - enroll)

**Options:**

A. Courses in which all the female students are enrolled
B. Courses in which a proper subset of female students are enrolled.
C. Courses in which only male students are enrolled.
D. None of the above.

**Type:** MCQ

**Answer:** VERIFICATION REQUIRED

**Source:** GATE 2007 CS, `12-PYQ/2007/question-paper.pdf`

---
