# Spring Boot: Detailed Notes and Solved Questions

---

## Spring Boot Overview

Spring Boot is a framework built on top of the Spring Framework that simplifies the process of building stand-alone, production-grade Spring applications. It provides defaults for code and configuration, reducing boilerplate and setup time.The main goal of Spring Boot is to reduce, development, unit test, and integration test time and in Spring Boot, there is no requirement for XML
configuration allowing developers to focus more on writing code for their applications.It facilitates Rapid Application Development (RAD) capabilities.

---

## 1. Why is Spring Boot preferred over any other framework?

**Question 1: Why is Spring Boot preferred over any other framework?**

- **Spring Boot** is preferred because it:
  - Reduces configuration effort with sensible defaults (auto-configuration).
  - Allows rapid development of stand-alone applications.
  - Has embedded servers (Tomcat, Jetty) so no need for external deployment.
  - Provides production-ready features (metrics, health checks, etc.).
  - Integrates easily with Spring ecosystem and third-party libraries.

- **Summary Table:**

  | Feature              | Spring Boot Advantage                        |
  |----------------------|----------------------------------------------|
  | Auto-configuration   | Reduces manual setup                         |
  | Embedded server      | No need for external deployment (WAR)        |
  | Starter dependencies | Simplifies dependency management             |
  | Actuator             | Built-in monitoring and management           |
  | Rapid prototyping    | Enables quick development and iteration      |

---

## 2. What makes Spring Boot superior to JAX-RS?

**Question 2: What makes Spring Boot superior to JAX-RS?**

- **Spring Boot** offers:
  - Auto-configuration and starter dependencies for quick setup.
  - Embedded server support (no need for external servlet container).
  - Rich ecosystem (Spring Data, Security, etc.).
  - Actuator for monitoring and management.
  - More flexible configuration (properties, YAML, profiles).

- **JAX-RS** is mainly for REST APIs and lacks many of these features out-of-the-box.

- **Summary Table:**
  | Feature            | Spring Boot | JAX-RS |
  |--------------------|-------------|--------|
  | Auto-configuration | Yes         | No     |
  | Embedded server    | Yes         | No     |
  | Monitoring tools   | Yes         | No     |
  | Ecosystem          | Large       | Small  |

## Spring Boot Configuration

- Spring Boot uses **application.properties** or **application.yml** for configuration.
- Supports environment-specific profiles (e.g., `application-dev.properties`).
- Configuration can be done via:

  - Properties files
  - YAML files
  - Command-line arguments
  - Environment variables

- Example (application.properties):
  ```properties
  server.port=8081
  spring.datasource.url=jdbc:mysql://localhost:3306/mydb
  spring.jpa.hibernate.ddl-auto=update
  ```

---

## Spring Boot Annotations [Q4]

**Question 4: Classify all the annotations that are exclusively used for Spring Boot applications.**

- **@SpringBootApplication**: Main entry point; combines @Configuration, @EnableAutoConfiguration, and @ComponentScan.
- **@EnableAutoConfiguration**: Enables Spring Boot’s auto-configuration.
- **@SpringBootConfiguration**: Marks a configuration class.
- **@ConditionalOnProperty, @ConditionalOnClass**: Conditional configuration.
- **@RestController**: Combines @Controller and @ResponseBody for REST APIs.
- **@Value**: Injects values from properties.
- **@ConfigurationProperties**: Binds external configuration to Java beans.
- **@Profile**: Specifies the profile for which a bean is active.
- **@Component, @Service, @Repository**: Stereotype annotations for beans.

---

## 5. Can we call a Java class with annotations as a POJO class or not?

**Question 5: Can we call a Java class with annotations as a POJO class or not?**

- **POJO** stands for Plain Old Java Object.
- A class is considered a POJO if it does not extend framework-specific classes or implement special interfaces.
- Adding annotations (such as `@Entity`, `@Component`, etc.) does not affect its POJO status, since annotations do not alter inheritance or interface implementation.
- **Conclusion:** Yes, a Java class with annotations can still be considered a POJO.
- **Example:**
  ```java
  @Entity
  public class User {
          private Long id;
          private String name;
          // getters and setters
  }
  ```
  In this example, `User` is still a POJO even though it uses the `@Entity` annotation.

---

## Spring Boot Actuator

- **Spring Boot Actuator** provides production-ready features to help monitor and manage applications.
- Exposes endpoints for health, metrics, info, environment, etc.
- Example endpoints:
  - `/actuator/health` – Application health status
  - `/actuator/metrics` – Metrics like memory, CPU, etc.
- To enable Actuator, add dependency:
  ```xml
  <dependency>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-starter-actuator</artifactId>
  </dependency>
  ```
- Configure endpoints in `application.properties`:
  ```properties
  management.endpoints.web.exposure.include=*
  ```

