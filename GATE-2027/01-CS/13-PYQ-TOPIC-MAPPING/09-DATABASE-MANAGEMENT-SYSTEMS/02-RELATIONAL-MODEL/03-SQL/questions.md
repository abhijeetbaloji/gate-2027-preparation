# GATE PYQs

## 2026

### Q.56

**Paper:** GATE 2026 CS-1 (forenoon)

**Question:**

An ISP having an address block 202.16.0.0/15 assigns a block of 6000 IP addresses
to a client, using the classless internet domain routing (CIDR) super-netting
approach. Which of the following address blocks can be assigned by the ISP?

**Options:**

A. 202.16.0.0/19
B. 202.17.64.0/19
C. 202.16.32.0/19
D. 202.17.24.0/19

**Type:** MCQ

**Answer:** VERIFICATION REQUIRED

**Source:** GATE 2026 CS-1 (forenoon), `12-PYQ/2026/set-01/question-paper.pdf`

---

## 2025

### Q.39

**Paper:** GATE 2025 CS-1

**Question:**

Consider two relations describing 𝑡𝑒𝑎𝑚𝑠 and 𝑝𝑙𝑎𝑦𝑒𝑟𝑠 in a sports league:
•  𝑡𝑒𝑎𝑚𝑠(𝑡𝑖𝑑, 𝑡𝑛𝑎𝑚𝑒): 𝑡𝑖𝑑, 𝑡𝑛𝑎𝑚e are team-id and team-name, respectively
•  𝑝𝑙𝑎𝑦𝑒𝑟𝑠(𝑝𝑖𝑑, 𝑝𝑛𝑎𝑚𝑒, 𝑡𝑖𝑑):  𝑝𝑖𝑑,  𝑝𝑛𝑎𝑚𝑒, and 𝑡𝑖𝑑 denote player-id, player-
name and the team-id of the player, respectively
Which ONE of the following tuple relational calculus queries returns the name of the
players who play for the team having 𝑡𝑛𝑎𝑚𝑒 as ′𝑀𝐼′?

**Options:**

A. { 𝑝. 𝑝𝑛𝑎𝑚𝑒 | 𝑝∈𝑝𝑙𝑎𝑦𝑒𝑟𝑠∧∃𝑡 (𝑡∈𝑡𝑒𝑎𝑚𝑠∧𝑝. 𝑡𝑖𝑑= 𝑡. 𝑡𝑖𝑑∧𝑡. 𝑡𝑛𝑎𝑚𝑒= ′𝑀𝐼′)}
B. { 𝑝. 𝑝𝑛𝑎𝑚𝑒 | 𝑝∈𝑡𝑒𝑎𝑚𝑠∧∃𝑡 (𝑡∈𝑝𝑙𝑎𝑦𝑒𝑟𝑠∧𝑝. 𝑡𝑖𝑑= 𝑡. 𝑡𝑖𝑑∧𝑡. 𝑡𝑛𝑎𝑚𝑒= ′𝑀𝐼′)}
C. { 𝑝. 𝑝𝑛𝑎𝑚𝑒 | 𝑝∈𝑝𝑙𝑎𝑦𝑒𝑟𝑠∧∃𝑡 (𝑡∈𝑡𝑒𝑎𝑚𝑠∧𝑡. 𝑡𝑛𝑎𝑚𝑒= ′𝑀𝐼′)}
D. { 𝑝. 𝑝𝑛𝑎𝑚𝑒 | 𝑝∈𝑡𝑒𝑎𝑚𝑠∧∃𝑡 (𝑡∈𝑝𝑙𝑎𝑦𝑒𝑟𝑠∧𝑡. 𝑡𝑛𝑎𝑚𝑒= ′𝑀𝐼′)}

**Type:** MCQ

**Answer:** VERIFICATION REQUIRED

**Source:** GATE 2025 CS-1, `12-PYQ/2025/set-01/question-paper.pdf`

---

### Q.55

**Paper:** GATE 2025 CS-1

**Question:**

Consider the following database tables of a sports league.
player(pid,pname,age)  team(tid,tname,city,cid)
coach(cid,cname)  members(pid,tid)
An instance of the table and an SQL query are given.
player  coach  team  members
SELECT MIN(P.age)
FROM player P
WHERE P.pid IN (
SELECT M.pid
FROM team T, coach C, members M
WHERE C.cname = 'Mark'
AND T.cid = C.cid
AND M.tid = T.tid
)
The value returned by the given SQL query is ______ . (Answer in integer)

