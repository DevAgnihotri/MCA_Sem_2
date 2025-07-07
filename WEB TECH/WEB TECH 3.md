# Servlets: Overview, Architecture, Life Cycle, and HTTP Requests

---

## Servlet Overview and Architecture

**Q1: What is Servlet?**

- A **Servlet** is a Java program that runs on a web server and handles requests from web browsers (clients).
- Servlets are used to create dynamic web pages (like login forms, shopping carts, etc.).
- They are part of Java EE (Enterprise Edition) and are managed by a **Servlet Container** (like Apache Tomcat).
- Servlets follow a request-response model: the browser sends a request, the servlet processes it, and sends back a response.

**Servlet Architecture Diagram:**

```
Browser <--> Web Server <--> Servlet Container <--> Servlet (Java Code)
```

- The browser sends a request (like clicking a link or submitting a form).
- The web server passes the request to the servlet container.
- The servlet container loads the servlet, which processes the request and
  sends a response back to the browser.

---

## Interface Servlet and the Servlet Life Cycle

**Q1 & Q2: What is Servlet? Explain the life cycle of Servlet. / Explain the life cycle of servlet in detail.**

- The **Servlet interface** defines methods that every servlet must implement.
- Most web servlets extend the `HttpServlet` class, which already implements the Servlet interface and provides methods for handling HTTP requests.

**Servlet Life Cycle Steps (Detailed):**

1. **Loading and Instantiation:**

   - When the web server receives the first request (or starts up), it loads the Java class and creates one object from it. This is done only once.

2. **Initialization (`init()` method):**

   - Right after creating the object, the server calls the `init()` method. This is where we set up things you need only once, like opening a database connection or reading settings.

3. **Handling Requests (`service()` method):**

   - For every browser request, the server calls the `service()` method (using a new thread each time). This method figures out if the request is a GET, POST, etc., and calls the matching method (`doGet()`, `doPost()`, etc).
   - Here, we write the code to process the request and send back a response (like HTML or JSON).

4. **Destruction (`destroy()` method):**

   - When the server is shutting down or removing your class, it calls the `destroy()` method once. Use this to clean up—close files, database connections, etc.

5. **Garbage Collection:**
   - After destruction, Java’s memory manager (the JVM) eventually deletes the object to free up memory. No more requests are handled after this.

**Summary Table: Servlet Life Cycle Methods**

| Step             | Method      | When Called                   | Purpose                        |
| ---------------- | ----------- | ----------------------------- | ------------------------------ |
| Loading          | Constructor | On first request/startup      | Create servlet instance        |
| Initialization   | `init()`    | After instantiation (once)    | Setup resources/configuration  |
| Request Handling | `service()` | For every client request      | Process requests and responses |
| Destruction      | `destroy()` | Before servlet removal (once) | Cleanup resources              |
| GC               | N/A         | After destruction             | Memory reclamation             |

**Servlet Life Cycle Diagram:**

```
Load -> init() -> service() [doGet()/doPost()/...] -> destroy() -> GC
```

**Q3: Which class has to be extended for creating a Servlet?**

- For most web applications, extend the `HttpServlet` class.

**Example:**

```java
public class MyServlet extends HttpServlet {
    // Override doGet, doPost, etc.
}
```

---

## Handling HTTP GET Requests

**Q4: Differentiate between handling HTTP GET requests and handling HTTP POST requests.**

- **GET** is used to request data from the server (like loading a web page).
- Data is sent in the URL (e.g., `?name=Sam`).
- GET is not secure for sensitive data (shows in URL) and has limited data size.
- GET requests can be bookmarked and cached.

**How to handle GET in a Servlet:**

```java
protected void doGet(HttpServletRequest request, HttpServletResponse response) throws IOException {
    String name = request.getParameter("name");
    response.getWriter().println("Hello, " + name);
}
```

---

## Handling HTTP POST Requests

**Q4: Differentiate between handling HTTP GET requests and handling HTTP POST requests.**

- **POST** is used to send data to the server (like submitting a form).
- Data is sent in the request body (not visible in URL).
- POST is more secure for sensitive data and can send larger amounts of data.
- POST requests are not cached or bookmarked.

