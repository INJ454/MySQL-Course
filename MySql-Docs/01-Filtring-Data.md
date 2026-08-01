 #🗄️ MYSQL DATA FILTERING — QUERY REFERENCE

A COMPLETE MYSQL DATA FILTERING REFERENCE WITH PRACTICAL SQL QUERIES AND EXAMPLES. COVERS SELECT, WHERE, LIKE, IN, BETWEEN, IS NULL, ORDER BY, AND LIMIT TO HELP YOU RETRIEVE AND FILTER DATA EFFICIENTLY.


## 📋 TABLE OF CONTENTS

- 🏗️ [TABLE STRUCTURE](#-table-structure)
- 📝 [SAMPLE DATASET](#-sample-dataset)

### 🚀 GETTING STARTED
- 📘 [BASIC SELECT QUERIES](#-basic-select-queries)
- 🎯 [FILTERING WITH WHERE](#-filtering-with-where)
- ⚖️ [COMPARISON OPERATORS](#-comparison-operators)
- 🔗 [LOGICAL OPERATORS (AND, OR, NOT)](#-logical-operators-and-or-not)

### 🔍 PATTERN & RANGE FILTERING
- 🔍 [PATTERN MATCHING WITH LIKE](#-pattern-matching-with-like)
- 📋 [FILTERING WITH IN](#-filtering-with-in)
- 📏 [RANGE FILTERING WITH BETWEEN](#-range-filtering-with-between)
- 🚫 [NULL CHECKS](#-null-checks)

### 📊 SORTING & LIMITING RESULTS
- 📊 [SORTING WITH ORDER BY](#-sorting-with-order-by)
- 🔢 [LIMITING RESULTS](#-limiting-results)

### 🚀 ADVANCED SQL QUERIES
- 🧩 [COMBINED QUERY EXAMPLES](#-combined-query-examples)
- 🧠 [PRACTICE QUESTIONS](#-practice-questions)

⚙️ Creating Databases and Tables in MySQL

## 📌 CREATE DATABASE

```sql
CREATE DATABASE employee_db_2;
USE employee_db_2;
```

---

## 📌 CREATE TABLE

```sql
CREATE TABLE employees (
    emp_id INT PRIMARY KEY AUTO_INCREMENT,
    emp_name VARCHAR(100) NOT NULL,
    department VARCHAR(50),
    salary INT,
    email VARCHAR(100),
    status VARCHAR(20),
    manager_id INT
);
```

---


## 🏗️ TABLE SCHEMA

| Column       | Type         | Description                                      |
| ------------ | ------------ | ------------------------------------------------ |
| `emp_id`     | INT          | Primary key (Auto Increment)                     |
| `emp_name`   | VARCHAR(100) | Full name of the employee                        |
| `department` | VARCHAR(50)  | Employee's department (IT, HR, Finance, etc.)    |
| `salary`     | INT          | Employee salary                                  |
| `email`      | VARCHAR(100) | Employee email address                           |
| `status`     | VARCHAR(20)  | Employment status (Active / Inactive / On Leave) |
| `manager_id` | INT          | Manager's `emp_id` (Foreign Key if applicable)   |

---

## 📥 INSERT SAMPLE DATA

```sql
INSERT INTO employees
(emp_name, department, salary, email, status, manager_id)
VALUES
('Aman','IT',95000,'aman@gmail.com','Active',101),
('Aditi','HR',60000,'aditi@gmail.com','Active',102),
('Sohan','Finance',85000,'sohan@yahoo.com','Active',103),
('Simran','IT',75000,'simran@gmail.com','Active',101),
('Rohit','Marketing',55000,'rohit@gmail.com','Inactive',104),
('Ankit','Finance',72000,NULL,'Active',103),
('Neha','HR',48000,'neha@gmail.com','Inactive',NULL),
('Sakshi','IT',90000,'sakshi@gmail.com','Active',NULL),
('Priya','Marketing',68000,'priya@yahoo.com','Active',104),
('Arjun','IT',82000,'arjun@gmail.com','Inactive',101),
('Mohit','Finance',79000,'mohit@gmail.com','Active',103),
('Sunil','HR',51000,NULL,'Inactive',102),
('Ajay','IT',45000,'ajay@gmail.com','Active',NULL),
('Sneha','Finance',88000,'sneha@gmail.com','Active',103),
('Karan','Marketing',65000,'karan@gmail.com','Active',104);
```

---

## 🎯 DATASET HIGHLIGHTS

- ✅ Auto Increment Primary Key (`emp_id`)
- ✅ 15 Sample Employee Records
- ✅ Multiple Departments (IT, HR, Finance, Marketing)
- ✅ Active & Inactive Employee Status
- ✅ NULL Values for SQL Practice
- ✅ Manager IDs for Relationship-Based Queries
- ✅ Perfect for Learning Data Filtering with MySQL

# 📘 BASIC SELECT QUERIES

## 🔹 Q1 — Retrieve All Employee Details

```sql
SELECT * FROM employees;
```

---

## 🔹 Q2 — Retrieve Employee Name, Department & Salary

```sql
SELECT emp_name, department, salary
FROM employees;
```

---

## 🔹 Q3 — Find All Unique Departments

```sql
SELECT DISTINCT department
FROM employees;
```

---

# 🔍 FILTERING WITH WHERE

## 💼 Q4 — Employees in the IT Department

```sql
SELECT emp_name, department
FROM employees
WHERE department = 'IT';
```

---

## 💰 Q5 — Employees Earning More Than ₹80,000

```sql
SELECT emp_name, salary
FROM employees
WHERE salary > 80000;
```

---

## 💻 Q6 — IT Employees Earning More Than ₹80,000

```sql
SELECT emp_name, department
FROM employees
WHERE department = 'IT'
AND salary > 80000;
```

---

## 🏢 Q7 — Employees in IT or Finance

### ✅ Method 1 — Using OR

```sql
SELECT emp_name, department
FROM employees
WHERE department = 'IT'
OR department = 'Finance';
```

### ✅ Method 2 — Using IN

```sql
SELECT emp_name, department
FROM employees
WHERE department IN ('IT', 'Finance');
```

---

## 👥 Q8 — Employees Who Are NOT Active

### ✅ Method 1 — Using !=

```sql
SELECT emp_name, status
FROM employees
WHERE status != 'Active';
```

### ✅ Method 2 — Using <>

```sql
SELECT emp_name, status
FROM employees
WHERE status <> 'Active';
```

---

## 📂 Q9 — Employees in IT, HR & Finance

```sql
SELECT emp_name, department
FROM employees
WHERE department IN ('IT', 'HR', 'Finance');
```

---

## 💵 Q10 — Employees with Salary Between ₹50,000 and ₹80,000

```sql
SELECT emp_name, salary
FROM employees
WHERE salary BETWEEN 50000 AND 80000;
```

---

# 🔎 PATTERN MATCHING WITH LIKE

## 👤 Q11 — Employees Whose Name Starts With 'A'

```sql
SELECT *
FROM employees
WHERE emp_name LIKE 'A%';
```

---

## 📧 Q12 — Employees with Gmail Addresses

```sql
SELECT *
FROM employees
WHERE email LIKE '%gmail%';
```

---

## ⭐ Q13 — Active Employees Whose Name Starts With 'S'

```sql
SELECT *
FROM employees
WHERE status = 'Active'
AND emp_name LIKE 'S%';
```

---

# 🚫 NULL CHECKS

## 👨‍💼 Q14 — Employees Without a Manager

```sql
SELECT *
FROM employees
WHERE manager_id IS NULL;
```

---

## 📩 Q15 — Employees with an Email Address

```sql
SELECT *
FROM employees
WHERE email IS NOT NULL;
```

---

# 📊 SORTING WITH ORDER BY

## ⬆️ Q16 — Sort Salary from Lowest to Highest

```sql
SELECT *
FROM employees
ORDER BY salary ASC;
```

---

## ⬇️ Q17 — Sort Salary from Highest to Lowest

```sql
SELECT emp_name, salary
FROM employees
ORDER BY salary DESC;
```

---

## 🗂️ Q18 — Sort by Department, Then Salary

```sql
SELECT emp_name, department, salary
FROM employees
ORDER BY department ASC, salary DESC;
```

---

# 🔢 LIMITING RESULTS

## 🏆 Q19 — Top 5 Highest-Paid Employees

```sql
SELECT emp_name, department, salary
FROM employees
ORDER BY salary DESC
LIMIT 5;
```

---

# 🧩 COMBINED QUERY EXAMPLES

## 🚀 Q20 — Top 3 Highest-Paid IT/Finance Employees (₹70K–₹1L)

```sql
SELECT *
FROM employees
WHERE department IN ('IT', 'Finance')
AND salary BETWEEN 70000 AND 100000
ORDER BY salary DESC
LIMIT 3;
```

## 🚀 MINI CHALLENGE

## 📝 Q21 — Find Employees Earning Less Than ₹60,000

## 📝 Q22 — Find Employees Whose Name Ends with 'N'

## 📝 Q23 — Retrieve Active Employees from the HR Department

## 📝 Q24 — Display the Top 3 Lowest-Paid Employees

## 📝 Q25 — Find Employees Without an Email Address

## 📝 Q26 — Display Employees Sorted by Name (A–Z)

## 📝 Q27 — Find Finance Employees Earning More Than ₹75,000

## 📝 Q28 — Count the Number of Employees in Each Department

## 📝 Q29 — Display Employees with Yahoo Email Addresses

## 📝 Q30 — Retrieve Employees Whose Salary Is Not Between ₹60K and ₹90K





## ⭐ THANK YOU FOR VISITING THIS REPOSITORY!

IF YOU FOUND THIS PROJECT HELPFUL, PLEASE CONSIDER GIVING IT A ⭐ STAR. YOUR SUPPORT IS GREATLY APPRECIATED!








