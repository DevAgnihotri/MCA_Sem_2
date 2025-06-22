# Graph Data Structure: Complete Guide

---

## Introduction to Graphs

### Q6. Define graph. List the various graph traversal techniques.

### Q8. Define Graph. List some applications of the graph.

**Question 6 & 8: Define graph. List the various graph traversal techniques and applications of the graph.**

A **graph** is a non-linear data structure consisting of a collection of vertices (nodes) and edges that connect pairs of vertices. It is used to represent relationships between different entities.

#### Mathematical Definition:

- A graph G is defined as G = (V, E) where:
  - V = Set of vertices (nodes)
  - E = Set of edges (connections between vertices)

#### Graph Traversal Techniques:

1. **Depth First Search (DFS)**
2. **Breadth First Search (BFS)**

#### Applications of Graphs

| Application Area            | Examples                                                             |
| --------------------------- | -------------------------------------------------------------------- |
| **Social Networks**         | Modeling friendships (Facebook), professional connections (LinkedIn) |
| **Transportation**          | Road maps, airline routes, railway networks, GPS navigation          |
| **Computer Networks**       | Internet topology, data routing, network design                      |
| **Web Applications**        | Web page linking (Google PageRank), site navigation, crawling        |
| **Game Development**        | Pathfinding (A\* algorithm), AI decision trees, level maps           |
| **Biology**                 | Gene sequencing, protein interaction networks, food webs             |
| **Economics**               | Supply chain networks, market analysis, financial transactions       |
| **Artificial Intelligence** | Knowledge graphs, neural network architectures, reasoning systems    |

Graphs are widely used to represent and solve problems involving relationships and connections in various domains.

---

## Graph Terminology

### Basic Terms:

| Term                   | Definition                                        | Example                     |
| ---------------------- | ------------------------------------------------- | --------------------------- |
| **Vertex/Node**        | A point in the graph                              | Cities in a map             |
| **Edge**               | A connection between two vertices                 | Roads between cities        |
| **Adjacent Vertices**  | Two vertices connected by an edge                 | Connected cities            |
| **Degree**             | Number of edges connected to a vertex             | Number of roads from a city |
| **Path**               | Sequence of vertices connected by edges           | Route from city A to city B |
| **Cycle**              | A path that starts and ends at the same vertex    | Round trip route            |
| **Connected Graph**    | Every vertex is reachable from every other vertex | All cities are connected    |
| **Disconnected Graph** | Some vertices are not reachable from others       | Isolated islands            |

### Q10. Differentiate between directed and Undirected graph.

**Question 10: Differentiate between directed and Undirected graph.**

| Aspect             | Directed Graph (Digraph)                                     | Undirected Graph                                        |
| ------------------ | ------------------------------------------------------------ | ------------------------------------------------------- |
| **Edge Direction** | Edges have a specific direction (arrows)                     | Edges have no direction                                 |
| **Representation** | A → B (edge from A to B only)                                | A — B (edge connects A and B both ways)                 |
| **Degree Types**   | In-degree (incoming), Out-degree (outgoing)                  | Degree (total number of edges)                          |
| **Adjacency**      | If A → B, A is adjacent to B, but not necessarily vice versa | If A — B, both A and B are adjacent to each other       |
| **Examples**       | Twitter followers, web links, task scheduling                | Facebook friends, undirected roads, electrical circuits |
| **Notation**       | (u, v) ≠ (v, u)                                              | (u, v) = (v, u)                                         |

#### Visual Example:

```
Directed Graph:          Undirected Graph:
A → B → C               A — B — C
↓   ↓                   |   |
D → E                   D — E
```

### Q9. Explain Cycle and Hamilton cycle in graph.

**Question 9: Explain Cycle and Hamilton cycle in graph.**

#### Cycle:

- A **cycle** is a path in a graph that starts and ends at the same vertex, with no other vertex repeated.
- **Simple cycle**: No vertex is repeated except the starting/ending vertex.

#### Hamilton Cycle:

- A **Hamilton cycle** is a special type of cycle that visits every vertex in the graph exactly once and returns to the starting vertex.
- Not all graphs have Hamilton cycles.

**Example:**

```
Graph:     A — B
           |   |
           D — C

Simple Cycle: A → B → C → D → A
Hamilton Cycle: A → B → C → D → A (visits all vertices exactly once)
```

| Feature            | Simple Cycle                                 | Hamilton Cycle                                   |
|--------------------|----------------------------------------------|--------------------------------------------------|
| **Vertex Visit**   | May skip some vertices                       | Must visit every vertex exactly once              |
| **Definition**     | Any closed path with no repeated vertices    | Closed path that visits every vertex exactly once |
| **Existence**      | Common in many graphs                        | Exists only in certain graphs                     |

