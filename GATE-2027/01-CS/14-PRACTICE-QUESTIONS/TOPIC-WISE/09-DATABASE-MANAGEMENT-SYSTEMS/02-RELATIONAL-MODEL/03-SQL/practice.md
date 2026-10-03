# SQL — Practice Questions

Original practice for GATE CS. These questions are not from any GATE paper. Attempt the questions before reading the solutions.

The stall database below is the instance for every question that names these tables. Comparisons use three-valued logic. A `WHERE` or `HAVING` clause keeps a row only when its predicate is TRUE.

customers(cid, cname, city)

| cid | cname | city |
|-----|-------|------|
| C1 | Nia | Surat |
| C2 | Kabir | Surat |
| C3 | Hana | NULL |
| C4 | Dev | Agra |
| C5 | Iris | Agra |

orders(oid, cid, amt, status)

| oid | cid | amt | status |
|-----|-----|-----|--------|
| O1 | C1 | 200 | paid |
| O2 | C1 | 150 | paid |
| O3 | C2 | NULL | open |
| O4 | C4 | 80 | paid |
| O5 | C4 | 120 | void |
| O6 | C3 | 50 | paid |
| O7 | NULL | 90 | paid |

items(iid, oid, qty, price)

| iid | oid | qty | price |
|-----|-----|-----|-------|
| I1 | O1 | 2 | 40 |
| I2 | O1 | 1 | 120 |
| I3 | O2 | 3 | 50 |
| I4 | O4 | 4 | 20 |
| I5 | O6 | 1 | NULL |

## Level 1 — Conceptual

## Q1 — MCQ

In the logical processing order of a single SELECT statement, which sequence is correct?

A. FROM, WHERE, GROUP BY, HAVING, SELECT, ORDER BY
B. FROM, SELECT, WHERE, GROUP BY, HAVING, ORDER BY
C. SELECT, FROM, WHERE, HAVING, GROUP BY, ORDER BY
D. FROM, GROUP BY, WHERE, SELECT, HAVING, ORDER BY

---

## Q2 — MCQ

Which statement about aggregate functions and NULL is true?

A. COUNT(*) and COUNT(amt) always return the same value on orders
B. COUNT(amt) ignores rows in which amt is NULL
C. SUM(amt) treats a NULL amt as 0
D. AVG(amt) divides the sum by COUNT(*), so NULL amounts change the denominator

---

## Q3 — MCQ

Which statement about joins is true?

A. An inner join keeps every customer, including a customer with no order
B. An inner join of customers and orders on cid drops both unmatched customers and orders whose cid is NULL
C. A left outer join of customers to orders drops customers who have no order
D. A predicate in the WHERE clause after a left outer join cannot eliminate the padded rows

---

## Q4 — MSQ

Which statements are true of the stall database? Select all that apply.

A. The comparison NULL = NULL is not TRUE
B. Hana's city fails both city = 'Agra' and city <> 'Agra'
C. COUNT(city) on customers counts Hana
D. The comparison amt > 100 is UNKNOWN for order O3

---

## Q5 — MCQ

A condition on an aggregate of each group, such as "groups whose COUNT(*) is at least 2", is written

A. in the WHERE clause, because WHERE runs before grouping
B. in the HAVING clause, because HAVING runs after grouping
C. only in the SELECT list, which filters rows
D. in ORDER BY, because ordering decides which groups survive

---

## Level 2 — Standard GATE Style

## Q6 — NAT

How many rows does this query return?

```sql
SELECT oid FROM orders WHERE amt > 100
```

______

---

## Q7 — NAT

What is the value of `SELECT COUNT(amt) FROM orders`? ______

---

## Q8 — MCQ

How many rows does this query return?

```sql
SELECT cid FROM customers WHERE city = 'Agra' OR city <> 'Agra'
```

A. 3
B. 4
C. 5
D. 7

---

## Q9 — NAT

How many rows does this query return?

```sql
SELECT c.cid, o.oid
FROM customers c INNER JOIN orders o ON c.cid = o.cid
```

______

---

## Q10 — MCQ

What is `SELECT AVG(amt) FROM orders`?

A. 98.6
B. 115
C. 120
D. 570

---

## Q11 — MSQ

Which of these statements are illegal in standard SQL? Select all that apply.

A. `SELECT city FROM customers WHERE COUNT(*) > 1`
B. `SELECT status, COUNT(*) FROM orders GROUP BY status HAVING COUNT(*) >= 1`
C. `SELECT amt, COUNT(*) FROM orders GROUP BY status`
D. `SELECT COUNT(*) FROM orders HAVING COUNT(*) > 0`

