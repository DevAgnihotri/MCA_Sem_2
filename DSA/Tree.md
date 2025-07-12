
## Topics Covered in This Guide

This guide provides a comprehensive overview of tree data structures, focusing on binary trees and their variants. Below is a list of the main topics covered, each linked to its section for easy navigation:

- [Introduction to Trees](#introduction-to-trees)
- [Basic Terminology Used with Tree](#basic-terminology-used-with-tree)
- [Binary Trees](#binary-trees)
- [Binary Tree Representation](#binary-tree-representation)
- [Binary Search Tree (BST)](#binary-search-tree-bst)
- [AVL Trees](#avl-trees)
- [Complete Binary Tree](#complete-binary-tree)
- [Summary Table: Tree Types Comparison](#summary-table-tree-types-comparison)
- [Tree Traversal Algorithms](#tree-traversal-algorithms)
- [Constructing Binary Tree from Given Tree Traversal](#constructing-binary-tree-from-given-tree-traversal)
- [Operations in Binary Search Tree](#operations-in-binary-search-tree)
- [Threaded Binary Trees](#threaded-binary-trees)
- [Collective Topic: B-Trees and B+ Trees](#collective-topic-b-trees-and-b-trees)
- [Huffman Coding Using Binary Tree](#huffman-coding-using-binary-tree)

---


# Tree Data Structure: Complete Guide

---

## Introduction to Trees

A **tree** is a hierarchical data structure that consists of nodes connected by edges. It is a non-linear data structure that resembles an upside-down tree with a root at the top and leaves at the bottom.

---

## Basic Terminology Used with Tree

### Key Terms and Definitions

| Term                     | Definition                                                       | Example                       |
| ------------------------ | ---------------------------------------------------------------- | ----------------------------- |
| **Node**                 | Fundamental unit of a tree containing data and links to children | Each circle in a tree diagram |
| **Root**                 | The topmost node with no parent                                  | Starting point of the tree    |
| **Parent**               | A node that has one or more children                             | Node above another node       |
| **Child**                | A node that descends from a parent node                          | Node below another node       |
| **Leaf (External Node)** | A node with no children                                          | End nodes of the tree         |
| **Internal Node**        | A node with at least one child                                   | Any non-leaf node             |
| **Edge**                 | A connection between two nodes                                   | Line connecting nodes         |
| **Path**                 | Sequence of nodes connected by edges                             | Route from root to a leaf     |
| **Height of Tree**       | Length of the longest path from root to any leaf                 | Maximum depth of the tree     |
| **Depth of Node**        | Number of edges from root to that node                           | Distance from root            |
| **Level**                | All nodes at the same depth                                      | Horizontal layer in the tree  |
| **Degree**               | Number of children a node has                                    | Branching factor              |
| **Subtree**              | A tree formed by a node and all its descendants                  | Portion of the tree           |

### Tree Properties

- **Number of edges** = Number of nodes - 1
- **Maximum nodes at level i** = 2^i (for binary trees)
- **Maximum nodes in tree of height h** = 2^(h+1) - 1

### Visual Example:

```
        A (Root, Level 0)
       / \
      B   C (Level 1)
     / \   \
    D   E   F (Level 2, Leaves)
```

---

## Binary Trees

### Definition

A **binary tree** is a tree data structure where each node has at most two children, referred to as the **left child** and **right child**.

### Types of Binary Trees

| Type                         | Description                                                                | Characteristics                   |
| ---------------------------- | -------------------------------------------------------------------------- | --------------------------------- |
| **Full Binary Tree**         | Every node has either 0 or 2 children                                      | No node has only 1 child          |
| **Complete Binary Tree**     | All levels filled except possibly the last, which is filled left to right  | Efficient for heap implementation |
| **Perfect Binary Tree**      | All internal nodes have 2 children, all leaves are at the same level       | Most balanced form                |
| **Balanced Binary Tree**     | Height difference between left and right subtrees of any node is at most 1 | Good for search operations        |
| **Degenerate (Skewed) Tree** | Each parent has only one child                                             | Essentially a linked list         |

#### Detailed Definitions

- **Full Binary Tree**:  
   A binary tree in which every node has either 0 or 2 children. No node in a full binary tree has only one child. All leaves are at the same or different levels, but every internal node must have exactly two children.

- **Complete Binary Tree**:  
   A binary tree in which all levels are completely filled except possibly the last level, which is filled from left to right. This structure allows efficient array representation and is used in heap implementations.

- **Perfect Binary Tree**:  
   A binary tree in which all internal nodes have exactly two children and all leaves are at the same level. Every level is completely filled, making it the most balanced type of binary tree.

- **Balanced Binary Tree**:  
   A binary tree where the height difference between the left and right subtrees of any node is at most one. This property ensures that operations like search, insertion, and deletion can be performed efficiently (in O(log n) time).

- **Degenerate (Skewed) Tree**:  
   A binary tree where each parent node has only one child, making the tree behave like a linked list. This structure leads to the worst-case performance for binary tree operations (O(n) time).

### Binary Tree Properties

- **Maximum nodes at level i**: 2^i
- **Maximum nodes in tree of height h**: 2^(h+1) - 1
- **Minimum height for n nodes**: ⌊log₂(n)⌋
- **Maximum height for n nodes**: n - 1

---

## Binary Tree Representation

### 1. Array Representation

In array representation, nodes are stored in an array where:

- **Root** is stored at index 0 (or 1)
- For node at index i:
  - **Left child** at index 2i + 1 (or 2i if 1-indexed)
  - **Right child** at index 2i + 2 (or 2i + 1 if 1-indexed)
  - **Parent** at index (i-1)/2 (or i/2 if 1-indexed)

#### Example:

```
Tree:       1
          /   \
         2     3
        / \   /
       4   5 6

Array: [1, 2, 3, 4, 5, 6]
Index:  0  1  2  3  4  5
```

#### Advantages and Disadvantages:

| Advantages             | Disadvantages                          |
| ---------------------- | -------------------------------------- |
| ✓ Simple indexing      | ✗ Wastes memory for skewed trees       |
| ✓ No pointers required | ✗ Fixed size (array must be pre-sized) |
| ✓ Cache friendly       | ✗ Insertion/deletion is complex        |

### 2. Pointer (Linked List) Representation

Each node contains data and pointers to left and right children.

#### Advantages and Disadvantages:

| Advantages                | Disadvantages                      |
| ------------------------- | ---------------------------------- |
| ✓ Dynamic size            | ✗ Extra memory needed for pointers |
| ✓ No memory wasted        | ✗ Less cache friendly              |
| ✓ Easy insertion/deletion | ✗ Implementation is more complex   |

### Table Representation: Left and Right Child for Each Node

A binary tree can be represented in a table where each row lists a node and the values of its left and right children. This is useful for visualizing the structure and relationships between nodes.

#### Example Tree

```
    1
     / \
    2   3
   / \   \
  4   5   6
```

#### Table Representation

| Node | Left Child | Right Child |
| ---- | ---------- | ----------- |
| 1    | 2          | 3           |
| 2    | 4          | 5           |
| 3    | -          | 6           |
| 4    | -          | -           |
| 5    | -          | -           |
| 6    | -          | -           |

- If a node does not have a left or right child, a dash (`-`) is used to indicate absence.

---

## Binary Search Tree (BST)

### Q2. What is a binary search tree? Write an algorithm to implement recursive or iterative search for a binary search tree.

### Definition

A **Binary Search Tree (BST)** is a binary tree with the following properties:

- All nodes in the left subtree have values less than the root
- All nodes in the right subtree have values greater than the root
- Both left and right subtrees are also BSTs

### Algorithm: Search in a Binary Search Tree (BST)

#### Recursive Search Algorithm (Pseudocode)

```
Algorithm BST_Search(root, key)
Input: root - pointer to the root node of BST
    key  - value to search for
Output: pointer to the node containing key, or NULL if not found

1. If root is NULL
      return NULL
2. If root.data == key
      return root
3. If key < root.data
      return BST_Search(root.left, key)
4. Else
      return BST_Search(root.right, key)
```

#### Time Complexity:

- **Best/Average Case**: O(log n)
- **Worst Case**: O(n) for skewed tree
- **Space Complexity**: O(log n) for recursive, O(1) for iterative

---

### Q5. Discuss the basic properties of a Binary Search Tree.

#### Basic Properties of BST:

1. **Ordering Property**:

   - Left subtree contains only nodes with values less than the parent
   - Right subtree contains only nodes with values greater than the parent

2. **Unique Values**: Typically, no duplicate values are allowed

3. **Recursive Structure**: Each subtree is also a valid BST

4. **In-order Traversal**: Gives sorted sequence of elements

5. **Search Efficiency**: Average case O(log n) search time

6. **Dynamic Operations**: Supports insertion, deletion, and search operations

#### Benefits:

- Fast search, insertion, and deletion operations
- Maintains sorted order automatically
- No need for pre-sorting
- Efficient range queries

#### Limitations:

- Can become unbalanced (degenerate into linked list)
- Worst-case performance is O(n)
- No guarantee of balance without additional constraints

---

### Q3. Write down a recursive algorithm to insert a node in a binary search tree. Apply that algorithm to construct a BST with the given data: 8, 5, 12, 67, 43, 23, 6, 3, 2, 8, 24, 21, 20

#### Recursive Insertion Algorithm (Step-by-Step):

1. **If the tree is empty:**

   - Create a new node with the given value and return it as the root.

2. **If the value to insert is less than the current node's value:**

   - Recursively insert the value into the left subtree.

3. **If the value to insert is greater than the current node's value:**

   - Recursively insert the value into the right subtree.

4. **If the value is equal to the current node's value:**

   - Do not insert (to avoid duplicates).

5. **Return the (possibly updated) root node.**

---

#### Step-by-Step Construction with given data: 8, 5, 12, 67, 43, 23, 6, 3, 2, 8, 24, 21, 20

**Step 1: Insert 8 (becomes root)**

```
    8
```

**Step 2: Insert 5 (5 < 8, goes left)**

```
    8
   /
  5
```

**Step 3: Insert 12 (12 > 8, goes right)**

```
    8
   / \
  5   12
```

**Step 4: Insert 67 (67 > 8, > 12, goes right of 12)**

```
    8
   / \
  5   12
        \
         67
```

**Step 5: Insert 43 (43 > 8, > 12, < 67, goes left of 67)**

```
    8
   / \
  5   12
        \
         67
        /
       43
```

**Step 6: Insert 23 (23 > 8, > 12, < 67, < 43, goes left of 43)**

```
    8
   / \
  5   12
        \
         67
        /
       43
      /
     23
```

**Step 7: Insert 6 (6 < 8, > 5, goes right of 5)**

```
    8
   / \
  5   12
   \    \
    6    67
        /
       43
      /
     23
```

**Step 8: Insert 3 (3 < 8, < 5, goes left of 5)**

```
    8
   / \
  5   12
 / \    \
3   6    67
        /
       43
      /
     23
```

**Step 9: Insert 2 (2 < 8, < 5, < 3, goes left of 3)**

```
    8
   / \
  5   12
 / \    \
3   6    67
/       /
2      43
      /
     23
```

**Step 10: Insert 8 (duplicate, not inserted)**

**Step 11: Insert 24 (24 > 8, > 12, < 67, < 43, > 23, goes right of 23)**

```
    8
   / \
  5   12
        \
         67
        /
       43
      /
     23
      \
       24
```

**Step 12: Insert 21 (21 > 8, > 12, < 67, < 43, < 23, goes left of 23)**

```
    8
   / \
  5   12
        \
         67
        /
       43
      /
     23
    / \
   21  24
```

**Step 13: Insert 20 (20 > 8, > 12, < 67, < 43, < 23, < 21, goes left of 21)**

```
Final BST:
    8
   / \
  5   12
        \
         67
        /
       43
      /
     23
    / \
   21  24
  /
 20
```

---

### Q6. Explain the successor of a node in a Binary Search Tree.

#### Definition

The **successor** of a node in a BST is the node with the smallest value greater than the given node's value. In other words, it's the next node in the in-order traversal.

#### Two Cases:

**Case 1: Node has right subtree**

- Successor is the leftmost node in the right subtree

**Case 2: Node has no right subtree**

- Successor is the lowest ancestor whose left child is also an ancestor of the node

#### Example:

```
    20
   /  \
  10   30
 / \   / \
5  15 25 40

Successor of 10 = 15 (leftmost in right subtree)
Successor of 15 = 20 (lowest ancestor)
Successor of 25 = 30 (lowest ancestor)
```

---

## AVL Trees

### Q What is an AVL Tree?

An **AVL tree** is a special type of self-balancing binary search tree (BST). It was named after its inventors Adelson-Velsky and Landis. In an AVL tree, the heights of the left and right subtrees of every node differ by at most one. This property ensures that the tree remains approximately balanced, which keeps operations like search, insert, and delete efficient (O(log n) time).

#### Key Points:
- **Self-balancing:** The tree automatically keeps itself balanced after every insertion or deletion.
- **Binary Search Tree:** It follows all BST properties.
- **Height-balanced:** The difference in height between left and right subtrees (called the balancing factor) is always -1, 0, or +1 for every node.

---

### Q What is the Balancing Factor?

The **balancing factor** of a node in an AVL tree is calculated as:

```
Balancing Factor = Height of Left Subtree - Height of Right Subtree
```

- If the balancing factor is **-1, 0, or +1**, the node is balanced.
- If it becomes less than -1 or greater than +1, the tree needs to be rebalanced.

---

### Q Balancing Methods in AVL Trees

When an insertion or deletion causes the balancing factor of a node to become less than -1 or greater than +1, the tree must be rebalanced. This is done using **rotations**.

#### Types of Rotations

There are four possible cases:

1. **Left-Left (LL) Case:**  
    - Insertion in the left subtree of the left child.
    - **Solution:** Right rotation.

2. **Right-Right (RR) Case:**  
    - Insertion in the right subtree of the right child.
    - **Solution:** Left rotation.

3. **Left-Right (LR) Case:**  
    - Insertion in the right subtree of the left child.
    - **Solution:** Left rotation on left child, then right rotation on node.

4. **Right-Left (RL) Case:**  
    - Insertion in the left subtree of the right child.
    - **Solution:** Right rotation on right child, then left rotation on node.

#### Visual Examples

**1. LL Case (Right Rotation):**

```
Before:
     30
    /
 20
 /
10

Insert 10 causes imbalance at 30 (BF = 2)

After right rotation at 30:
    20
  /  \
10   30
```

**2. RR Case (Left Rotation):**

```
Before:
10
  \
  20
     \
     30

Insert 30 causes imbalance at 10 (BF = -2)

After left rotation at 10:
    20
  /  \
10   30
```

**3. LR Case (Left-Right Rotation):**

```
Before:
     30
    /
 20
    \
    25

Insert 25 causes imbalance at 30 (BF = 2)

Step 1: Left rotation at 20
     30
    /
 25
 /
20

Step 2: Right rotation at 30
    25
  /  \
20   30
```

**4. RL Case (Right-Left Rotation):**

```
Before:
10
  \
  30
  /
20

Insert 20 causes imbalance at 10 (BF = -2)

Step 1: Right rotation at 30
10
  \
 20
    \
    30

Step 2: Left rotation at 10
    20
  /  \
10   30
```

---

### Summary Table: AVL Tree Rotations

| Case | Where Insertion Occurs         | Rotation(s) Needed         |
|------|-------------------------------|---------------------------|
| LL   | Left of left child            | Right rotation            |
| RR   | Right of right child          | Left rotation             |
| LR   | Right of left child           | Left, then right rotation |
| RL   | Left of right child           | Right, then left rotation |

---

### Key Points

- **AVL trees** are always balanced, so operations are fast.
- **Balancing factor** helps detect imbalance.
- **Rotations** restore balance after insertions or deletions.
- **Balanced binary trees** (like AVL) are crucial for efficient data structures.

---

## Complete Binary Tree

### Q7. Differentiate between a Binary Tree and a Complete Binary Tree.

### Q8. Explain Complete Binary Tree and Extended Binary Tree.

### Binary Tree vs Complete Binary Tree

| Aspect                   | Binary Tree                                                      | Complete Binary Tree                                                                                              |
| ------------------------ | ---------------------------------------------------------------- | ----------------------------------------------------------------------------------------------------------------- |
| **Definition**           | A tree in which each node has at most 2 children                 | A binary tree where all levels are completely filled except possibly the last, which is filled from left to right |
| **Structure**            | Nodes can be arranged in any shape (may be skewed or unbalanced) | Nodes are arranged to fill each level before moving to the next, ensuring compactness                             |
| **Array Representation** | May result in wasted space due to gaps for missing children      | Very efficient; nodes are stored in contiguous array positions without gaps                                       |
| **Height**               | Can be unbalanced; height may be as large as the number of nodes | More balanced; height is minimized for the number of nodes                                                        |
| **Completeness**         | No requirement for completeness                                  | Must be complete except possibly the last level, which is filled left to right                                    |
| **Insertion Order**      | No specific order required                                       | Insertions always occur at the leftmost available position at the lowest level                                    |
| **Traversal**            | Traversal order and structure can vary widely                    | Traversal order is more predictable due to compact structure                                                      |
| **Applications**         | Used for general tree operations, expression trees, etc.         | Used in heaps, priority queues, and situations requiring efficient array storage                                  |
| **Efficiency**           | May be inefficient for some operations if unbalanced             | Efficient for operations like heapify, due to predictable structure                                               |
| **Examples**             | Any binary tree, including skewed or sparse trees                | Heap trees, complete levels except possibly the last                                                              |

### Complete Binary Tree

#### Definition

A **Complete Binary Tree** is a binary tree in which:

- All levels are completely filled except possibly the last level
- The last level is filled from left to right
- No gaps between nodes

#### Properties:

- **Height**: ⌊log₂(n)⌋ where n is number of nodes
- **Efficient array representation**: No wasted space
- **Parent-child relationship**: Easy to calculate using array indices

#### Examples:

**Complete Binary Tree:**

```
    1
   / \
  2   3
 / \ /
4  5 6
```

**Not Complete Binary Tree:**

```
    1
   / \
  2   3
 /   / \
4   6   7
```

#### Array Representation:

```
Complete Tree: [1, 2, 3, 4, 5, 6]
Indices:       [0, 1, 2, 3, 4, 5]

For node at index i:
- Left child: 2i + 1
- Right child: 2i + 2
- Parent: (i-1)/2
```

### Extended Binary Tree

#### Definition

An **Extended Binary Tree** (also called **Full Binary Tree**) is a binary tree where:

- Every node has either 0 or 2 children
- No node has exactly 1 child
- All internal nodes have degree 2

#### Properties:

- **Number of leaves** = Number of internal nodes + 1
- **Total nodes** = 2 × leaves - 1
- **Minimum height** for n leaves = ⌈log₂(n)⌉

#### Example:

```
Extended Binary Tree:
    A
   / \
  B   C
     / \
    D   E

A, C are internal nodes (degree 2)
B, D, E are leaves (degree 0)
```

#### Applications:

- Expression trees
- Huffman coding trees
- Decision trees

---

## Summary Table: Tree Types Comparison

| Tree Type                    | Key Characteristics                                          | Common Use Cases                               | Time Complexity (Search/Insert/Delete) |
| ---------------------------- | ------------------------------------------------------------ | ---------------------------------------------- | -------------------------------------- |
| **Binary Tree**              | Each node has at most 2 children                             | General hierarchical data, parsing expressions | Varies (depends on shape)              |
| **Binary Search Tree (BST)** | Left subtree < root < right subtree; no duplicates           | Searching, dynamic sorting, dictionaries       | O(log n) average, O(n) worst           |
| **Complete Binary Tree**     | All levels filled except possibly last, filled left to right | Heaps, priority queues, array-based trees      | O(log n)                               |
| **Extended Binary Tree**     | Every node has either 0 or 2 children (full binary tree)     | Expression trees, Huffman coding               | Varies                                 |

---

## Tree Traversal Algorithms

### Q2. Short note on tree traversal.

### Introduction to Tree Traversal

**Tree traversal** is the process of visiting each node in a tree data structure exactly once in a systematic way. Unlike linear data structures (arrays, linked lists), trees can be traversed in multiple ways due to their hierarchical nature.

#### Why Tree Traversal is Important:

- **Data Processing**: Apply operations to all nodes
- **Search Operations**: Find specific elements
- **Tree Analysis**: Calculate properties like height, size
- **Expression Evaluation**: Process mathematical expressions
- **File System Operations**: Navigate directory structures

#### Types of Tree Traversal:

Tree traversals are broadly classified into two categories:

1. **Depth-First Search (DFS) Traversals**:

   - Inorder Traversal
   - Preorder Traversal
   - Postorder Traversal

2. **Breadth-First Search (BFS) Traversal**:
   - Level Order Traversal

---

### Q. Give static and dynamic memory representation of a binary tree. (Simple English & Complete Detail)

#### 1. Static Memory Representation (Array Representation)

**What is it?**  
In static representation, the binary tree is stored in a fixed-size array. Each node is placed at a specific index, and the relationships between parent and child nodes are determined by their positions in the array.

**How does it work?**

- The root node is stored at index 0 (or 1, depending on convention).
- For a node at index `i`:
  - **Left child** is at index `2i + 1` (if 0-based) or `2i` (if 1-based).
  - **Right child** is at index `2i + 2` (if 0-based) or `2i + 1` (if 1-based).
  - **Parent** is at index `(i - 1) / 2` (if 0-based) or `i / 2` (if 1-based).

**Example:**

Suppose we have this tree:

```
        1
     / \
    2   3
 / \
4   5
```

Array representation (0-based): `[1, 2, 3, 4, 5]`

| Index | Value | Parent | Left Child | Right Child |
| ----- | ----- | ------ | ---------- | ----------- |
| 0     | 1     | -      | 1          | 2           |
| 1     | 2     | 0      | 3          | 4           |
| 2     | 3     | 0      | -          | -           |
| 3     | 4     | 1      | -          | -           |
| 4     | 5     | 1      | -          | -           |

**Advantages:**

- Simple and fast access using indices.
- Good for complete or nearly complete trees.

**Disadvantages:**

- Wastes memory for sparse or skewed trees (many empty spots).
- Fixed size; cannot easily grow or shrink.

---

#### 2. Dynamic Memory Representation (Linked Structure)

**What is it?**  
In dynamic representation, each node is created as needed using pointers (links). Each node contains data and pointers to its left and right children.

**How does it work?**

- Each node is a structure (or class) with:
  - Data field (stores value)
  - Pointer to left child
  - Pointer to right child

**C Structure Example:**

```c
struct TreeNode {
        int data;
        struct TreeNode* left;
        struct TreeNode* right;
};
```

**Creating a Node:**

```c
struct TreeNode* createNode(int value) {
        struct TreeNode* node = (struct TreeNode*)malloc(sizeof(struct TreeNode));
        node->data = value;
        node->left = NULL;
        node->right = NULL;
        return node;
}
```

**Advantages:**

- Uses memory only for existing nodes (no wasted space).
- Tree can grow or shrink as needed.
- Suitable for any tree shape (balanced, skewed, sparse).

**Disadvantages:**

- Requires extra memory for pointers.
- Accessing nodes is slower than array indexing.
- More complex to implement.

---

#### **Summary Table**

| Representation  | How It Works               | Memory Usage      | Best For                | Drawbacks                   |
| --------------- | -------------------------- | ----------------- | ----------------------- | --------------------------- |
| Static (Array)  | Uses array indices         | Fixed, may waste  | Complete/near-complete  | Wastes space for sparse     |
| Dynamic (Links) | Uses pointers for children | Flexible, minimal | Any tree shape, dynamic | Extra pointer memory needed |

---

**In short:**

- **Static (array):** Fast, simple, but wastes space for uneven trees.
- **Dynamic (linked):** Flexible, memory-efficient, but needs pointers and is a bit slower to access.

### Q1. Write recursive algorithms for Pre-Order, Post-Order, and In-Order traversals of a binary tree.

### Detailed Tree Traversal Algorithms

#### 1. Inorder Traversal (Left → Root → Right)

**Definition**: In inorder traversal, we visit the left subtree first, then the root node, and finally the right subtree.

**Algorithm Steps**:

1. Traverse the left subtree recursively
2. Visit the root node
3. Traverse the right subtree recursively

**Recursive Algorithm**:

```c
void inorderTraversal(struct TreeNode* root) {
    if (root != NULL) {
        inorderTraversal(root->left);   // Visit left subtree
        printf("%d ", root->data);      // Visit root
        inorderTraversal(root->right);  // Visit right subtree
    }
}
```

**Special Property**: For Binary Search Trees (BST), inorder traversal gives nodes in **sorted ascending order**.

**Example**:

```
Tree:       1
          /   \
         2     3
        / \
       4   5

Inorder: 4 → 2 → 5 → 1 → 3
```

#### 2. Preorder Traversal (Root → Left → Right)

**Definition**: In preorder traversal, we visit the root node first, then the left subtree, and finally the right subtree.

**Algorithm Steps**:

1. Visit the root node
2. Traverse the left subtree recursively
3. Traverse the right subtree recursively

**Recursive Algorithm**:

```c
void preorderTraversal(struct TreeNode* root) {
    if (root != NULL) {
        printf("%d ", root->data);      // Visit root
        preorderTraversal(root->left);  // Visit left subtree
        preorderTraversal(root->right); // Visit right subtree
    }
}
```

**Special Property**: Preorder traversal is useful for **copying** or **creating a copy** of the tree, as it processes the root before its children.

**Example**:

```
Tree:       1
          /   \
         2     3
        / \
       4   5

Preorder: 1 → 2 → 4 → 5 → 3
```

#### 3. Postorder Traversal (Left → Right → Root)

**Definition**: In postorder traversal, we visit the left subtree first, then the right subtree, and finally the root node.

**Algorithm Steps**:

1. Traverse the left subtree recursively
2. Traverse the right subtree recursively
3. Visit the root node

**Recursive Algorithm**:

```c
void postorderTraversal(struct TreeNode* root) {
    if (root != NULL) {
        postorderTraversal(root->left);  // Visit left subtree
        postorderTraversal(root->right); // Visit right subtree
        printf("%d ", root->data);       // Visit root
    }
}
```

**Special Property**: Postorder traversal is useful for **deleting** trees or **calculating folder sizes**, as it processes children before the parent.

**Example**:

```
Tree:       1
          /   \
         2     3
        / \
       4   5

Postorder: 4 → 5 → 2 → 3 → 1
```

### Comparison of Traversal Methods

| Traversal Type | Order               | Best Use Case                   | Memory Usage           |
| -------------- | ------------------- | ------------------------------- | ---------------------- |
| **Inorder**    | Left → Root → Right | Getting sorted data from BST    | O(h) where h is height |
| **Preorder**   | Root → Left → Right | Copying/creating tree structure | O(h) where h is height |
| **Postorder**  | Left → Right → Root | Deleting tree/calculating sizes | O(h) where h is height |

### Complete Example with All Traversals

**Given Tree**:

```
        A
       / \
      B   C
     / \   \
    D   E   F
```

**Traversal Results**:

- **Inorder**: D → B → E → A → C → F
- **Preorder**: A → B → D → E → C → F
- **Postorder**: D → E → B → F → C → A

### Time and Space Complexity

| Aspect               | Complexity | Explanation                                            |
| -------------------- | ---------- | ------------------------------------------------------ |
| **Time Complexity**  | O(n)       | Each node is visited exactly once                      |
| **Space Complexity** | O(h)       | Recursive call stack uses space proportional to height |
| **Best Case Space**  | O(log n)   | For balanced tree                                      |
| **Worst Case Space** | O(n)       | For skewed tree                                        |

---

## Constructing Binary Tree from Given Tree Traversal

### Understanding Tree Construction

**Constructing a binary tree from traversal sequences** is the process of rebuilding the original tree structure using the output of tree traversal algorithms.

### Important Rules for Tree Construction

#### Single Traversal Limitation

- **Cannot construct unique tree** from only one traversal sequence
- Multiple different trees can produce the same traversal output

#### Two Traversal Combinations

1. **Inorder + Preorder** → Can construct unique tree
2. **Inorder + Postorder** → Can construct unique tree
3. **Preorder + Postorder** → Cannot always construct unique tree (except for full binary trees)

### Algorithm: Construct Tree from Inorder + Preorder

#### Step-by-Step Process:

1. **First element of preorder** is always the root
2. **Find root in inorder** to separate left and right subtrees
3. **Recursively construct** left and right subtrees

#### Example Construction:

**Given**:

- Inorder: [4, 2, 5, 1, 3]
- Preorder: [1, 2, 4, 5, 3]

**Step-by-Step Construction**:

**Step 1**: Root is 1 (first in preorder)

```
    1
```

**Step 2**: Find 1 in inorder [4, 2, 5, 1, 3]

- Left subtree: [4, 2, 5]
- Right subtree: [3]

**Step 3**: For left subtree [4, 2, 5], next in preorder is 2

```
    1
   /
  2
```

**Step 4**: Find 2 in [4, 2, 5]

- Left of 2: [4]
- Right of 2: [5]

**Step 5**: Continue recursively

```
Final Tree:
    1
   / \
  2   3
 / \
4   5
```

#### C Algorithm Implementation:

```c
int findIndex(int arr[], int start, int end, int value) {
    for (int i = start; i <= end; i++) {
        if (arr[i] == value)
            return i;
    }
    return -1;
}

struct TreeNode* buildTreeHelper(int inorder[], int preorder[],
                                int inStart, int inEnd, int* preIndex) {
    if (inStart > inEnd)
        return NULL;

    // Create root node from current preorder element
    struct TreeNode* root = createNode(preorder[(*preIndex)++]);

    // If this is the only node, return it
    if (inStart == inEnd)
        return root;

    // Find root in inorder array
    int inIndex = findIndex(inorder, inStart, inEnd, root->data);

    // Recursively build left and right subtrees
    root->left = buildTreeHelper(inorder, preorder, inStart, inIndex - 1, preIndex);
    root->right = buildTreeHelper(inorder, preorder, inIndex + 1, inEnd, preIndex);

    return root;
}

struct TreeNode* buildTree(int inorder[], int preorder[], int size) {
    int preIndex = 0;
    return buildTreeHelper(inorder, preorder, 0, size - 1, &preIndex);
}
```

---

## Operations in Binary Search Tree

### Overview of BST Operations

Binary Search Trees support several fundamental operations that maintain the BST property while providing efficient access to data.

#### Core Operations:

1. **Searching** - Find a specific value
2. **Insertion** - Add a new node
3. **Deletion** - Remove a node
4. **Modification** - Update node data

### 1. Searching Operation

**Already covered in previous sections** - refer to Q2 for detailed search algorithms.

**Quick Review**:

- **Time Complexity**: O(log n) average, O(n) worst case
- **Space Complexity**: O(log n) recursive, O(1) iterative

### 2. Insertion Operation

**Already covered in previous sections** - refer to Q3 for detailed insertion algorithm.

**Quick Review**:

- **Algorithm**: Compare with root, go left if smaller, right if larger
- **Time Complexity**: O(log n) average, O(n) worst case

### 3. Deletion Operation

**Deletion** is the most complex operation in BST due to three different cases.

#### Three Cases of Deletion:

**Case 1: Node with No Children (Leaf Node)**

- Simply remove the node
- Update parent's pointer to NULL

**Case 2: Node with One Child**

- Replace node with its child
- Update parent's pointer to point to the child

**Case 3: Node with Two Children**

- Find inorder successor (or predecessor)
- Replace node's data with successor's data
- Delete the successor

#### Deletion Algorithm (Step-by-Step):

1. **Search for the node** to be deleted (let’s call it `target`).
2. **If `target` is not found**, do nothing (or return the unchanged tree).
3. **If `target` has no children** (leaf node):
   - Remove `target` from the tree by setting its parent’s pointer to `NULL`.
4. **If `target` has one child**:
   - Replace `target` with its child (connect parent of `target` directly to the child).
5. **If `target` has two children**:
   - Find the inorder successor (smallest node in the right subtree) or inorder predecessor (largest node in the left subtree).
   - Copy the successor’s (or predecessor’s) value to `target`.
   - Recursively delete the successor (or predecessor) node, which will now have at most one child.
6. **Return the (possibly updated) root** of the tree.

**Note:** Always ensure the BST property is maintained after deletion.

#### Detailed Example of Deletion:

**Initial BST**:

```
    50
   /  \
  30   70
 / \   / \
20 40 60 80
```

**Case 1: Delete 20 (leaf node)**

```
    50
   /  \
  30   70
   \   / \
   40 60 80
```

**Case 2: Delete 30 (one child)**

```
    50
   /  \
  40   70
      / \
     60 80
```

**Case 3: Delete 50 (two children)**

```
    60  (successor of 50)
   /  \
  40   70
        \
        80
```

### 4. Modification Operation

**Modification** involves changing the data of an existing node. However, in BST, direct modification can violate the BST property.

#### Safe Modification Approaches:

**Method 1: Delete and Re-insert**

```c
struct TreeNode* modifyNode(struct TreeNode* root, int oldValue, int newValue) {
    // Delete the old value
    root = deleteNode(root, oldValue);
    // Insert the new value
    root = insert(root, newValue);
    return root;
}
```

**Method 2: Check BST Property Before Modification**

```c
bool canModify(struct TreeNode* node, int newValue) {
    // Check if modification maintains BST property
    if (node->left && node->left->data >= newValue)
        return false;
    if (node->right && node->right->data <= newValue)
        return false;
    return true;
}

bool modifyNodeSafe(struct TreeNode* root, int oldValue, int newValue) {
    struct TreeNode* node = searchIterative(root, oldValue);
    if (node && canModify(node, newValue)) {
        node->data = newValue;
        return true;
    }
    return false;
}
```

---

### Q3. Discuss the concept of inorder successor and inorder predecessor in a Binary Search Tree.

### Inorder Successor and Predecessor

#### Definitions

**Inorder Successor**: The node with the smallest value greater than the given node's value. It's the next node in the inorder traversal sequence.

**Inorder Predecessor**: The node with the largest value smaller than the given node's value. It's the previous node in the inorder traversal sequence.

#### Visual Understanding

**Example BST**:

```
    20
   /  \
  10   30
 / \   / \
5  15 25 40
   /
  12

Inorder traversal: 5, 10, 12, 15, 20, 25, 30, 40
```

**For node 15**:

- **Successor**: 20 (next larger value)
- **Predecessor**: 12 (previous smaller value)

### Finding Inorder Successor

#### Algorithm for Inorder Successor:

**Case 1: Node has right subtree**

- Successor is the leftmost node in the right subtree

**Case 2: Node has no right subtree**

- Successor is the lowest ancestor whose left child is also an ancestor of the node

### Finding Inorder Predecessor

#### Algorithm for Inorder Predecessor:

**Case 1: Node has left subtree**

- Predecessor is the rightmost node in the left subtree

**Case 2: Node has no left subtree**

- Predecessor is the lowest ancestor whose right child is also an ancestor of the node

### Detailed Examples

#### Example 1: Node with Right Subtree

```
    20
   /  \
  10   30
      /  \
     25   40
    /
   22

Finding successor of 20:
- 20 has right subtree
- Leftmost node in right subtree = 22
- Successor of 20 = 22
```

#### Example 2: Node without Right Subtree

```
    20
   /  \
  10   30
 / \
5  15

Finding successor of 15:
- 15 has no right subtree
- Travel up: 15 < 20, so 20 could be successor
- 20 is the lowest ancestor where 15 is in left subtree
- Successor of 15 = 20
```

### Applications of Successor and Predecessor

| Application               | Use Case                            | Example                               |
| ------------------------- | ----------------------------------- | ------------------------------------- |
| **BST Deletion**          | Replace deleted node with successor | When deleting node with two children  |
| **Range Queries**         | Find elements in a range            | Find all elements between x and y     |
| **Sorted Iteration**      | Traverse BST in sorted order        | Print elements in ascending order     |
| **Finding Next/Previous** | Navigation operations               | Next/Previous buttons in applications |

### Time Complexity Analysis

| Operation            | Best Case | Average Case | Worst Case |
| -------------------- | --------- | ------------ | ---------- |
| **Find Successor**   | O(1)      | O(log n)     | O(n)       |
| **Find Predecessor** | O(1)      | O(log n)     | O(n)       |

**Space Complexity**: O(1) for iterative implementation

### Summary of Key Concepts

#### Successor Summary:

- **With right subtree**: Leftmost in right subtree
- **Without right subtree**: Lowest ancestor from left side

#### Predecessor Summary:

- **With left subtree**: Rightmost in left subtree
- **Without left subtree**: Lowest ancestor from right side

#### Important Properties:

1. Every node (except maximum) has a successor
2. Every node (except minimum) has a predecessor
3. Successor and predecessor maintain BST ordering
4. Used extensively in BST deletion and range operations

---

## Complete BST Operations Summary

### Operation Comparison Table

| Operation       | Time Complexity (Avg) | Time Complexity (Worst) | Space Complexity   | Use Case                    |
| --------------- | --------------------- | ----------------------- | ------------------ | --------------------------- |
| **Search**      | O(log n)              | O(n)                    | O(1) iterative     | Find specific value         |
| **Insert**      | O(log n)              | O(n)                    | O(log n) recursive | Add new data                |
| **Delete**      | O(log n)              | O(n)                    | O(log n) recursive | Remove data                 |
| **Modify**      | O(log n)              | O(n)                    | O(log n)           | Update existing data        |
| **Successor**   | O(log n)              | O(n)                    | O(1)               | Find next larger value      |
| **Predecessor** | O(log n)              | O(n)                    | O(1)               | Find previous smaller value |
| **Traversal**   | O(n)                  | O(n)                    | O(log n)           | Process all nodes           |

### Best Practices for BST Operations

1. **Always check for NULL pointers** before accessing nodes
2. **Use iterative approaches** when possible to save space
3. **Keep tree balanced** for optimal performance
4. **Handle edge cases** (empty tree, single node, etc.)
5. **Consider using self-balancing trees** (AVL, Red-Black) for guaranteed performance

---

## Threaded Binary Trees

### Q5.1. What is a threaded binary tree? Explain the advantages and disadvantages of using this tree.

### Definition and Concept

A **Threaded Binary Tree** is a binary tree where the null pointers (also called null links) are replaced with pointers that point to other nodes in the tree. These special pointers are called "threads" and they help in faster traversal of the tree.

#### Understanding the Problem

In a normal binary tree, many pointers are null (approximately n+1 null pointers in a tree with n nodes). These null pointers waste memory and make traversal operations slower because we need recursion or a stack to traverse the tree.

#### Types of Threaded Binary Trees

1. **Single Threaded Binary Tree**:

   - Only right null pointers are replaced with threads
   - Threads point to the inorder successor

2. **Double Threaded Binary Tree**:
   - Both left and right null pointers are replaced with threads
   - Left threads point to inorder predecessor
   - Right threads point to inorder successor

#### Threading Rules

**For Right Threading (most common)**:

- If a node's right child is null, replace it with a thread pointing to the inorder successor
- If a node's left child is null, it remains null (in single threaded)

**For Double Threading**:

- Left null pointers point to inorder predecessor
- Right null pointers point to inorder successor

#### Visual Example

**Normal Binary Tree**:

```
    A
   / \
  B   C
 /   / \
D   E   F
```

**Inorder traversal**: D → B → A → E → C → F

**Threaded Binary Tree (Right Threaded)**:

```
    A
   / \
  B   C
 /   / \
D   E   F
 \     /
  B   C  (these are threads)
```

---

## Collective Topic: B-Trees and B+ Trees

(https://www.youtube.com/watch?v=BwUvgG29fPc&pp=ygUWYiB0cmVlIGIrIHRyZWUgYiogdHJlZQ%3D%3D)

### 3. Write a short note on B-Tree.

A **B-Tree** is a self-balancing search tree used to store large amounts of sorted data and allow searches, sequential access, insertions, and deletions in logarithmic time. B-Trees are widely used in databases and file systems because they minimize disk reads.

**Key Features:**
- Each node can have multiple keys and children (not just two like binary trees).
- All leaves are at the same level (balanced).
- Internal nodes can have a variable number of children within a predefined range.
- Efficient for systems that read and write large blocks of data (like disks).

**Properties:**
- A B-Tree of order *m* has at most *m* children per node.
- Every node (except root) must have at least ⌈m/2⌉ children.
- All leaves appear at the same level.
- Keys within a node are sorted.

**Use Cases:**  
Databases, file systems, and any application where large data blocks are stored and accessed efficiently.

---

### 4. Write procedures for B-tree search and B-tree insert.

#### B-Tree Search Procedure

1. Start at the root node.
2. For the current node:
    - Scan the keys in order.
    - If the key matches, return the node.
    - If the key is less than a key in the node, move to the left child.
    - If the key is greater than all keys, move to the rightmost child.
3. Repeat until the key is found or a leaf is reached (not found).

**Pseudocode:**
```
BTreeSearch(node, key):
     i = 1
     while i ≤ n and key > node.key[i]:
          i = i + 1
     if i ≤ n and key == node.key[i]:
          return (node, i)
     elif node.isLeaf:
          return NULL
     else:
          return BTreeSearch(node.child[i], key)
```

#### B-Tree Insert Procedure

1. Search for the correct leaf node where the key should be inserted.
2. Insert the key in sorted order in the node.
3. If the node overflows (has more than *m-1* keys), split the node:
    - The middle key moves up to the parent.
    - The node is split into two nodes.
4. If the parent overflows, repeat the split process up to the root.
5. If the root splits, create a new root.

**Summary:**  
Insertion may cause nodes to split and the tree to grow in height, but the tree remains balanced.

---

### 5. Explain B+ tree index files and B-tree index files in detail.

#### B-Tree Index Files

- B-Tree index files use B-Trees to organize and search for records efficiently.
- Each node contains keys and pointers to child nodes or data records.
- Both internal and leaf nodes can store data pointers.
- Searching, insertion, and deletion are efficient (O(log n)).

#### B+ Tree Index Files

- B+ Trees are a variation of B-Trees used in databases and file systems.
- All data records are stored at the leaf level; internal nodes only store keys for navigation.
- Leaf nodes are linked together, making range queries and full scans faster.
- Internal nodes act as a directory, while leaves hold actual data pointers.

**Advantages of B+ Trees for Indexing:**
- Faster range queries due to linked leaves.
- All data at the same level, making sequential access efficient.
- Internal nodes are smaller, allowing more keys per node and reducing tree height.

---

### 6. Write the difference between a B-tree and B+ tree. When might you prefer to use a B+ tree instead of a B-tree?

| Aspect                | B-Tree                                   | B+ Tree                                  |
|-----------------------|------------------------------------------|------------------------------------------|
| **Data Storage**      | Data in both internal and leaf nodes     | Data only in leaf nodes                  |
| **Leaf Node Linking** | Not necessarily linked                   | Leaf nodes are linked (linked list)      |
| **Search**            | May end at internal or leaf node         | Always ends at leaf node                 |
| **Range Queries**     | Slower, must traverse tree               | Faster, scan linked leaves sequentially  |
| **Tree Height**       | Slightly taller (less keys per node)     | Shorter (more keys per internal node)    |
| **Use Case**          | Good for single key lookups              | Best for range queries and full scans    |

**When to Prefer B+ Tree:**
- When you need efficient range queries or ordered traversals (e.g., database indexes).
- When you want all data at the leaf level for easier sequential access.
- When you need to minimize tree height for faster search and update operations.

---

**In summary:**  
- **B-Trees** are general-purpose balanced trees for fast search, insert, and delete.
- **B+ Trees** are optimized for database and file system indexing, especially when range queries and sequential access are important.


### Q5.2. Explain the operation of a threaded binary tree.

### Operations of a Threaded Binary Tree

A threaded binary tree is designed to make tree traversal more efficient by replacing some or all null pointers with special "threads" that point to the next node in a particular traversal order (usually inorder). Here are the main operations and how they work in a threaded binary tree:

#### 1. Inorder Traversal

- **Without Threading:** In a regular binary tree, inorder traversal (left, root, right) typically requires recursion or an explicit stack to keep track of nodes.
- **With Threading:** In a threaded binary tree, threads allow traversal without recursion or a stack. When a node's right pointer is a thread, it points directly to its inorder successor, so you can move to the next node efficiently.
- **Process:** Start at the leftmost node, visit it, and use threads to move to the next node in inorder sequence until all nodes are visited.

#### 2. Preorder and Postorder Traversal

- **Preorder Traversal:** Some threaded trees can be designed to support efficient preorder traversal by using threads that point to the preorder successor.
- **Postorder Traversal:** Postorder traversal is less common with threading, but double-threaded trees (with both left and right threads) can be adapted for this purpose.

#### 3. Insertion

- **Finding the Position:** To insert a new node, first find the appropriate parent node as in a regular binary search tree.
- **Updating Threads:** After insertion, update the threads of the new node and its neighbors. For example, if you insert a node as the left child, its left thread should point to the inorder predecessor, and its right thread (if applicable) should point to the parent or inorder successor.
- **Complexity:** Insertion is more complex than in a regular tree because you must carefully maintain the threading structure.

#### 4. Deletion

- **Removing the Node:** Deletion involves removing the node as in a regular binary tree.
- **Restoring Threads:** After deletion, update the threads of neighboring nodes to ensure the threaded structure remains correct. This may involve redirecting threads to bypass the deleted node and point to the correct inorder predecessor or successor.
- **Complexity:** Deletion is also more complex due to the need to update threads.

#### 5. Searching

- **Same as BST:** Searching for a value in a threaded binary tree is similar to searching in a regular binary search tree, as threading does not affect the search path.
- **Benefit:** Once a node is found, threads can be used for efficient traversal from that point.

#### 6. Successor and Predecessor Operations

- **Inorder Successor:** In a right-threaded tree, the right thread of a node points directly to its inorder successor, making this operation very efficient (O(1) time).
- **Inorder Predecessor:** In a left-threaded or double-threaded tree, the left thread points to the inorder predecessor, also allowing O(1) access.

#### 7. Traversal Without Recursion or Stack

- **Key Benefit:** The main advantage of threaded binary trees is that they allow traversing the tree in a specific order (usually inorder) without using recursion or an explicit stack, saving both time and memory.

#### Summary Table: Threaded Binary Tree Operations

| Operation         | How Threading Helps                          | Complexity      |
|-------------------|----------------------------------------------|-----------------|
| Inorder Traversal | No recursion/stack; use threads for next     | O(n), O(1) space|
| Insertion         | Must update threads for new node and neighbors| O(h)            |
| Deletion          | Must update threads for affected nodes       | O(h)            |
| Search            | Same as BST; threading not used              | O(h)            |
| Successor/Pred.   | Direct access via threads                    | O(1)            |

**Note:** `h` is the height of the tree, and `n` is the number of nodes.

Threaded binary trees are especially useful when frequent traversals are needed and memory or stack space is limited.

### Advantages of Threaded Binary Trees

| Advantage                           | Explanation                        | Benefit                   |
| ----------------------------------- | ---------------------------------- | ------------------------- |
| **Faster Traversal**                | No recursion or stack needed       | O(n) time with O(1) space |
| **Memory Utilization**              | Uses null pointers effectively     | Better memory usage       |
| **Efficient Successor/Predecessor** | Direct pointer access              | O(1) average time         |
| **Simplified Algorithms**           | Iterative implementations possible | Easier to understand      |
| **No Stack Overflow**               | Eliminates recursion               | Safe for large trees      |

### Disadvantages of Threaded Binary Trees

| Disadvantage               | Explanation                          | Impact                      |
| -------------------------- | ------------------------------------ | --------------------------- |
| **Complex Implementation** | More complex insertion/deletion      | Harder to code and maintain |
| **Extra Storage**          | Need boolean flags for threads       | Additional memory per node  |
| **Insertion Complexity**   | Must update multiple threads         | Slower insertion operations |
| **Deletion Complexity**    | Must handle thread updates carefully | Error-prone operations      |
| **Limited Flexibility**    | Structure is more rigid              | Less adaptable to changes   |

### Practical Applications

1. **Compiler Design**: Expression tree traversal
2. **Database Systems**: Index traversal
3. **Operating Systems**: Process tree navigation
4. **Memory-Constrained Systems**: When stack space is limited

---

## Huffman Coding Using Binary Tree

### Introduction to Huffman Coding

**Huffman Coding** is a lossless data compression algorithm that uses a binary tree to create variable-length codes for characters. Characters that appear more frequently get shorter codes, while less frequent characters get longer codes.

### How Huffman Coding Works

#### Basic Principle

- **More frequent characters** → **Shorter codes**
- **Less frequent characters** → **Longer codes**
- **No code is a prefix of another** (prefix property)

#### Algorithm Steps

1. **Calculate character frequencies**
2. **Create leaf nodes** for each character
3. **Build a min-heap** of nodes
4. **Repeatedly combine** two nodes with smallest frequencies
5. **Create Huffman tree** from root
6. **Generate codes** by traversing tree

### Step-by-Step Example

**Input String**: "ABRACADABRA"

#### Huffman Coding Algorithm

```
Algorithm: HuffmanCoding(text)
Input: text - input string to compress
Output: Huffman tree and character codes

1. START
2. // Step 1: Calculate character frequencies
3. frequencies = calculateFrequencies(text)
4. // Step 2: Create leaf nodes for each character
5. nodes = []
6. FOR each character c with frequency f DO
7.     node = createNode(c, f)
8.     nodes.add(node)
9. END FOR
10. // Step 3: Build min-heap
11. heap = createMinHeap(nodes)
12. // Step 4: Build Huffman tree
13. WHILE heap.size > 1 DO
14.     left = extractMin(heap)
15.     right = extractMin(heap)
16.     merged = createNode(null, left.freq + right.freq)
17.     merged.left = left
18.     merged.right = right
19.     insertMinHeap(heap, merged)
20. END WHILE
21. root = extractMin(heap)
22. // Step 5: Generate codes
23. codes = generateCodes(root)
24. RETURN root, codes
25. STOP

Algorithm: generateCodes(root)
Input: root - root of Huffman tree
Output: array of codes for each character

1. codes = []
2. generateCodesHelper(root, "", codes)
3. RETURN codes

Algorithm: generateCodesHelper(node, code, codes)
1. IF node = NULL THEN RETURN
2. IF node.isLeaf THEN
3.     codes[node.character] = code
4.     RETURN
5. END IF
6. generateCodesHelper(node.left, code + "0", codes)
7. generateCodesHelper(node.right, code + "1", codes)
```

#### Step 1: Calculate Frequencies

| Character | Frequency |
| --------- | --------- |
| A         | 5         |
| B         | 2         |
| R         | 2         |
| C         | 1         |
| D         | 1         |

#### Step 2: Create Initial Nodes

```
C(1)  D(1)  B(2)  R(2)  A(5)
```

#### Step 3: Build Huffman Tree

**Iteration 1**: Combine C(1) and D(1)

```
   (2)
  /   \
C(1) D(1)

Remaining: (2), B(2), R(2), A(5)
```

**Iteration 2**: Combine (2) and B(2)

```
   (4)
  /   \
(2)   B(2)
 /\
C D

Remaining: (4), R(2), A(5)
```

**Iteration 3**: Combine (4) and R(2)

```
     (6)
    /   \
  (4)   R(2)
  /\
(2) B
/\
C D

Remaining: (6), A(5)
```

**Iteration 4**: Combine (6) and A(5)

```
Final Huffman Tree:
       (11)
      /    \
    A(5)   (6)
           /   \
         (4)   R(2)
         /\
       (2) B(2)
       /\
     C(1) D(1)
```
