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
    - Divides a transaction’s execution into two phases:
        - **Growing phase:** The transaction acquires all the locks it needs; no locks are released.
        - **Shrinking phase:** The transaction releases locks; no new locks can be acquired.
    - Ensures serializability by preventing cycles in the schedule’s precedence graph.
    - Variants:
        - **Strict 2PL:** All exclusive locks are held until the transaction commits or aborts, preventing cascading rollbacks and ensuring recoverability.
        - **Rigorous 2PL:** All locks (shared and exclusive) are held until commit/abort, providing even stronger isolation.
        - **Conservative 2PL:** All required locks are acquired before the transaction starts, eliminating deadlocks but potentially reducing concurrency.

- **Multiple Granularity Locking:**
    - Locks can be applied at various levels of the database hierarchy (database, table, page, row).
    - Intention locks (IS, IX, SIX) allow transactions to indicate their locking intentions at higher levels before acquiring actual S or X locks at lower levels, reducing lock contention and improving concurrency.

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

### Q15. What do you mean by concurrency? Demonstrate how 2 phase protocol will be useful for controlling concurrency. Discuss variations of 2PL.

**Question 15: What do you mean by concurrency? Demonstrate how 2 phase protocol will be useful for controlling concurrency. Discuss variations of 2PL.**

- **Concurrency** is the ability of the database to allow multiple transactions to execute at the same time.
- **Two-Phase Locking (2PL):**
  - Ensures serializability by dividing transaction execution into two phases: growing (acquire locks) and shrinking (release locks).
  - Prevents conflicts and ensures consistency.
- **Variations of 2PL:**
  - **Strict 2PL:** Holds all exclusive locks until commit.
  - **Rigorous 2PL:** Holds all locks (shared and exclusive) until commit.
  - **Conservative 2PL:** Acquires all locks before transaction starts (prevents deadlocks).

---

## Time Stamping Protocols for Concurrency Control

- **Timestamp protocols** use transaction timestamps to order operations and ensure serializability.
- Each transaction is assigned a unique timestamp when it starts.
- The DBMS uses these timestamps to decide whether to allow or block operations.

### Q20. What do you mean by timestamp? Discuss timestamp ordering protocol in detail.

**Question 20: What do you mean by timestamp? Discuss timestamp ordering protocol in detail.**

- **Timestamp:** A unique identifier (often a number or time value) assigned to each transaction.
- **Timestamp Ordering Protocol:**
  - Each data item has two timestamps: read_TS (last read) and write_TS (last write).
  - When a transaction wants to read or write, the DBMS checks these timestamps to ensure serializability.
  - If an operation would violate the timestamp order, the transaction is rolled back.
- **Advantages:**
  - No locks, so no deadlocks.
  - Ensures serializability.
- **Disadvantages:**
  - May cause many rollbacks (especially under high contention).

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

## Multiple Granularity

- **Multiple Granularity Locking:**
  - Allows locks at different levels (database, table, page, row).
  - Uses intention locks (IS, IX, SIX) to indicate intention to acquire locks at a lower level.
- **Benefits:**
  - Reduces locking overhead.
  - Increases concurrency by allowing finer control.

| Level    | Example Lock |
| -------- | ------------ |
| Database | IS, IX       |
| Table    | IS, IX, SIX  |
| Page/Row | S, X         |

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

**Question 21: What is a Multi Version Protocol?**

- A protocol that allows multiple versions of data items to exist, enabling higher concurrency.
- Each transaction sees a consistent snapshot of the database.

### Q22. What is multi-version concurrency control? What are its benefits and disadvantages in comparison to locking?

**Question 22: What is multi-version concurrency control? What are its benefits and disadvantages in comparison to locking?**

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

**Question 23: What do you mean by dispatcher in terms of Oracle?**

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
