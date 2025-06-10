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