**Options:**

The paper does not print options for this numerical-answer question.

**Type:** NAT

**Answer:** VERIFICATION REQUIRED

**Source:** GATE 2025 CS-1, `12-PYQ/2025/set-01/question-paper.pdf`

---

### Q.54

**Paper:** GATE 2025 CS-2

**Question:**

Consider the following relational schema:
Students (rollno: integer, name: string, age: integer, cgpa: real)
Courses (courseno: integer, cname: string, credits: integer)
Enrolled (rollno: integer, courseno: integer, grade: string)
Which of the following options is/are correct SQL query/queries to retrieve the
names of the students enrolled in course number (i.e., courseno) 1470?

**Options:**

A. SELECT S.name FROM Students S WHERE EXISTS (SELECT * FROM Enrolled E WHERE E.courseno = 1470 AND E.rollno = S.rollno);
B. SELECT S.name FROM Students S WHERE SIZEOF (SELECT * FROM Enrolled E WHERE E.courseno = 1470 AND E.rollno = S.rollno) > 0;
C. SELECT S.name FROM Students S WHERE 0 < (SELECT COUNT(*) FROM Enrolled E WHERE E.courseno = 1470 AND E.rollno = S.rollno);
D. SELECT S.name FROM Students S NATURAL JOIN Enrolled E WHERE E.courseno = 1470;

**Type:** MCQ

**Answer:** VERIFICATION REQUIRED

**Source:** GATE 2025 CS-2, `12-PYQ/2025/set-02/question-paper.pdf`

---

## 2023

### Q.61

**Paper:** GATE 2023 CS

**Question:**

Consider the following table named Student in a relational database. The primary
key of this table is rollNum.
Student
rollNum name  gender marks
1  Naman  M  62
2  Aliya  F  70
3  Aliya  F  80
4  James  M  82
5  Swati  F  65
The SQL query below is executed on this database.
SELECT *
FROM Student
WHERE gender = ‘F’ AND
marks > 65;
The number of rows returned by the query is  .

**Options:**

The paper does not print options for this numerical-answer question.

**Type:** NAT

**Answer:** VERIFICATION REQUIRED

**Source:** GATE 2023 CS, `12-PYQ/2023/question-paper.pdf`

---

## 2022

### Q.56

**Paper:** GATE 2022 CS

**Question:**

Consider the relational database with the following four schemas and their
respective instances.
Student(sNo, sName, dNo) Dept(dNo, dName)
Course(cNo, cName, dNo) Register(sNo, cNo)
SQL Query:
SELECT * FROM Student AS S WHERE NOT EXIST
(SELECT cNo FROM Course WHERE dNo = “D01”
EXCEPT
SELECT cNo FROM Register WHERE sNo = S.sNo)
The number of rows returned by the above SQL query is___________.

**Options:**

The paper does not print options for this numerical-answer question.

**Type:** NAT

**Answer:** VERIFICATION REQUIRED

**Source:** GATE 2022 CS, `12-PYQ/2022/question-paper.pdf`

---

## 2021

### Q.7

**Paper:** GATE 2021 CS Set-2

**Question:**

Consider the three-way handshake mechanism followed during TCP connection es-
tablishment between hosts P and Q. Let X and Y be two random 32-bit starting
sequence numbers chosen by P and Q respectively. Suppose P sends a TCP connec-
tion request message to Q with a TCP segment having SYN bit = 1, SEQ number
= X. and ACK bit = 0. Suppose Q accepts the connection request. Which one of
the following choices represents the information present in the TCP segment header
that is sent by Q to P?

**Options:**

A. SYN bit = 1, SEQ number = X+1, ACK bit = 0, ACK number = Y, FIN bit = 0
B. SYN bit = 0, SEQ number = X+1, ACK bit = 0, ACK number = Y, FIN bit =1
C. | SYN bit = 1, SEQ number = Y, ACK bit = 1, ACK number = X+1, FIN bit = 0
D. SYN bit = 1, SEQ number = Y, ACK bit = 1, ACK number = X, FIN bit = 0 GATE Graduate Aptitude Test in Engineering 2021 2021 Organising Institute - IIT Bombay

**Type:** MCQ

**Answer:** VERIFICATION REQUIRED

