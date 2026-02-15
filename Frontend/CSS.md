# CSS - Cascading Style Sheets

> _Estimation time: 4-6 Days_

---

CSS (Cascading Style Sheets) is a stylesheet language used to describe the presentation of a document written in HTML. It controls layout, colors, fonts, animations, and responsive design.

The reason you are learning CSS is because structure without style is boring. CSS transforms plain HTML into beautiful, engaging user interfaces. Modern CSS includes powerful layout systems like Flexbox and Grid that make complex layouts straightforward.

Make sure you understand the learning concepts and **practice by building** - CSS is best learned through experimentation!

---

**_Learning objectives:_**

At the end of this module, you'll be able to:

- Apply styles using selectors, properties, and values
- Create layouts using Flexbox and CSS Grid
- Build responsive designs with media queries
- Use CSS variables for maintainable code
- Implement animations and transitions
- Understand the box model and positioning

---

_Send me back [home](home)_

[[_TOC_]]

---

**Learning note**: CSS is visual - experiment constantly! Use browser DevTools to test styles in real-time. If you find useful resources, please share them with me.

Here are some example links:

- [MDN CSS Basics](https://developer.mozilla.org/en-US/docs/Learn/Getting_started_with_the_web/CSS_basics) (45 minutes)
- [CSS Crash Course](https://www.youtube.com/watch?v=yfoY53QXEnI) (1.5 hours)
- [Flexbox Froggy](https://flexboxfroggy.com/) - Interactive Flexbox game
- [CSS Grid Garden](https://cssgridgarden.com/) - Interactive Grid game
- [CSS-Tricks](https://css-tricks.com/) - Comprehensive CSS reference
- [CSS-Battle](https://cssbattle.dev/) - Interactive CSS challenges (recommended)

## CSS Basics

### Ways to Add CSS

**Inline styles** (avoid when possible):
```html
<p style="color: blue; font-size: 16px;">Blue text</p>
```

**Internal stylesheet**:
```html
<head>
  <style>
    p { color: blue; }
  </style>
</head>
```

**External stylesheet** (recommended):
```html
<head>
  <link rel="stylesheet" href="styles.css">
</head>
```

### CSS Syntax

```css
selector {
  property: value;
  property: value;
}
```

Example:
```css
h1 {
  color: #333;
  font-size: 2rem;
  margin-bottom: 1rem;
}
```

### Selectors

**Basic selectors:**

```css
/* Element selector */
p { color: black; }

/* Class selector */
.container { max-width: 1200px; }

/* ID selector */
#header { background: #f0f0f0; }

/* Universal selector */
* { box-sizing: border-box; }
```

**Combinators:**

```css
/* Descendant (space) */
nav a { text-decoration: none; }

/* Direct child (>) */
ul > li { list-style: square; }

/* Adjacent sibling (+) */
h2 + p { margin-top: 0; }

/* General sibling (~) */
h2 ~ p { color: gray; }
```

**Pseudo-classes:**

```css
/* Hover state */
button:hover { background: #0056b3; }

/* Focus state */
input:focus { border-color: blue; }

/* First child */
li:first-child { font-weight: bold; }

/* Nth child */
li:nth-child(odd) { background: #f5f5f5; }

/* Not selector */
button:not(.disabled) { cursor: pointer; }
```

**Pseudo-elements:**

```css
/* First line */
p::first-line { font-weight: bold; }

/* Before content */
.required::before { content: "* "; color: red; }

/* After content */
.external-link::after { content: " ↗"; }
```

### Questions - Selectors

1. What is the difference between `.class` and `#id` selectors?
2. When would you use a direct child selector (`>`) instead of a descendant selector (space)?
3. What is specificity and how does it affect which styles are applied?

## The Box Model

Every element in CSS is a rectangular box. Understanding the box model is crucial for layout.

### Box Model Components

```
┌─────────────────────────────┐
│          Margin             │
│   ┌─────────────────────┐   │
│   │      Border         │   │
│   │   ┌─────────────┐   │   │
│   │   │   Padding   │   │   │
│   │   │   ┌─────┐   │   │   │
│   │   │   │Content│ │   │   │
│   │   │   └─────┘   │   │   │
│   │   └─────────────┘   │   │
│   └─────────────────────┘   │
└─────────────────────────────┘
```

```css
.box {
  width: 300px;
  height: 200px;
  padding: 20px;
  border: 2px solid black;
  margin: 10px;
}
```

**Total width** = width + padding-left + padding-right + border-left + border-right + margin-left + margin-right

### Box Sizing

```css
/* Default - width/height only includes content */
box-sizing: content-box;

/* Recommended - width/height includes padding and border */
box-sizing: border-box;
```

Always set `box-sizing: border-box` globally:

```css
*, *::before, *::after {
  box-sizing: border-box;
}
```

### Exercise: Style Your Task List with Flexbox

Create a `styles.css` file and link it to your HTML. This exercise teaches Flexbox through practical examples.

#### Step 1: Basic Setup

```css
* {
  box-sizing: border-box;
}

body {
  font-family: -apple-system, BlinkMacSystemFont, 'Segoe UI', Roboto, sans-serif;
  max-width: 600px;
  margin: 0 auto;
  padding: 20px;
}
```

#### Step 2: Flexbox for Input Row

Make the input and button sit side by side:

```css
.input-row {
  display: flex;
  gap: 10px;
  margin-bottom: 20px;
}

.input-row input {
  flex: 1; /* Takes all available space */
  padding: 8px;
}

.input-row button {
  padding: 8px 16px;
  white-space: nowrap; /* Prevents button text from wrapping */
}
```

**How `flex: 1` works:**
- The input grows to fill available space
- The button keeps its natural width
- Gap adds space between them

**Try changing:**
- `flex: 1` to `flex: 2` on input - see how it takes more space
- Add `flex-wrap: wrap` - see what happens on small screens
- Change `gap` to `20px` or `5px` - observe spacing changes

#### Step 3: Flexbox for Task Items

Align checkbox and text horizontally:

```css
.task-item {
  display: flex;
  align-items: center; /* Vertically centers items */
  gap: 10px;
  padding: 8px;
  border-bottom: 1px solid #ddd;
}

.task-item input[type="checkbox"] {
  /* Checkbox keeps its natural size */
}

.task-item span {
  flex: 1; /* Text takes remaining space */
}
```

**How `align-items: center` works:**
- Without it: items align to top (try removing it!)
- With `flex-start`: items align to top
- With `flex-end`: items align to bottom
- With `center`: items vertically centered

**Visual comparison:**
```
Without align-items:        With align-items: center:
[ ] Task text               [ ] Task text
     Delete                      Delete
(Checkbox and text          (Everything aligned
 not aligned)                to center)
```

#### Step 4: Visual Polish

```css
.completed {
  text-decoration: line-through;
  color: #888;
}

button:hover {
  background-color: #0056b3;
  cursor: pointer;
}
```

**Experiment:** Try these Flexbox variations in DevTools:
1. `justify-content: space-between` - pushes items to edges
2. `flex-direction: column` - stacks items vertically
3. `order: -1` on checkbox - moves it to the end

**Time:** ~20 minutes

**Key takeaway:** Flexbox makes horizontal alignment easy. The input grows (`flex: 1`), button stays fixed, and everything aligns with `align-items`.

## Colors and Typography

### Colors

```css
/* Named colors */
color: red;

/* Hexadecimal */
color: #ff0000;
color: #f00; /* shorthand */

/* RGB */
color: rgb(255, 0, 0);
color: rgba(255, 0, 0, 0.5); /* with transparency */

/* HSL (Hue, Saturation, Lightness) */
color: hsl(0, 100%, 50%);
color: hsla(0, 100%, 50%, 0.5); /* with transparency */
```

### Typography

```css
body {
  font-family: -apple-system, BlinkMacSystemFont, 'Segoe UI', Roboto, sans-serif;
  font-size: 16px;
  line-height: 1.5;
  color: #333;
}

h1 {
  font-size: 2.5rem;
  font-weight: 700;
  margin-bottom: 1rem;
}

p {
  margin-bottom: 1rem;
  text-align: left;
}
```

**Font properties:**

- `font-family` - Font stack (always provide fallbacks)
- `font-size` - Text size (use rem for accessibility)
- `font-weight` - Boldness (400 normal, 700 bold)
- `line-height` - Space between lines (unitless or em)
- `text-align` - Horizontal alignment
- `text-decoration` - Underline, line-through, etc.
- `text-transform` - Uppercase, lowercase, capitalize
- `letter-spacing` - Space between letters

## Layout with Flexbox

Flexbox is a one-dimensional layout method for laying out items in rows or columns.

### Flex Container

```css
.container {
  display: flex;
  flex-direction: row; /* row | row-reverse | column | column-reverse */
  justify-content: center; /* flex-start | flex-end | center | space-between | space-around | space-evenly */
  align-items: center; /* flex-start | flex-end | center | stretch | baseline */
  flex-wrap: wrap; /* nowrap | wrap | wrap-reverse */
  gap: 20px; /* Space between items */
}
```

### Flex Items

```css
.item {
  flex-grow: 1; /* Grow to fill space */
  flex-shrink: 0; /* Don't shrink below flex-basis */
  flex-basis: 200px; /* Initial size */
  /* Shorthand: flex: 1 0 200px; */
  align-self: flex-start; /* Override container align-items */
}
```

### Exercise: Responsive Design with Flexbox

Add a media query to make your task list responsive. This shows how Flexbox adapts to different screen sizes:

```css
/* Mobile: Stack input and button vertically */
@media (max-width: 480px) {
  .input-row {
    flex-direction: column; /* Stack vertically instead of side-by-side */
  }
  
  .input-row input,
  .input-row button {
    width: 100%; /* Full width on mobile */
  }
}
```

**What changed:**
- **Desktop (`flex-direction: row`):** `[Input field    ] [Button]`
- **Mobile (`flex-direction: column`):** 
  ```
  [Input field          ]
  [Button               ]
  ```

**Try this:** Resize your browser window and watch the layout change at 480px.

**Time:** ~10 minutes

## Layout with CSS Grid

CSS Grid is a two-dimensional layout system for rows and columns together.

### Grid Container

```css
.grid {
  display: grid;
  grid-template-columns: repeat(3, 1fr); /* 3 equal columns */
  grid-template-columns: 200px 1fr 200px; /* fixed-fluid-fixed */
  grid-template-rows: auto 1fr auto; /* header-content-footer */
  gap: 20px;
}
```

### Grid Items

```css
.header {
  grid-column: 1 / -1; /* Span all columns */
}

.sidebar {
  grid-row: 2 / 4; /* Span rows 2 to 4 */
}

/* Named grid areas */
.layout {
  display: grid;
  grid-template-areas:
    "header header header"
    "sidebar main main"
    "footer footer footer";
}

.header { grid-area: header; }
.sidebar { grid-area: sidebar; }
.main { grid-area: main; }
.footer { grid-area: footer; }
```

### Exercise: CSS Grid Layout (Optional)

Grid is great for two-dimensional layouts. Compare it to Flexbox:

**Flexbox (one-dimensional):** Good for rows OR columns
**Grid (two-dimensional):** Good for rows AND columns together

#### Grid Example: Task Dashboard Layout

Imagine expanding your task list into a dashboard:

```css
.dashboard {
  display: grid;
  grid-template-columns: 250px 1fr; /* Sidebar + Main content */
  grid-template-rows: auto 1fr auto; /* Header + Content + Footer */
  gap: 20px;
  min-height: 100vh;
}

.sidebar {
  grid-row: 1 / 4; /* Sidebar spans all 3 rows */
  background: #f5f5f5;
}

.header {
  grid-column: 2; /* Header in second column */
}

.main {
  grid-column: 2; /* Main content in second column */
}

.footer {
  grid-column: 2; /* Footer in second column */
}
```

**Visual result:**
```
┌──────────┬──────────────────┐
│          │     Header       │
│          ├──────────────────┤
│ Sidebar  │                  │
│ (lists,  │      Main        │
│ filters) │    (your tasks)  │
│          │                  │
│          ├──────────────────┤
│          │     Footer       │
└──────────┴──────────────────┘
```

**Key differences from Flexbox:**
- Grid defines both rows AND columns at once
- Items can span multiple rows/columns (`grid-row: 1 / 4`)
- Easier for complex page layouts
- Flexbox is better for single rows (like your input + button)

**For your task list:**
- Keep using **Flexbox** for the input row and individual task items
- Use **Grid** if you later add a sidebar with filters/categories

**Experiment:** Try creating a 3-column grid for task categories:
```css
.task-categories {
  display: grid;
  grid-template-columns: repeat(3, 1fr);
  gap: 15px;
}
```

**Time:** ~10 minutes (optional)

## Positioning

```css
/* Static (default) */
position: static;

/* Relative - positioned relative to its normal position */
position: relative;
top: 10px;
left: 20px;

/* Absolute - positioned relative to nearest positioned ancestor */
position: absolute;
top: 0;
right: 0;

/* Fixed - positioned relative to viewport */
position: fixed;
bottom: 20px;
right: 20px;

/* Sticky - toggles between relative and fixed */
position: sticky;
top: 0;
```

**Z-index for stacking:**

```css
.modal {
  position: fixed;
  z-index: 1000; /* Higher values appear on top */
}
```

### Questions - Positioning

1. What is the difference between `relative` and `absolute` positioning?
2. When would you use `sticky` positioning?
3. What creates a new stacking context?

## Responsive Design

Responsive design ensures your website looks good on all devices.

### Media Queries

```css
/* Mobile first approach */
.container {
  padding: 1rem;
}

/* Tablet */
@media (min-width: 768px) {
  .container {
    padding: 2rem;
    display: grid;
    grid-template-columns: 1fr 1fr;
  }
}

/* Desktop */
@media (min-width: 1024px) {
  .container {
    grid-template-columns: repeat(3, 1fr);
  }
}
```

### Common Breakpoints

- Mobile: < 768px
- Tablet: 768px - 1023px
- Desktop: 1024px+

### Responsive Images

```css
img {
  max-width: 100%;
  height: auto;
}
```

### Exercise: CSS Variables

Replace your hardcoded colors with CSS variables:

```css
:root {
  --primary: #4a90e2;
  --text: #333;
  --completed: #888;
}

/* Use them in your styles */
button { background: var(--primary); }
.completed { color: var(--completed); }
```

**Time:** ~5 minutes

## CSS Variables (Custom Properties)

CSS variables enable reusable values and theming.

```css
:root {
  --primary-color: #007bff;
  --secondary-color: #6c757d;
  --font-size-base: 16px;
  --spacing-unit: 1rem;
}

body {
  font-size: var(--font-size-base);
}

.button-primary {
  background-color: var(--primary-color);
  padding: calc(var(--spacing-unit) / 2) var(--spacing-unit);
}
```

**Scope and inheritance:**

```css
.card {
  --card-padding: 20px;
  padding: var(--card-padding);
}

.card-large {
  --card-padding: 40px; /* Overrides for this element and children */
}
```

## Transitions and Animations

### Transitions

Smooth property changes:

```css
.button {
  background-color: blue;
  transition: background-color 0.3s ease;
}

.button:hover {
  background-color: darkblue;
}
```

**Transition properties:**

- `transition-property` - Which property to animate
- `transition-duration` - How long the animation takes
- `transition-timing-function` - Speed curve (ease, linear, ease-in, ease-out)
- `transition-delay` - Delay before starting

### Animations

```css
@keyframes slideIn {
  from {
    transform: translateX(-100%);
    opacity: 0;
  }
  to {
    transform: translateX(0);
    opacity: 1;
  }
}

.modal {
  animation: slideIn 0.3s ease-out;
}
```

### Exercise: Simple Transition (Optional)

Add a hover transition to your button:

```css
button {
  transition: background-color 0.2s ease;
}

button:hover {
  background-color: darkblue;
}
```

**Time:** ~5 minutes (optional)

## Modern CSS Features

### Container Queries

Style based on container size, not viewport:

```css
.card-container {
  container-type: inline-size;
}

@container (min-width: 400px) {
  .card {
    display: grid;
    grid-template-columns: 200px 1fr;
  }
}
```

### CSS Nesting

```css
.card {
  padding: 1rem;
  
  &:hover {
    box-shadow: 0 4px 8px rgba(0,0,0,0.1);
  }
  
  .title {
    font-size: 1.5rem;
  }
}
```

### Logical Properties

```css
/* Instead of left/right, use inline-start/end */
margin-inline-start: 1rem;

/* Instead of top/bottom, use block-start/end */
padding-block: 1rem;

/* Border radius that works with text direction */
border-start-start-radius: 8px;
```

## Best Practices

- **Mobile first**: Write base styles for mobile, enhance for larger screens
- **Use relative units**: rem for fonts, % or fr for layouts
- **Limit specificity**: Avoid deep nesting and ID selectors
- **Organize with methodology**: BEM, SMACSS, or Atomic CSS
- **Comment complex sections**: Explain why, not what
- **Test in real browsers**: Don't rely solely on DevTools

### BEM Naming Convention

```css
/* Block */
.card { }

/* Element */
.card__title { }
.card__image { }

/* Modifier */
.card--featured { }
.card__title--large { }
```

## Tools & Resources

- [CSS-Tricks](https://css-tricks.com/) - Comprehensive guides and almanac
- [Flexbox Froggy](https://flexboxfroggy.com/) - Learn Flexbox interactively
- [Grid Garden](https://cssgridgarden.com/) - Learn Grid interactively
- [Can I Use](https://caniuse.com/) - Check browser support
- [MDN CSS Reference](https://developer.mozilla.org/en-US/docs/Web/CSS/Reference)
- [Chrome DevTools](https://developer.chrome.com/docs/devtools/css/) - Debug CSS

## SVG and CSS

SVG (Scalable Vector Graphics) is technically part of HTML markup, but we're covering it here because you needed to understand CSS fundamentals first. SVGs are incredibly powerful for creating resolution-independent graphics, icons, and animations.

### Why SVG Matters

SVGs are vector-based, meaning they:
- Scale to any size without losing quality
- Are resolution-independent (perfect for retina displays)
- Can be styled with CSS
- Can be animated with CSS or JavaScript
- Are searchable and accessible
- Have small file sizes for simple graphics

### Learn SVG Basics

Read this excellent introduction to understand how SVGs work:

- [A Friendly Introduction to SVG](https://www.joshwcomeau.com/svg/friendly-introduction-to-svg/) (~20 minutes)

### Questions - SVG Concepts

After reading the article, think about these questions:

1. What is the difference between raster images (PNG, JPG) and vector graphics (SVG)? When would you choose one over the other?
2. How is the SVG coordinate system different from HTML positioning? What is the `viewBox` attribute and why is it important?
3. SVG elements can be styled with CSS properties. Which CSS properties work on SVG elements vs HTML elements? Are there differences?
4. How would you embed an SVG in your HTML? What are the trade-offs between inline SVG vs using an `<img>` tag?
5. Can you use CSS transforms (rotate, scale, translate) on SVG elements? How might this be useful for animations?

### Optional Exercise: Add SVG Icons to Your Task List

Enhance your task list project by replacing text buttons with SVG icons:

**Ideas to implement:**

1. **Delete button icon**: Replace "Delete" text with a trash can or X icon
2. **Add button icon**: Replace "Add" text with a plus (+) icon
3. **Custom checkbox**: Style the checkbox using SVG instead of the default browser styling
4. **Status indicators**: Add colored SVG dots or badges to show task priority
5. **Loading spinner**: Create an animated SVG spinner for async operations

**Challenge yourself:**

- Create the SVG icons from scratch (circles, paths, rectangles)
- Style them with CSS (change color on hover, add transitions)
- Make them responsive (scale with viewport size)
- Try CSS animations (rotate, fade, bounce)

**Hint:** Start simple with basic shapes:

```html
<!-- Simple trash icon example -->
<svg width="24" height="24" viewBox="0 0 24 24" fill="none">
  <rect x="5" y="6" width="14" height="16" stroke="currentColor" stroke-width="2"/>
  <line x1="3" y1="6" x2="21" y2="6" stroke="currentColor" stroke-width="2"/>
  <line x1="10" y1="10" x2="10" y2="18" stroke="currentColor" stroke-width="2"/>
  <line x1="14" y1="10" x2="14" y2="18" stroke="currentColor" stroke-width="2"/>
</svg>
```

**Time:** ~30-60 minutes (optional)

**Why this matters:** Most modern web apps use SVG icons (Font Awesome, Heroicons, Lucide). Understanding how they work gives you the foundation to customize and create your own.

## Worth Knowing (Advanced)

These concepts are worth mentioning but don't learn them now:

- CSS Architecture methodologies (BEM, SMACSS, ITCSS)
- CSS Preprocessors (Sass, Less, Stylus)
- PostCSS and CSS custom processing
- CSS-in-JS solutions
- Web Fonts optimization (font-display, subsetting)
- CSS Houdini (paint API, layout API)
- View Transitions API
- Cascade Layers (@layer)
- SVG animation libraries (GSAP, Anime.js)
- SVG path drawing animations
- SVG filters and effects

## Next steps

You've styled your task list with:
- ✅ **Flexbox** for layout (input row, task alignment)
- ✅ **Media queries** for responsive design
- ✅ Basic visual polish

**Flexbox vs Grid - When to use:**
- **Flexbox**: Single rows or columns (navigation bars, form rows, centering items)
- **Grid**: Complex two-dimensional layouts (page layouts, dashboards, card grids)

Now let's add interactivity with [JavaScript Vanilla](Frontend/javascript-vanilla)!

You'll learn to:
- Add tasks dynamically
- Handle user interactions (clicks, keyboard)
- Store data in the browser
