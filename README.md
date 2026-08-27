<div align="center">
  <h1 align="center">MYSQL CHEAT SHEET</h1>

  <p align="center">JUST A CHEAT SHEET</p><br>
  <p align="center">BY: Raul A. Generoso lll</p><br>
</div>

<details>
  <summary>📚 Table of Contents</summary>
  <ol>
    <li><a href="#first-of-all-time-show-the-databases">FIRST OF ALL TIME SHOW THE DATABASES;</a></li>
    <li><a href="#then-use-the-word-use-to-use-the-databases">// THEN USE THE WORD "USE" TO USE THE DATABASES;</a></li>
    <li><a href="#where-going-to-use-crud-for-the-query">// WHERE GOING TO USE CRUD FOR THE QUERY</a></li>
  </ol>
</details>



CHEAT SHEET

# MariaDB / MySQL CLI Cheat Sheet

A comprehensive CLI guide for managing MySQL/MariaDB databases, executing full CRUD operations, filtering data, and cleaning up structures.

---

##  1. Database Management

### View Existing Databases
```sql
SHOW DATABASES;
```
**Output:**
```text
+--------------------+
| Database           |
+--------------------+
| information_schema |
| mysql              |
| performance_schema |
| sys                |
+--------------------+
4 rows in set (0.001 sec)
```

### Create a New Database
```sql
CREATE DATABASE students;
```
**Output:**
```text
MariaDB [(none)]> CREATE DATABASE students;
Query OK, 1 row affected (0.001 sec)
```

### Confirm Database Creation
```sql
SHOW DATABASES;
```
**Output:**
```text
+--------------------+
| Database           |
+--------------------+
| information_schema |
| mysql              |
| performance_schema |
| students           |
| sys                |
+--------------------+
5 rows in set (0.000 sec)
```

### Select active Database
```sql
USE students;
```
**Output:**
```text
MariaDB [(none)]> USE students;
Database changed
```

---

##  2. Table Creation & Inspection

### Check Existing Tables
```sql
SHOW TABLES;
```
**Output:**
```text
MariaDB [students]> SHOW TABLES;
Empty set (0.001 sec)
```

### Create `STUDENT` Table
```sql
CREATE TABLE STUDENT (
    student_id INT PRIMARY KEY AUTO_INCREMENT,
    first_name VARCHAR(50) NOT NULL,
    last_name VARCHAR(50) NOT NULL,
    email VARCHAR(100) UNIQUE NOT NULL,
    date_of_birth DATE,
    enrollment_date DATE DEFAULT (CURRENT_DATE),
    gpa DECIMAL(3, 2)
);
```
**Output:**
```text
MariaDB [students]> CREATE TABLE STUDENT (
    ->     student_id INT PRIMARY KEY AUTO_INCREMENT,
    ->     first_name VARCHAR(50) NOT NULL,
    ->     last_name VARCHAR(50) NOT NULL,
    ->     email VARCHAR(100) UNIQUE NOT NULL,
    ->     date_of_birth DATE,
    ->     enrollment_date DATE DEFAULT (CURRENT_DATE),
    ->     gpa DECIMAL(3, 2)
    -> );
Query OK, 0 rows affected (0.061 sec)
```

### Inspect Table Schema
```sql
DESCRIBE STUDENT;
```
**Output:**
```text
+-----------------+---------------+------+-----+-------------------+----------------+
| Field           | Type          | Null | Key | Default           | Extra          |
+-----------------+---------------+------+-----+-------------------+----------------+
| student_id      | int(11)       | NO   | PRI | NULL              | auto_increment |
| first_name      | varchar(50)   | NO   |     | NULL              |                |
| last_name       | varchar(50)   | NO   |     | NULL              |                |
| email           | varchar(100)  | NO   | UNI | NULL              |                |
| date_of_birth   | date          | YES  |     | NULL              |                |
| enrollment_date | date          | YES  |     | curdate()         |                |
| gpa             | decimal(3,2)  | YES  |     | NULL              |                |
+-----------------+---------------+------+-----+-------------------+----------------+
7 rows in set (0.012 sec)
```

---

##  3. Data Operations (CRUD)

### Create (Insert Records)
```sql
INSERT INTO STUDENT (first_name, last_name, email, date_of_birth, gpa)
VALUES 
('Jane', 'Doe', 'jane.doe@example.com', '2002-05-15', 3.85),
('John', 'Smith', 'john.smith@example.com', '2001-11-20', 2.90);
```
**Output:**
```text
MariaDB [students]> INSERT INTO STUDENT (first_name, last_name, email, date_of_birth, gpa)
    -> VALUES 
    -> ('Jane', 'Doe', 'jane.doe@example.com', '2002-05-15', 3.85),
    -> ('John', 'Smith', 'john.smith@example.com', '2001-11-20', 2.90);
Query OK, 2 rows affected (0.005 sec)
Records: 2  Duplicates: 0  Warnings: 0
```

### Read (Query Records)

#### Fetch All Records
```sql
SELECT * FROM STUDENT;
```
**Output:**
```text
+------------+------------+-----------+------------------------+---------------+-----------------+------+
| student_id | first_name | last_name | email                  | date_of_birth | enrollment_date | gpa  |
+------------+------------+-----------+------------------------+---------------+-----------------+------+
|          1 | Jane       | Doe       | jane.doe@example.com   | 2002-05-15    | 2026-08-27      | 3.85 |
|          2 | John       | Smith     | john.smith@example.com | 2001-11-20    | 2026-08-27      | 2.90 |
+------------+------------+-----------+------------------------+---------------+-----------------+------+
2 rows in set (0.000 sec)
```

#### Filter Data with `WHERE` Clause
```sql
SELECT first_name, last_name, gpa FROM STUDENT WHERE gpa > 3.00;
```
**Output:**
```text
+------------+-----------+------+
| first_name | last_name | gpa  |
+------------+-----------+------+
| Jane       | Doe       | 3.85 |
+------------+-----------+------+
1 row in set (0.001 sec)
```

### Update (Modify Records)
```sql
UPDATE STUDENT 
SET gpa = 3.15 
WHERE student_id = 2;
```
**Output:**
```text
MariaDB [students]> UPDATE STUDENT 
    -> SET gpa = 3.15 
    -> WHERE student_id = 2;
Query OK, 1 row affected (0.004 sec)
Rows matched: 1  Changed: 1  Warnings: 0
```

### Delete (Remove Specific Records)
```sql
DELETE FROM STUDENT 
WHERE student_id = 2;
```
**Output:**
```text
MariaDB [students]> DELETE FROM STUDENT 
    -> WHERE student_id = 2;
Query OK, 1 row affected (0.003 sec)
```

---

##  4. Cleanup Commands

### Truncate (Reset Table Data & AUTO_INCREMENT)
Removes all rows in the table while keeping the table structure intact. Resets `AUTO_INCREMENT` back to `1`.

```sql
TRUNCATE TABLE STUDENT;
```
**Output:**
```text
MariaDB [students]> TRUNCATE TABLE STUDENT;
Query OK, 0 rows affected (0.025 sec)
```

### Drop (Delete Table or Database)

#### Drop Table
```sql
DROP TABLE STUDENT;
```
**Output:**
```text
MariaDB [students]> DROP TABLE STUDENT;
Query OK, 0 rows affected (0.015 sec)
```

#### Drop Database
```sql
DROP DATABASE students;
```
**Output:**
```text
MariaDB [(none)]> DROP DATABASE students;
Query OK, 0 rows affected (0.018 sec)
    
