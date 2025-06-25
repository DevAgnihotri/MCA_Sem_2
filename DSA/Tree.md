# Tree Data Structure: Complete Guide

---

## Introduction to Trees

A **tree** is a hierarchical data structure that consists of nodes connected by edges. It is a non-linear data structure that resembles an upside-down tree with a root at the top and leaves at the bottom.

---

## Basic Terminology Used with Tree

### Key Terms and Definitions

| Term                   | Definition                                                        | Example                        |
|------------------------|-------------------------------------------------------------------|--------------------------------|
| **Node**               | Fundamental unit of a tree containing data and links to children  | Each circle in a tree diagram  |
| **Root**               | The topmost node with no parent                                   | Starting point of the tree     |
| **Parent**             | A node that has one or more children                              | Node above another node        |
| **Child**              | A node that descends from a parent node                           | Node below another node        |
| **Leaf (External Node)** | A node with no children                                         | End nodes of the tree          |
| **Internal Node**      | A node with at least one child                                    | Any non-leaf node              |
| **Edge**               | A connection between two nodes                                    | Line connecting nodes          |
| **Path**               | Sequence of nodes connected by edges                              | Route from root to a leaf      |
| **Height of Tree**     | Length of the longest path from root to any leaf                  | Maximum depth of the tree      |
| **Depth of Node**      | Number of edges from root to that node                            | Distance from root             |
| **Level**              | All nodes at the same depth                                       | Horizontal layer in the tree   |
| **Degree**             | Number of children a node has                                     | Branching factor               |
| **Subtree**            | A tree formed by a node and all its descendants                   | Portion of the tree            |

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

| Type                       | Description                                                        | Characteristics                |
|----------------------------|--------------------------------------------------------------------|--------------------------------|
| **Full Binary Tree**       | Every node has either 0 or 2 children                              | No node has only 1 child       |
| **Complete Binary Tree**   | All levels filled except possibly the last, which is filled left to right | Efficient for heap implementation |
| **Perfect Binary Tree**    | All internal nodes have 2 children, all leaves are at the same level | Most balanced form             |
| **Balanced Binary Tree**   | Height difference between left and right subtrees of any node is at most 1 | Good for search operations     |
| **Degenerate (Skewed) Tree** | Each parent has only one child                                   | Essentially a linked list      |

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

| Advantages              | Disadvantages                          |
|-------------------------|----------------------------------------|
| ✓ Simple indexing       | ✗ Wastes memory for skewed trees       |
| ✓ No pointers required  | ✗ Fixed size (array must be pre-sized) |
| ✓ Cache friendly        | ✗ Insertion/deletion is complex        |


### 2. Pointer (Linked List) Representation

Each node contains data and pointers to left and right children.

#### Structure:
```c
struct TreeNode {
    int data;
    struct TreeNode* left;
    struct TreeNode* right;
};
```

#### Example Implementation:
```c
// Create a new node
struct TreeNode* createNode(int data) {
    struct TreeNode* newNode = (struct TreeNode*)malloc(sizeof(struct TreeNode));
    newNode->data = data;
    newNode->left = NULL;
    newNode->right = NULL;
    return newNode;
}
```

#### Advantages and Disadvantages:
| Advantages                | Disadvantages                    |
|---------------------------|----------------------------------|
| ✓ Dynamic size            | ✗ Extra memory needed for pointers |
| ✓ No memory wasted        | ✗ Less cache friendly             |
| ✓ Easy insertion/deletion | ✗ Implementation is more complex  |

---

## Binary Search Tree (BST)

### Q2. What is a binary search tree? Write an algorithm to implement recursive or iterative search for a binary search tree.


### Definition

A **Binary Search Tree (BST)** is a binary tree with the following properties:
- All nodes in the left subtree have values less than the root
- All nodes in the right subtree have values greater than the root
- Both left and right subtrees are also BSTs

### Search Algorithms

#### Recursive Search Algorithm:
```c
struct TreeNode* searchRecursive(struct TreeNode* root, int key) {
    // Base cases: root is null or key is present at root
    if (root == NULL || root->data == key)
        return root;
    
    // Key is greater than root's data
    if (key > root->data)
        return searchRecursive(root->right, key);
    
    // Key is smaller than root's data
    return searchRecursive(root->left, key);
}
```

#### Iterative Search Algorithm:
```c
struct TreeNode* searchIterative(struct TreeNode* root, int key) {
    while (root != NULL && root->data != key) {
        if (key > root->data)
            root = root->right;
        else
            root = root->left;
    }
    return root;
}
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

#### Recursive Insertion Algorithm:

```c
struct TreeNode* insert(struct TreeNode* root, int data) {
    // Base case: if tree is empty, create new node
    if (root == NULL) {
        return createNode(data);
    }
    
