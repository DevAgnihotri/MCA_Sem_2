# Event Driven Programming
---

## 1. Introduction to Graphics Programming

- Graphics programming in Java allows you to create visual elements like shapes, colors, images, and custom drawings in your applications.
- Java provides built-in classes and methods for graphics through packages like `java.awt` and `javax.swing`.

---

## 2. Frame

- A **Frame** is a top-level window with a title and a border, used as the main window for a Java GUI application.
- In Java, you can create a frame using the `Frame` class (AWT) or `JFrame` class (Swing).
- Example (using Swing):
  ```java
  JFrame frame = new JFrame("My Window");
  frame.setSize(400, 300);
  frame.setVisible(true);
  frame.setDefaultCloseOperation(JFrame.EXIT_ON_CLOSE);
  ```
- Frames can contain other components like buttons, labels, and panels.

---

## 3. Components

- **Components** are the building blocks of a GUI, such as buttons, labels, text fields, checkboxes, etc.
- All components in Java inherit from the `Component` class (AWT) or `JComponent` class (Swing).
- Common components:
  - `JButton` (button)
  - `JLabel` (label)
  - `JTextField` (text input)
  - `JPanel` (container for other components)
- Components are added to containers (like frames or panels) using the `add()` method.

### Difference Between `JFrame` and `JPanel` in Java Swing

| Feature                        | `JFrame`                               | `JPanel`                                |
| ------------------------------ | -------------------------------------- | --------------------------------------- |
| Purpose                        | Top-level window with title and border | Lightweight container for components    |
| Inheritance                    | Extends `java.awt.Frame`               | Extends `javax.swing.JComponent`        |
| Can be displayed independently | Yes                                    | No (must be added to another container) |
| Typical Usage                  | Main application window                | Organizing and grouping components      |
| Window Controls                | Yes (close, minimize, maximize)        | No                                      |
| Example                        | `new JFrame("Title")`                  | `new JPanel()`                          |

- Use `JFrame` as the main application window.
- Use `JPanel` to group and organize components inside containers like `JFrame`.

---

## 4. Working with 2D Shapes

- Java provides the `Graphics` and `Graphics2D` classes for drawing shapes.
- You can draw shapes by overriding the `paint()` or `paintComponent()` method in a component (like `JPanel`).
- Common 2D shapes:
  - **Line:** `drawLine(x1, y1, x2, y2)`
  - **Rectangle:** `drawRect(x, y, width, height)`
  - **Oval/Circle:** `drawOval(x, y, width, height)`
  - **Round Rectangle:** `drawRoundRect(x, y, width, height, arcWidth, arcHeight)`
  - **Polygon:** `drawPolygon(xPoints, yPoints, nPoints)`
- Example:
  ```java
  public void paintComponent(Graphics g) {
      super.paintComponent(g);
      g.drawRect(50, 50, 100, 60); // Draw rectangle
      g.drawOval(200, 50, 80, 80); // Draw circle
  }
  ```

---

## 5. Using Colors

- The `Color` class in Java is used to set the color for drawing shapes and text.
- You can use predefined colors (like `Color.RED`, `Color.BLUE`) or create custom colors using RGB values.
- To set a color: `g.setColor(Color.RED);`
- Example:
  ```java
  g.setColor(Color.GREEN);
  g.fillRect(20, 20, 50, 50); // Draw filled green square
  ```

---

## 6. Using Fonts

- The `Font` class is used to set the style, size, and typeface of text.
- To set a font: `g.setFont(new Font("Arial", Font.BOLD, 18));`
- Example:
  ```java
  g.setFont(new Font("Serif", Font.ITALIC, 24));
  g.drawString("Hello, Java!", 100, 100);
  ```

---

## 7. Using Images

