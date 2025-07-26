# Object-Oriented Programming (OOP) in Java: Complete Guide

---

## Object-Oriented Programming Overview

**Object-Oriented Programming (OOP)** is a programming paradigm based on the concept of "objects" which contain data (fields/attributes) and code (methods/functions). OOP helps organize code in a way that makes it easier to understand, maintain, and reuse.

### Q1. Distinguish between Procedure Oriented Programming and Object Oriented Programming.

| Aspect               | Procedure Oriented Programming (POP)     | Object Oriented Programming (OOP)      |
| -------------------- | ---------------------------------------- | -------------------------------------- |
| **Main Focus**       | Functions and procedures                 | Objects and classes                    |
| **Data Security**    | Low (uses global data, less data hiding) | High (encapsulation, data hiding)      |
| **Approach**         | Top-down (problem broken into functions) | Bottom-up (problem modeled as objects) |
| **Code Reusability** | Limited (code reuse via functions)       | High (inheritance, polymorphism)       |
| **Maintenance**      | Harder for large/complex programs        | Easier due to modular structure        |
| **Examples**         | C, Pascal, FORTRAN                       | Java, C++, Python                      |
| **Data Handling**    | Data and functions are separate          | Data and methods are bundled together  |

---

## Objects

### What is an Object ?

An **object** in Java is a fundamental building block of object-oriented programming. It represents a real-world entity and encapsulates both data and behavior.

#### Key Characteristics of an Object:

- **State:** The data or information stored in the object, represented by its attributes or fields (e.g., color, name, age).
- **Behavior:** The actions or operations the object can perform, defined by its methods (e.g. start(), study(), deposit()).
- **Identity:** A unique reference that distinguishes one object from another, even if their state is identical.

#### How Objects Work in Java:

- Objects are created from classes, which act as blueprints.
- Each object has its own set of attribute values (state), but shares the structure and behavior defined by the class.
- Objects interact with each other by invoking methods and accessing data through references.

#### Example:

```java
// Class definition (blueprint)
class Car {
    String color;      // State
    String model;      // State

    void start() {     // Behavior
        System.out.println("Car started");
    }
}

// Creating objects (instances)
Car car1 = new Car();
car1.color = "Red";
car1.model = "Sedan";

Car car2 = new Car();
car2.color = "Blue";
car2.model = "SUV";
```

- Here, `car1` and `car2` are two different objects with their own state but the same behavior.

#### Real-World Analogy:

Think of a **class** as a blueprint for a house, and **objects** as the actual houses built from that blueprint. Each house (object) can have different colors or features (state), but all are built using the same plan (class) and can perform similar actions (behavior).

---

### Examples of Objects:

- **Car object:** State (color, speed, model), Behavior (start, stop, accelerate)
- **Student object:** State (name, age, grade), Behavior (study, takeExam, sleep)

### Q7. Object is an instance of class, justify your answer.

**Question 7: Object is an instance of class, justify your answer.**

- A **class** is like a blueprint or template that defines the structure and behavior of objects.
- An **object** is a specific instance created from that class blueprint.
- **Justification:**
  - Class defines what attributes and methods an object will have
  - Object is the actual implementation with specific values
  - Multiple objects can be created from one class
  - Each object has its own memory space and values

**Example:**

```java
// Class (blueprint)
class Car {
    String color;
    String model;
    void start() { /* code */ }
}

// Objects (instances)
Car car1 = new Car(); // car1 is an instance of Car class
Car car2 = new Car(); // car2 is another instance of Car class
```

### Q1. How are objects implemented in Java?

**Question 1: How are objects implemented in Java?**
Objects in Java are implemented through the following process:

1. **Class Definition:** Define a class with attributes (fields) and methods.
2. **Object Creation:** Use the `new` keyword to create an object.
3. **Memory Allocation:** JVM allocates memory for the object in the heap.
4. **Constructor Call:** The constructor initializes the object's state.
5. **Reference Assignment:** The reference to the object is stored in a variable (on the stack).

**Syntax Example:**

```java
// Step 1: Define a class
class Student {
    String name;
    int age;

    // Constructor
    Student(String name, int age) {
        this.name = name;
        this.age = age;
    }

    void display() {
        System.out.println("Name: " + name + ", Age: " + age);
    }
}

// Step 2: Create an object
Student student1 = new Student("Alice", 21);

// Step 3: Use the object
student1.display(); // Output: Name: Alice, Age: 21
```

**Explanation:**

