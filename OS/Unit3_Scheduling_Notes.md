# Scheduling Concepts, Performance Criteria, and Process Management

## Table of Contents

1. Scheduling Concepts
2. Performance Criteria
3. Process States
4. Process Transition Diagram
5. Schedulers
6. Process Control Block (PCB) [Q1, Q2]
7. Process Address Space
8. Process Identification Information
9. Threads and Their Management
10. Multiprocessor Scheduling
11. Scheduling Algorithms
12. Deadlock in Operating Systems: Detailed Notes and Solved Questions

---

## 1. Scheduling Concepts [Q4]

**CPU Scheduling** is the process of deciding which process in the ready queue should be allocated the CPU next. The main goal is to make the best use of the CPU and improve system performance.

### Why do we need scheduling? [Q4]

- To maximize CPU utilization (keep CPU busy as much as possible)
- To provide fairness (every process gets a chance)
- To minimize waiting time, response time, and turnaround time
- To ensure efficient and smooth execution of processes

**Definition:**

> CPU scheduling is the method used by the operating system to decide which process will use the CPU at a given time.

---

## 2. Performance Criteria [Q6]

Performance criteria are the standards used to measure the effectiveness of a CPU scheduling algorithm.

| Criteria        | Description                                                                   |
| --------------- | ----------------------------------------------------------------------------- |
| CPU Utilization | Percentage of time the CPU is busy. Higher is better.                         |
| Throughput      | Number of processes completed per unit time. Higher is better.                |
| Turnaround Time | Total time taken from submission to completion of a process. Lower is better. |
| Waiting Time    | Total time a process spends in the ready queue. Lower is better.              |
| Response Time   | Time from submission to first response. Lower is better.                      |
| Fairness        | All processes get a fair share of CPU.                                        |

**Explanation:**

- Good scheduling algorithms try to maximize CPU utilization and throughput, and minimize turnaround, waiting, and response times.

---

## 3. Process States

A process can be in one of several states during its lifetime:

| State      | Description                                     |
| ---------- | ----------------------------------------------- |
| New        | Process is being created.                       |
| Ready      | Process is waiting to be assigned to the CPU.   |
| Running    | Process is currently being executed by the CPU. |
| Waiting    | Process is waiting for some event (like I/O).   |
| Terminated | Process has finished execution.                 |

---

## 4. Process Transition Diagram

A process moves between states as shown below:

```
[New] → [Ready] → [Running] → [Terminated]
                ↓         ↑
             [Waiting] ←
```

- **New → Ready:** Process is created and ready to run.
- **Ready → Running:** Scheduler picks the process for execution.
- **Running → Waiting:** Process waits for I/O or event.
- **Waiting → Ready:** Event completes, process is ready again.
- **Running → Terminated:** Process finishes execution.

---

## 5. Schedulers [Q5]

**Definition:**  
A **scheduler** is a part of the operating system that decides which process should move to the next stage of execution. Schedulers help manage how processes are selected for execution, admission, or suspension.

### Types of Schedulers

| Scheduler Type            | What It Does                                                                  |
| ------------------------- | ----------------------------------------------------------------------------- |
| Long-term (Job)           | Selects which jobs/processes enter the system (from job pool to ready queue). |
| Short-term (CPU)          | Picks which ready process gets the CPU next.                                  |
| Criteria / Scheduler Type | Long-term (Job)                                                               |

| Criteria           | LT (Long-term)            | ST (Short-term)              | MT (Medium-term)           |
| ------------------ | ------------------------- | ---------------------------- | -------------------------- |
| **Function**       | Admits new processes      | Selects ready process to run | Suspends/resumes processes |
| **Frequency**      | Infrequent                | Very frequent                | Occasional                 |
| **Responsibility** | Controls multiprogramming | Allocates CPU to processes   | Manages swapping in/out    |
| **Decision**       | Which jobs enter system   | Which process runs next      | Which to suspend/resume    |

### Why are Schedulers Important?

- They help balance system load and resource usage.
- Ensure efficient and fair use of CPU and memory.
- Improve overall system performance by managing process flow.

---

---

## 6. Process Control Block (PCB) [Q1, Q2]

### What is a Process Control Block (PCB)? [Q1]

A **Process Control Block (PCB)** is a data structure used by the operating system to store all information about a process. It acts like the "identity card" of a process.

### Information in the PCB [Q2]

