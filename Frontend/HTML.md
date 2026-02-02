# HTML - HyperText Markup Language

> _Estimation time: 2-3 Days_

---

HTML (HyperText Markup Language) is the standard markup language for documents designed to be displayed in a web browser. It defines the structure and content of web pages using a system of tags and attributes.

The reason you are learning HTML is because it's the foundation of every web page. Without HTML, there is no web content. Understanding HTML semantics is crucial for accessibility, SEO, and maintainable code.

Make sure you understand the learning concepts but **Don't memorize every tag** - know they exist and where to find them!

---

**_Learning objectives:_**

At the end of this module, you'll be able to:

- Create well-structured HTML documents with proper document structure
- Use semantic HTML elements to convey meaning and improve accessibility
- Work with forms, inputs, and validation attributes
- Embed media content (images, videos, audio)
- Understand the DOM (Document Object Model) structure

---

_Send me back [home](home)_

[[_TOC_]]

---

**Learning note**: all links in this path are reading tutorials. You can read them but you can watch a YouTube crash course on HTML or just experiment with building pages by yourself. If you find useful links, please share them with me.

Here are some example links:

- [MDN HTML Basics](https://developer.mozilla.org/en-US/docs/Learn/Getting_started_with_the_web/HTML_basics) (30 minutes)
- [HTML Crash Course For Absolute Beginners](https://www.youtube.com/watch?v=UB1O30fR-EE) (1 hour)
- [W3Schools HTML Tutorial](https://www.w3schools.com/html/)

## Setting Up Your Development Environment

Before you start writing HTML, you need a way to view your pages in a browser. The easiest way is using the **Live Server** extension for VS Code.

### Installing Live Server

1. Open VS Code
2. Go to the Extensions view (click the icon with squares on the left sidebar or press `Ctrl+Shift+X`)
3. Search for "Live Server" by Ritwick Dey
4. Click **Install**

### Using Live Server
Create a new folder for your project and open it in vscode -
open your terminal and run:
```sh
mkdir task-manager
code task-manager
```

1. Create an `index.html` file
2. Click the **"Go Live"** button at the bottom-right of VS Code, or right-click on your HTML file and select **"Open with Live Server"**
3. Your default browser will open automatically at `http://127.0.0.1:5500/`

**Benefits:**
- Automatically refreshes the browser when you save changes
- Serves files over HTTP (required for some JavaScript features)
- No need to manually refresh the browser
- Works with multiple devices on your network

## Document Structure

Learn the basic structure of an HTML document.

### Essential Elements

Every HTML document should have:

- `<!DOCTYPE html>` - Document type declaration
- `<html>` - Root element
- `<head>` - Metadata container
- `<body>` - Visible content container

```html
<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>My First Page</title>
  </head>
  <body>
    <h1>Hello, World!</h1>
    <p>This is my first web page.</p>
  </body>
</html>
```

### Head Section

The `<head>` contains metadata about the document:

- `<meta charset="UTF-8">` - Character encoding
- `<meta name="viewport">` - Responsive design settings
- `<title>` - Page title (shown in browser tab)
- `<link>` - External resources (CSS, favicon)
- `<script>` - JavaScript files

### Questions - Document Structure

1. What is the purpose of the `<!DOCTYPE html>` declaration?
2. Why is the `lang` attribute important on the `<html>` element?
3. What happens if you don't include the viewport meta tag?
4. Where should you place CSS links and why?

## Semantic HTML

Semantic HTML uses tags that convey meaning about the content, not just presentation.

### Common Semantic Elements

**Document Structure:**

- `<header>` - Introductory content or navigation
- `<nav>` - Navigation links
- `<main>` - Main content of the document
- `<article>` - Self-contained content
- `<section>` - Thematic grouping of content
- `<aside>` - Sidebar content
- `<footer>` - Footer content

**Text Content:**

- `<h1>` through `<h6>` - Headings (h1 is most important)
- `<p>` - Paragraph
- `<ul>`, `<ol>`, `<li>` - Lists
- `<blockquote>` - Quoted content
- `<code>` - Code snippets
- `<pre>` - Preformatted text

**Why Semantics Matter:**

- **Accessibility**: Screen readers use semantic tags to navigate
- **SEO**: Search engines understand content structure better
- **Maintainability**: Code is easier to read and maintain
- **Default Styling**: Browsers apply appropriate default styles

### Exercise: Semantic Blog Post

Convert this non-semantic HTML to use semantic elements:

```html
<div class="header">
  <div class="title">My Blog</div>
  <div class="nav">
    <div>Home</div>
    <div>About</div>
  </div>
</div>
<div class="content">
  <div class="post">
    <div class="post-title">My First Post</div>
    <div class="post-body">This is the content...</div>
  </div>
</div>
<div class="footer">
  <div>Copyright 2024</div>
</div>
```

## Forms and Inputs

Forms allow users to input data and interact with web applications.

### Basic Form Structure

```html
<form action="/submit" method="POST">
  <label for="username">Username:</label>
  <input type="text" id="username" name="username" required>
  
  <label for="email">Email:</label>
  <input type="email" id="email" name="email" required>
  
  <label for="password">Password:</label>
  <input type="password" id="password" name="password" minlength="8">
  
  <button type="submit">Sign Up</button>
</form>
```

### Input Types

Common input types:

- `text` - Single-line text
- `email` - Email address with validation
- `password` - Masked input
- `number` - Numeric input
- `tel` - Telephone number
- `url` - URL with validation
- `date` - Date picker
- `checkbox` - Multiple selections
- `radio` - Single selection from group
- `file` - File upload
- `hidden` - Invisible data

### Form Attributes

Important attributes:

- `required` - Field must be filled
- `placeholder` - Hint text
- `min` / `max` - Numeric range
- `minlength` / `maxlength` - Text length limits
- `pattern` - Regular expression validation
- `disabled` - Non-interactive field
- `readonly` - Non-editable field

### Exercise: Registration Form

Create a registration form with:

1. Username (required, 3-20 characters)
2. Email (required, valid email format)
3. Password (required, minimum 8 characters)
4. Age (optional, minimum 13)
5. Terms of service checkbox (required)
6. Submit button

Add appropriate labels and validation attributes.

## Media Elements

HTML supports embedding images, audio, and video directly.

### Images

```html
<img src="photo.jpg" alt="Description of the image" width="300" height="200">
```

**Important attributes:**

- `src` - Image source URL
- `alt` - Alternative text for accessibility
- `width` / `height` - Dimensions (prevents layout shift)
- `loading="lazy"` - Lazy loading for performance

### Video and Audio

```html
<video controls width="400" poster="thumbnail.jpg">
  <source src="video.mp4" type="video/mp4">
  <source src="video.webm" type="video/webm">
  Your browser does not support the video tag.
</video>

<audio controls>
  <source src="audio.mp3" type="audio/mpeg">
  Your browser does not support the audio element.
</audio>
```

### Questions - Media

1. Why is the `alt` attribute crucial for images?
2. What is the purpose of providing multiple `<source>` elements?
3. When should you use lazy loading for images?

## Tables

Tables display tabular data (not for layout!).

```html
<table>
  <thead>
    <tr>
      <th>Name</th>
      <th>Age</th>
      <th>City</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>Alice</td>
      <td>25</td>
      <td>New York</td>
    </tr>
    <tr>
      <td>Bob</td>
      <td>30</td>
      <td>London</td>
    </tr>
  </tbody>
</table>
```

## Links and Navigation

Links connect pages and resources.

```html
<!-- External link -->
<a href="https://example.com" target="_blank" rel="noopener noreferrer">
  Visit Example
</a>

<!-- Internal link -->
<a href="/about">About Page</a>
<a href="#section2">Jump to Section 2</a>

<!-- Email link -->
<a href="mailto:someone@example.com">Send Email</a>

<!-- Phone link -->
<a href="tel:+1234567890">Call Us</a>
```

**Security note**: Always use `rel="noopener noreferrer"` with `target="_blank"` to prevent tabnabbing attacks.

## HTML5 Features

Modern HTML includes many useful features:

### Data Attributes

Store custom data in elements:

```html
<div data-user-id="123" data-role="admin">User Info</div>
```

### Details and Summary

Collapsible content without JavaScript:

```html
<details>
  <summary>Click to expand</summary>
  <p>This content can be expanded and collapsed.</p>
</details>
```

### Exercise: Create a Simple Task List

Create a basic HTML file (`index.html`) with a simple task list structure:

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>My Tasks</title>
</head>
<body>
  <!-- Create:
       1. A heading with "My Tasks"
       2. An input field + button to add tasks
       3. A list (<ul>) with 3 sample tasks
       4. Each task should have a checkbox and text
  -->
</body>
</html>
```

**Requirements:**
- Use semantic HTML (`<header>`, `<main>`, etc.)
- Include proper labels for the input
- Use `data-id` attributes on task items

**Time:** ~15 minutes

**Validation:** Open with Live Server and check it displays correctly.

## Accessibility (A11y)

Accessible HTML ensures everyone can use your website.

### Key Principles

- Use semantic elements
- Provide alt text for images
- Ensure proper heading hierarchy (don't skip levels)
- Use labels with form inputs
- Ensure sufficient color contrast (CSS)
- Make interactive elements keyboard accessible

### ARIA Attributes

When semantic HTML isn't enough:

```html
<button aria-label="Close menu" aria-expanded="false">
  <span aria-hidden="true">×</span>
</button>

<div role="alert" aria-live="polite">
  Form submitted successfully!
</div>
```

### Questions - Accessibility

1. Why is it important not to skip heading levels (e.g., h1 to h3)?
2. When should you use ARIA attributes versus semantic HTML?
3. How do you make a custom button accessible?

## Best Practices

- **Validate your HTML**: Use the [W3C Validator](https://validator.w3.org/)
- **Indent consistently**: 2 spaces is standard
- **Use lowercase tags**: `<div>` not `<DIV>`
- **Quote attribute values**: `class="container"`
- **Close all tags**: Even self-closing in XHTML style: `<img />`
- **Comment when needed**: `<!-- Section: Header -->`

## Tools & Resources

- [HTML Validator](https://validator.w3.org/) - Check your HTML for errors
- [Can I Use](https://caniuse.com/) - Check browser support for HTML features
- [MDN HTML Reference](https://developer.mozilla.org/en-US/docs/Web/HTML/Reference) - Complete tag reference
- [HTML5 Doctor](http://html5doctor.com/) - HTML5 semantics guide

## Worth Knowing (Advanced)

These concepts are worth mentioning but don't learn them now:

- `<iframe>` - Embedding other web pages
- `<canvas>` - Drawing graphics with JavaScript
- `<svg>` - Scalable Vector Graphics
- Web Components (Custom Elements, Shadow DOM)
- Microdata and structured data for SEO
- Content Security Policy (CSP) meta tags

## Next steps

You've created a basic task list structure with HTML!

Next, add styling in the [CSS](Frontend/CSS) module:
- Basic layout with Flexbox
- Simple responsive design
- Visual polish

Then add interactivity in the [JavaScript Vanilla](Frontend/javascript-vanilla) module.

The exercises are short (5-20 minutes each) - just enough to understand the concepts.