- `Student` is the class (blueprint).
- `new Student("Alice", 21)` creates an object in heap memory and calls the constructor.
- `student1` is a reference variable pointing to the object.
- Methods and fields are accessed using the reference (`student1.display()`).

**Memory Implementation:**

- **Heap Memory:** Stores actual object data
- **Stack Memory:** Stores object references
- **Method Area:** Stores class information

---

## Classes

### What is a Class?

- A **class** is a blueprint or template for creating objects
- It defines the structure (attributes) and behavior (methods) that objects will have
- Classes are user-defined data types in Java

### Class Components:

| Component             | Description                                     | Example                          |
| --------------------- | ----------------------------------------------- | -------------------------------- |
| **Attributes/Fields** | Variables that hold the state of an object      | `String name; int age;`          |
| **Methods**           | Functions that define the behavior of an object | `void eat() { ... }`             |
| **Constructors**      | Special methods used to initialize objects      | `Person(String n) { ... }`       |
| **Access Modifiers**  | Keywords that control visibility and access     | `private`, `public`, `protected` |

**Basic Class Example:**

```java
public class Person {
    // Attributes
    private String name;
    private int age;

    // Constructor
    public Person(String name, int age) {
        this.name = name;
        this.age = age;
    }

    // Methods
    public void displayInfo() {
        System.out.println("Name: " + name + ", Age: " + age);
    }
}
```

---

## Abstraction

### What is Abstraction?

- **Abstraction** means hiding complex implementation details and showing only essential features
- It focuses on **what** an object does rather than **how** it does it
- Achieved through abstract classes and interfaces in Java

### Types of Abstraction:

1. **Data Abstraction:** Hiding data implementation details
2. **Process Abstraction:** Hiding method implementation details

### Benefits of Abstraction:

- Simplifies complex systems
- Reduces programming complexity
- Increases code reusability
- Improves maintainability

**Example:**

```java
// Abstract class
abstract class Animal {
    abstract void makeSound(); // Abstract method

    void sleep() { // Concrete method
        System.out.println("Animal is sleeping");
    }
}

class Dog extends Animal {
    void makeSound() {
        System.out.println("Dog barks");
    }
}
```

---

## Encapsulation

### What is Encapsulation?

- **Encapsulation** is the bundling of data (attributes) and methods that operate on that data into a single unit (class)
- It also involves **data hiding** using access modifiers
- Often called "data hiding" or "information hiding"

### Q8. Write 3 uses of Encapsulation in Object Oriented Programming.

1. **Data Security:** Prevents unauthorized access to sensitive data by making attributes private
2. **Data Validation:** Controls how data is modified through setter methods with validation logic
3. **Code Maintainability:** Internal implementation can be changed without affecting external code

### Implementation of Encapsulation:

```java
public class BankAccount {
    private double balance; // Private attribute (data hiding)

    // Public getter method
    public double getBalance() {
        return balance;
    }

    // Public setter method with validation
    public void setBalance(double balance) {
        if (balance >= 0) {
            this.balance = balance;
        } else {
            System.out.println("Invalid balance amount");
        }
    }

    // Method to deposit money
    public void deposit(double amount) {
        if (amount > 0) {
            balance += amount;
        }
    }
}
```

### Benefits of Encapsulation:

- **Security:** Data is protected from unauthorized access
- **Flexibility:** Internal implementation can be changed
- **Reusability:** Encapsulated code can be reused easily
- **Testing:** Individual components can be tested separately

---

## Polymorphism

## Q. What do you understand by Polymorphism? Explain types of polymorphism with proper example.

### What is Polymorphism?

**Polymorphism** is a core concept in object-oriented programming that allows a single interface or method to represent different underlying forms (data types). In Java, polymorphism enables objects to be treated as instances of their parent class rather than their actual class, allowing the same method or operation to behave differently based on the object that invokes it.

- The word "polymorphism" means "many forms".
- It allows the same method name or operator to perform different tasks depending on the context.
- Polymorphism increases flexibility and reusability in code.

### Types of Polymorphism in Java

Java supports two main types of polymorphism:

#### 1. Compile-time Polymorphism (Static Polymorphism)

- Achieved through **method overloading**.
- The method to be executed is determined at compile time.
- Multiple methods have the same name but different parameter lists (type, number, or order).

**Example: Method Overloading**

```java
class Calculator {
    int add(int a, int b) {
        return a + b;
    }

    double add(double a, double b) {
        return a + b;
    }

    int add(int a, int b, int c) {
        return a + b + c;
    }
}

class Main {
    public static void main(String[] args) {
        Calculator calc = new Calculator();
        System.out.println(calc.add(2, 3));         // Output: 5
        System.out.println(calc.add(2.5, 3.5));     // Output: 6.0
        System.out.println(calc.add(1, 2, 3));      // Output: 6
    }
}
```

