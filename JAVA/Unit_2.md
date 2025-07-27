# PYQs Summary (Quick Links)

1. [What is the role of class path in Java Package?](#pyq-q20-what-is-the-role-of-class-path-in-java-package)
2. [Object is an instance of class, justify your answer.](#pyq-q21-object-is-an-instance-of-class-justify-your-answer)
3. [Explain the role of constructor and also explain how subclass constructor implicitly calls superclass constructor in Java.](#pyq-q22-explain-the-role-of-constructor-and-also-explain-how-subclass-constructor-implicitly-calls-superclass-constructor-in-java)
4. [What do you mean by abstract class? How abstract class is different from Interface?](#pyq-q23-what-do-you-mean-by-abstract-class-how-abstract-class-is-different-from-interface)
5. [Describe in detail about the types of inheritance in Java.](#pyq-q24-describe-in-detail-about-the-types-of-inheritance-in-java)
6. [Which is the alternative approach to implement multiple inheritances in Java? Explain, with an example?](#pyq-q25-which-is-the-alternative-approach-to-implement-multiple-inheritances-in-java-explain-with-an-example)
7. [Use of inheritance in OOPS](#pyq-q26-use-of-inheritance-in-oops)
8. [Use of Super Keyword and example](#pyq-q27-use-of-super-keyword-and-example)
9. [Diff between Abstract Class and Interface](#pyq-q28-diff-between-abstract-class-and-interface)
10. [What is ServerSocket in java.net package?](#pyq-q29-what-is-serversocket-in-javanet-package)

---

# Java Unit 2: Inheritance, Interfaces, Packages, Networking (with PYQs)

---

## Inheritance in Java

Inheritance is a fundamental concept in OOP (Object-Oriented Programming) that allows a class (subclass) to inherit properties and behaviors (fields and methods) from another class (superclass).

- **Super Class:** The class whose features are inherited.
- **Sub Class:** The class that inherits features from the superclass.
- **Protected Members:** Members marked as `protected` are accessible within the same package and by subclasses.
- **Constructors in Subclasses:** Subclass constructors can call superclass constructors using `super()`.
- **Object Class:** The root class of all Java classes. Every class in Java implicitly extends `Object`.

### Types of Inheritance in Java

**PYQ Q24. Describe in detail about the types of inheritance in Java.**

Inheritance means acquiring properties and behaviors from another class. Java supports several types:

1. **Single Inheritance**
   - One subclass inherits from one superclass.
   - Example:
     ```java
     class Animal {}
     class Dog extends Animal {}
     ```
2. **Multilevel Inheritance**
   - A subclass inherits from a superclass, and another subclass inherits from that subclass.
   - Example:
     ```java
     class Animal {}
     class Dog extends Animal {}
     class Puppy extends Dog {}
     ```
3. **Hierarchical Inheritance**
   - Multiple subclasses inherit from one superclass.
   - Example:
     ```java
     class Animal {}
     class Dog extends Animal {}
     class Cat extends Animal {}
     ```
4. **Multiple Inheritance**
   - A class inherits from more than one class. **Not supported for classes in Java** (to avoid confusion if two parents have the same method).
| Type         | Structure / Example                                                                 |
|--------------|-------------------------------------------------------------------------------------|
| Single       | `A → B`<br>*(One subclass inherits from one superclass)*                            |
| Multilevel   | `A → B → C`<br>*(A superclass, a subclass, and a subclass of that subclass)*        |
| Hierarchical | <pre>   A<br>  / \<br>B   C</pre><br>*(Multiple subclasses inherit from one superclass)* |
| Multiple     | *Not supported for classes in Java*<br>*(Achieved via interfaces only)*             |

**Note:**

- Java supports multiple inheritance through interfaces, not classes.

---

### Use of Inheritance in OOPS

**PYQ Q26. Use of inheritance in OOPS**

**Uses of Inheritance:**

1. **Code Reusability:** Common code is written in the superclass and reused by subclasses.
2. **Method Overriding:** Subclasses can provide their own implementation for methods defined in the superclass.
3. **Polymorphism:** Allows objects to be treated as instances of their superclass, enabling flexible code.
4. **Logical Hierarchy:** Organizes classes in a logical structure, making code easier to understand and maintain.
5. **Extensibility:** New features can be added by creating new subclasses.

**Example:**

```java
class Animal {
    void eat() { System.out.println("Eating..."); }
}
class Dog extends Animal {
    void bark() { System.out.println("Barking..."); }
}
Dog d = new Dog();
d.eat(); // Inherited from Animal
d.bark(); // Defined in Dog
```

---

### Super Keyword

**PYQ Q27. Use of Super Keyword and example**

**Uses of `super` keyword:**

1. Access parent class variables when they are hidden by subclass variables.
2. Call parent class methods when overridden in subclass.
3. Call parent class constructor from subclass constructor.

**Examples:**
**Accessing parent variable:**

```java
class Animal {
    String color = "white";
}
class Dog extends Animal {
    String color = "black";
    void printColor() {
        System.out.println(super.color); // prints white
        System.out.println(color); // prints black
    }
}
```

**Calling parent method:**

```java
class Animal {
    void eat() { System.out.println("Animal eats"); }
}
class Dog extends Animal {
    void eat() {
        super.eat(); // calls Animal's eat
        System.out.println("Dog eats");
    }
}
```

**Calling parent constructor:**

```java
class Animal {
    Animal() { System.out.println("Animal constructor"); }
}
class Dog extends Animal {
    Dog() { super(); System.out.println("Dog constructor"); }
}
```

---

### Constructors in Subclasses

**PYQ Q22. Explain the role of constructor and also explain how subclass constructor implicitly calls superclass constructor in Java.**

**Role of Constructor in Java:**

- A constructor is a special method used to initialize objects when they are created.
- It sets up initial values for object fields and can perform setup tasks.
- Constructors have the same name as the class and do not have a return type.

**Types of Constructors:**

- Default constructor (no parameters)
- Parameterized constructor (with parameters)

**How Subclass Constructor Calls Superclass Constructor:**

- When you create an object of a subclass, its constructor is called.
- Before the subclass constructor runs, Java automatically calls the superclass constructor (using `super()`), even if you do not write it explicitly.
- If you want to call a specific superclass constructor, you can use `super(parameters)` as the first line in the subclass constructor.

**Example:**

```java
class Parent {
    Parent() { System.out.println("Parent constructor"); }
}
class Child extends Parent {
    Child() { System.out.println("Child constructor"); }
}
public class Test {
    public static void main(String[] args) {
        Child c = new Child();
    }
}
// Output:
// Parent constructor
// Child constructor
```

**Example with parameterized constructor:**

```java
class Parent {
    Parent(String msg) { System.out.println(msg); }
}
class Child extends Parent {
    Child() { super("Hello from Parent!"); System.out.println("Child constructor"); }
}
```

---

### Object Class

**PYQ Q21. Object is an instance of class, justify your answer.**

**Explanation:**

- A class in Java is like a blueprint or template. It defines what data (fields) and actions (methods) an object will have.
- An object is a real, usable thing created from a class. It has its own values for the fields and can use the methods.

**Points:**

1. Class defines structure; object is the actual thing in memory.
2. You can create many objects from one class, each with different data.
3. Objects interact with each other using methods.

**Example:**

```java
class Student {
    String name;
    int rollNo;
    void display() {
        System.out.println(name + " " + rollNo);
    }
}
public class Test {
    public static void main(String[] args) {
        Student s = new Student(); // s is an object (instance) of Student
        s.name = "Amit";
        s.rollNo = 101;
        s.display(); // Output: Amit 101
    }
}
```

---

## Abstract Classes and Methods

- **Abstract Class:** A class declared with `abstract` keyword. It may have abstract methods (without body) and concrete methods (with body).
- Cannot be instantiated directly.
- Used as a base for other classes.

**PYQ Q23. What do you mean by abstract class? How abstract class is different from Interface?**

**Abstract Class:**

- Declared with `abstract` keyword.
- Can have abstract methods (no body) and concrete methods (with body).
- Cannot be instantiated directly.
- Used as a base for other classes.

**Interface:**

- Declared with `interface` keyword.
- All methods are abstract by default (Java 7), but from Java 8, can have default and static methods.
- Cannot have instance fields (only static final fields).
- Used to achieve multiple inheritance and abstraction.

**Differences Table:**
| Feature | Abstract Class | Interface |
| -------------- | ------------------- | ---------------------- |
| Methods | Abstract + Concrete | Only abstract (Java 7) |
| Variables | Instance/Static | Static + final |
| Inheritance | Single | Multiple |
| Constructor | Yes | No |
| Implementation | Partial | Full (by implementing) |

**Key Points:**

- Abstract class can have method bodies, interfaces cannot (until Java 8 default methods).
- A class can implement multiple interfaces but can extend only one abstract class.

**Example:**

```java
abstract class Animal {
    abstract void sound();
    void eat() { System.out.println("Eating..."); }
}
class Dog extends Animal {
    void sound() { System.out.println("Bark"); }
}

interface Vehicle {
    void run();
}
class Car implements Vehicle {
    public void run() { System.out.println("Car is running"); }
}
```

---

## Interfaces in Java

- **Defining an Interface:** Use `interface` keyword.
- **Implementing Interface:** Use `implements` keyword in a class.
- **Extending Interfaces:** An interface can extend another interface.
- **Object Cloning:** Use `Cloneable` interface and `clone()` method.
- **Inner Classes:** Classes defined within another class.

**PYQ Q25. Which is the alternative approach to implement multiple inheritances in Java? Explain, with an example?**

**Explanation:**

- Java does not support multiple inheritance for classes to avoid ambiguity.
- The alternative is to use interfaces. A class can implement multiple interfaces.

**Example:**

```java
interface A { void show(); }
interface B { void display(); }
class C implements A, B {
    public void show() { System.out.println("Show"); }
    public void display() { System.out.println("Display"); }
}
```

**How it works:**

- Class `C` gets methods from both interfaces `A` and `B`.
- This is how Java achieves multiple inheritance.

---

**PYQ Q28. Diff between Abstract Class and Interface**

**PYQ Q28. Diff between Abstract Class and Interface**

**Abstract Class:**

- Can have method bodies (concrete methods) and abstract methods.
- Supports single inheritance.
- Can have constructors.
- Can have instance variables.

**Interface:**

- Only method signatures (Java 7), but can have default/static methods (Java 8+).
- Supports multiple inheritance.
- No constructors.
- Only static final variables.

**Summary Table:**
| Feature | Abstract Class | Interface |
| -------------- | ------------------- | ---------------------- |
| Methods | Abstract + Concrete | Only abstract (Java 7) |
| Variables | Instance/Static | Static + final |
| Inheritance | Single | Multiple |
| Constructor | Yes | No |
| Implementation | Partial | Full (by implementing) |

---

## Packages in Java

- **Defining Package:** Use `package` keyword at the top of the file.
- **Importing Package:** Use `import` keyword.
- **Static Import:** Use `import static` for static members.
- **Naming Convention:** Lowercase, reverse domain (e.g., `com.example.app`)
- **Making JAR Files:** Use `jar` tool to bundle classes.

**PYQ Q20. What is the role of class path in Java Package?**

**Explanation:**

- CLASSPATH is an environment variable in Java.
- It tells the Java Virtual Machine (JVM) and Java compiler where to look for user-defined classes and packages.
- If you use packages or external libraries, you must set CLASSPATH so Java can find them.

**How to set CLASSPATH:**

- On Windows: `set CLASSPATH=C:\myclasses;.`
- On Linux/Mac: `export CLASSPATH=/home/user/myclasses:.`

**Points:**

1. If CLASSPATH is not set, Java looks in the current directory by default.
2. You can include multiple paths separated by `;` (Windows) or `:` (Linux/Mac).
3. Required for running programs that use external packages or JAR files.

**Example:**
Suppose you have a package `com.mycompany.utils` in `C:\myclasses`, set CLASSPATH to include that folder.

---

## Networking in Java (`java.net` package)

- Provides classes for networking (TCP/IP, UDP, sockets).
- Common classes: `Socket`, `ServerSocket`, `InetAddress`, `URL`, `URLConnection`

**PYQ Q29. What is ServerSocket in java.net package?**

**Explanation:**

- `ServerSocket` is a class in the `java.net` package used for server-side socket programming.
- It allows a server application to listen for incoming client connections on a specific port.
- When a client connects, the server accepts the connection and communicates using a `Socket` object.

**Points:**

1. Used for TCP/IP communication.
2. The server must specify a port number (e.g., 8080).
3. The `accept()` method waits (blocks) until a client connects.
4. After accepting, you can read/write data using streams.

**Example:**

```java
import java.net.*;
import java.io.*;
public class ServerExample {
    public static void main(String[] args) throws IOException {
        ServerSocket ss = new ServerSocket(8080); // create server socket
        System.out.println("Waiting for client...");
        Socket s = ss.accept(); // waits for client
        System.out.println("Client connected!");
        // You can now use s.getInputStream() and s.getOutputStream()
        ss.close();
    }
}
```

---

## Summary Table

| Topic                | Key Points / Example                       |
| -------------------- | ------------------------------------------ |
| Inheritance          | Superclass, subclass, protected, super     |
| Types of Inheritance | Single, multilevel, hierarchical           |
| Abstract Class       | Abstract/concrete methods, base class      |
| Interface            | Multiple inheritance, implements, extends  |
| Object Class         | Root of all classes                        |
| Object Cloning       | Cloneable interface, clone()               |
| Inner Classes        | Class within class                         |
| Packages             | package/import/static import/JAR/CLASSPATH |
| Networking           | java.net, ServerSocket, Socket             |

---
