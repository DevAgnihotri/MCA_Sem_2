# I/O Devices, I/O Subsystems, Buffering, Disk Storage, Disk Scheduling, and RAID: Extra Detailed Notes

---
https://www.youtube.com/watch?v=dEt7mr9R_Z8&ab_channel=Lastmomenttuitions

## File System: Explained in Simple English

A **file system** is the way an operating system organizes and manages files and folders on a storage device (like a hard disk, SSD, or USB drive). It acts like a librarian, keeping track of where everything is stored, how to find it, and who can use it.

### What Does a File System Do?

- **Stores files and folders:** Keeps your documents, pictures, programs, and other data in an organized way.
- **Manages space:** Decides where to put new files and how to use free space efficiently.
- **Keeps track of locations:** Remembers where each file is physically stored on the disk.
- **Controls access:** Decides who can read, write, or delete each file.
- **Protects data:** Helps prevent data loss or corruption.

### Main Parts of a File System

1. **Files:** Collections of data (like text, images, or programs).
2. **Directories (Folders):** Containers that organize files and other folders.
3. **Metadata:** Information about each file (name, size, type, permissions, dates).
4. **Allocation Table:** A map showing which parts of the disk are used by which files (e.g., FAT, NTFS Master File Table).
5. **Free Space Management:** Keeps track of which parts of the disk are empty and available for new files.

### How Files are Organized

- **Hierarchical Structure:** Files are grouped into folders, and folders can contain more folders (like a tree).
- **Path Names:** Each file has a unique path (e.g., `C:\Users\John\Documents\file.txt`).

### How Data is Stored

- **Blocks:** The disk is divided into small pieces called blocks. Files are stored in one or more blocks.
- **Allocation Methods:** The file system decides how to assign blocks to files (contiguous, linked, indexed, etc.).

### Common File Systems

- **FAT (File Allocation Table):** Simple, used in USB drives and memory cards.
- **NTFS (New Technology File System):** Used in Windows, supports large files, security, and recovery.
- **ext4:** Used in Linux, fast and reliable.
- **APFS:** Used in macOS, optimized for SSDs.

### File System Operations

- **Create:** Make a new file or folder.
- **Read:** Open and view a file.
- **Write:** Save changes to a file.
- **Delete:** Remove a file or folder.
- **Rename:** Change the name of a file or folder.
- **Move/Copy:** Change the location or make a duplicate.

### File System Protection and Security

- **Permissions:** Decide who can read, write, or execute a file.
- **Access Control Lists (ACLs):** More detailed rules for file access.
- **Encryption:** Scrambles data to keep it safe from unauthorized users.

### Why File Systems Matter

- **Organization:** Makes it easy to find and manage files.
- **Efficiency:** Uses storage space wisely.
- **Reliability:** Protects data from loss or corruption.
- **Security:** Keeps files safe from unauthorized access.

In summary, a file system is like the brain of your storage device, making sure all your data is safe, organized, and easy to use.


## Detailed Discussion: Linked, Contiguous, Indexed, and Multi-level Indexing File Allocation Schemes

### 1. Contiguous Allocation

- **How it works:** Each file occupies a set of contiguous (neighboring) blocks on the disk. The directory stores the starting block and the length (number of blocks) for each file.
- **Advantages:**
  - Simple to implement.
  - Fast sequential and direct access (just calculate the block address).
- **Disadvantages:**
  - External fragmentation: Free space gets scattered, making it hard to find large enough contiguous blocks for new files.
  - Difficult to grow files: If a file needs to expand, there may not be enough space after its current blocks.
- **Use case:** Good for files with known, fixed sizes (e.g., system files, read-only media).

**Diagram:**  
```
|---File A---|---File B---|---Free---|---File C---|
```

### 2. Linked Allocation

- **How it works:** Each file is a linked list of disk blocks. Each block contains a pointer to the next block. The directory stores the address of the first block.
- **Advantages:**
  - No external fragmentation.
  - Easy to grow files (just add another block and update the pointer).