- Here, the `add` method is overloaded with different parameter types and counts.

#### 2. Runtime Polymorphism (Dynamic Polymorphism)

- Achieved through **method overriding**.
- The method to be executed is determined at runtime.
- A subclass provides a specific implementation of a method already defined in its superclass.

**Example: Method Overriding**

```java
class Animal {
    void makeSound() {
        System.out.println("Animal makes a sound");
    }
}

class Dog extends Animal {
    @Override
    void makeSound() {
        System.out.println("Dog barks");
    }
}

class Cat extends Animal {
    @Override
    void makeSound() {
        System.out.println("Cat meows");
    }
}

class Main {
    public static void main(String[] args) {
        Animal a1 = new Dog();
        Animal a2 = new Cat();
        a1.makeSound(); // Output: Dog barks
        a2.makeSound(); // Output: Cat meows
    }
}
```

- Here, the `makeSound` method is overridden in subclasses. The actual method called depends on the object's runtime type.

### Summary Table

| Type                      | How Achieved       | When Resolved | Example                  |
| ------------------------- | ------------------ | ------------- | ------------------------ |
| Compile-time Polymorphism | Method Overloading | Compile time  | Multiple `add()` methods |
| Runtime Polymorphism      | Method Overriding  | Runtime       | Overridden `makeSound()` |

**Conclusion:**  
Polymorphism allows Java programs to be more flexible and maintainable by enabling the same interface to be used for different underlying forms (objects), supporting both compile-time and runtime method resolution.

---

## OOP in Java

### Java's OOP Features:

Java fully supports object-oriented programming with all four main principles:

1. **Classes and Objects:** Blueprint and instances
2. **Encapsulation:** Data hiding with access modifiers
3. **Inheritance:** Code reuse through class extension
4. **Polymorphism:** Method overloading and overriding

### Q9. What are uses of `this` keyword? Explain with proper example.

**Question 9: What are uses of `this` keyword? Explain with proper example.**

The `this` keyword in Java refers to the current object instance. Its main uses are:

1. **Distinguish between instance variables and parameters**
2. **Call other constructors in the same class**
3. **Pass current object as parameter**
4. **Return current object from method**

**Examples:**

```java
class Student {
    private String name;
    private int age;

    // Use 1: Distinguish between instance variable and parameter
    public Student(String name, int age) {
        this.name = name; // this.name refers to instance variable
        this.age = age;   // name refers to parameter
    }

    // Use 2: Constructor chaining
    public Student(String name) {
        this(name, 18); // Calls the parameterized constructor
    }

    // Use 3: Return current object
    public Student setName(String name) {
        this.name = name;
        return this; // Returns current object for method chaining
    }

    // Use 4: Pass current object as parameter
    public void display() {
        printStudentInfo(this); // Passing current object
    }

    private void printStudentInfo(Student student) {
        System.out.println("Name: " + student.name);
    }
}
```

---

## Static Members and Their Limitations

### Q2. What are the limitations of static members?

**Question 2: What are the limitations of static members?**

**Static members** belong to the class rather than any specific instance. Their limitations include:

1. **Cannot access non-static members directly**
2. **Cannot use `this` and `super` keywords**
3. **Cannot be overridden (for methods)**
4. **Memory overhead if not used properly**
5. **Difficult to test and mock**

**Example showing limitations:**

```java
class Example {
    int instanceVar = 10;        // Non-static variable
    static int staticVar = 20;   // Static variable

    static void staticMethod() {
        // System.out.println(instanceVar); // ERROR: Cannot access non-static
        System.out.println(staticVar);      // OK: Can access static
        // this.instanceVar = 5;            // ERROR: Cannot use 'this'
    }

    void instanceMethod() {
        System.out.println(instanceVar); // OK: Can access both
        System.out.println(staticVar);   // OK: Can access both
    }
}
```

---

## Characteristics of Java

## Q4. Explain 10 features of Java Programming Language.

### Main Characteristics of Java

