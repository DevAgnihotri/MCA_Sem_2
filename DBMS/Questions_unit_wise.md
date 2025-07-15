# DBMS University Question Paper Analysis (Unit-wise)

---

## Unit I – DBMS Basics, Architecture, ER Model

### 2016–17
- What are the disadvantages of database systems?
- Construct an ER diagram for a university registrar’s office.
- List and briefly explain the advantages of DBMS over traditional file systems.
- What problems are associated with the three-schema architecture?

### 2021–22
- What is logical data independence?
- "Data redundancy leads to data inconsistency." Justify this statement.
- What are the advantages of databases over file systems?
- Discuss the three-level architecture of DBMS with a neat diagram.
- Explain participation constraint in an ER diagram with a suitable example.
- Draw an ER diagram based on given assumptions and convert it to a relational model.

### 2022–23
- Define the terms "Data" and "Database".
- Discuss various advantages of DBMS.
- Explain the ANSI/SPARC architecture in detail.
- Discuss different types of entities, attributes, and relations used in designing an ER diagram.

---

## Unit II – Relational Model, SQL, Algebra, Calculus

### 2016–17
- Define joins in SQL. Briefly explain its types. Also, discuss the importance of triggers in SQL with an example.
- Discuss different types of SQL commands. Explain joins, aggregate functions, and sub-queries with neat examples.
- Explain the division operator with an example. How can it be implemented using other relational algebraic operators?
- Define referential integrity constraint. Explain its importance and how it is implemented in SQL.

### 2021–22
- What is domain integrity?
- Write the relational algebra expression: For relation Employee(EID, Ename, City), find the names of employees who live in Delhi or Mumbai.
- Write an SQL query to display all customer details, displaying the earliest date of registration first.
- Write the SQL command to create a table named STUDENT with constraints: Roll (Primary Key, must start with ‘S’), Name (Not Null), DOB, Email (Unique), DOR (>= DOB).
- What is the difference between a trigger and a procedure? Write a trigger that logs updated salary in the Employee_Backup table.
- Write SQL queries on EMP and DEPT tables for joins, filters, and conditions.

### 2022–23
- Create a table Employee(Emp_id, Emp_name, Emp_add, Emp_basicpay) and insert some records. Create another table Emp_detail(Emp_name, Emp_add) from Employee using a SELECT statement.
- What are sub-queries?
- Define a cursor in PL/SQL.
- Create the tables Supplier(SNo, SName, City), Parts(PNo, Pname, Color, City), and Shipment(SNo, PNo, Quantity). Answer queries: total suppliers, suppliers supplying parts, part numbers, change red to black.
- Discuss Primary Key, Unique Key, Candidate Key, and Foreign Key with examples.

---

## Unit III – Functional Dependencies, Normalization

### 2016–17
- Explain in detail all functional dependency-based normal forms with suitable examples.
- Why are certain functional dependencies called trivial?

### 2021–22
- What are the possible superkeys for the relation schema R(E, F, G, H) with EF as the key?
- Find the canonical cover Fc for FDs: P → QR, Q → R, P → Q, PQ → R.
- Given STUDENT(Roll, Name, DOB, Address, AdharNo, Email), find: alternative keys, non-key attributes, non-prime attributes, and prime attributes.
- What is partial functional dependency? Explain how insertion, update, and deletion anomalies occur in such relations.
- What is lossless decomposition of a relation? Given FDs and decomposition, check if it is lossless.

### 2022–23
- Why is normalization used?
- What is pseudo-transitivity?
- Explain basic inference rules. Given R(A–F), A→BC, B→E, CD→EF. Prove AD→F.
- Given relation R(P, Q, R, S, T), FD = {PQ → R, S → T}, determine if it is in 2NF and convert if not.
- How do you check if a decomposition is dependency preserving? Explain with an example.

---

## Unit IV – Transactions, Recovery, Distributed DB

### 2016–17
- State the need for serializability in transactions.
- What problems occur in transactions if they run concurrently?
- When does a transaction reach its commit point?
- What is transaction recovery? Illustrate the importance of log-based recovery and checkpoints.
- What is a distributed database? What are its advantages and disadvantages? How is concurrency control handled in distributed databases?
- List the implementation issues of distributed databases.

### 2021–22
- "A transaction must follow the Durability property." What is Durability?
- There is a schedule S with 5 transactions. How many serial schedules are possible?
- What is concurrency control? What is a timestamp? Discuss basic and strict timestamp protocols.
- What is a serializable schedule? Given a schedule, check for conflict serializability.
- What is a system log? What entries are made into the system log during the execution of a transaction?
- Write a short note on testing serializability.

### 2022–23
- Define a serializable schedule.
- What is transaction failure?
- Define concurrent processing in databases.
- Explain ACID properties of a transaction in detail.
- Write a short note on log-based recovery.
- What are the various types of locks applied on data items? Discuss two-phase locking protocol and strict two-phase locking protocol.

---

## Unit V – Concurrency Control Techniques

### 2016–17
- Explain in detail the various issues of multiple-granularity locking protocols.
- How is concurrency control performed in distributed databases?

### 2021–22
- What is concurrency control? What is a timestamp? Discuss basic and strict timestamp protocols.
- How is a serial schedule different from a non-serial schedule? Check whether a given schedule is conflict serializable.

### 2022–23
- What is the Timestamp Ordering Protocol? Discuss the working of the basic timestamp ordering protocol along with its advantages and disadvantages.
- Write a short note on multiple granularity.

