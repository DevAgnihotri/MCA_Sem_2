# Memory Management Concepts in Operating Systems

---

## Basic Bare Machine

- A **bare machine** is a computer system without any operating system or software support.
- In this setup, there is no user interface, no memory protection, and no multitasking.
- Programs are loaded and run directly on the hardware, often using switches, punch cards, or simple loaders.
- **Problems:**
  - No protection: One program can overwrite another.
  - No convenience: Users must manage everything manually.
  - No multitasking: Only one program runs at a time.
- **Use:** Early computers (before operating systems were developed).

---

## Resident Monitor

- A **resident monitor** is an early form of operating system that stays ("resides") in memory while programs are run.
- It automates the loading and running of user programs, and provides basic control over the system.
- **How it works:**
  - The monitor is loaded into a reserved part of memory.
  - User programs are loaded into the rest of memory.
  - When a program finishes, control returns to the monitor.
- **Features:**
  - Simple job sequencing (runs one job after another).
  - Basic error handling and device management.
- **Limitations:**
  - No multitasking or memory protection.
  - Still only one program at a time.

---

## Multiprogramming with Fixed Partitions

- **Multiprogramming** allows multiple programs to be in memory at the same time, so the CPU can switch between them.
- **Fixed partitions:** Memory is divided into fixed-size blocks (partitions) when the system starts.
- Each partition can hold one program/job.
- **How it works:**
  - When a program arrives, it is loaded into a free partition.
  - If no partition is free, the program waits.
  - The OS switches the CPU between programs to keep it busy.
- **Advantages:**
  - Simple to implement.
  - Allows some multitasking.
- **Disadvantages:**
  - Internal fragmentation: Wasted space if a program is smaller than its partition. 
  - Number and size of partitions are fixed; not flexible.

| Partition | Size (KB) | Program Loaded |
| --------- | --------- | -------------- |
| 1         | 100       | A              |
| 2         | 200       | B              |
| 3         | 300       | C              |

---

## Multiprogramming with Variable Partitions

- Memory is divided into partitions **dynamically** as programs arrive.
- Each program gets exactly as much memory as it needs (no fixed sizes).
- **How it works:**
  - When a program arrives, the OS finds a block of memory large enough for it.
  - When a program finishes, its memory is freed and can be reused.
- **Advantages:**
  - No internal fragmentation (less wasted space).
  - More flexible use of memory.
- **Disadvantages:**
  - External fragmentation: Free memory is split into small pieces over time.
  - More complex to manage (need algorithms like first-fit, best-fit, worst-fit).

| Program | Size Needed (KB) | Memory Block Allocated |
| ------- | ---------------- | ---------------------- |
| X       | 120              | 120                    |
| Y       | 80               | 80                     |
| Z       | 200              | 200                    |

---

## Protection Schemes

- **Protection** in memory management means preventing one program from accessing or
  modifying another program's memory.
- **Why needed?**
  - To keep programs from interfering with each other.
  - To protect the operating system from user programs.
- **Common protection schemes:**
  - **Base and Limit Registers:**
    - Each program is given a base address (start of its memory) and a limit (size).
    - The CPU checks every memory access to make sure it is within the allowed range.
  - **Segmentation:**
    - Memory is divided into segments (code, data, stack), each with its own base and limit.
    - Provides fine-grained protection.
  - **Paging:**
    - Memory is divided into small fixed-size pages.
    - The OS controls which pages belong to which program.
    - Prevents programs from accessing each other's pages.
- **Modern OS:** Use a combination of these methods, often with hardware support
  (like MMU - Memory Management Unit).

---

# Paging, Segmentation, and Virtual Memory Concepts

## 1. Differentiate between paging and segmentation. [Q1]

**Question 1: Differentiate between paging and segmentation.**

| Feature       | Paging                                | Segmentation                                  |
| ------------- | ------------------------------------- | --------------------------------------------- |
| Division      | Memory divided into fixed-size pages  | Memory divided into variable-size segments    |
| Size          | All pages are the same size           | Segments can be different sizes               |
| Address       | Logical address: page number + offset | Logical address: segment number + offset      |
| Fragmentation | Internal fragmentation possible       | External fragmentation possible               |
| Use           | Used for simplicity and efficiency    | Used for logical division (code, data, stack) |
| Protection    | Harder to protect logical units       | Easy to protect segments (code, data, etc.)   |

