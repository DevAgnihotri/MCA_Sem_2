# DSA

### Data

Data is raw facts or figures without any meaning by themselves. For example, numbers, letters, or symbols.

### Entity

An entity is something that exists and can be identified. For example, a person, a book, or a car.

### Information

Information is processed data that has meaning and is useful for making decisions.

### Difference between Data and Information

- **Data** is unprocessed and meaningless on its own.
- **Information** is data that has been processed and given meaning.

### Data Type

A data type defines what kind of value a variable can hold, such as numbers, characters, or true/false.

### Built-in Data Type

Built-in data types are basic types provided by a programming language, like `int`, `float`, `char`, and `bool` in C.

### Abstract Data Type (ADT)

An abstract data type (ADT) is a way to describe what you can do with a group of data, without worrying about how it is stored or implemented.

For example, a stack ADT can be described by the operations `push`, `pop`, and `peek`, without specifying how the stack is implemented. In C, you might use a `struct` to represent the stack and write functions to perform these operations. The implementation details (such as using an array or a linked list) are hidden from the user, who interacts only with the defined operations.

This separation of interface (what operations are available) from implementation (how those operations are carried out) is a key idea behind ADTs in C.

### Difference between Abstract Data Type, Data Type, and Data Structure

| Term                         | Simple Definition                                                                    | Example (in C/C++)        |
| ---------------------------- | ------------------------------------------------------------------------------------ | ------------------------- |
| **Data Type**                | Describes the kind of value a variable can hold and what operations are allowed.     | `int`, `float`, `char`    |
| **Data Structure**           | A way of organizing and storing data for efficient access and modification.          | Array, Linked List, Stack |
| **Abstract Data Type (ADT)** | A logical description of data and allowed operations, hiding implementation details. | Stack ADT (with push/pop) |

**In short:**

- Data Type: What kind of data?
- Data Structure: How is data stored?
- ADT: What can you do with the data (operations), without worrying about how it's done?

## Definition of Data Structures

Data structures are ways of organizing and storing data so that it can be used efficiently, like arrays, linked lists, stacks, and queues.

### Classification of Data Structures

Data structures can be classified into two main categories:

- **Primitive Data Structures**: These are the basic data types provided by a programming language, such as `int`, `float`, `char`, and `bool`.
- **Non-Primitive Data Structures**: These are more complex and are built using primitive data structures. They are further divided into:

  - **Linear Data Structures**: Elements are arranged in a sequential manner. Examples include arrays, linked lists, stacks, and queues.
  - **Non-Linear Data Structures**: Elements are arranged in a hierarchical manner. Examples include trees and graphs.

  ### Linear Data Structures

  Linear data structures arrange their elements in a sequential order, where each element has a unique predecessor and successor (except the first and last elements). You can traverse all elements in a single run, one after another.

  **Examples:** Arrays, Linked Lists, Stacks, Queues

  **Key Points:**

  - Elements are stored in a linear or sequential manner.
  - Easy to implement and use.
  - Memory is often allocated in a contiguous block (like arrays) or linked through pointers (like linked lists).

  ***

  ### Non-Linear Data Structures

  Non-linear data structures arrange their elements in a hierarchical or interconnected way, where each element can be connected to multiple elements. Traversal is not always sequential.

  **Examples:** Trees, Graphs

  **Key Points:**

  - Elements are stored in a hierarchical or networked manner.
  - More complex to implement and use.
  - Useful for representing relationships like parent-child (trees) or networks (graphs).

  ***

  ### Difference Between Linear and Non-Linear Data Structures

  | Feature        | Linear Data Structures           | Non-Linear Data Structures        |
  | -------------- | -------------------------------- | --------------------------------- |
  | Arrangement    | Sequential (one after another)   | Hierarchical or interconnected    |
  | Traversal      | Single run (one by one)          | Multiple paths possible           |
  | Examples       | Array, Linked List, Stack, Queue | Tree, Graph                       |
  | Memory Usage   | Often contiguous or simple links | Can be complex and non-contiguous |
  | Implementation | Easier                           | More complex                      |
  | Relationship   | One-to-one                       | One-to-many or many-to-many       |

### Importance of Data Structures

Choosing the right data structure is crucial because it affects the efficiency of algorithms and the overall performance of software. Proper use of data structures can lead to:

- Faster data access and manipulation
- Efficient memory usage
- Simplified code maintenance and readability

### Examples of Data Structures

