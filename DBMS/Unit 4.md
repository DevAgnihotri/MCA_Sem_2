# Transaction System and Serializability in DBMS

---

## Transaction System

- A **transaction** is a sequence of database operations (like read, write, update) that are performed as a single logical unit of work.
- Transactions are used to ensure data consistency and integrity, especially in multi-user environments.
- **Example:** Transferring money from one bank account to another (debit from one, credit to another) should be done as a single transaction.

---

## 1. What do you mean by commit point of transaction? [Q1]

**Question 1: What do you mean by commit point of transaction?**

- The **commit point** is the moment in a transaction when all its operations are successfully completed, and the changes made by the transaction are permanently saved to the database.
- After the commit point, the transaction cannot be rolled back.
- If a failure occurs before the commit, all changes are undone (rolled back).

---

## 3. Explain ACID properties of a transaction in detail. [Q3]

**Question 3: Explain ACID properties of a transaction in detail.**

The four ACID properties ensure reliable processing of database transactions:

| Property    | Meaning                                                                               |
| ----------- | ------------------------------------------------------------------------------------- |
| Atomicity   | All operations in a transaction are completed, or none are (all-or-nothing).          |
| Consistency | A transaction brings the database from one valid state to another.                    |
| Isolation   | Transactions do not interfere with each other; intermediate results are hidden.       |
| Durability  | Once a transaction is committed, its changes are permanent, even if the system fails. |

- **Atomicity:** If any part of the transaction fails, the whole transaction is rolled back.
- **Consistency:** The database remains in a valid state before and after the transaction.
- **Isolation:** Transactions appear to run independently, even if they are executed concurrently.
- **Durability:** Committed changes survive system crashes or failures.

---

## 4. “A transaction must follow Durability property”. What do you mean by Durability? [Q4]

**Question 4: “A transaction must follow Durability property”. What do you mean by Durability?**

- **Durability** means that once a transaction is committed, its changes are saved permanently in the database.
- Even if there is a power failure or system crash after the commit, the changes will not be lost.
- This is usually achieved by writing changes to non-volatile storage (like hard disk) before confirming the commit.

---

## Serializability of Schedules

- **Schedule:** The order in which operations (read, write) of multiple transactions are executed.
- **Serial Schedule:** All operations of one transaction are completed before another starts. No interleaving.
- **Non-Serial Schedule:** Operations of transactions are interleaved.
- **Serializable Schedule:** A non-serial schedule that produces the same result as some serial schedule.

---

## 7. There is a schedule S having 5 transactions. How many serial schedules can be made possible? [Q7]

**Question 7: There is a schedule S having 5 transactions. How many serial schedules can be made possible?**

- For n transactions, the number of possible serial schedules is n! (n factorial).
- For 5 transactions: 5! = 5 × 4 × 3 × 2 × 1 = 120 serial schedules.

---

## 8. How is a serial schedule different from a non-serial schedule? What is a serializable schedule? A schedule is given as follows S: r1(X), r2(X), w1(X), r1(Y), w2(X), W1(Y). Check whether schedule S is a conflict serializable schedule or not. [Q8]

**Question 8: How is a serial schedule different from a non-serial schedule? What is a serializable schedule? A schedule is given as follows S: r1(X), r2(X), w1(X), r1(Y), w2(X), W1(Y). Check whether schedule S is a conflict serializable schedule or not.**

- **Serial schedule:** All operations of one transaction are executed before another starts (no interleaving).
- **Non-serial schedule:** Operations of transactions are interleaved.
- **Serializable schedule:** A non-serial schedule that is equivalent to some serial schedule (produces the same result).

**Conflict Serializability Test:**

- List all conflicting operations (read/write or write/write on the same data by different transactions).
- Build a precedence (serialization) graph:
  - Draw an edge from Ti to Tj if an operation of Ti precedes and conflicts with an operation of Tj.
- If the graph has no cycles, the schedule is conflict serializable.