- **Paging**: Breaks memory into equal-sized blocks (pages). Good for managing memory efficiently,
  but can waste space inside pages (internal fragmentation).
- **Segmentation**: Breaks memory into logical units (segments) like code, data, stack. More natural
  for programmers, but can waste space between segments (external fragmentation).

---

## 2. Define Paging and Segmentation [Q2]

**Question 2: Define Paging and Segmentation**

- **Paging** is a memory management scheme that eliminates the need for contiguous allocation of physical memory. The process's memory is divided into fixed-size pages, and physical memory is divided into frames of the same size. Pages are mapped to frames using a page table.
- **Segmentation** is a memory management technique where each job is divided into several segments of different lengths, such as code, data, and stack. Each segment is loaded into a different part of memory.

---

## 3. Define Paging scheme with an example in detail. [Q3]

**Question 3: Define Paging scheme with an example in detail.**

- In **paging**, both logical and physical memory are divided into fixed-size blocks: pages (logical) and frames (physical).
- The operating system keeps a **page table** for each process, which maps logical pages to physical frames.
- When a process needs to access memory, the CPU uses the page table to translate the logical address to a physical address.

**Example:**

- Suppose page size = 1 KB, logical address = 2048 (2 KB), and the page table says page 2 is in frame 5.
- Logical address 2048 = page 2, offset 0.
- Physical address = frame 5 × 1 KB + 0 = 5120.

| Logical Page | Physical Frame |
| ------------ | -------------- |
| 0            | 3              |
| 1            | 1              |
| 2            | 5              |
| 3            | 2              |

---

## Segmentation (Detailed)

- In **segmentation**, a program is divided into segments (code, data, stack, etc.), each with its own length.
- Each segment has a segment number and an offset.
- The OS keeps a **segment table** with the base address and length of each segment.
- Logical address = segment number + offset; physical address = base + offset.

**Example:**

- Segment table:
  | Segment | Base Address| Length |
  |---------|-------------|--------|
  | 0 | 1000 | 400 |
  | 1 | 2000 | 600 |
  | 2 | 3000 | 500 |
- Logical address (1, 50) = segment 1, offset 50 → physical address = 2000 + 50 = 2050.

---

## Paged Segmentation

- **Paged segmentation** combines paging and segmentation.
- Each segment is divided into pages, and each page is mapped to frames in physical memory.
- Logical address: segment number + page number + offset.
- This approach reduces both internal and external fragmentation and allows for flexible memory management.

---

## Virtual Memory Concepts [Q4]

**Question 4: What is Virtual Memory? How is it implemented?**

- **Virtual memory** is a technique that allows programs to use more memory than is
  physically available by using disk space as an extension of RAM.
- Each process gets its own virtual address space, which is mapped to physical memory as needed.
- The OS uses **paging** or **segmentation** to manage virtual memory.
- When a program accesses a part of memory that is not in RAM, a **page fault** occurs, and the OS loads the required page from disk into RAM.

**Implementation:**

- Uses a combination of hardware (MMU) and software (OS).
- Keeps only the most frequently used pages in RAM; others are stored on disk.
- Uses a **page table** to keep track of where each page is.

---

## Demand Paging

- **Demand paging** is a memory management technique used by operating systems to load pages into memory only when they are needed, instead of loading the entire program at once.
- At the start, only a small part of the program (the pages that are immediately needed) are loaded into RAM.
- When a program tries to access a part of memory (a page) that is not currently in RAM, a **page fault** occurs.
- The operating system then pauses the program, finds the required page on the disk, loads it into RAM, and then lets the program continue.
- This process allows the system to run programs that are larger than the available physical memory, because only the necessary parts are kept in memory at any time.
- Demand paging helps to use memory more efficiently and allows more programs to run at the same time.

**How Demand Paging Works:**

1. When a program starts, only some of its pages are loaded into memory.
2. If the program tries to use a page that is not in memory, the hardware detects this and sends a signal to the operating system (a page fault).
3. The operating system finds the required page on the disk, loads it into a free frame in memory, and updates the page table.
4. The program continues running as if the page had always been in memory.