| Characteristic           | Description                                                                                                                                                        |
| ------------------------ | ------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| **Platform Independent** | Java code is compiled into bytecode, which can run on any system with a Java Virtual Machine (JVM). This enables the "Write Once, Run Anywhere" (WORA) capability. |
| **Object-Oriented**      | Java is based on the principles of object-oriented programming, using objects and classes to organize code.                                                        |
| **Simple**               | Java has a clean and easy-to-understand syntax, making it straightforward to learn and use.                                                                        |
| **Secure**               | Java provides built-in security features such as bytecode verification, no explicit pointers, and a security manager.                                              |
| **Robust**               | Java emphasizes reliability with strong memory management, automatic garbage collection, and comprehensive exception handling.                                     |
| **Multithreaded**        | Java supports multithreading, allowing concurrent execution of two or more threads for maximum CPU utilization.                                                    |
| **Interpreted**          | Java bytecode is interpreted (and optionally compiled at runtime) by the JVM, making it platform-independent.                                                      |
| **High Performance**     | Java achieves high performance through Just-In-Time (JIT) compilation and efficient memory management.                                                             |
| **Dynamic**              | Java supports dynamic loading of classes at runtime, enabling flexible and extensible applications.                                                                |
| **Distributed**          | Java provides built-in networking libraries (like RMI and sockets) to create distributed applications that can communicate over networks.                          |
| **Portable**             | Java programs are portable across platforms because there are no implementation-dependent features and the same bytecode runs on any JVM.                          |

### Detailed Explanation:

1. **Platform Independence:**

   - Java code is compiled to bytecode
   - JVM interprets bytecode on any platform
   - Same program runs on Windows, Linux, Mac

2. **Object-Oriented:**

   - Everything is an object (except primitives)
   - Supports all OOP principles

3. **Security:**

   - No pointers to avoid memory corruption
   - Bytecode verification
   - Security manager for applets

4. **Robustness:**
   - Automatic garbage collection
   - Exception handling mechanism
   - Type checking at compile time

---

## Summary Table: OOP Concepts

| Concept           | Purpose               | Key Feature                     | Java Implementation                |
| ----------------- | --------------------- | ------------------------------- | ---------------------------------- |
| **Object**        | Real-world entity     | State + Behavior                | `new` keyword                      |
| **Class**         | Blueprint for objects | Template                        | `class` keyword                    |
| **Abstraction**   | Hide complexity       | Essential features only         | Abstract classes, Interfaces       |
| **Encapsulation** | Bundle data + methods | Data hiding                     | Private attributes, Public methods |
| **Inheritance**   | Code reuse            | IS-A relationship               | `extends` keyword                  |
| **Polymorphism**  | Multiple forms        | Same method, different behavior | Overloading, Overriding            |

---

# Java Environment, Source File Structure, and Fundamental Programming Structures

---

## The Java Environment

### Q1. Compare Java Runtime Environment and Java Virtual Machine.

**Question 1: Compare Java Runtime Environment and Java Virtual Machine.**

| Aspect                  | Java Virtual Machine (JVM)                      | Java Runtime Environment (JRE)                                          |
| ----------------------- | ----------------------------------------------- | ----------------------------------------------------------------------- |
| **Definition**          | A runtime engine that executes Java bytecode    | A software package that provides libraries and JVM to run Java programs |
| **Components**          | Interpreter, JIT compiler, garbage collector    | JVM + Java libraries + supporting files                                 |
| **Purpose**             | Executes compiled Java bytecode                 | Complete runtime environment for Java applications                      |
| **Platform Dependency** | Platform-specific (different for Windows/Linux) | Platform-specific but provides same Java API                            |
| **Scope**               | Core execution engine only                      | Broader runtime environment                                             |
| **Memory Management**   | Handles heap, stack, method area                | Provides memory through JVM                                             |

**Simple Explanation:**

- **JVM** is like the engine of a car that makes it run
- **JRE** is like the complete car with engine, fuel, and all necessary parts

---

### Q2. Explain the difference between JDK and JRE in Java.

**Question 2: Explain the difference between JDK and JRE in Java.**

| Feature            | JDK (Java Development Kit)                         | JRE (Java Runtime Environment)          |
| ------------------ | -------------------------------------------------- | --------------------------------------- |
| **Full Form**      | Java Development Kit                               | Java Runtime Environment                |
| **Purpose**        | For developing Java applications                   | For running Java applications           |
| **Target Users**   | Java developers/programmers                        | End users who run Java programs         |
| **Components**     | JRE + Development tools (compiler, debugger, etc.) | JVM + Java libraries + supporting files |
| **Size**           | Larger (includes development tools)                | Smaller (only runtime components)       |
| **Tools Included** | javac, java, javadoc, jar, etc.                    | Only java command and libraries         |
| **Can Compile?**   | Yes (has javac compiler)                           | No (cannot compile Java source code)    |
| **Can Run?**       | Yes (includes JRE)                                 | Yes (designed for running)              |

