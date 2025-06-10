# Arrays, Vectors, Wrapper Classes, and Strings in Java

---

## Arrays

**Definition:**
An array in Java is a fixed-size, ordered collection of elements of the same data type. Arrays are used to store multiple values in a single variable, making it easier to manage large amounts of data.

**Key Points:**

- Arrays have a fixed length, which must be specified at the time of creation and cannot be changed later.
- Elements are stored in contiguous memory locations and can be accessed using an index (starting from 0).
- Arrays can be of primitive types (like `int`, `char`, `double`) or reference types (like objects).
- Useful for storing and processing large collections of data efficiently.

**When to Use:**

- When you know the number of elements in advance and need fast, indexed access.

---

## Array Syntax in Java

Here are all possible ways to declare, initialize, and use arrays in Java:

### 1. Declaration and Initialization Separately

```java
int[] numbers; // Declaration
numbers = new int[5]; // Initialization with size
```

### 2. Declaration and Initialization Together

```java
int[] numbers = new int[5]; // Declares and initializes an array with default values
```

### 3. Declaration with Values

```java
int[] numbers = {10, 20, 30, 40, 50}; // Declares and initializes with specific values
```

### 4. Using `new` with Values

```java
int[] numbers = new int[]{10, 20, 30, 40, 50}; // Explicitly using `new` keyword
```

### 5. Multi-Dimensional Arrays

#### Declaration and Initialization Separately

```java
int[][] matrix; // Declaration
matrix = new int[3][3]; // Initialization with size
```

#### Declaration and Initialization Together

```java
int[][] matrix = new int[3][3]; // Declares and initializes a 3x3 array
```

#### Declaration with Values

```java
int[][] matrix = {
    {1, 2, 3},
    {4, 5, 6},
    {7, 8, 9}
}; // Declares and initializes with specific values
```

#### Using `new` with Values

```java
int[][] matrix = new int[][]{
    {1, 2, 3},
    {4, 5, 6},
    {7, 8, 9}
}; // Explicitly using `new` keyword
```

### 6. Jagged Arrays (Arrays of Arrays)

```java
int[][] jaggedArray = new int[3][]; // Declares a jagged array
jaggedArray[0] = new int[2]; // First row with 2 columns
jaggedArray[1] = new int[3]; // Second row with 3 columns
jaggedArray[2] = new int[1]; // Third row with 1 column
```

### 7. Array of Objects

```java
String[] names = {"Alice", "Bob", "Charlie"}; // Array of Strings
```

### 8. Anonymous Arrays

```java
printArray(new int[]{1, 2, 3, 4, 5}); // Passing an array directly to a method
```

### 9. Varargs (Variable-Length Arguments)

```java
public void printNumbers(int... numbers) {
    for (int num : numbers) {
        System.out.println(num);
    }
}
```

**Note:** Varargs internally use arrays to handle variable-length arguments.

---

These syntaxes cover all possible ways to work with arrays in Java.

## Code Example: Arrays

Here is an example of how to declare, initialize, and use arrays in Java:

```java
public class ArrayExample {
    public static void main(String[] args) {
        // Declare and initialize an array
        int[] numbers = {10, 20, 30, 40, 50};

        // Access elements using an index
        System.out.println("First element: " + numbers[0]);
        System.out.println("Last element: " + numbers[numbers.length - 1]);

        // Iterate through the array using a for loop
        System.out.println("Array elements:");
        for (int i = 0; i < numbers.length; i++) {
            System.out.println(numbers[i]);
        }

        // Iterate using an enhanced for loop
        System.out.println("Array elements (enhanced for loop):");
        for (int num : numbers) {
            System.out.println(num);
        }

        // Modify an element
        numbers[2] = 35;
        System.out.println("Modified third element: " + numbers[2]);
    }
}
```

**Explanation:**

- The array `numbers` is declared and initialized with values `{10, 20, 30, 40, 50}`.
- Elements are accessed using their index (e.g., `numbers[0]` for the first element).
- The `length` property is used to determine the size of the array.
- Both traditional `for` loops and enhanced `for` loops can be used to iterate through the array.
- Array elements can be modified by assigning new values to specific indices.

**Output:**

```
First element: 10
Last element: 50
Array elements:
10
20
30
40
50
Array elements (enhanced for loop):
10
20
30
40
50
Modified third element: 35
```

## Dimensions and Matrix Multiplication in Arrays

### Dimensions in Arrays

In Java, arrays can have one or more dimensions. The number of dimensions determines how data is organized and accessed.

#### 1. One-Dimensional Arrays

A one-dimensional array is a simple list of elements.

```java
int[] array = {1, 2, 3, 4, 5};
```

#### 2. Two-Dimensional Arrays

