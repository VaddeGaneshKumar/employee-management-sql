# 🧑‍💼 Employee Management System (PostgreSQL)

## 📌 Project Overview

This project is a **relational database system** built using PostgreSQL to manage employee data, departments, and attendance records. It demonstrates real-world SQL skills including joins, subqueries, aggregation, and database design.

---

## 🚀 Features

* Manage employee records
* Track department details and managers
* Maintain attendance data
* Perform advanced SQL queries for insights
* Use of views for simplified reporting

---

## 🧠 Concepts Used

* Relational Database Design
* Primary Key & Foreign Key
* Normalization (1NF, 2NF, 3NF)
* SQL Joins (INNER, LEFT, RIGHT)
* Aggregation (COUNT, AVG, MAX)
* Subqueries (Correlated & Non-correlated)
* Views
* Index basics

---

## 🗂️ Database Schema

### 👨‍💼 Employees Table

* emp_id (Primary Key)
* emp_name
* salary
* dept_id (Foreign Key)

### 🏢 Departments Table

* dept_id (Primary Key)
* dept_name
* manager_name

### 📊 Attendance Table

* att_id (Primary Key)
* emp_id (Foreign Key)
* att_date
* status (Present / Absent)

---

## ⚙️ Setup Instructions

1. Install PostgreSQL
2. Open pgAdmin or psql
3. Create a database:

```sql
CREATE DATABASE employee_db;
```

4. Run the table creation scripts (see below)

---

## 🏗️ Table Creation

```sql
CREATE TABLE departments (
    dept_id INT PRIMARY KEY,
    dept_name VARCHAR(50),
    manager_name VARCHAR(50)
);

CREATE TABLE employees (
    emp_id INT PRIMARY KEY,
    emp_name VARCHAR(50),
    salary INT,
    dept_id INT,
    FOREIGN KEY (dept_id) REFERENCES departments(dept_id)
);

CREATE TABLE attendance (
    att_id INT PRIMARY KEY,
    emp_id INT,
    att_date DATE,
    status VARCHAR(10),
    FOREIGN KEY (emp_id) REFERENCES employees(emp_id)
);
```

---

## 📥 Sample Data

```sql
INSERT INTO departments VALUES
(1, 'HR', 'Suresh'),
(2, 'IT', 'Kavitha'),
(3, 'Finance', 'Ramesh'),
(4, 'Marketing', 'Divya');

INSERT INTO employees VALUES
(101, 'Ravi', 30000, 1),
(102, 'Priya', 55000, 2),
(103, 'Arun', 45000, 3),
(104, 'Sneha', 60000, 2),
(105, 'Kiran', 35000, 4);
```

---

## 🔍 Key Queries

### 1. Employee + Department + Manager

```sql
SELECT e.emp_name, d.dept_name, d.manager_name
FROM employees e
JOIN departments d ON e.dept_id = d.dept_id;
```

---

### 2. Department-wise Employee Count

```sql
SELECT d.dept_name, COUNT(e.emp_id) AS total_emp
FROM departments d
LEFT JOIN employees e ON d.dept_id = e.dept_id
GROUP BY d.dept_name;
```

---

### 3. Employees Above Department Average Salary

```sql
SELECT e.emp_name, e.salary
FROM employees e
WHERE e.salary > (
    SELECT AVG(e2.salary)
    FROM employees e2
    WHERE e2.dept_id = e.dept_id
);
```

---

### 4. Create View

```sql
CREATE VIEW employee_summary AS
SELECT e.emp_name, d.dept_name, e.salary
FROM employees e
JOIN departments d ON e.dept_id = d.dept_id;
```

---

## 📊 Future Improvements

* Add triggers
* Add stored procedures
* Build API using Django or Flask
* Connect with Power BI dashboard

---

## 💼 Resume Highlight

> Developed a PostgreSQL-based Employee Management System implementing relational database design, joins, subqueries, and views to manage and analyze employee data.

---

## 👨‍💻 Author

Ganesh Kumar