- **Array**: Stores elements of the same type in a contiguous block of memory.
- **Linked List**: Consists of nodes where each node contains data and a reference to the next node.
- **Stack**: Follows Last-In-First-Out (LIFO) principle.
- **Queue**: Follows First-In-First-Out (FIFO) principle.
- **Tree**: Hierarchical structure with a root node and child nodes.
- **Graph**: Consists of nodes (vertices) connected by edges.

### Basic Operations on Data Structures

Common operations performed on data structures include:

- **Insertion**: Adding a new element to the data structure.
- **Deletion**: Removing an existing element from the data structure.
- **Traversal**: Accessing each element of the data structure, often to display or process them.
- **Searching**: Finding the location of a specific element within the data structure.
- **Sorting**: Arranging the elements in a particular order (e.g., ascending or descending).

These operations may vary in implementation and efficiency depending on the type of data structure used.

## Definition of Algorithms

An **algorithm** is a step-by-step procedure or set of rules to solve a specific problem or perform a task. It takes input, processes it, and produces output.

## Difference between Algorithm and Program

| Feature    | Algorithm                                 | Program                                    |
| ---------- | ----------------------------------------- | ------------------------------------------ |
| Definition | Step-by-step procedure to solve a problem | Set of instructions written in a language  |
| Purpose    | Problem-solving logic                     | Implementation of logic for execution      |
| Language   | Independent of programming language       | Written in a specific programming language |
| Output     | Produces a result or solution             | Produces a complete, working application   |

## Properties of an Algorithm

1. **Input**: Should have zero or more inputs.
2. **Output**: Should produce at least one output.
3. **Definiteness**: Each step must be clear and unambiguous.
4. **Finiteness**: Must terminate after a finite number of steps.
5. **Effectiveness**: Each step must be basic enough to be carried out.

## Algorithm Design Techniques

- **Divide and Conquer**: Break the problem into smaller subproblems, solve them, and combine results (e.g., Merge Sort).
- **Greedy Method**: Make the best choice at each step (e.g., Dijkstra’s algorithm).
- **Dynamic Programming**: Solve subproblems and store their results to avoid recomputation (e.g., Fibonacci sequence).
- **Backtracking**: Try all possible solutions and backtrack when a solution fails (e.g., N-Queens problem).

## Performance Analysis of Algorithms

- **Time Complexity**: Measures the amount of time an algorithm takes as a function of input size.
- **Space Complexity**: Measures the amount of memory an algorithm uses as a function of input size.

## Order of Growth and Asymptotic Notations

### Order of Growth

- **Definition:**  
   Order of Growth describes how the running time or space requirements of an algorithm increase as the input size (`n`) increases.
- **Purpose:**  
   It helps compare algorithms based on their efficiency, especially for large inputs.
- **Key Idea:**  
   Focuses on the dominant term in the time/space complexity, ignoring constants and lower-order terms.
- **Examples:**
  - Linear: `O(n)` – time grows proportionally with input size.
  - Quadratic: `O(n^2)` – time grows with the square of input size.
  - Logarithmic: `O(log n)` – time grows slowly as input increases.
  - Constant: `O(1)` – time does not depend on input size.

### Asymptotic Notations

Asymptotic notations are mathematical tools to describe the limiting behavior of a function when the argument tends towards a particular value or infinity. In algorithms, they describe the running time or space as input size grows.

#### 1. Big O Notation (`O`)

- **Definition:**  
   Describes the upper bound of an algorithm's running time.  
   It gives the worst-case scenario.
- **Usage:**  
   `f(n) = O(g(n))` means for large enough `n`, `f(n)` grows no faster than a constant multiple of `g(n)`.
- **Example:**  
   If an algorithm takes at most `3n^2 + 2n + 1` steps, it is `O(n^2)`.

#### 2. Omega Notation (`Ω`)

- **Definition:**  
   Describes the lower bound of an algorithm's running time.  
   It gives the best-case scenario.
- **Usage:**  
   `f(n) = Ω(g(n))` means for large enough `n`, `f(n)` grows at least as fast as a constant multiple of `g(n)`.
- **Example:**  
   If an algorithm takes at least `n` steps, it is `Ω(n)`.

#### 3. Theta Notation (`Θ`)

- **Definition:**  
   Describes the tight bound (both upper and lower) of an algorithm's running time.
- **Usage:**  
   `f(n) = Θ(g(n))` means for large enough `n`, `f(n)` grows at the same rate as `g(n)`.
- **Example:**  
   If an algorithm always takes `2n + 3` steps, it is `Θ(n)`.

#### 4. Little o Notation (`o`)

- **Definition:**  
   Describes a strict upper bound.  
   `f(n) = o(g(n))` means `f(n)` grows strictly slower than `g(n)` as `n` increases.
