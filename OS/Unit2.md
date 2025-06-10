# Unit 2

### **Process and States of a Process**

A **process** is simply a program that is currently running on your computer. It is an active task managed by the operating system, with its own memory and resources. For example, when you open a web browser, a process is created to run it.

### **What is Context Switch?**

A **context switch** is the process by which an operating system saves the state (context) of a currently running process so that it can resume execution later, and loads the state of another process to start or resume its execution. This allows the CPU to switch between multiple processes, enabling multitasking.

During a context switch, the OS saves information such as the program counter, registers, and memory mappings of the current process, and restores the saved information of the next process to run. Context switching is essential for process scheduling and efficient CPU utilization, but it introduces some overhead due to the time taken to save and restore process states.

#### **States of a Process**

A process typically moves through the following states during its lifetime:

- **New**: The process is being created.
- **Ready**: The process is waiting to be assigned to a processor.
- **Running**: Instructions are being executed.
- **Waiting (Blocked)**: The process is waiting for some event to occur (such as I/O completion).
- **Terminated**: The process has finished execution.

The operating system manages these states and transitions between them to ensure efficient process execution.

### **Principle of Concurrency**

Concurrency means that more than one process or task can make progress at the same time. In an operating system, this happens when the CPU quickly switches between different tasks, so it looks like they are running together, even if only one is running at any moment.

#### **Key Points of Concurrency**

- **Resource Sharing**: Multiple processes may need to access shared resources (like memory, files, or devices) at the same time.
- **Synchronization**: Mechanisms are required to coordinate access to shared resources to prevent conflicts and ensure data consistency.
- **Interleaving Execution**: The execution of processes is interleaved, meaning their instructions are mixed together in time, but not necessarily executed at the same moment.
- **Improved Utilization**: Concurrency helps in better utilization of CPU and other resources by keeping them busy.

Concurrency is fundamental in modern operating systems to achieve efficiency, responsiveness, and resource sharing among multiple users and applications.

### **Mutual Exclusion: Definition, Example, and Analogy**

**Mutual exclusion** is a property of concurrency control, which ensures that only one process or thread can access a critical section (shared resource) at a time. This prevents data inconsistency and race conditions.

#### **Example**

Suppose two processes, P1 and P2, both want to update a shared variable `counter`. If both enter the critical section at the same time and increment `counter`, the final value may be incorrect due to overlapping operations. Mutual exclusion ensures that only one process can increment `counter` at a time, preserving data integrity.

#### **Analogy**

Imagine a single-person restroom with a lock on the door. Only one person can use the restroom at a time. If someone is inside (critical section), others must wait outside (waiting state) until the restroom is free. The lock acts as a mechanism to enforce mutual exclusion, preventing multiple people from entering at once.

### Process Synchronization & Race Condition\*\*

As we understand in a multiprogramming environment a good number of processes compete for limited number of resources. Concurrent access to shared data at some time may result in data inconsistency for e.g.

Race condition is a situation in which the output of a process depends on the execution sequence of process. i.e. if we change the order of execution of different process the output **may change**.

---

### **General Structure of a process**

- **Initial Section**: Where process is accessing resources.

- **Entry Section**: Entry Section is that part of code where, each process request for permission to enter its critical section.

- **Critical Section**: Where process is access shared resources.

- **Exit Section**: It is the section where a process will exit from its critical section.

- **Remainder Section**: Remaining Code.

```c
P()
{
    While(T)
    {
        Initial Section
        Entry Section
        Critical Section
        Exit Section
        Remainder Section
    }
}
```

---

## **Critical Section**

A **critical section** is a part of a program where a process accesses shared resources (like variables, files, or devices) that can also be used by other processes. To prevent problems like data corruption or inconsistent results, only one process should be allowed in the critical section at a time. This ensures that shared resources are used safely and correctly.

### **Critical Section Problem**

The **critical section problem** is about making sure that when multiple processes (or programs) need to use the same shared resource (like a variable or file), only one process can use it at a time. If two or more processes try to use or change the shared resource at the same time, it can cause errors or unexpected results. The goal is to design a way for processes to take turns safely, so the shared resource is always used correctly.

**Goal:**
Design a protocol or mechanism so that:

- Only one process can be in its critical section at any given time (mutual exclusion).
- No process is unnecessarily delayed (progress).
- Every process gets a fair chance to enter its critical section (bounded waiting).