- The `Image` class is used to display images in Java GUIs.
- You can load an image using `Toolkit.getDefaultToolkit().getImage("path/to/image.jpg")` or `ImageIcon` in Swing.
- To draw an image: `g.drawImage(image, x, y, this);`
- Example:
  ```java
  Image img = Toolkit.getDefaultToolkit().getImage("myPic.jpg");
  g.drawImage(img, 50, 50, this);
  ```
- In Swing, you can also use `ImageIcon`:
  ```java
  JLabel label = new JLabel(new ImageIcon("myPic.jpg"));
  panel.add(label);
  ```

---

# Basics of Event Handling in Java

Event handling is a core concept in Java GUI programming. It allows your program to respond to user actions like button clicks, mouse movements, key presses, and more. Here is a detailed explanation of the basics, with answers to your specific questions included in the relevant sections.

---

## 1. What is an Event? [Q7]

**Question 7: Determine event? How is event handling done in Java'? Explain with an example.**

- An **event** is an object that describes a change in the state of a source (like a button or window) due to user interaction or system-generated actions.

**How is event handling done in Java?**

- **Event handling** in Java is the mechanism that allows a program to respond to user interactions (such as clicks, key presses, or mouse movements) or system-generated events.
- Java uses the **event delegation model**, where an event source (like a button or text field) generates an event, and one or more event listeners handle it.
- An **event listener** is an object that implements a specific interface (such as `ActionListener`, `KeyListener`, or `MouseListener`) and contains methods that are called when the event occurs.
- To handle events, you **register** the listener with the event source using methods like `addActionListener()`, `addKeyListener()`, or `addMouseListener()`.
- When the event occurs, the corresponding method in the listener is automatically invoked by the Java runtime.
- This model separates the event-generating code from the event-handling code, making programs more modular and easier to maintain.

**Key Definitions:**

- **Event Source:** The component that generates the event (e.g., a button, text field, or window).
- **Event Object:** An object that encapsulates information about the event (e.g., `ActionEvent`, `KeyEvent`).
- **Event Listener:** An interface that defines methods to handle specific types of events.

**Example:**

```java
JTextField textField = new JTextField();
textField.addKeyListener(new KeyAdapter() {
    public void keyPressed(KeyEvent e) {
        System.out.println("Key pressed: " + e.getKeyChar());
    }
});
```

In this example:

- The `JTextField` is the event source.
- The `KeyAdapter` is used to handle keyboard events, allowing you to override only the methods you need.
- The `keyPressed` method is called automatically whenever a key is pressed while the text field is focused.

Here, a key event is handled by a `KeyAdapter` attached to a text field.

---

## 2. Event Handling Model in Java [Q6, Q9]

**Question 6: Explain event handling model in Java with proper example.**
**Question 9: What is event and event delegation model, explain with proper example of keyboard or mouse event handling.**

- Java uses the **event delegation model** for handling events.
- In this model, an event is generated by a source (like a button), and sent to one or more listeners (objects that want to handle the event).
- The listener must register itself with the source to receive events.

### Main Components:

- **Event Source:** The object that generates the event (e.g., JButton, JFrame).
- **Event Object:** Contains information about the event (e.g., ActionEvent, MouseEvent).
- **Event Listener:** An interface that defines methods to handle the event (e.g., ActionListener, MouseListener).

**Example (Button Click):**

```java
JButton button = new JButton("Click Me");
button.addActionListener(new ActionListener() {
    public void actionPerformed(ActionEvent e) {
        System.out.println("Button was clicked!");
    }
});
```

Here, the button is the event source, the `ActionListener` is the listener, and `actionPerformed` is the event handler.

**Example (Mouse Event):**

```java
panel.addMouseListener(new MouseAdapter() {
    public void mousePressed(MouseEvent e) {
        System.out.println("Mouse pressed at: " + e.getX() + ", " + e.getY());
    }
});
```

**Example (Keyboard Event):**

```java
textField.addKeyListener(new KeyAdapter() {
    public void keyPressed(KeyEvent e) {
        System.out.println("Key pressed: " + e.getKeyChar());
    }
});
```