**Given schedule S:** r1(X), r2(X), w1(X), r1(Y), w2(X), w1(Y)

- Transactions: T1, T2
- Conflicts:
  - r2(X) after w1(X): T1 → T2
  - w2(X) after w1(X): T1 → T2
  - w1(Y) after r1(Y): No conflict (same transaction)
- Precedence graph: T1 → T2 (no cycles)
- **Conclusion:** The schedule is conflict serializable.

---

## Testing of Serializability [Q6]

**Question 6: Write a short note on Testing of serializability.**

- **Testing serializability** is the process of checking if a given schedule is serializable (i.e., equivalent to a serial schedule).
- The most common method is to use a **precedence graph** (also called a serialization graph):
  1. Create a node for each transaction.
  2. For every pair of conflicting operations (read/write or write/write on the same data by different transactions), draw a directed edge from the first transaction to the second.
  3. If the graph has no cycles, the schedule is serializable; if there is a cycle, it is not serializable.
- This helps ensure database consistency in concurrent transaction processing.

---

## Serializability of Schedules: Conflict & View Serializable Schedule

- **Conflict Serializable:** A schedule is conflict serializable if it can be transformed into a serial schedule by swapping non-conflicting operations.
- **View Serializable:** A schedule is view serializable if it is view equivalent to a serial schedule (reads and writes produce the same final result), even if not conflict serializable.
- **Conflict serializability** is easier to test and is commonly used in practice.

---

## Recoverability and Recovery from Transaction Failures

### Recoverability in Transaction Schedules

- **Recoverability** is a property of a transaction schedule that ensures if a transaction fails and is rolled back, all other transactions that depend on it (i.e., have read its uncommitted changes) are also rolled back. This prevents the database from ending up in an inconsistent state.

### Why is Recoverability Important?

- In concurrent transaction processing, transactions may read data written by other transactions before those transactions are committed.
- If a transaction (say, T1) writes a value and another transaction (T2) reads that value before T1 commits, and then T1 fails, T2 has read an invalid (uncommitted) value. This is called a **dirty read**.
- If T2 commits before T1, the system cannot recover to a consistent state if T1 fails. This is called a **non-recoverable schedule**.

### Types of Schedules Based on Recoverability

| Type of Schedule         | Description                                                                                  |
| ------------------------ | -------------------------------------------------------------------------------------------- |
| Recoverable Schedule     | Transactions commit only after all transactions whose changes they have read have committed. |
| Non-Recoverable Schedule | A transaction commits before a transaction whose uncommitted changes it has read.            |
| Cascadeless Schedule     | Transactions only read committed data (no dirty reads), so no cascading rollbacks occur.     |
| Strict Schedule          | Transactions neither read nor overwrite uncommitted data.                                    |

#### Example: Recoverable vs. Non-Recoverable

- **Recoverable:**
  - T1 writes X, T2 reads X, T1 commits, T2 commits (OK)
- **Non-Recoverable:**
  - T1 writes X, T2 reads X, T2 commits, T1 fails (NOT OK)

---

## Recovery from Transaction Failures

- **Recovery** is the process of restoring the database to a consistent state after a failure (such as a system crash, power failure, or transaction error).
- The DBMS uses various techniques to ensure that committed transactions are not lost and uncommitted changes are undone.

### Types of Transaction Failures [Q2]

**Question 2: What do you mean by transaction failure?**

- A **transaction failure** occurs when a transaction cannot complete its operations successfully and must be rolled back.
- Causes of transaction failure include:
  - System crash (hardware/software failure)
  - Deadlock (transactions waiting for each other)
  - Logical errors (e.g., invalid data, constraint violation)
  - User-initiated abort (user cancels the transaction)
- When a transaction fails, all its changes must be undone to maintain database consistency.

### States of a Transaction

