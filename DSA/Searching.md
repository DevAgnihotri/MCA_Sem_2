# Searching and Hashing: Concepts, Techniques, and PYQs (with Answers)

---

## 1. Concept of Searching

**Searching** is the process of finding a specific element (called the target or key) in a collection of data, such as an array, list, or database. The goal is to determine whether the element exists in the collection and, if so, to find its position.

- **Why is searching important?**
  - It is a basic operation in computer science, used in databases, file systems, and many algorithms.
  - Efficient searching saves time and resources.

**Types of Searching:**

- **Linear (Sequential) Search**: Checks each element one by one.
- **Binary Search**: Efficiently searches in sorted data by repeatedly dividing the search interval in half.
- **Hashing**: Uses a hash function to directly compute the location of the target.

---

## 2. Sequential (Linear) Search

**Definition:**
Sequential search (also called linear search) is the simplest searching technique. It checks each element in the list, one by one, until the target is found or the end of the list is reached.

**How it works:**

1. Start from the first element.
2. Compare the target value with the current element.
3. If they match, return the position.
4. If not, move to the next element.
5. Repeat until the end of the list.

**Advantages:**

- Simple to implement.
- Works on both sorted and unsorted data.

**Disadvantages:**

- Slow for large lists (O(n) time complexity).

**Algorithm for Linear Search:**

```c
// Linear Search Algorithm
int linearSearch(int arr[], int n, int key) {
    for (int i = 0; i < n; i++) {
        if (arr[i] == key)
            return i; // Found at index i
    }
    return -1; // Not found
}
```

**Time Complexity:**

- Best case: O(1) (if the element is at the first position)
- Worst case: O(n) (if the element is at the last position or not present)

---

### PYQ 6.3: What is searching and sorting? Write an algorithm for linear search and binary search

**Question:**

> What is searching and sorting? Write an algorithm for linear search and binary search.

**Answer:**

- **Searching** is the process of finding a specific element in a collection of data.
- **Sorting** is the process of arranging data in a particular order (ascending or descending).

**Algorithm for Linear Search:**
(See above for code)

**Algorithm for Binary Search:**
(See below in Binary Search section)

---

## 3. Index Sequential Search

**Definition:**
Index sequential search is an improved version of sequential search. It divides the data into blocks and creates an index for each block. The index helps to quickly locate the block where the target may be, and then a sequential search is performed within that block.

**How it works:**

1. Create an index table with the highest key of each block and a pointer to the block.
2. Search the index to find the block that may contain the target.
3. Perform a sequential search within that block.

**Advantages:**

- Faster than simple sequential search for large datasets.
- Used in file systems and databases.

**Disadvantages:**

- Requires extra space for the index.
- Still slower than binary search for sorted data.

---

## 4. Binary Search

**Definition:**
Binary search is an efficient searching technique for sorted data. It repeatedly divides the search interval in half, eliminating half of the remaining elements each time.

**How it works:**

1. Start with the entire sorted array.
2. Find the middle element.
3. If the target equals the middle element, search is successful.
4. If the target is less, repeat the search on the left half.
5. If the target is greater, repeat the search on the right half.
6. Repeat until the element is found or the interval is empty.

**Algorithm for Binary Search:**

```c
// Binary Search Algorithm (Iterative)
int binarySearch(int arr[], int n, int key) {
    int low = 0, high = n - 1;
    while (low <= high) {
        int mid = (low + high) / 2;
        if (arr[mid] == key)
            return mid; // Found
        else if (arr[mid] < key)
            low = mid + 1;
        else
            high = mid - 1;
    }
    return -1; // Not found
}
```

**Time Complexity:**

- Best case: O(1)
- Worst case: O(log n)

**Comparison with Linear Search:**

- **Linear Search:** O(n) time, works on unsorted data.
- **Binary Search:** O(log n) time, but only works on sorted data.

**Table: Linear vs Binary Search**

| Feature         | Linear Search | Binary Search    |
| --------------- | ------------- | ---------------- |
| Data Order      | Any           | Sorted only      |
| Time Complexity | O(n)          | O(log n)         |
| Implementation  | Simple        | Slightly complex |
| Speed           | Slower        | Faster           |