**How to handle POST in a Servlet:**

```java
protected void doPost(HttpServletRequest request, HttpServletResponse response) throws IOException {
    String name = request.getParameter("name");
    response.getWriter().println("Posted name: " + name);
}
```

**Table: GET vs POST (Q4)**

| Feature      | GET (`doGet`)         | POST (`doPost`)         |
|--------------|-----------------------|-------------------------|
| Data Location| URL                   | Request Body            |
| Security     | Less secure           | More secure             |
| Data Size    | Limited               | Large                   |
| Use Case     | Fetch data            | Submit data/forms       |
| Bookmarked   | Yes                   | No                      |
| Cached       | Yes                   | No                      |

---

## Redirecting Requests to Other Resources

- Sometimes, a servlet needs to send the user to another page or resource. This is called **redirection**.
- Redirection tells the browser to go to a new URL.

**How to redirect in a Servlet:**

```java
response.sendRedirect("anotherPage.html");
```

**Example:**

```java
if (userNotLoggedIn) {
    response.sendRedirect("login.html");
}
```

---

# Session Tracking, Cookies, and HttpSession

---

## Cookies (Q5, Q6)

**Q5: What do you mean by cookies?**

- A **cookie** is a small piece of data stored by the browser on the user's computer.
- Cookies are sent by the server to the browser, and then sent back by the browser with every request to the same server.
- Used to remember information about the user (like login status, preferences, or shopping cart items).

**Q6: Demonstrate the role of cookies in web applications with an example.**

- Cookies help web applications remember users between requests (since HTTP is stateless).
- Example: When a user logs in, the server sends a cookie with a unique ID. The browser stores this cookie and sends it with every request, so the server knows which user is making the request.

**How Cookies Work in Web Applications (Detailed Explanation):**

1. **Server Creates and Sends a Cookie:**

   - When a user performs an action (like logging in), the server creates a cookie containing information such as a session ID or username.
   - The server sends this cookie to the user's browser in the HTTP response header.

   ```java
   // After successful login
   Cookie sessionCookie = new Cookie("sessionId", "ABC123XYZ");
   sessionCookie.setMaxAge(60 * 60); // 1 hour
   response.addCookie(sessionCookie);
   ```

2. **Browser Stores the Cookie:**

   - The browser receives the cookie and stores it locally.
   - The cookie can have properties like expiration time, domain, and path, which control when and where it is sent.

3. **Browser Sends Cookie with Each Request:**

   - For every subsequent request to the same server (and matching path/domain), the browser automatically includes the cookie in the HTTP request header.
   - This allows the server to identify the user or retrieve user-specific data.

   ```java
   Cookie[] cookies = request.getCookies();
   if (cookies != null) {
        for (Cookie c : cookies) {
             if (c.getName().equals("sessionId")) {
                   // Use sessionId to retrieve user info
             }
        }
   }
   ```

4. **Server Uses Cookie Data:**
   - The server reads the cookie value (like `sessionId`) to look up information about the user, such as login status, preferences, or items in a shopping cart.
   - This enables the server to maintain state and provide a personalized experience, even though HTTP itself is stateless.

**Example: User Login with Cookies**

Suppose a user logs in to a website. The server creates a cookie to identify the user:

```java
// After successful login
Cookie sessionCookie = new Cookie("sessionId", "ABC123XYZ");
sessionCookie.setMaxAge(60 * 60); // 1 hour
response.addCookie(sessionCookie);
```

On subsequent requests, the browser automatically sends this cookie:

```java
Cookie[] cookies = request.getCookies();
if (cookies != null) {
     for (Cookie c : cookies) {
          if (c.getName().equals("sessionId")) {
                // Use sessionId to retrieve user info
          }
     }
}
```

**Summary:**  
Cookies allow the server to recognize returning users, manage sessions, and personalize the user experience (such as keeping users logged in or remembering preferences).

**Key Points about Cookies:**

