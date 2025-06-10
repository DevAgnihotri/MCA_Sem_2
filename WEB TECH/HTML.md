# HTML Fundamentals

## Introduction to HTML

- Stands for Hyper Text Markup Language
- It is language for describing web pages
- It is the language of tags
- It is the language understand by browser
- HTML was invented in 1990 by a CERN scientist Tim Berners-Lee
- To see the HTML code of a page on the Internet press ctrl + u

### Features of HTML

- Hypertext is a text which is not considered as linear text
- Non-linear means the reader can jump from anywhere to anywhere while pursuing a chain of thought

### HTML Basic Concepts

**Tags** - used to specify the regions of the HTML document, which a browser will read later.
Tags will look like this: `<tag>`

**Element** - is a complete tag, having an opening `<tag>` and a closing `</tag>`.

**Attribute** - is used to change the value of an element in HTML. Usually an element has several attributes.

## Document Structure

An HTML document will always begin and end with an `<html>` tag.
This is the standard structure of an HTML.

### Head Element

- Information placed in this section is essential to the inner working of the document
- Content placed in head has nothing to do with the webpage content
- The `<title>` tag must be inside the head tag. What you write between those two title tags will be seen on the title bar of browser

### Body Element

- The body element is the one that defines the beginning of the page content
- Body contains text, images, graphics, audio, video etc

### Basic HTML Structure

```html
<html>
  <head> </head>
  <body>
    <h2>Welcome to my first web page!</h2>
  </body>
</html>
```

## HTML Tags

### What is an HTML Tag? How is it different from an HTML Element?

- An **HTML tag** is a keyword surrounded by angle brackets, like `<p>`. Tags are used to mark the start or end of an element in an HTML document.
- An **HTML element** includes the opening tag, the content inside, and the closing tag. For example, `<p>Hello</p>` is a complete HTML element.
- In short, a tag is just the markup (like `<p>` or `</p>`), while an element is the whole structure (opening tag, content, and closing tag).
- Some elements are self-closing and only use one tag, like `<br />`.

### Structure of HTML element

- Tags have three parts, the opening, closing and content
- `<openingtag>Content</closingtag>`
- Example: `<p>Paragraph</p>`

### Common Tags

```html
<body>
  <p>paragraph</p>
  <i>italic</i>
  <b>bold</b>
  <u>underline</u>
</body>
```

### Self-closing Tags

- `<br/>`: Used for line break
- `<hr/>`: Used to draw horizontal line

## Tag Attributes

- The attributes are used to personalize tags
- Attributes can be used to change look and feel of a particular tag
- For example: Size, alignment, color of content
- HTML attributes are always defined in the start tag
- Attributes are written in name/value pair like: `<tag name="value">`
- Attribute once used can't be repeated in same element

### Common Attributes

**For `<hr>` tag:**

- `align="left/right/center"`
- `size="number"`
- `width="number"`

**For `<p>` tag:**

- `align="left/right/center/justify"`
- Example: `<p align="justify">The paragraph is a base element in ...</p>`

### Style Attribute

Style allows for inline CSS styling:

```
style="att1=value;att2=value......"
```

Common styles:

- `background:url(../bg1.jpg)`
- `background-color:red`
- `color:white`
- `font-family: 'Monotype Corsiva'`
- `font-size:28px`
- `text-align:center/left/right`

Example:

```html
<html>
  <head> </head>
  <body>
    <p
      style="background-color:red; color:white; font-family:Monotype Corsiva; font-size:28px; text-align:center"
    >
      paragraph tag with attribute
    </p>
  </body>
</html>
```

## HTML Headings

HTML headings are used to define the titles and subtitles on a webpage. They range from `<h1>` (the most important heading, usually the main title, biggest font-size) to `<h6>` (the least important, smallest font size). Headings help organize content, improve readability, and provide structure for both users and search engines. Using headings appropriately also enhances accessibility and SEO.