**Source:** GATE 2021 CS Set-2, `12-PYQ/2021/set-02/question-paper.pdf`

---

### Q.31

**Paper:** GATE 2021 CS Set-2

**Question:**

The relation scheme given below is used to store information about the employees of
a company, where empId is the key and deptId indicates the department to which
the employee is assigned. Each employee is assigned to exactly one department.
emp (empId, name, gender, salary, deptId)
Consider the following SQL query:
select deptId, count (*)
from emp
where gender = "female" and salary > (select avg(salary) from emp)
group by deptId;
The above query gives, for each department in the company, the number of
female employees whose salary is greater than the average salary of

**Options:**

A. employees in the department.
B. employees in the company.
C. female employees in the department.
D. female employees in the company. GATE Graduate Aptitude Test in Engineering 2021 2021 Organising Institute - IIT Bombay

**Type:** MCQ

**Answer:** VERIFICATION REQUIRED

**Source:** GATE 2021 CS Set-2, `12-PYQ/2021/set-02/question-paper.pdf`

---

### Q.34

**Paper:** GATE 2021 CS Set-2

**Question:**

Consider the cyclic redundancy check (CRC) based error detecting scheme having
he genratorpolynomial3A1.Suppose themesse mgn
is to be transmitted. Check bits cocico are appended at the end of the message by
the transmitter using the above CRC scheme. The transmitted bit string is denoted
by mamgmamm. The value of the checkbit sequence cac_co is

**Options:**

A. 101
B. 110
C. 100
D. 111 GATE Graduate Aptitude Test in Engineering 2021 2021 Organising Institute - IIT Bombay

**Type:** MCQ

**Answer:** VERIFICATION REQUIRED

**Source:** GATE 2021 CS Set-2, `12-PYQ/2021/set-02/question-paper.pdf`

---

## 2018

### Q.12

**Paper:** GATE 2018 CS

**Question:**

Consider the following two tables and four queries in SQL.
Book (isbn, bname), Stock (isbn, copies)
Query 1:  SELECT B.isbn, S.copies
FROM Book B INNER JOIN Stock S
ON B.isbn = S.isbn;
Query 2:  SELECT B.isbn, S.copies
FROM Book B LEFT OUTER JOIN Stock S
ON B.isbn = S.isbn;
Query 3:  SELECT B.isbn, S.copies
FROM Book B RIGHT OUTER JOIN Stock S
ON B.isbn = S.isbn;
Query 4:  SELECT B.isbn, S.copies
FROM Book B FULL OUTER JOIN Stock S
ON B.isbn = S.isbn;
Which one of the queries above is certain to have an output that is a superset of the outputs
of the other three queries?

**Options:**

A. Query 1
B. Query 2
C. Query 3
D. Query 4

**Type:** MCQ

**Answer:** VERIFICATION REQUIRED

**Source:** GATE 2018 CS, `12-PYQ/2018/question-paper.pdf`

---

### Q.44

**Paper:** GATE 2018 CS

**Question:**

Consider Guwahati (G) and Delhi (D) whose temperatures can be classified as high (𝐻),
medium (𝑀) and low (𝐿). Let  𝑃(𝐻_{𝐺}) denote the probability that Guwahati has high
temperature. Similarly,  𝑃(𝑀_{𝐺}) and  𝑃(𝐿_{𝐺}) denotes the probability of Guwahati having
medium and low temperatures respectively. Similarly, we use 𝑃(𝐻_{𝐷}), 𝑃(𝑀_{𝐷}) and 𝑃(𝐿_{𝐷}) for
Delhi.
The following table gives the conditional probabilities for Delhi’s temperature given
Guwahati’s temperature.
𝐻_{𝐷}  𝑀_{𝐷}  𝐿_{𝐷}
𝐻_{𝐺}  0.40  0.48  0.12
𝑀_{𝐺}  0.10  0.65  0.25
𝐿_{𝐺}  0.01  0.50  0.49
Consider the first row in the table above. The first entry denotes that if Guwahati has high
temperature (𝐻_{𝐺}) then the probability of Delhi also having a high temperature (𝐻_{𝐷}) is 0.40;
i.e.,  𝑃(𝐻_{𝐷}|𝐻_{𝐺}) = 0.40. Similarly, the next two entries are  𝑃(𝑀_{𝐷}|𝐻_{𝐺}) = 0.48 and
𝑃(𝐿_{𝐷}|𝐻_{𝐺}) = 0.12. Similarly for the other rows.
If it is known that  𝑃(𝐻_{𝐺}) = 0.2,  𝑃(𝑀_{𝐺}) = 0.5, and  𝑃(𝐿_{𝐺}) = 0.3, then the probability
(correct to two decimal places) that Guwahati has high temperature given that Delhi has high
temperature is _______.