Spring Boot Actuator is a sub-project of the Spring Boot framework that provides production-ready features for monitoring and managing Spring Boot applications. It exposes operational information about
the running application through a set of built-in endpoints. Spring Boot provides an actuator dependency that can be used to monitor and manage your Spring Boot application.
Features of Spring Boot Actuator:

• Monitoring: Provides insights into the application's health, performance, and resource usage.
• Metrics: Collects and exposes various metrics, such as JVM memory usage, HTTP request counts, and
database connection pool statistics.
• Health Checks: Allows for checking the health status of the application and its dependencies.
• Configuration: Provides access to the application's configuration properties.
• Auditing: Tracks application events and changes.
• Management: Enables remote management of the application. 

---

## Spring Boot Build Systems

- Supports **Maven** and **Gradle** as build tools.
- **Maven**: Uses `pom.xml` for dependencies and build configuration.
- **Gradle**: Uses `build.gradle` for configuration.
- Example (Maven):
  ```xml
  <dependency>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-starter-web</artifactId>
  </dependency>
  ```
- Example (Gradle):
  ```groovy
  implementation 'org.springframework.boot:spring-boot-starter-web'
  ```

---

## Spring Boot Code Structure

- Typical structure:
  ```
  src/
    main/
      java/
        com/example/demo/
          DemoApplication.java
          controller/
          service/
          repository/
      resources/
        application.properties
  ```
- **DemoApplication.java** contains the main method with @SpringBootApplication.
- Controllers, services, and repositories are organized in separate packages.

---

## Spring Boot Runners

- **CommandLineRunner** and **ApplicationRunner** are interfaces for running code at application startup.
- Example:
  ```java
  @Component
  public class MyRunner implements CommandLineRunner {
      @Override
      public void run(String... args) throws Exception {
          System.out.println("App started!");
      }
  }
  ```
- Use for initialization, data loading, etc.

---

## 6. Explain Dependency Injection in Spring Boot.

**Question 6: Explain Dependency Injection in Spring Boot.**

- **Dependency Injection (DI)** is a design pattern where objects receive their dependencies from an external source rather than creating them themselves.
- In Spring Boot, DI is achieved using annotations:
  - **@Autowired**: Injects dependencies automatically.
  - **@Component, @Service, @Repository**: Mark classes as beans for DI.
- Example:
  ```java
  @Service
  public class UserService {
      @Autowired
      private UserRepository userRepository;
  }
  ```
- DI promotes loose coupling, easier testing, and better code organization.

---

## 7 & 8. How to save image in database using Spring Boot?

**Question 7 & 8: How to save image in database using Spring Boot?**

- To save an image in a database:
  1. Create an entity with a `byte[]` field for the image.
  2. Use a REST controller to handle file upload.
  3. Store the image bytes in the database.
- **Example Entity:**
  ```java
  @Entity
  public class ImageEntity {
      @Id
      @GeneratedValue(strategy = GenerationType.IDENTITY)
      private Long id;
      private String name;
      @Lob
      private byte[] imageData;
      // getters and setters
  }
  ```
- **Example Controller:**
  ```java
  @RestController
  public class ImageController {
      @Autowired
      private ImageRepository imageRepository;
      @PostMapping("/upload")
      public String uploadImage(@RequestParam("file") MultipartFile file) throws IOException {
          ImageEntity img = new ImageEntity();
          img.setName(file.getOriginalFilename());
          img.setImageData(file.getBytes());
          imageRepository.save(img);
          return "Image saved!";
      }
  }
  ```
- **Repository:**
  ```java
  public interface ImageRepository extends JpaRepository<ImageEntity, Long> {}
  ```
- **Note:** Storing images in the database is possible, but for large files, storing them in the filesystem and saving the path in the database is often preferred.

---

## Logger in Spring Boot

- **Logger** is used to record information, warnings, errors, and debug messages during application execution.
- Spring Boot uses popular logging frameworks like **SLF4J** with **Logback** by default.
- Logging helps in monitoring, debugging, and auditing application behavior.
- **How to use Logger:**

  ```java
  import org.slf4j.Logger;
  import org.slf4j.LoggerFactory;

  @RestController
  public class MyController {
      private static final Logger logger = LoggerFactory.getLogger(MyController.class);
      @GetMapping("/hello")
      public String hello() {
          logger.info("Hello endpoint called");
          return "Hello World!";
      }
  }
  ```

- Log levels: TRACE, DEBUG, INFO, WARN, ERROR.
- Configure logging in `application.properties`:
  ```properties
  logging.level.root=INFO
  logging.level.com.example=DEBUG
  ```

---

## Building RESTful Web Services in Spring Boot

