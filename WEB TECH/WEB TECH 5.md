# Spring Boot: Detailed Notes and Solved Questions

---

## Spring Boot Overview

Spring Boot is a framework built on top of the Spring Framework that simplifies the process of building stand-alone, production-grade Spring applications. It provides defaults for code and configuration, reducing boilerplate and setup time.

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
| Feature              | Spring Boot Advantage                  |
|----------------------|----------------------------------------|
| Auto-configuration   | Reduces manual setup                   |
| Embedded server      | No need for external deployment (WAR)  |
| Starter dependencies | Simplifies dependency management       |
| Actuator             | Built-in monitoring and management     |
| Rapid prototyping    | Enables quick development and iteration|

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

---

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
