# Stack in C

A **stack** is a linear data structure that follows the Last In First Out (LIFO) principle. This means the last element added to the stack will be the first one to be removed.

### Example: Stack using Array

```c
#define MAX 100
int stack[MAX];
int top = -1;

// (Operations as shown above)
```

## Summary

- Stack is a LIFO data structure.
- Main operations: push, pop, peek, isEmpty, isFull.
- Can be implemented using arrays or linked lists in C.
- Used in function calls, expression evaluation, undo features, etc.

## Complete Stack Program in C

Below is a complete example of a stack implementation in C using an array, including a simple menu-driven interface:

```c
#include <stdio.h>
#define MAX 100

int stack[MAX];
int top = -1;

void push(int value) {
    if (top == MAX - 1)
        printf("Stack Overflow\n");
    else
        stack[++top] = value;
}

int pop() {
    if (top == -1) {
        printf("Stack Underflow\n");
        return -1;
    } else
        return stack[top--];
}

int peek() {
    if (top == -1) {
        printf("Stack is Empty\n");
        return -1;
    } else
        return stack[top];
}

int isEmpty() {
    return top == -1;
}

int isFull() {
    return top == MAX - 1;
}

void display() {
    if (top == -1) {
        printf("Stack is Empty\n");
    } else {
        printf("Stack elements:\n");
        for (int i = top; i >= 0; i--)
            printf("%d\n", stack[i]);
    }
}

int main() {
    int choice, value;
    while (1) {
        printf("\n--- Stack Menu ---\n");
        printf("1. Push\n2. Pop\n3. Peek\n4. Display\n5. Exit\n");
        printf("Enter your choice: ");
        scanf("%d", &choice);

        switch (choice) {
            case 1:
                printf("Enter value to push: ");
                scanf("%d", &value);
                push(value);
                break;
            case 2:
                value = pop();
                if (value != -1)
                    printf("Popped: %d\n", value);
                break;
            case 3:
                value = peek();
                if (value != -1)
                    printf("Top element: %d\n", value);
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

## Reverse a String Using Stack

### Logic

1. **Push each character of the string onto the stack.**
2. **Pop characters from the stack and overwrite the string.**
   - Since stack is LIFO, popping gives characters in reverse order.

#### Dry Run Example

Suppose the input string is `"ABC"`:

| Step      | Stack Content | String Content |
| --------- | ------------- | -------------- |
| Initial   | (empty)       | "ABC"          |
| Push 'A'  | A             | "ABC"          |
| Push 'B'  | A, B          | "ABC"          |
| Push 'C'  | A, B, C       | "ABC"          |
| Pop → 'C' | A, B          | "C"            |
| Pop → 'B' | A             | "CB"           |
| Pop → 'A' | (empty)       | "CBA"          |

- After all pops, the string is reversed to `"CBA"`.

**Summary:**

- Push all characters to stack → stack holds ['A', 'B', 'C'] (top is 'C').
- Pop and overwrite string → get 'C', 'B', 'A' in order.
- Result: string is reversed.

### Code

```c
#include <stdio.h>
#include <string.h>
#define MAX 100

char stack[MAX];
int top = -1;

// Push character onto stack
void push(char c) {
    if (top == MAX - 1)
        printf("Stack Overflow\n");
    else
        stack[++top] = c;
}

// Pop character from stack
char pop() {
    if (top == -1)
        return '\0';
    else
        return stack[top--];
}

void reverseString(char str[]) {
    int len = strlen(str);
    // Push all characters onto stack
    for (int i = 0; i < len; i++)
        push(str[i]);
    // Pop all characters and put back into str
    for (int i = 0; i < len; i++)
        str[i] = pop();
}