    // If data is less than root, insert in left subtree
    if (data < root->data) {
        root->left = insert(root->left, data);
    }
    // If data is greater than root, insert in right subtree
    else if (data > root->data) {
        root->right = insert(root->right, data);
    }
    // If data equals root data, don't insert (no duplicates)
    
    return root;
}
```

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

**Question 6: Explain the successor of a node in a Binary Search Tree.**

#### Definition
The **successor** of a node in a BST is the node with the smallest value greater than the given node's value. In other words, it's the next node in the in-order traversal.

#### Algorithm to Find Successor:

```c
struct TreeNode* findMin(struct TreeNode* root) {
    while (root->left != NULL)
        root = root->left;
    return root;
}

struct TreeNode* findSuccessor(struct TreeNode* root, struct TreeNode* node) {
    // Case 1: Node has right subtree
    if (node->right != NULL) {
        return findMin(node->right);
    }
    
    // Case 2: Node has no right subtree
    struct TreeNode* successor = NULL;
    while (root != NULL) {
        if (node->data < root->data) {
            successor = root;
            root = root->left;
        } else if (node->data > root->data) {
            root = root->right;
        } else {
            break;
        }
    }
    return successor;
}
```

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

## Complete Binary Tree

### Q7. Differentiate between a Binary Tree and a Complete Binary Tree.
### Q8. Explain Complete Binary Tree and Extended Binary Tree.

**Questions 7 & 8: Differentiate between a Binary Tree and a Complete Binary Tree. Explain Complete Binary Tree and Extended Binary Tree.**

### Binary Tree vs Complete Binary Tree

| Aspect                | Binary Tree                                                                 | Complete Binary Tree                                                      |
|-----------------------|-----------------------------------------------------------------------------|---------------------------------------------------------------------------|
| **Definition**        | A tree in which each node has at most 2 children                          | A binary tree where all levels are completely filled except possibly the last, which is filled from left to right |
| **Structure**         | Nodes can be arranged in any shape (may be skewed or unbalanced)            | Nodes are arranged to fill each level before moving to the next, ensuring compactness |
| **Array Representation** | May result in wasted space due to gaps for missing children               | Very efficient; nodes are stored in contiguous array positions without gaps |
| **Height**            | Can be unbalanced; height may be as large as the number of nodes            | More balanced; height is minimized for the number of nodes                 |
| **Completeness**      | No requirement for completeness                                             | Must be complete except possibly the last level, which is filled left to right |
| **Insertion Order**   | No specific order required                                                  | Insertions always occur at the leftmost available position at the lowest level |
| **Traversal**         | Traversal order and structure can vary widely                               | Traversal order is more predictable due to compact structure               |
| **Applications**      | Used for general tree operations, expression trees, etc.                    | Used in heaps, priority queues, and situations requiring efficient array storage |
| **Efficiency**        | May be inefficient for some operations if unbalanced                        | Efficient for operations like heapify, due to predictable structure        |
| **Examples**          | Any binary tree, including skewed or sparse trees                           | Heap trees, complete levels except possibly the last                       |


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
| Tree Type               | Key Characteristics                                      | Common Use Cases                | Time Complexity (Search/Insert/Delete) |
|-------------------------|----------------------------------------------------------|---------------------------------|----------------------------------------|
| **Binary Tree**         | Each node has at most 2 children                         | General hierarchical data, parsing expressions | Varies (depends on shape)              |
| **Binary Search Tree (BST)** | Left subtree < root < right subtree; no duplicates         | Searching, dynamic sorting, dictionaries | O(log n) average, O(n) worst           |
| **Complete Binary Tree**| All levels filled except possibly last, filled left to right | Heaps, priority queues, array-based trees | O(log n)                              |
| **Extended Binary Tree**| Every node has either 0 or 2 children (full binary tree) | Expression trees, Huffman coding | Varies                                 |

---

## Tree Traversal Algorithms

### Q2. Short note on tree traversal.

**Question 2: Short note on tree traversal.**

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

### Q1. Write recursive algorithms for Pre-Order, Post-Order, and In-Order traversals of a binary tree.

**Question 1: Write recursive algorithms for Pre-Order, Post-Order, and In-Order traversals of a binary tree.**

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

| Traversal Type | Order | Best Use Case | Memory Usage |
|----------------|-------|---------------|--------------|
| **Inorder** | Left → Root → Right | Getting sorted data from BST | O(h) where h is height |
| **Preorder** | Root → Left → Right | Copying/creating tree structure | O(h) where h is height |
| **Postorder** | Left → Right → Root | Deleting tree/calculating sizes | O(h) where h is height |

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

| Aspect | Complexity | Explanation |
|--------|------------|-------------|
| **Time Complexity** | O(n) | Each node is visited exactly once |
| **Space Complexity** | O(h) | Recursive call stack uses space proportional to height |
| **Best Case Space** | O(log n) | For balanced tree |
| **Worst Case Space** | O(n) | For skewed tree |

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

#### Deletion Algorithm:
```c
struct TreeNode* findMin(struct TreeNode* root) {
    while (root && root->left)
        root = root->left;
    return root;
}

