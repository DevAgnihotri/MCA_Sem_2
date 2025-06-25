# DSA Unit 5: Advanced Algorithms

---

## Matrix Multiplication: Strassen's Algorithm

### Introduction to Matrix Multiplication

**Matrix multiplication** is a fundamental operation in computer science and mathematics. For two matrices A (m×n) and B (n×p), the result is matrix C (m×p) where each element C[i][j] is computed as the dot product of row i of A and column j of B.

### Classical Matrix Multiplication

#### Traditional Algorithm

**Classical Matrix Multiplication Algorithm:**

1. **Initialize** the result matrix C with dimensions m×p and set all elements to zero
2. **For each row i** in matrix A (from 0 to m-1):
   - **For each column j** in matrix B (from 0 to p-1):
     - **Initialize** the current element C[i][j] to zero
     - **For each element k** in the current row of A and column of B (from 0 to n-1):
       - **Multiply** element A[i][k] with element B[k][j]
       - **Add** this product to the current sum in C[i][j]
     - **Store** the final sum as C[i][j]
3. **Return** the completed result matrix C

**Process**: Each element of the result matrix is computed as the dot product of the corresponding row from the first matrix and column from the second matrix.

**Time Complexity**: O(n³) for n×n matrices

### Q1.1. How does Strassen's matrix multiplication provide better time complexity over the classical matrix multiplication algorithm? Apply Strassen's algorithm on the following matrices:

**Question 1.1: How does Strassen's matrix multiplication provide better time complexity over the classical matrix multiplication algorithm? Apply Strassen's algorithm on the following matrices:**

```
1 5      8 2
7 3  x   6 4
```

### Strassen's Algorithm Explanation

#### Why Strassen's Algorithm is Better

**Classical vs Strassen Comparison:**

| Aspect               | Classical Algorithm | Strassen's Algorithm |
| -------------------- | ------------------- | -------------------- |
| **Time Complexity**  | O(n³)               | O(n^2.807)           |
| **Multiplications**  | n³                  | 7 × (n/2)^2.807      |
| **Approach**         | Direct computation  | Divide and conquer   |
| **Space Complexity** | O(1) extra          | O(n²) extra          |

#### How Strassen's Works

**Key Insight**: Instead of 8 multiplications for 2×2 matrices, use only 7 multiplications with clever additions and subtractions.

#### Strassen's Algorithm for 2×2 Matrices

**Strassen's Matrix Multiplication Algorithm:**

1. **Partition the input matrices** A and B into 2×2 format:
   - Matrix A has elements a11, a12, a21, a22
   - Matrix B has elements b11, b12, b21, b22

2. **Calculate seven strategic products** (instead of the usual eight multiplications):
   - **Product P1**: Multiply a11 by the difference (b12 - b22)
   - **Product P2**: Multiply the sum (a11 + a12) by b22
   - **Product P3**: Multiply the sum (a21 + a22) by b11
   - **Product P4**: Multiply a22 by the difference (b21 - b11)
   - **Product P5**: Multiply the sum (a11 + a22) by the sum (b11 + b22)
   - **Product P6**: Multiply the difference (a12 - a22) by the sum (b21 + b22)
   - **Product P7**: Multiply the difference (a11 - a21) by the sum (b11 + b12)

3. **Combine the products** to form the result matrix elements:
   - **Element c11**: Add P5, P4, subtract P2, then add P6
   - **Element c12**: Add P1 and P2
   - **Element c21**: Add P3 and P4
   - **Element c22**: Add P5, P1, subtract P3, then subtract P7

4. **Construct the final result matrix** C using the calculated elements

**Key Innovation**: This method reduces the number of scalar multiplications from 8 to 7, which leads to better asymptotic performance for large matrices.

#### Applied Example

**Given Matrices:**

```
A = [1 5]    B = [8 2]
    [7 3]        [6 4]
```

**Step 1: Calculate the 7 Products**

```
P1 = a11 × (b12 - b22) = 1 × (2 - 4) = 1 × (-2) = -2
P2 = (a11 + a12) × b22 = (1 + 5) × 4 = 6 × 4 = 24
P3 = (a21 + a22) × b11 = (7 + 3) × 8 = 10 × 8 = 80
P4 = a22 × (b21 - b11) = 3 × (6 - 8) = 3 × (-2) = -6
P5 = (a11 + a22) × (b11 + b22) = (1 + 3) × (8 + 4) = 4 × 12 = 48
P6 = (a12 - a22) × (b21 + b22) = (5 - 3) × (6 + 4) = 2 × 10 = 20
P7 = (a11 - a21) × (b11 + b12) = (1 - 7) × (8 + 2) = (-6) × 10 = -60
```

