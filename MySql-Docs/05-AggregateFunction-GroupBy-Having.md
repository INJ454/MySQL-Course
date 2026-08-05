# 🗄️ MySQL Aggregate Functions, GROUP BY & HAVING – Query Reference

A complete beginner-friendly guide to understanding **MySQL Aggregate Functions, GROUP BY, and HAVING** with practical examples, sample table data, query outputs, detailed explanations, and interview questions.

# 📘 Aggregate Functions

Aggregate Functions are used to perform calculations on multiple rows and return a **single value**.

**Common Aggregate Functions:**

- `SUM()` → Returns the total of a numeric column.
- `AVG()` → Returns the average value.
- `MAX()` → Returns the highest value.
- `MIN()` → Returns the lowest value.
- `COUNT()` → Returns the total number of rows or non-NULL values.

---

# 📂 GROUP BY

The `GROUP BY` clause is used to group rows that have the same values in one or more columns. It is commonly used with Aggregate Functions to calculate results for each group.

**Example:**

```sql
SELECT department, AVG(salary)
FROM employees
GROUP BY department;
```

---

# 🎯 HAVING

The `HAVING` clause is used to filter grouped data **after** the `GROUP BY` operation. It is mainly used with Aggregate Functions.

**Example:**

```sql
SELECT department, AVG(salary)
FROM employees
GROUP BY department
HAVING AVG(salary) > 60000;
```

---

## 📌 Difference Between WHERE and HAVING

| WHERE | HAVING |
|--------|---------|
| Filters rows before grouping | Filters groups after grouping |
| Cannot use Aggregate Functions | Can use Aggregate Functions |
| Executed before `GROUP BY` | Executed after `GROUP BY` |

---
# Table of Contents

## 📑 Table of Contents