---

## Level 3 — Multi-Step

## Q12 — NAT

What is `SELECT SUM(amt) FROM orders WHERE status = 'paid'`? ______

---

## Q13 — NAT

How many groups does this query return?

```sql
SELECT oid, SUM(qty * price) AS line_total
FROM items
GROUP BY oid
HAVING SUM(qty * price) > 100
```

______

---

## Q14 — MCQ

Which query returns exactly the customer name Nia?

A.
```sql
SELECT c.cname
FROM customers c JOIN orders o ON c.cid = o.cid
WHERE o.status = 'paid' AND o.amt > 300
```
B.
```sql
SELECT c.cname
FROM customers c JOIN orders o ON c.cid = o.cid
WHERE o.status = 'paid'
GROUP BY c.cid, c.cname
HAVING SUM(o.amt) > 300
```
C.
```sql
SELECT c.cname
FROM customers c JOIN orders o ON c.cid = o.cid
WHERE o.status = 'paid' AND SUM(o.amt) > 300
GROUP BY c.cid, c.cname
```
D.
```sql
SELECT c.cname
FROM customers c JOIN orders o ON c.cid = o.cid
GROUP BY c.cid, c.cname
HAVING SUM(o.amt) > 100
```

---

## Q15 — NAT

What is `SELECT COUNT(DISTINCT city) FROM customers`? ______

---

## Q16 — MCQ

How many rows does this query return?

```sql
SELECT c.cname
FROM customers c LEFT JOIN orders o ON c.cid = o.cid
WHERE o.oid IS NULL
```

A. 0
B. 1
C. 2
D. 5

---

## Level 4 — Tricky / Trap-Based

## Q17 — MCQ

How many names does this query return?

```sql
SELECT cname
FROM customers
WHERE cid NOT IN (SELECT cid FROM orders)
```

A. 0
B. 1
C. 4
D. 5

---

## Q18 — MSQ

Consider query B from Q14, which groups paid orders and keeps customers with SUM(amt) > 300. Which statements are true? Select all that apply.

A. Moving the test SUM(o.amt) > 300 into the WHERE clause makes the statement illegal
B. The query in option A of Q14 returns Nia
C. HAVING sees both of Nia's paid amounts, 200 and 150
D. The predicate status = 'paid' removes Dev's void order before the sum is computed

---

## Q19 — NAT

How many rows does `SELECT iid FROM items WHERE price > 30` return? ______

---

## Level 5 — Challenge

## Q20 — NAT

How many names does this query return?

```sql
SELECT c.cname
FROM customers c
WHERE EXISTS (SELECT 1 FROM orders o WHERE o.cid = c.cid)
  AND NOT EXISTS (
        SELECT 1 FROM orders o
        WHERE o.cid = c.cid AND o.status <> 'paid')
```

______

---

## Q21 — MCQ

How many rows does this query return?

```sql
SELECT iid
FROM items
WHERE price NOT IN (SELECT amt FROM orders)
```

A. 0
B. 2
C. 3
D. 5

---

## Q22 — NAT

How many rows does this query return?

```sql
SELECT oid
FROM orders o
WHERE o.amt > ALL (
        SELECT x.amt
        FROM orders x
        WHERE x.cid = 'C4' AND x.amt IS NOT NULL)
```

______

---

## Answer Key

| Q | Type | Answer |
|---|------|--------|
| 1 | MCQ | A |
| 2 | MCQ | B |
| 3 | MCQ | B |
| 4 | MSQ | A, B, D |
| 5 | MCQ | B |
| 6 | NAT | 3 |
| 7 | NAT | 6 |
| 8 | MCQ | B |
| 9 | NAT | 6 |
| 10 | MCQ | B |
| 11 | MSQ | A, C |
| 12 | NAT | 570 |
| 13 | NAT | 2 |
| 14 | MCQ | B |
| 15 | NAT | 2 |
| 16 | MCQ | B |
| 17 | MCQ | A |
| 18 | MSQ | A, C, D |
| 19 | NAT | 3 |
| 20 | NAT | 2 |
| 21 | MCQ | A |
| 22 | NAT | 2 |

## Detailed Solutions

### Q1

Answer: A

Rows are taken from the FROM clause, then filtered by WHERE, then collected by GROUP BY. HAVING filters those groups. Only then is the SELECT list evaluated, and ORDER BY sorts the finished rows. B and C run SELECT too early, before the row and group filters. D applies WHERE after grouping, which is the opposite of the rule that makes an aggregate illegal in WHERE.