**Step 2: Calculate Result Elements**

```
c11 = P5 + P4 - P2 + P6 = 48 + (-6) - 24 + 20 = 38
c12 = P1 + P2 = (-2) + 24 = 22
c21 = P3 + P4 = 80 + (-6) = 74
c22 = P5 + P1 - P3 - P7 = 48 + (-2) - 80 - (-60) = 26
```

**Final Result:**

```
C = [38 22]
    [74 26]
```

**Verification using Classical Method:**

```
c11 = 1×8 + 5×6 = 8 + 30 = 38 ✓
c12 = 1×2 + 5×4 = 2 + 20 = 22 ✓
c21 = 7×8 + 3×6 = 56 + 18 = 74 ✓
c22 = 7×2 + 3×4 = 14 + 12 = 26 ✓
```

#### Advantages and Disadvantages

**Advantages:**

- Better asymptotic complexity O(n^2.807)
- Significant speedup for large matrices
- Divide and conquer approach

**Disadvantages:**

- More complex implementation
- Higher constant factors
- Requires extra memory
- Not numerically stable for floating-point

---

## Dynamic Programming

### Introduction to Dynamic Programming

**Dynamic Programming (DP)** is an algorithmic technique for solving optimization problems by breaking them into smaller subproblems and storing solutions to avoid redundant calculations.

#### Key Characteristics:

1. **Optimal Substructure**: Optimal solution contains optimal solutions to subproblems
2. **Overlapping Subproblems**: Same subproblems are solved multiple times
3. **Memoization**: Store solutions to subproblems

#### DP Approaches:

- **Top-Down (Memoization)**: Recursion with memory
- **Bottom-Up (Tabulation)**: Iterative approach

---

## Shortest Path Algorithms

### Dijkstra's Algorithm

#### Introduction

**Dijkstra's Algorithm** finds the shortest path from a source vertex to all other vertices in a weighted graph with non-negative edge weights.

#### Algorithm

```
Algorithm: Dijkstra(Graph G, source s)
Input: Weighted graph G, source vertex s
Output: Shortest distances from s to all vertices

1. START
2. FOR each vertex v in G DO
3.     distance[v] = INFINITY
4.     previous[v] = NULL
5.     visited[v] = FALSE
6. END FOR
7. distance[s] = 0
8. priorityQueue = createMinHeap()
9. INSERT(priorityQueue, s, 0)
10. WHILE priorityQueue is not empty DO
11.     u = EXTRACT_MIN(priorityQueue)
12.     IF visited[u] = TRUE THEN CONTINUE
13.     visited[u] = TRUE
14.     FOR each neighbor v of u DO
15.         alt = distance[u] + weight(u, v)
16.         IF alt < distance[v] THEN
17.             distance[v] = alt
18.             previous[v] = u
19.             INSERT(priorityQueue, v, alt)
20.         END IF
21.     END FOR
22. END WHILE
23. RETURN distance[], previous[]
24. STOP
```

#### Example

**Graph:**

```
     (2)
  A -----> B
  |      / |
(4)|   (1)  |(7)
  |  /      |
  v v       v
  C -----> D
     (3)
```

**Step-by-Step Execution (Source = A):**

| Step | Current | Queue          | Distance[A] | Distance[B] | Distance[C] | Distance[D] |
| ---- | ------- | -------------- | ----------- | ----------- | ----------- | ----------- |
| 1    | -       | A(0)           | 0           | ∞           | ∞           | ∞           |
| 2    | A       | B(2),C(4)      | 0           | 2           | 4           | ∞           |
| 3    | B       | C(3),C(4),D(9) | 0           | 2           | 3           | 9           |
| 4    | C       | D(6),D(9)      | 0           | 2           | 3           | 6           |
| 5    | D       | -              | 0           | 2           | 3           | 6           |

**Final Shortest Distances:**

- A to A: 0
- A to B: 2
- A to C: 3
- A to D: 6

**Time Complexity**: O((V + E) log V) with binary heap

### Bellman-Ford Algorithm

#### Introduction

**Bellman-Ford Algorithm** finds shortest paths from a source vertex to all other vertices, and can handle negative edge weights. It also detects negative cycles.

#### Algorithm

