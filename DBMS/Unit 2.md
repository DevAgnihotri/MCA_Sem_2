**Relational Algebra & DBMS PYQs:**

1. [Define referential integrity constraint. Explain its importance and how it is implemented in SQL.](#22-referential-integrity)
2. [What is domain integrity?](#24-domain-constraints)
3. [Write the relational algebra expression: For relation Employee(EID, Ename, City), find the names of employees who live in Delhi or Mumbai.](#3-relational-algebra)

**SQL PYQs Summary:**

1. [Define joins in SQL. Briefly explain its types. Also, discuss the importance of triggers in SQL with an example.](#joins-in-sql)
2. [Discuss different types of SQL commands. Explain joins, aggregate functions, and sub-queries with neat examples.](#types-of-sql-commands)
3. [Explain the division operator with an example. How can it be implemented using other relational algebraic operators?](#division-operator-in-sqlrelational-algebra)
4. [Write the SQL command to create a table named STUDENT with constraints: Roll (Primary Key, must start with ‘S’), Name (Not Null), DOB, Email (Unique), DOR (>= DOB).](#example-table-creation-and-queries)
5. [What is the difference between a trigger and a procedure? Write a trigger that logs updated salary in the Employee_Backup table.](#triggers-in-sql)
6. [Write SQL queries on EMP and DEPT tables for joins, filters, and conditions.](#example-table-creation-and-queries)
7. [Create a table Employee(Emp_id, Emp_name, Emp_add, Emp_basicpay) and insert some records. Create another table Emp_detail(Emp_name, Emp_add) from Employee using a SELECT statement.](#example-table-creation-and-queries)
8. [What are sub-queries?](#queries-and-subqueries)
9. [Define a cursor in PL/SQL.](#cursors-in-plsql)
10. [Create the tables Supplier(SNo, SName, City), Parts(PNo, Pname, Color, City), and Shipment(SNo, PNo, Quantity). Answer queries: total suppliers, suppliers supplying parts, part numbers, change red to black.](#example-table-creation-and-queries)

---

# Relational Data Model & Relational Algebra (with PYQs)

This note covers all key concepts of the Relational Data Model, Integrity Constraints, Relational Algebra, and Relational Calculus, with clear explanations and answers to previous year questions (PYQs).

---

## 1. Relational Data Model

The **Relational Data Model** is a way to organize data in tables (called relations). Each table consists of rows (records/tuples) and columns (attributes/fields). It is the most widely used model in modern databases.

- **Table (Relation):** Collection of rows and columns.
- **Row (Tuple):** Represents a single record.
- **Column (Attribute):** Represents a property of the record.
- **Example:**

| EID | Ename | City   |
| --- | ----- | ------ |
| 101 | Rahul | Delhi  |
| 102 | Priya | Mumbai |
| 103 | Aman  | Pune   |

---

## 2. Integrity Constraints

**Integrity Constraints** are rules that ensure the accuracy and consistency of data in a database. They prevent invalid data from being entered.

### Types of Integrity Constraints:

- **Entity Integrity** (Table must have Primary key, Unique, Not Null)
- **Referential Integrity** (F key in a table matches P key in another)
- **Key Constraints**
- **Domain Constraints**

---

### 2.1 Entity Integrity

**Entity Integrity** ensures that every table has a primary key and that the value of the primary key is unique and not NULL for any row.

- **Why?** To uniquely identify each record in a table.
- **Example:** In the Employee table, EID is the primary key and must be unique and not NULL.

---

### 2.2 Referential Integrity

**PYQ 1: Define referential integrity constraint. Explain its importance and how it is implemented in SQL.**

**Definition:**
Referential Integrity ensures that a foreign key in one table matches a primary key in another table, or is NULL. It maintains valid links between related tables.

- **Importance:**

  - Prevents orphan records (records that reference non-existent rows).
  - Maintains consistency across tables.
  - Ensures relationships between tables are valid.

- **Implementation in SQL:**
  - Use the `FOREIGN KEY` constraint.
  - Example:

```sql
CREATE TABLE Department (
  DeptID INT PRIMARY KEY,
  DeptName VARCHAR(50)
);

CREATE TABLE Employee (
  EID INT PRIMARY KEY,
  Ename VARCHAR(50),
  DeptID INT,
  FOREIGN KEY (DeptID) REFERENCES Department(DeptID)
);
```

- Here, `DeptID` in Employee must exist in Department.

---

### 2.3 Key Constraints

**Key Constraints** ensure that certain columns (keys) uniquely identify rows in a table.

- **Primary Key:** Uniquely identifies each row. Cannot be NULL.
- **Foreign Key:** Refers to the primary key in another table.
- **Candidate Key:** Any column that can be a primary key.
- **Super Key:** Any set of columns that uniquely identifies a row.

---

### 2.4 Domain Constraints

**PYQ 2: What is domain integrity?**

**Definition:**
Domain Constraints (Domain Integrity) specify that the value of each attribute must be from a predefined domain (set of valid values).

- **Example:**
  - Age must be an integer between 0 and 120.
  - City must be one of: Delhi, Mumbai, Pune, etc.
- **SQL Implementation:**
  - Use data types and `CHECK` constraints.

```sql
CREATE TABLE Student (
  RollNo INT,
  Name VARCHAR(50),
  Age INT CHECK (Age >= 0 AND Age <= 120)
);
```

---

## 3. Relational Algebra

**Relational Algebra** is a set of operations used to query and manipulate data in relational databases. It forms the theoretical foundation of SQL.

### Main Operations:

- **SELECT (σ):** Selects rows that satisfy a condition.
- **PROJECT (π):** Selects specific columns.
- **UNION (∪):** Combines rows from two tables.
- **SET DIFFERENCE (−):** Rows in one table but not in another.
- **CARTESIAN PRODUCT (×):** Combines every row of one table with every row of another.
- **JOIN:** Combines related rows from two tables.

---

**PYQ 3: Write the relational algebra expression: For relation Employee(EID, Ename, City), find the names of employees who live in Delhi or Mumbai.**

**Answer:**

- **Relational Algebra Expression:**

```
π_Ename (σ_City = 'Delhi' ∨ City = 'Mumbai' (Employee))
```

- **Explanation:**
  - `σ_City = 'Delhi' ∨ City = 'Mumbai' (Employee)` selects rows where City is Delhi or Mumbai.
  - `π_Ename` projects only the Ename column.

---

## 4. Relational Calculus

**Relational Calculus** is a non-procedural query language. It specifies what to retrieve rather than how to retrieve it.

### Types:

- **Tuple Relational Calculus (TRC):** Uses tuples (rows) as variables.
- **Domain Relational Calculus (DRC):** Uses domain values (column values) as variables.

---

### 4.1 Tuple Relational Calculus (TRC)

- **Form:** `{ t | P(t) }` where t is a tuple and P(t) is a condition.
- **Example:**
  - Find names of employees in Delhi:
    - `{ t.Ename | Employee(t) AND (t.City = 'Delhi') }`

---

### 4.2 Domain Relational Calculus (DRC)

- **Form:** `{ <d1, d2, ...> | P(d1, d2, ...) }` where d1, d2 are domain variables.
- **Example:**
  - Find names of employees in Mumbai:
    - `{ e | ∃id ∃c (Employee(id, e, c) AND (c = 'Mumbai')) }`

---

# Introduction to SQL (with PYQs)

## What is SQL?

**SQL (Structured Query Language)** is a standard language used to manage and manipulate relational databases. It allows users to create, modify, and query data stored in tables.

---

## Characteristics of SQL

- **Simple and easy to learn**
- **Non-procedural**: You specify what you want, not how to get it
- **Standardized**: Used in almost all relational databases (MySQL, Oracle, SQL Server, PostgreSQL)
- **Supports data definition, manipulation, and control**
- **Can handle large amounts of data efficiently**

## Advantages of SQL

- **Universal language for databases**
- **Flexible and powerful**
- **Supports complex queries and joins**
- **Allows for data security and integrity**
- **Can be embedded in other programming languages**

---

## SQL Data Types and Literals

**Data Types:**

- `INT`, `FLOAT`, `DECIMAL` – Numbers
- `CHAR`, `VARCHAR` – Text
- `DATE`, `TIME`, `DATETIME` – Dates and times
- `BOOLEAN` – True/False

**Literals:**

- Numbers: `123`, `45.67`
- Strings: `'John'`, `'2025-07-16'`

---

## Types of SQL Commands

**PYQ: Discuss different types of SQL commands. Explain joins, aggregate functions, and sub-queries with neat examples.**

SQL commands are grouped into:

- **DDL (Data Definition Language):** `CREATE`, `ALTER`, `DROP`, `TRUNCATE`
- **DML (Data Manipulation Language):** `SELECT`, `INSERT`, `UPDATE`, `DELETE`
- **DCL (Data Control Language):** `GRANT`, `REVOKE`
- **TCL (Transaction Control Language):** `COMMIT`, `ROLLBACK`, `SAVEPOINT`

| Command Type | Purpose             | Example                  |
| ------------ | ------------------- | ------------------------ |
| DDL          | Define structure    | CREATE TABLE Student ... |
| DML          | Manipulate data     | INSERT INTO Student ...  |
| DCL          | Control access      | GRANT SELECT ON ...      |
| TCL          | Manage transactions | COMMIT; ROLLBACK;        |

---

## SQL Operators and Their Procedure

- **Arithmetic Operators:** `+`, `-`, `*`, `/`
- **Comparison Operators:** `=`, `<>`, `>`, `<`, `>=`, `<=`
- **Logical Operators:** `AND`, `OR`, `NOT`
- **Set Operators:** `UNION`, `INTERSECT`, `MINUS`

---

## Tables, Views, and Indexes

- **Table:** Main storage structure for data
- **View:** Virtual table based on a query
- **Index:** Improves speed of data retrieval

**Example:**

```sql
CREATE TABLE Employee (
  Emp_id INT PRIMARY KEY,
  Emp_name VARCHAR(50),
  Emp_add VARCHAR(100),
  Emp_basicpay DECIMAL(10,2)
);

CREATE VIEW Emp_detail AS
SELECT Emp_name, Emp_add FROM Employee;

CREATE INDEX idx_emp_name ON Employee(Emp_name);
```

---

## Queries and Subqueries

- **Query:** Statement to retrieve data
- **Subquery:** Query inside another query

**PYQ: What are sub-queries?**

- Sub-queries are queries nested inside another SQL query, often used in `WHERE`, `FROM`, or `SELECT` clauses.
- **Example:**

```sql
SELECT Emp_name FROM Employee WHERE Emp_basicpay > (SELECT AVG(Emp_basicpay) FROM Employee);
```

---

## Aggregate Functions

- **SUM()**: Total
- **AVG()**: Average
- **COUNT()**: Number of rows
- **MAX()**: Maximum value
- **MIN()**: Minimum value

**Example:**

```sql
SELECT COUNT(*) FROM Employee;
SELECT AVG(Emp_basicpay) FROM Employee;
```

---

## Insert, Update, and Delete Operations

- **INSERT:** Add new records
- **UPDATE:** Modify existing records
- **DELETE:** Remove records

**Example:**

```sql
INSERT INTO Employee VALUES (101, 'John', 'Delhi', 50000);
UPDATE Employee SET Emp_basicpay = 55000 WHERE Emp_id = 101;
DELETE FROM Employee WHERE Emp_id = 101;
```

---

## Joins in SQL

**PYQ: Define joins in SQL. Briefly explain its types.**

**Definition:**

A **join** in SQL is used to combine rows from two or more tables based on a related column between them. Joins help retrieve data that is spread across multiple tables by linking them through common fields.

### Types of Joins (with simple explanations and examples):

- **INNER JOIN:** Returns only the rows where there is a match in both tables.
  - *Example:* Get employees with their department names.
    ```sql
    SELECT E.Emp_name, D.Dept_name
    FROM Employee E
    INNER JOIN Department D ON E.Dept_id = D.Dept_id;
    ```

- **LEFT JOIN (LEFT OUTER JOIN):** Returns all rows from the left table, and the matched rows from the right table. If there is no match, NULLs are shown for right table columns.
  - *Example:* List all employees and their department names (if any).
    ```sql
    SELECT E.Emp_name, D.Dept_name
    FROM Employee E
    LEFT JOIN Department D ON E.Dept_id = D.Dept_id;
    ```

- **RIGHT JOIN (RIGHT OUTER JOIN):** Returns all rows from the right table, and the matched rows from the left table. If there is no match, NULLs are shown for left table columns.
  - *Example:* List all departments and their employees (if any).
    ```sql
    SELECT E.Emp_name, D.Dept_name
    FROM Employee E
    RIGHT JOIN Department D ON E.Dept_id = D.Dept_id;
    ```

- **FULL JOIN (FULL OUTER JOIN):** Returns all rows when there is a match in either left or right table. If there is no match, NULLs are shown for missing matches.
  - *Example:* List all employees and departments, matching where possible.
    ```sql
    SELECT E.Emp_name, D.Dept_name
    FROM Employee E
    FULL OUTER JOIN Department D ON E.Dept_id = D.Dept_id;
    ```
  - *Real Example:*
    Suppose:
    ```
    Employee
    +---------+-----------+----------+
    | Emp_id  | Emp_name  | Dept_id  |
    +---------+-----------+----------+
    | 1       | John      | 10       |
    | 2       | Priya     | 20       |
    | 3       | Aman      | NULL     |
    +---------+-----------+----------+

    Department
    +---------+-----------+
    | Dept_id | Dept_name |
    +---------+-----------+
    | 10      | HR        |
    | 30      | IT        |
    +---------+-----------+
    ```
    Result:
    ```
    +-----------+-----------+
    | Emp_name  | Dept_name |
    +-----------+-----------+
    | John      | HR        |
    | Priya     | NULL      |
    | Aman      | NULL      |
    | NULL      | IT        |
    +-----------+-----------+
    ```

- **CROSS JOIN:** Returns the Cartesian product of both tables (every row of the first table combined with every row of the second table).
  - *Example:* Combine every employee with every department.
    ```sql
    SELECT E.Emp_name, D.Dept_name
    FROM Employee E
    CROSS JOIN Department D;
    ```
  - *Real Example:*
    Using the same tables as above, the result is:
    ```
    +-----------+-----------+
    | Emp_name  | Dept_name |
    +-----------+-----------+
    | John      | HR        |
    | John      | IT        |
    | Priya     | HR        |
    | Priya     | IT        |
    | Aman      | HR        |
    | Aman      | IT        |
    +-----------+-----------+
    ```

---

## Set Operators: Union, Intersection, Minus

- **UNION:** Combines results of two queries (removes duplicates)
- **INTERSECT:** Returns common rows
- **MINUS:** Returns rows from first query not in second

**Example:**

```sql
SELECT Emp_name FROM Employee
UNION
SELECT Emp_name FROM RetiredEmployee;
```

---

## Division Operator in SQL/Relational Algebra

**PYQ: Explain the division operator with an example. How can it be implemented using other relational algebraic operators?**

**Definition:**
The division operator finds rows in one table that are related to all rows in another table.

**Example:**

- Find employees who worked on all projects:

Let `Works(Emp_id, Proj_id)` and `Project(Proj_id)`

Relational Algebra:

```
Works ÷ Project
```

**Implementation using other operators:**

- Use `PROJECT`, `SET DIFFERENCE`, and `JOIN` to simulate division.

---

## Cursors in PL/SQL

**PYQ: Define a cursor in PL/SQL.**

**Definition:**
- A **cursor** is a  used to retrive data one row at a time from the result set.
- It allows row by row processing in PL/SQL.

**Example:**

```sql
DECLARE
  CURSOR emp_cursor IS SELECT * FROM Employee;
BEGIN
  FOR emp_rec IN emp_cursor LOOP
    -- process each row
  END LOOP;
END;
```

---

## Triggers in SQL

**PYQ: Discuss the importance of triggers in SQL with an example. What is the difference between a trigger and a procedure? Write a trigger that logs updated salary in the Employee_Backup table.**

**Definition:**
A **trigger** is a special procedure that automatically executes in response to certain events (INSERT, UPDATE, DELETE) on a table.


**Importance of Triggers in SQL:**

- Triggers are special procedures that run automatically when certain events (like INSERT, UPDATE, DELETE) happen on a table.
- They help automate tasks such as logging changes, enforcing business rules, or maintaining audit trails.

**Example of a Trigger:**

Suppose you want to log every salary update in an Employee_Backup table:

```sql
CREATE TABLE Employee_Backup (
  Emp_id INT,
  New_Salary DECIMAL(10,2)
);

CREATE TRIGGER LogSalaryUpdate
AFTER UPDATE OF Emp_basicpay ON Employee
FOR EACH ROW
BEGIN
  INSERT INTO Employee_Backup VALUES (:NEW.Emp_id, :NEW.Emp_basicpay);
END;
```


- **Importance:**
  - Automates actions (logging, validation)
  - Enforces business rules
  - Maintains audit trails

**Difference between Trigger and Procedure:**

- **Trigger:** Runs automatically when an event occurs
- **Procedure:** Must be called explicitly by the user

**Example Trigger:**

```sql
CREATE TABLE Employee_Backup (
  Emp_id INT,
  New_Salary DECIMAL(10,2)
);

CREATE TRIGGER LogSalaryUpdate
AFTER UPDATE OF Emp_basicpay ON Employee
FOR EACH ROW
BEGIN
  INSERT INTO Employee_Backup VALUES (:NEW.Emp_id, :NEW.Emp_basicpay);
END;
```

---

## Procedures in SQL/PL SQL

- **Procedure:** A stored program that can be called to perform operations
- **Example:**

```sql
CREATE PROCEDURE UpdateSalary (IN eid INT, IN newpay DECIMAL)
BEGIN
  UPDATE Employee SET Emp_basicpay = newpay WHERE Emp_id = eid;
END;
```

---

## Example Table Creation and Queries

**PYQ For a relation ClientMaster[Client_No(Varchar, primary key), Name(Varchar, not null), Address1 (Varchar), City (Varchar, default 'Delhi'), Pincode(Number), Bal_Due(Float)], find the SQL queries for following-** 
1. Create the given relation. 
2. Add new field as state in the relation. 
3. Remove the city field from the relation. 
4. Remove the existence of ClientMaster relation. 
5. Rename clientMaster to Client Master. 

Sure! Let's go step by step and **answer both parts (a and b)** in detail.

---

## **a. SQL Queries for the `ClientMaster` Relation**

Given relation:
**ClientMaster\[Client\_No (Varchar, primary key), Name (Varchar, not null), Address1 (Varchar), City (Varchar, default 'Delhi'), Pincode (Number), Bal\_Due (Float)]**

---

### 1. **Create the given relation**

```sql
CREATE TABLE ClientMaster (
    Client_No VARCHAR(20) PRIMARY KEY,
    Name VARCHAR(100) NOT NULL,
    Address1 VARCHAR(255),
    City VARCHAR(50) DEFAULT 'Delhi',
    Pincode NUMERIC(6),
    Bal_Due FLOAT
);
```

---

### 2. **Add new field as `State` in the relation**

```sql
ALTER TABLE ClientMaster
ADD State VARCHAR(50);
```

---

### 3. **Remove the `City` field from the relation**

```sql
ALTER TABLE ClientMaster
DROP COLUMN City;
```

---

### 4. **Remove the existence of `ClientMaster` relation**

```sql
DROP TABLE ClientMaster;
```

---

### 5. **Rename `ClientMaster` to `Client Master`**

> Note: Table names with spaces are **allowed** in SQL, but they must be enclosed in quotes or brackets depending on the RDBMS (like MySQL, PostgreSQL, SQL Server). Still, it's not recommended due to readability issues.

```sql
ALTER TABLE ClientMaster
RENAME TO "Client Master";
```

(If you're using MySQL, you can use: `RENAME TABLE ClientMaster TO \`Client Master\`;\`)

---

## **b. EMP Table Attributes Analysis**

**EMP(Empid, Name, DOB, Address, Passport\_No, License\_No, SSN)**

Let's analyze:

---


**PYQ A table named EMP(Empid, Name, DOB, Address, Passport_No, Lisence_No, SSN) is there. Find out the following: Alternative Keys, Non-key Attributes, Non-Prime attributes, Prime Attribute.** 

### 🔑 **Alternative Keys:**

Alternative keys are candidate keys **other than** the primary key.

Assuming each of the following is **unique** for every employee:

* Passport\_No
* License\_No
* SSN

So, the **candidate keys** are:

* Empid (assumed primary key)
* Passport\_No
* License\_No
* SSN

**➡ Alternative keys:**
`Passport_No`, `License_No`, `SSN`

---

### 🔒 **Non-key Attributes:**

These are attributes **not part of any candidate key**.

So from the table:

* `Name`, `DOB`, `Address`

**➡ Non-key attributes:**
`Name`, `DOB`, `Address`

---

### ❌ **Non-prime Attributes:**

Attributes **not part of any candidate key** = same as non-key attributes.

**➡ Non-prime attributes:**
`Name`, `DOB`, `Address`

---

### ✅ **Prime Attributes:**

Attributes that are **part of any candidate key**.

From earlier:

* `Empid`, `Passport_No`, `License_No`, `SSN`

**➡ Prime attributes:**
`Empid`, `Passport_No`, `License_No`, `SSN`

---

**PYQ: Write the SQL command to create a table named STUDENT with constraints: Roll (Primary Key, must start with ‘S’), Name (Not Null), DOB, Email (Unique), DOR (>= DOB).**

```sql
CREATE TABLE STUDENT (
  Roll VARCHAR(10) PRIMARY KEY CHECK (Roll LIKE 'S%'),
  Name VARCHAR(50) NOT NULL,
  DOB DATE,
  Email VARCHAR(100) UNIQUE,
  DOR DATE CHECK (DOR >= DOB)
);
```

---

**PYQ: Create the tables Supplier(SNo, SName, City), Parts(PNo, Pname, Color, City), and Shipment(SNo, PNo, Quantity). Answer queries: total suppliers, suppliers supplying parts, part numbers, change red to black.**

```sql
CREATE TABLE Supplier (
  SNo INT PRIMARY KEY,
  SName VARCHAR(50),
  City VARCHAR(50)
);

CREATE TABLE Parts (
  PNo INT PRIMARY KEY,
  Pname VARCHAR(50),
  Color VARCHAR(20),
  City VARCHAR(50)
);

CREATE TABLE Shipment (
  SNo INT,
  PNo INT,
  Quantity INT,
  FOREIGN KEY (SNo) REFERENCES Supplier(SNo),
  FOREIGN KEY (PNo) REFERENCES Parts(PNo)
);

-- Total suppliers
SELECT COUNT(*) FROM Supplier;

-- Suppliers supplying parts
SELECT DISTINCT SNo FROM Shipment;

-- Part numbers
SELECT PNo FROM Parts;

-- Change red to black
UPDATE Parts SET Color = 'Black' WHERE Color = 'Red';
```

---

**PYQ: Create a table Employee(Emp_id, Emp_name, Emp_add, Emp_basicpay) and insert some records. Create another table Emp_detail(Emp_name, Emp_add) from Employee using a SELECT statement.**

```sql
CREATE TABLE Employee (
  Emp_id INT PRIMARY KEY,
  Emp_name VARCHAR(50),
  Emp_add VARCHAR(100),
  Emp_basicpay DECIMAL(10,2)
);

INSERT INTO Employee VALUES (1, 'John', 'Delhi', 50000);
INSERT INTO Employee VALUES (2, 'Priya', 'Mumbai', 60000);

CREATE TABLE Emp_detail AS
SELECT Emp_name, Emp_add FROM Employee;
```

---

**PYQ: Write SQL queries on EMP and DEPT tables for joins, filters, and conditions.**

```sql
-- Join
SELECT E.Emp_name, D.Dept_name
FROM EMP E
JOIN DEPT D ON E.Dept_id = D.Dept_id;

-- Filter
SELECT * FROM EMP WHERE Emp_basicpay > 50000;

-- Condition
SELECT * FROM EMP WHERE Emp_add = 'Delhi' AND Emp_basicpay >= 50000;
```

---

## Summary Table

| Concept               | Description                                   |
| --------------------- | --------------------------------------------- |
| Relational Data Model | Organizes data in tables (relations)          |
| Integrity Constraints | Rules for data accuracy and consistency       |
| Entity Integrity      | Primary key must be unique and not NULL       |
| Referential Integrity | Foreign key must match primary key or be NULL |
| Key Constraints       | Uniqueness and identification of rows         |
| Domain Constraints    | Attribute values must be from valid domains   |
| Relational Algebra    | Operations to query/manipulate tables         |
| Relational Calculus   | Non-procedural query language (TRC, DRC)      |
| SQL Characteristics   | Simple, non-procedural, standardized          |
| SQL Advantages        | Universal, flexible, secure                   |
| SQL Data Types        | INT, VARCHAR, DATE, etc.                      |
| SQL Commands          | DDL, DML, DCL, TCL                            |
| SQL Operators         | Arithmetic, Comparison, Logical, Set          |
| Tables/Views/Indexes  | CREATE, SELECT, CREATE VIEW, CREATE INDEX     |
| Queries/Subqueries    | SELECT, nested SELECT                         |
| Aggregate Functions   | SUM, AVG, COUNT, MAX, MIN                     |
| DML Operations        | INSERT, UPDATE, DELETE                        |
| Joins                 | INNER, LEFT, RIGHT, FULL, CROSS               |
| Set Operators         | UNION, INTERSECT, MINUS                       |
| Division Operator     | Finds rows related to all in another table    |
| Cursors               | Row-by-row processing in PL/SQL               |
| Triggers              | Automatic actions on table events             |
| Procedures            | Stored programs for operations                |

---
