# Java Fundamentals

## 1. Java Environment, Java Source File Structure, and Compilation

### 1.1 Java Environment

The Java environment includes all the tools and settings needed to write, compile, and run Java programs.

#### Components:

- **JDK (Java Development Kit):** Contains tools to write and compile Java code.
- **JRE (Java Runtime Environment):** Contains libraries and JVM to run Java programs.
- **JVM (Java Virtual Machine):** Executes Java bytecode on any platform.

> Think of the JDK as your car manufacturing tools, the JRE as your testing facility, and the JVM as the engine that runs the car.

### 1.2 Java Source File Structure

A typical Java program has this structure:

```java
// Car.java
public class Car {
    // variables
    String model;
    int speed;

    // method
    public void startEngine() {
        System.out.println("Engine started");
    }
}
```

#### Breakdown:

- `public class Car` - Every Java file should have a class with the same name as the file.
- Variables like `model` and `speed` store data.
- `startEngine()` is a method (function inside a class).

### 1.3 Compilation Process (Detailed)

The compilation process in Java involves several steps that transform human-readable source code into machine-executable instructions. Here's a detailed breakdown:

#### Step 1: Writing the Source Code

- You write Java code in a `.java` file using a text editor or an Integrated Development Environment (IDE).
- Example:
  ```java
  // Car.java
  public class Car {
          public static void main(String[] args) {
                  System.out.println("Car is running");
          }
  }
  ```

#### Step 2: Compilation

- The Java compiler (`javac`) translates the `.java` file into a `.class` file containing **bytecode**.
- Bytecode is a platform-independent, intermediate representation of the program.
- Command:
  ```bash
  javac Car.java
  ```
- Output:
  - A `Car.class` file is generated in the same directory.

#### Step 3: Class Loading

- The **ClassLoader** loads the `.class` file into memory.
- It verifies the bytecode for security and correctness using the **Bytecode Verifier**.

#### Step 4: Bytecode Interpretation

- The **JVM (Java Virtual Machine)** reads the bytecode and interprets it into native machine code.
- The JVM uses the **Just-In-Time (JIT) Compiler** to optimize frequently executed code by converting it into native code for faster execution.

#### Step 5: Execution

- The JVM executes the native machine code on the host system.
- Execution starts from the `main()` method.

---

### What Happens Internally?

1. **Source Code to Bytecode:**

   - The Java compiler checks for syntax errors.
   - If the code is valid, it generates a `.class` file containing bytecode.

2. **Bytecode Verification:**

   - The Bytecode Verifier ensures the bytecode adheres to Java's security and integrity rules.
   - It prevents malicious code from accessing unauthorized memory or performing illegal operations.

3. **Class Loading:**

   - The ClassLoader loads required classes dynamically during runtime.
   - It follows a delegation model:
     - **Bootstrap ClassLoader**: Loads core Java classes (e.g., `java.lang`).
     - **Extension ClassLoader**: Loads classes from the `ext` directory.
     - **Application ClassLoader**: Loads classes from the application's classpath.

4. **Execution by JVM:**
   - The JVM interprets bytecode or compiles it into native code using the JIT Compiler.
   - Native code is executed directly by the CPU.

---

### Analogy for Better Understanding

- **Source Code**: Writing a recipe in your language.
- **Compilation**: Translating the recipe into a universal format (bytecode).
- **Class Loading**: Loading the recipe into a kitchen.
- **Execution**: Cooking the dish using the recipe.

---

### Tools Involved in Compilation

| Tool    | Purpose                                      |
| ------- | -------------------------------------------- |
| `javac` | Compiles `.java` files into `.class` files.  |
| `java`  | Executes the `.class` file using the JVM.    |
| JIT     | Optimizes bytecode into native machine code. |

> The entire process ensures that Java programs are platform-independent and secure while maintaining high performance.

---

## 2. Fundamental Programming Structures in Java

### 2.1 Methods

A method is a group of statements that perform a specific task.

