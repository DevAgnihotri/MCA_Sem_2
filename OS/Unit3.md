1. What is a Process Control Block (PCB)?
2. What information is in the PCB? Discuss it with a diagram.
3. Define CPU scheduling. Why do we need scheduling?
4. What is the use of a job scheduler?
5. What are the performance criteria in CPU scheduling? Explain.

6. Compare and contrast single-threaded and multi-threaded processes.
7. Give some benefits of multithreaded programming.

8. Distinguish between multilevel queue scheduling and multilevel feedback queue scheduling.

9. What is deadlock? What are the necessary conditions for deadlock?
10. What are the conditions under which a deadlock situation may arise?
11. What is deadlock? How can we avoid deadlocks? Explain.
12. What do you mean by deadlock? Discuss various conditions for occurrence of deadlock. Also differentiate between deadlock detection and avoidance.
13. How is starvation different from deadlock? Explain.

14. What is deadlock detection algorithm? Explain it with an example.
15. Discuss deadlock avoidance using Banker’s algorithm.

16. Consider three processes, all arriving at time zero, with total execution times of 10, 20, and 30 units respectively. Each process spends the first 20% of execution time doing I/O, the next 70% doing computation, and the last 10% doing I/O again. The operating system uses a shortest remaining compute time first scheduling algorithm and schedules a new process either when the running process gets blocked on I/O or when the running process finishes its compute burst. Assume that all I/O operations can be overlapped as much as possible. For what percentage of time does the CPU remain idle?

    1. 0%
    2. 10.6%
    3. 30%
    4. 89.4%

17. Consider the set of 4 processes whose arrival time and burst time are given below:

    | Process No. | Arrival Time | Priority | CPU Burst | I/O Burst | CPU Burst |
    | ----------- | ------------ | -------- | --------- | --------- | --------- |
    | P1          | 0            | 2        | 1         | 5         | 3         |
    | P2          | 2            | 3        | 3         | 3         | 1         |
    | P3          | 3            | 1        | 2         | 3         | 1         |

    If the CPU scheduling policy is Priority Scheduling, calculate the average waiting time and average turnaround time. (Lower number means higher priority)

18. Consider the set of 4 processes whose arrival time and burst time are given below:

    | Process No. | Arrival Time | Burst Time | CPU Burst | I/O Burst | CPU Burst |
    | ----------- | ------------ | ---------- | --------- | --------- | --------- |
    | P1          | 0            | 3          | 2         | 2         |           |
    | P2          | 0            | 2          | 4         | 1         |           |
    | P3          | 2            | 1          | 3         | 2         |           |
    | P4          | 5            | 2          | 2         | 1         |           |

    If the CPU scheduling policy is Shortest Remaining Time First, calculate the average waiting time and average turnaround time.

19. Consider the following set of processes, with the arrival times and the CPU-burst times given in milliseconds:

    | Process | Arrival Time | Burst Time |
    | ------- | ------------ | ---------- |
    | P1      | 0            | 5          |
    | P2      | 1            | 3          |
    | P3      | 2            | 3          |
    | P4      | 3            | 1          |

    What is the average turnaround time for these processes with the preemptive shortest remaining processing time first (SRPT) algorithm?

---
