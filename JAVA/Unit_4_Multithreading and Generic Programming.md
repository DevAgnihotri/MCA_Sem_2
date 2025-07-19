# Multithreading in Java: Complete Notes

---

## 1. Introduction to Multithreading and Multitasking

**Definition of Thread (Q1, Q5):**

- A **thread** is a small part of a program that can run independently at the same time as other parts.  
- Threads share the same memory and resources of the main program but each thread does its own work separately.  
- In Java, threads help you do many things at once, like downloading a file while showing a progress bar.  
- Simply put, a thread lets your program do more than one task at the same time.

**Definition of Process:**

- A **process** is an independent program in execution, with its own memory space, code, data, and system resources (such as open files and network connections).
- Processes are isolated from each other by the operating system, so one process cannot directly access the memory or resources of another process.
- Communication between processes (Inter-Process Communication, IPC) is more complex and slower compared to threads.

**Multitasking:**

- **Multitasking** is the ability of an operating system or environment to execute multiple tasks (programs or processes) seemingly at the same time by rapidly switching between them.
- There are two main types:

  1. **Process-based multitasking:** Multiple independent programs (processes) run simultaneously. Each process has its own memory and resources. Example: Running a web browser and a text editor at the same time.
  2. **Thread-based multitasking:** Multiple threads within the same program run concurrently, sharing the same memory and resources. Example: A media player playing music (one thread) while downloading album art (another thread).

- Multitasking improves system efficiency and responsiveness, especially on multi-core processors, by allowing better resource utilization and parallelism.
- In Java, thread-based multitasking is commonly used to perform background tasks, improve performance, and keep applications responsive.

**Q2 & Q6: Compare thread-based and process-based multitasking (mutual answer)**

| Feature             | Process-based Multitasking              | Thread-based Multitasking       |
| ------------------- | --------------------------------------- | ------------------------------- |
| Basic Unit          | Process                                 | Thread                          |
| Memory              | Separate for each process               | Shared among threads            |
| Communication       | Slow (IPC needed)                       | Fast (shared memory)            |
| Overhead            | High                                    | Low                             |
| Context Switch      | Slow                                    | Fast                            |
| Example             | Running Word & Chrome                   | Download + play music           |
| Resource Allocation | Allocated per process                   | Shared within process           |
| Failure Impact      | One process crash doesn't affect others | Thread crash may affect process |
| Security/Isolation  | High (isolated by OS)                   | Low (shared address space)      |
| Creation Time       | Slower (more resources)                 | Faster (less resources)         |
| Scalability         | Limited by OS resources                 | More scalable within a process  |
| Use Case            | Running independent apps                | Handling tasks in same app      |

---

## 2. Thread Life Cycle (Q1)

A thread in Java goes through several states during its life:

**Thread States:**

1. **New:** Thread is created but not started yet.
2. **Runnable:** Thread is ready to run and waiting for CPU.
3. **Running:** Thread is currently executing.
4. **Blocked/Waiting:** Thread is waiting for a resource or signal.
5. **Timed Waiting:** Thread is waiting for a specified time.
6. **Terminated (Dead):** Thread has finished execution.

**Diagram: Thread Life Cycle**