| State               | Description                                             |
| ------------------- | ------------------------------------------------------- |
| Active              | Transaction is executing its operations.                |
| Partially Committed | All operations are done, but changes not yet permanent. |
| Committed           | All changes are saved permanently.                      |
| Failed              | Transaction cannot proceed due to an error.             |
| Aborted             | All changes are rolled back; transaction is terminated. |

---

### Recovery Techniques

- **Undo:** Reverses the changes made by a failed or aborted transaction.
- **Redo:** Reapplies the changes of committed transactions after a crash.
- **Log-based Recovery:** The DBMS maintains a log of all changes. In case of failure, the log is used to undo or redo operations.
- **Checkpoints:** Periodically, the DBMS saves the current state, so recovery can start from the last checkpoint.

#### Example Table: Actions During Recovery

| Transaction State | Action Taken During Recovery |
| ----------------- | ---------------------------- |
| Committed         | Redo changes                 |
| Aborted/Failed    | Undo changes                 |

---

## Restarting or Killing a Transaction After Failure [Q5]

**Question 5: A transaction has failed and has entered Aborted state. Mention the conditions under which we can restart a transaction or kill a transaction.**

- When a transaction fails, it enters the **Aborted** state. The DBMS must decide whether to restart (re-execute) the transaction or kill (terminate) it permanently.

### Conditions for Restarting a Transaction

- The cause of failure was temporary (e.g., deadlock, system crash, resource unavailability).
- The transaction does not violate any integrity constraints.
- The user/application requests a retry.
- The system is configured to automatically retry certain types of failures.

### Conditions for Killing a Transaction

- The failure is due to a logical error in the transaction (e.g., invalid data, programming bug).
- The transaction repeatedly fails after several retries.
- The user/application explicitly cancels the transaction.
- The system detects a security violation or unauthorized access.

#### Table: Actions After Transaction Failure

| Condition                        | Action  |
| -------------------------------- | ------- |
| Temporary/system failure         | Restart |
| Deadlock                         | Restart |
| User cancels transaction         | Kill    |
| Logical/programming error        | Kill    |
| Repeated failures                | Kill    |
| Security/authorization violation | Kill    |

---

## Summary Table: Recoverability and Recovery

| Concept             | Description                                                            |
| ------------------- | ---------------------------------------------------------------------- |
| Recoverability      | Ensures dependent transactions are rolled back if a transaction fails. |
| Transaction Failure | When a transaction cannot complete and must be rolled back.            |
| Recovery            | Restoring the database to a consistent state after a failure.          |
| Restart             | Re-executing a failed transaction under certain conditions.            |
| Kill                | Terminating a failed transaction permanently under certain conditions. |

---

## Log-Based Recovery [Q9, Q10, Q11]

### What is Log-Based Recovery?

**Log-based recovery** is a fundamental technique used by database management systems (DBMS) to ensure data integrity and durability in the event of failures such as system crashes, power outages, or transaction errors. The main idea is to keep a **log** (also called a journal) of all important actions performed by transactions so that the system can recover to a consistent state after a failure.

#### How Log-Based Recovery Works

- The DBMS maintains a **system log** on stable storage (like a hard disk) that records all changes made to the database.
- If a failure occurs, the DBMS uses the log to **undo** the effects of incomplete transactions and **redo** the effects of committed transactions.
- This ensures that the database remains consistent and no committed data is lost.

#### Types of Log Records

| Log Record Type | Description                                                             |
| --------------- | ----------------------------------------------------------------------- |
| Start           | Marks the beginning of a transaction.                                   |
| Update          | Records the old and new values when data is changed.                    |
| Commit          | Indicates that a transaction has completed successfully.                |
| Abort/Rollback  | Indicates that a transaction has failed and its changes must be undone. |

#### Example Log Entry

| Transaction | Operation | Data Item | Old Value | New Value |
| ----------- | --------- | --------- | --------- | --------- |
| T1          | Update    | X         | 100       | 200       |

---

### Q9. Write a short note on Log-Based Recovery.

**Question 9: Write a short note on Log-Based Recovery.**

