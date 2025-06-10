# Object Oriented Programming (OOP) in Java

Object Oriented Programming (OOP) is a programming paradigm based on the concept of "objects," which can contain data and code to manipulate that data. Java is a language that strongly supports OOP principles.

Java is a programming language that uses the ideas of Object-Oriented Programming (OOP). In Java, you create "objects" to represent real things, like cars, people, or animals. Each object has its own data (like a car's color or speed) and methods (like driving or stopping).

Java is called "class-based" because you first define a "class" as a blueprint. Then, you make objects from that class. This helps you organize your code, reuse it in different places, and keep it easy to understand.

By using OOP in Java, you can:

- Break big problems into smaller parts (objects)
- Reuse code by making new objects from existing classes
- Protect data by hiding details inside objects
- Make your programs easier to change and fix

In short, Java helps you write programs that are organized, reusable, and simple to maintain by using objects and classes.

### Key Features:

- **Class-based structure:**  
  Java organizes code into classes, which act as blueprints for creating objects.
- **Support for OOP principles:**  
  Java supports the four fundamental principles of Object-Oriented Programming:

  1. **Abstraction:** Hiding implementation details and exposing only the essential features.
  2. **Encapsulation:** Wrapping data (fields) and methods into a single unit (class) and restricting access using access modifiers.
  3. **Inheritance:** Allowing a class to inherit properties and methods from another class, promoting code reuse.
  4. **Polymorphism:** Enabling a single interface to represent different underlying forms (e.g., method overloading and overriding).

- **Built-in access modifiers:**  
  Java provides four access levels to control visibility:
  - `private`: Accessible only within the same class.
  - `public`: Accessible from anywhere.
  - `protected`: Accessible within the same package and subclasses.
  - Default (no modifier): Accessible within the same package.

**Syntax Example:**

```java
public class ClassName {
    // fields (variables) and methods
}
```

**Use Case:**  
OOP principles are ideal for building robust, modular, and scalable applications. For example, in a car-related Java application, you can model cars as objects with attributes like `color`, `model`, and `speed`, and behaviors like `drive()` and `brake()`.

---

## 🔹 Related Concepts

### ➤ Constructor

**Definition:**  
A constructor is a special method invoked when an object is created. It is used to initialize the object's state (fields). Constructors have the same name as the class and do not have a return type.

**Real-Life Example:**  
Think of a **Car factory** that uses a constructor to create a fully set-up car. For example, when a car is manufactured, it is initialized with specific attributes like its model, color, and engine type.

**Syntax:**

```java
ClassName() {
    // initialization code
}
```

**Code Example:**

```java
class Car {
    String model;
    String color;

    // Constructor
    Car(String model, String color) {
        this.model = model;
        this.color = color;
        System.out.println("Car constructed: " + model + " in " + color);
    }
}
```

**Use Case:**  
Constructors are particularly useful for automatically initializing object data during creation. For example:

```java
public class Main {
    public static void main(String[] args) {
        Car car1 = new Car("Sedan", "Red");
        Car car2 = new Car("SUV", "Blue");
    }
}
```

**Output:**

```
Car constructed: Sedan in Red
Car constructed: SUV in Blue
```

---

### Comparison: Abstract Class vs Interface

#### Key Differences Table

| Sr. No. | Parameter            | Class                                                              | Interface                                                                      |
| ------- | -------------------- | ------------------------------------------------------------------ | ------------------------------------------------------------------------------ |
| 1       | Supported Methods    | Can have both abstract and concrete methods                        | Can have only abstract methods (Java 8+ allows default and static methods)     |
| 2       | Multiple Inheritance | Not supported                                                      | Supported                                                                      |
| 3       | Supported Variables  | Can have final, non-final, static, and non-static variables        | Only static and final variables are permitted                                  |
| 4       | Implementation       | A class can implement an interface                                 | Interface cannot implement another interface, but can extend another interface |
| 5       | Keyword              | Declared using `class` keyword                                     | Declared using `interface` keyword                                             |
| 6       | Inheritance (Class)  | Can inherit another class using `extends` and implement interfaces | Can inherit only an interface using `extends`                                  |
| 7       | Inheritance (Usage)  | Can be inherited using `extends` keyword                           | Can only be implemented using `implements` keyword                             |
| 8       | Access               | Can have any type of members: `private`, `public`, etc.            | Members are implicitly `public`                                                |
| 9       | Constructor          | Can have constructors                                              | Cannot have constructors                                                       |

#### Additional Comparison Table

| Parameter                     | Abstract Class                                                   | Interface                                                                                        |
| ----------------------------- | ---------------------------------------------------------------- | ------------------------------------------------------------------------------------------------ |
| Default Method Implementation | Can have default method implementation                           | Provides pure abstraction; cannot have implementation (except default/static methods in Java 8+) |
| Variables                     | May contain non-final variables                                  | Variables are by default `public static final`                                                   |
| Keyword Used                  | Extended using `extends` keyword                                 | Implemented using `implements` keyword                                                           |
| Access Modifiers              | Can have `public`, `protected`, `private`, and default modifiers | Methods are by default `public`; cannot use other access modifiers                               |
| Speed of Implementation       | Faster than interface                                            | Slightly slower; requires extra indirection                                                      |
| Normal Class Extension        | Can extend only one abstract class                               | Can implement multiple interfaces                                                                |
| Constructors                  | Can have constructors                                            | Cannot have constructors                                                                         |
| Multiple Inheritance          | Can extend another class and implement multiple interfaces       | Can extend another interface only                                                                |

## 🔹 1. Objects

**Definition:** An object is an instance of a class. It represents a real-world entity with state and behavior.

**Key Characteristics of Objects:**

- **State:** Represented by attributes or fields (e.g., a car's color, brand, and model).
- **Behavior:** Represented by methods or functions (e.g., a car can drive, brake, or honk).
- **Identity:** Each object has a unique identity, which distinguishes it from other objects, even if they have the same state and behavior.

**How Objects Work:**

- Objects are created using the `new` keyword in Java.
- They occupy memory space and can interact with other objects through method calls.

**Advantages of Using Objects:**

- **Modularity:** Objects help break down complex systems into smaller, manageable parts.
- **Reusability:** Objects can be reused across different parts of a program or even in other programs.
- **Encapsulation:** Objects bundle data and methods together, promoting data security and abstraction.

**Example in Real Life:**

- A **Person** object can have attributes like name, age, and height (state) and behaviors like walking, talking, and eating (methods).

**Code Example:**

```java
class Person {
    String name;
    int age;

    void introduce() {
        System.out.println("Hi, my name is " + name + " and I am " + age + " years old.");
    }
}

public class Main {
    public static void main(String[] args) {
        Person person = new Person();
        person.name = "Alice";
        person.age = 25;
        person.introduce();
    }
}
```

**Output:**

```
Hi, my name is Alice and I am 25 years old.
```

---

## 🔹 2. Classes

**Definition:** A class is a blueprint from which individual objects are created. It defines fields and methods.

**Key Characteristics of Classes:**

- **Blueprint for Objects:** A class provides the structure and behavior that its objects will have.
- **Encapsulation:** Classes encapsulate data and methods, ensuring modularity and security.
- **Reusability:** Classes can be reused in different parts of a program or in other programs.
- **Inheritance Support:** Classes can inherit properties and behaviors from other classes, promoting code reuse.

**Components of a Class:**

1. **Fields (Attributes):** Variables that hold the state of the object.
2. **Methods:** Functions that define the behavior of the object.
3. **Constructors:** Special methods used to initialize objects.
4. **Access Modifiers:** Keywords like `public`, `private`, `default` and `protected` that control access to class members.

**Real-Life Example:** A **Car class** is a blueprint. Multiple car objects like sedan, SUV, and hatchback can be made from it.

**Syntax:**

```java
class ClassName {
    // fields
    // methods
}
```

**Code Example:**

```java
class Car {
    String model;
    int year;

    void honk() {
        System.out.println("Honking");
    }
}
```

**Use Case:** Organizing car-related data and behaviors like honking and model/year info.

**Advantages of Using Classes:**

- **Modularity:** Classes help divide a program into smaller, manageable parts.
- **Abstraction:** Classes allow hiding of implementation details while exposing only necessary functionalities.
- **Scalability:** Classes make it easier to scale applications by adding new features or modifying existing ones.

**Best Practices for Defining Classes:**

- Use meaningful names for classes that reflect their purpose.
- Keep classes focused on a single responsibility (Single Responsibility Principle).
- Use access modifiers to enforce encapsulation.
- Document the purpose and usage of the class for better maintainability.
- Avoid making classes unnecessarily large; split them into smaller, cohesive classes if needed.

---

## 🔹 3. Abstraction

**Definition:** Abstraction is the process of hiding the internal details of a showing only the relevant information to the user. It focuses on "what" an object does rather than "how" it does it.

**Key Characteristics of Abstraction:**

- **Simplification:** Reduces complexity by showing only the relevant details to the user.
- **Focus on Functionality:** Allows developers to focus on high-level design without worrying about implementation details.
- **Improved Maintainability:** Changes to the internal implementation do not affect the external interface.

**Real-Life Example:** A **Car dashboard** provides controls like steering, accelerator, and speedometer. The user interacts with these controls without needing to understand the internal mechanics of the engine or transmission.

**Types of Abstraction in Java:**

1. **Abstract Classes:** Classes that cannot be instantiated and may contain both abstract (unimplemented) and concrete (implemented) methods.
2. **Interfaces:** Fully abstract types that define a contract for classes to implement.

### ➤ Abstract Classes

**Syntax:**

```java
abstract class ClassName {
    // Abstract method (no body)
    abstract void methodName();

    // Concrete method (with body)
    void concreteMethod() {
        System.out.println("This is a concrete method.");
    }
}
```

**Code Example:**

```java
abstract class Car {
    abstract void start();

    void stop() {
        System.out.println("Car is stopping.");
    }
}

class Sedan extends Car {
    void start() {
        System.out.println("Sedan starting with key.");
    }
}

public class Main {
    public static void main(String[] args) {
        Car myCar = new Sedan();
        myCar.start();
        myCar.stop();
    }
}
```

**Output:**

```
Sedan starting with key.
Car is stopping.
```

**Use Case:** Abstract classes are useful when we want to provide a common base class with some shared functionality while allowing subclasses to define specific behaviors.

### ➤ Interfaces

**Syntax:**

```java
interface InterfaceName {
    void methodName();
}
```

**Code Example:**

```java
interface Vehicle {
    void start();
    void stop();
}

class Bike implements Vehicle {
    public void start() {
        System.out.println("Bike starting with kick.");
    }

    public void stop() {
        System.out.println("Bike is stopping.");
    }
}

public class Main {
    public static void main(String[] args) {
        Vehicle myBike = new Bike();
        myBike.start();
        myBike.stop();
    }
}
```

**Output:**

```
Bike starting with kick.
Bike is stopping.
```

**Use Case:** Interfaces are ideal for defining a contract that multiple classes can implement, ensuring consistency across different implementations.

**Advantages of Abstraction:**

- **Code Reusability:** Abstract classes and interfaces promote code reuse by defining common behaviors.
- **Flexibility:** Allows developers to change the implementation without affecting the external interface.
- **Security:** Hides sensitive implementation details from the user.

**Best Practices for Abstraction:**

- Use abstract classes when you need to share code among related classes.
- Use interfaces when you need to define a contract for unrelated classes.
- Avoid overusing abstraction, as it can lead to unnecessary complexity.

> 📘 **Note:** Abstraction is a cornerstone of OOP, enabling developers to build scalable and maintainable applications by separating concerns and focusing on high-level design.

---

## 🔹 4. Encapsulation

**Definition:** Encapsulation is the technique of wrapping data (variables) and code (methods) together as a single unit and restricting access to some components. It ensures that the internal representation of an object is hidden from the outside world, exposing only what is necessary.

**Key Characteristics of Encapsulation:**

- **Data Hiding:** Internal details of an object are hidden, and only a controlled interface is exposed.
- **Access Control:** Access modifiers like `private`, `protected`, and `public` are used to control access to class members.
- **Improved Security:** Sensitive data is protected from unauthorized access or modification.
- **Ease of Maintenance:** Changes to the internal implementation do not affect external code that uses the object.

**Advantages of Encapsulation:**

1. **Improved Code Maintainability:** Encapsulation allows changes to the internal implementation without affecting external code.
2. **Enhanced Security:** By restricting access to certain components, encapsulation prevents unintended interference or misuse.
3. **Modularity:** Encapsulation helps in dividing a program into smaller, manageable parts.
4. **Reusability:** Encapsulated code can be reused across different parts of a program or in other programs.
5. **Flexibility:** Encapsulation allows developers to modify the internal workings of a class without impacting its external behavior.

**Real-Life Example:** A **Car's speedometer**—you can see the speed but can't directly change the way it calculates speed. The internal mechanism is hidden, and only the result is exposed.

**How Encapsulation Works in Java:**

1. Declare the variables of a class as `private`.
2. Provide `public` getter and setter methods to access and update the values of private variables.

**Syntax (getter/setter):**

```java
private Type var;
public Type getVar();
public void setVar(Type val);
```

**Code Example:**

```java
class Car {
    private int speed;

    // Getter method
    public int getSpeed() {
        return speed;
    }

    // Setter method
    public void setSpeed(int s) {
        if (s >= 0) { // Adding validation
            speed = s;
        } else {
            System.out.println("Speed cannot be negative.");
        }
    }
}

public class Main {
    public static void main(String[] args) {
        Car myCar = new Car();
        myCar.setSpeed(50); // Setting speed
        System.out.println("Car speed: " + myCar.getSpeed()); // Getting speed
    }
}
```

**Output:**

```
Car speed: 50
```

**Best Practices for Encapsulation:**

1. Always declare class variables as `private` to restrict direct access.
2. Use meaningful names for getter and setter methods, following the naming convention (`getVariableName`, `setVariableName`).
3. Add validation logic in setter methods to ensure data integrity.
4. Avoid exposing unnecessary internal details through getter and setter methods.
5. Document the purpose of each getter and setter method for better maintainability.

> 📘 **Note:** Encapsulation is a fundamental principle of OOP that promotes data security, modularity, and maintainability, making it easier to build robust and scalable applications.

---

## 🔹 5. Inheritance

**Definition:** Inheritance is a mechanism in object-oriented programming that allows one class (child or subclass) to inherit the properties and behaviors of another class (parent or superclass). It promotes code reuse and establishes a natural hierarchy between classes.

**Real-Life Example:** An **ElectricCar** inherits general properties from a **Car** like wheels, steering, and the ability to drive, while adding its own unique behavior, such as charging the battery.

---

### ➤ Subclasses and Superclasses in Inheritance:

1. **Superclass (Parent Class):**

   - A superclass, also known as a _base class_ or _parent class_, is the class from which other classes inherit. It contains common attributes and methods that can be shared across multiple subclasses.
   - The superclass provides a foundation of functionality that can be reused and extended by its subclasses.
   - Example: In a `Vehicle` superclass, attributes like `speed` and methods like `start()` can be defined, which are common to all types of vehicles.

2. **Subclass (Child Class):**

   - A subclass, also known as a _derived class_ or _child class_, is a class that inherits from a superclass. It can use the attributes and methods of the superclass and also define its own unique behavior.
   - Subclasses can override methods from the superclass to provide specific implementations or add new methods and attributes.
   - Example: A `Car` subclass can inherit from the `Vehicle` superclass and add specific attributes like `numberOfDoors` or override the `start()` method to include additional functionality.

3. **Relationship Between Subclass and Superclass:**

   - The subclass is a specialized version of the superclass. This "is-a" relationship is a key principle of inheritance. For example, a `Car` is a `Vehicle`.
   - Subclasses can access public and protected members of the superclass but cannot directly access private members unless accessor methods (like getters and setters) are provided.

4. **Terminology Recap:**

   - Superclass: Also called _base class_ or _parent class_.
   - Subclass: Also called _derived class_ or _child class_.

5. **Example in Java:**

   ```java
   // Superclass
   class Vehicle {
       int speed;

       void start() {
           System.out.println("Vehicle is starting");
       }
   }

   // Subclass
   class Car extends Vehicle {
       int numberOfDoors;

       @Override
       void start() {
           System.out.println("Car is starting");
       }
   }

   public class Main {
       public static void main(String[] args) {
           Car myCar = new Car();
           myCar.start(); // Output: Car is starting
       }
   }
   ```

### ➤ Syntax:

```java
class ParentClass {
    // fields and methods
}

class ChildClass extends ParentClass {
    // additional fields and methods
}
```

---

### ➤ Code Example:

```java
class Car {
    String brand;

    void drive() {
        System.out.println("Driving a car");
    }
}

class ElectricCar extends Car {
    int batteryCapacity;

    void charge() {
        System.out.println("Charging the battery");
    }
}

public class Main {
    public static void main(String[] args) {
        ElectricCar myElectricCar = new ElectricCar();
        myElectricCar.brand = "Tesla";
        myElectricCar.batteryCapacity = 100;
        myElectricCar.drive(); // Inherited from Car
        myElectricCar.charge(); // Defined in ElectricCar
    }
}
```

**Output:**

```
Driving a car
Charging the battery
```

---

### ➤ Types of Inheritance in Java:

1. **Single Inheritance:** A child class inherits from one parent class.

   ```java
   class Parent {}
   class Child extends Parent {}
   ```

2. **Multilevel Inheritance:** A class inherits from a child class, forming a chain.

   ```java
   class Grandparent {}
   class Parent extends Grandparent {}
   class Child extends Parent {}
   ```

3. **Hierarchical Inheritance:** Multiple child classes inherit from a single parent class.
   ```java
   class Parent {}
   class Child1 extends Parent {}
   class Child2 extends Parent {}
   ```

> 📘 **Note:** Java does not support multiple inheritance with classes to avoid ambiguity (the "diamond problem"). However, it can be achieved using interfaces.

---

### ➤ Method Overriding in Inheritance:

Child classes can provide their own implementation of a method defined in the parent class. This is known as **method overriding**.

**Code Example:**

```java
class Car {
    void start() {
        System.out.println("Starting a generic car");
    }
}

class SportsCar extends Car {
    @Override
    void start() {
        System.out.println("Starting a sports car with a roar");
    }
}

public class Main {
    public static void main(String[] args) {
        Car myCar = new SportsCar();
        myCar.start(); // Calls the overridden method in SportsCar
    }
}
```

**Output:**

```
Starting a sports car with a roar
```

---

### ➤ Advantages of Inheritance:

1. **Code Reusability:** Reduces duplication by reusing existing code in parent classes.
2. **Improved Maintainability:** Changes in the parent class automatically propagate to child classes.
3. **Extensibility:** Allows adding new features to child classes without modifying the parent class.
4. **Polymorphism:** Enables dynamic method invocation, improving flexibility and scalability.

---

### ➤ Best Practices for Using Inheritance:

1. **Use Inheritance for "Is-A" Relationships:** Ensure the child class is a specialized version of the parent class (e.g., an ElectricCar "is a" Car).
2. **Avoid Deep Inheritance Hierarchies:** Keep the hierarchy shallow to reduce complexity and improve readability.
3. **Favor Composition Over Inheritance:** Use composition when a "Has-A" relationship is more appropriate (e.g., a Car "has a" Engine).
4. **Override Methods Judiciously:** Only override methods when necessary to provide specific behavior in the child class.
5. **Document the Hierarchy:** Clearly document the purpose of each class in the hierarchy for better maintainability.

> 📘 **Note:** Inheritance is a powerful tool in OOP, but it should be used carefully to avoid tight coupling and maintain a clean, modular design.

---

---

## 🔹 6. Polymorphism

**Definition:** Polymorphism is one of the core principles of Object-Oriented Programming (OOP). It allows a single interface or method to represent different behaviors based on the object or context. The term "polymorphism" is derived from the Greek words "poly" (many) and "morph" (forms), meaning "many forms."

**Real-Life Example:** Consider the action of starting a car. Different types of cars may start in different ways:

- A traditional car may start with a key.
- A modern car may start with a push-button.
- A luxury car may start remotely using a mobile app.

Despite the differences in implementation, the action is conceptually the same: starting the car.

---

### ➤ Types of Polymorphism in Java

Java supports two types of polymorphism:

1. **Compile-Time Polymorphism (Method Overloading):**

   - Achieved by defining multiple methods with the same name but different parameter lists within the same class.
   - The method to be called is determined at compile time based on the method signature.

2. **Run-Time Polymorphism (Method Overriding):**
   - Achieved by defining a method in a subclass with the same name and signature as a method in its superclass.
   - The method to be called is determined at runtime based on the actual object type.

---

### ➤ Compile-Time Polymorphism (Method Overloading)

**Definition:** Method overloading allows multiple methods in the same class to have the same name but different parameter lists (number, type, or order of parameters). It is resolved during the compilation phase.

**Key Characteristics:**

- Methods must have the same name but different parameter lists.
- Return type can be the same or different.
- It is a form of static binding.

**Syntax:**

```java
class ClassName {
     returnType methodName(param1);
     returnType methodName(param1, param2);
}
```

**Code Example:**

```java
class Car {
     // Method with no parameters
     void start() {
          System.out.println("Starting the car");
     }

     // Overloaded method with one parameter
     void start(String mode) {
          System.out.println("Starting the car in " + mode + " mode");
     }

     // Overloaded method with two parameters
     void start(String mode, int speed) {
          System.out.println("Starting the car in " + mode + " mode at speed " + speed + " km/h");
     }
}

public class Main {
     public static void main(String[] args) {
          Car myCar = new Car();
          myCar.start(); // Calls the method with no parameters
          myCar.start("Eco"); // Calls the method with one parameter
          myCar.start("Sport", 100); // Calls the method with two parameters
     }
}
```

**Output:**

```
Starting the car
Starting the car in Eco mode
Starting the car in Sport mode at speed 100 km/h
```

**Use Case:** Method overloading is useful when you want to provide multiple ways to perform the same action, such as starting a car with different configurations.

---

### ➤ Run-Time Polymorphism (Method Overriding)

**Definition:** Method overriding allows a subclass to provide a specific implementation of a method that is already defined in its superclass. It is resolved during the runtime phase.

**Key Characteristics:**

- The method in the subclass must have the same name, return type, and parameter list as the method in the superclass.
- The `@Override` annotation is used to indicate that a method is being overridden.
- It is a form of dynamic binding.

**Syntax:**

```java
class SuperClass {
     returnType methodName() {
          // implementation
     }
}

class SubClass extends SuperClass {
     @Override
     returnType methodName() {
          // new implementation
     }
}
```

**Code Example:**

```java
// Superclass
class Car {
     void start() {
          System.out.println("Starting a generic car");
     }
}

// Subclass
class SportsCar extends Car {
     @Override
     void start() {
          System.out.println("Starting a sports car with a roar");
     }
}

public class Main {
     public static void main(String[] args) {
          Car myCar = new SportsCar(); // Polymorphic reference
          myCar.start(); // Calls the overridden method in SportsCar
     }
}
```

**Output:**

```
Starting a sports car with a roar
```

**Use Case:** Method overriding is useful when you want to allow subclasses to define their own specific behavior while maintaining a consistent interface.

---

### ➤ Differences Between Method Overloading and Method Overriding

| Feature         | Method Overloading                     | Method Overriding                     |
| --------------- | -------------------------------------- | ------------------------------------- |
| **Definition**  | Same method name, different parameters | Same method name, same parameters     |
| **Binding**     | Static (compile-time)                  | Dynamic (runtime)                     |
| **Inheritance** | Not required                           | Requires inheritance                  |
| **Return Type** | Can be different                       | Must be the same or covariant         |
| **Annotation**  | Not required                           | `@Override` annotation is recommended |

---

### ➤ Advantages of Polymorphism

1. **Code Reusability:** Polymorphism allows the same method to be reused for different types of objects or scenarios.
2. **Flexibility:** Enables dynamic method invocation, allowing behavior to be determined at runtime.
3. **Extensibility:** Makes it easier to extend existing code by adding new classes or methods without modifying existing ones.
4. **Improved Readability:** Reduces code duplication and improves clarity by using a consistent interface.

---

### ➤ Best Practices for Using Polymorphism

1. **Use Method Overloading for Convenience:** Provide multiple ways to perform the same action, but avoid excessive overloading that can confuse users.
2. **Use Method Overriding for Specialization:** Allow subclasses to define their own behavior while maintaining a consistent interface.
3. **Leverage the `@Override` Annotation:** Always use the `@Override` annotation to ensure that the method is correctly overriding a superclass method.
4. **Avoid Overusing Polymorphism:** While polymorphism is powerful, overusing it can lead to complex and hard-to-maintain code.
5. **Document Behavior Clearly:** Clearly document the behavior of overloaded and overridden methods to avoid confusion.

> 📘 **Note:** Polymorphism is a cornerstone of OOP, enabling developers to write flexible, reusable, and maintainable code. By mastering polymorphism, you can design systems that are both robust and scalable.

---

### ➤ Interface

**Definition:** An interface is a contract that a class can implement. It contains abstract methods only.

**Real-Life Example:** A **Car control interface** defines buttons like accelerate and brake. Any car can implement these.

**Syntax:**

```java
interface InterfaceName {
    void method();
}
```

**Code Example:**

```java
interface CarFeatures {
    void playMusic();
}

class LuxuryCar implements CarFeatures {
    public void playMusic() {
        System.out.println("Playing music in car");
    }
}
```

**Use Case:** Implementing a common set of features across various car types.

---

### ➤ "this" Keyword

**Definition:** The `this` keyword refers to the current instance of the class.

**Real-Life Example:** Inside a **Car object**, saying "this color" refers to the specific car's color.

**Syntax:**

```java
this.variableName = variableName;
```

**Code Example:**

```java
class Car {
    String brand;
    Car(String brand) {
        this.brand = brand;
    }
}
```

**Use Case:** Clarifying object fields when variable names conflict with method parameters.

---

> 📘 **Note:** Mastery of OOP concepts leads to better design and development of clean, maintainable Java applications.

---

## 🔹 7. Packages

**Definition:**  
A package in Java is a namespace that organizes classes and interfaces. It helps avoid name conflicts and makes it easier to manage and structure large projects.

---

### ➤ Defining a Package

To define a package, use the `package` keyword at the top of your Java file. For example:

```java
package com.example.myapp;

public class MyClass {
    public void display() {
        System.out.println("This is MyClass in com.example.myapp package.");
    }
}
```

**Advantages of Packages:**

1. **Organized Code:** Helps group related classes and interfaces together.
2. **Avoids Name Conflicts:** Prevents naming clashes by providing unique namespaces.
3. **Access Control:** Provides access protection with public, private, and protected modifiers.
4. **Reusability:** Makes it easier to reuse classes across different projects.

---

### ➤ Setting the CLASSPATH for Packages

The `CLASSPATH` environment variable tells the Java compiler and JVM where to look for user-defined classes and packages.

**Steps to Set CLASSPATH:**

1. Locate the directory containing your package.
2. Add the directory path to the `CLASSPATH` variable.

**Example (Windows):**

```bash
set CLASSPATH=C:\myproject\classes;
```

**Example (Linux/Mac):**

```bash
export CLASSPATH=/home/user/myproject/classes
```

**Note:** You can also use the `-cp` option with `javac` and `java` commands to specify the classpath.

---

### ➤ Making JAR Files for Library Packages

A JAR (Java Archive) file is a compressed file format used to bundle Java classes, metadata, and resources into a single file.

**Steps to Create a JAR File:**

1. Compile your Java files into `.class` files.
2. Use the `jar` command to create the JAR file.

**Example:**

```bash
jar cf mylibrary.jar -C classes/ .
```

- `c`: Create a new JAR file.
- `f`: Specify the file name.
- `-C`: Change to the specified directory.

**Using the JAR File:**

Add the JAR file to your `CLASSPATH`:

```bash
java -cp mylibrary.jar com.example.myapp.MyClass
```

---

### ➤ Import and Static Import

**Import:**  
The `import` keyword allows you to use classes from other packages without specifying their fully qualified names.

**Example:**

```java
import java.util.Scanner;

public class Main {
    public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in);
        System.out.println("Enter your name: ");
        String name = scanner.nextLine();
        System.out.println("Hello, " + name);
    }
}
```

**Static Import:**  
The `static import` keyword allows you to access static members of a class directly, without qualifying them with the class name.

**Example:**

```java
import static java.lang.Math.*;

public class Main {
    public static void main(String[] args) {
        System.out.println("Square root of 16: " + sqrt(16));
        System.out.println("Value of PI: " + PI);
    }
}
```

---

### ➤ Naming Conventions for Packages

1. **Use Lowercase Letters:** Package names should be in lowercase to avoid conflicts with class names.
2. **Follow Domain Name Structure:** Use your organization's domain name in reverse as the package name prefix (e.g., `com.example.myapp`).
3. **Be Descriptive:** Use meaningful names that reflect the purpose of the package.

**Example:**

- `com.companyname.projectname.module`

---

## 🔹 8. Networking (`java.net` Package)

**Definition:**  
The `java.net` package provides classes for networking operations, such as creating sockets, sending and receiving data, and building networked applications.

---

### ➤ Key Classes in `java.net`

1. **`InetAddress`:** Represents an IP address.

   - **Example:**

     ```java
     import java.net.InetAddress;

     public class Main {
         public static void main(String[] args) throws Exception {
             InetAddress address = InetAddress.getByName("www.google.com");
             System.out.println("IP Address: " + address.getHostAddress());
         }
     }
     ```

2. **`URL`:** Represents a Uniform Resource Locator.

   - **Example:**

     ```java
     import java.net.URL;

     public class Main {
         public static void main(String[] args) throws Exception {
             URL url = new URL("https://www.example.com");
             System.out.println("Protocol: " + url.getProtocol());
             System.out.println("Host: " + url.getHost());
             System.out.println("Port: " + url.getPort());
         }
     }
     ```

3. **`HttpURLConnection`:** Used for HTTP communication.

   - **Example:**

     ```java
     import java.net.HttpURLConnection;
     import java.net.URL;

     public class Main {
         public static void main(String[] args) throws Exception {
             URL url = new URL("https://www.example.com");
             HttpURLConnection connection = (HttpURLConnection) url.openConnection();
             connection.setRequestMethod("GET");
             System.out.println("Response Code: " + connection.getResponseCode());
         }
     }
     ```

4. **`Socket` and `ServerSocket`:** Used for TCP communication.

   - **Example (Client):**

     ```java
     import java.io.OutputStream;
     import java.net.Socket;

     public class Client {
         public static void main(String[] args) throws Exception {
             Socket socket = new Socket("localhost", 8080);
             OutputStream output = socket.getOutputStream();
             output.write("Hello, Server!".getBytes());
             socket.close();
         }
     }
     ```

   - **Example (Server):**

     ```java
     import java.io.InputStream;
     import java.net.ServerSocket;
     import java.net.Socket;

     public class Server {
         public static void main(String[] args) throws Exception {
             ServerSocket serverSocket = new ServerSocket(8080);
             Socket socket = serverSocket.accept();
             InputStream input = socket.getInputStream();
             byte[] data = new byte[1024];
             int bytesRead = input.read(data);
             System.out.println("Received: " + new String(data, 0, bytesRead));
             socket.close();
             serverSocket.close();
         }
     }
     ```

5. **`DatagramSocket` and `DatagramPacket`:** Used for UDP communication.

   - **Example:**

     ```java
     import java.net.DatagramPacket;
     import java.net.DatagramSocket;

     public class UDPExample {
         public static void main(String[] args) throws Exception {
             DatagramSocket socket = new DatagramSocket();
             String message = "Hello, UDP!";
             DatagramPacket packet = new DatagramPacket(message.getBytes(), message.length(), InetAddress.getByName("localhost"), 8080);
             socket.send(packet);
             socket.close();
         }
     }
     ```

---

### ➤ Advantages of `java.net`

1. **Simplified Networking:** Provides high-level abstractions for common networking tasks.
2. **Cross-Platform:** Works seamlessly across different operating systems.
3. **Built-in Support:** No need for external libraries for basic networking operations.

---

> 📘 **Note:** The `java.net` package is a powerful tool for building networked applications, from simple client-server programs to complex web-based systems.

---

This concludes the detailed explanation of packages and networking in Java.
