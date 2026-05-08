<h1 align="Center"> 🎯 DOM Manipulation Cheatsheet</h1>

> :bulb: This is a quick reference for selecting, creating, and manipulating DOM elements with JavaScript.

> :book: Official Docs : **[MDN DOM Reference](https://developer.mozilla.org/en-US/docs/Web/API/Document_Object_Model)**

> :rocket: For study : **[DOM Tutorial](https://www.javascripttutorial.net/javascript-dom/)** , **[W3Schools](https://www.w3schools.com/js/js_htmldom.asp)**

## 📑 Table of Contents

- [1. Selecting Elements](#1-selecting-elements)
  - [Single Element](#single-element)
  - [Multiple Elements](#multiple-elements)
  - [Parent / Child / Sibling](#parent--child--sibling)
- [2. CSS Selectors](#2-css-selectors)
  - [Basic Selectors](#basic-selectors)
  - [Combinators](#combinators)
  - [Pseudo-classes](#pseudo-classes)
  - [Attribute Selectors](#attribute-selectors)
- [3. Content Manipulation](#3-content-manipulation)
  - [Text Content](#text-content)
  - [HTML Content](#html-content)
  - [Attributes](#attributes)
- [4. Creating & Removing Elements](#4-creating--removing-elements)
  - [Create](#create)
  - [Insert](#insert)
  - [Remove](#remove)
  - [Clone](#clone)
- [5. Classes & Styles](#5-classes--styles)
  - [Class Manipulation](#class-manipulation)
  - [Inline Styles](#inline-styles)
  - [Computed Styles](#computed-styles)
- [6. Events](#6-events)
  - [Event Listeners](#event-listeners)
  - [Event Object](#event-object)
  - [Common Events](#common-events)
  - [Delegation](#delegation)
- [7. Traversing the DOM](#7-traversing-the-dom)
- [8. Forms](#8-forms)
- [9. Common Patterns](#9-common-patterns)

---

## 1. Selecting Elements

### Single Element

```js
document.getElementById("myId")           // Fastest: by ID
document.querySelector(".myClass")        // First match: CSS selector
document.querySelector("#myId > p")       // Any valid CSS selector
```

```html
<div id="myId">Element</div>
<script>
  const el = document.getElementById("myId")
  console.log(el) // <div id="myId">Element</div>
</script>
```

> [!NOTE]
> - `getElementById` is fastest (uses internal hash map)
> - `querySelector` supports any CSS selector
> - Returns `null` if no match found

---

### Multiple Elements

```js
document.getElementsByClassName("myClass")   // HTMLCollection (live)
document.getElementsByTagName("div")         // HTMLCollection (live)
document.querySelectorAll(".myClass")        // NodeList (static)
```

```html
<ul>
  <li class="item">Item 1</li>
  <li class="item">Item 2</li>
  <li class="item">Item 3</li>
</ul>
<script>
  const items = document.querySelectorAll(".item")
  items.forEach(item => console.log(item.textContent))
  // Item 1, Item 2, Item 3
</script>
```

> [!NOTE]
> - `getElementsByClassName` / `getElementsByTagName` return **live** collections (auto-update)
> - `querySelectorAll` returns **static** NodeList
> - Use `.forEach()` on NodeList; HTMLCollection needs Array conversion

---

### Parent / Child / Sibling

```js
element.parentElement          // Parent (or null)
element.parentNode             // Parent node (includes text nodes)

element.children               // Child elements (HTMLCollection)
element.childNodes             // All children (includes text nodes)

element.firstElementChild      // First child element
element.lastElementChild       // Last child element

element.previousElementSibling // Previous sibling
element.nextElementSibling      // Next sibling
```

```html
<div class="container">
  <p>First</p>
  <p>Second</p>
</div>
<script>
  const container = document.querySelector(".container")
  console.log(container.children.length)   // 2
  console.log(container.firstElementChild) // <p>First</p>
  console.log(container.lastElementChild)  // <p>Second</p>
</script>
```

---

## 2. CSS Selectors

### Basic Selectors

| Selector | Syntax | Example |
|----------|--------|---------|
| ID | `#id` | `#header` |
| Class | `.class` | `.btn` |
| Tag | `tag` | `div`, `span` |
| Universal | `*` | `*` |
| Multiple | `,` | `div, p, span` |

```js
document.querySelector("#nav")        // ID
document.querySelectorAll(".active")   // Class
document.querySelectorAll("h1, h2, h3") // Multiple tags
```

---

### Combinators

| Combinator | Syntax | Description |
|------------|--------|-------------|
| Descendant | ` ` | Any nested descendant |
| Child | `>` | Direct children only |
| Adjacent Sibling | `+` | Next sibling only |
| General Sibling | `~` | All following siblings |

```html
<div class="wrapper">
  <ul>
    <li><a href="#">Link</a></li>
  </ul>
  <p>Text</p>
</div>
<script>
  // Descendant: any <a> inside .wrapper
  document.querySelectorAll(".wrapper a")

  // Child: only direct <li> children of <ul>
  document.querySelectorAll("ul > li")

  // Adjacent sibling: <p> directly after <ul>
  document.querySelector("ul + p")

  // General sibling: all <p> after <ul>
  document.querySelectorAll("ul ~ p")
</script>
```

---

### Pseudo-classes

```js
document.querySelector("li:first-child")      // First child
document.querySelector("li:last-child")       // Last child
document.querySelector("li:nth-child(2)")     // 2nd child (1-indexed)
document.querySelector("li:nth-child(odd)")   // Odd children
document.querySelector("li:nth-child(even)")  // Even children
document.querySelector("li:nth-child(3n)")    // Every 3rd

document.querySelector(":not(.disabled)")     // Not matching selector
document.querySelector(":not(p)")             // Not <p> tag
document.querySelector("a:hover")            // Hover state (dynamic)

document.querySelector(":empty")             // No children
document.querySelector(":first-of-type")      // First of its type
document.querySelector(":last-of-type")      // Last of its type
```

```html
<ul>
  <li class="item">One</li>
  <li class="item">Two</li>
  <li class="item active">Three</li>
</ul>
<script>
  // Select first item
  document.querySelector("li:first-child") // <li>One</li>

  // Select 2nd item
  document.querySelector("li:nth-child(2)") // <li>Two</li>

  // Select all except .active
  document.querySelectorAll("li:not(.active)") // One, Two
</script>
```

---

### Attribute Selectors

| Syntax | Description |
|--------|-------------|
| `[attr]` | Has attribute |
| `[attr="value"]` | Exact match |
| `[attr*="value"]` | Contains substring |
| `[attr^="value"]` | Starts with |
| `[attr$="value"]` | Ends with |
| `[attr~="value"]` | Contains word (space-separated) |
| `[attr\|="value"]` | Exact or prefix (e.g., "en-US") |

```html
<input type="text" name="username" placeholder="Enter name">
<input type="email" name="email" required>
<input type="checkbox" checked>
<script>
  document.querySelectorAll("[type]")           // All with type attr
  document.querySelectorAll('[name="email"]')  // Exact match
  document.querySelectorAll('[placeholder*="name"]') // Contains "name"
  document.querySelectorAll("[required]")      // Has required
  document.querySelectorAll("[checked]")       // Checked inputs
</script>
```

---

## 3. Content Manipulation

### Text Content

```js
element.textContent          // Get all text (including hidden)
element.innerText            // Get visible text (respects CSS)
element.textContent = "Hi"   // Set text (escapes HTML)
```

```html
<div id="box"><span>Hello</span> World</div>
<script>
  const box = document.getElementById("box")
  console.log(box.textContent)  // "Hello World"
  console.log(box.innerText)    // "Hello World" (rendered)

  box.textContent = "<strong>New</strong> text"
  // Output: <div id="box">&lt;strong&gt;New&lt;/strong&gt; text</div>
</script>
```

> [!NOTE]
> - `textContent` is faster (no CSS parsing)
> - `textContent` gets ALL text including `<script>` and `<style>`
> - Setting `textContent` removes all child nodes

---

### HTML Content

```js
element.innerHTML            // Get HTML content
element.innerHTML = "<p>New</p>" // Set HTML (parses & renders)
element.outerHTML            // Get element + itself as HTML
element.outerHTML = "<div>New</div>" // Replace element itself
```

```html
<div id="container"><p>Old content</p></div>
<script>
  const container = document.getElementById("container")

  console.log(container.innerHTML)  // "<p>Old content</p>"

  container.innerHTML = "<strong>New content</strong>"
  // <div id="container"><strong>New content</strong></div>

  container.outerHTML = "<section>Replaced</section>"
  // The <div> is now completely gone, replaced by <section>
</script>
```

> [!NOTE]
> - Never set `innerHTML` with user input (XSS risk) — use `textContent`
> - `innerHTML` is slower than `textContent` due to parsing

---

### Attributes

```js
element.getAttribute("class")     // Get attribute
element.setAttribute("class", "btn") // Set attribute
element.hasAttribute("disabled")   // Check existence
element.removeAttribute("disabled") // Remove attribute

element.id                         // Direct property access (for common attrs)
element.className                 // Get/set class string
element.src                        // For <img>, <script>, etc.
```

```html
<img id="logo" src="logo.png" alt="Logo" class="responsive">
<script>
  const img = document.getElementById("logo")

  // Using methods
  console.log(img.getAttribute("alt"))  // "Logo"
  img.setAttribute("alt", "Company Logo")

  // Using properties
  console.log(img.className)     // "responsive"
  img.className = "thumbnail"

  // Check/remove
  img.hasAttribute("src")        // true
  img.removeAttribute("alt")
</script>
```

```js
element.dataset              // Access data-* attributes
element.dataset.name = "value" // Set data-name="value"
element.dataset.userId = "123" // data-user-id="123"
```

```html
<div id="user" data-name="John" data-user-id="42"></div>
<script>
  const user = document.getElementById("user")
  console.log(user.dataset.name)    // "John"
  console.log(user.dataset.userId)  // "42"

  user.dataset.role = "admin"
  // Now: data-role="admin"
</script>
```

---

## 4. Creating & Removing Elements

### Create

```js
document.createElement("div")        // Create element
document.createTextNode("Hello")      // Create text node
document.createComment("Comment")    // Create comment
```

```js
const btn = document.createElement("button")
btn.textContent = "Click me"
btn.className = "btn primary"
```

---

### Insert

```js
parent.appendChild(node)              // Add as last child
parent.prepend(node)                  // Add as first child

parent.insertBefore(newNode, refNode)  // Insert before reference
parent.insertAdjacentHTML("beforeend", "<span>Item</span>")
parent.insertAdjacentElement("afterbegin", element)
```

```js
const list = document.getElementById("list")
const newItem = document.createElement("li")
newItem.textContent = "New item"

// appendChild - add to end
list.appendChild(newItem)

// prepend - add to beginning
const first = document.createElement("li")
first.textContent = "First"
list.prepend(first)
```

| Position | HTML inserted |
|----------|---------------|
| `beforebegin` | Before the element |
| `afterbegin` | Inside, before first child |
| `beforeend` | Inside, after last child |
| `afterend` | After the element |

```html
<ul id="list">
  <!-- beforebegin: outside before <ul> -->
  <li>Existing</li>
  <!-- afterbegin: inside, first -->
  <!-- beforeend: inside, last -->
  <!-- afterend: outside after </ul> -->
</ul>
<script>
  const list = document.getElementById("list")
  list.insertAdjacentHTML("beforeend", "<li>Appended</li>")
  list.insertAdjacentHTML("afterbegin", "<li>Prepended</li>")
</script>
```

---

### Remove

```js
parent.removeChild(node)    // Remove child
element.remove()           // Remove element itself (modern)
element.innerHTML = ""      // Clear all children
```

```html
<ul id="list">
  <li>Keep</li>
  <li class="to-delete">Remove</li>
</ul>
<script>
  const item = document.querySelector(".to-delete")
  item.remove()  // Modern: removes element

  // Or older way:
  // item.parentNode.removeChild(item)
</script>
```

---

### Clone

```js
node.cloneNode()            // Clone (shallow - no children)
node.cloneNode(true)        // Deep clone (with all children)
```

```html
<div class="card">
  <h3>Title</h3>
  <p>Content</p>
</div>
<script>
  const original = document.querySelector(".card")

  const shallow = original.cloneNode()      // Only <div class="card">
  const deep = original.cloneNode(true)    // Full copy with children
</script>
```

---

## 5. Classes & Styles

### Class Manipulation

```js
element.classList.add("active")          // Add class
element.classList.remove("active")       // Remove class
element.classList.toggle("active")       // Toggle on/off
element.classList.contains("active")    // Check if has class

element.classList.replace("old", "new")  // Replace class

element.className = "new-classes"       // Set all (overwrites)
```

```html
<button id="btn" class="btn">Click</button>
<script>
  const btn = document.getElementById("btn")

  btn.classList.add("primary", "large")
  // class="btn primary large"

  btn.classList.contains("primary") // true
  btn.classList.toggle("active")    // Added: class="btn primary large active"
  btn.classList.toggle("active")   // Removed: class="btn primary large"

  btn.classList.replace("large", "small")
  // class="btn primary small"
</script>
```

---

### Inline Styles

```js
element.style.color = "red"           // Set inline style
element.style.backgroundColor = "blue" // Use camelCase
element.style.cssText = "color: red; font-size: 16px" // Set multiple
element.style.display                 // Get inline style only
element.style.display = "none"       // Hide element
```

```html
<div id="box" style="color: blue;">Box</div>
<script>
  const box = document.getElementById("box")

  console.log(box.style.color)    // "blue" (inline only)

  box.style.backgroundColor = "#f0f0f0"
  box.style.borderRadius = "8px"
  box.style.display = "none"     // Hide
  setTimeout(() => box.style.display = "block", 1000) // Show after 1s
</script>
```

> [!NOTE]
> - Property names use **camelCase** (e.g., `backgroundColor`, not `background-color`)
> - `style` only reads inline styles, not CSS classes

---

### Computed Styles

```js
window.getComputedStyle(element)           // Get all computed styles
window.getComputedStyle(element).color    // Get computed color
window.getComputedStyle(element).getPropertyValue("color")
```

```html
<div id="box" class="styled">Box</div>
<style>
  .styled { color: blue; font-size: 20px; }
</style>
<script>
  const box = document.getElementById("box")
  const styles = window.getComputedStyle(box)

  console.log(styles.color)        // rgb(0, 0, 255)
  console.log(styles.fontSize)     // 20px
  console.log(styles.display)     // block
</script>
```

---

## 6. Events

### Event Listeners

```js
element.addEventListener("click", handler)     // Add listener
element.removeEventListener("click", handler) // Remove listener

function handler(event) { /* ... */ }
element.addEventListener("click", (e) => { /* ... */ })
```

```html
<button id="btn">Click me</button>
<script>
  const btn = document.getElementById("btn")

  function handleClick(event) {
    console.log("Clicked!", event.target)
  }

  btn.addEventListener("click", handleClick)

  // Later: remove if needed
  btn.removeEventListener("click", handleClick)
</script>
```

> [!NOTE]
> - `addEventListener` allows multiple handlers per event
> - Use named function if you need to remove later
> - Third arg: `{ capture: true }` for capture phase, `{ once: true }` for auto-remove

---

### Event Object

```js
event.target           // Element that triggered event
event.currentTarget    // Element listener is attached to
event.type             // Event type ("click", "submit", etc.)
event.preventDefault() // Stop default behavior
event.stopPropagation() // Stop bubbling
event.stopImmediatePropagation() // Stop + prevent other handlers
```

```html
<form id="form">
  <button type="submit">Submit</button>
</form>
<script>
  document.getElementById("form").addEventListener("submit", (e) => {
    e.preventDefault()           // Stop form submission
    console.log("Submitted!")
  })

  document.querySelector("button").addEventListener("click", (e) => {
    e.stopPropagation()          // Stop event from bubbling up
  })
</script>
```

---

### Common Events

| Category | Events |
|----------|--------|
| Mouse | `click`, `dblclick`, `mousedown`, `mouseup`, `mouseenter`, `mouseleave`, `mousemove`, `mouseover`, `mouseout` |
| Keyboard | `keydown`, `keypress`, `keyup` |
| Form | `submit`, `change`, `input`, `focus`, `blur`, `reset` |
| Window | `load`, `DOMContentLoaded`, `resize`, `scroll`, `unload` |
| Touch | `touchstart`, `touchmove`, `touchend` |

```js
// Mouse events
element.addEventListener("click", handler)
element.addEventListener("mouseenter", handler)  // Mouse enters element
element.addEventListener("mouseleave", handler)  // Mouse leaves element

// Keyboard events
document.addEventListener("keydown", (e) => {
  console.log(e.key)          // "a", "Enter", "ArrowUp"
  console.log(e.code)         // "KeyA", "Enter", "ArrowUp"
  console.log(e.ctrlKey)      // true if Ctrl held
})

// Form events
form.addEventListener("submit", handler)
input.addEventListener("input", (e) => console.log(e.target.value)) // Real-time as user types
input.addEventListener("change", handler) // Fires on blur after value changed

// Focus
input.addEventListener("focus", handler)
input.addEventListener("blur", handler)
```

> [!NOTE]
> - `input` fires on every keystroke/value change (real-time)
> - `change` fires on blur AFTER value was changed (less frequent)
> - Use `input` for instant validation, `change` for final value

```js
// Check if element matches a selector
const btn = document.querySelector("button")
console.log(btn.matches(".primary")) // true/false
console.log(btn.matches("[data-action]")) // true/false
```

---

### Delegation

Attach one listener to parent instead of many on children.

```html
<ul id="menu">
  <li><button>Action 1</button></li>
  <li><button>Action 2</button></li>
  <li><button>Action 3</button></li>
</ul>
<script>
  const menu = document.getElementById("menu")

  // Single listener on parent
  menu.addEventListener("click", (e) => {
    if (e.target.tagName === "BUTTON") {
      console.log("Clicked:", e.target.textContent)
    }
  })

  // Works for dynamically added items too!
</script>
```

> [!NOTE]
> - Use `event.target` to check what was clicked
> - Great for dynamic lists and tables

---

## 7. Traversing the DOM

```js
// Up
element.parentElement        // Nearest element parent
element.closest(".class")    // Nearest ancestor matching selector

// Down
element.querySelector(".item")     // Find descendant
element.querySelectorAll(".items") // Find all descendants

// Same level
element.previousElementSibling
element.nextElementSibling
```

```js
// Scroll element into view
element.scrollIntoView()              // Default: scroll to top of element
element.scrollIntoView({ behavior: "smooth", block: "center" })

// Get element position/size (relative to viewport)
const rect = element.getBoundingClientRect()
console.log(rect.top, rect.bottom, rect.left, rect.right)
console.log(rect.width, rect.height)
console.log(rect.x, rect.y)

// Check if element is in viewport
const isVisible = rect.top >= 0 && rect.left >= 0 &&
                  rect.bottom <= window.innerHeight &&
                  rect.right <= window.innerWidth
```

```html
<div class="container">
  <div class="child"></div>
  <div class="child"></div>
</div>
<script>
  const child = document.querySelector(".child")

  // Move around
  child.parentElement              // <div class="container">
  child.closest(".container")      // Same as above
  child.previousElementSibling    // null (first child)
  child.nextElementSibling        // <div class="child">

  // Find inside
  child.querySelector(".sub")     // Look inside this child
</script>
```

---

## 8. Forms

```js
form.addEventListener("submit", (e) => {
  e.preventDefault()

  const formData = new FormData(e.target)
  const data = Object.fromEntries(formData) // Convert to object

  // Or get individual values
  const name = e.target.elements.name.value
  const email = e.target.elements.email.value

  // Reset form after submit
  e.target.reset()
})
```

```html
<form id="login">
  <input type="text" name="username" required>
  <input type="password" name="password" required>
  <select name="role">
    <option value="user">User</option>
    <option value="admin">Admin</option>
  </select>
  <label><input type="checkbox" name="remember"> Remember</label>
  <button type="submit">Login</button>
</form>
<script>
  document.getElementById("login").addEventListener("submit", (e) => {
    e.preventDefault()
    const formData = new FormData(e.target)
    console.log(formData.get("username"))
    console.log(formData.get("remember")) // "on" if checked
  })
</script>
```

---

## 9. Common Patterns

### Wait for DOM Ready

```js
// Check current state
console.log(document.readyState) // "loading" | "interactive" | "complete"

// DOMContentLoaded: when HTML is parsed (CSS/images may still load)
document.addEventListener("DOMContentLoaded", () => {
  // Safe to query DOM
})

// Load: everything loaded
window.addEventListener("load", () => {
  // Everything including images loaded
})

// Or place script at end of body (simpler)
```

### Toggle Visibility

```js
const toggle = (el) => {
  el.style.display = el.style.display === "none" ? "block" : "none"
}

// Or with class
element.classList.toggle("hidden")
```

```css
.hidden { display: none; }
```

### Add Items to List

```html
<ul id="list"></ul>
<script>
  const items = ["Apple", "Banana", "Cherry"]
  const list = document.getElementById("list")

  items.forEach(item => {
    const li = document.createElement("li")
    li.textContent = item
    list.appendChild(li)
  })
</script>
```

### Handle Multiple Buttons

```html
<div class="actions">
  <button data-action="save">Save</button>
  <button data-action="delete">Delete</button>
  <button data-action="cancel">Cancel</button>
</div>
<script>
  document.querySelector(".actions").addEventListener("click", (e) => {
    if (e.target.matches("button")) {
      const action = e.target.dataset.action
      console.log("Action:", action)
    }
  })
</script>
```

### Debounce / Throttle

```js
// Debounce: wait until user stops typing before acting
function debounce(fn, delay) {
  let timeout
  return (...args) => {
    clearTimeout(timeout)
    timeout = setTimeout(() => fn(...args), delay)
  }
}

// Throttle: limit how often action fires (e.g., scroll, resize)
function throttle(fn, limit) {
  let inThrottle
  return (...args) => {
    if (!inThrottle) {
      fn(...args)
      inThrottle = true
      setTimeout(() => inThrottle = false, limit)
    }
  }
}

// Usage - Debounce (search input)
const handleSearch = debounce((query) => {
  console.log("Searching:", query)
}, 300)
input.addEventListener("input", (e) => handleSearch(e.target.value))

// Usage - Throttle (scroll handler)
const handleScroll = throttle(() => {
  console.log("Scroll position:", window.scrollY)
}, 100)
window.addEventListener("scroll", handleScroll)
```

> [!NOTE]
> - **Debounce**: wait until user stops typing before acting (search, validation)
> - **Throttle**: limit how often action fires (scroll, resize, mousemove)

---

> [!NOTE]
> ✅ **Quick Hints**
>
> - Use `querySelector` / `querySelectorAll` for most selections
> - Prefer `classList` over `className` for class manipulation
> - Use event delegation for dynamic/many elements
> - Sanitize user input before using `innerHTML` (use `textContent`)
> - Store references to elements if used frequently