**Relationship Diagram:**

```
JDK = JRE + Development Tools
JRE = JVM + Java Libraries
JVM = Core execution engine
```

**Example:**

- To **write** Java code: Need JDK
- To **run** Java programs: Need JRE (included in JDK)

---

### Q3. Explain the compilation and execution process of Java program with proper diagram.

**Question 3: Explain the compilation and execution process of Java program with proper diagram.**

#### Step-by-Step Process:

1. **Source Code Creation (.java file)**
2. **Compilation (javac compiler)**
3. **Bytecode Generation (.class file)**
4. **Loading into JVM**
5. **Execution by JVM**

#### Detailed Process:

```
Java Source Code (.java)
         ↓
    javac Compiler
         ↓
   Bytecode (.class)
         ↓
   Class Loader (JVM)
         ↓
   Bytecode Verifier
         ↓
   Interpreter/JIT Compiler
         ↓
   Machine Code
         ↓
   Output/Execution
```

#### Detailed Explanation:

| Stage                | Description                                            | Tool/Component    |
| -------------------- | ------------------------------------------------------ | ----------------- |
| **1. Source Code**   | Human-readable Java code written in .java files        | Text editor/IDE   |
| **2. Compilation**   | Source code converted to platform-independent bytecode | javac compiler    |
| **3. Bytecode**      | Intermediate code stored in .class files               | Java bytecode     |
| **4. Class Loading** | Bytecode loaded into JVM memory                        | Class Loader      |
| **5. Verification**  | Bytecode checked for security and correctness          | Bytecode Verifier |
| **6. Execution**     | Bytecode converted to machine code and executed        | Interpreter/JIT   |

#### Example:

```java
// HelloWorld.java (Source Code)
public class HelloWorld {
    public static void main(String[] args) {
        System.out.println("Hello World!");
    }
}

// Compilation: javac HelloWorld.java
// Creates: HelloWorld.class (Bytecode)
// Execution: java HelloWorld
// Output: Hello World!
```

---

## Java Source File Structure

### Basic Structure of a Java Source File:

```java
// 1. Package declaration (optional)
package com.example.myapp;

// 2. Import statements (optional)
import java.util.Scanner;
import java.io.*;

// 3. Class declaration (required)
public class MyClass {
    // 4. Fields/Variables
    private int number;
    static String className = "MyClass";

    // 5. Constructors
    public MyClass() {
        // Default constructor
    }

    public MyClass(int num) {
        this.number = num;
    }

    // 6. Methods
    public void displayNumber() {
        System.out.println("Number: " + number);
    }

    // 7. Main method (entry point)
    public static void main(String[] args) {
        MyClass obj = new MyClass(10);
        obj.displayNumber();
    }
}
```

### Rules for Java Source Files:

- File name must match the public class name
- Only one public class per file
- Package declaration must be first (if present)
- Import statements come after package declaration

---

## Fundamental Programming Structures in Java

### Defining Classes in Java

A **class** is a blueprint for creating objects. It defines the structure and behavior of objects.

#### Basic Class Syntax:

```java
[access_modifier] class ClassName {
    // Fields (attributes)
    // Constructors
    // Methods
}
```

#### Example:

```java
public class Student {
    // Fields
    private String name;
    private int age;
    private String course;

    // Constructor
    public Student(String name, int age, String course) {
        this.name = name;
        this.age = age;
        this.course = course;
    }

    // Methods
    public void study() {
        System.out.println(name + " is studying " + course);
    }

    public void displayInfo() {
        System.out.println("Name: " + name + ", Age: " + age + ", Course: " + course);
    }
}
```

---

## Constructors

### Q4. List out the types of constructors.

**Question 4: List out the types of constructors.**

1. **Default Constructor (No-argument constructor)**
2. **Parameterized Constructor**
3. **Copy Constructor (not built-in in Java)**

### Q5. What do you mean by Constructor? How many types of constructors are available in Java?

**Question 5: What do you mean by Constructor? How many types of constructors are available in Java?**

#### What is a Constructor?

- A **constructor** is a special method that is automatically called when an object is created
- It has the same name as the class
- It doesn't have a return type (not even void)
- Used to initialize object's state

#### Types of Constructors in Java:

| Type                          | Description                                             | Example                        |
| ----------------------------- | ------------------------------------------------------- | ------------------------------ |
| **Default Constructor**       | No parameters, provides default values                  | `Person() { }`                 |
| **Parameterized Constructor** | Takes parameters to initialize with specific values     | `Person(String name, int age)` |
| **Copy Constructor**          | Creates object by copying another object (not built-in) | Custom implementation          |