#### Structure:

```java
modifier returnType methodName(parameters) {
    // method body
}
```

#### Example:

```java
public void drive(int distance) {
    System.out.println("Car drove " + distance + " kilometers.");
}
```

### 2.1.1 Types of Methods

| Type               | Description                    | Example                          |
| ------------------ | ------------------------------ | -------------------------------- |
| Void Method        | Does not return a value        | `public void honk()`             |
| Return Type Method | Returns a value                | `public int getSpeed()`          |
| Static Method      | Belongs to class, not instance | `public static void totalCars()` |
| Instance Method    | Requires object to be called   | `myCar.drive(50);`               |
| Parameterized      | Accepts input                  | `drive(int distance)`            |
| Non-Parameterized  | Takes no input                 | `public void stop()`             |

### 2.2 Modifiers (Access + Non-access)

Modifiers change the accessibility and behavior of classes, methods, and variables.

#### Access Modifiers Table:

| Modifier  | Scope & Usage                                |
| --------- | -------------------------------------------- |
| public    | Anywhere (any class)                         |
| private   | Only within the declared class               |
| protected | Same package + subclasses                    |
| default   | Only in the same package (no keyword needed) |

### Examples of Access Modifiers

#### 1. `public` Modifier

A `public` member can be accessed from anywhere.

```java
// File: Main.java
public class Main {
    public String message = "Hello, World!";

    public void displayMessage() {
        System.out.println(message);
    }
}

// File: Test.java
public class Test {
    public static void main(String[] args) {
        Main main = new Main();
        System.out.println(main.message); // Accessing public variable
        main.displayMessage();           // Accessing public method
    }
}
```

#### 2. `private` Modifier

A `private` member can only be accessed within the same class.

```java
public class Car {
    private String model = "Sedan";

    private void displayModel() {
        System.out.println("Model: " + model);
    }

    public void showDetails() {
        displayModel(); // Accessing private method within the same class
    }
}

public class Test {
    public static void main(String[] args) {
        Car car = new Car();
        // car.model; // Error: model has private access
        // car.displayModel(); // Error: displayModel() has private access
        car.showDetails(); // Indirect access through public method
    }
}
```

#### 3. `protected` Modifier

A `protected` member can be accessed within the same package or by subclasses.

```java
// File: Vehicle.java
package vehicles;

public class Vehicle {
    protected String type = "Car";

    protected void displayType() {
        System.out.println("Vehicle Type: " + type);
    }
}

// File: Car.java
package vehicles;

public class Car extends Vehicle {
    public void showDetails() {
        System.out.println(type); // Accessing protected variable
        displayType();            // Accessing protected method
    }
}

// File: Test.java
package test;

import vehicles.Car;

public class Test {
    public static void main(String[] args) {
        Car car = new Car();
        car.showDetails(); // Accessing protected members through subclass
    }
}
```

#### 4. `default` (Package-Private) Modifier

A member with no modifier is accessible only within the same package.

```java
// File: Bike.java
package vehicles;

class Bike {
    String brand = "Yamaha"; // Default access modifier

    void displayBrand() { // Default access modifier
        System.out.println("Brand: " + brand);
    }
}

// File: Test.java
package vehicles;

public class Test {
    public static void main(String[] args) {
        Bike bike = new Bike();
        System.out.println(bike.brand); // Accessing default variable
        bike.displayBrand();           // Accessing default method
    }
}

// File: TestOutside.java
package test;

import vehicles.Bike;

public class TestOutside {
    public static void main(String[] args) {
        // Bike bike = new Bike(); // Error: Bike is not public
        // bike.brand; // Error: brand has default access
    }
}
```

#### Non-access Modifiers Table:

| Modifier     | Use                                                         |
| ------------ | ----------------------------------------------------------- |
| static       | Belongs to class, not object                                |
| final        | Cannot be changed after assignment (like `final int speed`) |
| abstract     | Method without a body, to be implemented in subclass        |
| synchronized | Used in multi-threading to avoid race conditions            |
| transient    | Prevents serialization of a variable                        |
| volatile     | Variable changes are visible across threads                 |