**Options:**

The paper does not print options for this numerical-answer question.

**Type:** NAT

**Answer:** VERIFICATION REQUIRED

**Source:** GATE 2018 CS, `12-PYQ/2018/question-paper.pdf`

---

## 2017

### Q.46

**Paper:** GATE 2017 CS Session 2

**Question:**

Correct: 2 Wrong : 0
Consider the following database table named top_scorer.
top scorer
player country goals
Klose Germany 16
Ronaldo Brazil 15
G Müller Germany 14
Fontaine France 13
Pelé Brazil 12
Klinsmann Germany 11
Kocsis Hungary 11
Batistuta Argentina 10
Cubillas Peru 10
Lato Poland 10
Lineker England 10
T Müller Gernany 10
Rahn Gernany 10
Consider the following SQL query:
SELECT ta.Player FROM toP_ scorer AS ta
WHERE ta.goals >ALL (SELECT tb.goals
FROM tOP_ scorer AS tb
WHERE tb.country = 'Spain')
AND ta.goals >ANY(SELECT tc.goals
FROM toP_ scorer AS tc
WHERE tc.country = 'Germany')
The number of tuples returned by the above SQL query is

**Options:**

The paper does not print options for this numerical-answer question.

**Type:** NAT

**Answer:** VERIFICATION REQUIRED

**Source:** GATE 2017 CS Session 2, `12-PYQ/2017/set-02/question-paper.pdf`

---

### Q.65

**Paper:** GATE 2017 CS Session 2

**Question:**

Correct : 2 Wrong:-0.66
An air pressure contour line joins locations in a region having the same atmospheric pressure. The
following is an air pressure contour plot of a geographical region. Contour lines are shown at 0.05
bar intervals in this plot.
0.65
01
0.9
0.8
08- 0.15
2 km
If the possibility of a thunderstorm is given by how fast air pressure rises or drops over a region.
which of the following regions is most likely to have a thunderstorm?

**Options:**

A. P
B. Q
C. R
D. S

**Type:** MCQ

**Answer:** VERIFICATION REQUIRED

**Source:** GATE 2017 CS Session 2, `12-PYQ/2017/set-02/question-paper.pdf`

---

## 2016

### Q.39

**Paper:** GATE 2016 CS-1

**Question:**

Let G be a complete undirected graph on 4 vertices, having 6 edges with weights being 1, 2,
3, 4, 5, and 6. The maximum possible weight that a minimum weight spanning tree of G can
have is  .
CS(Set A)  12/17

**Options:**

The paper does not print options for this numerical-answer question.

**Type:** NAT

**Answer:** VERIFICATION REQUIRED

**Source:** GATE 2016 CS-1, `12-PYQ/2016/set-01/question-paper.pdf`

---

### Q.52

**Paper:** GATE 2016 CS-2

**Question:**

Consider the following database table named water_schemes :
water_schemes
scheme_no district_name capacity
1  Ajmer  20
1  Bikaner  10
2  Bikaner  10
3  Bikaner  20
1  Churu  10
2  Churu  20
1  Dungargarh  10
The number of tuples returned by the following SQL query is  .
with total(name, capacity) as
select district_name, sum(capacity)
from water_schemes
group by district_name
with total_avg(capacity) as
select avg(capacity)
from total
select name
from total, total_avg
where total.capacity ≥ total_avg.capacity

**Options:**

The paper does not print options for this numerical-answer question.

**Type:** NAT

**Answer:** VERIFICATION REQUIRED

**Source:** GATE 2016 CS-2, `12-PYQ/2016/set-02/question-paper.pdf`

---

## 2015

### Q.31

**Paper:** GATE 2015 CS, 7 February Shift 1

**Question:**

SELECT operation in SQL is equivalent to

**Options:**

A. the selection operation in relational algebra
B. the selection operation in relational algebra, except that SELECT in SQL retains duplicates
C. the projection operation in relational algebra
D. the projection operation in relational algebra, except that SELECT in SQL retains duplicates 2 % B 3. % C 4. VD