#### Examples:

```java
public class Person {
    private String name;
    private int age;

    // 1. Default Constructor
    public Person() {
        this.name = "Unknown";
        this.age = 0;
    }

    // 2. Parameterized Constructor
    public Person(String name, int age) {
        this.name = name;
        this.age = age;
    }

    // 3. Copy Constructor (manual implementation)
    public Person(Person other) {
        this.name = other.name;
        this.age = other.age;
    }
}
```

### Q10. Explain the role of constructor and also explain how subclass constructor implicitly calls superclass constructor in Java.

**Question 10: Explain the role of constructor and also explain how subclass constructor implicitly calls superclass constructor in Java.**

#### Role of Constructor:

1. **Initialize object state** with default or specific values
2. **Allocate memory** for object creation
3. **Set up object** before it's used
4. **Ensure object is in valid state** from creation

#### Subclass Constructor and Superclass Constructor:

**Key Points:**

- Every subclass constructor **implicitly calls** the superclass constructor
- If not specified, `super()` is automatically called
- `super()` must be the **first statement** in constructor if used explicitly

#### Example:

```java
// Superclass
class Animal {
    protected String species;

    // Superclass constructor
    public Animal() {
        System.out.println("Animal constructor called");
        species = "Unknown";
    }

    public Animal(String species) {
        System.out.println("Animal parameterized constructor called");
        this.species = species;
    }
}

// Subclass
class Dog extends Animal {
    private String breed;

    // Subclass constructor
    public Dog() {
        // super(); is implicitly called here
        System.out.println("Dog constructor called");
        breed = "Unknown";
    }

    public Dog(String species, String breed) {
        super(species); // Explicit call to superclass constructor
        System.out.println("Dog parameterized constructor called");
        this.breed = breed;
    }
}

// Usage
Dog dog1 = new Dog();
// Output:
// Animal constructor called
// Dog constructor called

Dog dog2 = new Dog("Canine", "Labrador");
// Output:
// Animal parameterized constructor called
// Dog parameterized constructor called
```

#### Constructor Chaining Rules:

1. **First line** of subclass constructor calls superclass constructor
2. If no explicit `super()` call, `super()` is automatically added
3. **Compilation error** if superclass has no default constructor and no explicit `super()` call

---

## Methods

### Method Structure:

```java
[access_modifier] [static] [return_type] methodName([parameters]) {
    // Method body
    [return value;]
}
```

### Example:

```java
public class Calculator {
    // Instance method
    public int add(int a, int b) {
        return a + b;
    }

    // Static method
    public static double multiply(double x, double y) {
        return x * y;
    }

    // Method with no return value
    public void displayResult(int result) {
        System.out.println("Result: " + result);
    }
}
```

---

## Access Specifiers

| Access Modifier               | Same Class | Same Package | Subclass (Different Package) | Different Package |
| ----------------------------- | ---------- | ------------ | ---------------------------- | ----------------- |
| **private**                   | ✓          | ✗            | ✗                            | ✗                 |
| **default** (package-private) | ✓          | ✓            | ✗                            | ✗                 |
| **protected**                 | ✓          | ✓            | ✓                            | ✗                 |
| **public**                    | ✓          | ✓            | ✓                            | ✓                 |

### Example:

```java
public class AccessExample {
    private int privateVar = 1;      // Only within this class
    int defaultVar = 2;              // Within same package
    protected int protectedVar = 3;  // Subclasses and same package
    public int publicVar = 4;        // Everywhere
}
```

---

## Static Members

### What are Static Members?

- **Static variables:** Belong to the class, not to any specific instance
- **Static methods:** Can be called without creating an object
- Shared among all instances of the class

### Example:

```java
public class Counter {
    private static int count = 0;  // Static variable
    private int instanceId;

    public Counter() {
        count++;  // Increment static variable
        instanceId = count;
    }

    public static int getCount() {  // Static method
        return count;
    }

    public int getInstanceId() {
        return instanceId;
    }
}

// Usage
Counter c1 = new Counter();
Counter c2 = new Counter();
System.out.println(Counter.getCount()); // Output: 2
```

_Note: Static member limitations were covered earlier in this document._

---

## Comments

### Types of Comments in Java:

```java
// 1. Single-line comment
int x = 10; // This is a single-line comment

/* 2. Multi-line comment
   This is a multi-line comment
   that spans multiple lines */

/** 3. Documentation comment (Javadoc)
 * This method calculates the sum of two numbers
 * @param a first number
 * @param b second number
 * @return sum of a and b
 */
public int add(int a, int b) {
    return a + b;
}
```