![Thread Life Cycle](https://www.tutorialspoint.com/java/images/thread_life_cycle.jpg)

**Explanation:**

- A thread starts in the New state, moves to Runnable when `start()` is called, and then to Running when scheduled by the CPU.
- It can move to Blocked/Waiting if it needs a resource or is waiting for another thread.
- It returns to Runnable when notified or resource is available.
- It ends in Terminated after `run()` completes.

---

## 3. Creating Threads in Java (Q3, Q5, Q7)

There are two main ways to create a thread in Java:

### a) By Extending the Thread Class (Q7)

- Create a class that extends `Thread`.
- Override the `run()` method.
- Create an object and call `start()`.

**Example:**

```java
// Q7: Creating a thread by extending Thread class
class MyThread extends Thread {
    public void run() {
        System.out.println("Thread is running");
    }
}
public class Test {
    public static void main(String[] args) {
        MyThread t = new MyThread();
        t.start();
    }
}
```

### b) By Implementing the Runnable Interface (Q3, Q5)

- Create a class that implements `Runnable`.
- Override the `run()` method.
- Pass an object of your class to a `Thread` object and call `start()`.

**Example:**

```java
class MyRunnable implements Runnable {
    public void run() {
        System.out.println("Runnable thread running");
    }
}
public class Test {
    public static void main(String[] args) {
        Thread t = new Thread(new MyRunnable());
        t.start();
    }
}
```

**Runnable vs Thread**

| Feature     | Extending Thread           | Implementing Runnable     |
| ----------- | -------------------------- | ------------------------- |
| Inheritance | Can't extend another class | Can extend another class  |
| Code Reuse  | Less                       | More                      |
| Flexibility | Less                       | More                      |
| Use Case    | Simple threads             | When you need inheritance |

---

## 4. Synchronizing Threads (Q4)

**What is Synchronization?**

- Synchronization is a mechanism that ensures only one thread can access a shared resource (like a variable, object, or file) at a time.
- It is essential when multiple threads modify or read shared data, to prevent problems like data inconsistency, race conditions, or corrupted results.
- Without synchronization, two or more threads could simultaneously update the same data, leading to unpredictable outcomes.

**Why Synchronization is Needed:**

- Imagine two threads incrementing the same counter variable at the same time. Without synchronization, both threads might read the same value before either writes back, causing one increment to be lost.
- Synchronization ensures that only one thread can execute a critical section (the part of code that accesses shared resources) at a time.

**How to Synchronize:**

- In Java, you can use the `synchronized` keyword to mark a method or a block of code as synchronized.
- When a thread enters a synchronized method or block, it acquires a lock (monitor) on the object. Other threads trying to enter any synchronized method/block on the same object will be blocked until the lock is released.

**Ways to Synchronize:**

1. **Synchronized Methods:**  
   The entire method is locked for one thread at a time.
   ```java
   class Counter {
        private int count = 0;
        public synchronized void increment() {
             count++;
        }
   }
   ```
2. **Synchronized Blocks:**  
   Only a specific block of code is locked, allowing finer control and potentially better performance.
   ```java
   class Counter {
        private int count = 0;
        public void increment() {
             synchronized(this) {
                   count++;
             }
        }
   }
   ```

**Key Points:**

- Synchronization can be applied to static methods as well, locking the class object.
- Overusing synchronization can lead to performance issues or deadlocks if not managed carefully.

---

## 5. Daemon Threads (Q4)

**What is a Daemon Thread?**

- A daemon thread is a special type of thread that runs in the background to perform tasks such as garbage collection, monitoring, or housekeeping.
- Daemon threads are low-priority threads that do not prevent the JVM from exiting. When all user (non-daemon) threads finish, the JVM will terminate, even if daemon threads are still running.
- Typical uses include background services, timers, or cleanup tasks that should not block application shutdown.

**How to Create a Daemon Thread:**

- You can make any thread a daemon by calling `setDaemon(true)` before starting the thread.
- Once started, you cannot change a thread's daemon status.

**Example:**

```java
class MyDaemon extends Thread {
     public void run() {
          while (true) {
                System.out.println("Daemon thread running...");
                try { Thread.sleep(1000); } catch (InterruptedException e) {}
          }
     }
}

public class TestDaemon {
     public static void main(String[] args) {
          MyDaemon daemon = new MyDaemon();
          daemon.setDaemon(true); // Must be called before start()
          daemon.start();

          System.out.println("Main thread finished.");
          // JVM will exit after main thread ends, stopping the daemon
     }
}
```

**Key Points:**

- Daemon threads are useful for background tasks that should not block application exit.
- If only daemon threads remain, the JVM will shut down automatically.
- Always set a thread as daemon before calling `start()`, otherwise an `IllegalThreadStateException` will be thrown.

---

---

## 6. Inter-thread Communication

**Why Needed?**

- Sometimes threads need to coordinate their actions, such as in the producer-consumer problem, where one thread produces data and another consumes it.
- Without proper communication, a consumer might try to consume data before it is produced, or a producer might overwrite data before it is consumed.

**How to Communicate:**

- Java provides the `wait()`, `notify()`, and `notifyAll()` methods for inter-thread communication.
- These methods must be called from within a synchronized context (inside a synchronized method or block).
  - `wait()`: Causes the current thread to release the lock and wait until another thread calls `notify()` or `notifyAll()` on the same object.
  - `notify()`: Wakes up one waiting thread.
  - `notifyAll()`: Wakes up all waiting threads.

**Example (Producer-Consumer Concept):**

- **Producer thread** calls `produce()`, puts data in the buffer, and calls `notify()` to wake up the consumer.
- **Consumer thread** calls `consume()`, waits if no data is available, and calls `notify()` after consuming to wake up the producer.

**Key Points:**

- Always use `wait()`, `notify()`, and `notifyAll()` inside synchronized blocks/methods to avoid `IllegalMonitorStateException`.
- Inter-thread communication helps avoid busy-waiting and enables efficient thread cooperation.
- Common use cases: producer-consumer, reader-writer, and thread pools.

---

## 7. Thread Groups

**What is a Thread Group?**

- A thread group is a way to group multiple threads into a single object for easier management.
- You can start, interrupt, or set priorities for all threads in a group at once.
- Useful for organizing threads in large applications, monitoring, or applying common operations.

**How to Create and Use:**

```java
// Creating a thread group
ThreadGroup group = new ThreadGroup("MyGroup");

// Creating threads in the group
Thread t1 = new Thread(group, "Thread1") {
    public void run() {
        System.out.println("Thread1 running in group: " + Thread.currentThread().getThreadGroup().getName());
    }
};
Thread t2 = new Thread(group, "Thread2") {
    public void run() {
        System.out.println("Thread2 running in group: " + Thread.currentThread().getThreadGroup().getName());
    }
};

// Starting threads
t1.start();
t2.start();
```

**Key Points:**

- You can enumerate, interrupt, or set priorities for all threads in a group.
- Thread groups can be nested (a group can have subgroups).
- Modern Java often uses thread pools (`ExecutorService`) instead of thread groups for advanced management.

---

## 8. Summary Table

| Topic              | Key Points / Technical Terms                                                                                 |
| ------------------ | ------------------------------------------------------------------------------------------------------------ |
| Thread             | Smallest unit of execution within a process; shares memory, has its own stack and execution context          |
| Process            | Independent program in execution; has its own memory space and resources; isolated from other processes      |
| Multitasking       | Running multiple tasks seemingly at once; includes process-based and thread-based multitasking               |
| Thread Life Cycle  | States: New, Runnable, Running, Blocked/Waiting, Timed Waiting, Terminated; transitions managed by JVM       |
| Creating Threads   | Two ways: extend Thread class or implement Runnable interface; use `start()` to begin execution              |
| Synchronization    | Mechanism to control access to shared resources; uses `synchronized` keyword to prevent race conditions      |
| Daemon Thread      | Background thread; JVM exits when only daemon threads remain; set with `setDaemon(true)` before `start()`    |
| Inter-thread Comm. | Coordination between threads using `wait()`, `notify()`, `notifyAll()`; must be used in synchronized context |
| Thread Group       | Organizes multiple threads for collective management; can start, interrupt, or set priorities for a group    |
| Use Cases          | Examples: background tasks, producer-consumer, thread pools, resource sharing, responsive applications       |

---

# Generic Programming in Java: Complete Notes

## 1. Introduction to Generic Programming (Q9, Q10, Q11)

**What is Generic Programming? (Q9, Q10, Q11)**

- Generic programming is a paradigm that enables you to write code that can handle different data types using a single implementation. In Java, this is achieved through **generics**, which allow classes, interfaces, and methods to operate on objects of various types while maintaining strong type safety.
- **Generics** introduce the concept of **type parameters** (like `<T>`) that act as placeholders for actual types, enabling code reuse and reducing redundancy.
- With generics, the Java compiler performs **compile-time type checking**, which helps catch type-related errors early and eliminates the need for explicit type casting.
- Technical terms: type parameter, type safety, compile-time checking, type inference, parameterized types.

**Why Use Generics?**

- To avoid code duplication by writing logic once for any type, rather than repeating it for each specific type.
- To catch type errors at compile time, making code safer and reducing runtime exceptions.
- To make code more reusable, flexible, and easier to maintain.
- To improve readability by making the intended type usage explicit.

**Example (without generics):**

```java
ArrayList list = new ArrayList();
list.add("Hello");
list.add(123); // No error at compile time, but may cause problems at runtime
String s = (String) list.get(0); // Requires casting
```

**Example (with generics):**

```java
ArrayList<String> list = new ArrayList<>();
list.add("Hello");
// list.add(123); // Compile-time error: incompatible types
String s = list.get(0); // No casting needed
```

- Using generics, you ensure that only the specified type (e.g., `String`) can be added to the collection, preventing accidental misuse and making your code more robust.

**Advantages and Disadvantages of Generics (Q11):**

| Advantages                                   | Disadvantages / Limitations                                 |
| -------------------------------------------- | ----------------------------------------------------------- |
| Type safety at compile time                  | Cannot use primitive types directly (e.g., `int`, `double`) |
| Code reusability and flexibility             | Type information is erased at runtime (type erasure)        |
| No need for explicit type casting            | Cannot create arrays of generic types (e.g., `T[]`)         |
| Fewer runtime errors (early error detection) | Cannot use `instanceof` with parameterized types            |
| Cleaner, more readable and maintainable code | Cannot instantiate generic type parameters (`new T()`)      |
| Supports compile-time checking               | Static members cannot use type parameters                   |
| Enables implementation of generic algorithms | Cannot create generic exceptions or catch them              |
| Reduces code duplication                     | Type parameters cannot be used in static contexts           |
| Works well with collections framework        | Some reflection operations are limited                      |

---

## 2. Generic Classes (Q9, Q10, Q11, Q12)

**What is a Generic Class?**

- A **generic class** is a class that can operate on objects of various types while providing compile-time type safety.
- It uses a **type parameter** (like `<T>`) as a placeholder for the actual type that will be specified when an object is created.
- Syntax: `class ClassName<T> { ... }`
- Technical terms: type parameter, parameterized class, type argument, type inference.

**Why Use Generic Classes?**

- To write reusable, type-safe code that works with any object type.
- To avoid code duplication (no need to write separate classes for each data type).
- To catch type errors at compile time, reducing runtime exceptions.
- To eliminate the need for explicit type casting.

**Example: Basic Generic Class**

```java
class Box<T> {
    private T value;
    public void set(T value) { this.value = value; }
    public T get() { return value; }
}
```

**How to Use:**

```java
Box<Integer> intBox = new Box<>();
intBox.set(10);
System.out.println(intBox.get()); // Output: 10

Box<String> strBox = new Box<>();
strBox.set("Hello");
System.out.println(strBox.get()); // Output: Hello
```

**Q12: Bounded Generic Classes (with example)**

- Sometimes you want to restrict the types that can be used as type parameters.
- Use **bounded types** with `extends` (for upper bound) or `super` (for lower bound).

**Example (Q12):**

```java
// Only allow Number or its subclasses
class NumericBox<T extends Number> {
    private T num;
    public NumericBox(T num) { this.num = num; }
    public double doubleValue() { return num.doubleValue(); }
}
```

---

## 3. Generic Methods

**What is a Generic Method?**

- A **generic method** is a method that introduces its own type parameter(s), allowing it to operate on different types independently of any generic type parameters declared by its class.
- Syntax: `<T> ReturnType methodName(T param)`
- Generic methods can be declared in both generic and non-generic classes.

**Why Use Generic Methods?**

- To write reusable, type-safe methods that work with any type.
- To avoid code duplication for similar logic that operates on different types.
- To enable compile-time type checking and eliminate the need for explicit casting.

**When to Use Generic Methods?**

- When the logic of a method is independent of the type of data it processes.
- When you want to perform operations like printing, swapping, comparing, or processing elements of any type.
- When you need to write utility/helper methods that should work for multiple types (e.g., sorting arrays, finding maximum/minimum, etc.).

**Example: Print Array Elements**

```java
public <T> void printArray(T[] array) {
    for (T item : array) {
        System.out.println(item);
    }
}
```

---

## 4. Bounded Types: Restrictions and Limitations (Q12)

**What are Bounded Types?**

- Bounded types restrict the kinds of types that can be used as generic parameters.
- Use `extends` for upper bounds (e.g., `<T extends Number>`) and `super` for lower bounds (e.g., `<? super Integer>`).

**Why Use Bounds?**

- To ensure that the type parameter has certain properties or methods (e.g., only numbers can be used for math operations).

**Limitations of Generics:**

- Cannot use primitive types directly (use wrapper classes like Integer, Double)
- Cannot create arrays of generic types (e.g., `T[] arr = new T[10];` is not allowed)
- Type information is erased at runtime (type erasure)
- Cannot use `instanceof` with parameterized types (e.g., `if (obj instanceof Box<String>)` is not allowed)
- Cannot instantiate generic type parameters (e.g., `new T()` is not allowed)
- Cannot create static fields or methods that use type parameters (type parameters are not available in static context)
- Cannot throw or catch generic types (e.g., `catch (T e)` is not allowed)
- Cannot use generic type parameters in exception classes
- Cannot use generic type parameters with `synchronized` blocks (e.g., `synchronized(T.class)` is not allowed)
- Cannot perform explicit type casting to a parameterized type (e.g., `(Box<String>) obj` may cause warnings)
- Cannot create generic enums or generic annotation types
- Type parameters cannot be used with reflection to obtain runtime type information

---

## 5. Q8: Generic Program for Sum or Merge

**Q8: Write a generic Java program that displays the sum if numeric data is passed and merges text if string data is passed.**

**Example:**

```java
class Utility {
    public static <T> void process(T a, T b) {
        if (a instanceof Number && b instanceof Number) {
            double sum = ((Number)a).doubleValue() + ((Number)b).doubleValue();
            System.out.println("Sum: " + sum);
        } else if (a instanceof String && b instanceof String) {
            System.out.println("Merged: " + a.toString() + b.toString());
        } else {
            System.out.println("Unsupported types");
        }
    }
}
// Usage:
// Utility.process(10, 20); // Output: Sum: 30.0
// Utility.process("Hello", "World"); // Output: Merged: HelloWorld
```

---

## 6. Summary Table

| Topic            | Key Points / Technical Terms                                                                                       |
| ---------------- | ------------------------------------------------------------------------------------------------------------------ |
| Generics         | Enables code to work with any reference type; provides compile-time type safety; reduces code duplication          |
| Generic Class    | Class with type parameter(s) (e.g., `<T>`); allows creation of type-safe, reusable classes                         |
| Generic Method   | Method with its own type parameter(s); can be used in generic or non-generic classes; enables flexible utilities   |
| Bounded Type     | Restricts type parameter using `extends` (upper bound) or `super` (lower bound); ensures type has required methods |
| Type Erasure     | Type parameters are removed at compile time; generic type info not available at runtime                            |
| Limitations      | Cannot use primitives as type parameters; cannot create arrays of generic types; cannot instantiate type parameter |
| Type Safety      | Compile-time checking prevents invalid type assignments; eliminates need for explicit casting                      |
| Code Reusability | Write logic once for any type; improves maintainability and reduces redundancy                                     |
| Wildcards        | Use `?`, `? extends T`, `? super T` for flexible method parameters and collections                                 |
| Use Cases        | Collections framework, utility classes, algorithms (sorting, searching), type-safe containers                      |

## PYQs inluded

1. What is a thread? Explain the life cycle of a thread with a proper diagram.
2. Compare thread-based and process-based multitasking in Java.
3. Explain the different ways to create a thread in Java.
4. Discuss synchronizing threads and daemon threads.
5. Differentiate the usage of `Runnable` and `Thread` for multithreading.
6. What is the difference between process-based and thread-based multitasking?
7. Give the two ways by which a thread can be created using Java. Write a short program to demonstrate the creation of a new thread by extending the `Thread` class.
8. Write a generic Java program that displays the sum if numeric data is passed and merges text if string data is passed.
9. Explain generic programming concepts in Java.
10. Discuss generic programming in Java.
11. What do you mean by generics in Java? Explain the advantages and disadvantages of generic programming in Java.
12. Discuss generic bounded classes with the help of a suitable example.