- **Disadvantages:**
  - Slow direct access: To read block N, must follow N pointers from the start.
  - Extra space needed for pointers in each block.
  - Reliability: If a pointer is lost or corrupted, the rest of the file is inaccessible.
- **Use case:** Suitable for sequential access files (e.g., log files).

**Diagram:**  
```
[Block1]→[Block2]→[Block3]→[Block4]→NULL
```

### 3. Indexed Allocation

- **How it works:** Each file has an index block that contains a list of pointers to all the file's disk blocks. The directory stores the address of the index block.
- **Advantages:**
  - Supports both sequential and direct access efficiently.
  - No external fragmentation.
  - Easy to grow files (add pointers to the index block).
- **Disadvantages:**
  - The index block can be large for big files (may need to limit file size or use multi-level indexing).
  - Slight overhead for storing and accessing the index block.
- **Use case:** Used in systems where both sequential and random access are needed.

**Diagram:**  
```
[Index Block] → [Block1], [Block2], [Block3], ...
```

### 4. Multi-level Indexing

- **How it works:** Uses multiple levels of index blocks (like a tree structure). The first-level index points to second-level index blocks, which then point to data blocks. This allows very large files to be managed efficiently.
- **Advantages:**
  - Can handle very large files (scalable).
  - Efficient direct access using multiple index levels.
- **Disadvantages:**
  - More complex to implement.
  - Slightly more overhead for accessing data (may require multiple reads to follow index pointers).
- **Use case:** Used in UNIX file systems (e.g., inode structure with direct, single, double, and triple indirect pointers).

**Diagram:**  
```
[Inode] → [Direct Blocks], [Single Indirect] → [Blocks], [Double Indirect] → [Index Blocks] → [Blocks], etc.
```

**Summary Table:**

| Method         | Pros                        | Cons                        | Best For                |
| -------------- | --------------------------- | --------------------------- | ----------------------- |
| Contiguous     | Fast, simple                | Fragmentation, hard to grow | Fixed-size files        |
| Linked         | Easy to grow, no frag.      | Slow direct access          | Sequential access files |
| Indexed        | Fast access, flexible       | Index block overhead        | Mixed access patterns   |
| Multi-level    | Handles very large files    | More complex                | Large file systems      |


## I/O Devices: What They Are and How They Work

### What are I/O Devices?

- **I/O (Input/Output) devices** are the parts of a computer system that let it talk to the outside world.
- They help the computer get information from users or other systems (input), and send information out (output).

#### Types of I/O Devices

| Type          | Examples                         | What They Do                  |
| ------------- | -------------------------------- | ----------------------------- |
| Input         | Keyboard, Mouse, Scanner, Camera | Let you give data to computer |
| Output        | Monitor, Printer, Speakers       | Show results to you           |
| Storage       | Hard disk, SSD, USB drive        | Save data for later           |
| Communication | Network card, Modem, Bluetooth   | Connect to other computers    |

#### How I/O Devices Connect

- **Ports:** Physical connectors (USB, HDMI, audio jack)
- **Wireless:** Bluetooth, Wi-Fi
- **Expansion Cards:** Plugged into motherboard (graphics card, network card)

#### How Data Moves

- **Character Devices:** Send or get one character at a time (like a keyboard or serial port).
- **Block Devices:** Send or get a block of data at once (like a hard disk or SSD).
- **Network Devices:** Move data over a network (like Wi-Fi cards or Ethernet adapters).

#### Device Communication Methods

- **Programmed I/O:** CPU is in charge of all data transfer. Simple but wastes CPU time.
- **Interrupt-Driven I/O:** Device interrupts CPU when ready. CPU can do other work while waiting.
- **Direct Memory Access (DMA):** Device sends/receives data directly to/from memory, freeing up CPU.

---

## I/O Subsystems: The OS Side of I/O