- HTML includes 6 headings: `<h1>`, `<h2>`, `<h3>`, `<h4>`, `<h5>` and `<h6>`
- Heading elements are used to write headings on a webpage, whereas p tag is only for plain text
- All Headings are bold and block level elements

## HTML Block and Inline Elements

HTML Elements are classified as Block Level and Inline Level elements based on their display behavior.

### Block Level Elements

- `<p>`, `<div>`, `<h1>` to `<h6>`, `<address>`, etc.
- Start from a new line
- Occupy full width of parent

### Inline Level Elements

- `<b>`, `<i>`, `<span>`, `<u>`, etc.
- Start in the same line
- Take only width of their content

### Div Tag

- HTML div tag is used to create divisions
- Div is block level, thus starts from new line and occupies full width of parent
- Div can group all block level elements
- Example: `<div>content inside div</div>`

### Span Tag

- HTML span tag is used to create division inside line
- Span is inline level, thus starts in the same line and occupies width of content
- Example: `<span>content inside span</span>`

## Text Formatting Elements

- `<b>Hello</b>` - Bold Text
- `<i>Hello</i>` - Italic
- `<u>Hello</u>` - Underline Text
- `<sup>2</sup>` - Superscripted Text (X²)
- `<sub>2</sub>` - Subscripted Text (H₂O)
- `<del>Text</del>` - Deleted Text

## HTML Lists

HTML has three types of lists:

- Unordered list (bullets): `<ul></ul>`
- Ordered list (numbers): `<ol></ol>`
- Definition list: `<dl></dl>`

### Unordered List

- An unordered list starts with the `<ul>` and ends with `</ul>` tag
- Each list item starts with the `<li>` tag
- Example:

```html
<h4 align="center">List of Cities</h4>
<ul>
  <li>Kanpur</li>
  <li>Lucknow</li>
  <li>Allahabad</li>
  <li>Varanasi</li>
</ul>
```

- Style can be changed with: `<ul style="list-style-type: circle/square/disk">`

### Ordered Lists

- An ordered list starts with the `<ol>` tag
- Each list item starts with the `<li>` tag
- The list items will be marked with numbers
- Type attribute options:
  - `<ol type="a">` - lowercase letters
  - `<ol type="A">` - uppercase letters
  - `<ol type="i">` - lowercase roman numerals
  - `<ol type="I">` - uppercase roman numerals
- Start attribute specifies starting point:
  - `<ol type="1" start="4">` - Numerals starts with 4
  - `<ol type="I" start="4">` - Numerals starts with IV
  - `<ol type="i" start="4">` - Numerals starts with iv
  - `<ol type="a" start="4">` - Letters starts with d
  - `<ol type="A" start="4">` - Letters starts with D

### Definition List

- Definition list value appear within `<dl></dl>` tag
- Definition list consists of two parts:
  - Definition term `<dt>`
  - Definition description `<dd>`
- Example:

```html
<dl>
  <dt>HTML</dt>
  <dd>This stands for Hyper Text Markup Language</dd>
  <dt>HTTP</dt>
  <dd>This stands for Hyper Text Transfer protocol</dd>
</dl>
```

## Images in HTML

- You can insert any image in your web page by using `<img>` tag
- Syntax: `<img src="Image path" ... attributes-list/>`

### Image Attributes

- `width` and `height`: Set image dimensions in pixels
- `border`: Specify border thickness in pixels
- `alt`: Specifies alternate text if the image cannot be displayed
- `align`: Alignment of the image

Example:

```html
<html>
  <head>
    <title>Displaying Image</title>
  </head>
  <body>
    <img
      src="image.jpeg"
      alt="Test Image"
      border="3"
      align="right"
      height="200"
      width="300"
    />
  </body>
</html>
```

## Links in HTML

- A webpage can contain various links (hyperlinks) that take you directly to other pages
- Hyperlinks allow visitors to navigate between websites by clicking on words, phrases, and images