### Q2

Answer: B

COUNT of a column skips NULL. COUNT(*) counts rows, so the two differ as soon as any amt is NULL. On this instance that happens for O3, but the statement in B is the general rule and is true here as well.

A is false because of O3. C is false because SUM skips NULL rather than adding zero; the sum of an empty set of numbers is NULL, not zero, when every value is NULL. D is false because AVG divides by the number of non-NULL values, which is what COUNT(amt) counts, not by COUNT(*).

### Q3

Answer: B

An inner join keeps a pair only when the ON predicate is TRUE. Iris has no order, so she disappears. O7 has a NULL cid, and NULL equals no customer cid, so O7 disappears too.

A describes a left outer join, not an inner join. C reverses the left outer join: customers with no order are kept and padded. D is false because a later WHERE predicate such as o.oid IS NULL, or any test that rejects NULL, is applied to the padded result and can delete those rows. That interaction is exactly Q16.

### Q4

Answer: A, B, D

NULL equals nothing, including another NULL, under a comparison predicate. The result is UNKNOWN, not TRUE, so A holds. Hana's city is NULL, so both comparisons with 'Agra' are UNKNOWN and the row fails a WHERE clause. That is B. O3's amt is NULL, so amt > 100 is UNKNOWN. That is D.

C is false. COUNT(city) skips NULL, so Hana is not counted. COUNT(*) would count her.

### Q5

Answer: B

WHERE filters input rows and cannot call an aggregate of a group that has not been formed yet. HAVING filters groups after GROUP BY. SELECT computes output values; it does not decide which groups survive. ORDER BY only sorts survivors.

### Q6

Answer: 3

The amounts are 200, 150, NULL, 80, 120, 50, and 90. The values strictly above 100 are 200 (O1), 150 (O2), and 120 (O5). NULL is not above 100, and 80, 50, and 90 fail the inequality. The query returns 3 rows.

### Q7

Answer: 6

orders has 7 rows. Only O3 has a NULL amt. COUNT(amt) skips that row and returns 6. COUNT(*) would return 7.

### Q8

Answer: B

Nia and Kabir have city Surat, so city <> 'Agra' is TRUE for both. Dev and Iris have city Agra, so city = 'Agra' is TRUE for both. That is 4 rows. Hana's city is NULL, so both comparisons are UNKNOWN, the OR is UNKNOWN, and the row is rejected. The query does not return all 5 customers. D counts orders rather than customers.

### Q9

Answer: 6

Matching pairs are O1–C1, O2–C1, O3–C2, O4–C4, O5–C4, and O6–C3. O7 does not match any customer. Iris does not match any order. The inner join has 6 rows, one per matched order, not one per customer. C1 and C4 each contribute two rows.

### Q10

Answer: B

AVG ignores NULL. The six non-NULL amounts are 200, 150, 80, 120, 50, and 90. Their sum is 690, and 690 / 6 = 115.

A is the trap of dividing 690 by COUNT(*), which is 7; 690 / 7 is about 98.6. C is 600 / 5, the average obtained by also dropping O7's 90. D is the sum of paid amounts from Q12, not an average.

### Q11

Answer: A, C

A puts COUNT(*) in WHERE. Aggregates are not allowed there, whether or not a GROUP BY is present. C selects amt while grouping only by status. amt is neither in the group key nor inside an aggregate, which standard SQL rejects.

B is legal: status is the group key, and HAVING refers to an aggregate. D is legal: a query with HAVING and no GROUP BY treats the whole table as one group, and COUNT(*) is an aggregate. The predicate is TRUE because orders is not empty.

### Q12

Answer: 570

The paid rows are O1 (200), O2 (150), O4 (80), O6 (50), and O7 (90). The sum is 200 + 150 + 80 + 50 + 90 = 570. O5 is void, so its 120 is excluded. O3 is open and its amount is NULL anyway. Leaving out O7, because its cid is NULL, produces 480 and answers a different query. The WHERE clause never looks at cid.

### Q13

Answer: 2

The line totals are:

- O1: 2·40 + 1·120 = 80 + 120 = 200
- O2: 3·50 = 150
- O4: 4·20 = 80
- O6: 1·NULL = NULL

Orders with no item rows do not appear. HAVING keeps a group only when the sum is TRUE and greater than 100. O1 and O2 qualify. O4's 80 does not. O6's NULL sum makes NULL > 100 UNKNOWN, so O6 is rejected. The number of groups is 2.

### Q14

Answer: B