---

## Data Types

### Primitive Data Types:

| Type        | Size    | Range                | Default Value | Example                |
| ----------- | ------- | -------------------- | ------------- | ---------------------- |
| **byte**    | 8 bits  | -128 to 127          | 0             | `byte b = 100;`        |
| **short**   | 16 bits | -32,768 to 32,767    | 0             | `short s = 1000;`      |
| **int**     | 32 bits | -2³¹ to 2³¹-1        | 0             | `int i = 100000;`      |
| **long**    | 64 bits | -2⁶³ to 2⁶³-1        | 0L            | `long l = 100000L;`    |
| **float**   | 32 bits | ±3.4E38 (7 digits)   | 0.0f          | `float f = 3.14f;`     |
| **double**  | 64 bits | ±1.8E308 (15 digits) | 0.0d          | `double d = 3.14159;`  |
| **char**    | 16 bits | 0 to 65,535          | '\u0000'      | `char c = 'A';`        |
| **boolean** | 1 bit   | true or false        | false         | `boolean flag = true;` |

### Reference Data Types:

- **Classes:** `String`, `Scanner`, custom classes
- **Arrays:** `int[]`, `String[]`
- **Interfaces:** `List`, `Map`

---

## Variables

### Types of Variables:

```java
public class VariableExample {
    static int staticVar = 10;        // Static/Class variable
    int instanceVar = 20;             // Instance variable

    public void method() {
        int localVar = 30;            // Local variable
        final int CONSTANT = 40;      // Constant (final variable)

        // localVar is only accessible within this method
    }
}
```

### Variable Declaration and Initialization:

```java
int number;              // Declaration
number = 42;             // Initialization
int count = 0;           // Declaration + Initialization
final double PI = 3.14159; // Constant declaration
```

---

## Operators

### Types of Operators:

| Category       | Operators                        | Example                  |
| -------------- | -------------------------------- | ------------------------ |
| **Arithmetic** | `+`, `-`, `*`, `/`, `%`          | `int sum = a + b;`       |
| **Assignment** | `=`, `+=`, `-=`, `*=`, `/=`      | `x += 5;`                |
| **Comparison** | `==`, `!=`, `<`, `>`, `<=`, `>=` | `if (a > b)`             |
| **Logical**    | `&&`, `\|\|`, `!`                | `if (a > 0 && b > 0)`    |
| **Bitwise**    | `&`, `\|`, `^`, `~`, `<<`, `>>`  | `int result = a & b;`    |
| **Unary**      | `++`, `--`, `+`, `-`, `!`        | `++count;`               |
| **Ternary**    | `? :`                            | `max = (a > b) ? a : b;` |

### Example:

```java
public class OperatorExample {
    public static void main(String[] args) {
        int a = 10, b = 20;

        // Arithmetic operators
        int sum = a + b;          // 30
        int difference = b - a;   // 10
        int product = a * b;      // 200
        int quotient = b / a;     // 2
        int remainder = b % a;    // 0

        // Comparison operators
        boolean isEqual = (a == b);     // false
        boolean isGreater = (b > a);    // true

        // Logical operators
        boolean result = (a > 5) && (b < 30);  // true

        // Assignment operators
        a += 5;  // a = a + 5, now a = 15

        // Unary operators
        a++;     // a = 16
        ++b;     // b = 21

        // Ternary operator
        int max = (a > b) ? a : b;  // max = 21
    }
}
```

---

## Control Flow

### 1. Conditional Statements:

#### if-else Statement:

```java
int score = 85;

if (score >= 90) {
    System.out.println("Grade A");
} else if (score >= 80) {
    System.out.println("Grade B");
} else if (score >= 70) {
    System.out.println("Grade C");
} else {
    System.out.println("Grade D");
}
```

#### switch Statement:

```java
int day = 3;
String dayName;

switch (day) {
    case 1:
        dayName = "Monday";
        break;
    case 2:
        dayName = "Tuesday";
        break;
    case 3:
        dayName = "Wednesday";
        break;
    default:
        dayName = "Invalid day";
}
```

### 2. Loop Statements:

#### for Loop:

```java
// Traditional for loop
for (int i = 0; i < 10; i++) {
    System.out.println("Number: " + i);
}

// Enhanced for loop (for-each)
int[] numbers = {1, 2, 3, 4, 5};
for (int num : numbers) {
    System.out.println(num);
}
```

#### while Loop:

```java
int count = 0;
while (count < 5) {
    System.out.println("Count: " + count);
    count++;
}
```

#### do-while Loop:

```java
int num;
do {
    System.out.println("Enter a positive number:");
    num = scanner.nextInt();
} while (num <= 0);
```

### 3. Control Transfer Statements:

- **break:** Exit from loop or switch
- **continue:** Skip current iteration
- **return:** Exit from method

---

## Arrays

### Q1. Explain in detail about Array with syntax and example.

**Question 1: Explain in detail about Array with syntax and example.**

#### What is an Array?

- An **array** is a collection of elements of the same data type stored in contiguous memory locations
- Elements are accessed using an index (starting from 0)
- Fixed size once created

#### Array Declaration Syntax:

```java
// Method 1: Declaration then initialization
dataType[] arrayName;
arrayName = new dataType[size];

// Method 2: Declaration and initialization together
dataType[] arrayName = new dataType[size];

// Method 3: Declaration and initialization with values
dataType[] arrayName = {value1, value2, value3, ...};
```

#### Examples:

##### 1. Integer Array:

```java
// Declaration and initialization
int[] numbers = new int[5];  // Array of size 5

// Assigning values
numbers[0] = 10;
numbers[1] = 20;
numbers[2] = 30;
numbers[3] = 40;
numbers[4] = 50;

// Alternative initialization
int[] scores = {85, 90, 78, 92, 88};

// Accessing elements
System.out.println("First number: " + numbers[0]);  // Output: 10
System.out.println("Array length: " + numbers.length);  // Output: 5
```

##### 2. String Array:

```java
String[] names = {"Alice", "Bob", "Charlie", "Diana"};

// Iterating through array
for (int i = 0; i < names.length; i++) {
    System.out.println("Name " + (i+1) + ": " + names[i]);
}

// Enhanced for loop
for (String name : names) {
    System.out.println("Hello, " + name);
}
```

##### 3. Multi-dimensional Array:

```java
// 2D Array (Matrix)
int[][] matrix = new int[3][3];

// Initialize with values
int[][] table = {
    {1, 2, 3},
    {4, 5, 6},
    {7, 8, 9}
};

// Accessing 2D array elements
System.out.println("Element at [1][2]: " + table[1][2]);  // Output: 6

// Iterating through 2D array
for (int i = 0; i < table.length; i++) {
    for (int j = 0; j < table[i].length; j++) {
        System.out.print(table[i][j] + " ");
    }
    System.out.println();
}
```

#### Array Characteristics:

| Feature                 | Description                                      |
| ----------------------- | ------------------------------------------------ |
| **Fixed Size**          | Size cannot be changed after creation            |
| **Same Data Type**      | All elements must be of the same type            |
| **Zero-based Indexing** | First element is at index 0                      |
| **Contiguous Memory**   | Elements stored in adjacent memory locations     |
| **Random Access**       | Any element can be accessed directly using index |

#### Common Array Operations:

```java
public class ArrayOperations {
    public static void main(String[] args) {
        int[] arr = {5, 2, 8, 1, 9, 3};

        // 1. Finding maximum element
        int max = arr[0];
        for (int i = 1; i < arr.length; i++) {
            if (arr[i] > max) {
                max = arr[i];
            }
        }
        System.out.println("Maximum: " + max);

        // 2. Calculating sum
        int sum = 0;
        for (int num : arr) {
            sum += num;
        }
        System.out.println("Sum: " + sum);

        // 3. Searching for an element
        int target = 8;
        boolean found = false;
        for (int i = 0; i < arr.length; i++) {
            if (arr[i] == target) {
                System.out.println("Element " + target + " found at index " + i);
                found = true;
                break;
            }
        }
        if (!found) {
            System.out.println("Element not found");
        }
    }
}
```

#### Array vs Other Collections:

| Feature         | Array         | ArrayList                             |
| --------------- | ------------- | ------------------------------------- |
| **Size**        | Fixed         | Dynamic                               |
| **Performance** | Faster access | Slightly slower                       |
| **Memory**      | Less overhead | More overhead                         |
| **Type Safety** | Compile-time  | Runtime (with generics: compile-time) |

---

## Summary

This comprehensive guide covers:

- **Java Environment:** JDK, JRE, JVM differences and compilation process
- **Java Source Structure:** Package, imports, class structure
- **Fundamental Concepts:** Classes, constructors, methods, access specifiers
- **Programming Elements:** Data types, variables, operators, control flow
- **Arrays:** Declaration, initialization, operations, and examples

All topics are explained with practical examples and detailed explanations for easy understanding and learning.

---
