# Exception Handling in Java

> **This file answers your assignment questions in simple English. Each question is clearly marked (Q1, Q2, etc.) and explained with easy points, tables, and examples.**

## 🔹 Q1: What do you mean by Exception? What is checked and unchecked exception?

**Definition:**
An exception is an unexpected event or error that happens during the execution of a program. It stops the normal flow of the program and creates an exception object that contains information about the error.

**Simple Example:**
Think of an exception like a traffic jam on a road. When there's a traffic jam, cars can't move normally - similarly, when an exception occurs, the program can't continue its normal execution.

**Common Situations Where Exceptions Occur:**

- Dividing a number by zero
- Trying to access an array element that doesn't exist
- Opening a file that doesn't exist
- Converting invalid text to numbers

---

## 🔹 Exception Hierarchy in Java

Java has a well-organized hierarchy (family tree) of exception classes:

```
Object
  └── Throwable
      ├── Error (System-level problems)
      └── Exception
          ├── RuntimeException (Unchecked Exceptions)
          │   ├── NullPointerException
          │   ├── ArrayIndexOutOfBoundsException
          │   ├── ArithmeticException
          │   └── IllegalArgumentException
          └── Other Exceptions (Checked Exceptions)
              ├── IOException
              ├── SQLException
              └── ClassNotFoundException
```

**Key Classes in Hierarchy:**

| Class              | Description                                       | Example              |
| ------------------ | ------------------------------------------------- | -------------------- |
| `Throwable`        | Parent of all exceptions and errors               | Base class           |
| `Error`            | Serious system problems (not handled by programs) | OutOfMemoryError     |
| `Exception`        | Problems that programs can handle                 | IOException          |
| `RuntimeException` | Exceptions that happen during runtime             | NullPointerException |

---

## 🔹 Checked vs Unchecked Exceptions

### ➤ Checked Exceptions

**Definition:** Exceptions that must be handled at compile time. The compiler forces you to handle them.

**Characteristics:**

- Must be handled using try-catch or declared using throws
- Compiler checks if they are handled properly
- Usually occur due to external factors (file not found, network issues)

**Common Checked Exceptions:**

- `IOException` - Input/Output operations fail
- `SQLException` - Database operation fails
- `ClassNotFoundException` - Class not found during loading

**Example:**

```java
// This code won't compile without try-catch or throws
FileReader file = new FileReader("data.txt"); // IOException must be handled
```

### ➤ Unchecked Exceptions

**Definition:** Exceptions that occur during runtime and are not checked by the compiler.

**Characteristics:**

- Also called Runtime Exceptions
- Don't need to be declared or caught (but can be)
- Usually occur due to programming errors
- Extend `RuntimeException` class

**Common Unchecked Exceptions:**

- `NullPointerException` - Using null reference
- `ArithmeticException` - Mathematical errors (divide by zero)
- `ArrayIndexOutOfBoundsException` - Invalid array access

**Example:**

```java
int result = 10 / 0; // ArithmeticException - no need to handle at compile time
```

**Comparison Table:**

| Feature                | Checked Exceptions        | Unchecked Exceptions                      |
| ---------------------- | ------------------------- | ----------------------------------------- |
| **Compile Time Check** | Must be handled           | Not required to handle                    |
| **Inheritance**        | Extend Exception          | Extend RuntimeException                   |
| **When Occurs**        | External factors          | Programming errors                        |
| **Examples**           | IOException, SQLException | NullPointerException, ArithmeticException |

---

## 🔹 Q2: Exception Chaining

**Definition:**
Exception chaining is a technique where one exception causes another exception. It helps preserve the original cause of an error while adding more specific information.

**Why Use Exception Chaining?**

- Provides complete error information
- Shows the root cause of the problem
- Helps in debugging complex applications

**How it Works:**
When an exception occurs, you can catch it and throw a new exception while preserving the original exception as the "cause."

**Methods for Exception Chaining:**

1. `initCause(Throwable cause)` - Sets the cause
2. `getCause()` - Gets the original cause

**Example:**