**Advantages:**

- Saves memory by only loading needed pages.
- Allows running large programs on small memory systems.
- Increases the number of programs that can run at the same time (multiprogramming).

**Disadvantages:**

- If page faults happen too often, the system can slow down (this is called thrashing).
- Accessing a page from disk is much slower than accessing it from RAM.

---

## Performance of Demand Paging

- **Page Fault Rate:** The percentage of memory accesses that cause a page fault. Lower is better.
- **Effective Access Time (EAT):**
  - EAT = (1 - p) × memory access time + p × page fault service time
  - Where p = page fault rate.
- **Thrashing:** If too many page faults occur, the system spends more time swapping pages than running programs. This slows down the system.
- **Optimizations:**
  - Use good page replacement algorithms (LRU, FIFO, Optimal).
  - Increase physical memory.
  - Reduce the number of running processes.

---

## 15. Define graceful degradation. [Q15]

**Question 15: Define graceful degradation?**

- **Graceful degradation** means that a system continues to operate, but with reduced performance or functionality, when part of it fails or is under heavy load.
- In operating systems, this means the system slows down or limits features instead of crashing completely when resources are low or errors occur.
- Example: If memory is low, the OS may slow down but still allow basic tasks to continue.

---

# Page Replacement Algorithms, Thrashing, Cache Memory, and Locality of Reference

## 9. Storage Placement Strategies: Best Fit, First Fit, Worst Fit [Q9]

**Question 9: Discuss the following storage placement strategies with suitable examples: (i) Best fit (ii) First fit (iii) Worst fit**

### 1. First Fit

- Allocates the first block of memory that is large enough for the process.
- **Advantage:** Fast and simple.
- **Disadvantage:** Can leave small unusable holes (fragmentation).
- **Example:**
  - Memory blocks: 100 KB, 500 KB, 200 KB, 300 KB, 600 KB
  - Process size: 212 KB
  - Allocated to 500 KB (first block large enough)

### 2. Best Fit

- Allocates the smallest block that is large enough for the process.
- **Advantage:** Reduces wasted space (internal fragmentation).
- **Disadvantage:** Can create many small holes (external fragmentation).
- **Example:**
  - Memory blocks: 100 KB, 500 KB, 200 KB, 300 KB, 600 KB
  - Process size: 212 KB
  - Allocated to 300 KB (smallest block that fits)

### 3. Worst Fit

- Allocates the largest available block to the process.
- **Advantage:** Leaves the largest possible remaining hole.
- **Disadvantage:** May waste large memory blocks.
- **Example:**
  - Memory blocks: 100 KB, 500 KB, 200 KB, 300 KB, 600 KB
  - Process size: 212 KB
  - Allocated to 600 KB (largest block)

---

## 10. Page Replacement Algorithms [Q10]

**Question 10: Illustrate the following page-replacement algorithms.**

- i) FIFO
- ii) LRU
- Use the reference string 7, 0, 1, 2, 0, 3, 0, 4, 2, 3, 0, 3, 2, 1, 2, 0, 1, 7, 0, 1 for a memory with four frames

### i) FIFO (First-In, First-Out)

- The oldest page in memory is replaced first.
- **How it works:** Pages are loaded in order. When a new page is needed and memory is full, the page that has been in memory the longest is removed.

**Example Table:**
| Step | Reference | Frames (after step) | Page Fault? |
|------|-----------|---------------------|-------------|
| 1 | 7 | 7 \_ \_ _ | Yes |
| 2 | 0 | 7 0 _ _ | Yes |
| 3 | 1 | 7 0 1 _ | Yes |
| 4 | 2 | 7 0 1 2 | Yes |
| 5 | 0 | 7 0 1 2 | No |
| 6 | 3 | 0 1 2 3 | Yes |
| 7 | 0 | 1 2 3 0 | Yes |
| 8 | 4 | 2 3 0 4 | Yes |
| 9 | 2 | 3 0 4 2 | Yes |
| 10 | 3 | 0 4 2 3 | Yes |
| 11 | 0 | 4 2 3 0 | Yes |
| 12 | 3 | 2 3 0 4 | Yes |
| 13 | 2 | 3 0 4 2 | Yes |
| 14 | 1 | 0 4 2 1 | Yes |
| 15 | 2 | 4 2 1 0 | Yes |
| 16 | 0 | 2 1 0 4 | Yes |
| 17 | 1 | 1 0 4 2 | Yes |
| 18 | 7 | 0 4 2 7 | Yes |
| 19 | 0 | 4 2 7 0 | Yes |
| 20 | 1 | 2 7 0 1 | Yes |

