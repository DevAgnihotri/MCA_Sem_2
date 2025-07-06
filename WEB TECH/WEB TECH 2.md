# Introduction to JavaScript

JavaScript is a computer language that helps make web pages interactive. It runs inside your web browser and can also run on servers (using Node.js). JavaScript is easy to start with and is used on almost every website.

Think of a website like a house:

- **HTML** is the walls and roof (structure).
- **CSS** is the paint and furniture (style).
- **JavaScript** is the electricity and switches (makes things work and move).

## What are the features of JavaScript? (Covered Question)

- **Easy to Learn:** The basics are simple to pick up.
- **Runs in Browser:** No need to install anything extra to use it on websites.
- **Interpreted:** The browser reads and runs the code line by line.
- **Flexible Types:** You don’t have to say if something is a number or a word; JavaScript figures it out.
- **Object-Based:** You can group related data and actions together using objects.
- **Event-Driven:** JavaScript can react to things like clicks, typing, or mouse movement.
- **Works Everywhere:** It runs on all devices and operating systems with a browser.
- **First-Class Functions:** You can treat functions like any other value (store them in variables, pass them around).
- **Can Run on Servers:** With Node.js, JavaScript can also be used to build server-side programs.
- **Big Community:** Lots of help, code, and tools are available online.

**Example: Print “Hello” and use a FOR loop**

```javascript
console.log("Hello");
for (let i = 1; i <= 5; i++) {
  console.log("Number: " + i);
}
```

---

# Creating Variables in JavaScript

Variables are like boxes where you store information. You can use three main ways to make a variable:

- **var:** Old way, works in the whole function or globally.
- **let:** Newer, works only inside the nearest curly braces `{}` (block).
- **const:** Like let, but you can’t change its value after you set it.

**Examples:**

```javascript
var age = 20; // can change and re-declare
let name = "Sam"; // can change, but not re-declare in the same block
const pi = 3.14; // cannot change
```

## Explain the scope of `let` and `var` variables in JavaScript. (Covered Question)

**Scope** means where you can use a variable in your code.

- **var:**

  - If you use var inside a function, you can use it anywhere in that function.
  - If you use var outside a function, it’s available everywhere (global).
  - var is “hoisted,” so you can use it before you write it, but its value will be undefined until you set it.

- **let:**
  - let only works inside the nearest curly braces `{}` (block), like inside an if statement or a loop.
  - let is also “hoisted,” but you can’t use it before you write it (it will give an error).

**Table: var vs let**

| Feature         | var (old)       | let (new)                           |
| --------------- | --------------- | ----------------------------------- |
| Scope           | Function/Global | Block                               |
| Can re-declare? | Yes             | No                                  |
| Can update?     | Yes             | Yes                                 |
| Hoisted?        | Yes (undefined) | Yes (error if used before declared) |

**Example:**

```javascript
if (true) {
  var x = 10;
  let y = 20;
}
console.log(x); // 10 (works)
console.log(y); // Error (not defined)
```

---

# Creating Functions in JavaScript

A function is a set of instructions you can use again and again. It helps you organize your code and avoid repeating yourself.

**How to make a function:**

```javascript
function greet(name) {
  return "Hello, " + name + "!";
}
```

**How to use (call) a function:**

```javascript
greet("Sam"); // returns "Hello, Sam!"
```

**Other ways to write functions:**

- **Function Expression:**

  ```javascript
  const sayHi = function (name) {
    return "Hi, " + name;
  };
  ```

- **Arrow Function (shorter way):**

  ```javascript
  // Arrow Function (shorter way)
  const add = (a, b) => a + b;

  // Example usage:
  let answer = add(2, 3); // answer is 5 ```

---

# Returning Data from Functions

A function can give back (return) a value using the `return` keyword. If you don’t use return, the function gives back `undefined`.

**Example:**

```javascript
function add(a, b) {
  return a + b;
}
let sum = add(5, 3); // sum is 8
```

You can also return objects, arrays, or even other functions.

---

# UI Events in JavaScript

UI (User Interface) events are things that happen on a web page, like clicking a button, typing in a box, or moving the mouse. JavaScript can “listen” for these events and do something when they happen.

**Common UI Events:**

