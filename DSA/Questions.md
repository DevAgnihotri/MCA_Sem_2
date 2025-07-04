# Data Structures and Algorithms Questions

Unit 1 and 2

## 1. Algorithms

1. Define the term ‘Algorithm’. Give the essential properties of an algorithm.
2. Describe the Big Oh notation.
3. Write down algorithm to evaluate postfix expression and also evaluate given postfix expression using the algorithm:  
    `10, 7 + 30, 6 / * 8 -`
4. (a) Let A[n] be an array of “n” numbers. Design a data structure and algorithm to perform any sequence of the following two operations:  
    (i) Add(i, y): add the value y to the ith number in the array.  
    (ii) Partial-sum(i): returns the sum of the first ”i” numbers in the array, i.e.,  
    $$\sum_{j=1}^{i} A[j]$$

## 2. Data Structures: Definitions and Types

1. Define the term data structure. List some linear and non-linear data structures stating the application area where they will be used.
2. Discuss Linear and Nonlinear data structure with example.
3. Differentiate between array and linked list.
4. Define Data structure and also write down the primitive and non-primitive data
structure in detail with examples. 

## 3. Queues

1. Define the types of queues.
2. What is Queue? Explain Priority Queue. Write uses of Queue.
3. (a) Write an algorithm for insertion and deletion of elements of a queue. Use a Boolean variable to distinguish between a queue being empty or full.
4. (b) Consider the following linear queue capable of accommodating maximum five elements.  
    Front = 2, Rear = 4, Queue = [_, L, M, N, _]  
    Compute the following operations:  
    (i) Add O  
    (ii) Add P  
    (iii) Delete two letters  
    (iv) Add Q, R
5. WAP it insert and element in already exisiting queue
6. Define Queue also write the algorithm for insertion and deletion of element in a
Queue.
7. Why circular queues are better than simple queue? Write an algorithm to insert
and delete an item from the circular queue. 

## 4. Arrays

1. (a) How two-dimensional arrays are represented in memory? Also obtain the formula for calculating the address of any element stored in array, in case of column major order. (Make necessary assumptions yourself)
2. (b) Drive the index formula for 2-Dimensional array stored as row major order.

## 5. Stacks

1. (b) Write a “C” program using stack to check whether a string is palindrome or not. Do not define empty, push, and pop functions. (Note: Palindrome is a sequence of characters that reads the same backward and forward.)
2. (c) Transform the following prefix expression to infix:  
    `++A-*$BCD/+EF*GHI`
3. Define Stack. Convert the expressioninfix to prefix using stack:
A*(B+D)/E-F*(G+H/K).
4. What is the Tower of Hanoi problem? Explain the solutions of the Tower of
Hanoi problem where the numbers of disks are 3 and numbers of pages are 3.
5. Define Stack and algo for Push and Pop

## 6. Searching

1. (b) Write function in C, which deletes all occurrences of a given character from a given string.
2. Write an algorithm for binary search and discuss its speed compared with linear
search.
3. What is searching and sorting? Write an algorithm for linear search and binary
search

## 7. Hashing

1. Define Hashing. Discuss various methods of collision resolution with suitable example.
2. What do you understand by hashing? What are the different hashing techniques? Discuss different techniques to resolve collision once it is occurred during hashing.
3. Define Hash function. Explain Collision resolution strategies. How collision is resolved using separate chaining concept?
4. Define hashing. What are the properties of a good hash function? With necessary examples explain four different hashing techniques.

## 8. Parameter Passing

1. (d) Explain parameter-passing technique used in C with example.

## 9. Recursion

1. (c) Let J and K be integers and suppose Q(J, K) is recursively defined as  
    - Q(J, K) = 5 if J < K  
    - Q(J, K) = Q(J-K, K+3) + J if J ≥ K  
    Find Q(4, 7).

## 10. LL

1. How to represent followings linked lists in memory provide their self-referential
structure and proper diagram
(i) Single linear Linked List
(ii) Doubly linear Linked list
(iii) Circular Doubly Linked List
(iv) Header Li

2. Give an algorithm or C function to perform following operations on single linear linked
list
(i) Insert a node after a given node
(ii) Delete a node from end