```
Algorithm: BellmanFord(Graph G, source s)
Input: Weighted graph G, source vertex s
Output: Shortest distances and negative cycle detection

1. START
2. // Initialize distances
3. FOR each vertex v in G DO
4.     distance[v] = INFINITY
5.     predecessor[v] = NULL
6. END FOR
7. distance[s] = 0
8.
9. // Relax edges V-1 times
10. FOR i = 1 TO |V| - 1 DO
11.     FOR each edge (u, v) in G DO
12.         IF distance[u] + weight(u, v) < distance[v] THEN
13.             distance[v] = distance[u] + weight(u, v)
14.             predecessor[v] = u
15.         END IF
16.     END FOR
17. END FOR
18.
19. // Check for negative cycles
20. FOR each edge (u, v) in G DO
21.     IF distance[u] + weight(u, v) < distance[v] THEN
22.         RETURN "Negative cycle detected"
23.     END IF
24. END FOR
25.
26. RETURN distance[], predecessor[]
27. STOP
```

#### Example

**Graph with Negative Edges:**

```
     (1)      (-3)
  A -----> B -----> C
  |                 |
(4)|                 |(2)
  |                 |
  v                 v
  D <------------- E
        (5)
```

**Iteration Process:**

| Iteration | Distance[A] | Distance[B] | Distance[C] | Distance[D] | Distance[E] |
| --------- | ----------- | ----------- | ----------- | ----------- | ----------- |
| 0         | 0           | ∞           | ∞           | ∞           | ∞           |
| 1         | 0           | 1           | ∞           | 4           | ∞           |
| 2         | 0           | 1           | -2          | 4           | 0           |
| 3         | 0           | 1           | -2          | 4           | 0           |
| 4         | 0           | 1           | -2          | 4           | 0           |

**Time Complexity**: O(VE)

---

## All-Pair Shortest Path: Floyd-Warshall Algorithm

### Q1. Write down the algorithm of Floyd-Warshall to compute all-pair shortest paths in a graph. Also, apply it on a given graph.

**Question 1: Write down the algorithm of Floyd-Warshall to compute all-pair shortest paths in a graph. Also, apply it on a given graph.**

### Floyd-Warshall Algorithm

#### Introduction

**Floyd-Warshall Algorithm** finds the shortest paths between all pairs of vertices in a weighted graph. It works with negative edges but not negative cycles.

#### Algorithm

```
Algorithm: FloydWarshall(Graph G)
Input: Weighted graph G with adjacency matrix
Output: All-pair shortest distances

1. START
2. n = number of vertices
3. // Initialize distance matrix
4. FOR i = 0 TO n-1 DO
5.     FOR j = 0 TO n-1 DO
6.         IF i = j THEN
7.             distance[i][j] = 0
8.         ELSE IF edge(i,j) exists THEN
9.             distance[i][j] = weight(i,j)
10.        ELSE
11.            distance[i][j] = INFINITY
12.        END IF
13.    END FOR
14. END FOR
15.
16. // Main algorithm - try all intermediate vertices
17. FOR k = 0 TO n-1 DO
18.     FOR i = 0 TO n-1 DO
19.         FOR j = 0 TO n-1 DO
20.             IF distance[i][k] + distance[k][j] < distance[i][j] THEN
21.                 distance[i][j] = distance[i][k] + distance[k][j]
22.             END IF
23.         END FOR
24.     END FOR
25. END FOR
26.
27. RETURN distance[][]
28. STOP
```

#### Applied Example

**Given Graph:**

```
     (3)      (8)
  0 -----> 1 -----> 3
  |        |        ^
(5)|      (2)|       |(1)
  |        |        |
  v        v        |
  2 -----> 4 -------+
     (6)      (7)
```

**Initial Distance Matrix:**

```
     0   1   2   3   4
0 [  0   3   5  ∞  ∞ ]
1 [  ∞   0  ∞   8   2 ]
2 [  ∞  ∞   0  ∞   6 ]
3 [  ∞  ∞  ∞   0  ∞ ]
4 [  ∞  ∞  ∞   1  0 ]
```

**Step-by-Step Execution:**

**k = 0 (via vertex 0):**

```
     0   1   2   3   4
0 [  0   3   5  ∞  ∞ ]
1 [  ∞   0  ∞   8   2 ]
2 [  ∞  ∞   0  ∞   6 ]
3 [  ∞  ∞  ∞   0  ∞ ]
4 [  ∞  ∞  ∞   1   0 ]
```

**k = 1 (via vertex 1):**

```
     0   1   2   3   4
0 [  0   3   5  11   5 ]
1 [  ∞   0  ∞   8   2 ]
2 [  ∞  ∞   0  ∞   6 ]
3 [  ∞  ∞  ∞   0  ∞ ]
4 [  ∞  ∞  ∞   1   0 ]
```

**k = 2 (via vertex 2):**

```
     0   1   2   3   4
0 [  0   3   5  11   5 ]
1 [  ∞   0  ∞   8   2 ]
2 [  ∞  ∞   0  ∞   6 ]
3 [  ∞  ∞  ∞   0  ∞ ]
4 [  ∞  ∞  ∞   1   0 ]
```

