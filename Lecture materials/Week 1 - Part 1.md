
> **NOTE!** The material has been created with the help of the ChatGPT AI application

# The Role and Connection of HTML, CSS, and JavaScript

## HTML - Overview

### What is HTML?
- HTML (HyperText Markup Language) is the "building block" of web pages.
- It defines the content and structure of a website.
- Together with CSS and JavaScript, HTML creates dynamic and interactive experiences.

### The Role of HTML in Web Development
- HTML defines the structure of content, while:
    - CSS handles the appearance.
    - JavaScript adds functionality.
- HTML serves as the foundation for all web applications, from basic pages to advanced SPAs (Single Page Applications).

### The History of HTML
- 1989: Tim Berners-Lee developed the World Wide Web and HTML.
- 1991: The first version of HTML was released.
- 1997: HTML 4.0 introduced forms and stylesheets.
- 2014: HTML5 was standardized to meet the needs of the modern web.

### The Evolution of HTML
- HTML5 introduced the following features:
    - Support for multimedia playback (audio and video).
    - New semantic elements, such as `<article>`, `<nav>`, `<footer>`.
    - Offline capabilities and better integration with JavaScript.
- HTML5 enabled advanced web applications and responsive design.

### Structure of HTML
```html
<!DOCTYPE html>
<html>
  <head>
    <title>Example</title>
  </head>
  <body>
    <h1>Welcome!</h1>
    <p>This is an example page.</p>
  </body>
</html>
```
- Main elements:
    - `html`: Root.
    - `head`: Metadata (title, meta).
    - `body`: Visible content.

### The UI/UX Role of HTML
- The foundation of user experience (UX):
    - A clear and logical structure supports usability.
    - Semantic elements (e.g., `<nav>`, `<header>`) help both users and search engines.
- Supporting the user interface (UI):
    - HTML defines the structure upon which CSS adds visual elements.
    - Forms and interactive elements (e.g., `<input>`, `<button>`) make the UI functional.

### HTML and Accessibility
- Semantic elements like `<main>` and `<section>` improve screen reader support.
- Attributes like `alt` and `aria-label` make web pages more accessible.
- Accessibility is an essential part of UX.

### Practical Use of HTML
Links and images:
```html
<a href="https://example.com">Visit the page</a>
<img src="image.jpg" alt="Description">
```
Forms:
```html
<form action="/submit" method="post">
  <input type="text" placeholder="Enter your name">
  <button type="submit">Submit</button>
</form>
```
### The Future of HTML
- Progressive Web Apps (PWA):
    - Native-like experience in web applications.
- Web Components:
    - Reusable elements extend HTML functionality.
- WebAssembly:
    - Enables high-performance applications directly in the browser.
- Semantics and AI:
    - HTML’s role as the basis for semantic data will grow.

### Summary
- HTML is the foundation of web pages and an essential part of UI/UX design.
- UI/UX concepts through HTML:
    - Logical structure → Usability.
    - Semantics → Better accessibility and SEO.
    - HTML seamlessly integrates with CSS and JavaScript to create intuitive web experiences.

## CSS - In Brief

### What is CSS?
- CSS (Cascading Style Sheets) defines the appearance and style of a website.
- It separates content (HTML) from design.
- CSS enables control over colors, fonts, layout, and animations.

### The Role of CSS in Web Development
- HTML provides the structure, CSS adds the appearance.
- Enables responsive design.
- A key component of user experience (UX) and user interface (UI).

### The History of CSS
- 1996: The first CSS1 standard was published.
- 1998: CSS2 added media support and layout features.
- 2011: CSS3 introduced modularity and new features like animations and flexbox.

### Structure of CSS
```css
h1 {
  color: blue;
  font-size: 24px;
  text-align: center;
}
```
- Selectors define what elements styles apply to.
- Properties and values determine the style.

### Adding CSS Styles
1. Inline:
```html
<h1 style="color: red;">Title</h1>
```
2. Internal Style:
```html
<style>
  h1 { color: green; }
</style>
```
3. External File:
```html
<link rel="stylesheet" href="styles.css">
```

