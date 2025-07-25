# Concurrency Control in DBMS: Detailed Notes and Solved Questions

---

## Introduction to Concurrency and Concurrency Control

- **Concurrency** in databases means that multiple transactions are executed at the same time (concurrently), possibly accessing the same data.
- **Concurrent processing** improves system performance and resource utilization but can lead to problems like lost updates, dirty reads, and uncommitted data being read if not managed properly.

### Q13. Define concurrent processing in database.

**Question 13: Define concurrent processing in database.**

- **Concurrent processing** refers to the execution of multiple transactions simultaneously in a database system.
- It allows multiple users to access and modify the database at the same time, increasing throughput and efficiency.
- The DBMS must ensure that concurrent transactions do not interfere with each other and that the database remains consistent.

---

## What is Concurrency Control?

- **Concurrency control** is a collection of methods and protocols used by a Database Management System (DBMS) to ensure that multiple transactions can execute simultaneously without interfering with each other, and that the integrity and consistency of the database are preserved.
- When transactions run concurrently, several issues can arise if their operations overlap or conflict. Concurrency control mechanisms are designed to prevent these problems and ensure that the outcome of executing transactions concurrently is the same as if they were executed one after another (serially).
- The main goals of concurrency control are:
    - **Consistency:** Ensure that the database remains in a valid state after concurrent transactions.
    - **Isolation:** Ensure that the intermediate state of a transaction is not visible to other transactions.
    - **Serializability:** Guarantee that the concurrent execution of transactions results in a state that could be produced by some serial execution.
- Common problems that concurrency control aims to prevent include:
    - **Lost update:** Occurs when two transactions read the same data and then update it, causing one update to overwrite the other.
    - **Dirty read:** Happens when a transaction reads data written by another transaction that has not yet committed, potentially reading invalid or temporary data.
    - **Unrepeatable read:** When a transaction reads the same row twice and gets different values because another transaction has modified the data in between the reads.
    - **Phantom read:** Occurs when a transaction re-executes a query and finds rows that were not visible before because another transaction has inserted or deleted rows.
- To address these issues, DBMSs use various concurrency control techniques such as locking protocols, timestamp ordering, validation (optimistic) protocols, and multi-version concurrency control (MVCC). Each technique has its own advantages and trade-offs in terms of performance, complexity, and suitability for different workloads.
- Effective concurrency control is essential for maintaining data accuracy, supporting multiple users, and ensuring reliable transaction processing in modern database systems.

### Q14. What do you mean by concurrency control? What is a timestamp? Discuss basic timestamp and strict timestamp protocol as concurrency control mechanisms.

**Question 14: What do you mean by concurrency control? What is a timestamp? Discuss basic timestamp and strict timestamp protocol as concurrency control mechanisms.**

- **Concurrency control** is the set of techniques used by a DBMS to ensure that multiple transactions can execute simultaneously without causing inconsistencies in the database.
- **Timestamp:** A unique value (such as a counter or system time) assigned to each transaction when it begins. Timestamps are used to determine the order of transactions.

#### Timestamp Protocols for Concurrency Control

**Basic Timestamp Ordering Protocol:**
- Each transaction gets a unique timestamp when it starts.
- All operations are ordered based on these timestamps.
- If a transaction tries to perform an operation that would violate the timestamp order (for example, writing to a data item that has already been read or written by a newer transaction), it is rolled back and restarted.
- This protocol ensures serializability and avoids deadlocks, but may cause frequent rollbacks if there is high contention.

**Strict Timestamp Ordering Protocol:**
- Similar to the basic protocol, but with an added restriction: a transaction must wait until all earlier transactions (with lower timestamps) that accessed the same data have either committed or aborted before it can proceed.
- This prevents cascading rollbacks and provides stronger consistency (strict serializability).
- However, it may increase waiting time for transactions compared to the basic protocol.


**Summary:**
- **Basic timestamp ordering** ensures serializability by rolling back transactions that violate timestamp order.
- **Strict timestamp ordering** adds the requirement that transactions must wait for earlier conflicting transactions to finish, providing stronger consistency guarantees.

--- 
### Q17. Explain Locking Techniques for Concurrency Control.

