# CSS - Cascading Style Sheets

## Introduction

Cascading Style Sheets (CSS) is a styling language used to describe the presentation of a document written in HTML. CSS defines how HTML elements should be displayed, It controls layout, colors, fonts, and can adapt the display to different types of devices, such as laptops(widescreen) Monitors (square screen) Mobile phones(portrait).

This guide covers the following topics:

- CSS fundamentals and syntax
- Selectors and how to target HTML elements
- CSS properties for styling text, backgrounds, borders
- Box model and layout techniques
- Positioning elements
- Creating responsive designs
- Introduction to Bootstrap framework

## CSS Fundamentals

### What is CSS?

CSS (Cascading Style Sheets) is the language that styles web pages. It describes how HTML elements should be displayed, controlling everything from colors and fonts to layout and animations.

CSS solves a big problem: Before CSS, HTML elements had to contain style information. CSS removes the styling from HTML content, making it easier to maintain websites.

### Basic CSS Syntax

CSS consists of **selectors** and **declarations**:

```css
selector {
  property: value;
  property: value;
}
```

For example:

```css
body {
  background-color: lightgrey;
  font-family: Arial, sans-serif;
}

h1 {
  color: white;
  text-align: center;
}

p {
  font-family: verdana;
  font-size: 16px;
}
```

In this example:

- `body`, `h1`, and `p` are selectors (targeting HTML elements)
- `background-color`, `font-family`, `color`, etc. are properties
- `lightgrey`, `Arial, sans-serif`, `white`, etc. are values

## Adding CSS to HTML

There are three ways to insert CSS into your HTML:

### 1. Inline CSS

Applied directly to a single HTML element using the `style` attribute:

```html
<h1 style="color: blue; margin-left: 30px;">This is a heading</h1>
```

**Pros**: Immediate application to a specific element.  
**Cons**: Mixes content with presentation; difficult to maintain; needs to be repeated for similar elements.

### 2. Internal CSS

Placed inside a `<style>` element in the `<head>` section:

```html
<head>
  <style>
    body {
      background-color: lightgrey;
    }
    h1 {
      color: maroon;
      margin-left: 50px;
    }
  </style>
</head>
```

**Pros**: No need for external files; styles apply to the entire page.  
**Cons**: Increases page size; styles don't apply across multiple pages.

### 3. External CSS

Linked from an external CSS file:

```html
<head>
  <link rel="stylesheet" type="text/css" href="mystyle.css" />
</head>
```

Where `mystyle.css` is a separate file containing CSS rules.

**Pros**: Separates content from presentation; can be cached by browsers; can be applied to multiple pages.  
**Cons**: Extra HTTP request to load the file.

### CSS Rule Priority (Cascade)

When multiple CSS rules target the same element, they "cascade" into a new "virtual" style rule. The priority order is:

1. Inline style (highest priority)
2. Internal/External style sheets (priority based on order)
3. Browser default (lowest priority)

For rules with equal specificity, the last one defined wins.

## CSS Selectors

| Selector Type          | Syntax Example       | Description / Usage                                     |
| ---------------------- | -------------------- | ------------------------------------------------------- |
| **Element**            | `p {}`               | Selects all `<p>` elements                              |
| **ID**                 | `#header {}`         | Selects element with `id="header"` (unique per page)    |
| **Class**              | `.important {}`      | Selects all elements with `class="important"`           |
| **Element + Class**    | `p.highlight {}`     | Selects `<p>` elements with `class="highlight"`         |
| **Multiple Classes**   | `.center.large {}`   | Selects elements with both `center` and `large` classes |
| **Universal**          | `* {}`               | Selects all elements                                    |
| **Descendant**         | `div p {}`           | Selects `<p>` inside any `<div>`                        |
| **Child**              | `div > p {}`         | Selects `<p>` directly inside `<div>`                   |
| **Adjacent Sibling**   | `div + p {}`         | Selects `<p>` immediately after a `<div>`               |
| **Attribute**          | `input[type="text"]` | Selects `<input>` with `type="text"`                    |
| **Attribute (starts)** | `a[href^="https"]`   | Selects `<a>` with `href` starting with "https"         |
| **Attribute (ends)**   | `img[alt$="icon"]`   | Selects `<img>` with `alt` ending with "icon"           |
| **Grouping**           | `h1, h2, h3 {}`      | Selects all `<h1>`, `<h2>`, and `<h3>` elements         |
| **Pseudo-class**       | `a:hover {}`         | Selects `<a>` elements when hovered                     |
| **Pseudo-element**     | `p::first-letter {}` | Selects the first letter of each `<p>`                  |