---

### PYQ 6.2: Write an algorithm for binary search and discuss its speed compared with linear search

**Question:**

> Write an algorithm for binary search and discuss its speed compared with linear search.

**Answer:**

- **Algorithm:** (See above for code)
- **Speed Comparison:**
  - Binary search is much faster than linear search for large, sorted datasets because it reduces the search space by half each time (O(log n)), while linear search checks every element (O(n)).

---

## 5. PYQ 6.1: Write function in C, which deletes all occurrences of a given character from a given string

**Question:**

> Write function in C, which deletes all occurrences of a given character from a given string.

**Answer:**

Here is a simple C function to delete all occurrences of a given character from a string:

```c
void removeChar(char* str, char c) {
    int i = 0, j = 0;
    while (str[i]) {
        if (str[i] != c) {
            str[j++] = str[i];
        }
        i++;
    }
    str[j] = '\0';
}
```

**How it works:**

- The function uses two pointers: `i` to read the string, `j` to write the new string.
- If the current character is not the one to remove, it is copied to the new position.
- At the end, the string is properly terminated.

---

## 6. Concept of Hashing

**Hashing** is a technique used to quickly store and retrieve data using a special function called a **hash function**. The hash function converts a key (like a number or string) into an index in a table (called a hash table).

- **Why use hashing?**
  - Fast access to data (ideally O(1) time).
  - Used in databases, caches, symbol tables, etc.

**How it works:**

1. The hash function takes a key and computes an index.
2. The data is stored at that index in the hash table.
3. To search, apply the hash function to the key and go directly to the index.

**Example:**

- If the key is 123 and the table size is 10, a simple hash function could be `index = key % 10`, so 123 would be stored at index 3.

---

### PYQ 7.1: Define Hashing. Discuss various methods of collision resolution with suitable example.

**Question:**

> Define Hashing. Discuss various methods of collision resolution with suitable example.

**Answer:**

- **Hashing** is a technique to convert a given key into an index in a hash table using a hash function.
- **Collision** occurs when two keys produce the same index.
- **Collision Resolution Techniques:**
  1. **Open Addressing:**
     - If a collision occurs, find another empty slot using a probing sequence.
     - Types: Linear probing, Quadratic probing, Double hashing.
  2. **Chaining (Separate Chaining):**
     - Each index in the table points to a linked list of entries that hash to the same index.

**Example:**

- Table size = 5, keys = 10, 15, 20
- Hash function: `index = key % 5`
- 10 → 0, 15 → 0 (collision)
- With chaining, both 10 and 15 are stored in a linked list at index 0.

---

### PYQ 7.2: What do you understand by hashing? What are the different hashing techniques? Discuss different techniques to resolve collision once it is occurred during hashing.

**Question:**

> What do you understand by hashing? What are the different hashing techniques? Discuss different techniques to resolve collision once it is occurred during hashing.

**Answer:**

- **Hashing** is a method to map data of arbitrary size to fixed-size values (indices) using a hash function.
- **Hashing Techniques:**
    1. **Division Method:** `index = key % table_size`  
         *Example:* key = 27, table_size = 10 → index = 27 % 10 = 7
    2. **Multiplication Method:** `index = floor(table_size * (key * A % 1))`, where 0 < A < 1  
         *Example:* key = 27, table_size = 10, A = 0.618 → index = floor(10 * (27 * 0.618 % 1)) ≈ floor(10 * 0.686) = 6
    3. **Mid-square Method:** Square the key and use the middle digits as the index.  
         *Example:* key = 27 → 27² = 729, middle digit is 2 (if table_size = 10) → index = 2
    4. **Folding Method:** Break the key into parts, add them, and use the sum as the index.  
         *Example:* key = 123456, parts = 123 + 456 = 579, table_size = 10 → index = 579 % 10 = 9
- **Collision Resolution:**
    - **Open Addressing:** Linear, quadratic, double hashing.  
        *Example (Linear Probing):* If index 7 is occupied, try 8, then 9, etc.
    - **Chaining:** Use linked lists at each index.  
        *Example:* If both keys 27 and 37 hash to index 7, both are stored in a linked list at index 7.