**Type:** MCQ

**Answer:** VERIFICATION REQUIRED

**Source:** GATE 2015 CS, 7 February Shift 1, `12-PYQ/2015/set-01/question-paper.pdf`

---

### Q.61

**Paper:** GATE 2015 CS, 7 February Shift 1

**Question:**

Consider the following relations:
Student Performance
Roll No Student Name Roll No Course Marks
1 Raj 1 Math 80
2 Rohit 1 English
3 Raj 2 Math
3 English
2 Physics
3 Math
Consider the following SQL query.
SELECT S.Student_Name, sum (P.Marks)
FROM Student S, Pertormance P
WHERE S.Ro11 - No = P.Rol1 _NO
GROUP BY S.Student _Name
The number of rows that will be returned by the SQL query is
Correct Answer :

**Options:**

The paper does not print options for this numerical-answer question.

**Type:** NAT

**Answer:** VERIFICATION REQUIRED

**Source:** GATE 2015 CS, 7 February Shift 1, `12-PYQ/2015/set-01/question-paper.pdf`

---

### Q.25

**Paper:** GATE 2015 CS, 8 February Shift 1

**Question:**

The number of 4 digit numbers having their digits in non-decreasing order (from left to right)
constructed by using the digits belonging to the set (1, 2, 3) is
Correct Answer :

**Options:**

The paper does not print options for this numerical-answer question.

**Type:** NAT

**Answer:** VERIFICATION REQUIRED

**Source:** GATE 2015 CS, 8 February Shift 1, `12-PYQ/2015/set-03/question-paper.pdf`

---

### Q.29

**Paper:** GATE 2015 CS, 8 February Shift 1

**Question:**

Consider the following relation
Cinema(theater, address, capacity)
Which of the following options will be needed at the end of the SQL query
SELECT P1.address
FROM Cinema P1
such that it always finds the addresses of theaters with maximum capacity?

**Options:**

A. WHERE P1.capacity >= All (select P2.capacity from Cinema P2)
B. WHERE P1.capacity >= Any (select P2.capacity from Cinema P2)
C. WHERE P1.capacity > All (select max(P2.capacity) from Cinema P2)
D. WHERE P1.capacity > Any (select max(P2.capacity) from Cinema P2)

**Type:** MCQ

**Answer:** VERIFICATION REQUIRED

**Source:** GATE 2015 CS, 8 February Shift 1, `12-PYQ/2015/set-03/question-paper.pdf`

---

## 2014

### Q.12

**Paper:** GATE 2014 CS SET-1

**Question:**

Conssider a rootedd ݊  node binarry tree repressented using ppointers.  Thee best upper bbound on the time
CS01 (GATE 2014)requiired to determmine the nummber of subtreees having exxactly 4 nodees is  (݊^{௔} logg^{௕} ).  Thenn the
valuee of  + 10ܾ  is ___________.

**Options:**

The paper does not print options for this numerical-answer question.

**Type:** NAT

**Answer:** VERIFICATION REQUIRED

**Source:** GATE 2014 CS SET-1, `12-PYQ/2014/set-01/question-paper.pdf`

---

### Q.37

**Paper:** GATE 2014 CS SET-1

**Question:**

There are 5 bags labeled 1 to 5.  All the coins in a given bag have the same weight.  Some bags
have coins of weight 10 gm, others have coins of weight 11 gm.  I pick 1, 2, 4, 8, 16 coins
respectively from bags 1 to 5.  Their total weight comes out to 323 gm.  Then the product of the
labels of the bags having 11 gm coins is ___.

**Options:**

The paper does not print options for this numerical-answer question.

**Type:** NAT

**Answer:** VERIFICATION REQUIRED

**Source:** GATE 2014 CS SET-1, `12-PYQ/2014/set-01/question-paper.pdf`

---

### Q.52

**Paper:** GATE 2014 CS SET-1

**Question:**

An ordered ݊ -tuple (݀_{ଵ},_{ଶ}, … ,_{௡}) with ݀_{ଵ} ≥_{ଶ} ≥⋯≥_{௡} is called graphic if there exists a simple
undirected graph with ݊  vertices having degrees _{ଵ},_{ଶ}, … ,_{௡} respectively. Which of the following
6-tuples is NOT graphic?

**Options:**