- `onclick`: When you click something
- `onchange`: When a value changes (like in a text box)
- `onmouseover`: When your mouse goes over something
- `onkeydown`: When you press a key

**How to use an event:**

```html
<button onclick="sayHello()">Click Me</button>
<script>
  function sayHello() {
    alert("Hello!");
  }
</script>
```

**Better way (using addEventListener):**

```html
<button id="myBtn">Click Me</button>
<script>
  document.getElementById("myBtn").addEventListener("click", function () {
    alert("Button clicked!");
  });
</script>
```

**What is the Event Object?**
When an event happens, JavaScript gives you an object with details about the event (like what was clicked, which key was pressed, etc.).

**Example:**

```html
<input type="text" id="myInput" />
<script>
  document
    .getElementById("myInput")
    .addEventListener("change", function (event) {
      alert("You typed: " + event.target.value);
    });
</script>
```

**Diagram: Event Bubbling**
If you click a button inside a box, the event happens on the button first, then the box, then the page. This is called “bubbling.”

```
  Page
    ^
   Box
    ^
 Button (clicked here)
```

You can stop this bubbling with `event.stopPropagation()`.

---

# JavaScript: Conditions, Loops, Objects, and DOM (with Key Questions Answered)

---

## Working with Conditions in JavaScript

Conditions let your code make decisions based on whether something is true or false.
The most common way to do this is with `if`, `else if`, and `else` statements.

- **`if` statement:** This runs a block of code only if a specific condition is true.
  Think of it as: "If this is true, then do this."

- **`else if` statement:** If the first `if` condition is false, JavaScript checks the `else if` condition.
  You can have multiple `else if` blocks to check for several different conditions.
  Think of it as: "Otherwise, if this other thing is true, then do this instead."

- **`else` statement:** If all the `if` and `else if` conditions are false, the code inside the `else` block will run.
  This is like a fallback: "If none of the above were true, then do this."

**Syntax:**

```javascript
if (condition) {
  // code runs if condition is true
}
else if (anotherCondition) {
  // code runs if anotherCondition is true
}
else {
  // code runs if none above are true
}
```

**Example:**

```javascript
let age = 18;
if (age >= 18) {
  console.log("Adult");
}
else {
  console.log("Not an adult");
}
```

### Switch Case (Q14: What do you mean by Switch Case? Explain the various control statements in JavaScript.)

The `switch` statement is used to perform different actions based on different conditions. It checks the value of an expression against multiple possible cases and runs the code for the first matching case.

**Syntax:**

```javascript
switch (expression) {
  case value1:
    // code to run if expression === value1
    break;
  case value2:
    // code to run if expression === value2
    break;
  default:
  // code to run if no cases match
}
```

**Example:**

```javascript
let day = 2;
switch (day) {
  case 1:
    console.log("Monday");
    break;
  case 2:
    console.log("Tuesday");
    break;
  default:
    console.log("Other day");
}
```

**Other Control Statements in JavaScript:**

- `break`: Exits a loop or a switch statement immediately.
- `continue`: Skips the rest of the current loop iteration and moves to the next one.
- `return`: Exits a function and optionally returns a value.

**Example of break and continue:**

```javascript
for (let i = 1; i <= 5; i++) {
  if (i === 3) continue; // skip 3
  if (i === 5) break; // stop loop at 5
  console.log(i);
}
// Output: 1, 2, 4
```

---

## Looping in JavaScript

Looping means repeating a set of instructions multiple times. JavaScript provides several ways to loop through code, which helps you handle tasks like processing lists, repeating actions, or checking conditions until something changes.

### Types of Loops

- **for loop:** Runs code a specific number of times.
- **while loop:** Runs code as long as a condition is true.
- **do...while loop:** Like while, but runs the code at least once before checking the condition.
- **for...of loop:** Used to loop through the values of an array or other iterable objects.
- **for...in loop:** Used to loop through the keys (properties) of an object.

### Definitions and Examples

- **for loop:**  
   Used when you know how many times you want to repeat something.

  ```javascript
  for (let i = 0; i < 5; i++) {
    console.log(i); // prints 0 to 4
  }
  ```