A PCB contains:

- **Process State:** (new, ready, running, waiting, terminated)
- **Process ID (PID):** Unique number for each process
- **Program Counter:** Address of the next instruction to execute
- **CPU Registers:** Values of all CPU registers for the process
- **Memory Management Info:** Base/limit registers, page tables, segment tables
- **Accounting Info:** CPU used, time limits, job/account numbers
- **I/O Status Info:** List of I/O devices allocated, open files

#### Diagram of PCB [Q2]

```
+---------------------+
| Process State       |
+---------------------+
| Process ID (PID)    |
+---------------------+
| Program Counter     |
+---------------------+
| CPU Registers       |
+---------------------+
| Memory Info         |
+---------------------+
| Accounting Info     |
+---------------------+
| I/O Status Info     |
+---------------------+
```

---

## 7. Process Address Space

- The address space of a process is the set of memory addresses that the process can use.
- It includes code, data, stack, and heap segments.
- Each process has its own address space, isolated from others for security and stability.

---

## 8. Process Identification Information

- Each process is identified by a unique **Process ID (PID)**.
- Other identification info may include user ID, group ID, parent process ID, etc.
- This information helps the OS manage and control processes.

---

## 9. Threads and Their Management

### What is a Thread?

- A **thread** is the smallest unit of execution in a process. It is like a single line of work inside a program.
- Each process can have one or more threads. If there is only one, it is called a single-threaded process. If there are many, it is called a multi-threaded process.
- Threads in the same process share memory and resources, but each thread has its own program counter, registers, and stack.

### Thread Management

- **Thread management** means creating, running, and ending threads in a process.
- Threads can be managed by the operating system (kernel-level threads) or by user-level libraries (user-level threads).
- Main operations:
  - **Creation:** Making a new thread inside a process.
  - **Scheduling:** Deciding which thread runs next.
  - **Synchronization:** Making sure threads do not interfere with each other (using locks, semaphores, etc.).
  - **Termination:** Ending a thread when its work is done.

### Advantages of Threads

- Faster context switching than processes (less overhead).
- Easy sharing of data between threads (since they share memory).
- Useful for tasks that can run in parallel (like web servers, games, etc.).

---

### Q6. Compare and contrast single-threaded and multi-threaded processes.

| Feature           | Single-threaded Process                       | Multi-threaded Process                    |
| ----------------- | --------------------------------------------- | ----------------------------------------- |
| Number of Threads | Only one                                      | Two or more                               |
| Parallelism       | No parallel execution within the process      | Threads can run in parallel               |
| Blocking          | If the thread blocks, the whole process waits | If one thread blocks, others can continue |
| Design Complexity | Simpler to design and debug                   | More complex (requires synchronization)   |
| Resource Sharing  | No sharing within process (only one thread)   | Threads share memory and resources        |
| Context Switching | Higher overhead (process-level)               | Lower overhead (thread-level)             |

**Summary:**

- **Single-threaded process:**

  - Has only one thread of execution.
  - If the thread is blocked (e.g., waiting for I/O), the whole process waits.
  - Simpler to design and debug.

- **Multi-threaded process:**
  - Has two or more threads running in the same process.
  - Threads can run in parallel, improving performance.
  - If one thread is blocked, others can continue.
  - More complex to manage (need synchronization).

---

### Q7. Give some benefits of multithreaded programming.

- **Responsiveness:** The program remains active even if some threads are blocked, improving user experience.
- **Resource sharing:** Threads within the same process share memory and resources, making communication and data sharing efficient.
- **Economy:** Creating and managing threads is less resource-intensive than creating and managing processes.
- **Scalability:** Multithreaded programs can utilize multiple CPUs/cores, improving performance on multiprocessor systems.
- **Faster context switching:** Switching between threads is quicker than switching between processes, reducing overhead.
- **Simplified program structure:** Tasks that are logically concurrent (like handling multiple client requests) can be implemented more naturally.
- **Improved throughput:** Multiple threads can perform different tasks simultaneously, increasing the overall work done.
- **Better resource utilization:** Idle time (e.g., waiting for I/O) can be minimized as other threads continue execution.
- **Parallelism:** Threads can execute in parallel, making programs faster for suitable workloads.
- **Modularity:** Programs can be divided into smaller, manageable threads, improving code organization and maintainability.

---

## 10. Multiprocessor Scheduling