- **RESTful Web Services** allow applications to communicate over HTTP using standard methods (GET, POST, PUT, DELETE).
- Spring Boot makes it easy to build REST APIs using annotations and auto-configuration.

### Rest Controller

- Annotate a class with `@RestController` to define REST endpoints.
- Combines `@Controller` and `@ResponseBody`.
- Example:
  ```java
  @RestController
  public class UserController {
      @GetMapping("/users")
      public List<User> getAllUsers() {
          // ...
      }
  }
  ```

### Request Mapping

- `@RequestMapping` is used to map HTTP requests to handler methods.
- Can specify path and HTTP method.
- Example:
  ```java
  @RequestMapping(value = "/users", method = RequestMethod.GET)
  public List<User> getUsers() { ... }
  ```
- Shortcuts: `@GetMapping`, `@PostMapping`, `@PutMapping`, `@DeleteMapping`.

### Request Body

- `@RequestBody` binds the HTTP request body to a Java object.
- Used for POST/PUT requests to receive data.
- Example:
  ```java
  @PostMapping("/users")
  public User createUser(@RequestBody User user) { ... }
  ```

### Path Variable

- `@PathVariable` extracts values from the URI path.
- Example:
  ```java
  @GetMapping("/users/{id}")
  public User getUser(@PathVariable Long id) { ... }
  ```

### Request Parameter

- `@RequestParam` extracts query parameters from the URL.
- Example:
  ```java
  @GetMapping("/search")
  public List<User> searchUsers(@RequestParam String name) { ... }
  ```

---

## 9. Explain GET, PUT, POST, and DELETE method with respect to REST API.

**Question 9: Explain GET, PUT, POST, and DELETE method with respect to REST API.**

| Method | Purpose                      | Usage Example    |
| ------ | ---------------------------- | ---------------- |
| GET    | Retrieve data                | Get user details |
| POST   | Create new resource          | Add a new user   |
| PUT    | Update/replace existing data | Update user info |
| DELETE | Remove resource              | Delete a user    |

- **GET:** Used to fetch data from the server. Should not modify data.
- **POST:** Used to create a new resource. Sends data in the request body.
- **PUT:** Used to update or replace an existing resource. Sends updated data in the request body.
- **DELETE:** Used to remove a resource from the server.

---

## 10. Write short note on:

### i. GET

- Retrieves data from the server.
- Safe and idempotent (multiple calls have the same effect).
- Example: `GET /users/1` returns user with ID 1.

### ii. POST

- Creates a new resource on the server.
- Not idempotent (multiple calls create multiple resources).
- Example: `POST /users` with user data creates a new user.

### iii. PUT

- Updates or replaces an existing resource.
- Idempotent (multiple calls with same data have same effect).
- Example: `PUT /users/1` with updated data replaces user 1.

### iv. DELETE

- Removes a resource from the server.
- Idempotent (deleting same resource multiple times has same effect).
- Example: `DELETE /users/1` deletes user 1.

---

## 11. Create a RESTful Spring Boot application for handling the DELETE and PUT request.

**Question 11: Create a RESTful Spring Boot application for handling the DELETE and PUT request.**

- **Entity:**
  ```java
  @Entity
  public class User {
      @Id
      @GeneratedValue(strategy = GenerationType.IDENTITY)
      private Long id;
      private String name;
      private String email;
      // getters and setters
  }
  ```
- **Repository:**
  ```java
  public interface UserRepository extends JpaRepository<User, Long> {}
  ```
- **Controller:**

  ```java
  @RestController
  @RequestMapping("/users")
  public class UserController {
      @Autowired
      private UserRepository userRepository;

      @PutMapping("/{id}")
      public ResponseEntity<User> updateUser(@PathVariable Long id, @RequestBody User userDetails) {
          User user = userRepository.findById(id).orElseThrow();
          user.setName(userDetails.getName());
          user.setEmail(userDetails.getEmail());
          userRepository.save(user);
          return ResponseEntity.ok(user);
      }

      @DeleteMapping("/{id}")
      public ResponseEntity<Void> deleteUser(@PathVariable Long id) {
          userRepository.deleteById(id);
          return ResponseEntity.noContent().build();
      }
  }
  ```

- **Explanation:**
  - `@PutMapping` handles updating a user by ID.
  - `@DeleteMapping` handles deleting a user by ID.

---

## Build Web Applications with Spring Boot

- Spring Boot simplifies building web applications with embedded servers, auto-configuration, and starter dependencies.
- Supports RESTful APIs, MVC, static content, and more.
- Typical steps:
  1. Create a Spring Boot project (using Spring Initializr or build tool).
  2. Define entities, repositories, and controllers.
  3. Configure application properties.
  4. Run the application and access endpoints via browser or API client.
- **Example:**
  - Access `http://localhost:8080/users` to interact with the REST API.

---
