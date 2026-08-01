# 🗄️ MySQL DDL & DML Commands – Query Reference

A complete beginner-friendly reference for **MySQL DDL (Data Definition Language)** and **DML (Data Manipulation Language)** commands with practical SQL examples.

This guide covers table creation, table modification, inserting data, updating records, deleting records, and other commonly used SQL operations.

---

# 📚 Table of Contents

- 📖 DDL vs DML
- 🏗️ CREATE TABLE
- 📋 Table Schema
- ➕ ALTER TABLE
- 📝 RENAME COLUMN
- 🔄 MODIFY COLUMN
- 📛 RENAME TABLE
- 🗑️ TRUNCATE TABLE
- ❌ DROP TABLE
- ➕ INSERT
- 🔍 SELECT
- 🎯 WHERE Clause
- ✏️ UPDATE
- 🗑️ DELETE

---

# 📖 DDL vs DML

| DDL (Data Definition Language) | DML (Data Manipulation Language) |
|--------------------------------|----------------------------------|
| Used to define database structure | Used to manipulate data |
| CREATE | INSERT |
| ALTER | UPDATE |
| DROP | DELETE |
| TRUNCATE | REPLACE |
| RENAME | SELECT |

---

## 📷 DDL vs DML Difference

<img width="2720" height="1600" alt="ddl_vs_dml_sql_commands" src="https://github.com/user-attachments/assets/7a578215-0a08-466a-901e-641f8b5e3342" />

---

# 🏗️ CREATE TABLE

```sql
CREATE TABLE employee (
    emp_id INT PRIMARY KEY,
    emp_name VARCHAR(50),
    age INT,
    salary DECIMAL(10,2)
);

DESC employee;
```

---

# 📋 Table Schema

| Field | Type | Null | Key |
|--------|------|------|-----|
| emp_id | int | NO | PRI |
| emp_name | varchar(50) | YES | |
| age | int | YES | |
| salary | decimal(10,2) | YES | |

---

# ➕ ALTER TABLE (Add Column)

### SQL Query

```sql
ALTER TABLE employee
ADD department VARCHAR(30);
```

### Check Table Structure

```sql
DESC employee;
```

### Output

| Field | Type |
|--------|------|
| emp_id | int |
| emp_name | varchar(50) |
| age | int |
| salary | decimal(10,2) |
| department | varchar(30) |

---

# 📝 Rename Column

### SQL Query

```sql
ALTER TABLE employee
RENAME COLUMN department TO dept;
```

### Output

| Old Column | New Column |
|------------|------------|
| department | dept |

---

# 🔄 Modify Column Data Type

### SQL Query

```sql
ALTER TABLE employee
MODIFY salary DECIMAL(12,2);
```

### Output

Salary column size becomes:

```text
DECIMAL(12,2)
```

---

# 📛 Rename Table

### SQL Query

```sql
RENAME TABLE employee TO employees;
```

### Output

```text
employee
⬇
employees
```

---

# 🗑️ TRUNCATE TABLE

Removes **all records** from the table while keeping the table structure.

### SQL Query

```sql
TRUNCATE TABLE employees;
```

### Output

```text
Query OK

0 Rows
```

---

# ❌ DROP TABLE

Deletes the **entire table permanently**, including its structure and data.

### SQL Query

```sql
DROP TABLE employees;
```

### Output

```text
Query OK
```

---

# 📥 INSERT INTO

### SQL Query

```sql
INSERT INTO employee
(emp_id, emp_name, age, salary)
VALUES
(101, 'Tarun', 22, 30000),
(102, 'Rahul', 24, 35000),
(103, 'Aman', 21, 30000);
```

---

# 📄 Table Data

| emp_id | emp_name | age | salary |
|--------|----------|-----|--------|
|101|Tarun|22|30000|
|102|Rahul|24|35000|
|103|Aman|21|30000|

---

# 🔍 SELECT

### Select All Data

```sql
SELECT *
FROM employee;
```

### Output

| emp_id | emp_name | age | salary |
|--------|----------|-----|--------|
|101|Tarun|22|30000|
|102|Rahul|24|35000|
|103|Aman|21|30000|

---

# 🎯 SELECT Specific Columns

### SQL Query

```sql
SELECT emp_name, salary
FROM employee;
```