```java
public class ExceptionChaining {
    public static void method1() throws Exception {
        try {
            method2();
        } catch (ArithmeticException e) {
            // Throw new exception but preserve original cause
            throw new Exception("Error in method1", e);
        }
    }

    public static void method2() {
        int result = 10 / 0; // This throws ArithmeticException
    }

    public static void main(String[] args) {
        try {
            method1();
        } catch (Exception e) {
            System.out.println("Main exception: " + e.getMessage());
            System.out.println("Root cause: " + e.getCause());
        }
    }
}
```

**Output:**

```
Main exception: Error in method1
Root cause: java.lang.ArithmeticException: / by zero
```

---

## 🔹 Q3: Explain about try-catch with example

**Definition:**
Try-catch is a mechanism to handle exceptions in Java. Code that might cause an exception is placed in the `try` block, and the handling code is placed in the `catch` block.

**Basic Syntax:**

```java
try {
    // Code that might throw an exception
} catch (ExceptionType e) {
    // Code to handle the exception
}
```

**How it Works:**

1. Code in `try` block executes normally
2. If an exception occurs, execution jumps to the matching `catch` block
3. After handling, program continues with the next statement

**Simple Example:**

```java
public class TryCatchExample {
    public static void main(String[] args) {
        try {
            int result = 10 / 0; // This will cause ArithmeticException
            System.out.println("Result: " + result);
        } catch (ArithmeticException e) {
            System.out.println("Error: Cannot divide by zero!");
        }
        System.out.println("Program continues...");
    }
}
```

**Output:**

```
Error: Cannot divide by zero!
Program continues...
```

### ➤ Multiple Catch Blocks

You can have multiple catch blocks to handle different types of exceptions:

```java
try {
    // Risky code
} catch (ArithmeticException e) {
    System.out.println("Math error occurred");
} catch (NullPointerException e) {
    System.out.println("Null pointer error");
} catch (Exception e) {
    System.out.println("Some other error occurred");
}
```

### ➤ Finally Block

The `finally` block always executes, whether an exception occurs or not:

```java
try {
    // Risky code
} catch (Exception e) {
    // Handle exception
} finally {
    // This always runs
    System.out.println("Cleanup code here");
}
```

---

## 🔹 Q4: What is the meaning of "throwing an exception"? When does an exception throw?

### ➤ What is Throwing an Exception?

**Definition:**
Throwing an exception means creating and sending an exception object to indicate that an error has occurred. It's like raising an alarm when something goes wrong.

**When Does an Exception Throw?**

Exceptions are thrown in two ways:

1. **Automatically by JVM (Java Virtual Machine):**

   - When runtime errors occur
   - Examples: dividing by zero, accessing null objects, array index out of bounds

2. **Manually by Programmer:**
   - Using the `throw` keyword
   - When you want to signal a specific error condition

**Example of Automatic Exception Throwing:**

```java
int[] numbers = {1, 2, 3};
System.out.println(numbers[5]); // JVM throws ArrayIndexOutOfBoundsException
```

**Example of Manual Exception Throwing:**

```java
public void checkAge(int age) {
    if (age < 18) {
        throw new IllegalArgumentException("Age must be 18 or above");
    }
}
```

### ➤ The `throw` Keyword

**Syntax:**

```java
throw new ExceptionType("Error message");
```

**Example:**

```java
public class ThrowExample {
    public static void validateScore(int score) {
        if (score < 0 || score > 100) {
            throw new IllegalArgumentException("Score must be between 0 and 100");
        }
        System.out.println("Valid score: " + score);
    }

    public static void main(String[] args) {
        try {
            validateScore(150); // This will throw an exception
        } catch (IllegalArgumentException e) {
            System.out.println("Error: " + e.getMessage());
        }
    }
}
```

---

## 🔹 Q5: Explain difference between throws and throw keyword in Java

### ➤ `throw` Keyword

**Purpose:** Actually throws an exception

**Usage:**

- Used inside method body
- Creates and throws an exception object
- Used with an instance of exception

**Syntax:**

```java
throw new ExceptionType("message");
```

**Example:**