**Example:**
If two threads try to update the same bank account balance at the same time, without proper control, the final balance could be incorrect.

**Summary:**
The critical section problem is about ensuring safe and correct access to shared resources in concurrent systems.

### **Criterion to Solve Critical Section Problem**

- **Mutual Exclusion**:
  No two processes should be present inside the critical section at the same time, i.e. only one process is allowed in the critical section at an instant of time.
  _Mutexes_ (short for mutual exclusion) are a synchronization mechanism used to control access to shared resources in concurrent programming, preventing race conditions and data corruption.

- **Progress**:
  If no process is executing in its critical section and some processes wish to enter their critical sections, then only those processes that are not executing in their remainder sections can participate in deciding which will enter its critical section next (means other process will participate which actually wish to enter). There should be no deadlock.

- above 2 are mandatory criterion

- **Bounded Waiting**:
  There exists a bound or a limit on the number of times a process is allowed to enter its critical section and no process should wait indefinitely to enter the CS.
- - this one is optional criterion

## Peterson's Algorithm in Process Synchronization

Peterson's Algorithm is a classic solution to the critical section problem in process synchronization. It ensures mutual exclusion meaning only one process can access the critical section at a time and avoids race conditions. The algorithm uses two shared variables to manage the turn-taking mechanism between two processes ensuring that both processes follow a fair order of execution. It’s simple and effective for solving synchronization issues in two-process scenarios.

### What is Peterson's Algorithm?

- Peterson's Algorithm is a well-known solution for ensuring mutual exclusion in process synchronization. It is designed to manage access to shared resources between two processes in a way that prevents conflicts or data corruption.- It makes sure that only one process can be in the critical section (shared part) at a time.
- The algorithm uses two variables:
  - One variable shows if a process wants to enter the critical section.
  - The other variable shows whose turn it is.
- If both processes want to enter, the one whose turn it is goes first.
- It is useful when two programs need to share something safely without interfering with each other.

### Peterson's Algorithm: Parallel Code for Two Processes

Below is a side-by-side comparison of the Peterson's Algorithm code for processes Pi and Pj:

| **Process Pi**                | **Process Pj**                |
| ----------------------------- | ----------------------------- |
| do {                          | do {                          |
| flag[i] = true;               | flag[j] = true;               |
| turn = j;                     | turn = i;                     |
| while (flag[j] && turn == j); | while (flag[i] && turn == i); |
| // critical section           | // critical section           |
| flag[i] = false;              | flag[j] = false;              |
| // remainder section          | // remainder section          |
| } while(true);                | } while(true);                |

This table shows how both processes use the `flag` and `turn` variables to coordinate entry into the critical section, ensuring mutual exclusion.

### Working of Peterson's Algorithm

1. **Initial Setup**: At the start, both processes set their `flag` to `false`, meaning neither wants to enter the critical section. The `turn` variable is set to one of the process IDs (0 or 1), showing whose turn it is to enter.

2. **Wanting to Enter**: When a process wants to enter the critical section, it sets its `flag` to `true` to show its intention.

3. **Setting the Turn**: The process then sets the `turn` variable to the other process’s ID. This means it is giving the other process a chance to go first if it also wants to enter.

4. **Waiting Loop**: The process checks two things in a loop:

- If the other process also wants to enter (`flag` of the other process is `true`), and
- If it is the other process’s turn (`turn` is set to the other process’s ID),
- If both are true, the process waits. This lets the other process go first.

5. **Entering the Critical Section**: When the loop ends, it means it is safe for the process to enter the critical section. Now, it can safely use the shared resource.

6. **Exiting the Critical Section**: After finishing, the process sets its `flag` back to `false`. This shows it no longer wants to enter, so the other process can now try to enter the critical section.

This way, Peterson’s Algorithm makes sure only one process is in the critical section at a time, avoiding problems like race conditions.

## Dekker Algorithm (said and Done)

---

### Mutex vs Semaphore: Definition and Differences

| Feature       | Mutex                                                                      | Semaphore                                                                               |
| ------------- | -------------------------------------------------------------------------- | --------------------------------------------------------------------------------------- |
| Deadlock Risk | Higher if not used carefully.                                              | Lower, but can cause starvation if not managed well.                                    |
| Definition    | A lock that allows only one process/thread at a time to access a resource. | A signaling mechanism that controls access to a resource by multiple processes/threads. |
| Example       | Locking a file so only one thread can write.                               | Counting available slots in a buffer.                                                   |
| Ownership     | Has ownership; only the thread that locked it can unlock it.               | No ownership; any thread can signal or wait.                                            |
| Use Case      | Used for mutual exclusion (one at a time).                                 | Used for signaling and controlling access to multiple resources.                        |
| Value         | Binary (0 or 1)                                                            | Integer (can be >1)                                                                     |