**k = 3 (via vertex 3):**

```
     0   1   2   3   4
0 [  0   3   5  11   5 ]
1 [  ∞   0  ∞   8   2 ]
2 [  ∞  ∞   0  ∞   6 ]
3 [  ∞  ∞  ∞   0  ∞ ]
4 [  ∞  ∞  ∞   1   0 ]
```

**k = 4 (via vertex 4):**

```
     0   1   2   3   4
0 [  0   3   5   6   5 ]
1 [  ∞   0  ∞   3   2 ]
2 [  ∞  ∞   0   7   6 ]
3 [  ∞  ∞  ∞   0  ∞ ]
4 [  ∞  ∞  ∞   1   0 ]
```

**Final All-Pair Shortest Distances:**

- Shortest path from 0 to 3: 6 (via 0→1→4→3)
- Shortest path from 1 to 3: 3 (via 1→4→3)
- Shortest path from 2 to 3: 7 (via 2→4→3)

**Time Complexity**: O(V³)
**Space Complexity**: O(V²)

---

## Longest Common Subsequence (LCS)

### Q2.1. Discuss the applications of the longest common subsequence (LCS).

**Question 2.1: Discuss the applications of the longest common subsequence (LCS).**

### Introduction to LCS

A **Longest Common Subsequence (LCS)** of two sequences is the longest sequence that appears in both sequences in the same relative order, but not necessarily contiguous.

### Applications of LCS

#### 1. Bioinformatics and DNA Analysis

**Application**: Comparing DNA sequences to find similarities

```
DNA Sequence 1: AGGTAB
DNA Sequence 2: GXTXAYB
LCS: GTAB (common genetic pattern)
```

**Uses**:

- Gene sequence alignment
- Identifying mutations
- Evolutionary analysis
- Protein sequence comparison

#### 2. Version Control Systems (Git, SVN)

**Application**: Finding differences between file versions

```
Old File: "Hello World Program"
New File: "Hello Beautiful World Program"
LCS: "Hello World Program"
Difference: Added "Beautiful"
```

**Uses**:

- Efficient diff algorithms
- Merge conflict resolution
- Patch generation
- Code repository management

#### 3. Text Processing and Plagiarism Detection

**Application**: Comparing documents for similarity

```
Text 1: "The quick brown fox jumps"
Text 2: "A quick brown fox jumps high"
LCS: "quick brown fox jumps" (similarity measure)
```

**Uses**:

- Document similarity measurement
- Plagiarism detection systems
- Text comparison tools
- Content matching algorithms

#### 4. Data Compression

**Application**: Finding repeating patterns for compression

```
Data Stream: ABCABCABC
LCS patterns help identify: ABC repeats 3 times
Compressed: ABC*3
```

#### 5. Speech Recognition

**Application**: Matching spoken words with text patterns

```
Expected: "RECOGNIZE SPEECH"
Actual: "RECOG SPEECH"
LCS: "RECOG SPEECH" (error correction)
```

#### 6. File Comparison and Synchronization

**Application**: Rsync, backup systems

```
File 1: [Block A][Block B][Block C]
File 2: [Block A][Block D][Block C]
LCS: [Block A][Block C] (unchanged blocks)
Sync: Only send Block D
```

### LCS Applications Summary

| Domain                   | Application                               | Benefit                                  |
| ------------------------ | ----------------------------------------- | ---------------------------------------- |
| **Bioinformatics**       | DNA/Protein sequence analysis             | Evolutionary studies, mutation detection |
| **Software Development** | Version control, diff tools               | Efficient change tracking                |
| **Text Processing**      | Plagiarism detection, document comparison | Content similarity analysis              |
| **Data Compression**     | Pattern identification                    | Reduced storage requirements             |
| **Speech Processing**    | Error correction, pattern matching        | Improved recognition accuracy            |
| **File Systems**         | Synchronization, backup                   | Optimized data transfer                  |

### Q2.2. Determine the LCS of `<1,0,0,1,0,1,0,1>` and `<0,1,0,1,1,0,1,1,0>`.

**Question 2.2: Determine the LCS of `<1,0,0,1,0,1,0,1>` and `<0,1,0,1,1,0,1,1,0>`.**

### LCS Algorithm