- Cookies are small text files stored in the browser.
- They can store user IDs, session tokens, or preferences.
- Cookies have properties like name, value, expiration, domain, and path.
- They are automatically sent with every request to the server, enabling session management and personalization.
- Cookies can be set to expire after a certain time or when the browser is closed (session cookies).

**Diagram: How Cookies Work**

```
1. User logs in  --->  2. Server sends Set-Cookie header
        |                             |
        v                             v
    Browser <------------------- Server
        |                             |
        |--- Cookie sent with every request --->|
```

**Example: Setting and Reading Cookies in a Servlet**

```java
// Setting a cookie
Cookie userCookie = new Cookie("username", "Sam");
response.addCookie(userCookie);

// Reading cookies
Cookie[] cookies = request.getCookies();
if (cookies != null) {
    for (Cookie c : cookies) {
        if (c.getName().equals("username")) {
            out.println("Welcome back, " + c.getValue());
        }
    }
}
```

---

## Session Tracking (Q7, Q8)

**Q7 & Q8: What is session tracking? How is a session created? Explain (with example).**

- **Session tracking** is a way to remember a user's data and actions as they move from page to page in a web application.
- HTTP is stateless (it does not remember users between requests), so session tracking is needed for things like shopping carts, logins, etc.

**Common Session Tracking Methods:**

- **Cookies:** Store a unique session ID in the browser.
- **URL Rewriting:** Add session ID to the URL.
- **Hidden Form Fields:** Store session data in hidden fields in forms.
- **HttpSession (most common in Java):** Server creates a session object for each user.

**How is a session created?**

- When a user visits a website, the server creates a new session object and gives it a unique ID.
- This ID is usually stored in a cookie or added to the URL.
- The server uses this ID to keep track of the user's data across multiple requests.

**Example: Using HttpSession in a Servlet**

```java
// Creating or getting a session
HttpSession session = request.getSession();
// Storing data in the session
session.setAttribute("username", "Sam");
// Getting data from the session
String user = (String) session.getAttribute("username");
```

**Diagram: Session Tracking with HttpSession**

```
Browser <--> Web Server <--> Session (on server)
   |             ^
   |             |
   |--- session ID (cookie or URL) ---|
```

**Summary Table: Session Tracking Methods**

| Method            | Where Data is Stored | Typical Use Case               |
| ----------------- | -------------------- | ------------------------------ |
| Cookies           | Browser              | User preferences, login        |
| URL Rewriting     | URL                  | When cookies are disabled      |
| Hidden Form Field | Form data            | Multi-page forms               |
| HttpSession       | Server               | Most secure, flexible sessions |

---

# Java Server Pages (JSP): Introduction, Features, and Key Concepts

---

## Introduction to JSP

- **Java Server Pages (JSP)** is a technology for building dynamic web pages using Java.
- JSP lets developers mix HTML with Java code, so web pages can show changing data (like user names, search results, etc.).
- JSP files have the extension `.jsp` and run on a web server with a Java servlet container (like Apache Tomcat).

---

## JSP Overview

- JSP is part of Java EE (Enterprise Edition).
- When a browser requests a JSP page, the server turns it into a servlet (Java class), compiles it, and runs it.
- JSP is mainly used for the view (presentation) part of web applications.

**How JSP Works (Diagram):**

```
Browser <--> Web Server <--> JSP Engine <--> JSP (converted to Servlet) <--> Java Code/Database
```

---

## A First Java Server Page Example

**Example:**

```jsp
<%@ page language="java" %>
<html>
  <head><title>My First JSP</title></head>
  <body>
    <h1>Hello, JSP!</h1>
    <p>Current time: <%= new java.util.Date() %></p>
  </body>
</html>
```

- `<%= ... %>` is used to print Java values inside HTML.

---

## Implicit Objects in JSP

- JSP provides built-in objects (called **implicit objects**) that can be used directly in the page.
- Common implicit objects:
  - `request`: Info about the HTTP request
  - `response`: Info about the HTTP response
  - `session`: User session data
  - `application`: Data shared by all users
  - `out`: Used to send output to the browser
  - `config`: Servlet config info
  - `pageContext`: Info about the page
  - `page`: The JSP page itself
  - `exception`: Errors (used in error pages)