A. (1, 1, 1, 1, 1, 1)
B. (2, 2, 2, 2, 2, 2)
C. (3, 3, 3, 1, 0, 0)
D. (3, 2, 1, 1, 1, 0)

**Type:** MCQ

**Answer:** VERIFICATION REQUIRED

**Source:** GATE 2014 CS SET-1, `12-PYQ/2014/set-01/question-paper.pdf`

---

### Q.54

**Paper:** GATE 2014 CS SET-1

**Question:**

Given the following schema:
employees(emp-id, first-name, last-name, hire-date,
dept-id, salary)
departments(dept-id, dept-name, manager-id, location-id)
You want to display the last names and hire dates of all latest hires in their respective departments
in the location ID 1700. You issue the following query:
CS01 (GATE 2014)
SQL>SELECT last-name, hire-date
FROM employees
WHERE (dept-id, hire-date) IN
(SELECT dept-id, MAX(hire-date)
FROM employees JOIN departments USING(dept-id)
WHERE location-id = 1700
GROUP BY dept-id);
What is the outcome?

**Options:**

A. It executes but does not give the correct result.
B. It executes and gives the correct result.
C. It generates an error because of pairwise comparison.
D. It generates an error because the GROUP BY clause cannot be used with table joins in a sub- query.

**Type:** MCQ

**Answer:** VERIFICATION REQUIRED

**Source:** GATE 2014 CS SET-1, `12-PYQ/2014/set-01/question-paper.pdf`

---

### Q.54

**Paper:** GATE 2014 CS SET-2

**Question:**

SQL allows duplicate tuples in relations, and correspondingly defines the multiplicity of tuples in
the result of joins. Which one of the following queries always gives the same answer as the nested
query shown below:
select * from R where a in (select S.a from S)

**Options:**

A. select R.* from R, S where R.a=S.a
B. select distinct R.* from R,S where R.a=S.a
C. select R.* from R,(select distinct a from S) as S1 where R.a=S1.a
D. select R.* from R,S where R.a=S.a and is unique R

**Type:** MCQ

**Answer:** VERIFICATION REQUIRED

**Source:** GATE 2014 CS SET-2, `12-PYQ/2014/set-02/question-paper.pdf`

---

## 2013

### Q.29

**Paper:** GATE 2013 CS Booklet A

**Question:**

Consider a hard disk with 16 recording surfaces (0-15) having 16384 cylinders (0-16383) and each
cylinder contains 64 sectors (0-63). Data storage capacity in each sector is 512 bytes. Data are
organized cylinder-wise and the addressing format is <cylinder no., surface no., sector no.>. A file
of size 42797 KB is stored in the disk and the starting disk location of the file is <1200, 9, 40>.
What is the cylinder number of the last sector of the file, if it is stored in a contiguous manner?

**Options:**

A. 1281
B. 1282
C. 1283
D. 1284

**Type:** MCQ

**Answer:** VERIFICATION REQUIRED

**Source:** GATE 2013 CS Booklet A, `12-PYQ/2013/set-01/question-paper.pdf`

---

### Q.44

**Paper:** GATE 2013 CS Booklet B

**Question:**

Consider a hard disk with 16 recording surfaces (0-15) having 16384 cylinders (0-16383) and each
cylinder contains 64 sectors (0-63). Data storage capacity in each sector is 512 bytes. Data are
organized cylinder-wise and the addressing format is <cylinder no., surface no., sector no.>. A file
of size 42797 KB is stored in the disk and the starting disk location of the file is <1200, 9, 40>.
What is the cylinder number of the last sector of the file, if it is stored in a contiguous manner?

**Options:**

A. 1281
B. 1282
C. 1283
D. 1284

**Type:** MCQ

**Answer:** VERIFICATION REQUIRED

**Source:** GATE 2013 CS Booklet B, `12-PYQ/2013/set-02/question-paper.pdf`

---

### Q.33

**Paper:** GATE 2013 CS Booklet C

**Question:**

Consider a hard disk with 16 recording surfaces (0-15) having 16384 cylinders (0-16383) and each
cylinder contains 64 sectors (0-63). Data storage capacity in each sector is 512 bytes. Data are
organized cylinder-wise and the addressing format is <cylinder no., surface no., sector no.>. A file
of size 42797 KB is stored in the disk and the starting disk location of the file is <1200, 9, 40>.
What is the cylinder number of the last sector of the file, if it is stored in a contiguous manner?

