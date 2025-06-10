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

| Scheduler Type      | What It Does                                                                 |
| ------------------- | ---------------------------------------------------------------------------- |
| Long-term (Job)     | Selects which jobs/processes enter the system (from job pool to ready queue).|
| Short-term (CPU)    | Picks which ready process gets the CPU next.                                 |
| Criteria / Scheduler Type | Long-term (Job) 

| Criteria           | LT (Long-term)            | ST (Short-term)              | MT (Medium-term)           |
|--------------------|---------------------------|------------------------------|----------------------------|
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