```java
public void checkNumber(int num) {
    if (num < 0) {
        throw new IllegalArgumentException("Number cannot be negative");
    }
}
```

### ➤ `throws` Keyword

**Purpose:** Declares that a method might throw an exception

**Usage:**

- Used in method signature/declaration
- Informs caller that method might throw an exception
- Used with exception class names (not instances)

**Syntax:**

```java
public void methodName() throws ExceptionType1, ExceptionType2 {
    // method body
}
```

**Example:**

```java
public void readFile(String fileName) throws IOException {
    FileReader file = new FileReader(fileName); // might throw IOException
}
```

### ➤ Comparison Table

| Feature      | `throw`                      | `throws`                     |
| ------------ | ---------------------------- | ---------------------------- |
| **Purpose**  | Actually throws an exception | Declares possible exceptions |
| **Location** | Inside method body           | In method signature          |
| **Usage**    | `throw new Exception()`      | `throws Exception`           |
| **Type**     | Uses exception instance      | Uses exception class name    |
| **Multiple** | One exception at a time      | Multiple exceptions allowed  |

**Example Showing Both:**

```java
public class ThrowVsThrows {
    // Method declares it might throw IOException using 'throws'
    public void readFile(String fileName) throws IOException {
        if (fileName == null) {
            // Actually throwing an exception using 'throw'
            throw new IllegalArgumentException("File name cannot be null");
        }
        // Code that might throw IOException
        FileReader file = new FileReader(fileName);
    }
}
```

---

## 🔹 Built-in Exceptions

Java provides many built-in exception classes for common error situations:

### ➤ Common Runtime Exceptions (Unchecked)

| Exception                         | When it Occurs            | Example                                |
| --------------------------------- | ------------------------- | -------------------------------------- |
| `NullPointerException`            | Using null reference      | `String s = null; s.length();`         |
| `ArithmeticException`             | Mathematical errors       | `int x = 5/0;`                         |
| `ArrayIndexOutOfBoundsException`  | Invalid array index       | `arr[10]` when array size is 5         |
| `StringIndexOutOfBoundsException` | Invalid string index      | `str.charAt(100)` for short string     |
| `IllegalArgumentException`        | Invalid method argument   | Negative value where positive expected |
| `NumberFormatException`           | Invalid number conversion | `Integer.parseInt("abc")`              |

### ➤ Common Checked Exceptions

| Exception                | When it Occurs                 | Example                     |
| ------------------------ | ------------------------------ | --------------------------- |
| `IOException`            | Input/output operations fail   | File reading/writing errors |
| `FileNotFoundException`  | File not found                 | Opening non-existent file   |
| `SQLException`           | Database operation fails       | Invalid SQL query           |
| `ClassNotFoundException` | Class not found during loading | Missing class file          |
| `InterruptedException`   | Thread interrupted             | Thread sleep interrupted    |

---

## 🔹 Creating Custom Exceptions

Sometimes built-in exceptions are not enough. You can create your own exception classes:

### ➤ Creating Custom Checked Exception

```java
// Custom checked exception
class InvalidAgeException extends Exception {
    public InvalidAgeException(String message) {
        super(message);
    }
}

// Using the custom exception
public class CustomExceptionExample {
    public static void validateAge(int age) throws InvalidAgeException {
        if (age < 0 || age > 120) {
            throw new InvalidAgeException("Age must be between 0 and 120");
        }
    }

    public static void main(String[] args) {
        try {
            validateAge(150);
        } catch (InvalidAgeException e) {
            System.out.println("Custom Exception: " + e.getMessage());
        }
    }
}
```

### ➤ Creating Custom Unchecked Exception

```java
// Custom unchecked exception
class InvalidScoreException extends RuntimeException {
    public InvalidScoreException(String message) {
        super(message);
    }
}

// Using the custom exception
public class CustomRuntimeException {
    public static void validateScore(int score) {
        if (score < 0 || score > 100) {
            throw new InvalidScoreException("Score must be between 0 and 100");
        }
    }
}
```

### ➤ Best Practices for Custom Exceptions