---

## Scripting in JSP

- Scripting elements let you write Java code inside a JSP page.
- **Types of scripting elements:**
  - **Declarations (`<%! ... %>`):** Declare variables and methods.
    - Example: `<%! int count = 0; %>`
  - **Scriptlets (`<% ... %>`):** Write Java code that runs every time the page is requested.
    - Example: `<% count++; %>`
  - **Expressions (`<%= ... %>`):** Output the value of a Java expression.
    - Example: `<%= count %>`

---

## Standard Actions in JSP

- Standard actions are special tags that perform common tasks.
- Examples:
  - `<jsp:include page="header.jsp" />` — Includes another JSP file.
  - `<jsp:forward page="next.jsp" />` — Forwards the request to another page.
  - `<jsp:param>` — Passes parameters to another page.
  - `<jsp:useBean>` — Creates or finds a JavaBean.
  - `<jsp:setProperty>` and `<jsp:getProperty>` — Set or get bean properties.

---

## Directives in JSP

- Directives give instructions to the JSP engine.
- Main types:
  - **Page Directive:** Sets page-level instructions (like language, error page).
    - Example: `<%@ page language="java" %>`
  - **Include Directive:** Includes a file during translation.
    - Example: `<%@ include file="header.jsp" %>`
  - **Taglib Directive:** Declares a custom tag library.
    - Example: `<%@ taglib uri="/mytags" prefix="mt" %>`

---

## Custom Tag Libraries

- Custom tags are user-defined tags that make JSP pages easier to read and maintain.
- Tag libraries (taglibs) are collections of custom tags.
- Example: JSTL (JavaServer Pages Standard Tag Library) provides tags for common tasks like loops, conditions, and formatting.
- Custom tags are defined in Java classes and registered with a tag library descriptor (TLD) file.

---

## Advantages of JSP over Servlet (Q9, Q10, Q11)

**Q9: Describe the advantages of JSP over Servlet.**
**Q10: What are the advantages of using JSP over Servlet?**
**Q11: What is the functionality of JSP? What are the advantages of JSP over various server-side programming techniques?**

- JSP allows mixing HTML and Java, making it easier to design web pages.
- JSP is better for presentation (view) logic, while servlets are better for business logic.
- Changes to JSP pages do not require recompiling the whole application (just save and refresh).
- JSP code is easier for web designers to understand and edit.
- Built-in objects and tags make common tasks simpler.
- JSP supports tag libraries (like JSTL) for reusable code.
- JSP pages are automatically compiled into servlets by the server.
- Compared to other server-side techniques (like PHP, ASP), JSP is portable, secure, and integrates well with Java code and libraries.

**Table: JSP vs Servlet**

| Feature           | JSP                    | Servlet                     |
|-------------------|------------------------|-----------------------------|
| Syntax            | HTML + Java            | Pure Java code              |
| Best for          | Presentation (View)    | Business logic (Controller) |
| Designer-friendly | Yes                    | No                          |
| Code changes      | Just save and refresh  | Recompile and redeploy      |
| Built-in objects  | Yes                    | No                          |

---

## Forward vs sendRedirect in JSP (Q12)

**Q12: What is the difference between forward and sendRedirect tag in JSP?**

- **forward (jsp:forward):**

  - Forwards the request to another resource (JSP, servlet, or HTML) on the same server.
  - The browser does NOT know the change; the URL stays the same.
  - Faster, as it happens on the server side.
  - Example: `<jsp:forward page="next.jsp" />`

- **sendRedirect:**

  - Sends a response to the browser, telling it to make a new request to a different URL (can be on the same or another server).
  - The browser URL changes.
  - Slower, as it involves a new request/response cycle.
  - Example: `response.sendRedirect("next.jsp");`

**Table: forward vs sendRedirect**
| Feature                | forward (`<jsp:forward>`) | sendRedirect (`response.sendRedirect`)|
|------------------------|---------------------------|---------------------------------------|
| URL changes?           | No                        | Yes                                   |
| Server/Client action   | Server-side               | Client-side                           |
| Can go to other domain?| No                        | Yes                                   |
| Speed                  | Faster                    | Slower                                |