```
Algorithm: LCS(X, Y)
Input: Sequences X[1..m] and Y[1..n]
Output: Length of LCS and the LCS itself

1. START
2. m = length of X
3. n = length of Y
4. // Create DP table
5. FOR i = 0 TO m DO
6.     FOR j = 0 TO n DO
7.         IF i = 0 OR j = 0 THEN
8.             dp[i][j] = 0
9.         ELSE IF X[i-1] = Y[j-1] THEN
10.            dp[i][j] = dp[i-1][j-1] + 1
11.        ELSE
12.            dp[i][j] = max(dp[i-1][j], dp[i][j-1])
13.        END IF
14.    END FOR
15. END FOR
16.
17. // Backtrack to find LCS
18. i = m, j = n
19. lcs = ""
20. WHILE i > 0 AND j > 0 DO
21.     IF X[i-1] = Y[j-1] THEN
22.         lcs = X[i-1] + lcs
23.         i = i - 1
24.         j = j - 1
25.     ELSE IF dp[i-1][j] > dp[i][j-1] THEN
26.         i = i - 1
27.     ELSE
28.         j = j - 1
29.     END IF
30. END WHILE
31.
32. RETURN dp[m][n], lcs
33. STOP
```

### Applied Example

**Given Sequences:**

- X = `<1,0,0,1,0,1,0,1>` (length = 8)
- Y = `<0,1,0,1,1,0,1,1,0>` (length = 9)

#### Step 1: Build DP Table

**DP Table Construction:**

```
    ""  0  1  0  1  1  0  1  1  0
""   0  0  0  0  0  0  0  0  0  0
 1   0  0  1  1  1  1  1  1  1  1
 0   0  1  1  2  2  2  2  2  2  2
 0   0  1  1  2  2  2  3  3  3  3
 1   0  1  2  2  3  3  3  4  4  4
 0   0  1  2  3  3  3  4  4  4  5
 1   0  1  2  3  4  4  4  5  5  5
 0   0  1  2  3  4  4  5  5  5  6
 1   0  1  2  3  4  4  5  6  6  6
```

#### Step 2: Backtrack to Find LCS

**Backtracking Process:**

Starting from dp[8][9] = 6:

1. (8,9): X[7]=1, Y[8]=0 → Not equal → Move to (7,9)
2. (7,9): X[6]=0, Y[8]=0 → Equal → LCS = "0", Move to (6,8)
3. (6,8): X[5]=1, Y[7]=1 → Equal → LCS = "10", Move to (5,7)
4. (5,7): X[4]=0, Y[6]=1 → Not equal → Move to (5,6)
5. (5,6): X[4]=0, Y[5]=0 → Equal → LCS = "010", Move to (4,5)
6. (4,5): X[3]=1, Y[4]=1 → Equal → LCS = "1010", Move to (3,4)
7. (3,4): X[2]=0, Y[3]=1 → Not equal → Move to (2,4)
8. (2,4): X[1]=0, Y[3]=1 → Not equal → Move to (2,3)
9. (2,3): X[1]=0, Y[2]=0 → Equal → LCS = "01010", Move to (1,2)
10. (1,2): X[0]=1, Y[1]=1 → Equal → LCS = "101010", Move to (0,1)

**Final Answer:**

- **LCS Length**: 6
- **LCS**: `<1,0,1,0,1,0>`

#### Verification

**X**: `<1,0,0,1,0,1,0,1>`
**Y**: `<0,1,0,1,1,0,1,1,0>`
**LCS**: `<1,0,1,0,1,0>`

**In X**: Positions [0,1,3,4,5,6] → `<1,0,1,0,1,0>` ✓
**In Y**: Positions [1,2,3,5,6,8] → `<1,0,1,0,1,0>` ✓

---

## Greedy Programming

### Introduction to Greedy Algorithms

**Greedy Algorithm** makes locally optimal choices at each step, hoping to find a global optimum. It builds a solution piece by piece, always choosing the next piece that offers the most immediate benefit.

#### Characteristics:

1. **Greedy Choice Property**: Local optimal choice leads to global optimum
2. **Optimal Substructure**: Optimal solution contains optimal subproblems
3. **No Backtracking**: Decisions are never reconsidered

#### Applications:

- Minimum Spanning Tree (Prim's, Kruskal's)
- Shortest Path (Dijkstra's)
- Activity Selection Problem
- Huffman Coding

---

## Minimum Spanning Tree Algorithms

### Prim's Algorithm

#### Introduction

**Prim's Algorithm** finds a minimum spanning tree by starting with any vertex and repeatedly adding the minimum weight edge that connects a vertex in the tree to a vertex outside the tree.

#### Algorithm

```
Algorithm: PrimMST(Graph G)
Input: Connected weighted graph G
Output: Minimum Spanning Tree

1. START
2. mstSet = {}
3. key[] = array of size V, initialize all as INFINITY
4. parent[] = array to store MST
5. key[0] = 0  // Start with vertex 0
6. parent[0] = -1
7.
8. FOR count = 0 TO V-1 DO
9.     // Find minimum key vertex not in MST
10.    u = extractMin(key, mstSet)
11.    mstSet[u] = TRUE
12.
13.    // Update key values of adjacent vertices
14.    FOR each vertex v adjacent to u DO
15.        IF v not in mstSet AND weight(u,v) < key[v] THEN
16.            parent[v] = u
17.            key[v] = weight(u,v)
18.        END IF
19.    END FOR
20. END FOR
21.
22. RETURN parent[]
23. STOP
```

#### Example

**Graph:**

```
     (2)      (3)
  0 -------- 1 -------- 2
  |          |          |
(6)|        (8)|        (5)|
  |          |          |
  3 -------- 4 -------- 5
     (5)      (10)
```

**Step-by-Step Execution:**

| Step | Vertex Added | Key Values    | Parent              | MST Edges |
| ---- | ------------ | ------------- | ------------------- | --------- |
| 1    | 0            | [0,2,∞,6,∞,∞] | [-1,-1,-1,-1,-1,-1] | -         |
| 2    | 1            | [0,2,3,6,8,∞] | [-1,0,1,-1,1,-1]    | (0,1)     |
| 3    | 2            | [0,2,3,6,8,5] | [-1,0,1,-1,1,2]     | (1,2)     |
| 4    | 5            | [0,2,3,6,8,5] | [-1,0,1,-1,1,2]     | (2,5)     |
| 5    | 3            | [0,2,3,6,5,5] | [-1,0,1,0,3,2]      | (0,3)     |
| 6    | 4            | [0,2,3,6,5,5] | [-1,0,1,0,3,2]      | (3,4)     |

**Final MST:**

- Edges: (0,1), (1,2), (2,5), (0,3), (3,4)
- Total Weight: 2 + 3 + 5 + 6 + 5 = 21

### Q2. Explain Kruskal's algorithm to find the minimum cost spanning tree with an example.

**Question 2: Explain Kruskal's algorithm to find the minimum cost spanning tree with an example.**

### Kruskal's Algorithm

#### Introduction

**Kruskal's Algorithm** finds a minimum spanning tree by sorting all edges by weight and adding edges one by one, ensuring no cycles are formed using Union-Find data structure.

#### Algorithm

```
Algorithm: KruskalMST(Graph G)
Input: Connected weighted graph G
Output: Minimum Spanning Tree

1. START
2. result = []  // To store MST edges
3. edges = getAllEdges(G)
4. SORT edges by weight in ascending order
5.
6. // Initialize Union-Find
7. FOR each vertex v DO
8.     parent[v] = v
9.     rank[v] = 0
10. END FOR
11.
12. edgeCount = 0
13. i = 0
14. WHILE edgeCount < V-1 AND i < total_edges DO
15.     edge = edges[i]
16.     u = edge.source
17.     v = edge.destination
18.
19.     // Check if adding this edge creates cycle
20.     IF find(u) ≠ find(v) THEN
21.         result[edgeCount] = edge
22.         union(u, v)
23.         edgeCount = edgeCount + 1
24.     END IF
25.     i = i + 1
26. END WHILE
27.
28. RETURN result
29. STOP

// Union-Find Helper Functions
Function find(x):
    IF parent[x] ≠ x THEN
        parent[x] = find(parent[x])  // Path compression
    RETURN parent[x]

Function union(x, y):
    rootX = find(x)
    rootY = find(y)
    IF rank[rootX] < rank[rootY] THEN
        parent[rootX] = rootY
    ELSE IF rank[rootX] > rank[rootY] THEN
        parent[rootY] = rootX
    ELSE
        parent[rootY] = rootX
        rank[rootX] = rank[rootX] + 1
```

#### Applied Example

**Given Graph:**

```
     (10)     (6)      (5)
  0 ------- 1 ------- 2 ------- 3
  |         |         |         |
(6)|       (5)|      (4)|       (6)|
  |         |         |         |
  4 ------- 5 ------- 6 ------- 7
     (3)      (2)      (1)
```

#### Step 1: List and Sort All Edges

**All Edges with Weights:**

```
(6,7) - weight 1
(5,6) - weight 2
(4,5) - weight 3
(2,6) - weight 4
(1,5) - weight 5
(2,3) - weight 5
(1,2) - weight 6
(0,4) - weight 6
(3,7) - weight 6
(0,1) - weight 10
```

#### Step 2: Apply Kruskal's Algorithm

**Process edges in sorted order:**

| Step | Edge  | Weight | Action | Union-Find State              | MST Edges                                   |
| ---- | ----- | ------ | ------ | ----------------------------- | ------------------------------------------- |
| 1    | (6,7) | 1      | Add    | {0},{1},{2},{3},{4},{5},{6,7} | [(6,7)]                                     |
| 2    | (5,6) | 2      | Add    | {0},{1},{2},{3},{4},{5,6,7}   | [(6,7),(5,6)]                               |
| 3    | (4,5) | 3      | Add    | {0},{1},{2},{3},{4,5,6,7}     | [(6,7),(5,6),(4,5)]                         |
| 4    | (2,6) | 4      | Add    | {0},{1},{2,4,5,6,7},{3}       | [(6,7),(5,6),(4,5),(2,6)]                   |
| 5    | (1,5) | 5      | Add    | {0},{1,2,4,5,6,7},{3}         | [(6,7),(5,6),(4,5),(2,6),(1,5)]             |
| 6    | (2,3) | 5      | Add    | {0},{1,2,3,4,5,6,7}           | [(6,7),(5,6),(4,5),(2,6),(1,5),(2,3)]       |
| 7    | (1,2) | 6      | Skip   | Cycle detected                | Same                                        |
| 8    | (0,4) | 6      | Add    | {0,1,2,3,4,5,6,7}             | [(6,7),(5,6),(4,5),(2,6),(1,5),(2,3),(0,4)] |

#### Step 3: Final MST

**Minimum Spanning Tree Edges:**

1. (6,7) - weight 1
2. (5,6) - weight 2
3. (4,5) - weight 3
4. (2,6) - weight 4
5. (1,5) - weight 5
6. (2,3) - weight 5
7. (0,4) - weight 6

**Total Weight**: 1 + 2 + 3 + 4 + 5 + 5 + 6 = 26

**Visual Representation of MST:**

```
  0       1       2 ----- 3
  |       |       |
  |       |       |
  4 ----- 5 ----- 6 ----- 7
```

#### Algorithm Comparison

| Aspect               | Prim's Algorithm         | Kruskal's Algorithm     |
| -------------------- | ------------------------ | ----------------------- |
| **Approach**         | Vertex-based (grow tree) | Edge-based (sort edges) |
| **Data Structure**   | Priority Queue           | Union-Find              |
| **Time Complexity**  | O(E log V)               | O(E log E)              |
| **Space Complexity** | O(V)                     | O(V)                    |
| **Best For**         | Dense graphs             | Sparse graphs           |

---

## Huffman Algorithm

### Q3.1. Write a short note on the Huffman algorithm, explaining various steps with an example.

**Question 3.1: Write a short note on the Huffman algorithm, explaining various steps with an example.**

### Huffman Algorithm Overview

**Huffman Coding** is a greedy algorithm used for lossless data compression. It assigns variable-length codes to characters based on their frequencies - more frequent characters get shorter codes.

#### Key Principles:

1. **Frequency-based encoding**: High frequency → Short code
2. **Prefix property**: No code is prefix of another
3. **Binary tree structure**: Left = 0, Right = 1
4. **Greedy approach**: Build optimal tree bottom-up

### Huffman Algorithm Steps

```
Algorithm: HuffmanCoding(characters[], frequencies[])
Input: Array of characters and their frequencies
Output: Huffman codes for each character

1. START
2. // Step 1: Create leaf nodes
3. FOR each character c with frequency f DO
4.     node = createLeafNode(c, f)
5.     INSERT node into minHeap
6. END FOR
7.
8. // Step 2: Build Huffman tree
9. WHILE minHeap.size > 1 DO
10.    left = EXTRACT_MIN(minHeap)
11.    right = EXTRACT_MIN(minHeap)
12.    merged = createInternalNode(left.freq + right.freq)
13.    merged.left = left
14.    merged.right = right
15.    INSERT merged into minHeap
16. END WHILE
17.
18. // Step 3: Generate codes
19. root = EXTRACT_MIN(minHeap)
20. generateCodes(root, "", codes)
21. RETURN codes
22. STOP

Function generateCodes(node, code, codes):
1. IF node.isLeaf THEN
2.     codes[node.character] = code
3.     RETURN
4. END IF
5. generateCodes(node.left, code + "0", codes)
6. generateCodes(node.right, code + "1", codes)
```

### Detailed Example

**Problem**: Compress the string "PROGRAMMING"

#### Step 1: Calculate Character Frequencies

**Character Count:**

```
P: 1, R: 2, O: 1, G: 2, A: 1, M: 2, I: 1, N: 1
```

**Frequency Table:**
| Character | Frequency |
|-----------|-----------|
| P | 1 |
| R | 2 |
| O | 1 |
| G | 2 |
| A | 1 |
| M | 2 |
| I | 1 |
| N | 1 |

#### Step 2: Build Huffman Tree

**Initial Min-Heap:**

```
P(1), O(1), A(1), I(1), N(1), R(2), G(2), M(2)
```

**Tree Building Process:**

**Iteration 1:** Combine P(1) and O(1)

```
Min-Heap: A(1), I(1), N(1), (2), R(2), G(2), M(2)

Tree:  (2)
      /   \
    P(1) O(1)
```

**Iteration 2:** Combine A(1) and I(1)

```
Min-Heap: N(1), (2), (2), R(2), G(2), M(2)

Trees: (2)     (2)
      /  \    /  \
    P(1) O(1) A(1) I(1)
```

**Iteration 3:** Combine N(1) and first (2)

```
Min-Heap: (2), R(2), G(2), M(2), (3)

Trees: (2)     (3)
      /  \    /    \
    A(1) I(1) N(1) (2)
                  /  \
                P(1) O(1)
```

**Iteration 4:** Combine two (2) nodes - R(2) and G(2)

```
Min-Heap: M(2), (3), (4)

Trees: (2)     (3)        (4)
      /  \    /    \     /    \
    A(1) I(1) N(1) (2)  R(2)  G(2)
                  /  \
                P(1) O(1)
```

**Iteration 5:** Combine M(2) and (3)

```
Min-Heap: (4), (5)

Trees:    (4)         (5)
         /    \      /    \
       R(2)  G(2)  M(2)  (3)
                         /    \
                       N(1)   (2)
                             /    \
                           P(1)  O(1)
```

**Iteration 6:** Combine (4) and (5)

```
Final Huffman Tree:
                (9)
               /    \
            (4)      (5)
           /    \   /    \
         R(2)  G(2) M(2) (3)
                          /    \
                        N(1)   (2)
                              /    \
                            P(1)  O(1)
```

#### Step 3: Generate Huffman Codes

**Code Generation (Left=0, Right=1):**

| Character | Path from Root             | Huffman Code |
| --------- | -------------------------- | ------------ |
| R         | Left, Left                 | 00           |
| G         | Left, Right                | 01           |
| M         | Right, Left                | 10           |
| N         | Right, Right, Left         | 110          |
| P         | Right, Right, Right, Left  | 1110         |
| O         | Right, Right, Right, Right | 1111         |
| A         | Right, Right, Right, Left  | 1110         |
| I         | Right, Right, Right, Right | 1111         |

**Wait, let me recalculate this properly:**

**Corrected Tree Structure:**

```
                    (11)
                   /    \
                (5)      (6)
               /   \    /    \
             (2)   (3) M(2)  (4)
            /  \  /  \      /    \
          A(1) I(1) N(1) (2)   R(2) G(2)
                        /  \
                      P(1) O(1)
```

**Corrected Huffman Codes:**

| Character | Code | Length |
| --------- | ---- | ------ |
| A         | 000  | 3      |
| I         | 001  | 3      |
| N         | 010  | 3      |
| P         | 0110 | 4      |
| O         | 0111 | 4      |
| M         | 10   | 2      |
| R         | 110  | 3      |
| G         | 111  | 3      |

#### Step 4: Encode the String

**Original String**: "PROGRAMMING"
**Encoded**:

- P: 0110
- R: 110
- O: 0111
- G: 111
- R: 110
- A: 000
- M: 10
- M: 10
- I: 001
- N: 010
- G: 111

**Final Encoded String**: `0110 110 0111 111 110 000 10 10 001 010 111`
**Compressed**: `01101100111111110000101000101011`

#### Step 5: Compression Analysis

**Original String**: "PROGRAMMING" (11 characters)
**ASCII Encoding**: 11 × 8 = 88 bits
**Huffman Encoding**: 32 bits
**Compression Ratio**: 88/32 = 2.75:1

### Advantages and Applications

**Advantages:**

- Optimal prefix-free codes
- Lossless compression
- Efficient for files with skewed character frequencies

**Applications:**

- GZIP compression
- JPEG image compression (modified version)
- ZIP file format
- Network data transmission

**Time Complexity**: O(n log n) where n is the number of unique characters
**Space Complexity**: O(n)

---

## Summary

This unit covered advanced algorithms including:

1. **Strassen's Matrix Multiplication** - O(n^2.807) complexity improvement
2. **Dynamic Programming** approaches for shortest paths
3. **Dijkstra's Algorithm** - Single source shortest path with non-negative weights
4. **Bellman-Ford Algorithm** - Handles negative weights, detects negative cycles
5. **Floyd-Warshall Algorithm** - All-pair shortest paths in O(V³)
6. **Longest Common Subsequence** - Applications and DP solution
7. **Greedy Algorithms** - Prim's and Kruskal's for MST
8. **Huffman Coding** - Optimal prefix-free compression

Each algorithm demonstrates different problem-solving paradigms and optimization techniques essential for efficient algorithm design.