A two-dimensional array is like a table or matrix with rows and columns.

```java
int[][] matrix = {
    {1, 2, 3},
    {4, 5, 6},
    {7, 8, 9}
};
```

#### 3. Multi-Dimensional Arrays

Java supports arrays with more than two dimensions, though they are less commonly used.

```java
int[][][] cube = new int[3][3][3];
```

---

### Matrix Multiplication Program

Matrix multiplication involves multiplying two matrices to produce a third matrix. The number of columns in the first matrix must equal the number of rows in the second matrix.

#### Code Example

```java
public class MatrixMultiplication {
    public static void main(String[] args) {
        // Define two matrices
        int[][] matrixA = {
            {1, 2, 3},
            {4, 5, 6}
        };
        int[][] matrixB = {
            {7, 8},
            {9, 10},
            {11, 12}
        };

        // Resultant matrix
        int[][] result = new int[matrixA.length][matrixB[0].length];

        // Perform multiplication
        for (int i = 0; i < matrixA.length; i++) {
            for (int j = 0; j < matrixB[0].length; j++) {
                for (int k = 0; k < matrixB.length; k++) {
                    result[i][j] += matrixA[i][k] * matrixB[k][j];
                }
            }
        }

        // Print the result
        System.out.println("Resultant Matrix:");
        for (int[] row : result) {
            for (int value : row) {
                System.out.print(value + " ");
            }
            System.out.println();
        }
    }
}
```

#### Explanation

1. `matrixA` has dimensions 2x3, and `matrixB` has dimensions 3x2.
2. The resultant matrix has dimensions 2x2.
3. Nested loops are used to calculate the dot product of rows and columns.

#### Output

```
Resultant Matrix:
58 64
139 154
```

**Key Points:**

- Ensure the number of columns in the first matrix equals the number of rows in the second matrix.
- Use nested loops to compute the dot product for each element in the resultant matrix.

---

## Strings

**Definition:**
A `String` in Java is an object that represents a sequence of characters. Strings are widely used for storing and manipulating text data.

**Key Points:**

- Strings are immutable, meaning once created, their values cannot be changed. Any modification creates a new string object.
- Java provides many built-in methods for string manipulation, such as concatenation, comparison, searching, and substring extraction.
- String literals are stored in a special memory area called the string pool for memory efficiency.
- For mutable strings (when you need to modify the content frequently), Java provides `StringBuilder` and `StringBuffer` classes.

**When to Use:**

- For storing and processing textual data.
- When you need to perform operations like searching, replacing, or formatting text.

## Ways to Declare a String in Java

### 1. Using String Literals

```java
String str = "Hello, World!";
```

- The most common way to create a string.
- The string is stored in the string pool for memory efficiency.

### 2. Using the `new` Keyword

```java
String str = new String("Hello, World!");
```

- Creates a new string object in the heap memory, even if the same value exists in the string pool.

### 3. Using Character Array

```java
char[] chars = {'H', 'e', 'l', 'l', 'o'};
String str = new String(chars);
```

- Converts a character array into a string.

### 4. Using `String.valueOf()`

```java
String str = String.valueOf(12345);
```

- Converts other data types (e.g., numbers, booleans) into a string.

---

## Common String Operations in Java

### 1. Concatenation

```java
String str1 = "Hello";
String str2 = "World";
String result = str1 + " " + str2; // Using + operator
String result2 = str1.concat(" ").concat(str2); // Using concat() method
```

### 2. Length of a String

```java
String str = "Hello";
int length = str.length();
```

### 3. Character at a Specific Index

```java
char ch = str.charAt(1); // 'e'
```

### 4. Substring

```java
String str = "Hello, World!";
String sub = str.substring(7); // "World!"
String sub2 = str.substring(0, 5); // "Hello"
```

### 5. String Comparison

```java
String str1 = "Hello";
String str2 = "hello";
boolean isEqual = str1.equals(str2); // false
boolean isEqualIgnoreCase = str1.equalsIgnoreCase(str2); // true
```

### 6. Searching in a String

```java
String str = "Hello, World!";
int index = str.indexOf("World"); // 7
int lastIndex = str.lastIndexOf("o"); // 8
boolean contains = str.contains("Hello"); // true
```

### 7. Replace Characters or Substrings

```java
String str = "Hello, World!";
String replaced = str.replace("World", "Java"); // "Hello, Java!"
```

### 8. Convert to Uppercase or Lowercase

```java
String str = "Hello";
String upper = str.toUpperCase(); // "HELLO"
String lower = str.toLowerCase(); // "hello"
```

### 9. Trim Whitespace

```java
String str = "   Hello   ";
String trimmed = str.trim(); // "Hello"
```

### 10. Split a String

