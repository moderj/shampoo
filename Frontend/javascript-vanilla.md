# Frontend JavaScript

> _Estimation time: 4-5 Days_

---

Frontend JavaScript brings web pages to life. Unlike Node.js JavaScript that runs on servers, frontend JavaScript runs in the browser and can interact with HTML and CSS to create dynamic, interactive user experiences.

The reason you are learning frontend JavaScript is because modern web applications require interactivity. From handling user input to making API calls, from animations to real-time updates - JavaScript makes it all possible in the browser.

**Prerequisites**: Complete the [Node/JavaScript](Node/Javascript) module first. This module focuses specifically on browser APIs and DOM manipulation.

---

**_Learning objectives:_**

At the end of this module, you'll be able to:

- Manipulate the DOM to dynamically change page content
- Handle user events (clicks, input, keyboard, etc.)
- Make HTTP requests to fetch data from APIs
- Store data in the browser (localStorage, sessionStorage)
- Debug JavaScript using browser DevTools
- Understand the event loop and asynchronous operations in the browser

---

_Send me back [home](home)_

[[_TOC_]]

---

**Learning note**: This module assumes you know JavaScript basics (variables, functions, loops, etc.). We focus on browser-specific APIs and patterns. Practice by building small interactive features!

Here are some example links:

- [MDN Web APIs](https://developer.mozilla.org/en-US/docs/Web/API) - Browser API reference
- [JavaScript.info - Browser Document](https://javascript.info/document) - DOM manipulation
- [JavaScript.info - Events](https://javascript.info/events) - Event handling
- [Fetch API Guide](https://developer.mozilla.org/en-US/docs/Web/API/Fetch_API/Using_Fetch)

## The DOM (Document Object Model)

The DOM is a tree representation of your HTML document that JavaScript can interact with.

### Selecting Elements

```javascript
// By ID
const header = document.getElementById('header');

// By class name (returns HTMLCollection)
const buttons = document.getElementsByClassName('btn');

// By tag name (returns HTMLCollection)
const paragraphs = document.getElementsByTagName('p');

// CSS selector (returns first match)
const nav = document.querySelector('.navigation');

// CSS selector (returns all matches as NodeList)
const links = document.querySelectorAll('a.external');
```

### Manipulating Elements

```javascript
// Change text content
element.textContent = 'New text';

// Change HTML content (be careful with XSS!)
element.innerHTML = '<strong>Bold text</strong>';

// Change attributes
element.setAttribute('data-id', '123');
element.src = 'new-image.jpg';

// Add/remove classes
element.classList.add('active');
element.classList.remove('hidden');
element.classList.toggle('visible');
element.classList.contains('active'); // returns boolean

// Change styles (inline styles - use sparingly)
element.style.color = 'blue';
element.style.backgroundColor = '#f0f0f0';
```

### Creating and Removing Elements

```javascript
// Create element
const newDiv = document.createElement('div');
newDiv.textContent = 'I am new!';
newDiv.className = 'container';

// Add to DOM
parentElement.appendChild(newDiv);
parentElement.append(newDiv); // Modern, can append multiple
parentElement.prepend(newDiv); // Add as first child

// Insert at specific position
referenceElement.before(newDiv);
referenceElement.after(newDiv);
referenceElement.replaceWith(newDiv);

// Remove element
oldElement.remove();
parentElement.removeChild(oldElement);
```

### Traversing the DOM

```javascript
// Parent
const parent = element.parentElement;

// Children
const children = element.children; // HTMLCollection
const firstChild = element.firstElementChild;
const lastChild = element.lastElementChild;

// Siblings
const next = element.nextElementSibling;
const previous = element.previousElementSibling;

// Closest ancestor matching selector
const container = element.closest('.container');
```

### Exercise: Add Task Functionality

Create a `script.js` file and add basic functionality:

**Requirements:**
1. When user clicks "Add" button, create a new task item
2. Clear the input field after adding
3. Prevent empty tasks

**Starter code:**
```javascript
const input = document.getElementById('task-input');
const button = document.getElementById('add-btn');
const list = document.getElementById('task-list');

button.addEventListener('click', () => {
  // Your code here:
  // 1. Get input value
  // 2. Create <li> element
  // 3. Add to list
  // 4. Clear input
});
```

**Time:** ~15 minutes

## Event Handling

Events allow JavaScript to respond to user interactions.

### Adding Event Listeners

```javascript
// Modern approach (recommended)
button.addEventListener('click', function(event) {
  console.log('Button clicked!');
  console.log(event.target); // The clicked element
});

// Arrow function
button.addEventListener('click', (event) => {
  console.log('Clicked:', event.target.textContent);
});

// Named function (useful for removing later)
function handleClick(event) {
  console.log('Clicked!');
}

button.addEventListener('click', handleClick);
button.removeEventListener('click', handleClick);
```

### Common Events

**Mouse events:**
- `click` - Mouse click
- `dblclick` - Double click
- `mousedown` / `mouseup` - Mouse button pressed/released
- `mouseenter` / `mouseleave` - Mouse enters/leaves element
- `mousemove` - Mouse moves over element

**Keyboard events:**
- `keydown` - Key pressed down
- `keyup` - Key released
- `keypress` - Key pressed (legacy, use keydown)

**Form events:**
- `submit` - Form submitted
- `change` - Input value changed (on blur)
- `input` - Input value changed (immediate)
- `focus` / `blur` - Element gains/loses focus

**Window events:**
- `load` - Page fully loaded
- `DOMContentLoaded` - DOM parsed (use this!)
- `resize` - Window resized
- `scroll` - Page scrolled

### Event Object

```javascript
element.addEventListener('click', (event) => {
  event.preventDefault(); // Prevent default behavior
  event.stopPropagation(); // Stop bubbling
  
  console.log(event.target); // Element that triggered event
  console.log(event.currentTarget); // Element with listener
  console.log(event.type); // Event type
  
  // Mouse coordinates
  console.log(event.clientX, event.clientY); // Relative to viewport
  console.log(event.pageX, event.pageY); // Relative to document
});
```

### Event Delegation

Instead of adding listeners to many elements, add one to a parent:

```javascript
// Without delegation - inefficient for many items
document.querySelectorAll('.item').forEach(item => {
  item.addEventListener('click', handleClick);
});

// With delegation - one listener handles all
document.getElementById('list').addEventListener('click', (event) => {
  if (event.target.matches('.item')) {
    handleClick(event);
  }
});
```

**Benefits:**
- Better performance with many elements
- Automatically works for dynamically added elements
- Less memory usage

### Exercise: Toggle and Delete

Add two features:

1. **Toggle completion:** Clicking a checkbox toggles a `completed` class on the task
2. **Delete task:** Add delete buttons that remove tasks

**Hint:** Use event delegation on the list:
```javascript
list.addEventListener('click', (e) => {
  if (e.target.matches('.delete-btn')) {
    // Remove the task
  }
  if (e.target.matches('input[type="checkbox"]')) {
    // Toggle completed class
  }
});
```

**Time:** ~15 minutes

**Validation:**
- Test keyboard shortcuts work
- Test all three filter modes
- Verify event delegation works on newly added tasks
- Check that delete doesn't toggle completion

## Fetch API

The Fetch API makes HTTP requests to servers.

### Basic GET Request

```javascript
fetch('https://api.example.com/users')
  .then(response => {
    if (!response.ok) {
      throw new Error(`HTTP error! status: ${response.status}`);
    }
    return response.json();
  })
  .then(data => {
    console.log(data);
  })
  .catch(error => {
    console.error('Error:', error);
  });
```

### Async/Await Syntax

```javascript
async function getUsers() {
  try {
    const response = await fetch('https://api.example.com/users');
    
    if (!response.ok) {
      throw new Error(`HTTP error! status: ${response.status}`);
    }
    
    const data = await response.json();
    return data;
  } catch (error) {
    console.error('Error:', error);
    throw error;
  }
}
```

### POST Request

```javascript
async function createUser(userData) {
  const response = await fetch('https://api.example.com/users', {
    method: 'POST',
    headers: {
      'Content-Type': 'application/json',
    },
    body: JSON.stringify(userData),
  });
  
  return response.json();
}
```

### Request Options

```javascript
fetch(url, {
  method: 'GET', // GET, POST, PUT, DELETE, PATCH
  headers: {
    'Content-Type': 'application/json',
    'Authorization': 'Bearer token123',
  },
  body: JSON.stringify(data), // For POST/PUT
  mode: 'cors', // cors, no-cors, same-origin
  cache: 'no-cache', // default, no-cache, reload, force-cache
});
```

### Exercise: Fetch API (Optional)

Load initial tasks from an API:

```javascript
async function loadTasks() {
  const response = await fetch('https://jsonplaceholder.typicode.com/todos?_limit=3');
  const tasks = await response.json();
  // Display tasks in your list
}

loadTasks();
```

**Time:** ~15 minutes (optional)

## Browser Storage

Store data persistently in the browser.

### localStorage

Data persists until explicitly deleted:

```javascript
// Store data
localStorage.setItem('username', 'john_doe');
localStorage.setItem('settings', JSON.stringify({ theme: 'dark' }));

// Retrieve data
const username = localStorage.getItem('username');
const settings = JSON.parse(localStorage.getItem('settings'));

// Remove data
localStorage.removeItem('username');

// Clear all
localStorage.clear();
```

### sessionStorage

Data persists only for the session:

```javascript
// Same API as localStorage
sessionStorage.setItem('tempData', 'value');
const data = sessionStorage.getItem('tempData');
```

### Storage Limits and Considerations

- localStorage: ~5-10MB
- sessionStorage: ~5-10MB
- **Only strings** - use JSON.stringify/parse for objects
- Synchronous - can block main thread with large data
- Not secure - don't store sensitive data

### Exercise: Save to localStorage

Make tasks persist after page refresh:

```javascript
// Save tasks whenever they change
function saveTasks(tasks) {
  localStorage.setItem('my-tasks', JSON.stringify(tasks));
}

// Load tasks on page load
function loadTasks() {
  const saved = localStorage.getItem('my-tasks');
  return saved ? JSON.parse(saved) : [];
}
```

**Time:** ~10 minutes

## Browser DevTools

Master debugging with browser developer tools.

### Console

```javascript
// Different log levels
console.log('General info');
console.info('Information');
console.warn('Warning!');
console.error('Error!');

// Grouping
console.group('User Data');
console.log('Name:', name);
console.log('Age:', age);
console.groupEnd();

// Tables
console.table(users);

// Timing
console.time('operation');
// ... do something
console.timeEnd('operation');

// Assertions
console.assert(x > 0, 'x must be positive');
```

### Debugging

```javascript
// Set breakpoints in DevTools Sources tab
// Or use debugger statement
function calculate(a, b) {
  debugger; // Execution pauses here when DevTools open
  return a + b;
}
```

### Inspecting Elements

- **Elements tab**: View and edit HTML/CSS live
- **Console tab**: Run JavaScript, view logs
- **Sources tab**: Debug JavaScript, set breakpoints
- **Network tab**: Monitor HTTP requests
- **Application tab**: View storage, service workers
- **Performance tab**: Profile runtime performance

### Exercise: Debug with Console

Use `console.log()` to trace what happens when you add a task:

```javascript
button.addEventListener('click', () => {
  console.log('Button clicked');
  console.log('Input value:', input.value);
  // ... rest of your code
});
```

Open DevTools (F12) → Console tab to see the output.

**Time:** ~5 minutes

## Forms and Validation

Handle form submission and validation.

### Form Submission

```javascript
const form = document.getElementById('signup-form');

form.addEventListener('submit', (event) => {
  event.preventDefault(); // Prevent page reload
  
  // Get form data
  const formData = new FormData(form);
  const data = Object.fromEntries(formData);
  
  // Or get individual fields
  const email = form.querySelector('[name="email"]').value;
  
  // Validate
  if (!email.includes('@')) {
    showError('Please enter a valid email');
    return;
  }
  
  // Submit
  submitForm(data);
});
```

### HTML5 Validation API

```javascript
const input = document.getElementById('email');

// Check validity
if (input.validity.valid) {
  // Input is valid
}

// Validation properties
input.validity.valueMissing; // true if required but empty
input.validity.typeMismatch; // true if wrong format (e.g., email)
input.validity.tooShort; // true if below minlength

// Custom validation
input.setCustomValidity('Please enter a valid email');
input.setCustomValidity(''); // Clear error
```

### Exercise: Simple Validation

Prevent empty or very short tasks:

```javascript
function addTask() {
  const text = input.value.trim();
  
  if (text.length < 3) {
    alert('Task must be at least 3 characters');
    return;
  }
  
  // Add the task...
}
```

**Time:** ~5 minutes

## Modern JavaScript in Browser

### Modules

```javascript
// Export from module.js
export const helper = () => 'help!';
export default class MyClass { }

// Import in main.js
import MyClass, { helper } from './module.js';
```

Use in HTML:
```html
<script type="module" src="main.js"></script>
```

### Template Literals for HTML

```javascript
const user = { name: 'John', age: 30 };

const html = `
  <div class="user-card">
    <h2>${user.name}</h2>
    <p>Age: ${user.age}</p>
  </div>
`;

document.getElementById('container').innerHTML = html;
```

### Destructuring and Spread

```javascript
// Destructure event target
button.addEventListener('click', ({ target }) => {
  console.log(target.textContent);
});

// Spread for merging objects
const defaultSettings = { theme: 'light', fontSize: 16 };
const userSettings = { theme: 'dark' };
const settings = { ...defaultSettings, ...userSettings };
```

## Best Practices

- **Use strict mode**: `'use strict';` or ES modules (strict by default)
- **Cache DOM queries**: Query once, reuse the reference
- **Remove event listeners**: When removing elements, clean up listeners
- **Debounce expensive operations**: Resize, scroll handlers
- **Validate on both sides**: Client-side for UX, server-side for security
- **Progressive enhancement**: Site works without JavaScript, enhanced with it
- **Avoid innerHTML with user data**: XSS risk, use textContent instead

### Performance Tips

```javascript
// Bad - queries DOM on every iteration
for (let i = 0; i < 100; i++) {
  document.getElementById('list').appendChild(item);
}

// Good - cache reference, use DocumentFragment
const list = document.getElementById('list');
const fragment = document.createDocumentFragment();
for (let i = 0; i < 100; i++) {
  fragment.appendChild(item);
}
list.appendChild(fragment);
```

## Tools & Resources

- [MDN Web APIs](https://developer.mozilla.org/en-US/docs/Web/API) - Complete API reference
- [Can I Use](https://caniuse.com/) - Browser support tables
- [JavaScript.info](https://javascript.info/) - Modern JavaScript tutorial
- [Chrome DevTools](https://developer.chrome.com/docs/devtools/) - Debugging guide

## Worth Knowing (Advanced)

These concepts are worth mentioning but don't learn them now:

- Web Components (Custom Elements, Shadow DOM)
- Service Workers and PWAs
- WebSockets for real-time communication
- Web Workers for background processing
- IndexedDB for complex client-side storage
- Intersection Observer API (lazy loading)
- Mutation Observer API (watch DOM changes)
- History API (SPA routing)
- Drag and Drop API
- File API (reading files client-side)

## Next steps

Congratulations! You've learned the three pillars of frontend development:

1. **HTML** - Structure and semantics ✓
2. **CSS** - Styling and layout ✓
3. **JavaScript** - Interactivity ✓

You now have a working task list application. While it's basic, it demonstrates the core concepts you'll use with modern frontend frameworks.

### What to learn next:

- **Frontend frameworks**: React, Vue, or Angular (these handle the DOM manipulation for you)
- **Build tools**: Vite or Webpack
- **TypeScript**: Add type safety to your code
- **Testing**: Jest, Cypress

**Note:** In real projects, you'll use CSS frameworks (Bootstrap, Tailwind) and component libraries rather than writing all CSS from scratch. This training focused on understanding the fundamentals.