### Link Syntax

```html
<a href="Document URL" …Attributes-list>Link Text</a>
```

### Target Attribute

- Used to specify the location where linked document is opened
- `_blank`: Opens the linked document in a new window or tab
- `_self`: Opens the linked document in the same frame

Example:

```html
<a href="index.htm" target="_blank">Opens in New Window</a>
<a href="index.htm" target="_self">Opens in Self</a>
```

### Image as Link

```html
<a href="default.html">
  <img src="smiley.gif" width="50" height="50" />
</a>
```

### Download Links

```html
<a href="filename.ext">Download File</a>
```

### Linking to Page Sections (Bookmarks)

Two step process:

1. Create a link to the place where you want to reach with-in a webpage:
   ```html
   <a id="top"></a>
   ```
2. Create a hyperlink to link to that place:
   ```html
   <a href="page.html#top">Go to the Top</a>
   ```

### Image Maps

For an image, you can create an image map with clickable areas:

```html
<img src="planets.gif" alt="Planets" usemap="#planetmap" width=200 height=300">
<map name="planetmap">
  <area shape="rect" coords="0,0,82,126" href="sun.htm" />
  <area shape="circle" coords="90,58,3" href="mercur.htm" />
  <area shape="circle" coords="124,58,8" href="venus.htm" />
</map>
```

## HTML Tables

Tables are defined with the `<table>` tag:

- Tables are divided into rows with the `<tr>` tag
- Table rows are divided into data cells with the `<td>` tag
- A table row can also be divided into headings with the `<th>` tag
- Table data (`<td>`) can contain all sorts of HTML elements like text, images, lists, other tables, etc.

Example:

```html
<table>
  <tr>
    <th>First Name</th>
    <th>Last Name</th>
    <th>Age</th>
  </tr>
  <tr>
    <td>Aman</td>
    <td>Shukla</td>
    <td>70</td>
  </tr>
  <tr>
    <td>Sanjay</td>
    <td>Kumar</td>
    <td>94</td>
  </tr>
</table>
```

### Table Attributes

- `align`: Controls the horizontal alignment (`left/right/center/justify`)
- `valign`: Controls the vertical alignment (`top/bottom/middle`)
- `width`: Sets the width of table (e.g., `width=50%`)
- `border`: Used to set border thickness (e.g., `border=5`)
- `caption`: Serves as a title or explanation for the table and shows at the top

Example with caption:

```html
<table border="1" width="100%">
  <caption>
    This is the caption
  </caption>
  <tr>
    <td valign="middle">row 1, column 1</td>
    <td>row 1, columnn 2</td>
  </tr>
  <tr>
    <td>row 2, column 1</td>
    <td>row 2, columnn 2</td>
  </tr>
</table>
```

### Cell Padding and Cell Spacing

- Cell padding: Represents the distance between cell borders and content within a cell
- Cell spacing: Defines the spacing between adjacent cells

### Colspan and Rowspan

- `colspan`: Used to merge two or more columns into a single column
- `rowspan`: Used to merge two or more rows

Example:

```html
<table border="1">
  <tr>
    <th>Column 1</th>
    <th>Column 2</th>
    <th>Column3</th>
  </tr>
  <tr>
    <td rowspan="2">Row 1 Cell 1</td>
    <td>Row 1 Cell2</td>
    <td>Row 1 Cell 3</td>
  </tr>
  <tr>
    <td>Row 2 Cell 2</td>
    <td>Row 2 Cell 3</td>
  </tr>
  <tr>
    <td colspan="3">Row 3 Cell 1</td>
  </tr>
</table>
```

### Table Backgrounds

- `bgcolor` attribute: Sets background color for whole table or just for one cell
- `background` attribute: Sets background image for whole table or just for one cell

Example:

```html
<table border="1" bordercolor="green" bgcolor="yellow">
  ...
</table>
```

### Table Style Attributes