**Question 17: Explain Locking Techniques for Concurrency Control.**

### Q16. What are various types of Locks applied on data items? Discuss Two-phase locking protocol and Strict Two-phase locking protocols.

**Question 16: What are various types of Locks applied on data items? Discuss Two-phase locking protocol and Strict Two-phase locking protocols.**


## Locking Techniques for Concurrency Control

- **Locking** is a fundamental method used by DBMSs to coordinate concurrent access to data items, ensuring consistency and isolation.
- A **lock** temporarily restricts access to a data item, preventing conflicting operations by other transactions.

### Types of Locks

- **Binary Locks:** Each data item is either locked (in use) or unlocked (available). Simple but inflexible, as it does not distinguish between read and write operations.
- **Shared Lock (S-lock):** Permits multiple transactions to read a data item simultaneously, but none can write to it while the shared lock is held.
- **Exclusive Lock (X-lock):** Grants a single transaction the right to both read and modify a data item. No other transaction can access the item (read or write) while it is exclusively locked.
- **Intention Locks:** Used in multi-level locking (multiple granularity), intention locks (IS, IX, SIX) indicate a transaction’s intention to acquire shared or exclusive locks at a finer granularity, enabling efficient locking at different hierarchy levels (e.g., table, page, row).

### Locking Protocols

- **Two-Phase Locking (2PL):**
  
  ### Q15. What do you mean by concurrency? Demonstrate how 2 phase protocol will be useful for controlling concurrency. Discuss variations of 2PL.

  Two-Phase Locking (2PL) is a widely used method for managing how multiple transactions access data at the same time in a database. The main goal of 2PL is to ensure that transactions do not interfere with each other in a way that could cause errors or inconsistencies, such as lost updates or dirty reads.

  **How 2PL Works:**
  - Every transaction is divided into two distinct phases:
    1. **Growing Phase:** The transaction can acquire (get) new locks on data items as needed, but it cannot release any locks during this phase.
    2. **Shrinking Phase:** Once the transaction starts releasing any lock, it cannot acquire any new locks. It can only release the locks it already holds.
  - This rule ensures that once a transaction starts to release locks, it cannot interfere with other transactions by acquiring new locks, which helps maintain the consistency and correctness of the database.

  **How 2PL Controls Concurrency:**

  Suppose two transactions, T1 and T2, want to update the same data item X.

  - **Without 2PL:**  
    - T1 reads X.
    - T2 reads X.
    - T1 writes X.
    - T2 writes X (overwriting T1’s update, causing a lost update problem).

  - **With 2PL:**  
    - T1 acquires an exclusive lock on X before reading/writing.
    - T2 must wait until T1 releases the lock.
    - T1 completes and releases the lock.
    - T2 acquires the lock and proceeds.
    - This ensures that only one transaction updates X at a time, preventing lost updates and maintaining consistency.

  **Example Table:**

  | Step | T1 Action         | T2 Action         | Lock Status      |
  |------|-------------------|-------------------|------------------|
  | 1    | Lock X (X-lock)   |                   | X locked by T1   |
  | 2    | Read/Write X      |                   | X locked by T1   |
  | 3    |                   | Wait for X        | X locked by T1   |
  | 4    | Unlock X          |                   | X unlocked       |
  | 5    |                   | Lock X (X-lock)   | X locked by T2   |
  | 6    |                   | Read/Write X      | X locked by T2   |

  This protocol ensures serializability and prevents concurrency anomalies.

  **Why Use 2PL?**
  - 2PL guarantees **serializability**, meaning the final result of executing transactions concurrently is the same as if they were executed one after another (serially).
  - It helps prevent common concurrency problems like lost updates, dirty reads, and uncommitted data being read by other transactions.

  **Types of Two-Phase Locking:**
  - **Strict 2PL:** All exclusive (write) locks are held until the transaction finishes (commits or aborts). This prevents other transactions from reading uncommitted changes and avoids cascading rollbacks.
  - **Rigorous 2PL:** Even stricter than strict 2PL, all locks (both shared/read and exclusive/write) are held until the transaction ends. This provides the highest level of isolation.
  - **Conservative 2PL:** The transaction requests all the locks it will need before it starts. If it cannot get all the required locks, it waits and does not proceed. This approach avoids deadlocks but may reduce the number of transactions that can run at the same time.

  **Summary:**
  - 2PL is a simple and effective protocol for concurrency control. It ensures data consistency and prevents many common problems in concurrent transaction processing.
  - However, 2PL can cause transactions to wait for locks, which may lead to deadlocks (where two or more transactions wait indefinitely for each other). The different types of 2PL offer trade-offs between safety (isolation) and system performance (concurrency).


  - **Multiple Granularity Locking:**
    - This technique allows locks to be placed at different levels of the database structure, such as the entire database, a specific table, a page within a table, or a single row.
    - The main goal is to improve performance and flexibility by letting transactions lock only the part of the database they need, instead of locking large sections unnecessarily.
    - **Intention Locks** are special types of locks used to signal a transaction’s intention to acquire a more restrictive lock at a lower level. There are three main types:
      - **Intention Shared (IS):** Indicates that a transaction intends to acquire shared (read) locks at a lower level.
      - **Intention Exclusive (IX):** Indicates that a transaction intends to acquire exclusive (write) locks at a lower level.
      - **Shared and Intention Exclusive (SIX):** Indicates that a transaction holds a shared lock at the current level and intends to acquire exclusive locks at a lower level.
    - Before a transaction can lock a lower-level object (like a row), it must first acquire the appropriate intention lock at all higher levels (like table and database). This prevents conflicts and makes lock management more efficient.
    - **Benefits:**
      - Reduces unnecessary locking of large objects, allowing more transactions to run at the same time.
      - Makes it easier to manage locks in complex databases with many levels.
      - Helps prevent deadlocks and lock conflicts by clearly indicating locking intentions.
    - **Example:** If a transaction wants to update a row in a table, it first places an IX lock on the database, then an IX lock on the table, and finally an X (exclusive) lock on the row. Other transactions can see these intention locks and avoid conflicting operations.


