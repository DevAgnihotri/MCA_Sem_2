# Spring Core Basics and Design Patterns

---

## 1. What is Spring Framework? Discuss features of Spring. [Q1]

**Spring Framework** is a powerful, open-source framework used to build Java applications. It helps developers create reliable, maintainable, and flexible applications by providing a set of tools and features that make development easier.

Spring is widely used because it solves many common problems in Java development, such as managing objects, connecting to databases, and handling security. It is especially popular for building web applications and enterprise-level software.

### Key Features of Spring (in simple terms):

- **Lightweight:** Spring does not require a lot of resources. It is easy to set up and does not slow down your application.
- **Inversion of Control (IoC):** Instead of creating objects yourself, Spring creates and manages them for you. This makes your code cleaner and easier to manage.
- **Dependency Injection (DI):** Spring automatically provides the objects (dependencies) that your classes need. This reduces the amount of code you write and makes testing easier.
- **Modular:** You can use only the parts of Spring you need. For example, you can use just Spring Core for basic features, or add Spring MVC for web applications.
- **Aspect-Oriented Programming (AOP):** Lets you separate common tasks (like logging or security) from your main business logic, so your code is less cluttered.
- **Transaction Management:** Makes it easy to manage database transactions, so you can ensure data is saved or rolled back correctly.
- **Integration:** Works well with other popular frameworks and technologies, such as Hibernate, JPA, and JMS.
- **Testability:** Spring makes it easier to write unit tests for your code, because dependencies can be easily swapped out for mock objects.
- **Security:** Provides features to help secure your applications, such as authentication and authorization.

---

## 2. Discuss Spring Framework architecture with suitable example. [Q2]

Spring has a layered architecture. Each layer provides different functionalities and can be used independently.

### Main Layers:

| Layer                   | Description                                                     |
| ----------------------- | --------------------------------------------------------------- |
| Core Container          | Provides IoC and DI features (Beans, Core, Context, Expression) |
| Data Access/Integration | JDBC, ORM, JMS, Transactions                                    |
| Web                     | Web, Servlet, Web-Servlet, Web-Struts, Web-Portlet              |
| AOP                     | Aspect-Oriented Programming support                             |
| Test                    | Testing support for Spring components                           |

**Example:**

- You define beans (objects) in a configuration file or with annotations.
- Spring creates and manages these beans, injecting dependencies as needed.
- Example Bean definition (annotation):
  ```java
  @Component
  public class MyService {
      @Autowired
      private MyRepository repo;
  }
  ```

---

## 3. Discuss disadvantages of Spring Framework [Q3]

- **Complexity:** Spring has many features and modules, which can be overwhelming for beginners.
- **Configuration:** XML or annotation-based configuration can become large, repetitive, and hard to manage in big projects.
- **Performance:** Uses reflection and proxies, which may slow down application performance compared to plain Java code.
- **Learning Curve:** Requires understanding of several concepts like IoC, DI, AOP, and more, which can take time to learn.
- **Debugging:** Errors in configuration or bean wiring can be difficult to trace and fix.
- **Too Many Choices:** There are many ways to do the same thing in Spring, which can confuse developers.
- **Upgrades:** Upgrading to new Spring versions may require changes in configuration or code, leading to extra work.
- **Heavy for Small Apps:** For very simple applications, using Spring might be overkill and add unnecessary complexity.

---

## 4. Differentiate between Spring & Spring Boot [Q4]

| Feature           | Spring Framework                        | Spring Boot                                 |
| ----------------- | --------------------------------------- | ------------------------------------------- |
| Configuration     | Manual setup (XML/Java config)          | Auto-configuration, minimal setup           |
| Server Management | Requires external server (Tomcat, etc.) | Embedded servers (Tomcat, Jetty, etc.)      |
| Starter Templates | Not available                           | Provides starter templates (starters)       |
| Project Structure | Flexible, but more boilerplate          | Opinionated defaults, less boilerplate      |
| Deployment        | WAR packaging, needs deployment steps   | JAR packaging, run as standalone app        |
| Complexity        | More complex, fine-grained control      | Simplified, rapid development               |
| Learning Curve    | Steeper, more concepts to learn         | Easier for beginners                        |
| Microservices     | Needs extra setup                       | Built-in support for microservices          |
| Production Ready  | Manual setup for monitoring, metrics    | Built-in health checks, metrics, monitoring |
| Use Case          | Large, enterprise, legacy projects      | Quick prototyping, microservices, REST APIs |