**In simple terms:**

- Use a **mutex** when only one thread should access something at a time.
- Use a **semaphore** when you want to allow a certain number of threads to access a resource.

## Semaphores

Operating System Solution Using Semaphores

1. Semaphores are synchronization tools used to solve the n-process problem.(Peterson was a 2 process soln for bool vals)

2. A semaphore is like a counter that keeps track of how many resources are available.

3. It helps make sure that only a certain number of processes can use a resource at the same time.

4. A **semaphore** is a tool used by operating systems to help processes share resources safely.

5. A semaphore `S` is a simple integer variable. After initialization, it can only be accessed using two standard atomic operations: `wait(S)` and `signal(S)`.

6. The `wait(S)` operation was originally called `P(S)`, and the `signal(S)` operation was originally called `V(S)`.

---

| **wait(S)**                   | **signal(S)** |
| ----------------------------- | ------------- |
| `S--;`                        | `S++;`        |
| `while (S < 0) ;// Busy wait` |               |

### How Semaphores Work

### Example: Semaphore with Two Processes

Suppose we have two processes, **P1** and **P2**, and a semaphore `s` initialized to 1:

1. **P1 wants to enter the critical section:**

- P1 calls `wait(s)`. The value of `s` decreases from 1 to 0.
- P1 enters the critical section.

2. **P2 tries to enter the critical section while P1 is inside:**

- P2 calls `wait(s)`. Since `s` is 0, P2 cannot proceed and must wait.

3. **P1 exits the critical section:**

- P1 calls `signal(s)`. The value of `s` increases from 0 to 1.

4. **P2 can now enter:**

- Since `s` is now 1, P2's `wait(s)` succeeds, and P2 enters the critical section.

This ensures that only one process can be in the critical section at a time, maintaining mutual exclusion.

#### Why Use Semaphores?

- They help prevent problems like race conditions, where two or more processes try to change shared data at the same time.
- Semaphores make sure that resources are shared safely and fairly among processes.

Semaphores are important for making sure multiple processes can work together without causing errors or conflicts.

Here is the OCR (extracted) text from the image:

---

### Producer-Consumer Problem

- **Problem Definition** – The Producer-Consumer problem involves two types of processes: the Producer and the Consumer. The Producer generates data and places it into a buffer with _n_ bllocks, while the Consumer removes and uses this data. Both the Producer and Consumer can add or remove only one item at a time.

- The Producer must check if the buffer is full before adding a new item to avoid overflow.

- Similarly, the Consumer must check if the buffer is empty before removing an item to avoid underflow.

- The Producer and Consumer must be properly synchronized so that when one is accessing the buffer, the other waits, ensuring safe and consistent access to shared resources.

#### Semaphores Used

- **empty**: Counts the number of empty slots in the buffer as **E**
- **full**: Counts the number of full slots in the buffer as **F**
- **mutex**: Locks access to the buffer (mutual exclusion) as **S** (0,1)

- **E = 0**, **F = n** (initial state)

---

| **Producer()**                  | **Consumer()**                    |
| ------------------------------- | --------------------------------- |
| while (true) {                  | while (true) {                    |
| wait(empty); // Wait if full    | wait(full); // Wait if empty      |
| wait(mutex); // Enter critical  | wait(mutex); // Enter critical    |
| // Add item to buffer           | // Remove item from buffer        |
| signal(mutex); // Exit critical | signal(mutex); // Exit critical   |
| signal(full); // Increment full | signal(empty); // Increment empty |
| }                               | }                                 |

**Legend:**

- `empty`: Semaphore counting empty slots
- `full`: Semaphore counting filled slots
- `mutex`: Semaphore for mutual exclusion
- Producer waits if buffer is full; Consumer waits if buffer is empty.

### The Dining Philosophers Problem

The **Dining Philosophers Problem** is a classic synchronization problem that illustrates the challenges of resource sharing and process synchronization.

#### **Problem Definition**