### Layout Tools

- Flexbox:  
    - An easy way to create flexible and centered layouts.  
```css
display: flex;
justify-content: center;
align-items: center;
```

- Grid:  
    - A powerful tool for complex layouts.  
```css
display: grid;
grid-template-columns: repeat(3, 1fr);
```

### Responsive Design

- **CSS Media Queries** enable adapting the appearance to different devices.  
```css
@media (max-width: 600px) {
  body { font-size: 14px; }
}
```

- **Mobile-first design** is a common approach.

### CSS and Animation
- CSS allows simple animations without JavaScript.
```css
@keyframes fade {
  from { opacity: 0; }
  to { opacity: 1; }
}
div { animation: fade 2s; }
```

### The Future of CSS

- **CSS Custom Properties**:  
    - Variables that simplify theme management.  
```css
:root {
  --main-color: #3498db;
}
h1 {
  color: var(--main-color);
}
```

- **CSS Houdini**:  
    - Enhances the extensibility of CSS.

### Summary
- CSS makes web pages visually appealing.  
- It enables responsiveness and animations.  
- Together with HTML and JavaScript, CSS is the foundation of web design and styling.

## JavaScript - In Brief

### What is JavaScript?
- JavaScript (JS) is a programming language that adds interactivity to web pages.
- It is a browser-executable language that works together with HTML and CSS.

### The Role of JavaScript in Web Development
- Building dynamic web pages.
- Logic and interactions for user interfaces.
- Backend development (Node.js) and mobile applications.

### The History of JavaScript
- 1995: Brendan Eich developed JavaScript in 10 days.
- 1997: JavaScript was standardized as ECMAScript.
- 2015 (ES6): A major update introduced new features like `let`, `const`, and arrow functions.

### Basics of JavaScript
```javascript
let name = "Ville";
function greet() {
  alert("Hello, " + name + "!");
}
greet();
```

- `Variables`: `let`, `const`, `var`.
- `Functions`: Code that performs a specific task.

### DOM Manipulation
- JavaScript can dynamically change the content of a web page.
```javascript
document.getElementById("title").innerText = "Welcome!";
```

### Event Handling
- JavaScript reacts to user actions.
```javascript
button.addEventListener("click", function() {
  alert("Button was clicked!");
});
```

### AJAX and API Connections
- Enables loading data without reloading the page.
```javascript
fetch("https://api.example.com/data")
  .then(response => response.json())
  .then(data => console.log(data));
```

### JavaScript Frameworks
- React: For building user interfaces.
- Vue and Angular: Versatile frameworks for large projects.
- Node.js: JavaScript for backend development.

### The Future of JavaScript
- WebAssembly: Better performance in the browser.
- Deno: A modern alternative to Node.js.
- AI and Machine Learning: JavaScript integrations.

### Summary
- JavaScript adds functionality to web pages.
- Together with HTML and CSS, it forms the foundation of modern web development.
- It enables the development of everything from web applications to mobile and server solutions.

## HTML, CSS, and JavaScript in a Web Page

### Separate Files

> **Prompt (ChatGPT):** Can you create a simple and responsive single-page web application that utilizes HTML, CSS, and JavaScript, where each resides in its own file?

- index.html
```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Single Page Web App</title>
  <link rel="stylesheet" href="styles.css">
</head>
<body>
  <header>
    <h1>Welcome to My Single Page</h1>
    <nav>
      <ul>
        <li><a href="#home">Home</a></li>
        <li><a href="#about">About</a></li>
        <li><a href="#contact">Contact</a></li>
      </ul>
    </nav>
  </header>

  <main>
    <section id="home" class="section">
      <h2>Home</h2>
      <p>This is the home section. Scroll down to explore more!</p>
    </section>

    <section id="about" class="section">
      <h2>About</h2>
      <p>This is the about section. Learn more about this page here.</p>
    </section>

    <section id="contact" class="section">
      <h2>Contact</h2>
      <p>Feel free to reach out via the form below:</p>
      <form id="contactForm">
        <input type="text" id="name" placeholder="Your Name" required>
        <input type="email" id="email" placeholder="Your Email" required>
        <textarea id="message" placeholder="Your Message" required></textarea>
        <button type="submit">Send</button>
      </form>
      <p id="formFeedback"></p>
    </section>
  </main>

  <footer>
    <p>&copy; 2025 My Single Page</p>
  </footer>

  <script src="script.js"></script>
</body>
</html>
```
- styles.css