- **Spring Boot** is built on top of Spring and makes it easier to create stand-alone, production-grade Spring applications with minimal configuration.

---

## Spring Dependency Injection Concepts

- **Dependency Injection (DI)** is a design pattern where an object's dependencies are provided by an external source (like Spring), not created by the object itself.
- **Types of DI in Spring:**
  - **Constructor Injection:** Dependencies are provided through the class constructor.
  - **Setter Injection:** Dependencies are set through setter methods.
  - **Field Injection:** Dependencies are injected directly into fields (not recommended for testing).
- **Benefits:**
  - Loose coupling
  - Easier testing
  - Better code organization

---

## Spring Inversion of Control (IoC)

- **Inversion of Control (IoC)** means the control of object creation and dependency management is transferred from the program to the Spring container.
- The container creates, configures, and manages the lifecycle of objects (beans).
- IoC is implemented through Dependency Injection.

---

## 12 & 13. What are the different types of scopes in Spring? Explain in detail. [Q12, Q13]

**Spring Bean Scopes:**

Spring provides several bean scopes that define the lifecycle and visibility of beans managed by the Spring container. Here are the main scopes:

| Scope       | Description                                                                                           | Usage Example           |
| ----------- | ----------------------------------------------------------------------------------------------------- | ----------------------- |
| singleton   | Only one instance per Spring container (default). All requests for the bean return the same instance. | `@Scope("singleton")`   |
| prototype   | A new instance is created every time the bean is requested from the container.                        | `@Scope("prototype")`   |
| request     | A new bean instance is created for each HTTP request. (Web applications only)                         | `@Scope("request")`     |
| session     | A new bean instance is created for each HTTP session. (Web applications only)                         | `@Scope("session")`     |
| application | A single bean instance is created for the lifecycle of a ServletContext. (Web applications only)      | `@Scope("application")` |
| websocket   | A single bean instance is created for the lifecycle of a WebSocket. (WebSocket apps only)             | `@Scope("websocket")`   |

**More details:**

- **singleton**: Most commonly used. All components share the same instance.
- **prototype**: Useful when you need a new instance for each use, e.g., stateful beans.
- **request**: Each HTTP request gets its own bean. Good for request-scoped data.
- **session**: Each user session gets its own bean. Useful for user-specific data.
- **application**: Shared across the entire application (ServletContext).
- **websocket**: Scoped to a WebSocket session.

**Example usage in code:**

```java
@Component
@Scope("prototype")
public class MyPrototypeBean {
    // This bean will have a new instance every time it is requested
}
```

**Note:** Scopes other than `singleton` and `prototype` are available only in web-aware Spring ApplicationContexts (like Spring MVC).

For custom requirements, you can also define your own custom scopes.

- **singleton:** Shared, single object for all requests.
- **prototype:** New object each time you ask for it.
- **request/session/application/websocket:** Used in web applications for different lifecycles.

---

# Spring Beans: Scopes, Autowiring, Annotations, Life Cycle, and Configuration

## 1. What is a Java Bean? Is bean life cycle controlled by Spring? [Q6]

**Question 6: What do you meant by Java bean? Is bean life cycle controlled by Spring?**

- A **Java Bean** is a simple Java class that follows certain rules:
  - It must have a public no-argument constructor.
  - It should have private fields (variables) with public getter and setter methods.
  - It should be serializable (optional, but recommended).
- In Spring, a **bean** is any object that is managed by the Spring IoC container.
- **Bean life cycle** refers to the process of creation, initialization, use, and destruction of a bean.
- **Yes, Spring controls the bean life cycle**. It creates beans, injects dependencies, manages initialization and destruction, and can call custom methods at specific points in the life cycle.

---

## 2. What is Bean in Spring? How bean life cycle can be controlled Spring? [Q7]

**Question 7: What is Bean in Spring? How bean life cycle can be controlled Spring?**

In Spring, a **bean** is simply any Java object that is managed by the Spring container.

### How Spring Controls the Bean Life Cycle

Spring takes care of the entire life cycle of a bean, from creation to destruction. Here’s how it works in simple steps:

