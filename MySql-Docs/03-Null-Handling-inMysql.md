#  🗄️MySQL NULL Handling – Query Reference

A complete beginner-friendly guide to understanding **NULL Handling in MySQL** with practical examples, table data, outputs, interview questions, and explanations.

---
## 📑 Table of Contents

* 📌 [What is NULL?](#what-is-null)
* ❓ [Why is NULL Important?](#why-is-null-important)
* 🗄️ [Create Database](#create-database)
* 🏗️ [Create Table](#create-table)
* ➕ [Insert Data](#insert-data)
* 📋 [Table Content](#table-content)
* 👀 [Display Table](#display-table)
* 🔍 [Find NULL Values](#find-null-values)
* ✅ [Find NOT NULL Values](#find-not-null-values)
* ❌ [Wrong Way](#wrong-way-)
* ✔️ [Correct Way](#correct-way-)
* 🔄 [IFNULL()](#ifnull)
* 🧩 [COALESCE()](#coalesce)
* ⚖️ [Difference Between IFNULL() and COALESCE()](#difference-between-ifnull-and-coalesce)
* ➕➖ [NULL in Arithmetic](#null-in-arithmetic)
* 🔗 [NULL in CONCAT()](#null-in-concat)
* 📊 [ORDER BY with NULL](#order-by-with-null)
* 🔢 [COUNT()](#count)
* ✏️ [UPDATE NULL Values](#update-null-values)
* 🗑️ [DELETE NULL Values](#delete-null-values)
* 💼 [Interview Questions with Answers](#interview-questions-with-answers)
* ⚡ [Quick Revision](#quick-revision)
* 🎯 [Conclusion](#conclusion)


---

# What is NULL?

In MySQL, **NULL** represents a **missing, unknown, or unavailable value**.

It does **NOT** mean:

- Zero (0)
- Empty string ('')
- False

A NULL value simply means **no value has been assigned**.

### Example

Suppose an employee has not received a bonus yet.

| Employee | Bonus |
|----------|------:|
| Amit | 5000 |
| Rahul | NULL |

Rahul's bonus is **unknown or not assigned**, so MySQL stores it as **NULL**.

---

# Why is NULL Important?

NULL values are common in databases.

Examples:

- Customer phone number not available
- Employee bonus not decided
- Student email not submitted
- Delivery date not assigned

Therefore, every SQL developer should know how to work with NULL values.

---

# Create Database

```sql
CREATE DATABASE CompanyDb_5;

USE CompanyDb_5;
```

---

# Create Table

```sql
CREATE TABLE employees(
    emp_id INT PRIMARY KEY,
    emp_name VARCHAR(50),
    department VARCHAR(60),
    salary INT,
    bonus INT
);
```

---

# Insert Data

```sql
INSERT INTO employees VALUES
(1,'Amit','IT',50000,5000),
(2,'Rahul','HR',40000,NULL),
(3,'Priya','IT',60000,7000),
(4,'Neha','Finance',55000,NULL),
(5,'Rohit','Sales',45000,3000),
(6,'Anjali','HR',48000,NULL),
(7,'Vikas','IT',70000,8000),
(8,'Sneha','Marketing',52000,2500),
(9,'Karan','Sales',43000,NULL),
(10,'Pooja','Finance',61000,6000),
(11,'Arjun','IT',75000,NULL),
(12,'Simran','HR',47000,2000),
(13,'Deepak','Marketing',58000,NULL),
(14,'Nisha','Sales',49000,4000),
(15,'Kavya','Marketing',54000,3500);
```

---

# Table Content

| emp_id | emp_name | department | salary | bonus |
|------:|-----------|------------|-------:|------:|
|1|Amit|IT|50000|5000|
|2|Rahul|HR|40000|NULL|
|3|Priya|IT|60000|7000|
|4|Neha|Finance|55000|NULL|
|5|Rohit|Sales|45000|3000|
|6|Anjali|HR|48000|NULL|
|7|Vikas|IT|70000|8000|
|8|Sneha|Marketing|52000|2500|
|9|Karan|Sales|43000|NULL|
|10|Pooja|Finance|61000|6000|
|11|Arjun|IT|75000|NULL|
|12|Simran|HR|47000|2000|
|13|Deepak|Marketing|58000|NULL|
|14|Nisha|Sales|49000|4000|
|15|Kavya|Marketing|54000|3500|

---

# Display Table

```sql
DESC employees;
```

### Output

| Field | Type |
|------|------|
| emp_id | int |
| emp_name | varchar(50) |
| department | varchar(60) |
| salary | int |
| bonus | int |

---

```sql
SELECT * FROM employees;
```

### Output

Returns all 15 records.

---

# Find NULL Values

Employees whose bonus has not been assigned.

```sql
SELECT *
FROM employees
WHERE bonus IS NULL;
```

### Output

| emp_name | bonus |
|----------|------|
| Rahul | NULL |
| Neha | NULL |
| Anjali | NULL |
| Karan | NULL |
| Arjun | NULL |
| Deepak | NULL |

---

# Find NOT NULL Values

Employees who received bonus.

```sql
SELECT *
FROM employees
WHERE bonus IS NOT NULL;
```

### Output

| emp_name | bonus |
|----------|------:|
| Amit |5000|
| Priya |7000|
| Rohit |3000|
| Vikas |8000|
| Sneha |2500|
| Pooja |6000|
| Simran |2000|
| Nisha |4000|
| Kavya |3500|

---

# Wrong Way ❌

```sql
SELECT *
FROM employees
WHERE bonus = NULL;
```

### Output

```
Empty Set
```

---

```sql
SELECT *
FROM employees
WHERE bonus != NULL;
```

### Output

```
Empty Set
```

### Why?

NULL cannot be compared using:

- =
- !=
- < >
- >

Always use:

- IS NULL
- IS NOT NULL

---

# Correct Way ✅

```sql
SELECT *
FROM employees
WHERE bonus IS NULL;
```

Output:

Returns all employees having NULL bonus.

---

```sql
SELECT *
FROM employees
WHERE bonus IS NOT NULL;
```

Output:

Returns all employees having bonus.

---

# IFNULL()

Replaces NULL values.

```sql
SELECT
emp_name,
IFNULL(bonus,0) AS bonus
FROM employees;
```

### Output

| emp_name | bonus |
|----------|------:|
| Amit |5000|
| Rahul |0|
| Priya |7000|
| Neha |0|
| Rohit |3000|
| ... | ... |

### Explanation

If bonus is NULL, MySQL returns **0**.

---

# COALESCE()

Returns the first non-NULL value.

```sql
SELECT
emp_name,
COALESCE(bonus,1000) AS bonus
FROM employees;
```

### Output

| emp_name | bonus |
|----------|------:|
| Amit |5000|
| Rahul |1000|
| Priya |7000|
| Neha |1000|

### Explanation

If bonus is NULL, MySQL returns **1000**.

---

# Difference Between IFNULL() and COALESCE()

| IFNULL() | COALESCE() |
|-----------|------------|
| Accepts only 2 arguments | Accepts multiple arguments |
| MySQL specific | Standard SQL |
| Faster for simple replacement | Better for multiple fallback values |

Example:

```sql
SELECT COALESCE(NULL,NULL,500,NULL);
```

### Output

```
500
```

---

# NULL in Arithmetic

```sql
SELECT
emp_name,
salary + IFNULL(bonus,0) AS total_salary
FROM employees;
```

### Output

| emp_name | total_salary |
|----------|-------------:|
| Amit |55000|
| Rahul |40000|
| Priya |67000|
| Neha |55000|

---

# Without IFNULL()

```sql
SELECT salary + bonus
FROM employees;
```

### Output

Employees with NULL bonus return:

```
NULL
```

Reason:

```
Any arithmetic operation with NULL returns NULL.
```

---

# NULL in CONCAT()

```sql
SELECT
CONCAT(emp_name,' ',IFNULL(bonus,0))
AS emp_bonus
FROM employees;
```

### Output

| emp_bonus |
|-----------|
| Amit 5000 |
| Rahul 0 |
| Priya 7000 |
| Neha 0 |

---

# ORDER BY with NULL

## Ascending

```sql
SELECT *
FROM employees
ORDER BY bonus;
```

### Output

NULL values appear first.

---

## Descending

```sql
SELECT *
FROM employees
ORDER BY bonus DESC;
```

### Output

Highest bonus first.

NULL values appear last.

---

# COUNT()

## COUNT(column)

```sql
SELECT COUNT(bonus)
FROM employees;
```

### Output

```
9
```

Explanation:

Only non-NULL bonus values are counted.

---

## COUNT(*)

```sql
SELECT COUNT(*)
FROM employees;
```

### Output

```
15
```

Explanation:

Counts every row.

---

# UPDATE NULL Values

```sql
UPDATE employees
SET bonus = 2000
WHERE bonus IS NULL;
```

### Output

```
6 Rows Updated
```

---

# DELETE NULL Values

```sql
DELETE
FROM employees
WHERE bonus IS NULL;
```

### Output

```
6 Rows Deleted
```

---

# Interview Questions with Answers

## Q1. What is NULL?

**Answer**

NULL represents a missing, unknown, or unavailable value.

---

## Q2. Is NULL equal to Zero?

**Answer**

No.

NULL means unknown.

0 is an actual numeric value.

---

## Q3. Difference between NULL and Empty String?

| NULL | Empty String |
|------|--------------|
| Unknown value | Value exists but empty |

---

## Q4. How do you check NULL values?

```sql
WHERE column IS NULL;
```

---

## Q5. How do you check NOT NULL values?

```sql
WHERE column IS NOT NULL;
```

---

## Q6. Why doesn't = NULL work?

**Answer**

NULL cannot be compared using comparison operators.

Always use:

```sql
IS NULL
```

---

## Q7. Difference between IFNULL() and COALESCE()?

| IFNULL | COALESCE |
|---------|----------|
|2 arguments|Multiple arguments|
|MySQL only|Standard SQL|

---

## Q8. Does COUNT(column) count NULL?

**Answer**

No.

Only non-NULL values are counted.

---

## Q9. What does COUNT(*) do?

**Answer**

Counts every row including rows containing NULL values.

---

## Q10. What happens when adding NULL?

```sql
SELECT 10 + NULL;
```

### Output

```
NULL
```

---

## Q11. What is the output?

```sql
SELECT IFNULL(NULL,500);
```

### Output

```
500
```

---

## Q12. What is the output?

```sql
SELECT COALESCE(NULL,NULL,200,NULL);
```

### Output

```
200
```

---

## Q13. Which function is ANSI SQL Standard?

**Answer**

COALESCE()

---

## Q14. Can NULL be stored in a PRIMARY KEY?

**Answer**

No.

A PRIMARY KEY cannot contain NULL values.

---

## Q15. Can UNIQUE column contain NULL?

**Answer**

Yes.

A UNIQUE column can contain NULL values (database behavior may vary slightly by SQL engine).

---

# Quick Revision

| Operation | Syntax |
|-----------|--------|
| Find NULL | `WHERE column IS NULL` |
| Find NOT NULL | `WHERE column IS NOT NULL` |
| Replace NULL | `IFNULL(column, value)` |
| First Non-NULL | `COALESCE(a,b,c)` |
| Count All Rows | `COUNT(*)` |
| Count Non-NULL Values | `COUNT(column)` |
| Arithmetic with NULL | Result is NULL |
| Update NULL | `UPDATE table SET column=value WHERE column IS NULL` |
| Delete NULL Rows | `DELETE FROM table WHERE column IS NULL` |

---

## 🚀 Connect With Me

If this repository helped you, consider giving it a ⭐ on GitHub.

Happy Learning! 💙