```java
String str = "apple,banana,orange";
String[] fruits = str.split(","); // ["apple", "banana", "orange"]
```

### 11. Check if String is Empty or Blank

```java
String str = "";
boolean isEmpty = str.isEmpty(); // true
boolean isBlank = str.isBlank(); // true (Java 11+)
```

### 12. Convert String to Char Array

```java
String str = "Hello";
char[] chars = str.toCharArray();
```

### 13. String Formatting

```java
String formatted = String.format("Name: %s, Age: %d", "Alice", 25);
// "Name: Alice, Age: 25"
```

### 14. Joining Strings

```java
String joined = String.join(", ", "apple", "banana", "orange");
// "apple, banana, orange"
```

---

These operations cover the most common ways to work with strings in Java.

## StringBuffer

**Definition:**
`StringBuffer` is a mutable sequence of characters in Java. Unlike `String`, which is immutable, `StringBuffer` allows modifications to its content without creating new objects. It is thread-safe, meaning it is synchronized and can be used in multi-threaded environments.

**Key Points:**

- `StringBuffer` is mutable, so operations like appending, inserting, or deleting characters modify the same object.
- It is synchronized, making it thread-safe but slightly slower than `StringBuilder`.
- Useful for scenarios where frequent modifications to strings are required in a multi-threaded environment.

**When to Use:**

- When you need a mutable string in a multi-threaded environment.
- For operations involving frequent string modifications, such as concatenation or deletion.

---

### Common Operations with `StringBuffer`

1. **Creating a `StringBuffer`:**

```java
StringBuffer sb = new StringBuffer("Hello");
```

2. **Appending Strings:**

```java
sb.append(" World"); // "Hello World"
```

3. **Inserting Characters or Strings:**

```java
sb.insert(5, ","); // "Hello, World"
```

4. **Replacing Characters or Substrings:**

```java
sb.replace(6, 11, "Java"); // "Hello, Java"
```

5. **Deleting Characters or Substrings:**

```java
sb.delete(5, 6); // "HelloJava"
```

6. **Reversing the String:**

```java
sb.reverse(); // "avaJolleH"
```

7. **Getting the Length and Capacity:**

```java
int length = sb.length(); // Length of the string
int capacity = sb.capacity(); // Capacity of the buffer
```

---

### Differences Between `String` and `StringBuffer`

| Feature           | `String`                         | `StringBuffer`                                                         |
| ----------------- | -------------------------------- | ---------------------------------------------------------------------- |
| **Mutability**    | Immutable                        | Mutable                                                                |
| **Thread Safety** | Not thread-safe                  | Thread-safe (synchronized)                                             |
| **Performance**   | Faster for read-only operations  | Slower due to synchronization                                          |
| **Memory Usage**  | Creates a new object for changes | Modifies the same object                                               |
| **Use Case**      | When immutability is required    | When frequent modifications are needed in a multi-threaded environment |

---

> **Note:** If thread safety is not required, consider using `StringBuilder` for better performance as it is similar to `StringBuffer` but not synchronized.

## Vectors

**Definition:**
A `Vector` is a dynamic array-like data structure provided by Java's `java.util` package. Unlike arrays, vectors can grow or shrink in size automatically as elements are added or removed.

**Key Points:**

- Vectors are part of the legacy collection classes but are still used for thread-safe operations.
- They are synchronized, meaning they are safe to use in multi-threaded environments, but this can make them slower than other collections like `ArrayList`.
- Vectors can store objects only (not primitive types directly), but autoboxing allows primitive values to be stored as objects.
- Useful when you need a resizable array with thread safety.

**When to Use:**

- When you need a dynamic array that is thread-safe.
- For legacy codebases or when synchronization is required.

---

## Code Example: Vectors

Here is an example of how to declare, initialize, and use a `Vector` in Java:

```java
import java.util.Vector;

public class VectorExample {
    public static void main(String[] args) {
        // Create a Vector of integers
        Vector<Integer> numbers = new Vector<>();

        // Add elements to the Vector
        numbers.add(10);
        numbers.add(20);
        numbers.add(30);
        System.out.println("Initial Vector: " + numbers);

        // Insert an element at a specific index
        numbers.add(1, 15);
        System.out.println("After inserting 15 at index 1: " + numbers);

        // Access elements using an index
        int firstElement = numbers.get(0);
        System.out.println("First element: " + firstElement);

        // Update an element at a specific index
        numbers.set(2, 25);
        System.out.println("After updating index 2 to 25: " + numbers);

        // Remove an element by index
        numbers.remove(3);
        System.out.println("After removing element at index 3: " + numbers);

        // Check if the Vector contains a specific element
        boolean contains20 = numbers.contains(20);
        System.out.println("Vector contains 20: " + contains20);

        // Iterate through the Vector using a for loop
        System.out.println("Iterating using a for loop:");
        for (int i = 0; i < numbers.size(); i++) {
            System.out.println(numbers.get(i));
        }

        // Iterate using an enhanced for loop
        System.out.println("Iterating using an enhanced for loop:");
        for (int num : numbers) {
            System.out.println(num);
        }

        // Clear all elements from the Vector
        numbers.clear();
        System.out.println("After clearing the Vector: " + numbers);
    }
}
```