1. **Creation:** Spring creates the bean instance.
2. **Dependency Injection:** Spring injects any required dependencies into the bean.
3. **Initialization:** Spring runs any initialization code. You can specify this using:
    - `@PostConstruct` annotation on a method.
    - Implementing the `InitializingBean` interface and overriding `afterPropertiesSet()`.
    - Defining a custom init method in the configuration.
4. **Usage:** The bean is ready to be used in your application.
5. **Destruction:** When the application is shutting down, Spring cleans up the bean. You can specify this using:
    - `@PreDestroy` annotation on a method.
    - Implementing the `DisposableBean` interface and overriding `destroy()`.
    - Defining a custom destroy method in the configuration.

**Summary:**  
Spring manages the bean’s entire life cycle, so you don’t have to worry about creating or destroying objects yourself. You can also add your own code to run during initialization or destruction if needed.

---

## 3. Bean Scopes in Spring

Spring provides several bean scopes that define how long a bean lives and how many instances are created.

| Scope       | Description                                                                                           | Usage Example           |
| ----------- | ----------------------------------------------------------------------------------------------------- | ----------------------- |
| singleton   | Only one instance per Spring container (default). All requests for the bean return the same instance. | `@Scope("singleton")`   |
| prototype   | A new instance is created every time the bean is requested from the container.                        | `@Scope("prototype")`   |
| request     | A new bean instance is created for each HTTP request. (Web applications only)                         | `@Scope("request")`     |
| session     | A new bean instance is created for each HTTP session. (Web applications only)                         | `@Scope("session")`     |
| application | A single bean instance is created for the lifecycle of a ServletContext. (Web applications only)      | `@Scope("application")` |
| websocket   | A single bean instance is created for the lifecycle of a WebSocket. (WebSocket apps only)             | `@Scope("websocket")`   |

- **singleton:** Shared, single object for all requests (default).
- **prototype:** New object each time you ask for it.
- **request/session/application/websocket:** Used in web applications for different lifecycles.

---

## 4. Autowiring in Spring

- **Autowiring** is a feature in Spring that automatically injects the required dependencies into a bean, so you don't have to do it manually.
- Types of autowiring:
  - **byName:** Injects dependency by matching the property name with a bean name.
  - **byType:** Injects dependency by matching the property type with a bean type.
  - **constructor:** Injects dependency using the constructor.
  - **@Autowired annotation:** Most common, automatically injects by type (and by name if needed).
- Example:
  ```java
  @Component
  public class Car {
      @Autowired
      private Engine engine;
  }
  ```

---

## 5. Annotations in Spring

- **Annotations** are special markers in Java code (starting with `@`) that provide metadata to the Spring framework.
- Common Spring annotations:
  - `@Component`: Marks a class as a Spring bean.
  - `@Service`: Marks a service class.
  - `@Repository`: Marks a data access class.
  - `@Controller`: Marks a web controller class.
  - `@Autowired`: Automatically injects dependencies.
  - `@Qualifier`: Specifies which bean to inject when multiple beans of the same type exist.
  - `@Scope`: Sets the bean scope.
  - `@PostConstruct` and `@PreDestroy`: Life cycle callback methods.
- Example:
  ```java
  @Component
  @Scope("prototype")
  public class MyBean {
      @Autowired
      private AnotherBean anotherBean;
      @PostConstruct
      public void init() { System.out.println("Bean initialized"); }
      @PreDestroy
      public void destroy() { System.out.println("Bean destroyed"); }
  }
  ```

---

## 6. Life Cycle Callbacks

- **Life cycle callbacks** are special methods that are called at specific points in a bean's life cycle.
- You can use annotations (`@PostConstruct`, `@PreDestroy`), interfaces (`InitializingBean`, `DisposableBean`), or XML configuration to define these methods.
- Example:
  ```java
  @Component
  public class ExampleBean {
      @PostConstruct
      public void start() { System.out.println("Bean is starting"); }
      @PreDestroy
      public void stop() { System.out.println("Bean is stopping"); }
  }
  ```

---

## 7. Bean Configuration Styles

Spring supports several ways to configure beans:

- **XML Configuration:** Define beans and dependencies in an XML file.
- **Annotation-based Configuration:** Use annotations like `@Component`, `@Autowired`, etc., in your Java classes.
- **Java-based Configuration:** Use `@Configuration` classes and `@Bean` methods to define beans in Java code.

