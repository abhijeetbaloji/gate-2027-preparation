# GATE PYQs

## 2026

### Q.65

**Paper:** GATE 2026 CS-1 (forenoon)

**Question:**

Consider a relational database schema with a relation  𝑅(𝐴, 𝐵, 𝐶, 𝐷).  If  {𝐴, 𝐵} and
{𝐴, 𝐶} are the only two candidate keys of the relation 𝑅, then the number of superkeys
of relation 𝑅 is ______. (answer in integer)

**Options:**

The paper does not print options for this numerical-answer question.

**Type:** NAT

**Answer:** VERIFICATION REQUIRED

**Source:** GATE 2026 CS-1 (forenoon), `12-PYQ/2026/set-01/question-paper.pdf`

---

## 2022

### Q.31

**Paper:** GATE 2022 CS

**Question:**

Consider a relation  R ( A, B ,C , D , E)  with the following three functional
dependencies.
𝐴𝐵→𝐶;  𝐵𝐶→𝐷;  𝐶→𝐸;
The number of superkeys in the relation R is _____________.

**Options:**

The paper does not print options for this numerical-answer question.

**Type:** NAT

**Answer:** VERIFICATION REQUIRED

**Source:** GATE 2022 CS, `12-PYQ/2022/question-paper.pdf`

---

## 2021

### Q.6

**Paper:** GATE 2021 CS Set-2

**Question:**

Consider the following statements S1 and S2 about the relational data model:
S1: A relation scheme can have at most one foreign key.
S2: A foreign key in a relation scheme R cannot be used to refer to tuples of R.
Which one of the following choices is correct?

**Options:**

A. Both S1 and S2 are true.
B. S1 is true and S2 is false.
C. S1 is false and S2 is true.
D. Both S1 and S2 are false.

**Type:** MCQ

**Answer:** VERIFICATION REQUIRED

**Source:** GATE 2021 CS Set-2, `12-PYQ/2021/set-02/question-paper.pdf`

---

### Q.21

**Paper:** GATE 2021 CS Set-2

**Question:**

A data file consisting of 1,50,000 student-records is stored on a hard disk with block
size of 4096 bytes. The data file is sorted on the primary key RollNo. The size of'
a record pointer for this disk is 7 bytes. Each student-record has a candidate key
attribute called ANum of size 12 bytes. Suppose an index file with records consisting
of two fields, ANum value and the record pointer to the corresponding student record,
is built and stored on the same disk. Assume that the records of data file and index
file are not split across disk blocks. The number of blocks in the index file is

**Options:**

The paper does not print options for this numerical-answer question.

**Type:** NAT

**Answer:** VERIFICATION REQUIRED

**Source:** GATE 2021 CS Set-2, `12-PYQ/2021/set-02/question-paper.pdf`

---

## 2020

### Q.13

**Paper:** GATE 2020 CS

**Question:**