### 2.3 Static Members

Static members belong to the class itself, not instances.

```java
public class Car {
    static int numberOfCars = 0;

    Car() {
        numberOfCars++;
    }
}
```

> All Car objects share the same `numberOfCars`. It tracks how many cars were created.

### 2.4 Comments

Comments are used to explain code, improve readability, and make maintenance easier.

#### Types:

- **Single-line:** `// This starts the engine`
- **Multi-line:**

```java
/*
 This method is used to drive the car.
 It accepts distance in kilometers.
*/
```

#### Why Use Comments?

- Help others (and yourself) understand code later
- Describe complex logic
- Disable code during testing

---

## 3. Data Types

### 3.1 Primitive Data Types Table

| Type    | Size (bytes) | Range                      | Example                    |
| ------- | ------------ | -------------------------- | -------------------------- |
| byte    | 1            | -128 to 127                | `byte gear = 3;`           |
| short   | 2            | -32,768 to 32,767          | `short rpm = 3000;`        |
| int     | 4            | -2^31 to 2^31-1            | `int speed = 120;`         |
| long    | 8            | -2^63 to 2^63-1            | `long mileage = 100000;`   |
| float   | 4            | ~±3.40282347E+38F          | `float temp = 98.6f;`      |
| double  | 8            | ~±1.79769313486231570E+308 | `double fuel = 45.5;`      |
| char    | 2            | 0 to 65535 (Unicode)       | `char mode = 'D';`         |
| boolean | 1 bit        | true or false              | `boolean engineOn = true;` |

### 3.2 Reference Data Types

- **String**: `String model = "SUV";`
- **Arrays**: `int[] speeds = {80, 100, 120};`
- **Objects**: `Car myCar = new Car();`

---

## 4. Variables

Variables store data values.

### Types:

- **Local**: Inside methods
- **Instance**: Inside a class, not static
- **Static**: Shared across all instances

```java
public class Car {
    int speed;          // instance
    static int count;   // static

    public void setSpeed(int s) {
        int temp = s;  // local
        speed = temp;
    }
}
```

---

## 5. Operators

### Arithmetic Operators

| Operator | Meaning        | Example   | Result |
| -------- | -------------- | --------- | ------ |
| +        | Addition       | 50 + 30   | 80     |
| -        | Subtraction    | 100 - 20  | 80     |
| \*       | Multiplication | 5 \* 1000 | 5000   |
| /        | Division       | 400 / 2   | 200    |
| %        | Modulus        | 403 % 200 | 3      |

### Relational Operators

| Operator | Description      | Example     |
| -------- | ---------------- | ----------- |
| >        | Greater than     | speed > 60  |
| <        | Less than        | speed < 120 |
| >=       | Greater or equal | rpm >= 3000 |
| <=       | Less or equal    | fuel <= 50  |
| ==       | Equal to         | gear == 'D' |
| !=       | Not equal to     | mode != 'P' |

### Logical Operators

| Operator | Meaning     | Example                 |
| -------- | ----------- | ----------------------- | ---------- | ---------- | --- | ---------- |
| `&&`     | Logical AND | `engineOn && speed > 0` |
| `        |             | `                       | Logical OR | `fuel < 10 |     | warningOn` |
| `!`      | Logical NOT | `!engineOn`             |

### Assignment Operators

| Operator | Description            | Example     |
| -------- | ---------------------- | ----------- |
| =        | Assigns value          | speed = 80  |
| +=       | Adds and assigns       | speed += 10 |
| -=       | Subtracts and assigns  | fuel -= 5   |
| \*=      | Multiplies and assigns | rpm \*= 2   |
| /=       | Divides and assigns    | range /= 2  |
| %=       | Modulus and assigns    | fuel %= 10  |