| Style       | How it works                                     | Example                                          |
| ----------- | ------------------------------------------------ | ------------------------------------------------ |
| XML         | Beans defined in XML files                       | `<bean id="myBean" class="com.example.MyBean"/>` |
| Annotations | Use annotations in Java classes                  | `@Component`, `@Autowired`                       |
| Java Config | Use `@Configuration` and `@Bean` in Java classes | `@Bean public MyBean myBean() { ... }`           |

---

## Introduction to Design Patterns [Q14]

Design patterns are standard solutions to common software design problems. They help make code more flexible, reusable, and maintainable.

### Common Design Patterns in Java:

| Pattern   | Purpose                                       |
| --------- | --------------------------------------------- |
| Singleton | Only one instance of a class                  |
| Factory   | Create objects without specifying exact class |
| Strategy  | Select algorithm at runtime                   |
| Observer  | Notify objects about changes                  |
| Decorator | Add behavior to objects dynamically           |
| Adapter   | Make incompatible interfaces work together    |

---

## Factory Design Pattern

- **Factory Pattern** is a creational pattern that provides an interface for creating objects, but lets subclasses decide which class to instantiate.
- Useful when you have a superclass with multiple subclasses and you want to return one of the subclasses based on input.
- Example:
  ```java
  public interface Animal { void speak(); }
  public class Dog implements Animal { public void speak() { System.out.println("Woof"); } }
  public class Cat implements Animal { public void speak() { System.out.println("Meow"); } }
  public class AnimalFactory {
      public static Animal getAnimal(String type) {
          if (type.equals("dog")) return new Dog();
          else if (type.equals("cat")) return new Cat();
          else return null;
      }
  }
  // Usage: Animal a = AnimalFactory.getAnimal("dog");
  ```

---

## Strategy Design Pattern

- **Strategy Pattern** is a behavioral pattern that lets you select an algorithm's behavior at runtime.
- You define a family of algorithms, put each in a separate class, and make them interchangeable.
- Example:
  ```java
  public interface PaymentStrategy { void pay(int amount); }
  public class CreditCardPayment implements PaymentStrategy {
      public void pay(int amount) { System.out.println("Paid by credit card: " + amount); }
  }
  public class PayPalPayment implements PaymentStrategy {
      public void pay(int amount) { System.out.println("Paid by PayPal: " + amount); }
  }
  public class ShoppingCart {
      private PaymentStrategy strategy;
      public void setPaymentStrategy(PaymentStrategy s) { this.strategy = s; }
      public void checkout(int amount) { strategy.pay(amount); }
  }
  // Usage: cart.setPaymentStrategy(new PayPalPayment());
  ```

---

## 8 & 9. What is AOP? Define AOP. [Q8, Q9]

**Aspect-Oriented Programming (AOP)** is a programming paradigm that allows you to separate cross-cutting concerns (like logging, security, transactions) from your main business logic.

- **Aspect:** A module that encapsulates a cross-cutting concern.
- **Advice:** Code that is executed at a certain point (before, after, or around a method call).
- **Join Point:** A point in the program where advice can be applied (like method execution).
- **Pointcut:** A set of join points where advice should run.
- **Weaving:** The process of applying aspects to the target code.

**Example:**

- You can use AOP in Spring to log every time a method is called, without changing the method's code.
- Example with annotation:
  ```java
  @Aspect
  public class LoggingAspect {
      @Before("execution(* com.example.service.*.*(..))")
      public void logBefore(JoinPoint joinPoint) {
          System.out.println("Method called: " + joinPoint.getSignature().getName());
      }
  }
  ```
1. What is Spring framework? Discuss feature of the Spring.
2. Discuss Spring Framework architecture with suitable example.
3. Discuss disadvantages of Spring Framework
4. Differentiate between spring & spring boot.
5. What are the various attributes of Tables?
6. What do you meant by Java bean? Is bean life cycle controlled by Spring
7. What is Bean in Spring? How bean life cycle can be controlled Spring?
8. What is AOP?
9. Define AOP.
10. Illustrate Aspect Oriented Programming in spring framework.
11. Compare constructor injection and setter injection in spring with suitable example.
12. What are the different types of scopes in Spring? Explain in detail.
13. Explain the various types of scopes in spring?
14. Classify the design patterns that are used in java programming.

---