- Log-based recovery is a method used by DBMS to recover from failures by maintaining a log of all transaction activities.
- The log contains records of all changes made to the database, including the old and new values.
- In case of a failure, the DBMS uses the log to redo the operations of committed transactions and undo the operations of uncommitted transactions.
- This ensures the **atomicity** and **durability** properties of transactions.
- Log-based recovery is essential for maintaining database consistency and preventing data loss.

---

### Q10. What is system log? What are the record entries done into the system log during execution of a transaction?

**Question 10: What is system log? What are the record entries done into the system log during execution of a transaction?**

- A **system log** is a sequential record maintained by the DBMS that stores all important actions performed by transactions.
- The log is stored on stable storage to survive system crashes.
- Typical entries in the system log during a transaction include:
  - **[start, T]**: Marks the start of transaction T.
  - **[T, X, old_value, new_value]**: Records an update by transaction T on data item X, showing both old and new values.
  - **[commit, T]**: Marks the successful completion of transaction T.
  - **[abort, T]**: Marks the failure and rollback of transaction T.

---

### Q11. What is a system log used for? What are typical kinds of records in a system log? What are transaction commit points, and why are they important?

**Question 11: What is a system log used for? What are typical kinds of records in a system log? What are transaction commit points, and why are they important?**

- The **system log** is used for recovery purposes. It helps the DBMS restore the database to a consistent state after a failure.
- Typical records in a system log include:
  - Start of transaction
  - Update operations (with old and new values)
  - Commit and abort records
- **Transaction commit point** is the moment when all operations of a transaction are completed and the changes are made permanent in the database.
- Commit points are important because:
  - Only changes of committed transactions are redone during recovery.
  - Changes of uncommitted transactions are undone to maintain consistency.

---

## Checkpoints

### What is a Checkpoint?

- A **checkpoint** is a mechanism used by DBMS to reduce the amount of work needed during recovery after a failure.
- At certain intervals, the DBMS writes all modified data (dirty pages) and log records to stable storage and records a checkpoint in the log.
- This marks a point where the database is known to be consistent.

#### How Checkpoints Work

- During recovery, the DBMS can start from the last checkpoint instead of scanning the entire log, making recovery faster.
- All transactions that committed before the checkpoint do not need to be redone or undone.

#### Steps in Checkpointing

1. Suspend all new transactions temporarily.
2. Write all log records and modified data to disk.
3. Write a checkpoint record to the log.
4. Resume normal transaction processing.

#### Table: Benefits of Checkpoints

| Benefit               | Description                                      |
| --------------------- | ------------------------------------------------ |
| Faster Recovery       | Reduces the amount of log to scan after failure. |
| Consistency Guarantee | Ensures database is consistent at checkpoint.    |

---

## Deadlock Handling [Q17, Q19]

### What is a Deadlock? [Q19]

**Question 19: What is a deadlock? Explain one deadlock detection algorithm in database transaction processing.**

- A **deadlock** occurs when two or more transactions are waiting indefinitely for each other to release locks on resources, so none of them can proceed.
- Example: T1 holds a lock on X and waits for Y; T2 holds a lock on Y and waits for X.

#### Deadlock Detection Algorithm: Wait-For Graph

- The **Wait-For Graph (WFG)** is a common deadlock detection method.
- Each transaction is a node; an edge from T1 to T2 means T1 is waiting for a resource held by T2.
- The system periodically checks the WFG for cycles:
  - If a cycle is found, a deadlock exists.
  - The system can break the deadlock by aborting one or more transactions in the cycle.

#### Table: Deadlock Handling Methods