---

## 3. Event Handlers

- An **event handler** is a method that is called when an event occurs.
- You write event handler code inside listener methods (like `actionPerformed`, `mouseClicked`).
- Example:
  ```java
  button.addActionListener(new ActionListener() {
      public void actionPerformed(ActionEvent e) {
          System.out.println("Button clicked!");
      }
  });
  ```

---

## 4. Adapter Classes

- **Adapter classes** are helper classes that provide empty implementations of event listener interfaces with multiple methods.
- You can extend an adapter class and override only the methods you need, instead of all methods in the interface.
- Example: `MouseAdapter` implements `MouseListener` with empty methods.
- Usage:
  ```java
  panel.addMouseListener(new MouseAdapter() {
      public void mouseClicked(MouseEvent e) {
          System.out.println("Mouse clicked!");
      }
  });
  ```

---

## 5. Actions

- An **Action** in Java is an interface that combines an event listener with additional properties (like name, icon, enabled/disabled state).
- Used for buttons, menu items, and toolbars that share the same behavior.
- Example:
  ```java
  Action action = new AbstractAction("Click Me") {
      public void actionPerformed(ActionEvent e) {
          System.out.println("Action performed!");
      }
  };
  JButton button = new JButton(action);
  ```

---

## 6. Mouse Events [Q8]

**Question 8: What do you understand by event handling in Java? Give an example of any event like mouse event, keyboard event and windows events.**

- **Mouse events** are actions performed with the mouse, such as clicking, pressing, releasing, entering, or exiting a component.
- Handled using `MouseListener` or `MouseAdapter`.

**Mouse Event Example:**

```java
panel.addMouseListener(new MouseAdapter() {
    public void mouseClicked(MouseEvent e) {
        System.out.println("Mouse clicked at: " + e.getX() + ", " + e.getY());
    }
});
```

**Keyboard Event Example:**

```java
textField.addKeyListener(new KeyAdapter() {
    public void keyTyped(KeyEvent e) {
        System.out.println("Key typed: " + e.getKeyChar());
    }
});
```

**Window Event Example:**

```java
frame.addWindowListener(new WindowAdapter() {
    public void windowClosing(WindowEvent e) {
        System.out.println("Window is closing");
        System.exit(0);
    }
});
```

---

## 7. AWT Event Hierarchy

- The **AWT event hierarchy** shows how different event classes are related in Java.
- All event classes inherit from `java.util.EventObject`.
- Main branches:
  - `AWTEvent` (base for all AWT events)
    - `ActionEvent` (button clicks, menu selections)
    - `MouseEvent` (mouse actions)
    - `KeyEvent` (keyboard actions)
    - `WindowEvent` (window open/close)
    - `ItemEvent` (checkbox, list selection)
    - `ComponentEvent` (component shown/hidden)

| Event Class    | Description                      |
| -------------- | -------------------------------- |
| ActionEvent    | Button/menu actions              |
| MouseEvent     | Mouse clicks, movement           |
| KeyEvent       | Keyboard presses                 |
| WindowEvent    | Window open, close, minimize     |
| ItemEvent      | Checkbox, list item selection    |
| ComponentEvent | Component shown, hidden, resized |

---

## 8. Difference Between AWT and Swing [Q13 & Q14]

**Question 13 & 14: Explain difference between AWT and Swing with proper example.**

| Feature       | AWT (Abstract Window Toolkit)   | Swing (javax.swing)                |
| ------------- | ------------------------------- | ---------------------------------- |
| Package       | java.awt                        | javax.swing                        |
| Look & Feel   | Native OS look                  | Customizable, platform-independent |
| Components    | Heavyweight (uses OS resources) | Lightweight (drawn by Java)        |
| Extensibility | Limited                         | Highly extensible                  |
| Pluggable L&F | No                              | Yes                                |
| Thread Safety | Not fully thread-safe           | Mostly thread-safe                 |
| Examples      | Button, Label, TextField        | JButton, JLabel, JTextField        |