- **while loop:**  
   Used when you want to repeat something until a condition is false.

  ```javascript
  let i = 0;
  while (i < 5) {
    console.log(i);
    i++;
  }
  ```

- **do...while loop:**  
   Similar to while, but always runs at least once.

  ```javascript
  let i = 0;
  do {
    console.log(i);
    i++;
  } while (i < 5);
  ```

- **for...of loop:**  
   Used for arrays and other iterable objects.

  ```javascript
  let arr = [1, 2, 3];
  for (let num of arr) {
    console.log(num);
  }
  ```

- **for...in loop:**  
   Used for objects to loop through property names.
  ```javascript
  let obj = { a: 1, b: 2 };
  for (let key in obj) {
    console.log(key, obj[key]);
  }
  ```

### Key Points

- Loops help avoid repeating code.
- Use `break` to exit a loop early.
- Use `continue` to skip to the next loop iteration.

### Table: JavaScript Loops Overview

| Loop Type  | Use Case                         | Syntax Example                   | Runs At Least Once? |
| ---------- | -------------------------------- | -------------------------------- | ------------------- |
| for        | Known number of repetitions      | `for (let i = 0; i < n; i++) {}` | No                  |
| while      | Unknown repetitions, condition   | `while (condition) {}`           | No                  |
| do...while | Like while, but run once minimum | `do { } while (condition);`      | Yes                 |
| for...of   | Loop through array values        | `for (let item of array) {}`     | No                  |
| for...in   | Loop through object properties   | `for (let key in object) {}`     | No                  |

**Example: Print reverse digits of a number (Q13)**

You can use a loop to reverse the digits of a number:

```javascript
function reverseNumber(num) {
  let reversed = 0;
  while (num > 0) {
    let digit = num % 10;
    reversed = reversed * 10 + digit;
    num = Math.floor(num / 10);
  }
  return reversed;
}
console.log(reverseNumber(12345)); // 54321
```

```javascript
function reverseNumber(num) {
  return Number(num.toString().split("").reverse().join(""));
}
console.log(reverseNumber(12345)); // 54321
```

---

## Block Scope Variables

Block scope means a variable only exists inside the nearest `{}` (block). Use `let` and `const` for block scope.

**Example:**

```javascript
if (true) {
  let x = 10;
  const y = 20;
  // x and y only exist here
}
// x and y are not available here
```

---

## Working with Objects in JavaScript (Q3, Q12)

Objects are special variables that can hold many values as properties and functions as methods.

**Definition:**

- **Object:** A collection of key-value pairs. Each key (property name) has a value, which can be data or a function.

### Creating an Object using Object Literals (Q3, Q12)

You can create an object easily using curly braces `{}`. This is called an object literal.

```javascript
let person = {
  name: "Alice",
  age: 25,
  greet: function () {
    console.log("Hello, " + this.name);
  },
};
person.greet(); // Hello, Alice
```

- `name` and `age` are properties (data).
- `greet` is a method (function inside the object).
- `this` refers to the current object.

### Q3: Write a Script to Generate Random Numbers

You can use the built-in `Math.random()` function to generate random numbers.

```javascript
function getRandomInt(min, max) {
  return Math.floor(Math.random() * (max - min + 1)) + min;
}
console.log(getRandomInt(1, 100)); // random number between 1 and 100
```

- `Math.random()` gives a random number between 0 and 1.
- Multiply and adjust to get a number in your desired range.

### Q12: ‘JavaScript is referred to as object-based programming language’

**Definition:**  
JavaScript is called an object-based programming language because it uses objects to store and manage data. Almost everything in JavaScript can be treated as an object, except for a few basic data types (like numbers and strings).

#### What is an Object?

- An object is a collection of properties(determined by state and behaviour).
- Each property has a name (key) and a value.
- Properties can be data (like numbers or text) or functions (called methods).

#### Why is JavaScript Object-Based?

- JavaScript uses objects to group related data and actions together.
- Arrays, functions, and dates are all special types of objects.
- You can create your own objects to organize your code.

#### Key Points about Objects in JavaScript:

- **Easy to Organize:** Objects help keep related information and actions together.
- **Flexible:** You can add, change, or remove properties and methods from objects at any time.
- **Reusable:** Objects make it easy to reuse code by creating templates (using constructors or classes).
- **Built-in Objects:** JavaScript provides many built-in objects like `Array`, `Date`, `Math`, and `String`.