1. **Extend appropriate parent class:**

   - Extend `Exception` for checked exceptions
   - Extend `RuntimeException` for unchecked exceptions

2. **Provide meaningful names:**

   - Use descriptive names ending with "Exception"

3. **Include constructors:**

   - Default constructor
   - Constructor with message
   - Constructor with message and cause

4. **Add relevant information:**
   - Include error codes if needed
   - Add additional fields for context

---

## 🔹 Exception Handling Best Practices

1. **Handle specific exceptions first:**

   ```java
   try {
       // risky code
   } catch (FileNotFoundException e) {
       // Handle file not found
   } catch (IOException e) {
       // Handle other IO exceptions
   }
   ```

2. **Don't catch and ignore:**

   ```java
   // Bad practice
   try {
       // code
   } catch (Exception e) {
       // Don't leave empty - at least log the error
   }
   ```

3. **Use finally for cleanup:**

   ```java
   FileInputStream file = null;
   try {
       file = new FileInputStream("data.txt");
       // use file
   } catch (IOException e) {
       // handle error
   } finally {
       if (file != null) {
           file.close(); // cleanup
       }
   }
   ```

4. **Provide meaningful error messages:**
   ```java
   throw new IllegalArgumentException("Age cannot be negative: " + age);
   ```

---

## 🔹 Summary

Exception handling is a crucial part of Java programming that helps create robust and reliable applications. Here's what we covered:

- **Exceptions** are unexpected events that disrupt normal program flow
- **Checked exceptions** must be handled at compile time
- **Unchecked exceptions** occur at runtime
- **Try-catch blocks** handle exceptions gracefully
- **Throwing exceptions** signals error conditions
- **Exception chaining** preserves original error causes
- **Custom exceptions** provide application-specific error handling

By understanding and properly implementing exception handling, you can write programs that gracefully handle errors and provide better user experience.

---

## 🔹 Stack Trace Elements

**Definition:**
A stack trace is a list of method calls that the Java Virtual Machine (JVM) was executing at the time an exception was thrown. Each entry in the stack trace is called a **Stack Trace Element**.

**Why Important?**

- Shows the exact sequence of method calls that led to the error (like a breadcrumb trail for debugging)
- Helps you find where the problem happened in your code, including the file and line number
- Makes it easier to fix bugs by showing the path the program took before crashing

**How to Read a Stack Trace:**

- The top line shows the exception type and message (e.g., `java.lang.ArithmeticException: / by zero`)
- Each line below shows a method call (from most recent to oldest)
- Each line has: class name, method name, file name, and line number
- The first method listed is where the error actually happened

**Example Stack Trace:**

```
Exception in thread "main" java.lang.ArithmeticException: / by zero
    at MyClass.divide(MyClass.java:10)
    at MyClass.main(MyClass.java:5)
```

**Explanation of Example:**

- The error happened in the `divide` method at line 10 of `MyClass.java`
- The `main` method called `divide` at line 5
- The exception type is `ArithmeticException` and the message is `/ by zero`

**Diagram:**

```
main()  --->  divide()  --->  Exception!
```

**How to Get Stack Trace in Java:**

- Every `Throwable` (Exception/Error) object has a method `getStackTrace()` that returns an array of `StackTraceElement` objects
- You can print the stack trace using `printStackTrace()` method

**Code Example:**

```java
try {
    int result = 10 / 0;
} catch (ArithmeticException e) {
    e.printStackTrace(); // Prints the stack trace to the console
    StackTraceElement[] elements = e.getStackTrace();
    for (StackTraceElement el : elements) {
        System.out.println("Class: " + el.getClassName() + ", Method: " + el.getMethodName() + ", Line: " + el.getLineNumber());
    }
}
```

**Technical Terms:**

- `StackTraceElement`: Java class representing one entry in the stack trace
- `Throwable`: Parent class for all errors and exceptions in Java
- `printStackTrace()`: Method to print the stack trace to the console
- `getStackTrace()`: Method to get stack trace elements as an array

**Best Practices:**

- Always check the first few lines of the stack trace to find the real cause
- Use stack traces to debug and fix errors quickly
- Don't ignore stack traces—they are your best friend for troubleshooting!