### What is Multiprocessor Scheduling?

- **Multiprocessor scheduling** is the method used by the operating system to decide which process or thread runs on which CPU/core in a system with more than one processor.

### Types of Multiprocessor Systems

- **Symmetric Multiprocessing (SMP):** All processors are equal; OS can schedule any process on any processor.
- **Asymmetric Multiprocessing (AMP):** One processor is the master, others are workers; master assigns tasks.

### Scheduling Approaches

- **Load sharing:** Distribute work evenly among all processors.
- **Processor affinity:** Try to keep a process on the same processor to use cache efficiently.
- **Real-time scheduling:** For systems needing guaranteed response times.

### Challenges

- Avoiding conflicts when multiple processors access shared data.
- Balancing the load so all processors are used efficiently.

---

### Q8. Distinguish between multilevel queue scheduling and multilevel feedback queue scheduling.

| Feature                      | Multilevel Queue Scheduling                         | Multilevel Feedback Queue Scheduling                        |
| ---------------------------- | --------------------------------------------------- | ----------------------------------------------------------- |
| 1. Queue Structure           | Multiple fixed queues for different process types   | Multiple queues, but processes can move between them        |
| 2. Process Movement          | No movement between queues                          | Processes can move up or down between queues                |
| 3. Scheduling Algorithm      | Each queue has its own fixed algorithm              | Algorithms can change as processes move between queues      |
| 4. Flexibility               | Less flexible; static assignment                    | More flexible; dynamic adjustment based on process behavior |
| 5. Priority Handling         | Priorities are fixed per queue                      | Priorities can change for a process over time               |
| 6. Starvation                | Lower-priority queues may suffer from starvation    | Feedback mechanism helps reduce starvation                  |
| 7. Adaptability              | Not adaptive to process behavior                    | Adapts to how processes use CPU (CPU-bound vs I/O-bound)    |
| 8. Complexity                | Simpler to implement                                | More complex to implement                                   |
| 9. Example Use               | Separating system, interactive, and batch processes | General-purpose systems needing fairness and responsiveness |
| 10. Performance Optimization | Optimized for predictable workloads                 | Optimized for mixed and unpredictable workloads             |

---

## 11. Scheduling Algorithms

**Scheduling algorithms** are rules used by the operating system to decide the order in which processes get the CPU. Each algorithm has its own way of choosing which process runs next. Here are the main types, with simple explanations and examples:

### 1. First-Come, First-Served (FCFS)

- **How it works:** The process that arrives first gets the CPU first. Like standing in a queue at a shop.
- **Example:**
  - Processes: P1 (arrives at 0, burst 4), P2 (arrives at 1, burst 3), P3 (arrives at 2, burst 2)
  - Order: P1 → P2 → P3
- **How to solve:**
  - List processes in order of arrival.
  - Calculate waiting and turnaround times by adding burst times of earlier processes.

### 2. Shortest Job First (SJF)

- **How it works:** The process with the shortest burst time runs first.
- **Types:**
  - **Non-preemptive SJF:** Once a process starts, it runs to completion.
  - **Preemptive SJF (Shortest Remaining Time First, SRTF):** If a new process arrives with a shorter burst time than the remaining time of the current process, the CPU switches to the new process.
- **Example:**
  - Processes: P1 (burst 6), P2 (burst 2), P3 (burst 8), P4 (burst 3)
  - Order (non-preemptive): P2 → P4 → P1 → P3
- **How to solve:**
  - Sort processes by burst time.
  - If arrival times differ, pick the shortest job among those that have arrived.

### 3. Priority Scheduling

- **How it works:** Each process has a priority. The process with the highest priority runs first (lower number = higher priority).
- **Types:**
  - **Non-preemptive Priority:** The running process is not interrupted; new higher-priority processes wait.
  - **Preemptive Priority:** If a new process arrives with a higher priority, it preempts the current process.
- **Example:**
  - P1 (priority 2), P2 (priority 1), P3 (priority 3)
  - Order: P2 → P1 → P3
- **How to solve:**
  - Sort by priority.
  - If priorities are equal, use FCFS among them.

### 5. Round Robin (RR)

- **How it works:** Each process gets a fixed time slice (quantum). After its turn, it goes to the back of the queue if not finished.
- **Example:**
  - Quantum = 2 units. P1 (burst 5), P2 (burst 3), P3 (burst 1)
  - Order: P1(2) → P2(2) → P3(1) → P1(3) → P2(1)