```css
/* General Styles */
body {
  font-family: Arial, sans-serif;
  line-height: 1.6;
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}

header {
  background: #333;
  color: #fff;
  padding: 1rem 0;
  text-align: center;
}

nav ul {
  list-style: none;
  padding: 0;
}

nav ul li {
  display: inline;
  margin: 0 10px;
}

nav ul li a {
  color: #fff;
  text-decoration: none;
}

main {
  padding: 1rem;
}

.section {
  margin: 2rem 0;
  padding: 2rem;
  background: #f4f4f4;
  border-radius: 8px;
}

/* Form Styling */
form {
  display: flex;
  flex-direction: column;
  gap: 1rem;
}

form input, form textarea, form button {
  padding: 10px;
  font-size: 1rem;
  border: 1px solid #ccc;
  border-radius: 4px;
}

form button {
  background: #333;
  color: #fff;
  border: none;
  cursor: pointer;
}

form button:hover {
  background: #555;
}

footer {
  text-align: center;
  padding: 1rem 0;
  background: #333;
  color: #fff;
  position: fixed;
  width: 100%;
  bottom: 0;
}

/* Responsive Design */
@media (max-width: 600px) {
  nav ul li {
    display: block;
    margin: 5px 0;
  }
}
```
- script.js

```javascript
// Handle form submission
document.getElementById('contactForm').addEventListener('submit', function (e) {
  e.preventDefault();

  const name = document.getElementById('name').value;
  const email = document.getElementById('email').value;
  const message = document.getElementById('message').value;

  const feedback = `Thank you, ${name}! We have received your message.`;
  document.getElementById('formFeedback').innerText = feedback;

  // Clear form fields
  this.reset();
});
```
### All in one

> **Prompt (ChatGPT):** Can you make the same page again so that everything is in one file.
```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Single Page Web App</title>
  <style>
    /* General Styles */
    body {
      font-family: Arial, sans-serif;
      line-height: 1.6;
      margin: 0;
      padding: 0;
      box-sizing: border-box;
    }

    header {
      background: #333;
      color: #fff;
      padding: 1rem 0;
      text-align: center;
    }

    nav ul {
      list-style: none;
      padding: 0;
    }

    nav ul li {
      display: inline;
      margin: 0 10px;
    }

    nav ul li a {
      color: #fff;
      text-decoration: none;
    }

    main {
      padding: 1rem;
    }

    .section {
      margin: 2rem 0;
      padding: 2rem;
      background: #f4f4f4;
      border-radius: 8px;
    }

    /* Form Styling */
    form {
      display: flex;
      flex-direction: column;
      gap: 1rem;
    }

    form input, form textarea, form button {
      padding: 10px;
      font-size: 1rem;
      border: 1px solid #ccc;
      border-radius: 4px;
    }

    form button {
      background: #333;
      color: #fff;
      border: none;
      cursor: pointer;
    }

    form button:hover {
      background: #555;
    }

    footer {
      text-align: center;
      padding: 1rem 0;
      background: #333;
      color: #fff;
      position: fixed;
      width: 100%;
      bottom: 0;
    }

    /* Responsive Design */
    @media (max-width: 600px) {
      nav ul li {
        display: block;
        margin: 5px 0;
      }
    }
  </style>
</head>
<body>
  <header>
    <h1>Welcome to My Single Page</h1>
    <nav>
      <ul>
        <li><a href="#home">Home</a></li>
        <li><a href="#about">About</a></li>
        <li><a href="#contact">Contact</a></li>
      </ul>
    </nav>
  </header>

  <main>
    <section id="home" class="section">
      <h2>Home</h2>
      <p>This is the home section. Scroll down to explore more!</p>
    </section>

    <section id="about" class="section">
      <h2>About</h2>
      <p>This is the about section. Learn more about this page here.</p>
    </section>

    <section id="contact" class="section">
      <h2>Contact</h2>
      <p>Feel free to reach out via the form below:</p>
      <form id="contactForm">
        <input type="text" id="name" placeholder="Your Name" required>
        <input type="email" id="email" placeholder="Your Email" required>
        <textarea id="message" placeholder="Your Message" required></textarea>
        <button type="submit">Send</button>
      </form>
      <p id="formFeedback"></p>
    </section>
  </main>

  <footer>
    <p>&copy; 2025 My Single Page</p>
  </footer>

  <script>
    // Handle form submission
    document.getElementById('contactForm').addEventListener('submit', function (e) {
      e.preventDefault();

      const name = document.getElementById('name').value;
      const email = document.getElementById('email').value;
      const message = document.getElementById('message').value;

      const feedback = `Thank you, ${name}! We have received your message.`;
      document.getElementById('formFeedback').innerText = feedback;

      // Clear form fields
      this.reset();
    });
  </script>
</body>
</html>
```