Consider a relational database containing the following schemas.
Catalogue Suppliers
sno pno cost sno sname location
SI P1 150 SI M/s Royal furniture Delhi
S1 P2 50 S2 M/s Balaji furniture Bangalore
S1 P3 100 S3 M/s Premium furniture Chennai
S2 P4 200 Parts
S2 P5 250 pno [ pname partspec
S3 P1 250
S3 P2 150 P1 Table Wood
S3 P5 300 P2 Chair Wood
S3 P4 250 P3 Table Steel
P4 Almirah Steel
P5 Almirah Wood
The primary key of each table is indicated by underlining the constituent fields.
SELECT s.sno, s. sname
FROM Suppliers s, Catalogue c
WHERE s.sno = c.sno AND
cost› (SELECT AVG (cost)
FROM Catalogue
WHERE pno = 'P4'
GROUP BY pno) ;
The number of rows returned by the above SQL query is

**Options:**

A. 4
B. 5
D. 2

**Type:** MCQ

**Answer:** VERIFICATION REQUIRED

**Source:** GATE 2020 CS, `12-PYQ/2020/question-paper.pdf`

---

## 2019

### Q.51

**Paper:** GATE 2019 CS (printed header Set-2)

**Question:**

A relational database contains two tables Student and Performance as shown below:
Student Performance
Roll no. Student name Roll no. Subject code Marks
1 Amit A 86
2 Priya B 95
3 Vinit C 90
4 Rohan A 89
5 Smita C 92
80
The primary key of the Student table is Roll_no. For the Performance table, the columns
Roll no. and Subject code together form the primary key. Consider the SQL query given
SELECT S.Student_name, sum(P.Marks)
FROM Student S, Performance P
WHERE P.Marks > 84
GROUP BY S.Student_name;
The number of rows returned by the above SQL query is

**Options:**

The paper does not print options for this numerical-answer question.

**Type:** NAT

**Answer:** VERIFICATION REQUIRED

**Source:** GATE 2019 CS (printed header Set-2), `12-PYQ/2019/question-paper.pdf`

---

## 2018

### Q.41

**Paper:** GATE 2018 CS

**Question:**

Consider the relations r(A, B) and s(B, C), where s.B is a primary key and r.B is a foreign
key referencing s.B.  Consider the query
Q:  𝑟⋈(𝜎_{𝐵<5}(𝑠))
Let LOJ denote the natural left outer-join operation.  Assume that r and s contain no null
values.
Which one of the following queries is NOT equivalent to Q?

**Options:**

A. 𝜎_{𝐵<5}(𝑟⋈𝑠)
B. 𝜎_{𝐵<5}(𝑟 𝐿𝑂𝐽 𝑠)
C. 𝑟 𝐿𝑂𝐽 (𝜎_{𝐵<5}(𝑠))
D. 𝜎_{𝐵<5}(𝑟) 𝐿𝑂𝐽 𝑠

**Type:** MCQ

**Answer:** VERIFICATION REQUIRED

**Source:** GATE 2018 CS, `12-PYQ/2018/question-paper.pdf`

---

## 2017

### Q.19

**Paper:** GATE 2017 CS Session 2

**Question:**

Correct: 1 Wrong: 0
Consider the following tables T1 and T2.
T1 T2
P R S
2 2 2 2
3 8 8 3
7 3 3 2
5 8 9 7
6 9 5 7
8 5 7 2
9 8
In table T1, P is the primary key and Q is the foreign key referencing R in table T2 with on-delete
cascade and on-update cascade. In table T2, R is the primary key and S is the foreign key
referencing P in table T1 with on-delete set NULL and on-update cascade. In order to delete record
(3,8) from table T1, the number of additional records that need to be deleted from table T1 is

**Options:**

The paper does not print options for this numerical-answer question.

**Type:** NAT

**Answer:** VERIFICATION REQUIRED

**Source:** GATE 2017 CS Session 2, `12-PYQ/2017/set-02/question-paper.pdf`

---

## 2016

### Q.21

**Paper:** GATE 2016 CS-1

**Question:**

Which of the following is NOT a superkey in a relational schema with attributes
V , W , X, Y , Z and primary key V Y ?

**Options:**

A. VXYZ
B. VWXZ
C. VWXY
D. VWXYZ

**Type:** MCQ

**Answer:** VERIFICATION REQUIRED

**Source:** GATE 2016 CS-1, `12-PYQ/2016/set-01/question-paper.pdf`

---

## 2014

### Q.22

**Paper:** GATE 2014 CS SET-1

**Question:**

Given the following statements:
S1: A foreign key declaration can always be replaced by an equivalent check
assertion in SQL.
S2: Given the table R(a,b,c) where a and b together form the primary key,
the following is a valid table definition.
CREATE TABLE S (
a INTEGER,
d INTEGER,
e INTEGER,
PRIMARY KEY (d),
FOREIGN KEY (a) references R)
Which one of the following statements is CORRECT?

**Options:**

A. S1 is TRUE and S2 is FALSE.
B. Both S1 and S2 are TRUE.
C. S1 is FALSE and S2 is TRUE.
D. Both S1 and S2 are FALSE.

**Type:** MCQ

**Answer:** VERIFICATION REQUIRED

**Source:** GATE 2014 CS SET-1, `12-PYQ/2014/set-01/question-paper.pdf`

---

### Q.21

**Paper:** GATE 2014 CS SET-2

**Question:**

The maximum number of superkeys for the relation schema  R(E,F,G,H) with  E as the key is
_____.

**Options:**

The paper does not print options for this numerical-answer question.

**Type:** NAT

**Answer:** VERIFICATION REQUIRED

**Source:** GATE 2014 CS SET-2, `12-PYQ/2014/set-02/question-paper.pdf`

---

### Q.22

**Paper:** GATE 2014 CS SET-3

**Question:**

A prime attribute of a relation scheme ܴ  is an attribute that appears

**Options:**

A. in all candidate keys of ܴ .
B. in some candidate key of ܴ .
C. in a foreign key of ܴ .
D. only in the primary key of ܴ .

**Type:** MCQ

**Answer:** VERIFICATION REQUIRED

**Source:** GATE 2014 CS SET-3, `12-PYQ/2014/set-03/question-paper.pdf`

---

### Q.54

**Paper:** GATE 2014 CS SET-3

**Question:**

Consider the following relational schema:
employee(empId,empName,empDept)
customer(custId,custName,salesRepId,rating)
salesRepId is a foreign key referring to empId of the employee relation. Assume that each
employee makes a sale to at least one customer. What does the following query return?
SELECT empName
FROM employee E
WHERE NOT EXISTS (SELECT custId
FROM customer C
WHERE C.salesRepId = E.empId
AND C.rating <> ’GOOD’);

**Options:**

A. Names of all the employees with at least one of their customers having a ‘GOOD’ rating.
B. Names of all the employees with at most one of their customers having a ‘GOOD’ rating.
C. Names of all the employees with none of their customers having a ‘GOOD’ rating.
D. Names of all the employees with all their customers having a ‘GOOD’ rating.

**Type:** MCQ

**Answer:** VERIFICATION REQUIRED

**Source:** GATE 2014 CS SET-3, `12-PYQ/2014/set-03/question-paper.pdf`

---

## 2013

### Q.15

**Paper:** GATE 2013 CS Booklet A

**Question:**

An index is clustered, if

**Options:**

A. it is on a set of fields that form a candidate key.
B. it is on a set of fields that include the primary key.
C. the data records of the file are organized in the same order as the data entries of the index.
D. the data records of the file are organized not in the same order as the data entries of the index.

**Type:** MCQ

**Answer:** VERIFICATION REQUIRED

**Source:** GATE 2013 CS Booklet A, `12-PYQ/2013/set-01/question-paper.pdf`

---

### Q.54

**Paper:** GATE 2013 CS Booklet A

**Question:**

How many candidate keys does the relation R have?

**Options:**

A. 3
B. 4
C. 5
D. 6

**Type:** MCQ

**Answer:** VERIFICATION REQUIRED

**Source:** GATE 2013 CS Booklet A, `12-PYQ/2013/set-01/question-paper.pdf`

---

### Q.11

**Paper:** GATE 2013 CS Booklet B

**Question:**

An index is clustered, if

**Options:**

A. it is on a set of fields that form a candidate key.
B. it is on a set of fields that include the primary key.
C. the data records of the file are organized in the same order as the data entries of the index.
D. the data records of the file are organized not in the same order as the data entries of the index.

**Type:** MCQ

**Answer:** VERIFICATION REQUIRED

**Source:** GATE 2013 CS Booklet B, `12-PYQ/2013/set-02/question-paper.pdf`

---

### Q.52

**Paper:** GATE 2013 CS Booklet B

**Question:**

How many candidate keys does the relation R have?

**Options:**

A. 3
B. 4
C. 5
D. 6

**Type:** MCQ

**Answer:** VERIFICATION REQUIRED

**Source:** GATE 2013 CS Booklet B, `12-PYQ/2013/set-02/question-paper.pdf`

---

### Q.23

**Paper:** GATE 2013 CS Booklet C

**Question:**

An index is clustered, if

**Options:**

A. it is on a set of fields that form a candidate key.
B. it is on a set of fields that include the primary key.
C. the data records of the file are organized in the same order as the data entries of the index.
D. the data records of the file are organized not in the same order as the data entries of the index.

**Type:** MCQ

**Answer:** VERIFICATION REQUIRED

**Source:** GATE 2013 CS Booklet C, `12-PYQ/2013/set-03/question-paper.pdf`

---

### Q.54

**Paper:** GATE 2013 CS Booklet C

**Question:**

How many candidate keys does the relation R have?

**Options:**

A. 3
B. 4
C. 5
D. 6

**Type:** MCQ

**Answer:** VERIFICATION REQUIRED

**Source:** GATE 2013 CS Booklet C, `12-PYQ/2013/set-03/question-paper.pdf`

---

### Q.3

**Paper:** GATE 2013 CS Booklet D

**Question:**

An index is clustered, if

**Options:**

A. it is on a set of fields that form a candidate key.
B. it is on a set of fields that include the primary key.
C. the data records of the file are organized in the same order as the data entries of the index.
D. the data records of the file are organized not in the same order as the data entries of the index.

**Type:** MCQ

**Answer:** VERIFICATION REQUIRED

**Source:** GATE 2013 CS Booklet D, `12-PYQ/2013/set-04/question-paper.pdf`

---

### Q.52

**Paper:** GATE 2013 CS Booklet D

**Question:**

How many candidate keys does the relation R have?

**Options:**

A. 3
B. 4
C. 5
D. 6

**Type:** MCQ

**Answer:** VERIFICATION REQUIRED

**Source:** GATE 2013 CS Booklet D, `12-PYQ/2013/set-04/question-paper.pdf`

---

## 2012

### Q.43

**Paper:** GATE 2012 CS Booklet A

**Question:**

Suppose R_{1}(A, B) and R_{2}(C, D) are two relation schemas. Let  r_{1} and  r_{2} be the corresponding
relation instances. B is a foreign key that refers to C in R_{2}. If data in r_{1} and r_{2} satisfy referential
integrity constraints, which of the following is ALWAYS TRUE?

**Options:**

A. ∏_{B}(r_{1}) − ∏_{C}(r_{2}) = ∅
B. ∏_{C}(r_{2}) − ∏_{B}(r_{1}) = ∅
C. ∏_{B}(r_{1}) = ∏_{C}(r_{2})
D. ∏_{B}(r_{1}) − ∏_{C}(r_{2}) ≠ ∅ CS-A 10/20 2012 COMPUTER SCIENCE & INFORMATION TECH. – CS

**Type:** MCQ

**Answer:** VERIFICATION REQUIRED

**Source:** GATE 2012 CS Booklet A, `12-PYQ/2012/question-paper.pdf`

---

## 2011

### Q.12

**Paper:** GATE 2011 CS Booklet A

**Question:**

Consider a relational table with a single record for each registered student with the following
attributes.
1. Registration_Num: Unique registration number of each registered student
2. UID: Unique identity number, unique at the national level for each citizen
3. BankAccount_Num: Unique account number at the bank. A student can have multiple
accounts or joint accounts. This attribute stores the primary account number.
4. Name: Name of the student
5. Hostel_Room: Room number of the hostel
Which of the following options is INCORRECT?

**Options:**

A. BankAccount_Num is a candidate key
B. Registration_Num can be a primary key
C. UID is a candidate key if all students are from the same country
D. If S is a superkey such that SNUID is NULL then SUUID is also a superkey

**Type:** MCQ

**Answer:** VERIFICATION REQUIRED

**Source:** GATE 2011 CS Booklet A, `12-PYQ/2011/question-paper.pdf`

---