#### Example: Creating and Using an Object

```javascript
let car = {
  brand: "Toyota",
  model: "Corolla",
  start: function () {
    console.log("Car started");
  },
};

console.log(car.brand); // Toyota
car.start(); // Car started
```

#### Difference from Object-Oriented Programming (OOP)

- JavaScript is object-based, not fully object-oriented.
- It supports objects and methods, but does not require everything to be inside a class.
- JavaScript uses prototypes instead of strict classes (though ES6 introduced class syntax).

---

## Manipulating DOM Elements with JavaScript (Q7, Q11, Q15)

### What is the DOM? (Definition)

- **DOM** stands for **Document Object Model**.
- It is a tree-like structure that represents all the elements of a web page (like headings, paragraphs, buttons, etc.) as objects.
- JavaScript can use the DOM to read, change, add, or remove elements and content on a web page.

### Key Points about the DOM

- The DOM lets you interact with and update the web page without reloading it.
- Every HTML tag becomes a node (object) in the DOM tree.
- You can use JavaScript to select, create, modify, or delete these nodes.

### How to Create and Add Elements to the DOM

You can use JavaScript to create new elements (like a text box or button) and add them to the page.

#### Example: Creating a Text Box and Button

```javascript
// Create a text box (input element)
let input = document.createElement("input");
input.type = "text"; // set type to text
document.body.appendChild(input); // add to the page

// Create a button
let button = document.createElement("button");
button.innerHTML = "Submit"; // set button text
document.body.appendChild(button); // add to the page
```

- `document.createElement("tagName")`: Makes a new HTML element.
- `element.type`: Sets the type (for input elements).
- `element.innerHTML`: Sets the content inside the element (for buttons, etc.).
- `document.body.appendChild(element)`: Adds the new element to the web page.

#### Example: Adding an Event to the Button

You can make the button do something when clicked:

```javascript
button.addEventListener("click", function () {
  alert("Button clicked! Value: " + input.value);
});
```

### Table: Common DOM Methods

| Method                            | What it Does                                |
| --------------------------------- | ------------------------------------------- |
| `getElementById("id")`            | Selects an element by its ID                |
| `getElementsByClassName("class")` | Selects elements by class name              |
| `getElementsByTagName("tag")`     | Selects elements by tag name                |
| `querySelector("selector")`       | Selects the first element matching selector |
| `createElement("tag")`            | Creates a new HTML element                  |
| `appendChild(element)`            | Adds an element as a child                  |
| `removeChild(element)`            | Removes a child element                     |
| `setAttribute("name", "value")`   | Sets an attribute on an element             |

---

### Q15: Difference Between DOM and COM

| Feature     | DOM (Document Object Model)            | COM (Component Object Model)           |
| ----------- | -------------------------------------- | -------------------------------------- |
| What is it? | Structure for web pages (HTML/XML)     | Microsoft tech for software components |
| Used for    | Web development (browsers)             | Windows applications (not web pages)   |
| Language    | JavaScript, HTML, XML                  | C++, VB, and other Windows languages   |
| Purpose     | Manipulate web page content and layout | Enable software components to interact |

**Summary:**

- **DOM** is for web pages, lets you change the page with JavaScript.
- **COM** is for building reusable software parts in Windows, not related to web pages.

---

**In simple terms:**

- The DOM lets you use JavaScript to change what you see on a web page.
- You can create, update, or remove elements like text boxes and buttons.
- DOM is for web; COM is for Windows software components.

---

## Form Objects and Data Validation (Q6, Q8)

### What are Form Objects?

Form objects in JavaScript let you interact with forms and their elements on a web page. They help you get user input, check values, and control form behavior.

- **`document.forms`**: A collection of all forms on the page. You can access a form by its name or index, e.g., `document.forms["myForm"]`.
- **`form.elements`**: All input elements (like text boxes, checkboxes, etc.) inside a specific form.
- **`form.submit()`**: Submits the form programmatically (like clicking the submit button).
- **`form.reset()`**: Resets all form fields to their default values.

### Data Validation in JavaScript

