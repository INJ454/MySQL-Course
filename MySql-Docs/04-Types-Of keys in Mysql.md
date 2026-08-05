# 🔑 MYSQL KEY CONSTRAINTS — COMPLETE GUIDE

Easy guide to MySQL Primary Key, Foreign Key, Unique Key, and Composite Key. ✅
---

# 📑 Table of Contents

* 🗄️ Create Database
* 🔑 Primary Key
* 🔗 Foreign Key
* ⭐ Unique Key
* 🧩 Composite Key
* 📊 Difference Between Keys
* 🎯 Interview Definitions

---

# 🗄️ Create Database

```sql
CREATE DATABASE company_db08;
USE company_db08;
```

---

# 🔑 Primary Key (PK)

### 📖 Definition

A **Primary Key** uniquely identifies each record in a table.

### ✅ Features

* ✅ Every value must be unique.
* ❌ NULL values are not allowed.
* ❌ Duplicate values are not allowed.
* ✅ One Primary Key per table.

---

## 💻 Syntax

```sql
CREATE TABLE students(
    student_id INT PRIMARY KEY,
    student_name VARCHAR(50),
    age INT
);
```

---

## 📥 Insert Data

```sql
INSERT INTO students VALUES
(101,'Tarun',22),
(102,'Rahul',23),
(103,'Aman',21);
```

---

## 📋 Table Schema

| Column       | Data Type   | Constraint  |
| ------------ | ----------- | ----------- |
| student_id   | INT         | PRIMARY KEY |
| student_name | VARCHAR(50) | -           |
| age          | INT         | -           |

---

## 📊 Output

| student_id | student_name | age |
| ---------- | ------------ | --: |
| 101        | Tarun        |  22 |
| 102        | Rahul        |  23 |
| 103        | Aman         |  21 |

---

## ❌ Duplicate Primary Key

```sql
INSERT INTO students VALUES
(101,'Rohit',24);
```

### 🚫 Output

```text
Error Code: 1062
Duplicate entry '101' for key 'students.PRIMARY'
```

---

# 🔗 Foreign Key (FK)

### 📖 Definition

A **Foreign Key** links a child table with a parent table.

### ✅ Features

* 🔗 Creates relationships between tables.
* ✅ Maintains referential integrity.
* ❌ Prevents invalid parent references.
* ✅ Multiple Foreign Keys can exist in a table.

---

## 👨‍💼 Parent Table

```sql
CREATE TABLE departments(
    dept_id INT PRIMARY KEY,
    dept_name VARCHAR(50)
);
```

### 📥 Insert Data

```sql
INSERT INTO departments VALUES
(1,'IT'),
(2,'HR'),
(3,'Finance');
```

### 📋 Schema

| Column    | Data Type   | Constraint  |
| --------- | ----------- | ----------- |
| dept_id   | INT         | PRIMARY KEY |
| dept_name | VARCHAR(50) | -           |

### 📊 Output

| dept_id | dept_name |
| ------- | --------- |
| 1       | IT        |
| 2       | HR        |
| 3       | Finance   |

---

## 👨‍💻 Child Table

```sql
CREATE TABLE employees(
    emp_id INT PRIMARY KEY,
    emp_name VARCHAR(50),
    dept_id INT,
    FOREIGN KEY(dept_id)
    REFERENCES departments(dept_id)
);
```

### 📥 Insert Data

```sql
INSERT INTO employees VALUES
(1,'Tarun',1),
(2,'Rahul',2),
(3,'Aman',3);
```

### 📋 Schema

| Column   | Data Type   | Constraint  |
| -------- | ----------- | ----------- |
| emp_id   | INT         | PRIMARY KEY |
| emp_name | VARCHAR(50) | -           |
| dept_id  | INT         | FOREIGN KEY |

### 📊 Output

| emp_id | emp_name | dept_id |
| ------ | -------- | ------: |
| 1      | Tarun    |       1 |
| 2      | Rahul    |       2 |
| 3      | Aman     |       3 |

---

## ❌ Invalid Foreign Key

```sql
INSERT INTO employees VALUES
(4,'Rohit',10);
```

### 🚫 Output

```text
Error Code: 1452

Cannot add or update a child row:
a foreign key constraint fails
```

---

# ⭐ Unique Key (UK)

### 📖 Definition

A **Unique Key** ensures that all values in a column are unique.

### ✅ Features