* 📖 [Introduction](#introduction)
* 🗄️ [Create Database](#create-database)
* 🏗️ [Create Table](#create-table)
* ➕ [Insert Data](#insert-data)
* 📋 [Table Content](#table-content)
* ❓ [Q1. Total Salary Expense](#q1-find-the-total-salary-expense-of-the-company)
* ❓ [Q2. Average Salary](#q2-find-the-average-salary-of-all-employees)
* ❓ [Q3. Maximum Salary](#q3-find-the-maximum-salary-of-all-employees)
* ❓ [Q4. Minimum Salary](#q4-find-the-minimum-salary-of-all-employees)
* ❓ [Q5. Total Employees](#q5-find-the-total-number-of-employees-in-the-company)
* ❓ [Difference Between COUNT(*), COUNT(column), COUNT(1)](#difference-between-count-countcolumn-and-count1)
* ❓ [Q6. Highest & Lowest Salary](#q6-find-the-highest-and-lowest-salary-in-the-company)
* ❓ [Q7. Employees in Each Department](#q7-find-the-total-number-of-employees-in-each-department)
* ❓ [Q8. Average Salary in Each City](#q8-find-the-average-salary-of-employees-in-each-city)
* ❓ [Q9. Active Employees in Each Department](#q9-find-the-total-number-of-active-employees-in-each-department)
* ❓ [Q10. Salary Expense of Mumbai Employees](#q10-find-the-total-salary-expense-of-employees-working-in-mumbai-for-each-department)
* ❓ [Q11. Highest Salary in Each Department](#q11-find-the-highest-salary-in-each-department)
* ❓ [Q12. Lowest Salary in Each Department](#q12-find-the-lowest-salary-in-each-department)
* ❓ [Q13. Average Salary in Each Department](#q13-find-the-average-salary-in-each-department)
* ❓ [Q14. Departments Having More Than 2 Employees](#q14-find-departments-having-more-than-2-employees)
* ❓ [Q15. Cities Where Average Salary is Greater Than 60,000](#q15-find-cities-where-the-average-salary-is-greater-than-60000)
* ❓ [Q16. Departments Whose Total Salary is Greater Than 1,50000](#q16-find-departments-whose-total-salary-is-greater-than-150000)
* ❓ [Q17. Total Salary of Active Employees in Each Department](#q17-find-the-total-salary-of-active-employees-in-each-department)
* ❓ [Q18. Total Number of Inactive Employees in Each City](#q18-find-the-total-number-of-inactive-employees-in-each-city)
* ❓ [Q19. Department with Highest Total Salary](#q19-find-the-department-with-the-highest-total-salary)
* ❓ [Q20. City with Maximum Employees](#q20-find-the-city-with-the-maximum-number-of-employees)
* ❓ [Q21. Total Employees in Each City](#q21-find-the-total-number-of-employees-in-each-city)
* ❓ [Q22. Total Salary Paid in Each City](#q22-find-the-total-salary-paid-in-each-city)
* ❓ [Q23. Departments Having Average Salary Greater Than 65,000](#q23-find-departments-where-the-average-salary-is-greater-than-65000)
* ❓ [Q24. Cities Having More Than 3 Employees](#q24-find-cities-having-more-than-3-employees)
* ❓ [Q25. Department Having Maximum Active Employees](#q25-find-the-department-having-the-maximum-number-of-active-employees)
* ❓ [Q26. Employees Having a Manager Assigned](#q26-find-how-many-employees-have-a-manager-assigned)


---

# Create Database

```sql
CREATE DATABASE company_db07;

USE company_db07;
```

---

# Create Table

```sql
CREATE TABLE employees(
    emp_id INT PRIMARY KEY,
    emp_name VARCHAR(50),
    department VARCHAR(30),
    city VARCHAR(30),
    salary DECIMAL(10,2),
    manager_id INT,
    status VARCHAR(20)
);
```

---

# Insert Data

```sql
INSERT INTO employees
(emp_id,emp_name,department,city,salary,manager_id,status)
VALUES
(101,'Tarun','IT','Delhi',50000,NULL,'Active'),
...
(115,'Arjun','Marketing','Chandigarh',62000,110,'Active');
```

---

# Table Content

| ID | Name | Department | City | Salary | Manager | Status |
|----|------|------------|------|--------:|--------:|--------|
|101|Tarun|IT|Delhi|50000|NULL|Active|
|102|Rahul|IT|Mumbai|65000|101|Active|
|103|Aman|HR|Delhi|45000|105|Inactive|
|104|Neha|Finance|Mumbai|70000|106|Active|
|105|Simran|HR|Chandigarh|55000|NULL|Active|
|106|Priya|Finance|Delhi|80000|NULL|Active|
|107|Rohit|Sales|Mumbai|60000|108|Active|
|108|Karan|Sales|Pune|90000|NULL|Inactive|
|109|Anjali|Marketing|Delhi|52000|110|Active|
|110|Pooja|Marketing|Mumbai|75000|NULL|Active|
|111|Vikas|IT|Mumbai|68000|101|Active|
|112|Sonia|HR|Pune|48000|105|Active|
|113|Deepak|Finance|Mumbai|72000|106|Active|
|114|Meena|Sales|Delhi|58000|108|Inactive|
|115|Arjun|Marketing|Chandigarh|62000|110|Active|

---

# Q1. Find the Total Salary Expense of the Company

### Query

```sql
SELECT SUM(salary) AS total_salary
FROM employees;
```

### Output

| total_salary |
|-------------:|
|950000|

### Explanation

`SUM()` calculates the total salary of all employees.

---

# Q2. Find the Average Salary of Employees

### Query

```sql
SELECT AVG(salary) AS avg_salary
FROM employees;
```

### Output

| avg_salary |
|-----------:|
|63333.33|

### Explanation

`AVG()` returns the average salary.

---

# Q3. Find the Maximum Salary

### Query

```sql
SELECT MAX(salary) AS max_salary
FROM employees;
```

### Output

| max_salary |
|-----------:|
|90000|

### Explanation

`MAX()` returns the highest salary.

---

# Q4. Find the Minimum Salary

### Query

```sql
SELECT MIN(salary) AS min_salary
FROM employees;
```

### Output

| min_salary |
|-----------:|
|45000|

### Explanation

`MIN()` returns the lowest salary.

---

# Q5. Find Total Employees

### Query

```sql
SELECT COUNT(*) AS total_emp
FROM employees;
```

### Output

| total_emp |
|----------:|
|15|

### Explanation

`COUNT(*)` counts all rows.

---

# Difference Between COUNT(*), COUNT(column), and COUNT(1)

| Function | Description |
|----------|-------------|
|COUNT(*)|Counts all rows|
|COUNT(column)|Counts only NON-NULL values|
|COUNT(1)|Counts all rows|

### Example

```sql
SELECT COUNT(manager_id)
FROM employees;
```

### Output

| manager_id |
|-----------:|
|10|

Explanation:

There are 10 employees having a manager assigned.

---

# Q6. Find Highest and Lowest Salary

### Query

```sql
SELECT
MAX(salary) AS highest,
MIN(salary) AS lowest
FROM employees;
```

### Output

| highest | lowest |
|---------:|-------:|
|90000|45000|

---

# Q7. Find Total Employees in Each Department

### Query

```sql
SELECT department,
COUNT(*) AS total_employees
FROM employees
GROUP BY department;
```

### Output

| Department | Employees |
|------------|----------:|
|Finance|3|
|HR|3|
|IT|3|
|Marketing|3|
|Sales|3|

---

# Q8. Find Average Salary in Each City

### Query

```sql
SELECT city,
AVG(salary) AS avg_salary
FROM employees
GROUP BY city;
```

### Output

| City | Average Salary |
|------|---------------:|
|Chandigarh|58500|
|Delhi|57000|
|Mumbai|68333.33|
|Pune|69000|

---

# Q9. Find Active Employees in Each Department

### Query

```sql
SELECT department,
COUNT(*) AS active_emp
FROM employees
WHERE status='Active'
GROUP BY department;
```

### Output

| Department | Active Employees |
|------------|-----------------:|
|Finance|3|
|HR|2|
|IT|3|
|Marketing|3|
|Sales|1|

---

# Q10. Find Total Salary Expense of Mumbai Employees

### Query

```sql
SELECT department,
SUM(salary) AS total_expense
FROM employees
WHERE city='Mumbai'
GROUP BY department;
```

### Output

| Department | Total Expense |
|------------|--------------:|
|Finance|142000|
|IT|133000|
|Marketing|75000|
|Sales|60000|

---

# Q11. Find Highest Salary in Each Department

### Query

```sql
SELECT department,
MAX(salary) AS highest_salary
FROM employees
GROUP BY department;
```

### Output

| Department | Highest Salary |
|------------|---------------:|
|Finance|80000|
|HR|55000|
|IT|68000|
|Marketing|75000|
|Sales|90000|

---

# Q12. Find the Lowest Salary in Each Department

### SQL Query

```sql
SELECT department,
MIN(salary) AS lowest_salary
FROM employees
GROUP BY department;
```

### Output

| Department | Lowest Salary |
|------------|--------------:|
| Finance | 70000 |
| HR | 45000 |
| IT | 50000 |
| Marketing | 52000 |
| Sales | 58000 |

### Explanation

`MIN()` returns the smallest salary from each department.

---

# Q13. Find the Average Salary in Each Department

### SQL Query

```sql
SELECT department,
AVG(salary) AS avg_salary
FROM employees
GROUP BY department;
```

### Output

| Department | Average Salary |
|------------|---------------:|
| Finance | 74000.00 |
| HR | 49333.33 |
| IT | 61000.00 |
| Marketing | 63000.00 |
| Sales | 69333.33 |

### Explanation

`AVG()` calculates the average salary for each department.

---

# Q14. Find Departments Having More Than 2 Employees

### SQL Query

```sql
SELECT department,
COUNT(*) AS emp_count
FROM employees
GROUP BY department
HAVING COUNT(*) > 2;
```

### Output

| Department | Employees |
|------------|----------:|
| Finance | 3 |
| HR | 3 |
| IT | 3 |
| Marketing | 3 |
| Sales | 3 |

### Explanation

`HAVING` filters grouped data after `GROUP BY`.

---

# Q15. Find Cities Where the Average Salary is Greater Than 60,000

### SQL Query

```sql
SELECT city,
AVG(salary) AS avg_salary
FROM employees
GROUP BY city
HAVING AVG(salary) > 60000;
```

### Output

| City | Average Salary |
|------|---------------:|
| Mumbai | 68333.33 |
| Pune | 69000.00 |

### Explanation

Only cities whose average salary is above ₹60,000 are displayed.

---

# Q16. Find Departments Whose Total Salary is Greater Than 1,50,000

### SQL Query

```sql
SELECT department,
SUM(salary) AS total_salary
FROM employees
GROUP BY department
HAVING SUM(salary) > 150000;
```

### Output

| Department | Total Salary |
|------------|-------------:|
| Finance | 222000 |
| IT | 183000 |
| Marketing | 189000 |
| Sales | 208000 |

### Explanation

`HAVING` filters departments based on total salary.

---

# Q17. Find the Total Salary of Active Employees in Each Department

### SQL Query

```sql
SELECT department,
SUM(salary) AS active_emp_total_salary
FROM employees
WHERE status='Active'
GROUP BY department;
```

### Output

| Department | Total Salary |
|------------|-------------:|
| Finance | 222000 |
| HR | 103000 |
| IT | 183000 |
| Marketing | 189000 |
| Sales | 60000 |

### Explanation

The `WHERE` clause filters only active employees before grouping.

---

# Q18. Find the Total Number of Inactive Employees in Each City

### SQL Query

```sql
SELECT city,
COUNT(*) AS total_inactive_emp
FROM employees
WHERE status='Inactive'
GROUP BY city;
```

### Output

| City | Inactive Employees |
|------|-------------------:|
| Delhi | 2 |
| Pune | 1 |

### Explanation

Counts inactive employees city-wise.

---

# Q19. Find the Department with the Highest Total Salary

### SQL Query

```sql
SELECT department,
SUM(salary) AS total_highest_salary
FROM employees
GROUP BY department
ORDER BY SUM(salary) DESC
LIMIT 1;
```

### Output

| Department | Total Salary |
|------------|-------------:|
| Finance | 222000 |

### Explanation

`ORDER BY DESC` sorts the departments by total salary, and `LIMIT 1` returns the highest one.

---

# Q20. Find the City with the Maximum Number of Employees

### SQL Query

```sql
SELECT city,
COUNT(*) AS emp_counts
FROM employees
GROUP BY city
ORDER BY COUNT(*) DESC
LIMIT 1;
```

### Output

| City | Employees |
|------|----------:|
| Delhi | 5 |

### Explanation

Delhi has the highest number of employees.

---

# Q21. Find the Total Number of Employees in Each City

### SQL Query

```sql
SELECT city,
COUNT(*) AS total_emp
FROM employees
GROUP BY city;
```

### Output

| City | Employees |
|------|----------:|
| Chandigarh | 2 |
| Delhi | 5 |
| Mumbai | 6 |
| Pune | 2 |

### Explanation

Counts employees city-wise.

---

# Q22. Find the Total Salary Paid in Each City

### SQL Query

```sql
SELECT city,
SUM(salary) AS total_salary_paid
FROM employees
GROUP BY city;
```

### Output

| City | Total Salary |
|------|-------------:|
| Chandigarh | 117000 |
| Delhi | 285000 |
| Mumbai | 410000 |
| Pune | 138000 |

### Explanation

Calculates total salary for every city.

---

# Q23. Find Departments Where Average Salary is Greater Than 65,000

### SQL Query

```sql
SELECT department,
AVG(salary) AS avg_salary
FROM employees
GROUP BY department
HAVING AVG(salary) > 65000;
```

### Output

| Department | Average Salary |
|------------|---------------:|
| Finance | 74000.00 |
| Sales | 69333.33 |

### Explanation

Returns only departments whose average salary exceeds ₹65,000.

---

# Q24. Find Cities Having More Than 3 Employees

### SQL Query

```sql
SELECT city,
COUNT(*) AS emp_counts
FROM employees
GROUP BY city
HAVING COUNT(*) > 3;
```

### Output

| City | Employees |
|------|----------:|
| Delhi | 5 |
| Mumbai | 6 |

### Explanation

Displays cities with more than three employees.

---

# Q25. Find the Department Having the Maximum Number of Active Employees

### SQL Query

```sql
SELECT department,
COUNT(*) AS max_active_emp
FROM employees
WHERE status='Active'
GROUP BY department
ORDER BY COUNT(*) DESC
LIMIT 1;
```

### Output

| Department | Active Employees |
|------------|-----------------:|
| Finance | 3 |

> **Note:** IT and Marketing also have **3 active employees**. Since `LIMIT 1` is used, MySQL returns only one of the tied departments.

### Explanation

Finds the department with the highest count of active employees.

---

# Q26. Find How Many Employees Have a Manager Assigned

### SQL Query

```sql
SELECT COUNT(*) AS manager_assigned
FROM employees
WHERE manager_id IS NOT NULL;
```

### Output

| Manager Assigned |
|-----------------:|
| 10 |

### Explanation

Counts employees whose `manager_id` is not `NULL`, meaning they have a manager assigned.

---

---

# 📝 Practice Questions

Use the `employees` table to solve the following SQL problems on your own.

1. Find the total salary of employees in each city, but display only those cities where the total salary is greater than **1,50,000**.

2. Find the number of active employees in each department, but display only departments having at least **3 active employees**.

3. Find the highest salary in each city and sort the result in **descending order** of the highest salary.

4. Find the average salary of employees in each department, but exclude employees whose status is **'Inactive'**.

5. Find the department that has the **lowest average salary** in the company.

## ⭐ THANK YOU FOR VISITING THIS REPOSITORY!

IF YOU FOUND THIS PROJECT HELPFUL, PLEASE CONSIDER GIVING IT A ⭐ STAR. YOUR SUPPORT IS GREATLY APPRECIATED!

---