- **How to solve:**
  - Go in a circle, giving each process the quantum.
  - Subtract quantum from burst time, repeat until all are done.

---

# Deadlock in Operating Systems: Detailed Notes and Solved Questions

---

## Deadlock: System Model

- In a computer system, **deadlock** is a situation where a set of processes are blocked because each process is holding a resource and waiting for another resource held by another process.
- **System model:**
  - Resources (like CPU, memory, printers) are assigned to processes.
  - Processes request and release resources dynamically.
  - Resources can be of different types: single instance (one printer) or multiple instances (memory blocks).

---

## Deadlock Characterization

### Q9. What is deadlock? What are the necessary conditions for deadlock?

**Question 9: What is deadlock? What are the necessary conditions for deadlock?**

- **Deadlock** is a state in which two or more processes are unable to proceed because each is waiting for a resource held by the other(s).
- **Necessary conditions for deadlock (Coffman conditions):**
  1. **Mutual Exclusion:** At least one resource must be held in a non-sharable mode.
  2. **Hold and Wait:** A process is holding at least one resource and waiting to acquire additional resources held by others.
  3. **No Preemption:** Resources cannot be forcibly taken away from a process; they must be released voluntarily.
  4. **Circular Wait:** There exists a set of processes {P1, P2, ..., Pn} such that P1 is waiting for a resource held by P2, P2 for P3, ..., and Pn for P1.

---

### Q10. What are the conditions under which a deadlock situation may arise?

**Question 10: What are the conditions under which a deadlock situation may arise?**

- Deadlock can occur if all four Coffman conditions (listed above) are true at the same time in the system.

---

### Q11. What is deadlock? How can we avoid deadlocks? Explain.

**Question 11: What is deadlock? How can we avoid deadlocks? Explain.**

- **Deadlock** is when processes are stuck waiting for each other forever.
- **Deadlock avoidance** means designing the system so that deadlocks never happen.
- **Methods to avoid deadlocks:**
  - Do not allow at least one of the four necessary conditions.
  - Use algorithms like the **Banker’s algorithm** to check if granting a resource will lead to a safe state.
  - Request all resources at once (prevents hold and wait).
  - Impose an order on resource requests (prevents circular wait).

---

### Q12. What do you mean by deadlock? Discuss various conditions for occurrence of deadlock. Also differentiate between deadlock detection and avoidance.

**Question 12: What do you mean by deadlock? Discuss various conditions for occurrence of deadlock. Also differentiate between deadlock detection and avoidance.**

- **Deadlock** is a situation where processes cannot proceed because they are each waiting for resources held by others.
- **Conditions for deadlock:** Mutual exclusion, hold and wait, no preemption, circular wait.
- **Deadlock detection:** The system allows deadlocks to occur but has a way to detect and recover from them (e.g., using a wait-for graph).
- **Deadlock avoidance:** The system carefully allocates resources to ensure deadlocks never occur (e.g., Banker’s algorithm).

| Aspect                | Deadlock Detection       | Deadlock Avoidance        |
| --------------------- | ------------------------ | ------------------------- |
| When deadlock occurs? | Allowed to happen        | Prevented from happening  |
| System action         | Detects and recovers     | Avoids unsafe allocations |
| Example               | Wait-for graph, recovery | Banker’s algorithm        |

---

## Deadlock Prevention

- **Deadlock prevention** means designing the system so that at least one of the four necessary conditions for deadlock cannot hold.
- Examples:
  - **Mutual Exclusion:** Use only when necessary.
  - **Hold and Wait:** Require processes to request all resources at once.
  - **No Preemption:** Allow resources to be taken away if needed.
  - **Circular Wait:** Impose a strict order on resource requests.

---

## Deadlock Avoidance

- **Deadlock avoidance** means the system checks every resource request and only grants it if it will not lead to a deadlock.
- The most famous avoidance algorithm is the **Banker’s algorithm**.

---

### Q15. Discuss deadlock avoidance using Banker’s algorithm.

**Question 15: Discuss deadlock avoidance using Banker’s algorithm.**

- **Banker’s algorithm** checks if granting a resource request will leave the system in a safe state.
- If yes, the request is granted; if not, the process must wait.
- **Safe state:** There is at least one sequence in which all processes can finish.
- **How it works:**
  1. Each process tells the system its maximum resource needs.
  2. The system checks if resources can be allocated safely.
  3. If yes, resources are given; if not, the process waits.