**Data validation** means checking if the user’s input is correct before sending it to the server. This helps prevent errors and improves user experience.

#### Example: Simple Form Validation

This example checks if the "Name" field is empty before allowing the form to submit.

```html
<form name="myForm" onsubmit="return validateForm()">
  Name: <input type="text" name="fname" />
  <input type="submit" value="Submit" />
</form>

<script>
  function validateForm() {
    let x = document.forms["myForm"]["fname"].value;
    if (x == "") {
      alert("Name must be filled out");
      return false; // stops form submission
    }
  }
</script>
```

**How it works:**

- When the user submits the form, `validateForm()` runs.
- If the name field is empty, an alert shows and the form does not submit.
- If the field is filled, the form submits as normal.

**Key Points:**

- Always validate important fields (like name, email, password).
- You can add more checks (like email format, password length, etc.).
- Client-side validation is fast, but always validate on the server too for security.

**Q8: Difference between JavaScript and JScript? How to do client-side validation?**

### Table: JavaScript vs JScript (10 Key Differences)

| Point | JavaScript (JS)                     | JScript                                 |
| ----- | ----------------------------------- | --------------------------------------- |
| 1     | Standard scripting language for web | Microsoft’s version of JavaScript       |
| 2     | Created by Netscape                 | Created by Microsoft                    |
| 3     | Runs in all browsers                | Mainly runs in Internet Explorer        |
| 4     | Follows ECMAScript standard         | Based on ECMAScript, with some changes  |
| 5     | Supported on Windows, Mac, Linux    | Mostly supported on Windows             |
| 6     | Used for web development everywhere | Used for web pages on Internet Explorer |
| 7     | Regular updates and improvements    | Updates stopped, no longer maintained   |
| 8     | Works with modern web technologies  | May not support new web features        |
| 9     | Syntax is widely accepted           | Some syntax differences from JS         |
| 10    | Community support is very large     | Limited community and resources         |

### How to do Client-Side Validation?

Client-side validation means checking the user’s input in the browser before sending it to the server. This helps catch mistakes early and gives instant feedback to users.

#### Definition
- **Client-side validation** is the process of using JavaScript to check if the data entered in a form is correct and complete before the form is submitted to the server.

#### Why is it important?
- It prevents users from submitting incomplete or incorrect forms.
- It saves time and server resources by catching errors early.
- It improves user experience by showing messages right away.

#### How does it work?
- JavaScript checks each form field when the user tries to submit the form.
- If a field is empty or has the wrong format (like an invalid email), JavaScript can show a message and stop the form from submitting.
- Only when all checks pass, the form is sent to the server.

#### Common Checks in Client-Side Validation
- Required fields are not empty (like name or email).
- Email addresses are in the correct format.
- Passwords are strong enough (length, special characters, etc.).
- Numbers are within a certain range.
- Two fields match (like password and confirm password).

#### Example: Simple Client-Side Validation

```html
<form onsubmit="return validateForm()">
    Email: <input type="text" id="email" /><br />
    Password: <input type="password" id="password" /><br />
    <input type="submit" value="Submit" />
</form>

<script>
function validateForm() {
    let email = document.getElementById("email").value;
    let password = document.getElementById("password").value;
    // Check if email is empty
    if (email === "") {
        alert("Email is required.");
        return false;
    }
    // Check if email format is valid (simple check)
    if (!email.includes("@")) {
        alert("Please enter a valid email address.");
        return false;
    }
    // Check if password is at least 6 characters
    if (password.length < 6) {
        alert("Password must be at least 6 characters long.");
        return false;
    }
    // All checks passed
    return true;
}
</script>
```

#### Key Points
- Use JavaScript to check form fields before submitting.
- Show clear messages to help users fix mistakes.
- Always do server-side validation too, because users can turn off JavaScript.

**In summary:** Client-side validation makes forms safer and easier to use by checking data in the browser before sending it to the server. Use JavaScript to check for empty fields, correct formats, and other rules, and show helpful messages if something is wrong.


---

## Client-Side vs Server-Side Scripting, Differentiate between Client-Side and Server-Side Scripting. (Q5, Q10, Q17)

### Definitions