3. What is a 2 way LL and it's adv over one way LL
4. C program to find the greatest common divisor
5. C prog to reverse a LL
6. What is doubly linked list? Write an algorithm to add an element in the doubly
linked list before the given element.

Unit 4 and 5

## 1. Binary Trees

(d) What do you mean by pattern matching? Discuss any pattern matching
algorithm with proper example.
(e) Write an algorithm which finds the transitive closure of a graph. 

1. **Binary Search Tree (BST)**
    2. What is a binary search tree? Write an algorithm to implement recursive or iterative search for a binary search tree.
    3. Write down a recursive algorithm to insert a node in a binary search tree. Apply that algorithm to construct a BST with the given data:  
       `8, 5, 12, 67, 43, 23, 6, 3, 2, 8, 24, 21, 20`
    5. Discuss the basic properties of a Binary Search Tree.
    6. Explain the successor of a node in a Binary Search Tree.
    7. Differentiate between a Binary Tree and a Complete Binary Tree.
    8. Explain Complete Binary Tree and Extended Binary Tree.

2. **Tree Traversals**
    1. Write recursive algorithms for Pre-Order, Post-Order, and In-Order traversals of a binary tree.
    2. Short note on tree traversal.
    3. Discuss the concept of inorder *successor* and inorder *predecessor* in a Binary Search Tree.
    4. The pre-order and in-order traversal of binary tree is given below, construct the
tree:
preorder:-FAEKCDHGB
in-order:-EACKFHDBG 

3. **Memory Representation**
    1. Give static and dynamic memory representation of a binary tree.

4. **Balanced Trees**
    1. What is an AVL tree? What is the balancing factor? Explain the balancing method of AVL trees with all possible cases and suitable examples.
    2. Write a short note on AVL trees.
    3. Explain the balancing methods of AVL trees with an example.
    4. Write a short note on balanced binary trees.

5. **Threaded Binary Trees**
    1. What is a threaded binary tree? Explain the advantages and disadvantages of using this tree.
    2. Explain the operation of a threaded binary tree.

6. **Other Tree Types**
    3. Write a short note on B-Tree.
    4. Write procedures for B-tree search and B-tree insert.
    5. Explain B+ tree index files and B-tree index files in detail.
    6. 4. Write the difference between a B-tree and B+ tree. When might you prefer to use a B+ tree instead of a B-tree?
    7. Describe the minimum cost spanning tree with a suitable example.



## UNIT 5

**Graph Algorithms**
    1. Write down the algorithm of Floyd-Warshall to compute all-pair shortest paths in a graph. Also, apply it on a given graph.
    2. Explain Kruskal’s algorithm to find the minimum cost spanning tree with an example.

1. **Strassen’s Matrix Multiplication**
    1. How does Strassen’s matrix multiplication provide better time complexity over the classical matrix multiplication algorithm? Apply Strassen's algorithm on the following matrices:  
       ```
       1 5      8 2
       7 3  x   6 4
       ```

2. **Longest Common Subsequence (LCS)**
    1. Discuss the applications of the longest common subsequence (LCS).
    2. Determine the LCS of `<1,0,0,1,0,1,0,1>` and `<0,1,0,1,1,0,1,1,0>`.

3. **Huffman Algorithm**
    1. Write a short note on the Huffman algorithm, explaining various steps with an example.
    
## 3. Sorting Algorithms

### Quick Sort

1. Write down the Quick Sort algorithm and apply it on the following data to sort it:  
   `5, 8, 7, 6, 3, 4, 1, 9, 2, 10`
2. Write an algorithm for the implementation of Quick Sort. Apply the algorithm to sort the given list:  
   `65, 70, 75, 80, 85, 60, 55, 40, 45`  
   Also, find its time and space complexity.
3. Define Quick Sort. Illustrate the Quick Sort algorithm with a suitable example.

### Merge Sort

1. Write a C program to perform Merge Sort and analyze the time complexity of the algorithm.
2. Write the algorithm for Merge Sort. Explain its complexities and sort the following elements using Merge Sort:  
   `75, 10, 20, 70, 80, 90, 100, 40, 30, 50`

3. **Search Algorithms**
    1. Compare linear search and binary search algorithms with examples and their complexities.

---

**Note:** For questions that require applying algorithms to specific data or graphs, refer to the provided data or diagrams as needed.