- **Example Table:**
  | Process | Max Need | Allocated | Available | Need |
  |---------|----------|-----------|-----------|------|
  | P1 | 7 | 5 | 3 | 2 |
  | ... | ... | ... | ... | ... |

---

## Deadlock Detection

- **Deadlock detection** means the system allows deadlocks to happen but has a way to find them and recover.
- Uses a **wait-for graph** to detect cycles (deadlocks).

### Q14. What is deadlock detection algorithm? Explain it with an example.

**Question 14: What is deadlock detection algorithm? Explain it with an example.**

- **Wait-for graph algorithm:**
  - Each process is a node; an edge from P1 to P2 means P1 is waiting for a resource held by P2.
  - If there is a cycle in the graph, a deadlock exists.
- **Example:**
  - P1 waits for P2, P2 waits for P3, P3 waits for P1 → cycle → deadlock.

---

## Recovery from Deadlock

- **Recovery** means ending the deadlock by:
  - Killing one or more processes in the cycle.
  - Preempting (taking away) resources from some processes.
  - Rolling back processes to a safe state.

---

### Q13. How is starvation different from deadlock? Explain.

**Question 13: How is starvation different from deadlock? Explain.**

- **Starvation** is when a process waits indefinitely because it never gets the resources it needs, even though they are available.
- **Deadlock** is when a group of processes are all waiting for each other, and none can proceed.
- **Difference:**
  - In deadlock, processes are stuck because of each other.
  - In starvation, a process is stuck because the system keeps choosing other processes over it.

| Aspect   | Deadlock                       | Starvation                 |
| -------- | ------------------------------ | -------------------------- |
| Cause    | Circular waiting for resources | Resource allocation policy |
| Solution | Detection, avoidance, recovery | Fair scheduling            |

---

## Summary Table: Deadlock Handling

| Method     | What It Does                          | Example/Tool        |
| ---------- | ------------------------------------- | ------------------- |
| Prevention | Stops deadlock from happening         | Resource ordering   |
| Avoidance  | Checks before granting resources      | Banker’s algorithm  |
| Detection  | Finds deadlocks after they happen     | Wait-for graph      |
| Recovery   | Ends deadlock by killing/rolling back | Process termination |

## Banker’s Algorithm: Simple Explanation

**Banker’s Algorithm** is a deadlock avoidance algorithm used by operating systems to safely allocate resources to processes. It is called "Banker’s" because it works like a bank deciding whether to grant a loan, making sure it never runs out of money (resources).

### How Banker’s Algorithm Works

1. **Processes declare maximum needs:**  
  Each process tells the system the maximum number of each resource it may need.

2. **Resource allocation check:**  
  When a process requests resources, the system checks if it can safely grant the request without risking deadlock.

3. **Safe state:**  
  The system is in a *safe state* if there is at least one sequence in which all processes can finish, even if they all ask for their maximum resources.

4. **Grant or wait:**  
  - If granting the request keeps the system in a safe state, the resources are allocated.
  - If not, the process must wait.

### Steps of the Algorithm

- **Step 1:** Check if the request is less than or equal to the process’s declared maximum need.
- **Step 2:** Check if the requested resources are available.
- **Step 3:** Pretend to allocate the resources and check if the system remains in a safe state.
- **Step 4:** If safe, actually allocate the resources. If not, make the process wait.

### Example Table

| Process | Max Need | Allocated | Available | Need (Max - Allocated) |
|---------|----------|-----------|-----------|------------------------|
| P1      | 7        | 5         | 3         | 2                      |
| P2      | 3        | 2         |           | 1                      |
| ...     | ...      | ...       | ...       | ...                    |

### Simple Example

Suppose there are 3 processes (P1, P2, P3) and 10 total resources.  
- P1 has 3, P2 has 2, P3 has 2 (total allocated = 7, so 3 available).
- If P1 requests 2 more, the system checks:
  - Is 2 ≤ P1’s max need? Yes.
  - Are 2 resources available? Yes.
  - If granted, can all processes finish? If yes, grant; if not, P1 waits.

### Key Points

- Prevents deadlock by only granting requests that keep the system safe.
- Needs to know each process’s maximum resource needs in advance.
- Used in systems where resource allocation must be carefully controlled.

---