int main() {
    char str[MAX];
    printf("Enter a string: ");
    fgets(str, MAX, stdin);
    // Remove newline character if present
    str[strcspn(str, "\n")] = '\0';

    reverseString(str);
    printf("Reversed string: %s\n", str);
    return 0;
}
```

**How it works:**

- Each character of the string is pushed onto the stack.
- When popping from the stack, characters come out in reverse order, thus reversing the string.

## Recursion in C

### What is Recursion?

**Recursion** is a programming technique where a function calls itself directly or indirectly to solve a problem. Each recursive call solves a smaller instance of the original problem, and the process continues until a base case (a condition to stop recursion) is reached.

### When is Recursion Used?

Recursion is used when a problem can be solved by breaking it down into smaller versions of the same problem. This is helpful when each step of the solution looks similar to the whole problem.

**When to use recursion:**

- When a problem can be divided into smaller, similar subproblems.
- When the solution to a problem depends on solutions to smaller instances of the same problem.
- When the problem has a clear stopping condition (base case).

**Example: Calculating Factorial**

Suppose you want to calculate the factorial of a number `n` (written as `n!`). The factorial of 5 is:

```
5! = 5 × 4 × 3 × 2 × 1 = 120
```

Notice that `5! = 5 × 4!`, and `4! = 4 × 3!`, and so on. Each step is a smaller version of the same problem.

**Recursive Algorithm:**

To calculate the factorial recursively:

1. If `n` is 0, return 1 (base case).
2. Otherwise, return `n * factorial(n - 1)`.

**C Code Example:**

```c
int factorial(int n) {
    if (n == 0) // base case
        return 1;
    else
        return n * factorial(n - 1); // recursive call
}
```

**Time Complexity Analysis:**

- The function makes one recursive call for each decrement of `n` until it reaches 0.
- Therefore, for input `n`, there are `n + 1` calls (including the base case).
- **Time Complexity:** O(n)

**Summary:**  
Use recursion when a problem can be naturally split into smaller, similar problems, and you can define a clear stopping point.

### How Recursion Works

A recursive function has two main parts:

1. **Base Case:** The condition under which the function stops calling itself.
2. **Recursive Case:** The part where the function calls itself with a smaller or simpler input.

### Good Uses of Recursion

- **Tree Traversals:** Navigating hierarchical data like file systems or expression trees.
- **Divide and Conquer Algorithms:** Such as quicksort, mergesort, and binary search.
- **Problems with Unknown or Variable Depth:** Like exploring all possible paths in a maze.

#### Example: Fibonacci Sequence

```c
int fibonacci(int n) {
    if (n == 0) return 0; // Base case
    if (n == 1) return 1; // Base case
    return fibonacci(n-1) + fibonacci(n-2); // Recursive calls
}
```

### When Recursion is Not Good

- **When the problem can be solved more efficiently with loops:** Recursion can lead to high memory usage and slower performance due to repeated function calls.
- **When the recursion depth is very large:** This can cause a stack overflow error.
- **When the same subproblems are solved repeatedly:** This leads to inefficiency (e.g., naive Fibonacci).

#### Example: Bad Use of Recursion

Calculating Fibonacci numbers recursively without memoization is inefficient because it recalculates the same values many times.

```c
// Inefficient for large n
int fibonacci(int n) {
    if (n == 0) return 0;
    if (n == 1) return 1;
    return fibonacci(n-1) + fibonacci(n-2);
}
```

For large `n`, this approach is very slow and can crash due to too many recursive calls.

### Pros and Cons of Recursion

**Advantages:**

- Code is often simpler and easier to read for problems with recursive structure.
- Reduces complex problems to simpler subproblems.

**Disadvantages:**

- Uses more memory (stack space) due to function calls.
- Can be slower than iterative solutions.
- Risk of stack overflow if recursion is too deep.

### Summary Table

| Good for...                 | Bad for...                         |
| --------------------------- | ---------------------------------- |
| Tree/graph traversals       | Problems with large input sizes    |
| Divide and conquer          | Problems with repeated subproblems |
| Problems with unknown depth | When loops are more efficient      |

### Conclusion

Recursion is a powerful tool for solving problems that can be divided into similar subproblems. It makes code cleaner and easier to understand for certain tasks, but should be used carefully to avoid inefficiency and stack overflow. Always ensure there is a clear base case, and consider iterative solutions for performance-critical code.

---

## Tower of Hanoi

### What is the Tower of Hanoi?

The **Tower of Hanoi** is a classic mathematical puzzle involving three rods (also called pegs) and a number of disks of different sizes. The disks are initially stacked in ascending order of size (largest at the bottom, smallest at the top) on one rod. The goal is to move the entire stack to another rod, following these rules:

1. **Only one disk can be moved at a time.**
2. **Each move consists of taking the upper disk from one of the stacks and placing it on top of another stack or on an empty rod.**
3. **No disk may be placed on top of a smaller disk.**

### Problem Setup

- **Number of disks:** 3
- **Number of rods:** 3 (commonly named A, B, and C)

#### Initial State

All 3 disks are stacked on rod A (source rod), and rods B (auxiliary) and C (destination) are empty.

### Solution for 3 Disks and 3 Rods

Let's name the rods:

- **A:** Source rod
- **B:** Auxiliary rod
- **C:** Destination rod

#### Step-by-Step Moves

1. Move Disk 1 from A to C
2. Move Disk 2 from A to B
3. Move Disk 1 from C to B
4. Move Disk 3 from A to C
5. Move Disk 1 from B to A
6. Move Disk 2 from B to C
7. Move Disk 1 from A to C

**Total moves required:** 7 (for 3 disks, the minimum number of moves is 2³ - 1 = 7)

#### Visual Representation

| Move | From | To  |
| ---- | ---- | --- |
| 1    | A    | C   |
| 2    | A    | B   |
| 3    | C    | B   |
| 4    | A    | C   |
| 5    | B    | A   |
| 6    | B    | C   |
| 7    | A    | C   |

### Algorithm (Recursive Approach)

The Tower of Hanoi problem is best solved using recursion.

#### Steps

1. Move (n-1) disks from Source to Auxiliary rod.
2. Move the nth (largest) disk from Source to Destination rod.
3. Move the (n-1) disks from Auxiliary to Destination rod.

#### Pseudocode

```
TOH(n, Source, Auxiliary, Destination):
    if n == 1:
        print "Move disk 1 from Source to Destination"
        return
    TOH(n-1, Source, Destination, Auxiliary)
    print "Move disk", n, "from Source to Destination"
    TOH(n-1, Auxiliary, Source, Destination)
```

#### Example for 3 Disks

Call: `TOH(3, A, B, C)`

- Move 2 disks from A to B (using C)
- Move disk 3 from A to C
- Move 2 disks from B to C (using A)

### C Code Example

```c
#include <stdio.h>

void towerOfHanoi(int n, char source, char auxiliary, char destination) {
    if (n == 1) {
        printf("Move disk 1 from %c to %c\n", source, destination);
        return;
    }
    towerOfHanoi(n - 1, source, destination, auxiliary);
    printf("Move disk %d from %c to %c\n", n, source, destination);
    towerOfHanoi(n - 1, auxiliary, source, destination);
}

int main() {
    int n = 3; // Number of disks
    towerOfHanoi(n, 'A', 'B', 'C');
    return 0;
}
```

### Summary

- Tower of Hanoi is a puzzle with 3 rods and n disks.
- Only one disk can be moved at a time, and a larger disk cannot be placed on a smaller one.
- The minimum number of moves required is (2ⁿ - 1).
- The problem is solved recursively by moving smaller stacks between rods.