- `width: 100%;`
- `height: 50px;`
- `border: 1px solid red;`
- `background-image: url("img.gif");`
- `background-color: green;`
- `color: white;` (text color)
- `text-align: left/right/center;`
- `vertical-align: top/bottom/middle;`

## Marquee Tag

- The HTML `<marquee>` tag is used for scrolling piece of text or image displayed either horizontally across or vertically down your web site page

Example:

```html
<marquee>Text</marquee>
```

### Marquee Attributes

- `direction="up/down/left/right"`
- `behavior="scroll/slide/alternate"`
- `height="50"`
- `width="50"`
- `hspace="100"`
- `vspace="100"`
- `scrollamount="10"`
- `loop="5"` (times)

## HTML Multimedia

Web pages often contain multimedia elements of different types and formats like images, music, sound, videos, films, animations, and more.

### HTML Video Element

- The HTML5 `<video>` tag makes it simple to add video to a website
- The `<source>` element allows you to specify alternative video files which the browser may choose from

#### Video Tag Attributes

- `autoplay`: Video will automatically begin to play back
- `controls`: Allows user to control video playback (volume, seeking, pause/resume)
- `loop`: Video will automatically seek back to start after reaching the end
- `src`: URL of the video to embed (optional if using `<source>`)
- `poster`: URL of an image to show until the user plays or seeks
- `width` and `height`: Specifies dimensions of the video's display area

Example:

```html
<video width="400" height="250" controls>
  <source src="movie.mp4" type="video/mp4" />
</video>
```

### HTML Audio Element

- `<audio>` element is used to play an audio file in HTML

Example:

```html
<audio>
  <source src="song.mp3" type="audio/mpeg" />
</audio>
```

#### Audio Attributes

- `autoplay`: Audio will start playing as soon as it is ready
- `controls`: Audio controls should be displayed
- `loop`: Audio will start over again when finished
- `muted`: Audio output should be muted

### The Object Element

- The `<object>` element is supported by all browsers
- It defines an embedded object within an HTML document
- Used to embed plug-ins (like Java applets, PDF readers, Flash Players)

Examples:

```html
<object width="100%" height="500px" data="test.html"></object>
<object data="audi.jpeg"></object>
<object width="400" height="50" data="book.swf"></object>
```

## HTML Forms

HTML Forms are required when you want to collect data from site visitors. Forms can contain elements like:

- Text fields
- Text area
- Drop-down menus
- Radio buttons
- Buttons
- Checkboxes

The HTML `<form>` tag is used to create a form.

### Text Input Controls

There are three types of text input used on forms:

1. Single-line text input controls
2. Password input controls
3. Multi-line text input controls

#### Single-line Text Input

Created using HTML `<input>` tag:

```html
<form>
  First name: <input type="text" name="first_name" /><br />
  Last name: <input type="text" name="last_name" />
</form>
```

Attributes:

- `type`: Indicates the type of input control (set to "text")
- `name`: Used to give a name to the control
- `value`: Provides an initial value inside the control
- `size`: Specifies the width of the text-input control in terms of characters
- `maxlength`: Specifies the maximum number of characters a user can enter

#### Password Input Control

Masks characters as they are entered:

```html
<form>
  User ID: <input type="text" name="user_id" /><br />
  Password: <input type="password" name="password" />
</form>
```

#### Multiple-Line Text Input (Textarea)

Used when longer text input is needed:

```html
<form>
  Description:<br />
  <textarea rows="5" cols="50" name="description">
    Enter Your Address here...
  </textarea>
</form>
```

Attributes:

- `name`: Used to give a name to the control
- `rows`: Indicates the number of rows of text area box
- `cols`: Indicates the number of columns of text area box

### Checkbox Control

- Used when more than one option is required to be selected
- Created using HTML `<input>` tag with type attribute set to "checkbox"

Example:

```html
<form>
  <input type="checkbox" name="maths" value="maths" /> Maths
  <input type="checkbox" name="physics" value="Physics" /> Physics
</form>
```

