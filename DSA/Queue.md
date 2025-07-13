# PYQs on Queue (with Answers)

Below are important previous year questions (PYQs) on the Queue topic. Detailed answers are provided in the relevant sections below.

1. **Define the types of queues.**  
   See: [Types of Queues](#types-of-queues)

2. **What is Queue? Explain Priority Queue. Write uses of Queue.**  
   See: [Queue in C](#queue-in-c)

3. **Write an algorithm for insertion and deletion of elements of a queue. Use a Boolean variable to distinguish between a queue being empty or full.**  
   See: [Basic Operations on Queue (with Code)](#basic-operations-on-queue-with-code)

4. **Consider the following linear queue capable of accommodating maximum five elements.**  
   Front = 2, Rear = 4, Queue = [_, L, M, N, _]  
   Compute the following operations: (i) Add O (ii) Add P (iii) Delete two letters (iv) Add Q, R  
   See: [Example: Queue Operations (PYQ 4b)](#example-queue-operations-pyq-4b)

5. **WAP to insert an element in already existing queue**  
   See: [Inserting into an Existing Queue (PYQ 5)](#inserting-into-an-existing-queue-pyq-5)

6. **Define Queue also write the algorithm for insertion and deletion of element in a Queue.**  
   See: [Queue in C](#queue-in-c)

7. **Why circular queues are better than simple queue? Write an algorithm to insert and delete an item from the circular queue.**  
   See: [Circular Queue in C](#circular-queue-in-c)

---

# Queue in C

A **queue** is a linear data structure that follows the First In First Out (FIFO) principle. This means the first element added to the queue will be the first one to be removed.

  **PYQ 2 & 6:**
 
  **What is Queue? Explain Priority Queue. Write uses of Queue.**
 
  **Define Queue also write the algorithm for insertion and deletion of element in a Queue.**
 
  A **queue** is a linear data structure that follows FIFO (First In First Out) principle. Elements are inserted at the rear and removed from the front. A **priority queue** is a special type of queue in which each element is associated with a priority, and elements with higher priority are served before those with lower priority. If two elements have the same priority, they are served according to their order in the queue.
 
  **Uses of Queue:**
 
  - Job scheduling in operating systems
  - Print spooling
  - Data buffering (e.g., IO Buffers, keyboard buffers)
  - Breadth-First Search in graphs
  - Task scheduling
  - Bandwidth management
**Algorithm for Insertion (Enqueue):**

1. Check if the queue is full. If yes, report overflow.
2. If the queue is empty, set `front = 0` and `rear = 0`.
3. Else, increment `rear` by 1.
4. Insert the new element at `queue[rear]`.

```c

// Enqueue operation
void enqueue(int value) {
    if (rear == MAX - 1) {
        printf("Queue Overflow\n");
        return;
    }
    if (front == -1) {
        front = rear = 0;
    } else {
        rear++;
    }
    queue[rear] = value;
}

```

**Algorithm for Deletion (Dequeue):**

1. Check if the queue is empty. If yes, report underflow.
2. Remove the element at `queue[front]`.
3. If `front == rear`, set `front = rear = -1` (queue becomes empty).
4. Else, increment `front` by 1.

```c
// Dequeue operation
int dequeue() {
    if (front == -1) {
        printf("Queue Underflow\n");
        return -1;
    }
    int value = queue[front];
    if (front == rear) {
        front = rear = -1;
    } else {
        front++;
    }
    return value;
}
```

  **PYQ 1:**
 
  **Define the types of queues.**

### Types of Queues

1. **Simple Queue (Linear Queue):**  
    - Follows the First In First Out (FIFO) principle.  
    - Elements are inserted at the rear and removed from the front.  
    - Once the rear reaches the end of the array, no more elements can be added even if there is space at the front (due to deletions).  
    - Simple to implement but can lead to inefficient use of space.

2. **Circular Queue:**  
    - The last position is connected back to the first position, forming a circle.  
    - Allows efficient utilization of storage by reusing vacated spaces after deletions.  
    - Both `front` and `rear` wrap around to the beginning of the array when they reach the end.  
    - Prevents the problem of unused space in a simple queue.

3. **Priority Queue:**  
    - Each element is assigned a priority.  
    - Elements with higher priority are served before those with lower priority.  
    - If two elements have the same priority, they are served according to their order in the queue.  
    - Used in applications like task scheduling and bandwidth management.

4. **Double-Ended Queue (Deque):**  
    - Insertion and deletion can occur at both ends (front and rear).  
    - Supports all queue and stack operations.  
    - Useful in scenarios where elements need to be processed from both ends, such as undo operations or palindrome checking.  
    - Can be implemented using arrays or linked lists.

---

## Basic Operations on Queue (with Code)

  **PYQ 3(a):**
 
  **Write an algorithm for insertion and deletion of elements of a queue. Use a Boolean variable to distinguish between a queue being empty or full.**
 
  Let `isEmpty` and `isFull` be Boolean variables.
 
  **Algorithm for Insertion (Enqueue):**
 
  1. If `isFull` is true, report "Queue Overflow" and exit.
  2. If `isEmpty` is true, set `front = 0` and `rear = 0`.
  3. Else, increment `rear` by 1.
  4. Insert the new element at `queue[rear]`.
  5. If `rear == MAX-1`, set `isFull = true`.
  6. Set `isEmpty = false`.
 
  **Algorithm for Deletion (Dequeue):**
 
  1. If `isEmpty` is true, report "Queue Underflow" and exit.
  2. Remove the element at `queue[front]`.
  3. If `front == rear`, set `front = rear = -1`, `isEmpty = true`, `isFull = false`.
  4. Else, increment `front` by 1.
  5. If `front   rear`, set `isEmpty = true`.
  6. Set `isFull = false`.

Below is a simple queue implementation using an array in C, with comments explaining each operation:

```c
#include <stdio.h 
#define MAX 100

int queue[MAX];
int front = -1, rear = -1;

// Adds an element to the rear of the queue
void enqueue(int value) {
     if (rear == MAX - 1)
          printf("Queue Overflow\n");
     else {
          if (front == -1) front = 0; // First element
          queue[++rear] = value;
     }
}

// Removes and returns the front element from the queue
int dequeue() {
    ```c
        if (front == -1) {
            printf("Queue Underflow\n");
            return -1;
        } else
    ```
          return queue[front++];
}

// Returns the front element without removing it
int peek() {
     if (front == -1 || front > rear) {
          printf("Queue is Empty\n");
          return -1;
     } else
          return queue[front];
}

// Checks if the queue is empty
int isEmpty() {
     return (front == -1 || front > rear);
}

// Checks if the queue is full
int isFull() {
     return rear == MAX - 1;
}

// Displays all elements in the queue from front to rear
void display() {
     if (front == -1 || front   rear) {
          printf("Queue is Empty\n");
     } else {
          printf("Queue elements:\n");
          for (int i = front; i <= rear; i++)
                printf("%d\n", queue[i]);
     }
}

int main() {
    int choice, value;
    while (1) {
        printf("\n--- Queue Menu ---\n");
        printf("1. Enqueue\n2. Dequeue\n3. Peek\n4. Display\n5. Exit\n");
        printf("Enter your choice: ");
        scanf("%d", &choice);

        switch (choice) {
            case 1:
                printf("Enter value to enqueue: ");
                scanf("%d", &value);
                enqueue(value);
                break;
            case 2:
                value = dequeue();
                if (value != -1)
                    printf("Dequeued: %d\n", value);
                break;
            case 3:
                value = peek();
                if (value != -1)
                    printf("Front element: %d\n", value);
                break;
            case 4:
                display();
                break;
            case 5:
                return 0;
            default:
                printf("Invalid choice\n");
        }
    }
    return 0;
}
```

---

## Summary

- Queue is a FIFO data structure.
- Main operations: enqueue, dequeue, peek, isEmpty, isFull.
- Can be implemented using arrays or linked lists in C.
- Types include simple queue, circular queue, priority queue, and deque.
- Used in scheduling, buffering, and resource management.

## Circular Queue in C

A **circular queue** is a linear data structure that connects the last position back to the first position, forming a circle. This allows efficient utilization of storage by reusing vacated spaces, unlike a simple linear queue where space cannot be reused after deletion.

  **PYQ 7:**
 
  **Why circular queues are better than simple queue? Write an algorithm to insert and delete an item from the circular queue.**
 
  **Why Circular Queues are Better:**
 
  - In a simple queue, once the rear reaches the end of the array, no more elements can be added even if there is space at the front (due to deletions).
  - Circular queues connect the end of the array back to the front, allowing efficient use of all available space.
 
  **Algorithm for Insertion (Enqueue) in Circular Queue:**
 
  1. If (front == 0 && rear == MAX-1) or (rear + 1) % MAX == front, the queue is full (overflow).
  2. If the queue is empty (front == -1), set front = rear = 0.
  3. Else, set rear = (rear + 1) % MAX.
  4. Insert the new element at cqueue[rear].
 
  **Algorithm for Deletion (Dequeue) in Circular Queue:**
 
  1. If the queue is empty (front == -1), report underflow.
  2. Remove the element at cqueue[front].
  3. If front == rear, set front = rear = -1 (queue becomes empty).
  4. Else, set front = (front + 1) % MAX.

### Circular Queue Operations

Below is an implementation of a circular queue using arrays in C, including insertion (enqueue), deletion (dequeue), and display operations:

```c
#include <stdio.h> 
#define MAX 5

int cqueue[MAX];
int front = -1, rear = -1;

// Insert an element into the circular queue
void enqueue(int value) {
    if ((front == 0 && rear == MAX - 1) || (rear + 1) % MAX == front) {
        printf("Circular Queue Overflow\n");
        return;
    }
    if (front == -1) { // First element
        front = rear = 0;
    } else {
        rear = (rear + 1) % MAX;
    }
    cqueue[rear] = value;
}

// Delete an element from the circular queue
int dequeue() {
    if (front == -1) {
        printf("Circular Queue Underflow\n");
        return -1;
    }
    int value = cqueue[front];
    if (front == rear) { // Only one element
        front = rear = -1;
    } else {
        front = (front + 1) % MAX;
    }
    return value;
}

// Display elements of the circular queue
void display() {
    if (front == -1) {
        printf("Circular Queue is Empty\n");
        return;
    }
    printf("Circular Queue elements:\n");
    int i = front;
    while (1) {
        printf("%d\n", cqueue[i]);
        if (i == rear)
            break;
        i = (i + 1) % MAX;
    }
}

int main() {
    int choice, value;
    while (1) {
        printf("\n--- Circular Queue Menu ---\n");
        printf("1. Enqueue\n2. Dequeue\n3. Display\n4. Exit\n");
        printf("Enter your choice: ");
        scanf("%d", &choice);

        switch (choice) {
            case 1:
                printf("Enter value to enqueue: ");
                scanf("%d", &value);
                enqueue(value);
                break;
            case 2:
                value = dequeue();
                if (value != -1)
                    printf("Dequeued: %d\n", value);
                break;
            case 3:
                display();
                break;
            case 4:
                return 0;
            default:
                printf("Invalid choice\n");
        }
    }
    return 0;
}
```

**Key Points:**

- In a circular queue, both `front` and `rear` wrap around to the beginning of the array when they reach the end.
- Overflow occurs when the next position of `rear` is `front`.
- Underflow occurs when the queue is empty (`front == -1`).

## Double-Ended Queue (Deque) in C

A **double-ended queue (deque)** is a linear data structure that allows insertion and deletion of elements from both the front and the rear ends. This makes it more flexible than a simple queue or stack.

### Key Features

- Elements can be added or removed from both ends (front and rear).
- Supports all queue and stack operations.
- Useful in scenarios where elements need to be processed from both ends.

### Basic Operations

1. **Insert at Front**: Add an element at the front end.
2. **Insert at Rear**: Add an element at the rear end.
3. **Delete from Front**: Remove an element from the front end.
4. **Delete from Rear**: Remove an element from the rear end.
5. **Peek Front/Rear**: View the element at the front or rear.
6. **isEmpty / isFull**: Check if the deque is empty or full.

### Complete Deque Implementation in C (Using Array)

```c
#include <stdio.h> 
#define MAX 10

int deque[MAX];
int front = -1, rear = -1;

// Check if deque is full
int isFull() {
    return ((front == 0 && rear == MAX - 1) || (front == rear + 1));
}

// Check if deque is empty
int isEmpty() {
    return (front == -1);
}

// Insert at front
void insertFront(int value) {
    if (isFull()) {
        printf("Deque Overflow\n");
        return;
    }
    if (isEmpty()) {
        front = rear = 0;
    } else if (front == 0) {
        front = MAX - 1;
    } else {
        front--;
    }
    deque[front] = value;
}

// Insert at rear
void insertRear(int value) {
    if (isFull()) {
        printf("Deque Overflow\n");
        return;
    }
    if (isEmpty()) {
        front = rear = 0;
    } else if (rear == MAX - 1) {
        rear = 0;
    } else {
        rear++;
    }
    deque[rear] = value;
}

// Delete from front
int deleteFront() {
    if (isEmpty()) {
        printf("Deque Underflow\n");
        return -1;
    }
    int value = deque[front];
    if (front == rear) {
        front = rear = -1;
    } else if (front == MAX - 1) {
        front = 0;
    } else {
        front++;
    }
    return value;
}

// Delete from rear
int deleteRear() {
    if (isEmpty()) {
        printf("Deque Underflow\n");
        return -1;
    }
    int value = deque[rear];
    if (front == rear) {
        front = rear = -1;
    } else if (rear == 0) {
        rear = MAX - 1;
    } else {
        rear--;
    }
    return value;
}

// Display deque
void display() {
    if (isEmpty()) {
        printf("Deque is Empty\n");
        return;
    }
    printf("Deque elements:\n");
    int i = front;
    while (1) {
        printf("%d\n", deque[i]);
        if (i == rear)
            break;
        i = (i + 1) % MAX;
    }
}

int main() {
    int choice, value;
    while (1) {
        printf("\n--- Deque Menu ---\n");
        printf("1. Insert Front\n2. Insert Rear\n3. Delete Front\n4. Delete Rear\n5. Display\n6. Exit\n");
        printf("Enter your choice: ");
        scanf("%d", &choice);

        switch (choice) {
            case 1:
                printf("Enter value to insert at front: ");
                scanf("%d", &value);
                insertFront(value);
                break;
            case 2:
                printf("Enter value to insert at rear: ");
                scanf("%d", &value);
                insertRear(value);
                break;
            case 3:
                value = deleteFront();
                if (value != -1)
                    printf("Deleted from front: %d\n", value);
                break;
            case 4:
                value = deleteRear();
                if (value != -1)
                    printf("Deleted from rear: %d\n", value);
                break;
            case 5:
                display();
                break;
            case 6:
                return 0;
            default:
                printf("Invalid choice\n");
        }
    }
    return 0;
}
```

**Summary:**

- Deque allows insertion and deletion from both ends.
- Can be implemented using arrays or linked lists.
- Useful in various applications like palindrome checking, undo operations, and scheduling.

## Priority Queue in C

A **priority queue** is a special type of queue in which each element is associated with a priority, and elements are served according to their priority (not just their insertion order). Higher priority elements are dequeued before lower priority ones. If two elements have the same priority, they are served according to their order in the queue.

  **PYQ 2 (Priority Queue):**
 
  **Explain Priority Queue.**
 
  A priority queue is a queue in which each element is assigned a priority, and elements with higher priority are served before those with lower priority. If two elements have the same priority, they are served according to their order in the queue.

### Applications

- Task scheduling in operating systems
- Dijkstra’s shortest path algorithm
- Bandwidth management

### Priority Queue Operations

Below is a simple implementation of a priority queue using arrays in C, where lower integer value means higher priority.

#### Insertion (Enqueue) Operation

```c
#define MAX 100

typedef struct {
    int data;
    int priority;
} Element;

Element pq[MAX];
int size = 0;

// Insert an element into the priority queue
void enqueue(int value, int priority) {
    if (size == MAX) {
        printf("Priority Queue Overflow\n");
        return;
    }
    int i = size - 1;
    // Shift elements to maintain priority order (ascending)
    while (i  = 0 && pq[i].priority   priority) {
        pq[i + 1] = pq[i];
        i--;
    }
    pq[i + 1].data = value;
    pq[i + 1].priority = priority;
    size++;
}
```

#### Deletion (Dequeue) Operation

```c
// Remove and return the element with the highest priority
int dequeue() {
    if (size == 0) {
        printf("Priority Queue Underflow\n");
        return -1;
    }
    int value = pq[0].data;
    // Shift elements left
    for (int i = 1; i < size; i++) {
        pq[i - 1] = pq[i];
    }
    size--;
    return value;
}
```

#### Example Usage

```c
int main() {
    enqueue(10, 2);
    enqueue(5, 1);
    enqueue(20, 3);

    printf("Dequeued: %d\n", dequeue()); // 5 (priority 1)
    printf("Dequeued: %d\n", dequeue()); // 10 (priority 2)
    printf("Dequeued: %d\n", dequeue()); // 20 (priority 3)
    return 0;
}
```

**Note:** For more efficient priority queues, data structures like heaps are used.

## Example: Queue Operations (PYQ 4b)

  **PYQ 4(b):**
 
  **Consider the following linear queue capable of accommodating maximum five elements.**
  Front = 2, Rear = 4, Queue = [_, L, M, N, _]
  Compute the following operations:
  (i) Add O
  (ii) Add P
  (iii) Delete two letters
  (iv) Add Q, R
 
  **Answer:**
  Initial Queue: [_, L, M, N, _] (Front=2, Rear=4)
 
  - (i) Add O: Rear is at 4 (last position), so cannot add O (Queue Overflow)
  - (ii) Add P: Same as above, cannot add P (Queue Overflow)
  - (iii) Delete two letters:
    - First delete: Remove M (Front moves to 3)
    - Second delete: Remove N (Front moves to 4)
    - Queue now: [_, L, _, _, _] (Front=4, Rear=4)
  - (iv) Add Q, R:
    - Add Q: Rear at 4, cannot add (Queue Overflow)
    - Add R: Same, cannot add (Queue Overflow)
 
  **Note:** In a linear queue, once rear reaches the end, no more elements can be added even if there is space at the front. This is why circular queues are preferred.

## Inserting into an Existing Queue (PYQ 5)

  **PYQ 5:**
 
  **WAP to insert an element in already existing queue**
 
  Below is a C function to insert an element into an existing queue (assuming array implementation):
 
  ```c
  void enqueue(int queue[], int *rear, int MAX, int value) {
      if (*rear == MAX - 1) {
          printf("Queue Overflow\n");
          return;
      }
      (*rear)++;
      queue[*rear] = value;
  }
  ```