- **Example:**  
   `n = o(n^2)` because `n` grows much slower than `n^2`.

#### 5. Little omega Notation (`ω`)

- **Definition:**  
   Describes a strict lower bound.  
   `f(n) = ω(g(n))` means `f(n)` grows strictly faster than `g(n)` as `n` increases.
- **Example:**  
   `n^2 = ω(n)` because `n^2` grows much faster than `n`.

### Summary Table

| Notation | Meaning       | Describes    | Example    |
| -------- | ------------- | ------------ | ---------- |
| O        | Upper bound   | Worst-case   | O(n^2)     |
| Ω        | Lower bound   | Best-case    | Ω(n)       |
| Θ        | Tight bound   | Exact growth | Θ(n log n) |
| o        | Strictly less |              | o(n^2)     |
| ω        | Strictly more |              | ω(n)       |

### Why Use Asymptotic Notations?

- **Abstracts away machine-specific constants.**
- **Allows comparison of algorithms regardless of hardware.**
- **Focuses on scalability and efficiency for large inputs.**

### Key Points

- Asymptotic notations help analyze and compare algorithms.
- Order of growth is about how performance scales with input size.
- Big O is most commonly used for expressing worst-case complexity.
- Use these notations to choose efficient algorithms for large-scale problems.

## Complexity of Various Code Structures\Algorithms

Understanding how different code structures affect time complexity is essential for analyzing algorithms. Below are common code constructs and their typical complexities, with examples.

### Space and Time Complexity (in Simple Terms)

When we talk about how "good" an algorithm is, we usually look at two things:

- **Time Complexity:**  
   This tells us how much time (how many steps) an algorithm takes as the input gets bigger. For example, if you have to check every item in a list of `n` items, the time it takes grows as `n` grows.

- **Space Complexity:**  
   This tells us how much extra memory (space) an algorithm needs as the input gets bigger. For example, if you make a new list to store results, the space you need depends on how many items you store.

#### Why are these important?

- If an algorithm is slow (high time complexity), it will take a long time to finish for big inputs.
- If it uses too much memory (high space complexity), it might not run at all on a computer with limited RAM.

#### Simple Examples

- **Time Complexity Example:**  
   A loop that runs `n` times has time complexity O(n).  
   A loop inside a loop (nested) that both run `n` times has time complexity O(n²).

- **Space Complexity Example:**  
   If you only use a few variables, space complexity is O(1) (constant).  
   If you create a new array of size `n`, space complexity is O(n).

**In short:**

- Time complexity = How fast?
- Space complexity = How much memory?
- Lower is usually better for both.
- We use Big O notation (like O(n), O(1), O(n²)) to describe both.

### 1. Simple Statements

- **Description:** Single operations like assignments, arithmetic, or accessing an array element.
- **Complexity:** Constant time, O(1)
- **Example:**
  ```cpp
  int x = 5;
  arr[2] = 10;
  ```

### 2. Sequential Statements

- **Description:** Multiple statements executed one after another.
- **Complexity:** Still O(1) if the number of statements is fixed; otherwise, sum of individual complexities.
- **Example:**
  ```cpp
  int a = 1;
  int b = 2;
  int c = a + b;
  ```

### 3. Loops

- **Description:** Repeated execution of a block.
- **Complexity:** O(n) if the loop runs n times.
- **Example:**
  ```cpp
  for (int i = 0; i < n; i++) {
      // O(1) operation
  }
  ```

### 4. Nested Loops

- **Description:** A loop inside another loop.
- **Complexity:** Multiply the complexities, e.g., O(n^2) for two nested loops each running n times.
- **Example:**
  ```cpp
  for (int i = 0; i < n; i++) {
      for (int j = 0; j < n; j++) {
          // O(1) operation
      }
  }
  ```

### 5. Conditional Statements

- **Description:** if, else-if, else blocks.
- **Complexity:** O(1) for a single condition; overall complexity depends on code inside the branches.
- **Example:**
  ```cpp
  if (x > 0) {
      // O(1)
  } else {
      // O(1)
  }
  ```

### 6. Function Calls

- **Description:** Invoking a function.
- **Complexity:** Depends on the function's implementation. If the function is O(1), the call is O(1); if O(n), the call is O(n).
- **Example:**
  ```cpp
  int sum = add(a, b); // Complexity depends on add()
  ```

### 7. Recursion