---

### PYQ 7.3: Define Hash function. Explain Collision resolution strategies. How collision is resolved using separate chaining concept?

**Question:**

> Define Hash function. Explain Collision resolution strategies. How collision is resolved using separate chaining concept?

**Answer:**

- **Hash Function:** A function that takes a key and returns an index in the hash table.
- **Collision Resolution Strategies:**
  - **Open Addressing:** Try other slots in the table.
- **Separate Chaining:**
    - When a collision occurs, all elements that hash to the same index are stored in a linked list (chain) at that index in the hash table.
    - **How it works:** Each slot in the hash table contains a pointer to the head of a linked list. When inserting a key, if the slot is empty, a new node is created. If not, the new key is added to the front (or end) of the linked list at that slot.
    - **Example:**  
        Suppose the hash table size is 5 and the hash function is `index = key % 5`.  
        - Insert key 10: `10 % 5 = 0` → index 0 is empty, so insert 10 at index 0.
        - Insert key 15: `15 % 5 = 0` → index 0 already has 10, so add 15 to the linked list at index 0.
        - Insert key 7: `7 % 5 = 2` → index 2 is empty, insert 7 at index 2.
        - Insert key 20: `20 % 5 = 0` → index 0 already has 10 and 15, so add 20 to the linked list at index 0.

        The hash table will look like:
        - Index 0: 20 → 15 → 10 (linked list)
        - Index 1: NULL
        - Index 2: 7
        - Index 3: NULL
        - Index 4: NULL

    - **Advantage:** Separate chaining handles collisions efficiently and allows the table to store more elements than its size, as each slot can grow as needed.

---

### PYQ 7.4: Define hashing. What are the properties of a good hash function? With necessary examples explain four different hashing techniques.

**Question:**

> Define hashing. What are the properties of a good hash function? With necessary examples explain four different hashing techniques.

**Answer:**

- **Hashing:** See above.
- **Properties of a Good Hash Function:**
  1. **Uniform Distribution:** Should distribute keys evenly across the table.
  2. **Deterministic:** Same key always produces the same index.
  3. **Fast to Compute:** Should be quick to calculate.
  4. **Minimize Collisions:** Should avoid mapping different keys to the same index.
- **Examples of Hashing Techniques:**
  1. **Division Method:** `index = key % table_size` (e.g., key=123, table_size=10 → index=3)
  2. **Multiplication Method:** `index = floor(table_size * (key * A % 1))` (e.g., key=123, A=0.618, table_size=10)
  3. **Mid-square Method:** Square the key, extract middle digits (e.g., key=123 → 123\*123=15129, use 3 middle digits)
  4. **Folding Method:** Break key into parts, add them (e.g., key=123456, parts=123+456=579, index=579%table_size)

---

## 7. Collision Resolution Techniques in Hashing

When two keys hash to the same index, a **collision** occurs. There are several ways to resolve collisions:

### 1. Open Addressing

- **Linear Probing:** Check the next slot (index+1, index+2, ...) until an empty slot is found.
- **Quadratic Probing:** Check slots at intervals of 1^2, 2^2, 3^2, etc.
- **Double Hashing:** Use a second hash function to decide the step size.

### 2. Chaining (Separate Chaining)

- Each slot in the hash table points to a linked list of entries.
- All elements that hash to the same index are stored in the list.

**Table: Collision Resolution Methods**

| Method            | How it Works                       | Example               |
| ----------------- | ---------------------------------- | --------------------- |
| Linear Probing    | Next available slot                | 10→0, 15→1, 20→2      |
| Quadratic Probing | Next slot by i^2 steps             | 10→0, 15→1, 20→4      |
| Double Hashing    | Next slot by another hash function | 10→0, 15→h2(15), ...  |
| Chaining          | Linked list at each index          | 10,15 at index 0 list |

---

## 8. Summary Table: Searching and Hashing

| Topic     | Key Points                           |
| --------- | ------------------------------------ |
| Searching | Linear, Binary, Index Sequential     |
| Hashing   | Hash function, Collision, Resolution |
| Collision | Open Addressing, Chaining            |

---

# End of Notes