---

## Graph Representations in Memory

### Q1, Q2, Q3, Q4, Q5. Different ways to represent graphs in computer memory.

**Questions 1-5: What are the different ways the graph is represented in computer memory? Explain with suitable example.**

There are three main ways to represent graphs in computer memory:

### 1. Adjacency Matrix

**Definition:** A 2D array where entry (i,j) indicates whether there's an edge between vertex i and vertex j.

#### For Undirected Graph:

- Matrix[i][j] = 1 if there's an edge between vertex i and j
- Matrix[i][j] = 0 if there's no edge
- Matrix is symmetric (Matrix[i][j] = Matrix[j][i])

#### For Directed Graph:

- Matrix[i][j] = 1 if there's an edge from vertex i to j
- Matrix may not be symmetric

#### Example:

```
Graph:     0 — 1
           |   |
           3 — 2

Adjacency Matrix:
    0  1  2  3
0 [ 0  1  0  1 ]
1 [ 1  0  1  0 ]
2 [ 0  1  0  1 ]
3 [ 1  0  1  0 ]
```

#### Advantages and Disadvantages:

| Advantages                        | Disadvantages                                  |
| --------------------------------- | ---------------------------------------------- |
| ✓ Simple and easy to implement    | ✗ High space complexity: O(V²)                 |
| ✓ Constant time edge lookup: O(1) | ✗ Inefficient for sparse graphs (wastes space) |
| ✓ Quick to check if edge exists   | ✗ Adding or removing vertices is costly        |

---

### 2. Adjacency List

**Definition:** An array of lists where each list contains the neighbors of a vertex.

#### Implementation:

- Array of size V (number of vertices)
- Each array element points to a list of adjacent vertices

#### Example:

```
Graph:     0 — 1
           |   |
           3 — 2

Adjacency List:
0: [1, 3]
1: [0, 2]
2: [1, 3]
3: [0, 2]
```

#### Advantages and Disadvantages:

| Advantages                       | Disadvantages                                    |
| -------------------------------- | ------------------------------------------------ |
| ✓ Space efficient: O(V + E)      | ✗ Edge lookup: O(degree of vertex)               |
| ✓ Well-suited for sparse graphs  | ✗ Not cache-friendly                             |
| ✓ Easy to iterate over neighbors | ✗ Slightly more complex to implement than matrix |

---

## Comparison of Graph Representations

| Operation            | Adjacency Matrix | Adjacency List |
| -------------------- | ---------------- | -------------- |
| **Space Complexity** | O(V²)            | O(V + E)       |
| **Add Edge**         | O(1)             | O(1)           |
| **Remove Edge**      | O(1)             | O(V)           |
| **Check Edge**       | O(1)             | O(V)           |
| **Find Neighbors**   | O(V)             | O(degree)      |
| **Best For**         | Dense graphs     | Sparse graphs  |

---

## Graph Traversal Algorithms

### Q7. Write and explain the breadth first search and depth first search traversal algorithm. What are their complexities?

**Question 7: Write and explain the breadth first search and depth first search traversal algorithm. What are their complexities?**

## Depth First Search (DFS)

### Q1. Algorithm to do DFS in the graph. Apply that algorithm on given graph to compute DFS Tree.

**Question 1: Discuss various methods to represent graph in the memory, Also write down algorithm to do DFS in the graph. Apply that algorithm on given graph to compute DFS Tree.**

### DFS Algorithm:

**Definition:**  
Depth First Search (DFS) is a graph traversal technique that starts at a chosen node (vertex) and explores as far as possible along each branch before backtracking. In DFS, a node is visited, then one of its unvisited neighbors is selected for further exploration, continuing deeper until reaching a node with no unvisited neighbors. At that point, the algorithm backtracks to the previous node and continues the process until all nodes are visited.

**Key Points:**

- DFS uses a stack data structure, either explicitly or through recursion.
- The traversal goes deep into the graph before exploring siblings (other neighbors).
- DFS is useful for tasks such as finding connected components, detecting cycles, and solving puzzles (like mazes).

**Example (Step-by-step):**

1. Start at the source node (e.g., node 0).
2. Mark it as visited.
3. Visit one of its unvisited neighbors (e.g., node 1).
4. Continue visiting unvisited neighbors (e.g., node 2, then node 3).
5. If a node with no unvisited neighbors is reached, backtrack to the previous node and check for other unvisited neighbors.
6. Repeat until all nodes are visited.

DFS explores every path from the starting node as deeply as possible before moving to another path.

#### Pseudocode:

```
DFS(graph, vertex, visited):
    1. Mark vertex as visited
    2. Process/print vertex
    3. For each adjacent vertex 'adj' of vertex:
        a. If adj is not visited:
            i. DFS(graph, adj, visited)
```