- **Total Page Faults (FIFO):** 15 (count the 'Yes' entries)

### ii) LRU (Least Recently Used)

- The page that has not been used for the longest time is replaced first.
- **How it works:** When a page must be replaced, the OS removes the page that was least recently accessed.

**Example Table:**
| Step | Reference | Frames (after step) | Page Fault? |
|------|-----------|---------------------|-------------|
| 1 | 7 | 7 \_ \_ _ | Yes |
| 2 | 0 | 7 0 _ _ | Yes |
| 3 | 1 | 7 0 1 _ | Yes |
| 4 | 2 | 7 0 1 2 | Yes |
| 5 | 0 | 7 0 1 2 | No |
| 6 | 3 | 0 1 2 3 | Yes |
| 7 | 0 | 1 2 3 0 | Yes |
| 8 | 4 | 2 3 0 4 | Yes |
| 9 | 2 | 3 0 4 2 | Yes |
| 10 | 3 | 0 4 2 3 | Yes |
| 11 | 0 | 4 2 3 0 | Yes |
| 12 | 3 | 2 3 0 4 | Yes |
| 13 | 2 | 3 0 4 2 | Yes |
| 14 | 1 | 0 4 2 1 | Yes |
| 15 | 2 | 4 2 1 0 | Yes |
| 16 | 0 | 2 1 0 4 | Yes |
| 17 | 1 | 1 0 4 2 | Yes |
| 18 | 7 | 0 4 2 7 | Yes |
| 19 | 0 | 4 2 7 0 | Yes |
| 20 | 1 | 2 7 0 1 | Yes |

- **Total Page Faults (LRU):** 15 (count the 'Yes' entries)

---

## Thrashing

- **Thrashing** occurs when a system spends more time swapping pages in and out of memory than executing actual processes.
- It happens when there is not enough physical memory and too many page faults occur.
- **Symptoms:**
  - High CPU usage but low process progress.
  - Constant disk activity.
- **How to avoid thrashing:**
  - Reduce the number of running processes.
  - Increase physical memory.
  - Use better page replacement algorithms.
  - Use working set model to keep only needed pages in memory.

---

## Cache Memory Organization

- **Cache memory** is a small, fast memory located between the CPU and main memory.
- It stores frequently accessed data and instructions to speed up processing.
- **Levels:** L1 (fastest, smallest), L2, L3 (larger, slower).
- **Organization:**
  - **Direct-mapped cache:** Each block of main memory maps to exactly one cache line, determined by the address. Simple and fast, but can lead to frequent conflicts if multiple blocks compete for the same line.
  - **Fully associative cache:** Any block from main memory can be loaded into any cache line. This provides maximum flexibility and minimizes conflicts, but requires complex hardware to search all lines for a match.
  - **Set-associative cache:** Memory blocks are divided into sets, and each set contains multiple lines (e.g., 2-way, 4-way). A block maps to a specific set, but can be placed in any line within that set. This balances speed and flexibility, reducing conflicts compared to direct-mapped caches while being simpler than fully associative caches.
- **Cache hit:** Data is found in cache (fast access).
- **Cache miss:** Data is not in cache (must fetch from main memory).

| Cache Type        | Mapping Method | Speed   | Cost   |
| ----------------- | -------------- | ------- | ------ |
| Direct-mapped     | One-to-one     | Fast    | Low    |
| Fully associative | Any-to-any     | Fastest | High   |
| Set-associative   | Group-to-group | Medium  | Medium |

---

## Locality of Reference

- **Locality of reference** is the tendency of a program to access the same set of memory locations repeatedly over a short period.
- **Types:**
  - **Temporal locality:** Recently accessed memory is likely to be accessed again soon.
  - **Spatial locality:** Memory locations near recently accessed addresses are likely to be accessed soon.