### Output

| emp_name | salary |
|-----------|---------|
|Tarun|30000|
|Rahul|35000|
|Aman|30000|

---

# 🎯 WHERE Clause

### SQL Query

```sql
SELECT *
FROM employee
WHERE salary > 30000;
```

### Output

| emp_id | emp_name | age | salary |
|--------|----------|-----|--------|
|102|Rahul|24|35000|

---

# ✏️ UPDATE

### Update One Column

```sql
UPDATE employee
SET salary = 40000
WHERE emp_id = 101;
```

### Output

| emp_id | salary |
|--------|---------|
|101|40000|

---

# ✏️ Update Multiple Columns

### SQL Query

```sql
UPDATE employee
SET age = 23,
    salary = 45000
WHERE emp_id = 101;
```

### Output

| emp_id | age | salary |
|--------|-----|---------|
|101|23|45000|

---

# 🗑️ DELETE Specific Record

### SQL Query

```sql
DELETE FROM employee
WHERE emp_id = 102;
```

### Output

| Remaining Records |
|-------------------|
|101|
|103|

---

# 🗑️ DELETE All Records

Deletes every row but keeps the table.

### SQL Query

```sql
DELETE FROM employee;
```

### Output

```text
Empty Set
```

---

# 📌 Summary

| Command | Purpose |
|----------|----------|
| CREATE | Create a table |
| ALTER | Modify table structure |
| RENAME | Rename table or column |
| MODIFY | Change data type |
| TRUNCATE | Remove all rows |
| DROP | Delete table permanently |
| INSERT | Add records |
| SELECT | Retrieve data |
| UPDATE | Modify records |
| DELETE | Remove records |

---

# ⭐ Features

- ✅ Beginner Friendly
- ✅ Practical SQL Queries
- ✅ Clean Formatting
- ✅ MySQL Compatible
- ✅ GitHub Ready
- ✅ Interview Preparation
- ✅ Includes Expected Outputs
- ✅ Easy to Understand

---



---

# 💼 Interview Practice Questions

Practice these beginner-friendly SQL questions using the `employee` table.

---

## 📝 Question 1: Display All Employee Records

### SQL Query

```sql
SELECT *
FROM employee;
```

### Expected Output

| emp_id | emp_name | age | salary |
|--------|----------|-----|---------|
|101|Tarun|22|30000|
|102|Rahul|24|35000|
|103|Aman|21|30000|

---

## 📝 Question 2: Display Employee Name and Salary

### SQL Query

```sql
SELECT emp_name, salary
FROM employee;
```

### Expected Output

| emp_name | salary |
|-----------|---------|
|Tarun|30000|
|Rahul|35000|
|Aman|30000|

---

## 📝 Question 3: Find Employees with Salary Greater Than 30,000

### SQL Query

```sql
SELECT *
FROM employee
WHERE salary > 30000;
```

### Expected Output

| emp_id | emp_name | age | salary |
|--------|----------|-----|---------|
|102|Rahul|24|35000|

---

## 📝 Question 4: Increase Tarun's Salary to 40,000

### SQL Query

```sql
UPDATE employee
SET salary = 40000
WHERE emp_id = 101;

SELECT *
FROM employee
WHERE emp_id = 101;
```

### Expected Output

| emp_id | emp_name | age | salary |
|--------|----------|-----|---------|
|101|Tarun|22|40000|

---

## 📝 Question 5: Delete Rahul's Record

### SQL Query

```sql
DELETE FROM employee
WHERE emp_id = 102;

SELECT *
FROM employee;
```

### Expected Output

| emp_id | emp_name | age | salary |
|--------|----------|-----|---------|
|101|Tarun|22|30000|
|103|Aman|21|30000|

---

## 🎯 Interview Flow

1. 🏗️ Create the `employee` table.
2. ➕ Insert sample records.
3. 🔍 Display all records using `SELECT *`.
4. 📄 Retrieve specific columns.
5. 🎯 Filter records using the `WHERE` clause.
6. ✏️ Update employee details.
7. 🗑️ Delete a specific record.

These questions are commonly asked in **SQL interviews** and are great for **beginner practice**.

## 🚀 Connect With Me

If this repository helped you, consider giving it a ⭐ on GitHub.

Happy Learning! 💙
