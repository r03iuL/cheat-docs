<h1 align="center"> 🎨 CSS Crash Course Cheatsheet </h1>

> :rocket: A complete quick reference for mastering **CSS fundamentals and modern styling**.  
> :book: Official Docs: [MDN CSS Guide](https://developer.mozilla.org/en-US/docs/Web/CSS)  
> :tv: Recommended Video: [CSS Crash Course - Traversy Media](https://www.youtube.com/watch?v=yfoY53QXEnI)

---

# 📑 Table of Contents

- [1. CSS Basics and Syntax](#1-css-basics-and-syntax)
  - [What is CSS and How It Works](#what-is-css-and-how-it-works)
  - [Selectors, Properties, and Values](#selectors-properties-and-values)
  - [Inline, Internal, and External CSS](#inline-internal-and-external-css)
  - [Comments and Best Practices](#comments-and-best-practices)
  - [CSS Specificity](#css-specificity)
- [2. Colors, Units and Measurements](#2-colors-units-and-measurements)
  - [Color Systems: HEX, RGB, HSL](#color-systems-hex-rgb-hsl)
  - [Absolute vs Relative Units](#absolute-vs-relative-units)
  - [Opacity and RGBA Transparency](#opacity-and-rgba-transparency)
  - [CSS Variables (Custom Properties)](#css-variables-custom-properties)
- [3. The Box Model](#3-the-box-model)
  - [Content, Padding, Border, Margin](#content-padding-border-margin)
  - [Box-sizing and border-box](#box-sizing-and-border-box)
  - [Display Types](#display-types)
- [4. Typography](#4-typography)
  - [Font Families and Fallbacks](#font-families-and-fallbacks)
  - [Font Weight, Line Height, Letter Spacing](#font-weight-line-height-letter-spacing)
  - [Text Alignment and Decoration](#text-alignment-and-decoration)
  - [@font-face and Google Fonts](#font-face-and-google-fonts)
- [5. Backgrounds and Borders](#5-backgrounds-and-borders)
  - [Background Color, Images, and Gradients](#background-color-images-and-gradients)
  - [Background Position, Repeat, and Size](#background-position-repeat-and-size)
  - [Rounded Corners, Borders, and Shadows](#rounded-corners-borders-and-shadows)
- [6. Layout Fundamentals](#6-layout-fundamentals)
  - [Position Property](#position-property)
  - [Z-index and Stacking](#z-index-and-stacking)
  - [Overflow and Clipping](#overflow-and-clipping)
- [7. Flexbox](#7-flexbox)
  - [Main Axis vs Cross Axis](#main-axis-vs-cross-axis)
  - [justify-content, align-items, align-content](#justify-content-align-items-align-content)
  - [flex-wrap, flex-grow, flex-shrink, flex-basis](#flex-wrap-flex-grow-flex-shrink-flex-basis)
  - [Practical Layouts](#practical-layouts)
- [8. CSS Grid](#8-css-grid)
  - [Grid Container and Items](#grid-container-and-items)
  - [grid-template-columns and rows](#grid-template-columns-and-rows)
  - [gap, fr Units, minmax()](#gap-fr-units-minmax)
  - [Grid Areas and Auto-placement](#grid-areas-and-auto-placement)
- [9. Responsive Design](#9-responsive-design)
  - [Media Queries](#media-queries)
  - [Fluid Layouts with Relative Units](#fluid-layouts-with-relative-units)
  - [Mobile-first Design](#mobile-first-design)
  - [Responsive Utilities](#responsive-utilities)
- [10. Transitions and Animations](#10-transitions-and-animations)
  - [Transition Property](#transition-property)
  - [Transform](#transform)
  - [@keyframes Animations](#keyframes-animations)
  - [Hover, Active, Focus Effects](#hover-active-focus-effects)
- [11. Advanced Styling Tricks](#11-advanced-styling-tricks)
  - [Pseudo-classes](#pseudo-classes)
  - [Pseudo-elements](#pseudo-elements)
  - [Object-fit and Object-position](#object-fit-and-object-position)
  - [CSS Filters and Blend Modes](#css-filters-and-blend-modes)
- [12. CSS Architecture and Reusability](#12-css-architecture-and-reusability)
  - [DRY CSS and BEM](#dry-css-and-bem)
  - [Variables and Utility Classes](#variables-and-utility-classes)
  - [Reset vs Normalize](#reset-vs-normalize)
  - [Modular File Organization](#modular-file-organization)
- [13. Modern Features and Tools](#13-modern-features-and-tools)
  - [clamp(), calc(), aspect-ratio](#clamp-calc-aspect-ratio)
  - [Dark Mode](#dark-mode)
  - [Container Queries](#container-queries)
  - [Custom Scrollbars, Clip-path, Mask-image](#custom-scrollbars-clip-path-mask-image)

---

## 1. CSS Basics and Syntax

### What is CSS and How It Works

CSS (Cascading Style Sheets) controls how HTML elements look on a webpage. It uses selectors and properties to apply styles.

```css
p {
  color: blue;
  font-size: 18px;
}
```

The browser reads these rules and styles all `<p>` elements accordingly.

> :bulb: CSS “cascades” — the last rule applied has the highest priority if specificity is equal.

---

### Selectors, Properties, and Values

Selectors target HTML elements; properties define _what_ to style; values define _how_ to style.

```css
/* Universal selector */
* {
  margin: 0;
  padding: 0;
}

/* Element selector */
h1 {
  color: darkblue;
}

/* Class selector */
.title {
  text-transform: uppercase;
}

/* ID selector */
#main {
  background-color: #f0f0f0;
}
```

---

### Inline, Internal, and External CSS

```html
<!-- Inline -->
<p style="color:red;">Inline styled</p>

<!-- Internal -->
<style>
  p {
    color: blue;
  }
</style>

<!-- External -->
<link rel="stylesheet" href="style.css" />
```

> :bulb: Always prefer **external CSS** for maintainability.

---

### Comments and Best Practices

```css
/* This is a CSS comment */
body {
  background-color: #fff; /* Inline comment */
}
```

---

### CSS Specificity

Specificity determines which CSS rule is applied when multiple selectors match the same element.

```css
/* Specificity: ID > Class > Element */
p { color: black; }       /* Low specificity */
.text { color: blue; }    /* Higher */
#main { color: red; }     /* Highest */

<!-- HTML -->
<p id="main" class="text">Hello</p>
```

In this example, the text will be **red** because the ID selector has the highest specificity.

> :bulb: Inline styles override all external styles, but `!important` can override even those — use it sparingly.

---

## 2. Colors, Units and Measurements

### Color Systems: HEX, RGB, HSL

```css
h1 {
  color: #ff5733; /* HEX */
  color: rgb(255, 87, 51); /* RGB */
  color: hsl(14, 100%, 60%); /* HSL */
}
```

---

### Absolute vs Relative Units

```css
div {
  width: 200px; /* absolute */
  font-size: 1.2em; /* relative to parent */
  margin: 2rem; /* relative to root font size */
}
```

> :bulb: Use relative units for responsive design.

---

### Opacity and RGBA Transparency

```css
.box {
  background-color: rgba(255, 0, 0, 0.5);
}
```

---

### CSS Variables (Custom Properties)

```css
:root {
  --main-color: #007bff;
}
button {
  background: var(--main-color);
}
```

---

## 3. The Box Model

### Content, Padding, Border, Margin

```css
div {
  margin: 20px;
  padding: 10px;
  border: 2px solid black;
}
```

Each element has content, padding, border, and margin areas.

---

### Box-sizing and border-box

```css
* {
  box-sizing: border-box;
}
```

> :bulb: This makes width calculations more predictable.

---

### Display Types

```css
span {
  display: inline;
}
div {
  display: block;
}
img {
  display: inline-block;
}
```

---

## 4. Typography

### Font Families and Fallbacks

```css
body {
  font-family: "Poppins", Arial, sans-serif;
}
```

---

### Font Weight, Line Height, Letter Spacing

```css
h1 {
  font-weight: 700;
  line-height: 1.4;
  letter-spacing: 2px;
}
```

---

### Text Alignment and Decoration

```css
p {
  text-align: center;
  text-decoration: underline;
}
```

---

### @font-face and Google Fonts

```css
@import url("https://fonts.googleapis.com/css2?family=Roboto:wght@400;700&display=swap");
```

---

## 5. Backgrounds and Borders

### Background Color, Images, and Gradients

```css
body {
  background-color: #fafafa;
  background-image: url("image.jpg");
  background: linear-gradient(45deg, #ff9, #f06);
}
```

---

### Background Position, Repeat, and Size

```css
body {
  background-repeat: no-repeat;
  background-position: center;
  background-size: cover;
}
```

---

### Rounded Corners, Borders, and Shadows

```css
.card {
  border-radius: 10px;
  border: 1px solid #ddd;
  box-shadow: 0 4px 8px rgba(0, 0, 0, 0.2);
}
```

---

## 6. Layout Fundamentals

### Position Property

```css
.box {
  position: static;
}
.box1 {
  position: relative;
  top: 10px;
}
.box2 {
  position: absolute;
  left: 50px;
}
.box3 {
  position: fixed;
  bottom: 10px;
}
.box4 {
  position: sticky;
  top: 0;
}
```

---

### Z-index and Stacking

```css
div {
  position: relative;
  z-index: 10;
}
```

---

### Overflow and Clipping

```css
.container {
  overflow: hidden;
}
```

---

## 7. Flexbox

### Main Axis vs Cross Axis

Flexbox arranges items along a **main axis** (row or column).

---

### justify-content, align-items, align-content

```css
.container {
  display: flex;
  justify-content: center;
  align-items: center;
  align-content: space-between;
}
```

---

### flex-wrap, flex-grow, flex-shrink, flex-basis

```css
.container {
  flex-wrap: wrap;
}
.item {
  flex-grow: 1;
  flex-basis: 200px;
}
```

---

### Practical Layouts

```css
nav {
  display: flex;
  justify-content: space-between;
}
```

---

## 8. CSS Grid

### Grid Container and Items

```css
.container {
  display: grid;
  grid-template-columns: 1fr 1fr 1fr;
  gap: 20px;
}
```

---

### grid-template-columns and rows

```css
.container {
  grid-template-rows: 100px 200px;
}
```

---

### gap, fr Units, minmax()

```css
.container {
  gap: 1rem;
  grid-template-columns: repeat(3, minmax(200px, 1fr));
}
```

---

### Grid Areas and Auto-placement

```css
.container {
  grid-template-areas: "header header" "sidebar main";
}
```

---

## 9. Responsive Design

### Media Queries

```css
@media (max-width: 768px) {
  body {
    font-size: 14px;
  }
}
```

---

### Fluid Layouts with Relative Units

```css
.container {
  width: 80%;
}
```

---

### Mobile-first Design

> :bulb: Start styling for small screens, then scale up using `min-width` media queries.

---

### Responsive Utilities

Use dev tools or [Responsively App](https://responsively.app/) for testing.

---

## 10. Transitions and Animations

### Transition Property

```css
button {
  transition: background 0.3s ease;
}
```

---

### Transform

```css
button:hover {
  transform: scale(1.1) rotate(5deg);
}
```

---

### @keyframes Animations

```css
@keyframes slide {
  from {
    transform: translateX(-100%);
  }
  to {
    transform: translateX(0);
  }
}
```

---

### Hover, Active, Focus Effects

```css
a:hover {
  color: red;
}
input:focus {
  border-color: blue;
}
```

---

## 11. Advanced Styling Tricks

### Pseudo-classes

```css
li:nth-child(2) {
  color: green;
}
```

---

### Pseudo-elements

```css
h1::before {
  content: "★ ";
  color: gold;
}
```

---

### Object-fit and Object-position

```css
img {
  object-fit: cover;
  object-position: center;
}
```

---

### CSS Filters and Blend Modes

```css
img {
  filter: grayscale(50%);
  mix-blend-mode: multiply;
}
```

---

## 12. CSS Architecture and Reusability

### DRY CSS and BEM

```css
/* Block__Element--Modifier */
.card__title--large {
  font-size: 2rem;
}
```

---

### Variables and Utility Classes

```css
:root {
  --main-color: #333;
}
.text-center {
  text-align: center;
}
```

---

### Reset vs Normalize

> :bulb: Use `normalize.css` to maintain consistent browser defaults.

---

### Modular File Organization

Split CSS by components: `header.css`, `buttons.css`, `layout.css`.

---

## 13. Modern Features and Tools

### clamp(), calc(), aspect-ratio

```css
div {
  width: clamp(300px, 50%, 1000px);
  aspect-ratio: 16 / 9;
}
```

---

### Dark Mode

```css
@media (prefers-color-scheme: dark) {
  body {
    background: #111;
    color: #eee;
  }
}
```

---

### Container Queries

```css
@container (min-width: 500px) {
  .card {
    flex-direction: row;
  }
}
```

---

### Custom Scrollbars, Clip-path, Mask-image

```css
::-webkit-scrollbar {
  width: 8px;
}
.clip {
  clip-path: circle(50%);
}
.mask {
  mask-image: url(mask.svg);
}
```

---

> :bulb: **Tip:** Practice CSS concepts by designing layouts, animations, and responsive pages to build mastery.