**AWT Example:**

```java
import java.awt.*;
Frame frame = new Frame("AWT Example");
Button button = new Button("Click Me");
frame.add(button);
frame.setSize(200, 100);
frame.setVisible(true);
```

**Swing Example:**

```java
import javax.swing.*;
JFrame frame = new JFrame("Swing Example");
JButton button = new JButton("Click Me");
frame.add(button);
frame.setSize(200, 100);
frame.setVisible(true);
```

---

# Introduction to Swing in Java

Swing is a part of Java's standard library for building graphical user interfaces (GUIs). It is more powerful and flexible than the older AWT (Abstract Window Toolkit). Swing provides a rich set of components and supports advanced features like pluggable look-and-feel, lightweight components, and better event handling.

---

## Layout Management in Swing [Q3, Q4, Q5]

**Q3. What do you understand by Layout manager? Illustrate three type of layout available in Java with the help of suitable syntax.**
**Q4. What do you understand by Layout Manager in Java?**
**Q5. Describe different types of Layout Manager used in Java using example**

### What is a Layout Manager?
- A **Layout Manager** in Java is an object that controls the size and position of components inside a container (such as a `JFrame` or `JPanel`).
- It automatically arranges buttons, labels, text fields, and other components, so you don't have to manually specify their coordinates.
- Layout managers make GUIs flexible and responsive to window resizing and different screen sizes.
- Using a layout manager is essential for creating professional, portable, and maintainable Java GUIs.
- Java provides several built-in layout managers (like `FlowLayout`, `BorderLayout`, `GridLayout`, etc.), but you can also create custom layout managers if needed.
- In most cases, you should avoid using absolute positioning (`null` layout) because it makes your interface less adaptable and harder to maintain.
- To use a layout manager, you typically call the `setLayout()` method on your container and then add components; the layout manager takes care of arranging them.
- For complex interfaces, you can nest containers (like `JPanel`s) with different layout managers to achieve the desired arrangement.
- Proper use of layout managers ensures your application looks good and works well across platforms and screen resolutions.

### Common Layout Managers in Swing

| Layout Manager | Description                                                           | Example Syntax                                             |
| -------------- | --------------------------------------------------------------------- | ---------------------------------------------------------- |
| FlowLayout     | Arranges components in a row, left to right, then next line           | `panel.setLayout(new FlowLayout());`                       |
| BorderLayout   | Divides container into five regions: North, South, East, West, Center | `frame.setLayout(new BorderLayout());`                     |
| GridLayout     | Arranges components in a grid of rows and columns                     | `panel.setLayout(new GridLayout(2,2));`                    |
| BoxLayout      | Arranges components in a single row or column                         | `panel.setLayout(new BoxLayout(panel, BoxLayout.Y_AXIS));` |
| CardLayout     | Allows switching between different panels (like cards)                | `panel.setLayout(new CardLayout());`                       |

#### 1. FlowLayout Example

```java
JPanel panel = new JPanel();
panel.setLayout(new FlowLayout());
panel.add(new JButton("A"));
panel.add(new JButton("B"));
```

#### 2. BorderLayout Example

```java
JFrame frame = new JFrame();
frame.setLayout(new BorderLayout());
frame.add(new JButton("North"), BorderLayout.NORTH);
frame.add(new JButton("Center"), BorderLayout.CENTER);
```

#### 3. GridLayout Example

```java
JPanel panel = new JPanel();
panel.setLayout(new GridLayout(2, 2));
panel.add(new JButton("1"));
panel.add(new JButton("2"));
panel.add(new JButton("3"));
panel.add(new JButton("4"));
```

---

# Swing Components [Q2]

Swing provides many components for building GUIs. Here are some of the most common ones:

## 1. JLabel [Q2(i)]