#### DFS Example:

```
Graph:     0 — 1
           |   |
           3 — 2

Starting from vertex 0:
DFS Traversal: 0 → 1 → 2 → 3

DFS Tree:
    0
    |
    1
    |
    2
    |
    3
```

#### Time and Space Complexity:

- **Time Complexity:** O(V + E)
  - V = number of vertices
  - E = number of edges
- **Space Complexity:** O(V) for the recursion stack

---

## Breadth First Search (BFS)

### BFS Algorithm:

**Definition:**  
Breadth First Search (BFS) is a graph traversal technique that explores the graph level by level, visiting all nodes at the current "breadth" (distance from the source) before moving to nodes at the next level. Starting from a chosen source vertex, BFS visits all its direct neighbors first, then their neighbors, and so on, expanding outward in layers. This method guarantees finding the shortest path (fewest edges) from the source to any other reachable vertex in an unweighted graph.

#### Algorithm Steps:

1. Start from a source vertex
2. Mark it as visited and add to queue
3. While queue is not empty:
   - Remove vertex from front of queue
   - Process the vertex
   - Add all unvisited adjacent vertices to queue and mark as visited

#### Pseudocode:

```
BFS(graph, start):
    1. Create a queue and add start vertex
    2. Mark start as visited
    3. While queue is not empty:
        a. vertex = dequeue()
        b. Process/print vertex
        c. For each adjacent vertex 'adj' of vertex:
            i. If adj is not visited:
                - Mark adj as visited
                - Enqueue adj
```

#### BFS Example:

```
Graph:     0 — 1
           |   |
           3 — 2

Starting from vertex 0:
BFS Traversal: 0 → 1 → 3 → 2

BFS Tree:
      0
     / \
    1   3
    |   |
    2   (connected to 2)
```

#### Time and Space Complexity:

- **Time Complexity:** O(V + E)
- **Space Complexity:** O(V) for the queue

---

## Comparison: DFS vs BFS

| Aspect              | DFS (Depth First Search)                                | BFS (Breadth First Search)                                         |
| ------------------- | ------------------------------------------------------- | ------------------------------------------------------------------ |
| **Data Structure**  | Stack (implicit via recursion or explicit stack)        | Queue (FIFO)                                                       |
| **Memory Usage**    | O(depth/height of graph/tree)                           | O(width/level of graph/tree)                                       |
| **Path Finding**    | May not find the shortest path                          | Always finds the shortest path (unweighted graphs)                 |
| **Implementation**  | Simple (often recursive)                                | Slightly more complex (uses queue)                                 |
| **Applications**    | Cycle detection, topological sort, connected components | Shortest path, level-order traversal, finding connected components |
| **Traversal Order** | Explores as deep as possible before backtracking        | Explores all neighbors at current level before going deeper        |

---

## Connected Components

### Definition:

A **connected component** in an undirected graph is a maximal set of vertices such that there is a path between every pair of vertices in the set.

### Finding Connected Components:

1. Start DFS/BFS from any unvisited vertex
2. All vertices visited in this traversal form one connected component
3. Repeat for remaining unvisited vertices

### Example:

```
Graph:     0 — 1    4 — 5
           |        |
           2 — 3    6

Connected Components:
Component 1: {0, 1, 2, 3}
Component 2: {4, 5, 6}
```

---

## Summary Table: Graph Concepts

| Concept                    | Key Points                                   | Applications                      |
| -------------------------- | -------------------------------------------- | --------------------------------- |
| **Graph Representation**   | Matrix: O(V²), List: O(V+E), Edge List: O(E) | Choose based on graph density     |
| **DFS**                    | Deep exploration, uses stack/recursion       | Cycle detection, topological sort |
| **BFS**                    | Level-wise exploration, uses queue           | Shortest path, level-order        |
| **Connected Components**   | Separate groups of connected vertices        | Network analysis, clustering      |
| **Directed vs Undirected** | One-way vs two-way edges                     | Web graphs vs social networks     |

---

## PYQ

1. Discuss various methods to represent graph in the memory, Also write down algorithm to do DFS in the graph. Apply that algorithm on given graph to compute DFS Tree
2. What are the different ways the graph is represented in computer memory? Explain with suitable example
3. What are the different ways the graph is represented in computer memory? Explain with suitable example.
4. What are the different ways the graph is represented in computer memory? Explain with suitable example
5. Explain a method to store a graph in computer.
6. Define graph. List the various graph traversal techniques.
7. Write and explain the breadth first search and depth first search traversal algorithm. What are their complexities?
8. Define Graph. List some applications of the graph.
9. Explain Cycle and Hamilton cycle in graph.
10. Differentiate between directed and Undirected graph.