Use these selectors to target and style HTML elements efficiently.

Selectors are patterns used to select and style HTML elements.

### Element Selector

Selects HTML elements based on element name:

```css
p {
  text-align: center;
  color: blue;
}
```

This rule affects all `<p>` elements on the page.

### ID Selector

Uses the `id` attribute of an HTML element to select a specific element:

```css
#header {
  background-color: #333;
  color: white;
}
```

To use this selector:

```html
<div id="header">This is my header</div>
```

Note: IDs should be unique within a page.

### Class Selector

Uses the `class` attribute to select elements:

```css
.important {
  font-weight: bold;
  color: red;
}
```

To use this selector:

```html
<p class="important">This text is important!</p>
<h2 class="important">This heading is also important!</h2>
```

You can also specify that only specific elements with a certain class should be affected:

```css
p.highlight {
  background-color: yellow;
}
```

This will only apply to `<p class="highlight">` elements.

Elements can have multiple classes:

```html
<p class="center large">This paragraph is centered and large.</p>
```

### Universal Selector

Selects all HTML elements on the page:

```css
* {
  margin: 0;
  padding: 0;
}
```

You can combine it with other selectors:

```css
div * {
  background-color: yellow; /* All elements inside div elements */
}
```

### Grouping Selectors

Apply the same style to multiple selectors by separating them with commas:

```css
h1,
h2,
h3 {
  color: blue;
  font-family: Arial;
}
```

### Descendant Selectors

Select elements that are descendants of another element:

```css
div p {
  background-color: yellow; /* All p inside div */
}
```

This selects all `<p>` elements inside any `<div>` element.

### Child Selectors

Select elements that are direct children of another element:

```css
body > p {
  color: grey; /* Direct p children of body */
}

div > p {
  background-color: orange; /* Direct p children of div */
}
```

The child selector (`>`) targets only direct children, not all descendants.

### Adjacent Sibling Selector

Select an element immediately following another:

```css
div + p {
  background-color: yellow; /* p elements that directly follow a div */
}
```

This selects the first `<p>` element that immediately follows a `<div>` element.

### Attribute Selectors

Select elements based on their attributes:

```css
input[type="text"] {
  color: red; /* All text inputs */
}

a[href^="https"] {
  color: green; /* Links that start with https */
}

img[alt$="icon"] {
  border: 1px solid blue; /* Images whose alt ends with 'icon' */
}
```

### Pseudo-elements

Style specific parts of an element:

```css
p::first-letter {
  font-size: 200%;
  color: red;
}

p::before {
  content: "Read this: ";
  font-weight: bold;
}

p::after {
  content: " - Important";
  color: red;
}
```

Visual example:

```
Read this: This is a paragraph. - Important
```

Where "R" (first letter) would be large and red, "Read this:" would be bold, and "- Important" would be red.

## CSS Comments

Comments are useful for explaining your code or temporarily disabling parts of it:

```css
/* This is a single-line comment */

/*
  This is a
  multi-line comment
  that spans multiple lines
*/

p {
  color: red; /* This colors the text red */
}
```

## CSS Properties

### Background Properties

Control the background appearance of elements:

```css
body {
  background-color: #f0f0f0;
  background-image: url("paper.gif");
  background-repeat: no-repeat;
  background-position: center top;
  background-attachment: fixed;
  /* Shorthand version: */
  background: #f0f0f0 url("paper.gif") no-repeat center top fixed;
}
```