## Extras
- HTML-validointi: https://validator.w3.org/
- CSS-validointi: https://jigsaw.w3.org/css-validator/

## Frameworks in Brief

### What is a Framework?
- **Framework:** A pre-built collection of code and structure that accelerates software development.
- Why use frameworks?
  - Saves time and reduces repetitive tasks.
  - Provides standards and best practices.
  - Often includes community support and ready-made plugins.
- Types:
  - Frontend frameworks (User interfaces).
  - Backend frameworks (Server-side logic).

### Frontend Frameworks
**1. React**
- Developed by: Meta (Facebook).
- Why popular?
  - Component-based architecture.
  - Virtual DOM ensures speed.
  - Large ecosystem (e.g., Next.js, React Native).
- Use cases: SPAs, mobile applications.

**2. Vue.js**
- Developed by: Evan You.
- Why popular?
  - Easy to use and lightweight.
  - High performance and two-way data binding.
- Use cases: Medium-sized projects, startups.

**3. Angular**
- Developed by: Google.
- Why popular?
  - Complete package: Includes everything from routing to state management.
  - Great support for large projects.
- Use cases: Enterprise-level applications.

### Backend Frameworks
**1. Node.js and Express.js**
- Why popular?
  - JavaScript runs on both frontend and backend.
  - Lightweight and fast.
  - Great for API development (REST, GraphQL).
- Use cases: Fast APIs, reactive applications.

**2. Django (Python)**
- Why popular?
  - "Batteries included" philosophy: Comes with everything from databases to authentication.
  - Built-in security features.
- Use cases: Database-driven applications.

**3. Ruby on Rails**
- Why popular?
  - Easy to learn and quick to produce results.
  - Strong community and ready-made plugins (gems).
- Use cases: Startup applications, e-commerce platforms.

### Full-Stack Frameworks
**1. Next.js (React-based)**
- Why popular?
  - Server-side rendering (SSR) and static page generation.
  - Excellent SEO support.
- Use cases: Modern web applications.

**2. Nuxt.js (Vue-based)**
- Why popular?
  - An extension of Vue.js for building static and dynamic applications.
  - Built-in optimizations.
- Use cases: Universal applications.

**3. Laravel (PHP)**
- Why popular?
  - Simple syntax and comprehensive features.
  - Includes everything from routing to ORM.
- Use cases: Websites and web applications.

### How to Choose a Framework?
**1. Project Requirements**
- SPA, PWA, or monolithic application?
- Does it require static or dynamic rendering?

**2. Team Expertise**
- What languages and technologies are familiar?
- Is there a need to quickly learn something new?

**3. Scalability and Support**
- Does the framework have a strong community and documentation?
- How well does it scale for future needs?

**4. Community and Tools Support**
- Availability of plugins, libraries, and integrations.
- Popular frameworks offer long-term stability.