struct TreeNode* deleteNode(struct TreeNode* root, int key) {
    if (root == NULL)
        return root;
    
    // Key is in left subtree
    if (key < root->data) {
        root->left = deleteNode(root->left, key);
    }
    // Key is in right subtree
    else if (key > root->data) {
        root->right = deleteNode(root->right, key);
    }
    // Key found - this is the node to delete
    else {
        // Case 1: No children (leaf node)
        if (root->left == NULL && root->right == NULL) {
            free(root);
            return NULL;
        }
        // Case 2: One child
        else if (root->left == NULL) {
            struct TreeNode* temp = root->right;
            free(root);
            return temp;
        }
        else if (root->right == NULL) {
            struct TreeNode* temp = root->left;
            free(root);
            return temp;
        }
        // Case 3: Two children
        else {
            struct TreeNode* successor = findMin(root->right);
            root->data = successor->data;
            root->right = deleteNode(root->right, successor->data);
        }
    }
    return root;
}
```

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

**Question 3: Discuss the concept of inorder successor and inorder predecessor in a Binary Search Tree.**

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

#### Implementation:
```c
struct TreeNode* findInorderSuccessor(struct TreeNode* root, struct TreeNode* node) {
    // Case 1: Node has right subtree
    if (node->right != NULL) {
        return findMin(node->right);
    }
    
    // Case 2: Node has no right subtree
    struct TreeNode* successor = NULL;
    while (root != NULL) {
        if (node->data < root->data) {
            successor = root;
            root = root->left;
        } else if (node->data > root->data) {
            root = root->right;
        } else {
            break;
        }
    }
    return successor;
}
```

### Finding Inorder Predecessor

#### Algorithm for Inorder Predecessor:

**Case 1: Node has left subtree**
- Predecessor is the rightmost node in the left subtree

**Case 2: Node has no left subtree**
- Predecessor is the lowest ancestor whose right child is also an ancestor of the node

#### Implementation:
```c
struct TreeNode* findMax(struct TreeNode* root) {
    while (root && root->right)
        root = root->right;
    return root;
}

struct TreeNode* findInorderPredecessor(struct TreeNode* root, struct TreeNode* node) {
    // Case 1: Node has left subtree
    if (node->left != NULL) {
        return findMax(node->left);
    }
    
    // Case 2: Node has no left subtree
    struct TreeNode* predecessor = NULL;
    while (root != NULL) {
        if (node->data > root->data) {
            predecessor = root;
            root = root->right;
        } else if (node->data < root->data) {
            root = root->left;
        } else {
            break;
        }
    }
    return predecessor;
}
```

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

| Application | Use Case | Example |
|-------------|----------|---------|
| **BST Deletion** | Replace deleted node with successor | When deleting node with two children |
| **Range Queries** | Find elements in a range | Find all elements between x and y |
| **Sorted Iteration** | Traverse BST in sorted order | Print elements in ascending order |
| **Finding Next/Previous** | Navigation operations | Next/Previous buttons in applications |

### Time Complexity Analysis

| Operation | Best Case | Average Case | Worst Case |
|-----------|-----------|--------------|------------|
| **Find Successor** | O(1) | O(log n) | O(n) |
| **Find Predecessor** | O(1) | O(log n) | O(n) |

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

| Operation | Time Complexity (Avg) | Time Complexity (Worst) | Space Complexity | Use Case |
|-----------|----------------------|------------------------|------------------|----------|
| **Search** | O(log n) | O(n) | O(1) iterative | Find specific value |
| **Insert** | O(log n) | O(n) | O(log n) recursive | Add new data |
| **Delete** | O(log n) | O(n) | O(log n) recursive | Remove data |
| **Modify** | O(log n) | O(n) | O(log n) | Update existing data |
| **Successor** | O(log n) | O(n) | O(1) | Find next larger value |
| **Predecessor** | O(log n) | O(n) | O(1) | Find previous smaller value |
| **Traversal** | O(n) | O(n) | O(log n) | Process all nodes |

### Best Practices for BST Operations

1. **Always check for NULL pointers** before accessing nodes
2. **Use iterative approaches** when possible to save space
3. **Keep tree balanced** for optimal performance
4. **Handle edge cases** (empty tree, single node, etc.)
5. **Consider using self-balancing trees** (AVL, Red-Black) for guaranteed performance

---