#### Background-repeat Options:

- `repeat`: Repeats both horizontally and vertically (default)
- `repeat-x`: Repeats only horizontally
- `repeat-y`: Repeats only vertically
- `no-repeat`: Shows the image only once

Visual representation:

```
repeat:        repeat-x:      repeat-y:      no-repeat:
+--------+     +--------+     +--------+     +--------+
|IMAGE   |     |IMAGE   |     |IMAGE   |     |IMAGE   |
|IMAGE   |     |IMAGE   |     |        |     |        |
|IMAGE   |     |IMAGE   |     |IMAGE   |     |        |
+--------+     +--------+     +--------+     +--------+
```

#### Background Position:

Controls where the background image is placed:

```css
/* Named positions */
background-position: top left;
background-position: center center;
background-position: bottom right;

/* Pixel values */
background-position: 50px 100px; /* 50px from left, 100px from top */

/* Percentage values */
background-position: 25% 75%; /* 25% from left, 75% from top */
```

### Border Properties

Add and style borders around elements:

```css
p {
  border-style: solid;
  border-width: 5px;
  border-color: green;
  border-radius: 10px; /* Rounded corners */

  /* Shorthand version: */
  border: 5px solid green;
}
```

#### Border Styles:

- `none`: No border (default)
- `solid`: Solid line
- `dotted`: Dotted line
- `dashed`: Dashed line
- `double`: Double line
- `groove`: 3D grooved border
- `ridge`: 3D ridged border
- `inset`: 3D inset border
- `outset`: 3D outset border

Visual representation:

```
solid:    dotted:   dashed:   double:
+------+  ......    ------    +======+

groove:   ridge:    inset:    outset:
/------\  \------/  ┌------┐  ┌------┐
```

You can set different borders on different sides:

```css
p {
  border-top: 5px solid red;
  border-right: 2px dotted blue;
  border-bottom: 3px dashed green;
  border-left: 1px solid black;
}
```

### Font Properties

Control text appearance:

```css
p {
  font-family: "Times New Roman", Times, serif;
  font-size: 16px;
  font-style: italic;
  font-weight: bold;
  font-variant: small-caps;

  /* Shorthand version: */
  font: italic bold small-caps 16px/1.5 "Times New Roman", Times, serif;
}
```

#### Font Family:

Font families belong to five generic families:

1. Serif (e.g., Times New Roman, Georgia)
2. Sans-serif (e.g., Arial, Verdana)
3. Monospace (e.g., Courier New, Lucida Console)
4. Cursive (e.g., Brush Script MT)
5. Fantasy (e.g., Impact, Comic Sans MS)

Use multiple fonts as fallbacks:

```css
p {
  font-family: "Trebuchet MS", Helvetica, sans-serif;
}
```

#### Font Size:

Can be specified in various units:

- `px`: Pixels (fixed size)
- `em`: Relative to the font-size of the element (2em = 2 times the size)
- `rem`: Relative to font-size of the root element
- `%`: Percentage relative to parent element
- Keywords: `xx-small`, `x-small`, `small`, `medium`, `large`, `x-large`, `xx-large`

### Text Properties

Control text formatting:

```css
p {
  color: #0000ff; /* Blue text */
  text-align: center; /* center, left, right, justify */
  text-decoration: underline; /* underline, overline, line-through, none */
  text-transform: uppercase; /* uppercase, lowercase, capitalize */
  text-indent: 50px; /* Indentation of first line */
  letter-spacing: 3px; /* Space between characters */
  line-height: 1.8; /* Space between lines (1.8 times font size) */
  word-spacing: 10px; /* Space between words */
  text-shadow: 2px 2px 5px red; /* horizontal offset, vertical offset, blur, color */
}
```

Visual example of text properties:

```
Normal text:
The quick brown fox jumps over the lazy dog.

With text-transform: uppercase;
THE QUICK BROWN FOX JUMPS OVER THE LAZY DOG.

With text-indent: 50px;
    The quick brown fox jumps over the lazy dog.

With letter-spacing: 3px;
T h e  q u i c k  b r o w n  f o x...

With line-height: 1.8;
The quick brown fox

jumps over the lazy dog.
```

## Box Model

Every HTML element is treated as a box with:

1. Content - The actual content of the element
2. Padding - Space between content and border
3. Border - Line around the padding
4. Margin - Space outside the border

```
+-------------------------------------------+
| Margin                                    |
| +---------------------------------------+ |
| | Border                                | |
| | +-----------------------------------+ | |
| | | Padding                           | | |
| | | +-----------------------------+   | | |
| | | |          Content            |   | | |
| | | +-----------------------------+   | | |
| | |                                   | | |
| | +-----------------------------------+ | |
| |                                       | |
| +---------------------------------------+ |
|                                           |
+-------------------------------------------+
```

Control these properties:

```css
div {
  width: 300px; /* Content width */
  height: 200px; /* Content height */

  padding: 25px; /* Padding on all sides */
  padding-top: 10px;
  padding-right: 20px;
  padding-bottom: 30px;
  padding-left: 40px;
  /* Shorthand: padding: 10px 20px 30px 40px; (top, right, bottom, left) */

  border: 5px solid black;

  margin: 20px; /* Margin on all sides */
  margin-top: 10px;
  margin-right: 20px;
  margin-bottom: 30px;
  margin-left: 40px;
  /* Shorthand: margin: 10px 20px 30px 40px; (top, right, bottom, left) */
}
```

Note that the total width of an element is:
`width + padding-left + padding-right + border-left + border-right + margin-left + margin-right`

To include padding and border in the element's width/height calculation, use:

```css
div {
  box-sizing: border-box;
}
```

## Styling Links

Links can have different states that can be styled separately:

```css
/* Unvisited link */
a:link {
  color: blue;
}

/* Visited link */
a:visited {
  color: purple;
}

/* Mouse over link */
a:hover {
  color: red;
  text-decoration: underline;
}

/* Selected link */
a:active {
  color: green;
}
```

Note: The order matters. For proper styling, use the order: link, visited, hover, active.

## Styling Tables

Control the appearance of tables:

```css
table {
  width: 100%;
  border-collapse: collapse; /* Removes spacing between cells */
}

th,
td {
  border: 1px solid black;
  padding: 8px;
  text-align: left;
}

th {
  background-color: #f2f2f2;
  color: black;
}

tr:nth-child(even) {
  background-color: #f9f9f9; /* Zebra striping */
}

tr:hover {
  background-color: #e6e6e6; /* Highlight on hover */
}
```

Visual example:

```
+----------------------+----------------------+---------------------+
| Header 1             | Header 2             | Header 3            |
+----------------------+----------------------+---------------------+
| Row 1, Cell 1        | Row 1, Cell 2        | Row 1, Cell 3       |
+----------------------+----------------------+---------------------+
| Row 2, Cell 1        | Row 2, Cell 2        | Row 2, Cell 3       |
+----------------------+----------------------+---------------------+
```

## CSS Positioning

The `position` property specifies how an element is positioned:

### Static (Default)

Elements are positioned according to the normal flow of the document:

```css
div {
  position: static;
}
```

### Relative

Positioned relative to its normal position:

```css
div {
  position: relative;
  left: 30px;
  top: 20px;
}
```

This moves the element 30px from the left and 20px from the top of where it would normally be.

### Absolute

Positioned relative to its nearest positioned ancestor (or the document body):

```css
div {
  position: absolute;
  top: 80px;
  left: 50px;
}
```

This places the element 80px from the top and 50px from the left of its nearest positioned parent.

### Fixed

Positioned relative to the viewport, so it stays in the same place even when the page is scrolled:

```css
div.fixed {
  position: fixed;
  bottom: 0;
  right: 0;
  width: 300px;
  background-color: #f8f8f8;
}
```

This creates a fixed element at the bottom right corner of the screen.

## Float and Clear

The `float` property specifies how an element should float:

```css
img {
  float: left; /* Element floats to the left */
}

p {
  clear: both; /* No floating elements allowed on either side */
}
```

Float values:

- `left`: Float to the left
- `right`: Float to the right
- `none`: Default, don't float
- `inherit`: Inherit the float value from its parent

The `clear` property specifies which sides of an element should not be adjacent to floating elements:

- `left`: No floating elements on the left
- `right`: No floating elements on the right
- `both`: No floating elements on either side
- `none`: Default, allow floating elements on both sides

## Bootstrap Framework

Bootstrap is a popular CSS framework for building responsive, mobile-first websites.

### Key Features

- Free and open-source
- Responsive and mobile-first
- Pre-styled components (buttons, forms, etc.)
- Grid system for layout
- Highly customizable

### Advantages and Disadvantages of Bootstrap vs. Custom CSS

#### Advantages of Bootstrap

- **Rapid Development:** Pre-built components and utilities speed up the design process.
- **Responsive Design:** Built-in grid system and classes make mobile-first layouts easy.
- **Consistency:** Ensures a uniform look and feel across browsers and devices.
- **Cross-browser Compatibility:** Handles many browser quirks out of the box.
- **Community Support:** Extensive documentation and a large community for help and resources.
- **Customizable:** Can be customized via Sass variables and custom builds.

#### Disadvantages of Bootstrap

- **Generic Look:** Sites can look similar if not customized, as many use default styles.
- **File Size:** Including the full Bootstrap library can increase page load times.
- **Learning Curve:** Requires learning Bootstrap’s class names and structure.
- **Overhead:** May include features and styles you don’t need, leading to unused CSS.
- **Less Flexibility:** Custom designs may require overriding Bootstrap styles, which can be cumbersome.

**Summary:**  
Bootstrap is ideal for quickly building responsive, consistent interfaces, especially for prototypes or when design consistency is a priority. For highly customized or lightweight sites, custom CSS may be preferable.

### Bootstrap Grid System

Bootstrap uses a 12-column grid layout with different classes for different screen sizes:

- `col-` (extra small screens, <576px)
- `col-sm-` (small screens, ≥576px)
- `col-md-` (medium screens, ≥768px)
- `col-lg-` (large screens, ≥992px)
- `col-xl-` (extra large screens, ≥1200px)

Basic grid example:

```html
<div class="container">
  <div class="row">
    <div class="col-md-4">
      <!-- Content for the first column (4/12 width on medium screens) -->
    </div>
    <div class="col-md-8">
      <!-- Content for the second column (8/12 width on medium screens) -->
    </div>
  </div>
</div>
```

Visual representation:

```
+--------------------------------------+
|              Container               |
| +----------------------------------+ |
| |               Row                | |
| | +-----------+------------------+ | |
| | | col-md-4  |    col-md-8      | | |
| | | (4/12)    |     (8/12)       | | |
| | |           |                   | | |
| | |           |                   | | |
| | +-----------+------------------+ | |
| +----------------------------------+ |
+--------------------------------------+
```

### Responsive Design with Bootstrap

```html
<div class="container">
  <div class="row">
    <div class="col-sm-6 col-md-4 col-lg-3">
      <!-- This column takes:
           - 6/12 width on small screens
           - 4/12 width on medium screens
           - 3/12 width on large screens
      -->
      Content
    </div>
  </div>
</div>
```

## Conclusion

CSS is a powerful language for styling web pages. From basic text formatting to complex layouts, CSS provides the tools to create visually appealing and responsive websites. Combined with frameworks like Bootstrap, it becomes even easier to build professional-looking web applications that work well on all devices.

To continue learning, try experimenting with different CSS properties and values, and explore CSS animations, transitions, and advanced layout techniques like Flexbox and CSS Grid.