- The **I/O subsystem** is the part of the operating system (OS) that manages all I/O devices and operations.
- It acts as a bridge between programs and hardware, making it easy for programs to use any device without knowing its details.

#### Main Parts of the I/O Subsystem

1. **Device Drivers:** Special software for each device. Translates OS commands into device-specific actions.
2. **I/O Scheduler:** Decides the order in which I/O jobs are handled, especially when many requests come at once.
3. **Buffer Management:** Handles temporary storage (buffers) for data moving between devices and memory.
4. **Device Controllers:** Hardware that controls the device and communicates with the CPU.

#### How the I/O Subsystem Works (Step-by-Step)

1. A program asks the OS to read or write data.
2. The OS uses the device driver to talk to the hardware.
3. The device controller manages the actual data transfer.
4. Data may be stored in a buffer while moving between device and memory.
5. The OS tells the program when the job is done.

#### Why Use an I/O Subsystem?

- Hides hardware details from programs.
- Makes it easy to add new devices.
- Improves performance and reliability.

---

## I/O Buffering: Making Data Transfer Smoother [Q7a]

### Q7a: Write short notes on I/O buffering

- **I/O buffering** means using a special area in memory (called a buffer) to hold data while it moves between the computer and an I/O device.
- Buffering helps because the CPU is much faster than most I/O devices, so it can keep working while waiting for I/O.

#### Why Buffering is Important

- **Smooths out speed differences** between CPU and devices.
- **Prevents CPU from waiting** for slow devices.
- **Reduces the number of times the CPU is interrupted** by I/O.
- **Allows overlapping** of computation and I/O.

#### Types of Buffering

| Type            | How It Works                                   | When Used                |
| --------------- | ---------------------------------------------- | ------------------------ |
| Single Buffer   | One buffer; process waits for it to fill/empty | Simple jobs              |
| Double Buffer   | Two buffers; one fills, one empties            | Continuous data transfer |
| Circular Buffer | Several buffers in a loop                      | Real-time systems        |
| Buffer Pool     | Many buffers managed by OS                     | Complex I/O              |

#### How Buffering Works (Example)

- **Single Buffer:**
  - The program waits while the buffer is being filled or emptied.
  - Simple but can slow down the program.
- **Double Buffer:**
  - The program can use one buffer while the other is busy with I/O.
  - This means the program and device can work at the same time, making things faster.
- **Circular Buffer:**
  - Several buffers are used in a circle.
  - Good for real-time or streaming data (like audio or video).

#### Buffer Management Strategies

- **FIFO (First-In-First-Out):** Oldest buffer is used first.
- **LRU (Least Recently Used):** Buffer not used for the longest time is replaced.
- **Clock Algorithm:** Like LRU but uses a simple pointer and reference bits.

#### Benefits of Buffering

- Faster data transfer.
- Less waiting for CPU and devices.
- Better use of system resources.

---

## Disk Storage: How Data is Saved and Read [Q7b]

### Q7b: Write short notes on Disk storage & scheduling

#### What is Disk Storage?

- **Disk storage** means saving data on hard disks (HDDs) or solid-state drives (SSDs).
- Most computers use disks to store programs, files, and the operating system.

#### Hard Disk Drive (HDD) Structure

| Part            | What It Does               |
| --------------- | -------------------------- |
| Platter         | Disk where data is stored  |
| Track           | Circle on the platter      |
| Sector          | Piece of a track           |
| Cylinder        | Same track on all platters |
| Read/Write Head | Reads or writes data       |
| Actuator Arm    | Moves the head             |

#### How Data is Accessed

- **Seek Time:** Time to move the head to the right track.
- **Rotational Latency:** Time for the disk to spin to the right spot.
- **Transfer Time:** Time to actually move the data.
- **Controller Overhead:** Time for the controller to process the request.

**Total Access Time = Seek Time + Rotational Latency + Transfer Time + Controller Overhead**

#### Solid-State Drives (SSD)