**Options:**

A. 1281
B. 1282
C. 1283
D. 1284

**Type:** MCQ

**Answer:** VERIFICATION REQUIRED

**Source:** GATE 2013 CS Booklet C, `12-PYQ/2013/set-03/question-paper.pdf`

---

### Q.40

**Paper:** GATE 2013 CS Booklet D

**Question:**

Consider a hard disk with 16 recording surfaces (0-15) having 16384 cylinders (0-16383) and each
cylinder contains 64 sectors (0-63). Data storage capacity in each sector is 512 bytes. Data are
organized cylinder-wise and the addressing format is <cylinder no., surface no., sector no.>. A file
of size 42797 KB is stored in the disk and the starting disk location of the file is <1200, 9, 40>.
What is the cylinder number of the last sector of the file, if it is stored in a contiguous manner?

**Options:**

A. 1281
B. 1282
C. 1283
D. 1284

**Type:** MCQ

**Answer:** VERIFICATION REQUIRED

**Source:** GATE 2013 CS Booklet D, `12-PYQ/2013/set-04/question-paper.pdf`

---

## 2012

### Q.15

**Paper:** GATE 2012 CS Booklet A

**Question:**

Which of the following statements are TRUE about an SQL query?
P : An SQL query can contain a HAVING clause even if it does not have a GROUP BY clause
Q : An SQL query can contain a HAVING clause only if it has a GROUP BY clause
R : All attributes used in the GROUP BY clause must appear in the SELECT clause
S : Not all attributes used in the GROUP BY clause need to appear in the SELECT clause

**Options:**

A. P and R
B. P and S
C. Q and R
D. Q and S

**Type:** MCQ

**Answer:** VERIFICATION REQUIRED

**Source:** GATE 2012 CS Booklet A, `12-PYQ/2012/question-paper.pdf`

---

## 2010

### Q.19

**Paper:** GATE 2010 CS

**Question:**

A relational schema for a train reservation dalabase is given below:.
Passenger (pid, prame, age)
Reservation(piá, class, tid)
Tuble: Passenger pia pname Tuble: Reservaticn
Age pid class tid
'Sachin' 65 'AC 8200
Rahut" 66 •AC* 8201
2 'Sourav" 67 820L
3 'Anil' 69 'AC 8203
'SC" 8204
3 'AC 8202
Whar pids are returned by the fallowing SQL query for the above instance of tha tables?
SELECT pid
FROM Reservation
WHERE class = 'AC AND
EXISTS (SELECT *
FROM Passenger
WHERE agc > 65 AND
Passenger.pid = Reservation-pid)
(4)1.0 (By1.2 (C)1.3 (D) 1.5
2010 cS

**Options:**

The paper does not print options for this numerical-answer question.

**Type:** NAT

**Answer:** VERIFICATION REQUIRED

**Source:** GATE 2010 CS, `12-PYQ/2010/question-paper.pdf`

---

## 2007

### Q.24

**Paper:** GATE 2007 CS

**Question:**

Suppose we uniformly and randomly select a permutation from the 20! permutations
of 1,2,3,...,20. What is the probability that 2 appears at an earlier position than any
other even number in the selected permutation?

**Options:**

A. 2
B. 10
C. 9! 20!
D. None of the above.

**Type:** MCQ

**Answer:** VERIFICATION REQUIRED

**Source:** GATE 2007 CS, `12-PYQ/2007/question-paper.pdf`

---

### Q.61

**Paper:** GATE 2007 CS

**Question:**

Consider the table employee(empld, name, department, salary) and the two queries
Q1, Q2 below. Assuming that department 5 has more than one employee, and we want
to find the employees who get higher salary than anyone in the department 5, which
one of the statements is TRUE for any arbitrary employee table?
Qi: Select e.empld
From employee e
Where not exists
(Select * From employee s Where s.department = "5" and s.salary >= e.salary)
O2: Select e.empld
From employee e
Where e.salary > Any
( Select distinct salary From employee s Where s.department = "5")

**Options:**

A. Qi is the correct query.
B. Q2 is the correct query.
C. Both Qi and Q2 produce the same answer.
D. Neither Qi nor Q2 is the correct query.

**Type:** MCQ

**Answer:** VERIFICATION REQUIRED

**Source:** GATE 2007 CS, `12-PYQ/2007/question-paper.pdf`

---