### Deadlock and Starvation

- **Deadlock:** Occurs when two or more transactions wait indefinitely for locks held by each other. Detection and resolution mechanisms (e.g., wait-for graph, timeout) are used to handle deadlocks.
- **Starvation:** A transaction may never acquire the locks it needs if other transactions continually preempt it. Fair scheduling and lock management policies help prevent starvation.

### Summary

Locking techniques, when properly implemented, provide robust concurrency control by managing access to data items, preventing conflicts, and ensuring database consistency. The choice of locking protocol and granularity impacts system performance, deadlock risk, and transaction throughput.

---

- **Types of Locks:**
  - **Binary Lock:** Simple lock/unlock.
  - **Shared Lock (S):** Multiple transactions can read.
  - **Exclusive Lock (X):** Only one transaction can write.
  - **Intention Locks:** Used in multiple granularity locking (IS, IX, SIX).
- **Two-Phase Locking (2PL):**
  - **Growing phase:** Transaction acquires locks.
  - **Shrinking phase:** Transaction releases locks.
  - No new locks can be acquired after the first lock is released.
- **Strict 2PL:**
  - All exclusive locks are held until the transaction commits/aborts.
  - Prevents cascading rollbacks.

| Protocol   | Growing Phase | Shrinking Phase | Prevents Cascading Rollback | Guarantees Serializability |
| ---------- | ------------- | --------------- | --------------------------- | -------------------------- |
| 2PL        | Yes           | Yes             | No                          | Yes                        |
| Strict 2PL | Yes           | Yes             | Yes                         | Yes                        |

---

## Time Stamping Protocols for Concurrency Control

- **Timestamp protocols** use transaction timestamps to order operations and ensure serializability.
- Each transaction is assigned a unique timestamp when it starts.
- The DBMS uses these timestamps to decide whether to allow or block operations.

### Q20. What do you mean by timestamp? Discuss timestamp ordering protocol in detail.