- There are **K philosophers** seated around a circular table. (K will be an Odd num.)
- Between each pair of philosophers, there is **one chopstick** (so there are K chopsticks in total).
- Each philosopher alternates between two activities:
  - **Thinking**
  - **Eating**
- To eat, a philosopher needs to pick up **both** the chopsticks adjacent to them (the one on their left and the one on their right).
- A chopstick can be held by **only one philosopher at a time**.
- Philosophers must put down both chopsticks after eating so others can use them.

#### **Key Points**

- The problem demonstrates the need for proper synchronization to avoid issues such as **deadlock** (where no philosopher can eat) and **starvation** (where a philosopher never gets to eat).
- It is used to model situations where multiple processes compete for limited shared resources.

![Din Phy Problem](https://media.geeksforgeeks.org/wp-content/uploads/20231107114729/dining_philosopher_problem.png)

```c
void Philosopher(void)
 while (true)
   {  THINK();
      wait(CHOPSTICK[i]);
      wait(CHOPSTICK[i+1 mod 5]);
      EAT();
      signal(CHOPSTICK[i];)
      signal(CHOPSTICK[i+1 mod 5]);
   }
```

#### Ways to Treat Deadlock in the Dining Philosophers Problem

To treat **deadlock** in the **Dining Philosophers Problem** using **semaphores**, here are several effective strategies explained in **simple terms**:

---

##### 🔁 1. **Allow at Most (N–1) Philosophers to Sit at Once**

- **Idea**: If 5 philosophers are there, allow only **4 to try** picking up forks at the same time.
- **Why it works**: This ensures **at least one philosopher can eat**, freeing forks for others later — preventing circular wait.
- **How**: Use a semaphore `room` initialized to `N-1`. A philosopher must `wait(room)` before trying to pick up forks, and `signal(room)` after eating.

##### 🥢 1a. **Add an Extra Chopstick**

- **Idea**: Place one more chopstick than the number of philosophers (i.e., 6 chopsticks for 5 philosophers).
- **Why it works**: With more chopsticks than philosophers, at least one philosopher can always pick up two chopsticks and eat, breaking the deadlock cycle.
- **How**: Simply provide an extra chopstick on the table. Philosophers pick up their two adjacent chopsticks as usual.

---

##### 🔄 2. **Pick Up Both Forks Together (Atomic Operation)**

- **Idea**: A philosopher only proceeds if **both left and right forks** are available.
- **Why it works**: Prevents a philosopher from holding one fork and waiting forever for the other.
- **How**: Use a critical section or single semaphore per philosopher that checks and locks both forks at once.

---

##### 🔃 3. **Use Asymmetry in Fork Picking**

- **Idea**: Change the order of picking forks for some philosophers.
- **Why it works**: Avoids circular wait condition by breaking the pattern.
- **How**: For example:

  - Odd-numbered philosophers: pick **left**, then **right**
  - Even-numbered philosophers: pick **right**, then **left**

---

##### 🔐 4. **Use a Global Semaphore for Fork Access**

- **Idea**: Introduce a single semaphore to limit how many philosophers can access forks at once.
- **Why it works**: Helps control access to shared resources.
- **How**: Set a semaphore `mutex` initialized to `1`, and wrap fork-picking logic inside a `wait(mutex)` and `signal(mutex)` block.

---

##### 🛠️ 5. **Monitor with Additional States (Using Arrays)**

- **Idea**: Track philosopher states: THINKING, HUNGRY, EATING.
- **Why it works**: Only allow eating when neighbors are not eating.
- **How**:

  - Use semaphores per philosopher (`S[i]`)
  - Use a `mutex` to control access to state checks
  - Before eating, a philosopher checks neighbors’ states

---

##### 🔚 Summary Table

| Method           | Core Idea        | Prevents Deadlock by   |
| ---------------- | ---------------- | ---------------------- |
| Asymmetry        | Fork order       | Breaking circular wait |
| Atomic Fork Pick | All or none      | No partial holding     |
| Global Semaphore | Critical section | Controlled entry       |
| N–1 Philosophers | Limit access     | Avoiding full lock     |
| State Monitoring | Track status     | Conditional eating     |

## Sleeping Barber Problem in Process Synchronization

The **Sleeping Barber problem** is a classic example in process synchronization, used to show how to coordinate multiple processes (like customers and a barber) in a concurrent system.

### Problem Definition

- There is a barber shop with **one barber** and a certain number of **waiting chairs** for customers.
- **Customers** arrive at random times:
  - If there is an empty chair, the customer sits and waits.
  - If all chairs are full, the customer leaves.
- The **barber**:
  - If there are no customers, the barber goes to sleep.
  - When a customer arrives and the barber is sleeping, the customer wakes up the barber.
  - The barber cuts hair for one customer at a time.
  - After finishing, the barber checks for waiting customers. If there are any, he serves the next one; otherwise, he goes back to sleep.

### Key Points

- The problem demonstrates the need for **proper synchronization** to avoid issues like:
  - **Deadlock**: Where the system gets stuck and no progress is made.
  - **Starvation**: Where a customer never gets served.
- The goal is to coordinate the actions of the barber and customers so that:
  - No two customers get their hair cut at the same time.
  - The barber does not cut hair when there are no customers.
  - Customers are served in the order they arrive (FIFO).

### Solution Using Semaphores

To solve the Sleeping Barber problem, we use semaphores to synchronize the barber and customers:

- **waiting**: Counts the number of customers waiting (initially 0).
- **mutex**: Ensures mutual exclusion when updating the number of waiting customers.
- **barber**: Signals the barber when a customer arrives.
- **customer**: Signals a customer when the barber is ready.

#### Pseudocode

```c
semaphore waiting = 0;    // Number of waiting customers
semaphore mutex = 1;      // For mutual exclusion
semaphore barber = 0;     // Barber is sleeping
semaphore customer = 0;   // Customer is waiting

Barber() {
  while (true) {
    wait(customer);       // Wait for a customer to arrive
    wait(mutex);          // Enter critical section
    waiting--;            // One less waiting customer
    signal(barber);       // Barber is ready
    signal(mutex);        // Exit critical section
    // Cut hair
  }
}

Customer() {
  wait(mutex);            // Enter critical section
  if (waiting < N) {      // If there is a free chair
    waiting++;            // Increment waiting customers
    signal(customer);     // Notify barber
    signal(mutex);        // Exit critical section
    wait(barber);         // Wait for barber to be ready
    // Get hair cut
  } else {
    signal(mutex);        // Exit critical section
    // Leave (no chair available)
  }
}
```

### Summary

- The Sleeping Barber problem models real-world scenarios where resources (like a barber) must be shared among multiple users (customers) in a synchronized way.
- It teaches how to use semaphores to avoid deadlock and starvation, ensuring fair and efficient service.
- This problem is important for understanding process synchronization in operating systems.

## Test-and-Set Operation (Hardware Solution for Mutual Exclusion)

The **Test-and-Set** operation is a simple hardware-supported instruction used to solve the critical section problem and achieve mutual exclusion in multiprocessor systems.

### What is Test-and-Set?

- **Test-and-Set** is an **atomic** (indivisible) operation provided by hardware.
- It checks the value of a variable (usually a lock), and **sets it to true** (locked) in a single, uninterruptible step.
- The operation returns the old value of the variable.

### How Does It Work?

Suppose we have a shared variable `lock` initialized to `false` (unlocked):

```c
// Pseudocode for Test-and-Set
boolean TestAndSet(boolean *lock) {
  boolean old = *lock;
  *lock = true;
  return old;
}
```

- When a process wants to enter the critical section, it repeatedly calls `TestAndSet(&lock)`.
- If `TestAndSet` returns `false`, the process enters the critical section (it acquired the lock).
- If it returns `true`, another process is already in the critical section, so it keeps trying (busy waiting).

### Example Usage

```c
while (TestAndSet(&lock)) {
  // Busy wait (spin)
}
// Critical section
// ...
lock = false; // Release lock
```

### Simple Explanation

- Think of `Test-and-Set` as a special lock on a door.
- When you try to open the door, you check if it’s locked and lock it at the same time.
- If it was unlocked, you get in and lock it behind you.
- If it was already locked, you wait and keep trying until it’s free.

### Key Points

- **Atomicity**: The operation cannot be interrupted, so no two processes can enter the critical section at the same time.
- **Busy Waiting**: Processes may keep checking the lock in a loop (called "spinlock").
- **Hardware Support**: Most modern CPUs provide this as a single instruction.

### Summary

Test-and-Set is a hardware-based solution for mutual exclusion. It is simple and effective for protecting critical sections, but can cause busy waiting if many processes compete for the lock.
