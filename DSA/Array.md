# Arrays

## Definition

An array is a collection of elements, all of the same type, stored in a continuous block of memory. Each element can be accessed using its index, starting from 0.

## Single Dimensional Arrays

A single dimensional array is a simple list of elements. For example, an array of 5 integers:

```c
int numbers[5] = {1, 2, 3, 4, 5};
```

Here, `numbers[0]` is 1, `numbers[1]` is 2, and so on.

## Multidimensional Arrays

A multidimensional array is an array of arrays. The most common is a two-dimensional array, which can be thought of as a table with rows and columns.

```c
int matrix[2][3] = {
    {1, 2, 3},
    {4, 5, 6}
};
```

Here, `matrix[0][1]` is 2, and `matrix[1][2]` is 6.

## 2D Arrays and Their Applications

A **2D array** is an array of arrays, often visualized as a table with rows and columns. Each element is accessed using two indices: one for the row and one for the column.

### Applications of 2D Arrays

- **Matrices in Mathematics:** Used for matrix operations such as addition, multiplication, and transposition.
- **Image Processing:** Images are stored as 2D arrays of pixel values.
- **Game Boards:** Representing grids in games like chess, sudoku, or tic-tac-toe.
- **Tabular Data:** Storing data in rows and columns, such as spreadsheets or tables.
- **Graph Representations:** Adjacency matrices for representing graphs.

## Representation of Arrays

Arrays are stored in memory as a sequence of elements placed next to each other. The index helps to calculate the memory address of each element. For example, in a single dimensional array, the address of `arr[i]` is calculated as:

```
Base address + (i * size of each element)
```

This makes accessing any element fast and efficient.

## Row Major Order and Column Major Order

When storing multidimensional arrays (like 2D arrays) in memory, there are two common ways to arrange the elements: **Row Major Order** and **Column Major Order**.

### Row Major Order

- In Row Major Order, all elements of the first row are stored in memory first, followed by all elements of the second row, and so on.
- This is the default in languages like C and C++.

**Example:**

For a 2x3 array:

```c
int matrix[2][3] = {
    {1, 2, 3},
    {4, 5, 6}
};
```

The memory layout will be: `1, 2, 3, 4, 5, 6`

### Column Major Order

- In Column Major Order, all elements of the first column are stored first, then all elements of the second column, and so on.
- This is used in languages like Fortran.

**Example:**

For the same 2x3 array, the memory layout will be: `1, 4, 2, 5, 3, 6`

---

**So, the address of `Arr[20][50]` is `9200`.**

## Sparse Matrix

A **sparse matrix** is a matrix in which most of the elements are zero. In contrast, a **dense matrix** has most of its elements as non-zero values.

### Important Properties of Sparse Matrices

- **Memory Efficiency:** Since most elements are zero, sparse matrices can be stored efficiently by only keeping track of non-zero elements and their positions.
- **Faster Computations:** Operations like addition, multiplication, and transpose can be optimized by ignoring zero elements.
- **Special Storage Formats:** Common formats include Coordinate List (COO), Compressed Sparse Row (CSR), and Compressed Sparse Column (CSC).

### Example

Consider the following 4x5 matrix:

```
0  0  3  0  4
0  0  5  7  0
0  0  0  0  0
0  2  6  0  0
```

Most elements are zero. In COO format, we only store non-zero values and their coordinates:

| Row | Col | Value |
| --- | --- | ----- |
| 0   | 2   | 3     |
| 0   | 4   | 4     |
| 1   | 2   | 5     |
| 1   | 3   | 7     |
| 3   | 1   | 2     |
| 3   | 2   | 6     |

This reduces memory usage and speeds up matrix operations.

## Differences Between Arrays and Linked Lists

| Feature                 | Arrays                                         | Linked Lists                                     |
| ----------------------- | ---------------------------------------------- | ------------------------------------------------ |
| **Memory Allocation**   | Contiguous block of memory                     | Non-contiguous, nodes can be scattered in memory |
| **Size**                | Fixed at creation                              | Dynamic, can grow or shrink at runtime           |
| **Access Time**         | O(1) random access via index                   | O(n) access, requires traversal from head        |
| **Insertion**           | Costly (O(n)), elements may need to be shifted | Efficient (O(1)) if pointer to node is known     |
| **Deletion**            | Costly (O(n)), elements may need to be shifted | Efficient (O(1)) if pointer to node is known     |
| **Memory Usage**        | Less overhead, only data stored                | More overhead, stores data and pointers          |
| **Cache Performance**   | Better, due to locality of reference           | Worse, due to scattered nodes                    |
| **Implementation**      | Simple, direct memory allocation               | More complex, requires dynamic memory management |
| **Wasted Space**        | Possible if array is not fully utilized        | No wasted space, memory allocated as needed      |
| **Data Structure Type** | Linear, static data structure                  | Linear, dynamic data structure                   |