- A **JLabel** is used to display a short string or an image icon.
- It is not editable and does not react to user input.
- Example:
  ```java
  JLabel label = new JLabel("Hello, World!");
  panel.add(label);
  ```

## 2. JTextField [Q2(ii)]

- A **JTextField** is a single-line text input box.
- Users can type and edit text.
- Example:
  ```java
  JTextField textField = new JTextField(20); // 20 columns wide
  panel.add(textField);
  ```

## 3. JTextArea [Q2(iii)]

- A **JTextArea** is a multi-line area for displaying and editing text.
- Useful for longer input or output.
- Example:
  ```java
  JTextArea textArea = new JTextArea(5, 20); // 5 rows, 20 columns
  panel.add(textArea);
  ```

## 4. JList [Q2(iv)]

- A **JList** displays a list of items for the user to select from.
- Can allow single or multiple selections.
- Example:
  ```java
  String[] items = {"Apple", "Banana", "Cherry"};
  JList<String> list = new JList<>(items);
  panel.add(new JScrollPane(list));
  ```

## 5. JComboBox (Choice) [Q2(v)]

- A **JComboBox** (also called a drop-down or choice box) lets the user pick one item from a list.
- Example:
  ```java
  String[] choices = {"Red", "Green", "Blue"};
  JComboBox<String> comboBox = new JComboBox<>(choices);
  panel.add(comboBox);
  ```

## 6. JButton

- A **JButton** is a push button that users can click to perform an action.
- Example:
  ```java
  JButton button = new JButton("Click Me");
  panel.add(button);
  ```

## 7. JCheckBox

- A **JCheckBox** is a box that can be checked or unchecked.
- Used for options that can be turned on or off.
- Example:
  ```java
  JCheckBox checkBox = new JCheckBox("Accept Terms");
  panel.add(checkBox);
  ```

## 8. JRadioButton

- A **JRadioButton** is used for selecting one option from a group.
- Radio buttons are grouped using a `ButtonGroup` so only one can be selected at a time.
- Example:
  ```java
  JRadioButton r1 = new JRadioButton("Male");
  JRadioButton r2 = new JRadioButton("Female");
  ButtonGroup group = new ButtonGroup();
  group.add(r1);
  group.add(r2);
  panel.add(r1);
  panel.add(r2);
  ```

## 9. JScrollBar

- A **JScrollBar** is a component for scrolling content horizontally or vertically.
- Usually used inside scroll panes.
- Example:
  ```java
  JScrollBar scrollBar = new JScrollBar(JScrollBar.VERTICAL);
  panel.add(scrollBar);
  ```

## 10. JList, JComboBox, JScrollPane (Lists, Choices, Scrollbars)

- **JList** and **JComboBox** are for lists and choices (see above).
- **JScrollPane** is used to add scrollbars to components like JTextArea or JList.
- Example:
  ```java
  JTextArea area = new JTextArea(10, 30);
  JScrollPane scrollPane = new JScrollPane(area);
  panel.add(scrollPane);
  ```

## 11. JFrame, JDialog (Windows and Dialog Boxes)

- **JFrame** is the main window for a Swing application.
- **JDialog** is a pop-up window for messages, input, or custom dialogs.
- Example:
  ```java
  JFrame frame = new JFrame("Main Window");
  JDialog dialog = new JDialog(frame, "Dialog Box", true);
  dialog.setSize(200, 100);
  dialog.setVisible(true);
  ```

---
# Hierarchical Diagram of Java Swing Classes [Q10, Q11]

**Q10 & Q11. Draw hierarchical diagram of Java Swing Classes.**

## Theory

Java Swing is a part of the Java Foundation Classes (JFC) used to create graphical user interfaces (GUIs) for Java applications. Swing builds on top of the Abstract Window Toolkit (AWT) and provides a richer set of lightweight, platform-independent components. All Swing components inherit from the `javax.swing.JComponent` class, which itself extends from `java.awt.Container` and ultimately from `java.awt.Component`. This hierarchical structure allows for code reuse, consistency, and flexibility in building complex GUIs.