- **Client-Side Scripting:**  
    Code that runs in the user's web browser, after the web page is loaded. It is mainly used for user interface interactions, form validation, animations, and dynamic content updates without reloading the page. Common client-side scripting languages include JavaScript, HTML, and CSS.

- **Server-Side Scripting:**  
    Code that runs on the web server before the page is sent to the user's browser. It is used for processing data, accessing databases, authentication, and generating dynamic web pages. Common server-side scripting languages include PHP, Python, Ruby, Node.js, and ASP.NET.

### 10 Key Differences Between Client-Side and Server-Side Scripting

| Point | Client-Side Scripting                          | Server-Side Scripting                           |
|-------|-----------------------------------------------|-------------------------------------------------|
| 1     | Runs in the user's browser                    | Runs on the web server                          |
| 2     | Used for UI, validation, interactivity        | Used for database, authentication, data processing |
| 3     | Source code is visible to users               | Source code is hidden from users                |
| 4     | Executes after the page loads                 | Executes before the page is sent to browser     |
| 5     | Reduces server load by handling tasks locally | Handles complex, secure, or sensitive tasks     |
| 6     | Cannot access server resources directly       | Can access server files, databases, and APIs    |
| 7     | Faster response for user actions              | Slower, as requests must travel to the server   |
| 8     | Security is limited (can be bypassed)         | More secure for sensitive operations            |
| 9     | Examples: JavaScript, HTML, CSS               | Examples: PHP, Python, Node.js, ASP.NET         |
| 10    | Used for dynamic effects and validation       | Used for content generation and business logic  |

**Summary:**  
Client-side scripting makes web pages interactive and responsive, while server-side scripting handles data, security, and dynamic content generation. Both are essential for modern web applications, working together to deliver a complete user experience.

**Q5 & Q10: Compare CGI and JavaScript**

CGI and JavaScript are both used in web development, but they work in very different ways and serve different purposes.

### What is CGI?

- **CGI** stands for **Common Gateway Interface**.
- It is a standard way for web servers to run external programs or scripts (like Python, Perl, or C) when a user requests a web page.
- CGI scripts run **on the server**. When you fill out a form and click submit, the server can use CGI to process your data and send back a result.
- CGI is used for things like handling form submissions, generating dynamic web pages, or accessing databases.

**Example:**  
When you submit a contact form, the server might use a CGI script to save your message and send you a thank-you page.

### What is JavaScript?

- **JavaScript** is a programming language that runs **in your web browser** (client-side). It can also run on servers using Node.js, but it is mostly used for making web pages interactive.
- JavaScript can change what you see on a web page without reloading it. It can react to clicks, show messages, validate forms, and update content instantly.
- JavaScript is used for things like animations, form validation, pop-up messages, and dynamic content.

**Example:**  
When you type in a form and see a message like "Password too short" before you even submit, that's JavaScript working in your browser.

### Key Differences Table

| Feature                | CGI (Common Gateway Interface)         | JavaScript                              |
|------------------------|----------------------------------------|-----------------------------------------|
| Where it runs          | On the server                          | In the browser (client-side)            |
| Language               | Any (Python, Perl, C, etc.)            | JavaScript                              |
| Main use               | Process data, generate web pages       | Make pages interactive, validate forms  |
| Speed                  | Slower (needs server round-trip)       | Fast (runs instantly in browser)        |
| Access to server files | Yes                                    | No (unless using server-side JS)        |
| Example                | Saving form data to a database         | Showing/hiding content on a page        |
| Needs page reload      | Usually yes                            | No (can update page instantly)          |
| Security               | More secure for sensitive data         | Less secure, code is visible to users   |

### In Simple Terms

- **CGI** is like a worker in the kitchen (server) who prepares your food (data) and brings it to you when you order.
- **JavaScript** is like a waiter at your table (browser) who helps you interact with the menu, checks your order, and gives you instant feedback.

**Summary:**  
CGI is used for server-side tasks like processing and storing data, while JavaScript is used for client-side tasks like making web pages interactive and checking user input before sending it to the server. Both are important, but they work in different places and do different jobs.

**Q17: Define API and CGI.**

- **API (Application Programming Interface):**  
    An API is a set of rules and tools that allows different software programs to communicate with each other. It defines how requests and responses should be made, making it easier for developers to use features or data from another program, service, or platform.