- **Description:** A function calling itself.
- **Complexity:** Depends on the number of recursive calls and work per call. For example, O(n) for linear recursion, O(2^n) for exponential recursion.
- **Example:**
  ```cpp
  int factorial(int n) {
      if (n == 0) return 1;
      else return n * factorial(n - 1);
  }
  // O(n)
  ```

### 8. Switch Statements

- **Description:** Multi-way branching.
- **Complexity:** O(1) for a single switch; depends on code in each case.
- **Example:**
  ```cpp
  switch (option) {
      case 1: // O(1)
          break;
      case 2: // O(1)
          break;
  }
  ```

### 9. Early Termination (Break/Return)

- **Description:** Exiting loops or functions early.
- **Complexity:** Can improve best-case complexity, but worst-case is usually considered for Big O.
- **Example:**
  ```cpp
  for (int i = 0; i < n; i++) {
      if (arr[i] == target) break; // Best-case O(1), worst-case O(n)
  }
  ```

### 10. Logarithmic Time (`O(log n)`)

- **Description:** Operations that reduce the problem size by a constant factor each time, such as binary search.
- **Complexity:** O(log n)
- **Example:**
  ```cpp
  int binarySearch(int arr[], int n, int target) {
      int left = 0, right = n - 1;
      while (left <= right) {
          int mid = left + (right - left) / 2;
          if (arr[mid] == target) return mid;
          else if (arr[mid] < target) left = mid + 1;
          else right = mid - 1;
      }
      return -1;
  }
  // O(log n)
  ```

### 11. Linearithmic Time (`O(n log n)`)

- **Description:** Algorithms that perform a logarithmic operation for each element, such as efficient sorting algorithms.
- **Complexity:** O(n log n)
- **Example:**
  ```cpp
  void mergeSort(int arr[], int l, int r) {
      if (l < r) {
          int m = l + (r - l) / 2;
          mergeSort(arr, l, m);
          mergeSort(arr, m + 1, r);
          merge(arr, l, m, r);
      }
  }
  // O(n log n)
  ```

### 12. Polynomial Time (`O(n^k)`)

- **Description:** Algorithms with nested loops or repeated operations, where `k` is a constant (e.g., O(n^2), O(n^3)).
- **Complexity:** O(n^k)
- **Example:**
  ```cpp
  // O(n^3) triple nested loop
  for (int i = 0; i < n; i++)
      for (int j = 0; j < n; j++)
          for (int k = 0; k < n; k++)
              ; // O(1)
  ```

### 13. Exponential Time (`O(2^n)`)

- **Description:** Algorithms that double the work with each additional input, such as recursive solutions to the subset sum or traveling salesman problems.
- **Complexity:** O(2^n)
- **Example:**
  ```cpp
  int fib(int n) {
      if (n <= 1) return n;
      return fib(n - 1) + fib(n - 2);
  }
  // O(2^n)
  ```

### 14. Constant Exponential Time (`O(c^n)`)

- **Description:** Similar to exponential, but with a constant base `c > 1` (e.g., O(3^n)).
- **Complexity:** O(c^n)
- **Example:**
  ```cpp
  // For each element, three choices: O(3^n)
  void solve(int idx) {
      if (idx == n) return;
      for (int i = 0; i < 3; i++)
          solve(idx + 1);
  }
  ```

### 15. Factorial Time (`O(n!)`)

- **Description:** Algorithms that generate all permutations or combinations, such as brute-force solutions to the traveling salesman problem.
- **Complexity:** O(n!)
- **Example:**
  ```cpp
  void permute(vector<int>& nums, int l, int r) {
      if (l == r) return;
      for (int i = l; i <= r; i++) {
          swap(nums[l], nums[i]);
          permute(nums, l + 1, r);
          swap(nums[l], nums[i]);
      }
  }
  // O(n!)
  ```

---

### Summary Table

| Structure         | Example/Description       | Typical Complexity     |
| ----------------- | ------------------------- | ---------------------- |
| Simple Statement  | `int x = 5;`              | O(1)                   |
| Sequential        | Multiple statements       | O(1) or sum            |
| Loop              | `for (i = 0; i < n; i++)` | O(n)                   |
| Nested Loop       | Two loops over n          | O(n^2)                 |
| Conditional       | `if/else`                 | O(1) or branch content |
| Function Call     | `foo()`                   | Depends on function    |
| Recursion         | `factorial(n)`            | O(n), O(2^n), etc.     |
| Switch Statement  | `switch (x)`              | O(1) or branch content |
| Early Termination | `break`, `return` in loop | Best-case improved     |

**Key Point:**  
Always analyze the dominant code structure to determine the overall time complexity of your algorithm.