* ❌ Duplicate values are not allowed.
* ✅ NULL values are allowed.
* ✅ Multiple Unique Keys can exist.

---

## 💻 Syntax

```sql
CREATE TABLE users(
    user_id INT PRIMARY KEY,
    email VARCHAR(100) UNIQUE,
    name VARCHAR(50)
);
```

---

## 📥 Insert Data

```sql
INSERT INTO users VALUES
(1,'tarun@gmail.com','Tarun'),
(2,'rahul@gmail.com','Rahul');
```

---

## 📋 Schema

| Column  | Data Type    | Constraint  |
| ------- | ------------ | ----------- |
| user_id | INT          | PRIMARY KEY |
| email   | VARCHAR(100) | UNIQUE      |
| name    | VARCHAR(50)  | -           |

---

## 📊 Output

| user_id | email                                     | name  |
| ------: | ----------------------------------------- | ----- |
|       1 | [tarun@gmail.com](mailto:tarun@gmail.com) | Tarun |
|       2 | [rahul@gmail.com](mailto:rahul@gmail.com) | Rahul |

---

## ❌ Duplicate Email

```sql
INSERT INTO users VALUES
(3,'tarun@gmail.com','Aman');
```

### 🚫 Output

```text
Error Code: 1062

Duplicate entry 'tarun@gmail.com'
for key 'users.email'
```

---

# 🧩 Composite Key

### 📖 Definition

A **Composite Key** uses two or more columns together as a Primary Key.

### ✅ Features

* ✅ Uses multiple columns.
* ❌ Duplicate combinations are not allowed.
* ✅ Commonly used in junction tables.

---

## 💻 Syntax

```sql
CREATE TABLE students_course(
    student_id INT,
    course_id INT,
    marks INT,
    PRIMARY KEY(student_id,course_id)
);
```

---

## 📥 Insert Data

```sql
INSERT INTO students_course VALUES
(101,1,90),
(102,2,80),
(103,3,75);
```

---

## 📋 Schema

| Column     | Data Type | Constraint   |
| ---------- | --------- | ------------ |
| student_id | INT       | Composite PK |
| course_id  | INT       | Composite PK |
| marks      | INT       | -            |

---

## 📊 Output

| student_id | course_id | marks |
| ---------: | --------: | ----: |
|        101 |         1 |    90 |
|        102 |         2 |    80 |
|        103 |         3 |    75 |

---

## ❌ Duplicate Combination

```sql
INSERT INTO students_course VALUES
(101,1,95);
```

### 🚫 Output

```text
Error Code: 1062

Duplicate entry '101-1'
for key 'students_course.PRIMARY'
```

---

# 📊 Difference Between Keys

| Feature           | 🔑 Primary Key | 🔗 Foreign Key | ⭐ Unique Key       | 🧩 Composite Key           |
| ----------------- | -------------- | -------------- | ------------------ | -------------------------- |
| Unique Values     | ✅ Yes          | ❌ No           | ✅ Yes              | ✅ Combination              |
| NULL Allowed      | ❌ No           | ✅ Yes          | ✅ Yes              | ❌ No                       |
| Duplicate Allowed | ❌ No           | ✅ Yes          | ❌ No               | ❌ Combination              |
| Purpose           | Identify rows  | Link tables    | Prevent duplicates | Multiple-column identifier |

---

# 🎯 Interview One-Line Definitions

| Key              | Definition                                                                |
| ---------------- | ------------------------------------------------------------------------- |
| 🔑 Primary Key   | Uniquely identifies each row and does not allow NULL or duplicate values. |
| 🔗 Foreign Key   | Links a child table to a parent table.                                    |
| ⭐ Unique Key     | Ensures all values in a column are unique.                                |
| 🧩 Composite Key | A key made from two or more columns together.                             |

---

# 🎉 Conclusion

You have learned:

* ✅ Primary Key
* ✅ Foreign Key
* ✅ Unique Key
* ✅ Composite Key
* ✅ Table Schemas
* ✅ Sample Data
* ✅ Outputs
* ✅ Error Demonstrations
* ✅ Interview Definitions

---


## ⭐ THANK YOU FOR VISITING THIS REPOSITORY!

IF YOU FOUND THIS PROJECT HELPFUL, PLEASE CONSIDER GIVING IT A ⭐ STAR. YOUR SUPPORT IS GREATLY APPRECIATED!


## ⭐ Happy Learning MySQL!