- Use flash memory, no moving parts.
- Much faster than HDDs, but more expensive.

---

## Disk Scheduling: Making Disk Access Faster [Q7b]

- **Disk scheduling** is how the OS decides the order to handle read/write requests to make disk access faster and fairer.

#### Why is Disk Scheduling Needed?

- Disk heads move slowly compared to CPU.
- Many requests can come at once; good scheduling reduces waiting time.

#### Common Disk Scheduling Algorithms

| Algorithm | How It Works                              | Good For           | Drawbacks                    |
| --------- | ----------------------------------------- | ------------------ | ---------------------------- |
| FCFS      | First request, first served               | Simple, fair       | Can be slow                  |
| SSTF      | Closest request next                      | Faster, may starve | Some requests wait too long  |
| SCAN      | Head moves back and forth                 | Good performance   | Ends get less service        |
| C-SCAN    | Like SCAN, but only one direction         | Uniform wait       | Head returns without serving |
| LOOK      | Like SCAN, but only goes as far as needed | Efficient          | More complex                 |
| C-LOOK    | Like LOOK, but in one direction           | Best performance   | Most complex                 |

#### Example: SCAN Algorithm

- Requests: 98, 183, 37, 122, 14, 124, 65, 67
- Current head position: 53
- Head moves right: 65, 67, 98, 122, 124, 183, then back to 37, 14
- Total head movement is less than FCFS

#### Benefits of Disk Scheduling

- Faster disk access
- Less waiting for programs
- Better use of disk

---

## File Directory: Organizing Files [Q7c]

### Q7c: Write short notes on File Directory

- A **file directory** is a special file or data structure that keeps track of all files and folders on a disk.
- It helps the OS find, organize, and protect files.

#### What Does a Directory Do?

- Organizes files in folders and subfolders.
- Stores info like file name, size, location, and permissions.
- Controls who can use each file (read, write, execute).
- Keeps track of when files were created or changed.

#### Types of Directory Structures

| Type          | Description                           | Pros                | Cons                  |
| ------------- | ------------------------------------- | ------------------- | --------------------- |
| Single-Level  | All files in one place                | Simple              | Name conflicts, messy |
| Two-Level     | Each user has their own directory     | Better organization | Limited hierarchy     |
| Tree          | Folders inside folders (like Windows) | Flexible, organized | More complex          |
| Acyclic Graph | Folders can be shared                 | Sharing possible    | Harder to manage      |
| General Graph | Folders can link to each other        | Maximum flexibility | Can cause loops       |

#### What Info is in a Directory Entry?

- File name
- File type (text, image, etc.)
- File size
- Where the file is on disk
- Who owns the file
- Permissions (who can read/write)
- Dates (created, modified)

#### Path Names

- **Absolute Path:** Full path from the root (e.g., `/home/user/file.txt`)
- **Relative Path:** Path from current directory (e.g., `docs/file.txt`)

---

## RAID: Using Many Disks for Speed and Safety [Q7d]

### Q7d: Write short notes on RAID

- **RAID** stands for Redundant Array of Independent Disks.
- It means using several disks together to make storage faster, safer, or both.
- If one disk fails, RAID can keep your data safe (depending on the type).

#### Why Use RAID?

- Faster data access (using many disks at once)
- Protects data if a disk fails (redundancy)
- Can combine both speed and safety

#### Detailed RAID Levels

