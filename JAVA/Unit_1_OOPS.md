# Object-Oriented Programming (OOP) in Java: Complete Guide

---

## Object-Oriented Programming Overview

**Object-Oriented Programming (OOP)** is a programming paradigm based on the concept of "objects" which contain data (fields/attributes) and code (methods/functions). OOP helps organize code in a way that makes it easier to understand, maintain, and reuse.

### Q1. Distinguish between Procedure Oriented Programming and Object Oriented Programming.

**Question 1: Distinguish between Procedure Oriented Programming and Object Oriented Programming.**

| Aspect                | Procedure Oriented Programming (POP)         | Object Oriented Programming (OOP)         |
|-----------------------|----------------------------------------------|-------------------------------------------|
| **Main Focus**        | Functions and procedures                     | Objects and classes                       |
| **Data Security**     | Low (uses global data, less data hiding)     | High (encapsulation, data hiding)         |
| **Approach**          | Top-down (problem broken into functions)     | Bottom-up (problem modeled as objects)    |
| **Code Reusability**  | Limited (code reuse via functions)           | High (inheritance, polymorphism)          |
| **Maintenance**       | Harder for large/complex programs            | Easier due to modular structure           |
| **Examples**          | C, Pascal, FORTRAN                           | Java, C++, Python                         |
| **Data Handling**     | Data and functions are separate              | Data and methods are bundled together     |

**Summary:**  
POP organizes code around functions, making it less secure and harder to maintain for large projects. OOP organizes code around objects, improving security, reusability, and maintainability.

---

## Objects
### What is an Object?

An **object** in Java is a fundamental building block of object-oriented programming. It represents a real-world entity or concept within a program and encapsulates both data and behavior.

#### Key Characteristics of an Object:
- **State:** The data or information stored in the object, represented by its attributes or fields (e.g., color, name, age).
- **Behavior:** The actions or operations the object can perform, defined by its methods (e.g., start(), study(), deposit()).
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
| Component           | Description                                 | Example                        |
|---------------------|---------------------------------------------|--------------------------------|
| **Attributes/Fields** | Variables that hold the state of an object   | `String name; int age;`        |
| **Methods**           | Functions that define the behavior of an object | `void eat() { ... }`           |
| **Constructors**      | Special methods used to initialize objects     | `Person(String n) { ... }`     |
| **Access Modifiers**  | Keywords that control visibility and access    | `private`, `public`, `protected` |

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

### What is Polymorphism?
- **Polymorphism** means "many forms" - the ability of objects to take multiple forms
- Same method name can behave differently in different classes
- Achieved through method overloading and method overriding

### Types of Polymorphism:
1. **Compile-time Polymorphism (Static):**
   - Method Overloading
   - Operator Overloading (not in Java)

2. **Runtime Polymorphism (Dynamic):**
   - Method Overriding
   - Interface implementation

### Method Overloading Example:
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
```

### Method Overriding Example:
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
```

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

| Characteristic         | Description                                         |
|-----------------------|-----------------------------------------------------|
| **Platform Independent** | Java code is compiled into bytecode, which can run on any system with a Java Virtual Machine (JVM). This enables the "Write Once, Run Anywhere" (WORA) capability. |
| **Object-Oriented**      | Java is based on the principles of object-oriented programming, using objects and classes to organize code. |
| **Simple**               | Java has a clean and easy-to-understand syntax, making it straightforward to learn and use. |
| **Secure**               | Java provides built-in security features such as bytecode verification, no explicit pointers, and a security manager. |
| **Robust**               | Java emphasizes reliability with strong memory management, automatic garbage collection, and comprehensive exception handling. |
| **Multithreaded**        | Java supports multithreading, allowing concurrent execution of two or more threads for maximum CPU utilization. |
| **Interpreted**          | Java bytecode is interpreted (and optionally compiled at runtime) by the JVM, making it platform-independent. |
| **High Performance**     | Java achieves high performance through Just-In-Time (JIT) compilation and efficient memory management. |
| **Dynamic**              | Java supports dynamic loading of classes at runtime, enabling flexible and extensible applications. |
| **Distributed**          | Java provides built-in networking libraries (like RMI and sockets) to create distributed applications that can communicate over networks. |
| **Portable**             | Java programs are portable across platforms because there are no implementation-dependent features and the same bytecode runs on any JVM. |

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

| Concept | Purpose | Key Feature | Java Implementation |
|---------|---------|-------------|-------------------|
| **Object** | Real-world entity | State + Behavior | `new` keyword |
| **Class** | Blueprint for objects | Template | `class` keyword |
| **Abstraction** | Hide complexity | Essential features only | Abstract classes, Interfaces |
| **Encapsulation** | Bundle data + methods | Data hiding | Private attributes, Public methods |
| **Inheritance** | Code reuse | IS-A relationship | `extends` keyword |
| **Polymorphism** | Multiple forms | Same method, different behavior | Overloading, Overriding |

---