| Method     | Description                                                 |
| ---------- | ----------------------------------------------------------- |
| Prevention | Ensure deadlocks never occur (e.g., resource ordering).     |
| Detection  | Allow deadlocks, then detect and resolve them.              |
| Avoidance  | Dynamically avoid unsafe states (e.g., Banker's algorithm). |

---

### Lock-Based Protocols [Q17]

**Question 17: Short notes on Lock based Protocols**

- **Lock-based protocols** are concurrency control mechanisms that use locks to manage access to database items.
- Types of locks:
  - **Shared lock (S-lock):** Allows multiple transactions to read a data item but not modify it.
  - **Exclusive lock (X-lock):** Allows a transaction to both read and modify a data item; no other transaction can access it.
- **Two-Phase Locking (2PL):**
  - Transactions acquire all the locks they need (growing phase), then release them (shrinking phase).
  - Guarantees serializability but may cause deadlocks.

---

### Deadlock Prevention Protocols [Q17]

**Question 17: Short notes on Deadlock prevention protocols**

- **Deadlock prevention protocols** are techniques to ensure that deadlocks do not occur.
- Common methods:
  - **Wait-Die Scheme:** Older transactions may wait for younger ones; younger transactions requesting a lock held by an older one are aborted.
  - **Wound-Wait Scheme:** Older transactions requesting a lock held by a younger one preempt (wound) the younger one; younger transactions wait for older ones.
  - **Resource Ordering:** Impose a global order on resources and require transactions to request locks in that order.

---

## Distributed Database: Distributed Data Storage, Concurrency Control, Directory System [Q18]

### Distributed Data Storage

- In a **distributed database**, data is stored across multiple physical locations (sites or nodes) connected by a network.
- Data can be **replicated** (copies at multiple sites) or **partitioned** (different parts at different sites).
- Advantages:
  - Improved reliability and availability
  - Faster local access
  - Scalability
- Challenges:
  - Data consistency
  - Network failures
  - Distributed transactions

### Concurrency Control in Distributed Systems [Q18]

**Question 18: Short note on Concurrency control in distributed system.**

- **Concurrency control** in distributed systems ensures that simultaneous transactions at different sites do not interfere with each other and maintain database consistency.
- Techniques include:
  - **Distributed Two-Phase Locking (2PL):** Locks are managed across sites to ensure serializability.
  - **Timestamp Ordering:** Transactions are ordered based on timestamps to avoid conflicts.
  - **Commit Protocols (e.g., Two-Phase Commit):** Ensure all sites agree to commit or abort a transaction.
- Challenges:
  - Communication delays
  - Site failures
  - Maintaining global consistency

### Directory System in Distributed Databases

- The **directory system** keeps track of where data is stored in a distributed database.
- It maps data items to their physical locations across sites.
- Types:
  - **Centralized Directory:** Single site maintains the directory (simple but single point of failure).
  - **Distributed Directory:** Directory is spread across multiple sites (more robust, but complex).
- The directory helps in locating data quickly and efficiently during query processing and transaction execution.

---
# PYQ's Covered

### 1. Transaction Concepts
1. What do you mean by commit point of transaction?
3. Explain ACID properties of a transaction in detail.
4. “A transaction must follow Durability property”. What do you mean by Durability?

### 2. Serializability and Scheduling
6. Write a short note on Testing of serializability.
7. There is a schedule S having 5 transactions. How many serial schedules can be made possible?
8. How is a serial schedule different from a non-serial schedule? What is a serializable schedule? A schedule is given as follows S: r1(X), r2(X), w1(X), r1(Y), w2(X), W1(Y). Check whether schedule S is a conflict serializable schedule or not.
5. A transaction has failed and has entered Aborted state. Mention the conditions under which we can restart a transaction or kill a transaction.
2. What do you mean by transaction failure?


### 3. System Log and Recovery
9. Write a short note on Log-Based Recovery.
10. What is system log? What are the record entries done into the system log during execution of a transaction?
11. What is a system log used for? What are typical kinds of records in a system log? What are transaction commit points, and why are they important?

17. Short notes on:
    - Lock based Protocols
    - Deadlock prevention protocols
18. Short note on Concurrency control in distributed system.
19. What is a deadlock? Explain one deadlock detection algorithm in database transaction processing.