- **CGI (Common Gateway Interface):**  
    CGI is a standard way for web servers to run external programs (like scripts written in Python, Perl, or C) to generate dynamic web content. When a user submits a form or requests a web page, the server can use CGI to process the request and send back a response.


---
## Alert and Confirm Box (Q16)

**Q16: Code for Alert and Confirm Box**

### What is an Alert Box?

- An **alert box** is a simple pop-up message that appears in the browser.
- It is used to show information or warnings to the user.
- The user must click "OK" to close the alert box and continue.

**Example:**

```javascript
alert("This is an alert box!");
```

- When this code runs, a message pops up with the text "This is an alert box!" and an OK button.

### What is a Confirm Box?

- A **confirm box** is a pop-up that asks the user to make a choice.
- It shows a message with two buttons: **OK** and **Cancel**.
- The box returns `true` if the user clicks OK, and `false` if the user clicks Cancel.
- You can use this to ask the user for confirmation before doing something important (like deleting data).

**Example:**

```javascript
let result = confirm("Do you want to proceed?");
console.log(result); // true if OK, false if Cancel
```

- If the user clicks OK, `result` will be `true`.
- If the user clicks Cancel, `result` will be `false`.
- You can use this value to decide what to do next in your code.

### Key Points

- **alert()** is for showing a simple message.
- **confirm()** is for asking the user to confirm or cancel.
- Both stop the code until the user responds (they are "modal" pop-ups).
- Use alert for information, and confirm for yes/no questions.

---

---
## COM vs DCOM (Q4)

**Q4: Is COM same as DCOM?**

No, COM and DCOM are not the same, but they are related.

### What is COM?

- **COM** stands for **Component Object Model**.
- It is a Microsoft technology for building reusable software parts (called components) that can work together.
- COM components run on the **same computer** (locally).
- Used in Windows applications to let different programs or parts of a program communicate.

### What is DCOM?

- **DCOM** stands for **Distributed Component Object Model**.
- It is an extension of COM.
- DCOM allows components to communicate **over a network** (not just on the same computer).
- Used when you want software on different computers to work together.

### Key Differences

| Feature         | COM (Component Object Model)         | DCOM (Distributed COM)                |
|-----------------|-------------------------------------|---------------------------------------|
| Where it works  | Same computer (local)               | Across network (local and remote)     |
| Communication   | Within one machine                  | Between different machines            |
| Use case        | Local Windows applications          | Networked or distributed applications |
| Example         | Word and Excel sharing data locally | A program on one PC using a service on another PC |

### Summary Points

- **COM** is for local components on one computer.
- **DCOM** is for components that need to talk over a network.
- DCOM builds on COM by adding network features.
- Both are used mainly in Windows environments.

**In simple words:**  
COM lets programs on the same computer share features. DCOM lets programs on different computers share features over a network.

---






Introduction to JavaScript, Creating Variables in
JavaScript, Creating Functions in JavaScript, UI Events, Returning Data from Functions

1.  What are the objects in JavaScript?
2.  What are the features of JavaScript? Write a program in JavaScript to display “Hello”. Also show the usage of FOR statement by taking an example.
3.  What are objects in JavaScript? Write a Script to generate random numbers.
4.  Is COM same as DCOM? Comment on it.
5.  Compare CGI and JavaScript.
6.  Explain the various Form objects used by JavaScript. Write JavaScript to demonstrate how data validation can be performed.
7.  What is Document Object Model? How to create a text box and button in DOM.
8.  What is the difference between JavaScript and Jscript? How will you do client-side validation using JavaScript?
9.  Explain the scope of `let` and `var` variables in JavaScript.
10. Differentiate between Client-Side scripting and Server-Side Scripting.
11. Illustrate Document Object Model. How to create a text box and button in DOM.
12. ‘JavaScript is referred to as object-based programming language’. Illustrate with an example.
13. Construct a JavaScript program to print the reverse digits of any number.
14. What do you mean by Switch Case? Explain the various control statements in JavaScript.
15. Differentiate between DOM and COM.
16. Write a code in JavaScript for creating Alert and Confirm Box.
17. Define API and CGI.