- **Timestamp:** A timestamp is a unique identifier (usually a number or the system time) given to each transaction when it starts. It helps the DBMS decide the order in which transactions should be executed.
- **Timestamp Ordering Protocol:**
  - Each data item in the database keeps two timestamps:
    - **read_TS(X):** The largest timestamp of any transaction that has successfully read data item X.
    - **write_TS(X):** The largest timestamp of any transaction that has successfully written to data item X.

  - When a transaction wants to perform a read or write, the DBMS checks these timestamps:
    - **Read(X):** If the transaction’s timestamp is less than write_TS(X), it means a newer transaction has already written to X, so the read is rejected and the transaction is rolled back. Otherwise, the read is allowed, and read_TS(X) is updated if needed.

    - **Write(X):** If the transaction’s timestamp is less than either read_TS(X) or write_TS(X), it means a newer transaction has already read or written X, so the write is rejected and the transaction is rolled back. Otherwise, the write is allowed, and write_TS(X) is updated.

  - This protocol ensures that all operations occur in timestamp order, maintaining serializability.
  
- **Advantages:**
  - No locks are used, so there are no deadlocks.
  - Transactions are executed in a serializable order.
- **Disadvantages:**
  - Transactions may be rolled back frequently if there is a lot of overlap or contention, which can reduce performance.

---

## Validation Based Protocol

- **Validation (Optimistic) Concurrency Control:**
  - Transactions execute without restrictions, but before commit, the DBMS checks if they conflict with other transactions.
  - If validation passes, the transaction commits; otherwise, it is rolled back.
- **Phases:**
  1. **Read phase:** Transaction reads data and makes changes in a private workspace.
  2. **Validation phase:** Before commit, check for conflicts.
  3. **Write phase:** If validation succeeds, changes are written to the database.
- **Best for:** Low-conflict environments (few concurrent updates).

---

## Multi Version Schemes

- **Multi-Version Concurrency Control (MVCC):**
  - Maintains multiple versions of data items to allow concurrent reads and writes.
  - Readers can access a snapshot of the data without being blocked by writers.
- **Benefits:**
  - Increases concurrency.
  - Reduces locking and blocking.
- **Drawbacks:**
  - More storage required for multiple versions.
  - Garbage collection needed to remove old versions.

### Q21. What is a Multi Version Protocol?

- A protocol that allows multiple versions of data items to exist, enabling higher concurrency.
- Each transaction sees a consistent snapshot of the database.

### Q22. What is multi-version concurrency control? What are its benefits and disadvantages in comparison to locking?

- **MVCC** allows multiple versions of data for concurrent access.
- **Benefits:**
  - Readers are never blocked by writers.
  - Higher concurrency and performance.
- **Disadvantages:**
  - Increased storage requirements.
  - Complexity in managing versions.

---

## Recovery with Concurrent Transactions

- Recovery ensures that the database remains consistent after failures, even with concurrent transactions.
- Uses logs, checkpoints, and protocols like ARIES to recover committed transactions and roll back uncommitted ones.
- Must handle interleaved operations and dependencies between transactions.

---

## Case Study: Oracle Concurrency Control

- **Oracle** uses a combination of locking and multi-versioning (MVCC) for concurrency control.
- **Key features:**
  - **Read Consistency:** Readers see a snapshot of the data as of the start of their query.
  - **Row-level Locking:** Writers lock only the rows they modify.
  - **Undo Segments:** Used to provide old versions of data for readers.
  - **Deadlock Detection:** Oracle automatically detects and resolves deadlocks.

### Q23. What do you mean by dispatcher in terms of Oracle?

- In Oracle, a **dispatcher** is a background process used in a multi-threaded server (MTS) environment.
- Dispatchers manage client connections, routing requests to shared server processes.
- This allows Oracle to support thousands of concurrent users efficiently.
- **Benefits:**
  - Reduces resource usage.
  - Improves scalability and performance for large numbers of users.

---

# Summary Table: Concurrency Control Techniques

| Technique  | Main Idea                          | Pros                       | Cons                     |
| ---------- | ---------------------------------- | -------------------------- | ------------------------ |
| Locking    | Use locks to control access        | Simple, widely used        | Can cause deadlocks      |
| Timestamp  | Order by transaction timestamps    | No deadlocks, serializable | May cause rollbacks      |
| Validation | Check for conflicts at commit      | High concurrency possible  | Rollbacks if conflicts   |
| MVCC       | Multiple versions for reads/writes | Readers never blocked      | More storage, complexity |

---