- **`java.awt.Component`**: The root class for all AWT and Swing GUI elements.
- **`java.awt.Container`**: A subclass of `Component` that can hold other components (like panels and frames).
- **`javax.swing.JComponent`**: The base class for all lightweight Swing components, providing features like double buffering, borders, and tool tips.
- **Swing Components**: Classes like `JLabel`, `JButton`, `JTextField`, etc., extend `JComponent` and provide specific UI functionality.
- **Top-level Containers**: `JFrame` and `JDialog` are special containers used as main windows and dialog boxes.

## Hierarchy Diagram

```
java.lang.Object
    └── java.awt.Component
                └── java.awt.Container
                            └── javax.swing.JComponent
                                        ├── JLabel
                                        ├── JButton
                                        ├── JTextField
                                        ├── JTextArea
                                        ├── JPanel
                                        ├── JList
                                        ├── JComboBox
                                        ├── JCheckBox
                                        ├── JRadioButton
                                        ├── JScrollBar
                                        └── ...
                            └── javax.swing.JFrame
                            └── javax.swing.JDialog
```

- **JComponent** is the parent for most Swing components.
- **JFrame** and **JDialog** are top-level containers used to create windows and dialogs.
- Other components like `JPanel`, `JButton`, and `JLabel` are used to build the user interface inside these containers.

This hierarchy helps organize Swing classes and makes it easier to understand how different components relate to each other in Java GUI development.

---

# Example: Change Background Color and Show Message [Q15]

**Q15. Write Java Swing program that change background color whenever user click on button and displays the message “Welcome to Java Swing”.**

```java
import javax.swing.*;
import java.awt.*;
import java.awt.event.*;

public class ColorChangeDemo {
    public static void main(String[] args) {
        JFrame frame = new JFrame("Color Change Example");
        JButton button = new JButton("Click Me");
        JLabel label = new JLabel("");
        JPanel panel = new JPanel();
        panel.setLayout(new FlowLayout());
        panel.add(button);
        panel.add(label);
        frame.add(panel);
        frame.setSize(300, 200);
        frame.setDefaultCloseOperation(JFrame.EXIT_ON_CLOSE);
        frame.setVisible(true);

        button.addActionListener(new ActionListener() {
            public void actionPerformed(ActionEvent e) {
                panel.setBackground(Color.YELLOW);
                label.setText("Welcome to Java Swing");
            }
        });
    }
}
```

---

# Q16. How is Applet different from normal Java program?

## Definitions

- **Applet:** An applet is a small Java program that runs inside a web browser or applet viewer. It is typically used for creating interactive features on web pages and extends the `java.applet.Applet` class (or `javax.swing.JApplet` for Swing-based applets).
- **Normal Java Program (Application):** A normal Java program is a standalone application that runs independently on the Java Virtual Machine (JVM), typically starting execution from a `main()` method.

## Difference Table

| Feature                | Applet                                                      | Normal Java Program (Application)                  |
|------------------------|-------------------------------------------------------------|---------------------------------------------------|
| Definition             | Runs inside a browser or applet viewer                      | Runs independently as a standalone application     |
| Entry Point            | `init()`, `start()`, `paint()`, `stop()`, `destroy()` methods | `public static void main(String[] args)` method    |
| GUI Library            | Uses AWT/Swing, but must extend `Applet`/`JApplet`          | Can use AWT/Swing, no such restriction             |
| Execution Environment  | Needs browser/applet viewer                                 | Needs JVM, runs from command line or IDE           |
| Security Restrictions  | Runs in sandbox, limited access to system resources         | Fewer restrictions, can access local resources     |
| Usage                  | Web-based interactive content                               | Desktop applications, utilities, backend programs  |

---
---