### Explanation:

1. **Creating a Vector:** A `Vector` is created using the `Vector` class. In this example, it stores `Integer` objects.
2. **Adding Elements:** Use the `add()` method to add elements to the `Vector`.
3. **Accessing Elements:** Use the `get()` method with an index to access elements.
4. **Updating Elements:** Use the `set()` method to update an element at a specific index.
5. **Removing Elements:** Use the `remove()` method to remove an element by index.
6. **Checking for Elements:** Use the `contains()` method to check if the `Vector` contains a specific value.
7. **Iterating:** Use a traditional `for` loop or an enhanced `for` loop to iterate through the `Vector`.
8. **Clearing the Vector:** Use the `clear()` method to remove all elements.

### Output:

```
Initial Vector: [10, 20, 30]
After inserting 15 at index 1: [10, 15, 20, 30]
First element: 10
After updating index 2 to 25: [10, 15, 25, 30]
After removing element at index 3: [10, 15, 25]
Vector contains 20: false
Iterating using a for loop:
10
15
25
Iterating using an enhanced for loop:
10
15
25
After clearing the Vector: []
```

**Key Points:**

- Vectors are synchronized, making them thread-safe but slower than `ArrayList`.
- They automatically resize when elements are added or removed.
- Use `Vector` when thread safety is required; otherwise, prefer `ArrayList` for better performance.
- The `clear()` method removes all elements, leaving the `Vector` empty.

---

This example demonstrates the basic operations and features of `Vector` in Java.

## Wrapper Classes

**Definition:**
Wrapper classes in Java provide a way to use primitive data types (`int`, `char`, `double`, etc.) as objects. Each primitive type has a corresponding wrapper class in the `java.lang` package (e.g., `Integer` for `int`, `Double` for `double`).

**Key Points:**

- Wrapper classes allow primitives to be used in collections (like `ArrayList`, `Vector`) that require objects.
- They provide utility methods for converting between types, parsing strings, and more.
- Autoboxing and unboxing (automatic conversion between primitives and wrapper objects) make it easy to work with both types.
- Common wrapper classes: `Integer`, `Double`, `Character`, `Boolean`, `Float`, `Long`, `Short`, `Byte`.

**When to Use:**

- When you need to store primitive values in collections.
- When you need to use utility methods for parsing or converting values.

---

### Autoboxing and Unboxing in Java

**Autoboxing:**  
Autoboxing is the automatic conversion of primitive data types into their corresponding wrapper class objects. This feature simplifies the process of working with collections and other APIs that require objects instead of primitives.

**Example:**

```java
class BoxingExample1 {
    public static void main(String args[]) {
        int a = 50;

        // Explicit Boxing
        Integer a2 = new Integer(a);

        // Implicit Boxing (Autoboxing)
        Integer a3 = 5;

        System.out.println(a2 + " " + a3);
    }
}
```

**Output:**

```
50 5
```

---

**Unboxing:**  
Unboxing is the reverse process of autoboxing, where a wrapper class object is automatically converted back into its corresponding primitive type.

**Example:**

```java
class UnboxingExample1 {
    public static void main(String args[]) {
        Integer i = new Integer(50);

        // Unboxing
        int a = i;

        System.out.println(a);
    }
}
```

**Output:**

```
50
```

---

**Summary Table:**

| Concept        | Description                                           | Example Code Snippet       |
| -------------- | ----------------------------------------------------- | -------------------------- |
| **Autoboxing** | Automatic conversion of primitives to wrapper objects | `Integer a = 5;`           |
| **Unboxing**   | Automatic conversion of wrapper objects to primitives | `int a = new Integer(50);` |

---

| Topic           | Key Feature               | Use Case                                      |
| --------------- | ------------------------- | --------------------------------------------- |
| Array           | Fixed size, fast access   | Known number of elements, indexed access      |
| Vector          | Dynamic, thread-safe      | Resizable array, multi-threaded environment   |
| Wrapper Classes | Object form of primitives | Collections, utility methods, type conversion |
| String          | Immutable text object     | Text storage and manipulation                 |

---

> **Note:** Choose the appropriate data structure or class based on your requirements for size, mutability, thread safety, and type of data to be stored or processed.