- **RAID 0 (Striping):** Data is split evenly across two or more disks. This gives very fast read and write speeds and uses all available disk space, but there is no fault tolerance—if one disk fails, all data is lost.
- **RAID 1 (Mirroring):** Data is copied identically to two or more disks. This provides high data safety and easy recovery, but only half of the total disk space is usable and write speeds are not improved.
- **RAID 2:** Uses bit-level striping with Hamming code for error correction. It offers error correction and theoretical speed, but is complex, needs many disks, and is rarely used in practice.
- **RAID 3:** Uses byte-level striping with a dedicated parity disk. Good for large sequential data transfers, but the single parity disk can become a bottleneck.
- **RAID 4:** Uses block-level striping with a dedicated parity disk. Suitable for read-heavy workloads, but the parity disk can slow down writes.
- **RAID 5:** Uses block-level striping with distributed parity (no single parity disk). It offers fast reads, fault tolerance, and efficient storage use, but writes are slower due to parity calculations and it needs at least three disks.
- **RAID 6:** Similar to RAID 5 but with two sets of parity for extra fault tolerance. It can survive two disk failures, but writes are even slower and it needs at least four disks.
- **RAID 10 (1+0):** Combines mirroring and striping (mirror first, then stripe). This provides very fast speeds and high fault tolerance, but uses half the total disk space and needs at least four disks.
- **RAID 01 (0+1):** Combines striping and mirroring (stripe first, then mirror). It is fast and offers some redundancy, but is less fault tolerant than RAID 10 and also needs at least four disks.
- **Nested/Hybrid RAID:** Other combinations like RAID 50 or RAID 60 are used for special needs, offering customizable speed and safety but with more complexity and more disks required.

| Level  | How It Works                         | Good For                | Drawbacks                          |
| ------ | ------------------------------------ | ----------------------- | ---------------------------------- |
| RAID 0 | Splits data across disks (striping)  | Speed, no safety        | If one disk fails, all data lost   |
| RAID 1 | Copies data to two disks (mirroring) | Safety, not much speed  | Uses double space                  |
| RAID 5 | Splits data and adds parity info     | Speed + safety          | Slower writes, needs 3+ disks      |
| RAID 6 | Like RAID 5, but more safety         | Survive 2 disk failures | Even slower writes, needs 4+ disks |

#### How RAID Works (Simple Examples)

- **RAID 0:** Data is split into pieces and saved on different disks. Very fast, but no backup.
- **RAID 1:** Data is copied to two disks. If one fails, the other still has all the data.
- **RAID 5:** Data and special "parity" info are spread across all disks. If one disk fails, data can be rebuilt.
- **RAID 6:** Like RAID 5, but can survive two disks failing at once.

#### How RAID is Set Up

- **Hardware RAID:** Uses a special card in the computer. Fast and reliable, but costs more.
- **Software RAID:** The operating system manages the disks. Cheaper, but uses more CPU.

#### RAID in Real Life

- Used in servers, data centers, and high-end PCs.
- Helps keep data safe and systems running even if a disk breaks.

---

## Summary Table

| Topic           | What It Means               | Why It Matters          |
| --------------- | --------------------------- | ----------------------- |
| I/O Buffering   | Temporary memory for I/O    | Smoother, faster I/O    |
| Disk Storage    | Where data is saved         | Stores all your files   |
| Disk Scheduling | Order of disk requests      | Faster disk access      |
| File Directory  | List of files/folders       | Find and organize files |
| RAID            | Many disks working together | Speed and/or safety     |

---

# File System: Concepts, Organization, Allocation, Protection, and Security

---

## File Concept

- A **file** is a collection of related data stored on secondary storage (like a hard disk).
- Files can contain text, images, programs, or any other type of data.
- The operating system manages files using a file system.

### File Attributes

| Attribute  | Description                         |
| ---------- | ----------------------------------- |
| Name       | Human-readable identifier           |
| Type       | Format (e.g., .txt, .jpg, .exe)     |
| Location   | Where the file is stored on disk    |
| Size       | Number of bytes in the file         |
| Protection | Who can access the file             |
| Timestamps | Creation, modification, access time |

---

## File Organization and Access Mechanism

- **File organization** refers to how data is arranged within a file.
- **Access mechanism** is how data is read from or written to a file.

### Types of File Organization