## API and CGI

### Q13: Define API and CGI.

**API (Application Programming Interface):**
- An **API** is a set of rules and tools that lets different software programs talk to each other.
- It defines how requests and responses should be made, what data to send, and what to expect back.
- APIs are used to connect different parts of a program, or to connect different programs (like a website and a database).

**Example:**  
A weather website uses an API to get weather data from a remote server.

**CGI (Common Gateway Interface):**
- **CGI** is a standard way for web servers to run external programs (like scripts) and send their output to web browsers.
- CGI scripts can be written in languages like Python, Perl, or C.
- Used to create dynamic web pages before technologies like Servlets and JSP.

**Example:**  
A CGI script processes a form submission and returns a custom HTML page.

**Table: API vs CGI**

| Feature         | API                                   | CGI                                 |
|-----------------|---------------------------------------|-------------------------------------|
| Purpose         | Connects software components          | Runs programs on web server         |
| Usage           | Data exchange, integration            | Dynamic web content generation      |
| Modern Usage    | Very common (REST, SOAP, etc.)        | Rare (older technology)             |
| Language        | Any (Java, Python, etc.)              | Usually scripting languages         |

---

## Client–Server Architecture

### Q14: Explain Client–Server architecture with a suitable diagram.

- **Client–Server architecture** is a way of organizing computers so that one (the server) provides resources or services, and others (clients) request and use them.
- The **client** is usually a web browser or app on your device.
- The **server** is a powerful computer that stores data, runs applications, and sends responses to clients.

**How it works:**
1. The client sends a request (like opening a website).
2. The server receives the request, processes it, and sends back a response (like a web page).

**Diagram:**

```
+--------+         Request         +--------+
| Client | ---------------------> | Server |
|        | <--------------------- |        |
+--------+        Response        +--------+
```

**Key Points:**
- Clients and servers can be on different computers, connected by a network (like the Internet).
- Servers can handle many clients at once.
- This model is used for web applications, email, file sharing, etc.

---

## Client-Side vs Server-Side Scripting

### Q15: Differentiate between Client-Side scripting and Server-Side scripting.

**Client-Side Scripting:**
- Code runs in the user's browser (on their device).
- Used for things like form validation, animations, and updating content without reloading the page.
- Common languages: JavaScript, HTML, CSS.

**Server-Side Scripting:**
- Code runs on the web server.
- Used for processing form data, accessing databases, and generating dynamic web pages.
- Common languages: Java, PHP, Python, Node.js.

**Table: Client-Side vs Server-Side Scripting**

| Feature           | Client-Side Scripting      | Server-Side Scripting      |
|-------------------|---------------------------|---------------------------|
| Where it runs     | User's browser            | Web server                |
| Languages         | JavaScript, HTML, CSS     | Java, PHP, Python, etc.   |
| Access to server  | No                        | Yes                       |
| Security          | Less secure (user can see)| More secure (hidden code) |
| Example           | Form validation           | Login authentication      |
| Speed             | Fast (no server needed)   | Depends on server load    |

--- 


1. What is Servlet? Explain the life cycle of Servlet.
2. Explain the life cycle of servlet in detail.
3. Which class has to be extended for creating a Servlet?
4. Differentiate between handling HTTP GET requests and handling HTTP POST requests.
5. What do you mean by cookies?
6. Demonstrate the role of cookies in web applications with an example.
7. Discuss session tracking. How is a session created? Explain.
8. What do you mean by session tracking? How can a session be created? Explain with an example.
9. Describe the advantages of JSP over Servlet.
10. What are the advantages of using JSP over Servlet?
11. What is the functionality of JSP? What are the advantages of JSP over various server-side programming techniques?
12. What is the difference between forward and sendRedirect tag in JSP?
13. Define API and CGI.
14. Explain Client–Server architecture with a suitable diagram.
15. Differentiate between Client-Side scripting and Server-Side scripting.

---