## Derivation of Index Formulae for 1-D and 2-D Arrays

### 1-D Array Index Formula

For a 1-D array:

```
int arr[n];
```

The address of `arr[i]` is:

```
Address = Base_Address + (i * Size_of_Element)
```

Where:

- `Base_Address` is the address of `arr[0]`
- `i` is the index (starting from 0)
- `Size_of_Element` is the size of each array element (e.g., 4 bytes for `int`)

### 2-D Array Index Formula

Suppose you have a 2-D array `A[m][n]` (m rows, n columns):

#### Row Major Order

The address of element `A[i][j]`:

```
Address = Base_Address + [ (i * n) + j ] * Size_of_Element
```

- `i` = row index
- `j` = column index
- `n` = number of columns

#### Column Major Order

The address of element `A[i][j]`:

```
Address = Base_Address + [ (j * m) + i ] * Size_of_Element
```

- `j` = column index
- `i` = row index
- `m` = number of rows

---

### Summary Table

**for A (n × m) i.e. n = rows, m = columns**

| Order              | Formula for A[i][j]         |
| ------------------ | --------------------------- |
| Row Major Order    | Base + [(i × n) + j] × Size |
| Column Major Order | Base + [(j × m) + i] × Size |

---

### Examples

Suppose `int A[3][4]` and `Base_Address = 1000`, `Size_of_Element = 4 bytes`.

- Address of `A[2][1]` in Row Major:

  ```
  Address = 1000 + [ (2 * 4) + 1 ] * 4
          = 1000 + [8 + 1] * 4
          = 1000 + 9 * 4
          = 1000 + 36
          = 1036
  ```

- Address of `A[2][1]` in Column Major:
  ```
  Address = 1000 + [ (1 * 3) + 2 ] * 4
          = 1000 + [3 + 2] * 4
          = 1000 + 5 * 4
          = 1000 + 20
          = 1020
  ```

---

#### Example: Calculating Address of Data[10][10]

Given:

- Array: `Data[20][50]`
- Each element size: 4 bytes
- Base address: 2000

here `i = 10`, `j = 10`, `n = 50`, `Size = 4`

##### (i) Row Major Order

Formula:  
`Address = Base + [ (i × m) + j ] × Size`

```
Address = 2000 + [ (10 × 50) + 10 ] × 4
    = 2000 + [500 + 10] × 4
    = 2000 + 510 × 4
    = 2000 + 2040
    = 4040
```

##### (ii) Column Major Order

Formula:  
`Address = Base + [ (j × n) + i ] × Size`

```
Address = 2000 + [ (10 × 20) + 10 ] × 4
    = 2000 + [200 + 10] × 4
    = 2000 + 210 × 4
    = 2000 + 840
    = 2840
```

#### Example: Address Calculation for Arr[50][100] in Row Major Order

Given:

- Array: `Arr[50][100]`
- Each element size: 4 bytes
- Base address: 1000
- Find the address of `Arr[20][50]`

#### Row Major Order Formula

```
Address = Base_Address + [ (i × n) + j ] × Size_of_Element
```

Where:

- `i = 20` (row index)
- `j = 50` (column index)
- `n = 100` (number of columns)
- `Size_of_Element = 4` bytes

#### Calculation

```
Address = 1000 + [ (20 × 100) + 50 ] × 4
    = 1000 + [2000 + 50] × 4
    = 1000 + 2050 × 4
    = 1000 + 8200
    = 9200
```

## Algorithm to Transpose a Matrix

To **transpose** a matrix means to swap its rows and columns. For a matrix `A` of size `m x n`, the transposed matrix `A^T` will be of size `n x m`, where `A^T[j][i] = A[i][j]`.

### Algorithm

1. Create a new matrix `B` of size `n x m`.
2. For each element `A[i][j]`, set `B[j][i] = A[i][j]`.
3. Return matrix `B`.

**Pseudocode:**

```c
for (int i = 0; i < m; i++) {
    for (int j = 0; j < n; j++) {
        B[j][i] = A[i][j];
    }
}
```