### Radio Button Control

- Used when out of many options, just one option is required to be selected
- Created using HTML `<input>` tag with type attribute set to "radio"

Example:

```html
<form>
  <input type="radio" name="gender" value="male" /> Male
  <input type="radio" name="gender" value="female" /> Female
</form>
```

### Drop-down Menus (ComboBox)

- HTML select fields provide user to select one or more values from pre-determined options
- Created using the `<select>` tag
- List values are added using the `<option>` tag

Example:

```html
<select name="selectionField">
  <option value="Kanpur">Kanpur</option>
  <option value="Lucknow">Lucknow</option>
  <option value="Allahabad">Allahabad</option>
  <option value="Noida">Noida</option>
</select>
```

#### Select Attributes

- `size`: Specifies visible values
- `selected`: Specifies that an option should be the initially selected value
- `multiple`: Allows users to select multiple items
- `disabled`: Specifies that a drop-down list should be disabled

#### Multiple Selection Drop-down Menu

To allow multiple selections, use the `multiple` attribute:

```html
<select name="s1" size="3" multiple="yes">
  <option value="Kanpur">Kanpur</option>
  <option value="Lucknow">Lucknow</option>
  <option value="Allahabad">Allahabad</option>
  <option value="Noida">Noida</option>
</select>
```

#### Option Groups

You can group related options using the `<optgroup>` tag:

```html
<select>
  <optgroup label="Fruits">
    <option value="Apple">Apple</option>
    <option value="Mango">Mango</option>
  </optgroup>
  <optgroup label="Vegetables">
    <option value="Tomatos">Tomato</option>
    <option value="Onion">Onion</option>
  </optgroup>
</select>
```

### HTML Buttons

- Created using the `<button>` tag or `<input>` tag
- Syntax: `<button type="button" value="Submit">`
- Value can be "Submit", "Reset", or "Button"

Types of buttons:

- Button: A clickable button
- Submit: Submits form data
- Reset: Resets form data to initial values

Example:

```html
<form action="image.html" method="get">
  First name: <input type="text" name="fname" /><br />
  Last name: <input type="text" name="lname" /><br />

  <button type="button" value="Click" onclick="alert('hello');">Click</button>
  <button type="submit" value="Submit">Submit</button>
  <button type="reset" value="Reset">Reset</button>
</form>
```

### HTML5 New Input Types

HTML5 added several new input types:

- `color`
- `date`
- `email`
- `month`
- `number`
- `range`
- `search`
- `tel`
- `time`
- `url`

#### Input Type Image

```html
<form action="task.php">
  Roll No: <input type="text" name="fname" /><br />
  <input
    type="image"
    src="img_submit.gif"
    alt="Submit"
    width="48"
    height="48"
  />
</form>
```

#### Datalist Element

The `<datalist>` element specifies a list of pre-defined options for an `<input>` element:

```html
<form action="">
  <input list="browsers" />
  <datalist id="browsers">
    <option value="Internet Explorer"></option>
    <option value="Firefox"></option>
    <option value="Chrome"></option>
    <option value="Opera"></option>
    <option value="Safari"></option>
  </datalist>
</form>
```

### Form Examples

```html
<form>
  Enter your DOB: <input type="date" name="dob" /><br />
  Enter your email: <input type="email" name="email" /><br />
  Marks Obtained (between 0 and 100):
  <input type="number" name="marks" min="0" max="99" /><br />
  <input type="range" min="1" max="100" value="50" /><br />
</form>
```

Complete form example:

```html
<form>
  Name: <input type="text" name="fname" /><br />
  Email: <input type="text" name="lname" /><br />
  Gender: <input type="radio" name="gen" />Male
  <input type="radio" name="gen" />Female<br />
  <input type="Submit" value="Submit" />
  <input type="Reset" value="Reset" />
</form>
```

## Character Entities

