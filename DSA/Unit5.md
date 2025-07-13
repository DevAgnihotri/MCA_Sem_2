# DSA Unit 5: Advanced Algorithms

---

## Matrix Multiplication: Strassen's Algorithm

(https://www.youtube.com/watch?v=9GQwTbJozZg&ab_channel=ExamAasaanHai%21%21%21)

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

#### Key Characteristics of Dynamic Programming

1. **Optimal Substructure**: The optimal solution to a problem can be constructed from optimal solutions of its subproblems.
2. **Overlapping Subproblems**: The problem can be broken down into subproblems which are reused multiple times.
3. **Memoization**: Solutions to subproblems are stored to avoid redundant computations, improving efficiency.

#### Dynamic Programming Approaches

- **Top-Down (Memoization)**: Solve the problem recursively and store the results of subproblems in a table (usually a hash map or array). When a subproblem is encountered again, its solution is retrieved from the table instead of recomputing.
- **Bottom-Up (Tabulation)**: Solve all possible subproblems iteratively, starting from the smallest, and build up solutions to larger subproblems using a table. This approach avoids recursion and fills the table in a systematic way.

Both approaches ensure that each subproblem is solved only once, leading to significant performance improvements over naive recursive solutions.

---

## Shortest Path Algorithms

### Dijkstra's Algorithm

#### Introduction

**Dijkstra's Algorithm** finds the shortest path from a source vertex to all other vertices in a weighted graph with non-negative edge weights.

#### Algorithm

**Dijkstra's Shortest Path Algorithm:**

1. **Initialize the algorithm**:

   - Set the distance to the source vertex as zero
   - Set the distance to all other vertices as infinity
   - Mark all vertices as unvisited
   - Create a priority queue and add the source vertex with distance 0

2. **Main processing loop** (continue until priority queue is empty):

   - **Extract the vertex** with minimum distance from the priority queue
   - **Skip if already visited** to avoid reprocessing
   - **Mark the current vertex** as visited

3. **Update neighboring vertices**:

   - **For each unvisited neighbor** of the current vertex:
     - **Calculate alternative distance** = current vertex distance + edge weight
     - **If alternative distance is shorter** than the stored distance:
       - **Update the neighbor's distance** to the shorter value
       - **Update the neighbor's predecessor** to current vertex
       - **Add the neighbor** to priority queue with new distance

4. **Result**: The algorithm produces:
   - **Shortest distances** from source to all reachable vertices
   - **Predecessor information** to reconstruct actual shortest paths

**Key Principle**: Always process the closest unvisited vertex next, ensuring optimal distances are found in order of increasing distance from source.

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

**Bellman-Ford Shortest Path Algorithm:**

1. **Initialize distances**:

   - Set the distance to the source vertex as zero
   - Set the distance to all other vertices as infinity
   - Initialize predecessor array to track shortest paths

2. **Relaxation phase** (repeat V-1 times, where V is number of vertices):

   - **For each iteration**:
     - **Examine every edge** in the graph
     - **For each edge (u,v)** with weight w:
       - **Calculate potential shorter path**: distance[u] + w
       - **If this path is shorter** than current distance[v]:
         - **Update distance[v]** to the shorter value
         - **Set predecessor[v]** to vertex u

3. **Negative cycle detection** (one additional check):

   - **Examine every edge** one more time
   - **If any edge can still be relaxed** (distance can be reduced):
     - **Report negative cycle detected** in the graph
     - **Terminate algorithm** as shortest paths are undefined

4. **Result**:
   - **Return shortest distances** if no negative cycle exists
   - **Return negative cycle warning** if negative cycle is detected

**Key Features**:

- **Handles negative edge weights** unlike Dijkstra's algorithm
- **Detects negative cycles** which make shortest paths undefined
- **Guaranteed to find shortest paths** in graphs without negative cycles

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

### Floyd-Warshall Algorithm
(https://www.youtube.com/watch?v=DCDwITxLUZc&ab_channel=XtraLectures)
#### Introduction

**Floyd-Warshall Algorithm** finds the shortest paths between all pairs of vertices in a weighted graph. It works with negative edges but not negative cycles.

#### Algorithm

**Floyd-Warshall All-Pair Shortest Path Algorithm:**

1. **Initialize the distance matrix**:

   - **Create a matrix** of size n×n where n is the number of vertices
   - **For each pair of vertices (i,j)**:
     - **If i equals j**: set distance to 0 (vertex to itself)
     - **If direct edge exists**: set distance to the edge weight
     - **Otherwise**: set distance to infinity (no direct path)

2. **Main algorithm - try each vertex as intermediate**:

   - **For each possible intermediate vertex k** (from 0 to n-1):
     - **For each source vertex i** (from 0 to n-1):
       - **For each destination vertex j** (from 0 to n-1):
         - **Calculate path through k**: distance[i][k] + distance[k][j]
         - **If path through k is shorter** than current direct path:
           - **Update distance[i][j]** to the shorter path distance
           - **This represents finding a better route** from i to j via k

3. **Progressive improvement**:

   - **After processing vertex k**: all shortest paths using vertices 0 through k are optimal
   - **Each iteration** potentially discovers shorter paths by using the new intermediate vertex
   - **Final result** contains shortest paths between all pairs of vertices

4. **Result interpretation**:
   - **distance[i][j]** gives the shortest path distance from vertex i to vertex j
   - **Infinity values** indicate no path exists between those vertices
   - **Algorithm handles negative edges** but assumes no negative cycles

**Key Insight**: By systematically considering each vertex as a potential intermediate point, the algorithm discovers all possible shortest routes through the graph.

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
(https://www.youtube.com/watch?v=XeqwjB7hVZ0&ab_channel=Alltechnicalsolution)
### Q2.1. Discuss the applications of the longest common subsequence (LCS).

**Question 2.1: Discuss the applications of the longest common subsequence (LCS).**

### Introduction to LCS

A **Longest Common Subsequence (LCS)** of two sequences is the longest sequence that appears in both sequences in the same relative order, but not necessarily contiguous.

### Applications of LCS
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

**Longest Common Subsequence Algorithm:**

1. **Setup the dynamic programming table**:

   - **Create a 2D table** of size (m+1) × (n+1) where m and n are lengths of input sequences
   - **Initialize first row and column** to zero (representing empty sequence comparisons)

2. **Fill the DP table using bottom-up approach**:

   - **For each position (i,j)** in the table:
     - **If characters match** (X[i-1] equals Y[j-1]):
       - **Take diagonal value and add 1**: dp[i][j] = dp[i-1][j-1] + 1
       - **This represents extending the LCS** by including the matching character
     - **If characters don't match**:
       - **Take maximum** of left cell (dp[i][j-1]) and top cell (dp[i-1][j])
       - **This represents the best LCS** found by excluding one character

3. **Backtrack to reconstruct the actual LCS**:

   - **Start from bottom-right corner** of the filled table
   - **While both indices are positive**:
     - **If characters match**: add character to LCS, move diagonally up-left
     - **If top cell is larger**: move up (exclude current row character)
     - **Otherwise**: move left (exclude current column character)

4. **Build the result**:
   - **LCS length**: value in dp[m][n] (bottom-right corner)
   - **LCS sequence**: characters collected during backtracking (in reverse order)

**Key Principle**: The algorithm builds optimal solutions for smaller subproblems and combines them to solve larger problems, ensuring the longest common subsequence is found efficiently.

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

(https://www.youtube.com/watch?v=f30rxGvPWPo&ab_channel=Dr.GajendraPurohit)

## Minimum Spanning Tree Algorithms

### Minimum Cost Spanning Tree (MCST)

#### What is a Minimum Cost Spanning Tree?

A **Minimum Cost Spanning Tree (MCST)** of a connected, undirected, weighted graph is a subset of the edges that connects all the vertices together, without any cycles, and with the minimum possible total edge weight.

- **Spanning Tree**: A tree that includes all the vertices of the graph.
- **Minimum Cost**: The sum of the weights of the edges in the tree is as small as possible.

#### Properties

- Contains all vertices of the original graph.
- Has exactly (V-1) edges if there are V vertices.
- No cycles (i.e., it is a tree).
- The total weight is minimized.

#### Example

Consider the following graph:

```
   (2)      (3)
  A ------ B ------ C
  |        |        |
(6)|      (8)|      (5)|
  |        |        |
  D ------ E ------ F
   (5)      (10)
```

**Vertices**: A, B, C, D, E, F  
**Edges with weights**:  
- AB: 2
- BC: 3
- AE: 8
- AC: not directly connected
- AD: 6
- DE: 5
- EF: 10
- CF: 5

**Step-by-step MCST construction (using Kruskal's or Prim's algorithm):**

1. **Choose the smallest edge**: AB (2)
2. **Next smallest**: BC (3)
3. **Next**: AD (6)
4. **Next**: CF (5)
5. **Next**: DE (5)

Now, all vertices are connected with 5 edges (for 6 vertices), and no cycles are formed.

**Edges in MCST**: AB, BC, AD, CF, DE  
**Total Cost**: 2 + 3 + 6 + 5 + 5 = **21**

#### Visualization

```
   (2)      (3)
  A ------ B ------ C
  |                |
(6)|              (5)|
  |                |
  D ------ E      F
   (5)
```
(Edges AE and EF are not included as they would increase the total cost or form cycles.)

#### Applications

- Network design (telephone, electrical, computer networks)
- Road construction planning
- Cluster analysis

#### Summary

A minimum cost spanning tree connects all vertices with the least total edge weight and no cycles. Algorithms like Prim's and Kruskal's are commonly used to find MCSTs efficiently.

### Prim's Algorithm

#### Introduction

**Prim's Algorithm** finds a minimum spanning tree by starting with any vertex and repeatedly adding the minimum weight edge that connects a vertex in the tree to a vertex outside the tree.

#### Algorithm

**Prim's Minimum Spanning Tree Algorithm:**

1. **Initialize the algorithm**:

   - **Create an empty MST set** to track vertices included in the spanning tree
   - **Set up a key array** with all values as infinity except the starting vertex (set to 0)
   - **Initialize parent array** to track the MST structure
   - **Choose any vertex as starting point** (typically vertex 0)

2. **Main loop** (repeat until all vertices are included):

   - **Find the minimum key vertex** that is not yet in the MST set
   - **Add this vertex** to the MST set
   - **Mark it as processed** to avoid revisiting

3. **Update adjacent vertices**:

   - **For each neighbor** of the newly added vertex:
     - **If neighbor is not in MST** and **edge weight is smaller** than current key value:
       - **Update the neighbor's key** to the smaller edge weight
       - **Set the neighbor's parent** to the current vertex
       - **This represents finding a cheaper connection** to the growing MST

4. **Continue growing the tree**:

   - **Each iteration adds one vertex** with the minimum cost edge connection
   - **The algorithm ensures** that at each step, the cheapest possible edge is chosen
   - **Process continues** until all vertices are connected

5. **Result**:
   - **Parent array contains** the MST structure
   - **Total weight** is the sum of all selected edge weights
   - **The tree is guaranteed** to be minimum cost and span all vertices

**Key Strategy**: Always choose the cheapest edge that connects a vertex outside the current tree to a vertex inside the tree, ensuring minimum total cost.

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

(https://www.youtube.com/watch?v=1BVDvgDGKSE&ab_channel=CSEngineeringGyan)

### Kruskal's Algorithm

#### Introduction

**Kruskal's Algorithm** finds a minimum spanning tree by sorting all edges by weight and adding edges one by one, ensuring no cycles are formed using Union-Find data structure.

#### Algorithm

**Kruskal's Minimum Spanning Tree Algorithm:**

1. Remove all Loop edges. ex;....
2. Remove all parallel edges. ex;...
3. Arrange all edges in increasing weight
4. Start adding edges to the beggining from the one with least weight
5. Avoid edges thaat create a loop
6. After all edges are added, then check it is a MST or not
   - All vertices covered
   - Edges = vertices - 1

7. If yes then calculte total weight by adding all values of edges.



**Key Strategy**: Process edges from cheapest to most expensive, adding each edge only if it connects previously disconnected components, thus avoiding cycles while minimizing total cost.

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

**Huffman Coding Algorithm:**

1. **Analyze character frequencies**:

   - **Count the frequency** of each character in the input text
   - **Create leaf nodes** for each character with its frequency
   - **Add all leaf nodes** to a priority queue (min-heap) ordered by frequency

2. **Build the Huffman tree** using a greedy approach:

   - **While more than one node exists** in the priority queue:
     - **Extract the two nodes** with lowest frequencies
     - **Create a new internal node** with frequency equal to sum of the two nodes
     - **Set the two extracted nodes** as left and right children
     - **Insert the new internal node** back into the priority queue

3. **Generate binary codes** from the completed tree:

   - **Start from the root** and traverse to each leaf
   - **Assign '0' for left branches** and '1' for right branches
   - **The path from root to leaf** gives the binary code for that character
   - **More frequent characters** get shorter codes (closer to root)

4. **Encode the text**:

   - **Replace each character** in the original text with its corresponding binary code
   - **Concatenate all codes** to form the compressed bit stream

5. **Verification and analysis**:
   - **Calculate compression ratio** by comparing original and compressed sizes
   - **Ensure prefix property**: no code is a prefix of another code
   - **Store the tree structure** for later decoding

**Tree Construction Helper Process:**

- **Find minimum frequency nodes**: Always select the two nodes with smallest frequencies
- **Create parent node**: Combine selected nodes under a new parent with combined frequency
- **Maintain heap property**: Keep the priority queue ordered after each insertion

**Code Generation Process:**

- **Traverse recursively**: Visit left child (append '0') and right child (append '1')
- **Record leaf codes**: When reaching a leaf, save the accumulated path as the character's code
- **Build encoding table**: Create a lookup table mapping characters to their binary codes

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
