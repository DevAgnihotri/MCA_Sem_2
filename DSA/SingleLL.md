# PYQs on Linked Lists (with Answers)

Below are important previous year questions (PYQs) on Linked Lists. Detailed answers are provided in the relevant sections below.

1. **How to represent the following linked lists in memory? Provide their self-referential structure and proper diagram.**

   - (i) Single linear Linked List
   - (ii) Doubly linear Linked list
   - (iii) Circular Doubly Linked List
   - (iv) Header Linked List
     See: [Memory Representation and Diagrams of Linked Lists](#memory-representation-and-diagrams-of-linked-lists)

2. **Give an algorithm or C function to perform following operations on single linear linked list:**

   - (i) Insert a node after a given node
   - (ii) Delete a node from end
     See: [Insert at End / Delete at End](#3b-delete-at-end) and [Insert a node after a given node](#pyq-2i-insert-a-node-after-a-given-node)

3. **What is a 2 way LL and its advantages over one way LL?**
   See: [What is a Linked List?](#what-is-a-linked-list)

4. **C program to find the greatest common divisor (GCD)**
   See: [PYQ 4: C program to find the greatest common divisor (GCD)](#pyq-4-c-program-to-find-the-greatest-common-divisor-gcd)

5. **C program to reverse a linked list**
   See: [Reversing a Singly Linked List](#reversing-a-singly-linked-list)

6. **What is doubly linked list? Write an algorithm to add an element in the doubly linked list before the given element.**
   See: [PYQ 6: Algorithm to add an element in the doubly linked list before a given element](#pyq-6-algorithm-to-add-an-element-in-the-doubly-linked-list-before-a-given-element)

---

## What is a Linked List?

A **Linked List** is a way to store a collection of items (like numbers or words) in a sequence. It is called "linked" because each item, called a **node**, is connected to the next one using a pointer.

Each node has two parts:

- **Data**: This is the value we want to store (for example, a number).
- **Pointer (Link)**: This is a reference (or address) that tells where the next node is in memory.

Unlike arrays, linked lists do not store their elements in a fixed, continuous block of memory. Instead, each node can be anywhere in memory, and the pointers keep them connected in order.

**Extra details:**

- The first node is called the **head** of the list.
- The last node points to `NULL`, which means there are no more nodes after it.
- Linked lists can grow or shrink easily because we can add or remove nodes without moving the other elements.
- They are useful when we need to insert or delete items often, but not as fast for finding items by position (like the 5th item).

In summary, a linked list is a flexible way to organize data where each piece knows where the next one is.

Unlike arrays:

- Memory is not contiguous.
- Insertion/Deletion is easier (no shifting).
- No fixed size (dynamic allocation).

---

## ✅ Types of Linked Lists

1. **Singly Linked List**

   - Each node contains data and a pointer to the next node.
   - The first node is called the **head**.
   - The last node is called as tail, Tail pointer points to `NULL`, indicating the end of the list.
   - There is no direct way to go backwards; traversal is only forward. (One-way)
   - _Main use:_ Simple, efficient insertion/deletion at the beginning; used for stacks, queues, and basic dynamic memory structures.

2. **Doubly Linked List**

   - A DLL is used when 2 way traversal of the list is requored is is capable to search a LL from both end 1st node to the last and vice - versa..
   - Each node contains data, a pointer to the next node (`next`), and a pointer to the previous node (`prev`).
   - The first node is the **head** (its `prev` is `NULL`).
   - The last node is the **tail** (its `next` is `NULL`).
   - Allows traversal in both forward and backward directions.
   - _Main use:_ Enables easy two-way traversal and deletion from both ends; used in navigation systems, undo functionality, and complex data structures.

3. **Circular Linked List**

   - Similar to a singly linked list, but the last node's `next` pointer points back to the **head** instead of `NULL`.
   - There is no `NULL` at the end; the CL list forms a loop.
   - Traversal can continue indefinitely unless stopped by a condition.
   - _Main use:_ Useful for applications that require a continuous loop, like round-robin scheduling or buffering.

4. **Circular Doubly Linked List**
   - Each node has both `next` and `prev` pointers.
   - The last node's `next` points to the **head**, and the head's `prev` points to the **tail**.
   - Both forward and backward traversal is possible, and the list forms a closed loop.
   - _Main use:_ Combines two-way traversal and looping; used in advanced data structures like navigation menus and playlist management.

---

## ✅ Singly Linked List in C

### 🔹 Node Structure

Each node contains:

- An integer data.
- A pointer to the next node.

```c
struct Node {
    int data;
    struct Node* next;
};
```

### 🔹 Key Concepts

- `head` – A pointer to the first node.
- `NULL` – Indicates the end of the list.
- `malloc()` – Allocates memory dynamically for new nodes.

---

##  Operations on Singly Linked List

The 8 functions created for the singly linked list are:

1. `createNode` (demonstrated inline, not as a separate function)
2. `insertAtBeginning`
3. `insertAtEnd`
4. `deleteNode`
5. `printList`
6. `search`
7. `insertAtPosition`
8. `deleteAtPosition`

### 1. **Create a Node**

Use `malloc()` to allocate memory and assign data.

```c
struct Node* newNode = (struct Node*)malloc(sizeof(struct Node));
newNode->data = 10;
newNode->next = NULL;
```

---

### 2. **Insert at Beginning**

```c
void insertAtBeginning(struct Node** head, int newData) {
    struct Node* newNode = (struct Node*)malloc(sizeof(struct Node));
    newNode->data = newData;
    newNode->next = *head;
    *head = newNode;
}
```

🧠 Why `**head`?

- Because we want to change the original `head` pointer (pass by reference).

---

### 3. **Insert at End**

```c
// Function to insert a new node at the end of the linked list
void insertAtEnd(struct Node** head, int newData) {
    // Allocate memory for new node
    struct Node* newNode = (struct Node*)malloc(sizeof(struct Node));
    // Create a pointer to traverse the list, starting from head
    struct Node* last = *head;

    // Set the data for the new node
    newNode->data = newData;
    // The new node will be the last, so its next is NULL
    newNode->next = NULL;

    // If the list is empty, make newNode the head
    if (*head == NULL) {
        *head = newNode;
        return;
    }

    // Traverse to the last node
    while (last->next != NULL)
        last = last->next;

    // Link the last node to the new node
    last->next = newNode;
}
```

# Important

### 3b. **Delete at End**

PYQ 2(ii):

**Delete a node from end (C function):**

See the function `deleteAtEnd` below for deleting the last node of a singly linked list.

```c
// Function to delete the last node of the linked list
void deleteAtEnd(struct Node** head) {
    if (*head == NULL)
        return;

    struct Node* temp = *head;

    // If there's only one node
    if (temp->next == NULL) {
        free(temp);
        *head = NULL;
        return;
    }

    // Find the second last node
    while (temp->next->next != NULL)
        temp = temp->next;

    free(temp->next);
    temp->next = NULL;
}
```

---

### PYQ 2(i): Insert a node after a given node

PYQ 2(i):

**Give an algorithm or C function to insert a node after a given node in a singly linked list.**

```c
// Insert a node after a given node
void insertAfter(struct Node* prevNode, int newData) {
    if (prevNode == NULL) return;
    struct Node* newNode = (struct Node*)malloc(sizeof(struct Node));
    newNode->data = newData;
    newNode->next = prevNode->next;
    prevNode->next = newNode;
}
```

---

### 4. **Delete a Node (by value)**

```c
void deleteNode(struct Node** head, int key) {
    struct Node *temp = *head, *prev = NULL;

    // If head node itself holds the key
    if (temp != NULL && temp->data == key) {
        *head = temp->next;
        free(temp);
        return;
    }

    // Search for the key
    while (temp != NULL && temp->data != key) {
        prev = temp;
        temp = temp->next;
    }

    // If not found
    if (temp == NULL) return;

    // Unlink and free memory
    prev->next = temp->next;
    free(temp);
}
```

---

### 5. **Display the List**

```c
void printList(struct Node* node) {
    while (node != NULL) {
        printf("%d -> ", node->data);
        node = node->next;
    }
    printf("NULL\n");
}
```

---

### 6. **Search for a Value**

```c
bool search(struct Node* head, int key) {
    struct Node* current = head;
    while (current != NULL) {
        if (current->data == key)
            return true;
        current = current->next;
    }
    return false;
}
```

# Important

### 7. **Insert at a Specific Position**

```c
// Insert a new node at a given position (0-based index)
void insertAtPosition(struct Node** head, int newData, int position) {
    struct Node* newNode = (struct Node*)malloc(sizeof(struct Node));
    newNode->data = newData;

    // Insert at the beginning
    if (position == 0) {
        newNode->next = *head;
        *head = newNode;
        return;
    }

    struct Node* current = *head;
    int i;
    // Traverse to the node before the desired position
    for (i = 0; current != NULL && i < position - 1; i++) {
        current = current->next;
    }

    // If position is out of bounds
    if (current == NULL) {
        free(newNode);
        return;
    }

    newNode->next = current->next;
    current->next = newNode;
}
```

### 8. **Delete at a Specific Position**

```c
// Delete a node at a given position (0-based index)
void deleteAtPosition(struct Node** head, int position) {
    if (*head == NULL) return;

    struct Node* temp = *head;

    // If head needs to be removed
    if (position == 0) {
        *head = temp->next;
        free(temp);
        return;
    }

    // Find previous node of the node to be deleted
    for (int i = 0; temp != NULL && i < position - 1; i++)
        temp = temp->next;

    // If position is out of bounds
    if (temp == NULL || temp->next == NULL)
        return;

    struct Node* nodeToDelete = temp->next;
    temp->next = nodeToDelete->next;
    free(nodeToDelete);
}
```

---

## ✅ Full Example with All Operations

```c
#include <stdio.h>
#include <stdlib.h>
#include <stdbool.h>

// Define node
struct Node {
    int data;
    struct Node* next;
};

// Insert at beginning
void insertAtBeginning(struct Node** head, int newData) {
    struct Node* newNode = (struct Node*)malloc(sizeof(struct Node));
    newNode->data = newData;
    newNode->next = *head;
    *head = newNode;
}

// Insert at end
void insertAtEnd(struct Node** head, int newData) {
    struct Node* newNode = (struct Node*)malloc(sizeof(struct Node));
    struct Node* last = *head;

    newNode->data = newData;
    newNode->next = NULL;

    if (*head == NULL) {
        *head = newNode;
        return;
    }

    while (last->next != NULL)
        last = last->next;

    last->next = newNode;
}

// Delete by value
void deleteNode(struct Node** head, int key) {
    struct Node *temp = *head, *prev = NULL;

    if (temp != NULL && temp->data == key) {
        *head = temp->next;
        free(temp);
        return;
    }

    while (temp != NULL && temp->data != key) {
        prev = temp;
        temp = temp->next;
    }

    if (temp == NULL) return;

    prev->next = temp->next;
    free(temp);
}

// Print list
void printList(struct Node* node) {
    while (node != NULL) {
        printf("%d -> ", node->data);
        node = node->next;
    }
    printf("NULL\n");
}

// Search
bool search(struct Node* head, int key) {
    struct Node* current = head;
    while (current != NULL) {
        if (current->data == key)
            return true;
        current = current->next;
    }
    return false;
}

// Driver code
int main() {
    struct Node* head = NULL;

    insertAtEnd(&head, 10);
    insertAtBeginning(&head, 5);
    insertAtEnd(&head, 20);
    insertAtBeginning(&head, 2);

    printf("Linked List: ");
    printList(head);

    deleteNode(&head, 10);
    printf("After Deletion of 10: ");
    printList(head);

    if (search(head, 5))
        printf("5 found in the list.\n");
    else
        printf("5 not found.\n");

    return 0;
}
```

---

## ✅ Output

```
Linked List: 2 -> 5 -> 10 -> 20 -> NULL
After Deletion of 10: 2 -> 5 -> 20 -> NULL
5 found in the list.
```

## ✅ Applications of Linked Lists

1. **Implementation of Dynamic Data Structures:**  
   Linked lists are the foundation for dynamic data structures such as stacks, queues, and hash tables. Their ability to efficiently insert and delete elements makes them ideal for these structures, where the size can change frequently during program execution.

2. **Memory Management (Free Lists):**  
   Operating systems and memory allocators use linked lists to manage free memory blocks. When memory is allocated or freed, linked lists help keep track of available memory segments, enabling efficient allocation and deallocation.

---

## ✅ Memory Management Note

Always use `free()` to release memory we allocate with `malloc()` to prevent **memory leaks**.

---

## ✅ Summary

| Operation         | Time Complexity |
| ----------------- | --------------- |
| Insertion (begin) | O(1)            |
| Insertion (end)   | O(n)            |
| Deletion (value)  | O(n)            |
| Search            | O(n)            |

## ✅ Reversing a Singly Linked List

### 🔹 Function to Reverse the List

```c
// Function to reverse a singly linked list
void reverseList(struct Node** head) {
    struct Node* prev = NULL;
    struct Node* current = *head;
    struct Node* next = NULL;

    while (current != NULL) {
        next = current->next;   // Store next node
        current->next = prev;   // Reverse current node's pointer
        prev = current;         // Move prev to current node
        current = next;         // Move to next node
    }
    *head = prev; // Update head to new first node
}
```

### 🔹 How It Works

- **prev** keeps track of the previous node (initially `NULL`).
- **current** traverses the list.
- For each node, we:
  1. Save the next node.
  2. Reverse the `next` pointer to point to the previous node.
  3. Move `prev` and `current` forward.
- At the end, `prev` points to the new head, so we update `*head`.

### 🔹 Example Usage

```c
reverseList(&head);
printf("Reversed List: ");
printList(head);
```

**Output:**

```
Reversed List: 20 -> 5 -> 2 -> NULL
```

## ✅ Sorting a Singly Linked List (By Rearranging Links)

To sort a singly linked list **without changing the data values** in the nodes, you need to rearrange the links (pointers) between nodes. One common approach is to use **Bubble Sort** by swapping the nodes themselves (not just their data).

### 🔹 Function to Sort the List (Bubble Sort by Links)

```c
// Function to sort the linked list by rearranging links (not data)
void sortList(struct Node** head) {
    if (*head == NULL || (*head)->next == NULL)
        return;

    int swapped;
    struct Node **ptr;
    do {
        swapped = 0;
        ptr = head;
        while ((*ptr)->next != NULL) {
            struct Node* a = *ptr;
            struct Node* b = a->next;
            if (a->data > b->data) {
                // Swap nodes by changing links
                a->next = b->next;
                b->next = a;
                *ptr = b;
                swapped = 1;
            }
            ptr = &((*ptr)->next);
        }
    } while (swapped);
}
```

### 🔹 Example Usage

```c
sortList(&head);
printf("Sorted List: ");
printList(head);
```

**Output:**

```
Sorted List: 2 -> 5 -> 20 -> NULL
```

**Note:**

- This function does not modify the data field of any node.
- It only rearranges the links between nodes to achieve a sorted order.
- Time complexity is O(n²) for Bubble Sort; for large lists, consider more efficient algorithms.

---

## ✅ Memory Representation and Diagrams of Linked Lists

PYQ 1:

**How to represent the following linked lists in memory? Provide their self-referential structure and proper diagram.**
(i) Single linear Linked List
(ii) Doubly linear Linked list
(iii) Circular Doubly Linked List
(iv) Header Linked List

### (i) **Singly Linear Linked List**

**Self-referential Structure:**

```c
struct Node {
    int data;
    struct Node* next;
};
```

**Diagram:**

```
+------+     +------+     +------+
| Data | --> | Data | --> | Data | --> NULL
+---+--+     +---+--+     +---+--+
    |            |            |
   next         next         next
```

---

### (ii) **Doubly Linear Linked List**

**Self-referential Structure:**

```c
struct DNode {
    int data;
    struct DNode* prev;
    struct DNode* next;
};
```

**Diagram:**

```
NULL <--+------+<-->+------+<-->+------+--> NULL
       | Data |    | Data |    | Data |
       +--+---+    +--+---+    +--+---+
         ^  |        ^  |        ^  |
       prev next   prev next   prev next
```

---

### (iii) **Circular Doubly Linked List**

**Self-referential Structure:**

```c
struct CDNode {
    int data;
    struct CDNode* prev;
    struct CDNode* next;
};
```

**Diagram:**

```
   +------+<-->+------+<-->+------+
   | Data |    | Data |    | Data |
   +--+---+    +--+---+    +--+---+
   ^  |         ^  |        ^  |
   |  v         |  v        |  v
   +-------------+----------+
   |                        |
   +------------------------+
(Last node's next points to head, head's prev points to last)
```

---

### (iv) **Header Linked List**

A header linked list uses a special node (header) at the beginning, which may not store actual data but helps simplify list operations.

**Self-referential Structure:**

```c
struct Node {
    int data;
    struct Node* next;
};
// Header node (can use a flag or reserved value for header)
```

**Diagram:**

```
+--------+     +------+     +------+
| Header | --> | Data | --> | Data | --> NULL
+---+----+     +---+--+     +---+--+
    |             |            |
   next          next         next
```

## ✅ Representing a Polynomial Using Linked List

A polynomial like **5x³ + 4x² + 3x + 2** can be represented using a linked list where each node contains:

- The coefficient (`coeff`)
- The exponent (`exp`)
- A pointer to the next node

**Node Structure:**

```c
struct PolyNode {
    int coeff;
    int exp;
    struct PolyNode* next;
};
```

**Example Representation:**

| Coefficient | Exponent | Next |
| ----------- | -------- | ---- |
| 5           | 3        | →    |
| 4           | 2        | →    |
| 3           | 1        | →    |
| 2           | 0        | NULL |

---

## ✅ Algorithm: Addition of Two Polynomials Using Linked List

**Steps:**

1. Create two linked lists for the polynomials, sorted by decreasing exponents.
2. Traverse both lists:
   - If exponents are equal, add coefficients and create a new node.
   - If one exponent is greater, copy that term to the result and move its pointer.
   - Continue until both lists are exhausted.
3. Append any remaining terms from either list.

**Pseudocode:**

```c
struct PolyNode* addPolynomials(struct PolyNode* poly1, struct PolyNode* poly2) {
    struct PolyNode* result = NULL;
    struct PolyNode** lastPtr = &result;

    while (poly1 && poly2) {
        struct PolyNode* temp = (struct PolyNode*)malloc(sizeof(struct PolyNode));
        if (poly1->exp == poly2->exp) {
            temp->coeff = poly1->coeff + poly2->coeff;
            temp->exp = poly1->exp;
            poly1 = poly1->next;
            poly2 = poly2->next;
        } else if (poly1->exp > poly2->exp) {
            temp->coeff = poly1->coeff;
            temp->exp = poly1->exp;
            poly1 = poly1->next;
        } else {
            temp->coeff = poly2->coeff;
            temp->exp = poly2->exp;
            poly2 = poly2->next;
        }
        temp->next = NULL;
        *lastPtr = temp;
        lastPtr = &(temp->next);
    }

    // Append remaining terms
    while (poly1) {
        struct PolyNode* temp = (struct PolyNode*)malloc(sizeof(struct PolyNode));
        temp->coeff = poly1->coeff;
        temp->exp = poly1->exp;
        temp->next = NULL;
        *lastPtr = temp;
        lastPtr = &(temp->next);
        poly1 = poly1->next;
    }
    while (poly2) {
        struct PolyNode* temp = (struct PolyNode*)malloc(sizeof(struct PolyNode));
        temp->coeff = poly2->coeff;
        temp->exp = poly2->exp;
        temp->next = NULL;
        *lastPtr = temp;
        lastPtr = &(temp->next);
        poly2 = poly2->next;
    }
    return result;
}
```

**Summary:**

- Each term of the polynomial is a node.
- Addition is performed by traversing both lists and combining like terms.

---

## ✅ Advantages of Doubly Linked List Over Singly Linked List

- **Bidirectional Traversal:**  
   In a doubly linked list (DLL), each node has pointers to both the next and previous nodes. This allows traversal in both directions (forward and backward), making certain operations more efficient.

- **Easier Deletion:**  
   Deleting a node in a DLL is simpler and faster because you have direct access to the previous node via the `prev` pointer. In a singly linked list (SLL), you must traverse from the head to find the previous node before deletion.

- **Efficient Insertion/Deletion at Both Ends:**  
   DLLs allow efficient insertion and deletion at both the beginning and end of the list, especially if you maintain pointers to both head and tail.

- **Useful for Complex Data Structures:**  
   DLLs are better suited for implementing data structures like navigation systems, undo/redo functionality, and certain types of caches.

---

## ✅ Deleting a Node: Singly vs Doubly Linked List

### 🔹 In Singly Linked List

- Each node has only a `next` pointer.
- To delete a node (other than the head), you must:
  1. Traverse the list to find the node **before** the one to delete.
  2. Change its `next` pointer to skip the node to be deleted.
  3. Free the memory of the deleted node.

**Example:**

```c
// Delete node with value 'key' in SLL
void deleteNode(struct Node** head, int key) {
        struct Node *temp = *head, *prev = NULL;
        if (temp != NULL && temp->data == key) {
                *head = temp->next;
                free(temp);
                return;
        }
        while (temp != NULL && temp->data != key) {
                prev = temp;
                temp = temp->next;
        }
        if (temp == NULL) return;
        prev->next = temp->next;
        free(temp);
}
```

### 🔹 In Doubly Linked List

- Each node has both `next` and `prev` pointers.
- To delete a node:
  1. Update the `next` pointer of the previous node (if it exists).
  2. Update the `prev` pointer of the next node (if it exists).
  3. Free the memory of the deleted node.
- No need to traverse from the head to find the previous node.

**Example:**

```c
// Delete a given node 'del' in DLL
void deleteNode(struct DNode** head, struct DNode* del) {
        if (*head == NULL || del == NULL) return;
        if (*head == del)
                *head = del->next;
        if (del->next != NULL)
                del->next->prev = del->prev;
        if (del->prev != NULL)
                del->prev->next = del->next;
        free(del);
}
```

**Summary:**

- DLLs make deletion operations more efficient and straightforward, especially when you have a pointer to the node to be deleted.
- SLLs require extra traversal to find the previous node, making deletion less efficient.

---

## PYQ 4: C program to find the greatest common divisor (GCD)

PYQ 4:

**C program to find the greatest common divisor (GCD) of two numbers**

```c
#include <stdio.h>
int gcd(int a, int b) {
    if (b == 0)
        return a;
    else
        return gcd(b, a % b);
}
int main() {
    int x = 36, y = 60;
    printf("GCD of %d and %d is %d\n", x, y, gcd(x, y));
    return 0;
}
```

---

## PYQ 6: Algorithm to add an element in the doubly linked list before a given element

PYQ 6:

**What is doubly linked list? Write an algorithm to add an element in the doubly linked list before the given element.**

A **doubly linked list** is a linked list in which each node contains a pointer to both the next and previous nodes, allowing traversal in both directions.

**Algorithm to insert before a given element:**

1. Create a new node with the given data.
2. Traverse the list to find the node with the target value.
3. If the node is found:
   - Set newNode->prev = target->prev
   - Set newNode->next = target
   - If target->prev is not NULL, set target->prev->next = newNode
   - Set target->prev = newNode
   - If the node is the head, update the head pointer to newNode
4. If the node is not found, do nothing or report not found.

```c
// Insert before a given value in a doubly linked list
void insertBefore(struct DNode** head, int target, int newData) {
    struct DNode* curr = *head;
    while (curr && curr->data != target)
        curr = curr->next;
    if (!curr) return; // Target not found
    struct DNode* newNode = (struct DNode*)malloc(sizeof(struct DNode));
    newNode->data = newData;
    newNode->prev = curr->prev;
    newNode->next = curr;
    if (curr->prev)
        curr->prev->next = newNode;
    else
        *head = newNode; // New node becomes head
    curr->prev = newNode;
}
```