Character entities are used to display reserved characters in HTML or characters not present on your keyboard.

Syntax:

- `&entity_name;` OR
- `&#entity_number;`

Example: `&nbsp;` or `&#160;` is used for non-breaking space

### Useful HTML Character Entities

- `<` less than: `&lt;` or `&#60;`
- `>` greater than: `&gt;` or `&#62;`
- `&` ampersand: `&amp;` or `&#38;`
- `"` double quotation: `&quot;` or `&#34;`
- `'` single quotation: `&apos;` or `&#39;`
- `£` pound: `&pound;` or `&#163;`
- `©` copyright: `&copy;` or `&#169;`
- `®` registered trademark: `&reg;` or `&#174;`

## HTML Meta Tags

- Metadata is data (information) about data
- The `<meta>` tag provides metadata about the HTML document
- Metadata will not be displayed on the page
- Used to specify page description, keywords, author, last modified, and other metadata
- Used by browsers, search engines, or other web services

### Uses of Meta Tag

```html
<meta name="keywords" content="Institute,College, MCA, MBA,PGDM" />
<meta name="description" content="Website on HTML and CSS Tutorial" />
<meta name="author" content="Ivan Byros" />
<meta name="viewport" content="width=device-width, initial-scale=1.0" />
<meta http-equiv="refresh" content="30" />
<meta charset="UTF-8" />
```

## HTML Frames

- HTML Frames divide the web browser window into multiple sections
- Each section can be loaded separately
- A `<frameset>` tag is the collection of frames in the browser window
- The `<frame>` tag defines one particular window (frame) within a `<frameset>`

### Creating Frames

Vertical frames:

```html
<html>
<head>
<title>Frame tag</title>
</head>
<frameset cols="25%,50%,25%">
  <frame src="frame1.html">
  <frame src="frame2.html">
  <frame src="frame3.html">
</frameset>
</html>
```

Horizontal frames:

```html
<html>
<head>
<title>Frame tag</title>
</head>
<frameset rows="30%, 40%, 30%">
  <frame name="top" src="frame1.html">
  <frame name="main" src="frame2.html">
  <frame name="bottom" src="frame3.html">
</frameset>
</html>
```

## Iframes

- The `<iframe>` tag defines a rectangular region within the document in which the browser can display a separate document
- An inline frame is used to embed another document within the current HTML document

Syntax:

```html
<iframe src="URL"></iframe>
<iframe src="mypage.html"></iframe>
<iframe src="mypage.html" height="200" width="300"></iframe>
```

Adding border:

```html
<iframe src="mypage.htm" style="border:2px solid red;"></iframe>
```

Target for links:

```html
<iframe src="mypage.htm" name="iframe1"></iframe>
<p><a href="mypage.html" target="iframe1">Click</a></p>
```

## HTML5 Features

HTML5 is the next major revision of the HTML standard that incorporates features like video playback and drag-and-drop.

Modern browsers like Apple Safari, Google Chrome, Mozilla Firefox, and Opera all support HTML5, as do mobile web browsers on iPhones, iPads, and Android phones.

### Key HTML5 Features

- New Semantic Elements: `<header>`, `<footer>`, `<section>`, etc.
- Forms 2.0: Improvements to HTML web forms with new attributes for `<input>` tag
- Persistent Local Storage: Without third-party plugins
- WebSocket: Bidirectional communication technology for web apps
- Server-Sent Events (SSE): Events flowing from web server to browsers
- Canvas: Two-dimensional drawing surface programmable with JavaScript
- Audio & Video: Embed media without third-party plugins
- Geolocation: Share physical location with web applications
- Microdata: Create custom vocabularies beyond HTML5
- Drag and Drop: Move items between locations on the same webpage

### HTML5 Flexibility

HTML5 comes with a lot of flexibility:

- Uppercase tag names allowed
- Quotes optional for attributes
- Attribute values optional
- Closing empty elements optional