Nia's paid amounts are 200 and 150, and their sum is 350, which is greater than 300. Kabir has no paid order. Hana's only paid amount is 50. Dev's only paid amount is 80; the void amount 120 is removed by WHERE status = 'paid'. O7 never joins to a customer. B therefore returns only Nia.

A tests a single row. No paid amount is above 300, so A returns empty. C places SUM in WHERE and is illegal. D groups every status together. Dev's 80 + 120 = 200, which is greater than 100, so D returns Dev as well as Nia. Kabir's only amount is NULL, SUM of that group is NULL, and NULL > 100 does not keep him.

### Q15

Answer: 2

The non-NULL cities are Surat and Agra. COUNT(DISTINCT city) skips NULL, so Hana does not create a third group or a third distinct value. The answer is 2, not 3.

### Q16

Answer: B

The left join keeps every customer. Iris is the only customer with no matching order, and her order columns are NULL. The WHERE clause keeps that one padded row. Nia, Kabir, Hana, and Dev all have at least one order, so their joined rows have a non-NULL oid and fail the test. O7 is an order with no customer; a left join from customers does not invent a row for it. The result is the single name Iris.

A would be the inner-join outcome. C is the trap of also counting Hana, whose city is NULL but whose order O6 is real. D is every customer.

### Q17

Answer: A

The subquery of cid values contains C1, C2, C4, C3, and NULL, because O7's cid is NULL. For any customer cid c, the test c NOT IN (..., NULL) is UNKNOWN: c is not unequal to NULL under three-valued logic, so the NOT IN predicate is not TRUE. Every customer row is rejected, including Iris. The query returns 0 names.

B is the NOT EXISTS answer: Iris is the only customer for whom no order row satisfies o.cid = c.cid. That formulation is safe because the NULL cid in O7 does not make o.cid = 'C5' TRUE. C is the count of customers other than Kabir if the open order alone is excluded. D is every customer. None of those readings is what NOT IN does once NULL enters the subquery.

### Q18

Answer: A, C, D

SUM is an aggregate, so it is illegal in WHERE. A is true. In B, both of Nia's paid rows pass the WHERE clause and land in her group, and HAVING adds 200 and 150. C is true. Dev's void row has status void, so it is removed before grouping in that query; only the paid 80 remains, and 80 is not greater than 300. D is true.

B is false. Option A of Q14 requires a single paid amount above 300. Nia's amounts are 200 and 150, so that query is empty.

### Q19

Answer: 3

The prices are 40, 120, 50, 20, and NULL. Those strictly above 30 are 40 (I1), 120 (I2), and 50 (I3). The price 20 fails. The NULL price makes NULL > 30 UNKNOWN, so I5 is not returned. The count is 3.

### Q20

Answer: 2

A customer must have at least one order, and no order of that customer may have a status other than paid.

- Nia has O1 and O2, both paid. Kept.
- Kabir has O3, which is open. Rejected.
- Hana has O6, which is paid. Kept.
- Dev has O4 paid and O5 void. Rejected.
- Iris has no order, so the EXISTS test fails. Rejected.

O7 has a NULL cid and is not an order of any customer. The query returns Nia and Hana, so the count is 2.

### Q21

Answer: A

The subquery of amounts is {200, 150, NULL, 80, 120, 50, 90}. It contains NULL. For a concrete price such as 40 or 20, equality fails against every non-NULL amount, but equality with NULL is UNKNOWN. Then NOT IN is UNKNOWN, not TRUE, and the row is discarded. Prices that do equal some amount, such as 120 and 50, make NOT IN FALSE. The NULL price is not TRUE under NOT IN either. No item row survives, so the count is 0.

B counts 40 and 20, the prices that do not appear among the non-NULL amounts. That is what a NOT EXISTS comparison against amt would keep, together with a separate question about the NULL price. It is not what NOT IN returns while NULL sits in the subquery. C adds the NULL-price row to those two prices. D is every item.

### Q22

Answer: 2

The non-NULL amounts for C4 are 80 (O4) and 120 (O5). A value is greater than all of them only when it is greater than 120. O1 has 200 and O2 has 150. O5 itself is not greater than 120. O7 has 90. O3 is NULL and fails the comparison. The query returns O1 and O2, so the count is 2.

On this instance both of C4's amounts are already non-NULL, so the IS NOT NULL filter does not change the set {80, 120}. The filter still matters as a pattern: if a NULL amount were inside a > ALL subquery, every comparison would be UNKNOWN and the outer query would return no rows. That is the same NULL trap as Q21.