---

## 🔹 Input / Output (I/O) Basics

**Definition:**
Input/Output (I/O) in Java means reading data from a source (like keyboard, file, or network) and writing data to a destination (like screen, file, or network).

### ➤ What is a Stream?

**Answer to Question:**
A **Stream** is a sequence of data. In Java, streams are used to read data from and write data to different sources.

**Types of Streams:**

1. **Byte Streams** (for binary data)
2. **Character Streams** (for text data)

**Diagram:**

```
[Source] --(InputStream/Reader)--> [Java Program] --(OutputStream/Writer)--> [Destination]
```

---

### ➤ Byte Streams

- Used for reading and writing binary data (images, audio, etc.)
- Work with 8-bit bytes
- Main classes: `InputStream` (for input), `OutputStream` (for output)

**Common Byte Stream Classes:**
| Class | Use |
|------------------|----------------------------|
| FileInputStream | Read bytes from a file |
| FileOutputStream | Write bytes to a file |
| BufferedInputStream | Fast reading of bytes |
| BufferedOutputStream | Fast writing of bytes |

---

### ➤ Character Streams

- Used for reading and writing text data (characters)
- Work with 16-bit Unicode characters
- Main classes: `Reader` (for input), `Writer` (for output)

**Common Character Stream Classes:**
| Class | Use |
|------------------|----------------------------|
| FileReader | Read characters from a file |
| FileWriter | Write characters to a file |
| BufferedReader | Fast reading of text |
| BufferedWriter | Fast writing of text |

---

### ➤ Reading and Writing

#### Reading

- **InputStream/Reader** classes are used to read data
- You can read from keyboard, files, or other sources

#### Writing

- **OutputStream/Writer** classes are used to write data
- You can write to screen, files, or other destinations

---

### ➤ Console Reading and Writing

- **Reading from Console:** Use `Scanner` or `BufferedReader`
- **Writing to Console:** Use `System.out.print()` or `System.out.println()`

**Example:**

```java
Scanner sc = new Scanner(System.in); // Read from console
String name = sc.nextLine();
System.out.println("Hello, " + name); // Write to console
```

---

### ➤ Reading and Writing Files

- **Reading a File:** Use `FileInputStream`/`FileReader` (for bytes/characters)
- **Writing a File:** Use `FileOutputStream`/`FileWriter`

**Example:**

```java
FileReader fr = new FileReader("data.txt");
int ch;
while((ch = fr.read()) != -1) {
    System.out.print((char)ch);
}
fr.close();
```

---

### ➤ Summary Table: Streams in Java

| Stream Type      | Main Classes (Input)         | Main Classes (Output)          | Data Type      |
| ---------------- | ---------------------------- | ------------------------------ | -------------- |
| Byte Stream      | InputStream, FileInputStream | OutputStream, FileOutputStream | Bytes (binary) |
| Character Stream | Reader, FileReader           | Writer, FileWriter             | Characters     |

---

**Key Points:**

- Use byte streams for binary data, character streams for text
- Streams make it easy to read/write data from/to files, console, or network
- Always close streams after use to free resources

**Diagram Recap:**

```
[Keyboard/File/Network] --(InputStream/Reader)--> [Java Program] --(OutputStream/Writer)--> [Screen/File/Network]
```
LAST YEAR QUES

q. What do you mean by Exception? What is checked and unchecked exception?
q. Explain Exception chaining. 
Q. Explain about try-catch with example. 
Q. What is the meaning of “throwing an exception”? When does an exception
throw?
Q. Explain difference between throws and throw keyword in Java. 3

Q. What is meant by Stream and what are the types of Streams and classes of the
Streams? 
Q. Write generic Java program that display sum if pass numeric data and merge text if pass string data
Q. Write Java program that accepts a temperature in Celsius. It should throw an Exception “Temperature Below Normal” when the temperature is less than 20C, throw an Exception “Normal Temperature” when the temperature above 20C and below 40C and throw an Exception “Temperature is High” when the it is greater than 40C.