- **Importance:**
  - Used in designing cache and virtual memory systems.
  - Improves performance by keeping frequently used data close to the CPU.

---

## 11. Calculate the number of page faults (Optimal Page Replacement)

**Reference string:** 2, 3, 4, 3, 4, 1, 6, 7, 8, 7, 1, 8, 9, 8, 9, 5, 4, 2, 1
**Frames:** Not specified (commonly 3, but if not given, let's assume 3)

**Step-by-step (Optimal):**

- 2: [2] (fault)
- 3: [2,3] (fault)
- 4: [2,3,4] (fault)
- 3: [2,3,4] (hit)
- 4: [2,3,4] (hit)
- 1: [1,3,4] (fault, 2 replaced)
- 6: [1,4,6] (fault, 3 replaced)
- 7: [1,6,7] (fault, 4 replaced)
- 8: [1,7,8] (fault, 6 replaced)
- 7: [1,7,8] (hit)
- 1: [1,7,8] (hit)
- 8: [1,7,8] (hit)
- 9: [7,8,9] (fault, 1 replaced)
- 8: [7,8,9] (hit)
- 9: [7,8,9] (hit)
- 5: [8,9,5] (fault, 7 replaced)
- 4: [9,5,4] (fault, 8 replaced)
- 2: [5,4,2] (fault, 9 replaced)
- 1: [4,2,1] (fault, 5 replaced)

**Total page faults (Optimal, 3 frames):** 12

---

## 12. Page Faults for LRU and OPTIMAL (3 frames)

**Reference string:** 1, 2, 3, 4, 2, 4, 5, 6, 3, 1, 2, 3, 4, 6, 4, 5, 2, 6

### LRU:

- 1: [1] (fault)
- 2: [1,2] (fault)
- 3: [1,2,3] (fault)
- 4: [2,3,4] (fault, 1 out)
- 2: [3,4,2] (fault, 1 out)
- 4: [3,2,4] (hit)
- 5: [2,4,5] (fault, 3 out)
- 6: [4,5,6] (fault, 2 out)
- 3: [5,6,3] (fault, 4 out)
- 1: [6,3,1] (fault, 5 out)
- 2: [3,1,2] (fault, 6 out)
- 3: [1,2,3] (fault, 6 out)
- 4: [2,3,4] (fault, 1 out)
- 6: [3,4,6] (fault, 2 out)
- 4: [3,6,4] (hit)
- 5: [6,4,5] (fault, 3 out)
- 2: [4,5,2] (fault, 6 out)
- 6: [5,2,6] (fault, 4 out)

**Total page faults (LRU, 3 frames):** 16

### OPTIMAL:

- 1: [1] (fault)
- 2: [1,2] (fault)
- 3: [1,2,3] (fault)
- 4: [2,3,4] (fault, 1 out)
- 2: [3,4,2] (hit)
- 4: [3,4,2] (hit)
- 5: [4,2,5] (fault, 3 out)
- 6: [2,5,6] (fault, 4 out)
- 3: [5,6,3] (fault, 2 out)
- 1: [6,3,1] (fault, 5 out)
- 2: [3,1,2] (fault, 6 out)
- 3: [1,2,3] (fault, 6 out)
- 4: [2,3,4] (fault, 1 out)
- 6: [3,4,6] (fault, 2 out)
- 4: [3,4,6] (hit)
- 5: [4,6,5] (fault, 3 out)
- 2: [6,5,2] (fault, 4 out)
- 6: [5,2,6] (fault, 4 out)

**Total page faults (Optimal, 3 frames):** 14

---

## 16. Banker's Algorithm: Safe Sequence

**Question 16: Can the system execute the following processes without deadlock occurring, if yes find safe sequence?**

### Given:

- Resources: A=10, B=5, C=7
- Allocation and Maximum for each process:

| Process | Allocation (A B C) | Maximum (A B C) |
| ------- | ------------------ | --------------- |
| P1      | 0 1 0              | 7 5 3           |
| P2      | 2 0 0              | 3 2 2           |
| P3      | 3 0 2              | 9 0 2           |
| P4      | 2 1 1              | 2 2 2           |
| P5      | 0 0 2              | 4 3 3           |

- **Available:**

  - A: 10 - (0+2+3+2+0) = 3
  - B: 5 - (1+0+0+1+0) = 3
  - C: 7 - (0+0+2+1+2) = 2

- **Need = Maximum - Allocation**

| Process | Need (A B C) |
| ------- | ------------ |
| P1      | 7 4 3        |
| P2      | 1 2 2        |
| P3      | 6 0 0        |
| P4      | 0 1 1        |
| P5      | 4 3 1        |

**Safe Sequence Calculation:**

- Work = Available = [3,3,2]
- Find a process whose need <= work:
  - P2: Need [1,2,2] <= [3,3,2] → Yes. Work = Work + Allocation of P2 = [3+2,3+0,2+0] = [5,3,2]
  - P4: Need [0,1,1] <= [5,3,2] → Yes. Work = [5+2,3+1,2+1] = [7,4,3]
  - P1: Need [7,4,3] <= [7,4,3] → Yes. Work = [7+0,4+1,3+0] = [7,5,3]
  - P3: Need [6,0,0] <= [7,5,3] → Yes. Work = [7+3,5+0,3+2] = [10,5,5]
  - P5: Need [4,3,1] <= [10,5,5] → Yes. Work = [10+0,5+0,5+2] = [10,5,7]

**Safe Sequence:** P2 → P4 → P1 → P3 → P5

- **Yes, the system can execute all processes without deadlock.**

---

## 6. Page Table Size Calculation

**Question 6: Consider a machine with 64 MB physical memory and a 32-bit virtual address space. If the page size is 4KB, what is the approximate size of the page table?**

- **Virtual address space:** 32 bits → 2^32 bytes = 4 GB
- **Page size:** 4 KB = 2^12 bytes
- **Number of pages:** 2^32 / 2^12 = 2^20 = 1,048,576 pages
- **Assume each page table entry is 4 bytes**
- **Page table size:** 1,048,576 × 4 bytes = 4,194,304 bytes = 4 MB

**Approximate size of the page table: 4 MB**

---
1. Differentiate between paging and segmentation.
2. Define Paging and Segmentation
3. Define Paging scheme with an example in detail.

4. What is Virtual Memory? How is it implemented?
5. Consider a machine with 64 MB physical memory and a 32-bit virtual address space. If the page size is 4KB, what is the approximate size of the page table?
6. Consider a machine with 64 MB physical memory and a 32-bit virtual address space. If the page size is 4KB, what is the approximate size of the page table?
7. Explain the concept of segmentation with proper diagram.
8. Five memory partitions of 100, 500, 200, 300 & 600 (all in KB) are in order, how would the ‘first-fit, best-fit & worst-fit’ shall place processes of size 212, 417, 112, & 426 ((all in KB). Deduce the most efficient memory management technique
9. Discuss the following storage placement strategies with suitable examples : (i) Best fit (ii) First fit (iii) Worst fit
10. Illustrate the following page-replacement algorithms.
    i) FIFO
    ii) LRU
    Use the reference string 7, 0,1, 2, 0, 3, 0, 4, 2, 3, 0, 3, 2,1, 2, 0, 1, 7, 0,1 for a memory with four frames
11. Calculate the number of page faults that would occur in case of optimal page replacement algorithm for the following reference string? Assuming the demand paging technique is used by OS 2,3,4,3,4,1,6,7,8,7,1,8,9,8,9,5,4,2,1
12. Consider the following page reference string : 1 , 2 , 3 , 4 , 2 , 4 , 5 , 6 , 3 , 1 , 2 , 3 , 4 , 6 , 4 , 5 , 2 , 6. Calculate number of page faults using LRU and OPTIMAL Page replacement algorithm. Assume number of frames as three
13. Discuss Resource Allocation Graph (RAG)? Find how many cycles’ deadlocks reside in given figure.
14. what is a Resource allocation Graph
15. Define graceful degradation?
16. Suppose we have five processes and three resources, A, B, and C. A has 10 instances, B has 5 instances and C has 7 instances. Can the system execute the following processes without deadlock occurring, if yes find safe sequence? Process Allocation Maximum A B C A B C P1 0 1 0 7 5 3 P2 2 0 0 3 2 2 P3 3 0 2 9 0 2 P4 2 1 1 2 2 2 P5 0 0 2 4 3 3