| Type          | Description                          | Example Use Case       |
| ------------- | ------------------------------------ | ---------------------- |
| Sequential    | Data is stored and accessed in order | Log files, tapes       |
| Direct/Random | Data can be accessed at any position | Databases, index files |
| Indexed       | Uses an index to quickly find data   | Large databases        |

### File Access Methods

- **Sequential Access:** Read/write data in order, one after another.
- **Direct Access:** Jump to any part of the file and read/write.
- **Indexed Access:** Use an index to find and access data quickly.

---

## File Directories and File Sharing [Q1]

### Q1. What do you mean by file directories? Explain.

- A **file directory** is a special file or data structure that keeps track of all files and folders on a disk.
- It stores information like file names, locations, sizes, and permissions.
- Directories help organize files, control access, and make it easy to find and manage files.

#### Directory Structures

| Structure       | Description                           |
| --------------- | ------------------------------------- |
| Single-level    | All files in one directory            |
| Two-level       | Each user has their own directory     |
| Tree-structured | Folders inside folders (hierarchical) |
| Acyclic Graph   | Allows shared subdirectories          |

#### File Sharing

- Multiple users or programs can access the same file.
- File sharing is managed by permissions and locks to prevent conflicts.

---

## File Allocation Methods

### Q2. Define link file allocation method.

- **Linked file allocation** stores each file as a linked list of disk blocks.
- Each block contains a pointer to the next block.
- Only the starting block address is stored in the directory.
- Good for sequential access, but slow for direct access.

### Q3,4,5. Discuss in detail the ‘Linked, Contiguous, Index & Multi-level Indexing’ file allocation schemes.

#### Contiguous Allocation

- Each file occupies a set of contiguous (neighboring) blocks on disk.
- Simple and fast for direct access.
- Can cause external fragmentation (free space scattered).

#### Linked Allocation

- Each file is a linked list of disk blocks.
- No external fragmentation, but slow for direct access.

#### Indexed Allocation

- Each file has an index block containing pointers to all its disk blocks.
- Supports both sequential and direct access.
- No external fragmentation, but index block can be large.

#### Multi-level Indexing

- Uses multiple levels of index blocks (like a tree).
- Handles very large files efficiently.
- Used in UNIX file systems (inode structure).

| Method      | Pros                        | Cons                        |
| ----------- | --------------------------- | --------------------------- |
| Contiguous  | Fast, simple                | Fragmentation, hard to grow |
| Linked      | No fragmentation, easy grow | Slow direct access          |
| Indexed     | Fast access, flexible       | Index block overhead        |
| Multi-level | Handles big files           | More complex                |


## File System Implementation Issues

- **Free Space Management:** How to keep track of free disk blocks (bitmaps, free lists).
- **Directory Implementation:** How directories are stored and searched (linear list, hash table, B-tree).
- **Allocation Table:** Table (like FAT) to map files to disk blocks.
- **Performance:** Balancing speed, space, and reliability.
- **Crash Recovery:** Making sure files are not lost or corrupted after a crash.

---

## File System Protection and Security

- **Protection** means controlling who can access or change files.
- **Security** means protecting files from unauthorized access, modification, or deletion.

### Protection Mechanisms

| Mechanism                 | Description                                  |
| ------------------------- | -------------------------------------------- |
| Permissions               | Read, write, execute rights for users/groups |
| Access Control List (ACL) | List of who can access each file             |
| Passwords                 | Files can be password-protected              |

### Security Measures

- **Encryption:** Scrambles file data so only authorized users can read it.
- **Backups:** Copies of files to restore if lost or damaged.
- **Audit Logs:** Records of who accessed or changed files.

---

# Answers to Additional Questions

## Q6. Disk Scheduling and Storage

### Q6. A hard disk has 2000 cylinders, numbered from 0 to 1999. The drive is currently serving the request at cylinder 143, and the previous request was at cylinder 125. The status of the queue is as follows: 86, 1470, 913, 1774, 948, 1509, 1022, 1750, 130.

What is the total distance (in cylinders) that the disk arm moves to satisfy the entire pending request for each of the following disk scheduling algorithms?  
a. SSTF  
b. FCFS

#### a. FCFS (First-Come-First-Served)

- Order: 86, 1470, 913, 1774, 948, 1509, 1022, 1750, 130
- Start at 143
- Calculate total movement by summing absolute differences:
  - 143 → 86 = 57
  - 86 → 1470 = 1384
  - 1470 → 913 = 557
  - 913 → 1774 = 861
  - 1774 → 948 = 826
  - 948 → 1509 = 561
  - 1509 → 1022 = 487
  - 1022 → 1750 = 728
  - 1750 → 130 = 1620
- **Total = 57 + 1384 + 557 + 861 + 826 + 561 + 487 + 728 + 1620 = 7081 cylinders**

#### b. SSTF (Shortest Seek Time First)

- Always go to the closest request next.
- Start at 143. Queue: 86, 1470, 913, 1774, 948, 1509, 1022, 1750, 130
- Step-by-step:
  - 143 → 130 = 13
  - 130 → 86 = 44
  - 86 → 913 = 827
  - 913 → 948 = 35
  - 948 → 1022 = 74
  - 1022 → 1470 = 448
  - 1470 → 1509 = 39
  - 1509 → 1750 = 241
  - 1750 → 1774 = 24
- **Total = 13 + 44 + 827 + 35 + 74 + 448 + 39 + 241 + 24 = 1745 cylinders**

---

## Q8. Define Belady’s Anomaly.

- **Belady’s Anomaly** is a situation in some page replacement algorithms (like FIFO) where increasing the number of page frames results in more page faults, not fewer.
- This is unexpected, as more memory should usually mean fewer faults.

---

## Q9. Explain logical address space and physical address space diagrammatically.

- **Logical address space** is the set of addresses generated by a program (used by the CPU).
- **Physical address space** is the set of actual addresses in main memory (RAM).

**Diagram:**

```
Program (CPU) → Logical Address → Memory Management Unit (MMU) → Physical Address (RAM)
```

- The MMU translates logical addresses to physical addresses.

---

## Q10. Page Replacement Algorithms: FIFO, LRU, Optimal

### Q10. A system uses 3-page frames for storing process pages in main memory. Assume that all the page frames are initially empty. What is the total number of page faults that will occur while processing the page reference string given below for FIFO, LRU and Optimal Page Replacement algorithm? Also calculate the hit ratio and miss ratio.

Page reference string: 4, 7, 6, 1, 7, 6, 1, 2, 7, 2, 5

#### FIFO (First-In-First-Out)

- Pages in memory: [4, 7, 6] → 1 (replace 4), 7 (hit), 6 (hit), 1 (hit), 2 (replace 7), 7 (replace 6), 2 (hit), 5 (replace 1)
- **Page faults:** 4, 7, 6, 1, 2, 7, 5 = 7
- **Hits:** 6, 1, 2 = 3
- **Total references:** 11
- **Hit ratio:** 3/11 ≈ 0.27
- **Miss ratio:** 8/11 ≈ 0.73

#### LRU (Least Recently Used)

- Pages in memory: [4, 7, 6] → 1 (replace 4), 7 (hit), 6 (hit), 1 (hit), 2 (replace 7), 7 (replace 6), 2 (hit), 5 (replace 1)
- **Page faults:** 4, 7, 6, 1, 2, 7, 5 = 7
- **Hits:** 6, 1, 2 = 3
- **Total references:** 11
- **Hit ratio:** 3/11 ≈ 0.27
- **Miss ratio:** 8/11 ≈ 0.73

#### Optimal

- Replace the page that will not be used for the longest time in the future.
- **Page faults:** 4, 7, 6, 1, 2, 5 = 6
- **Hits:** 7, 6, 1, 2, 7 = 5
- **Hit ratio:** 5/11 ≈ 0.45
- **Miss ratio:** 6/11 ≈ 0.55

---
