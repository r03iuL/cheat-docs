<h1 align="Center"> 🧱 HTML Cheatsheet </h1>

> :bulb: This is a quick reference for HTML elements, attributes, and common patterns. **Official Docs : [WHATWG HTML Standard](https://html.spec.whatwg.org/)**

> :rocket: For study : **[MDN HTML Reference](https://developer.mozilla.org/en-US/docs/Web/HTML/Element)** , **[W3School](https://www.w3schools.com/html/)**

## 📑 Table of Contents

- [1. Basics](#1-basics)
  - [Boilerplate](#boilerplate)
  - [CSS](#css)
    - [1. Inline CSS](#1-inline-css)
    - [2. Internal CSS](#2-internal-css)
    - [3. External CSS (✅ Best Practice)](#3-external-css--best-practice)
    - [4. @import (Inside CSS file)](#4-import-inside-css-file)
  - [JavaScript](#javascript)
    - [1. Inline JavaScript](#1-inline-javascript)
    - [2. Internal JavaScript](#2-internal-javascript)
    - [3. External JavaScript (✅ Best Practice)](#3-external-javascript--best-practice)
    - [4. Modern ES Modules](#4-modern-es-modules)
  - [Comments](#comments)
- [2. Text \& Content](#2-text--content)
  - [Headings `<h1>–<h6>`](#headings-h1h6)
  - [Paragraphs `<p>`](#paragraphs-p)
  - [Inline Elements](#inline-elements)
  - [Emphasis \& Text Formatting](#emphasis--text-formatting)
  - [Quotes](#quotes)
  - [Inline Code `<code>`](#inline-code-code)
  - [Preformatted Text `<pre>`](#preformatted-text-pre)
  - [Keyboard Input \& Sample Output](#keyboard-input--sample-output)
- [3. Lists](#3-lists)
  - [Unordered List `<ul>`](#unordered-list-ul)
  - [Ordered List `<ol>`](#ordered-list-ol)
  - [List Item `<li>`](#list-item-li)
  - [Definition List `<dl>`](#definition-list-dl)
- [4. Links \& Navigation](#4-links--navigation)
  - [Anchor `<a>`](#anchor-a)
  - [Link `<link>`](#link-link)
- [5. Media](#5-media)
  - [Images `<img>`](#images-img)
    - [Responsive images (recommended)](#responsive-images-recommended)
    - [Common CSS for images](#common-css-for-images)
  - [Figures `<figure>` + `<figcaption>`](#figures-figure--figcaption)
  - [Audio `<audio>`](#audio-audio)
  - [Video `<video>`](#video-video)
    - [Common CSS for audio/video](#common-css-for-audiovideo)
  - [Iframe `<iframe>`](#iframe-iframe)
  - [Practical “media block” pattern](#practical-media-block-pattern)
- [6. Tables](#6-tables)
  - [Basic Table](#basic-table)
  - [Table Spanning (colspan / rowspan)](#table-spanning-colspan--rowspan)
  - [Common CSS for Tables](#common-css-for-tables)
    - [Responsive usage pattern](#responsive-usage-pattern)
  - [Useful Attributes \& Tips (Quick Reference)](#useful-attributes--tips-quick-reference)
- [7. Forms](#7-forms)
  - [Form Basics](#form-basics)
  - [Common Input Types (Practical Set)](#common-input-types-practical-set)
  - [Textarea \& Select](#textarea--select)
  - [Fieldset \& Legend (Grouping)](#fieldset--legend-grouping)
  - [Useful Attributes (Validation \& UX)](#useful-attributes-validation--ux)
  - [Common CSS for Forms (Layout \& Spacing)](#common-css-for-forms-layout--spacing)
  - [Pattern “Cheat Table” (Validation at a Glance)](#pattern-cheat-table-validation-at-a-glance)
- [8. Semantic \& Structure](#8-semantic--structure)
- [9. Advanced / Modern HTML](#9-advanced--modern-html)
  - [`<details>` + `<summary>` (Disclosure)](#details--summary-disclosure)
  - [`<dialog>` (Native modal)](#dialog-native-modal)
  - [`<progress>` (Task progress)](#progress-task-progress)
  - [`<meter>` (Scalar measurement)](#meter-scalar-measurement)
  - [`<template>` (Deferred DOM)](#template-deferred-dom)
  - [`<canvas>` (2D drawing via JS)](#canvas-2d-drawing-via-js)
  - [`<svg>` (Vector graphics)](#svg-vector-graphics)
- [10. Meta Tags](#10-meta-tags)
  - [Essential Meta Tags](#essential-meta-tags)
  - [Open Graph (Facebook, LinkedIn, etc.)](#open-graph-facebook-linkedin-etc)
  - [Twitter Cards](#twitter-cards)
  - [Performance \& Control](#performance--control)
  - [Social \& App Extras](#social--app-extras)
- [11. Accessibility](#11-accessibility)
- [12. Best Practices](#12-best-practices)

## 1. Basics

### Boilerplate

A minimal, valid **HTML5 page structure** with semantic sections.

```html
<!DOCTYPE html>
<!-- HTML5 doctype -->
<html lang="en">
  <head>
    <meta charset="utf-8" />
    <!-- Character encoding (UTF-8 recommended) -->
    <meta name="viewport" content="width=device-width, initial-scale=1" />
    <!-- Mobile-friendly scaling -->
    <title>Page title</title>
  </head>
  <body>
    <header>Header content</header>
    <main>Main content goes here</main>
    <footer>Footer content</footer>
  </body>
</html>
```

---

### CSS

There are 4 main ways to apply CSS styles to HTML:

#### 1. Inline CSS

Applied directly inside an element using the `style` attribute.  
⚠️ Good for **quick testing only**; not recommended for maintainable projects.

```html
<p style="color: green; font-size: 18px;">This is green text</p>
```

**Output:**

<p style="color: green; font-size: 18px;">This is green text</p>

---

#### 2. Internal CSS

Written inside a `<style>` block in the `<head>`.  
Useful for **small projects** or **single-page demos**.

```html
<head>
  <style>
    p {
      color: blue;
      font-size: 20px;
    }
  </style>
</head>
```

**Output:**

<p style="color: blue; font-size: 20px;">This is blue text</p>

---

#### 3. External CSS (✅ Best Practice)

Linked as a separate `.css` file using `<link>` in the `<head>`.  
Most common in real-world projects (modular, maintainable, cacheable).

```html
<head>
  <link rel="stylesheet" href="styles.css" />
</head>
```

`styles.css` example:

```css
p {
  color: green;
  font-size: 22px;
}
```

---

#### 4. @import (Inside CSS file)

Imports another CSS file inside an existing stylesheet.  
⚠️ Loads **slower** than `<link>`; use only if necessary.

```css
@import url("more-styles.css");

body {
  font-family: Arial, sans-serif;
}
```

---

> [!NOTE]  
> 🔑 **CSS Application Key Points:**
>
> - **Specificity order:** Inline > Internal > External.
> - **Cascade principle:** Later rules override earlier ones if same specificity.
> - **External CSS is preferred** → performance, caching, separation of concerns.
> - **Inline CSS drawbacks:** Hard to maintain, bloated HTML, overrides other rules.
> - **@import vs `<link>`:**
>   - `<link>` loads resources in parallel (faster).
>   - `@import` delays load until the CSS file is fetched (slower).

---

### JavaScript

There are 4 main ways to use JavaScript in HTML:

#### 1. Inline JavaScript

Written directly in element attributes (e.g., `onclick`).  
⚠️ Not recommended (mixes content and logic).

```html
<button onclick="alert('Hello!')">Click Me</button>
```

---

#### 2. Internal JavaScript

Written inside a `<script>` tag in the HTML file.  
Good for **quick experiments** or small projects.

```html
<!DOCTYPE html>
<html>
  <head>
    <title>Internal JS Example</title>
  </head>
  <body>
    <h1>Hello</h1>

    <script>
      // Selects the <h1> and changes its color
      document.querySelector("h1").style.color = "blue";
    </script>
  </body>
</html>
```

---

#### 3. External JavaScript (✅ Best Practice)

Keep JavaScript in a separate `.js` file and link it with `<script src="">`.  
Best for modular, reusable, and maintainable projects.

```html
<!DOCTYPE html>
<html>
  <head>
    <title>External JS Example</title>
    <!-- defer = run after HTML parsing -->
    <script src="app.js" defer></script>
  </head>
  <body>
    <h1>Hello</h1>
  </body>
</html>
```

`app.js`:

```js
document.querySelector("h1").style.color = "green";
```

---

#### 4. Modern ES Modules

Use `type="module"` for cleaner code organization with imports/exports.

```html
<script type="module" src="main.js"></script>
```

`main.js`:

```js
import { greet } from "./utils.js";
greet("World");
```

`utils.js`:

```js
export function greet(name) {
  console.log(`Hello, ${name}!`);
}
```

---

> [!NOTE]  
> 🔑 **Script Usage Key Points:**
>
> - **`defer`** → Loads script after parsing, executes in order. ✅ Best choice.
> - **`async`** → Loads script asynchronously, order not guaranteed (use for ads/analytics).
> - Place `<script>` at end of `<body>` if not using `defer`/`async`.
> - Prefer **external JS** → maintainability, caching, and modular design.
> - Avoid inline event attributes (`onclick`) → use `addEventListener` instead.

---

### Comments

HTML comments are ignored by the browser. Useful for notes, TODOs, or temporarily disabling code.

```html
<!-- This is a comment -->

<!-- 
  Multi-line comment example.
  Useful for section labeling.
-->

<p>This will show on the page</p>
<!-- <p>This is hidden and won’t render</p> -->
```

## 2. Text & Content

HTML provides a variety of tags to structure text content and inline elements. Use semantic tags where possible for better readability, SEO, and accessibility.

### Headings `<h1>–<h6>`

Headings create a **document outline**. Use them hierarchically (`<h1>` for page title, `<h2>` for section headings, etc.).

```html
<h1>Main Page Title</h1>
<!-- Only one <h1> per page is recommended -->
<h2>Section Heading</h2>
<h3>Subsection</h3>
...
<h6>Smallest Heading</h6>
```

---

### Paragraphs `<p>`

Used for blocks of text.

```html
<p>This is a paragraph of text.</p>
```

---

### Inline Elements

```html
<span>Generic inline container</span>
<!-- Use <span> for styling or grouping inline text -->

<br />
<!-- Line break (avoid overuse, prefer CSS margin for spacing) -->

<hr />
<!-- Thematic break / horizontal rule -->
```

---

### Emphasis & Text Formatting

Semantic tags convey meaning; stylistic tags only change appearance. Prefer semantic tags.

```html
<strong>Important</strong>
<!-- Strong emphasis, screen readers stress it -->
<em>Stressed</em>
<!-- Emphasis, screen readers may change tone -->
<mark>Highlighted</mark>
<!-- Highlighted text -->
<small>Fine print</small>
<!-- Side notes, disclaimers -->
<sup>2</sup> and <sub>2</sub>
<!-- Superscript / subscript -->

<b>Bold</b>
<!-- Stylistic bold, no extra meaning -->
<i>Italic</i>
<!-- Stylistic italic -->
<u>Underline</u>
<!-- Underlined (often used for annotations) -->
<del>Deleted</del>
<!-- Represents removed or outdated text -->
<ins>Inserted</ins
><!-- Represents added text -->
```

> [!NOTE]  
> 🔑 Use `<strong>` and `<em>` instead of `<b>` and `<i>` when meaning (importance/emphasis) is intended. Screen readers treat them differently.

---

### Quotes

```html
<blockquote cite="https://example.com">
  Block-level quotation. Can include multiple paragraphs.
</blockquote>

<q>Inline quotation</q>
<!-- For short, inline quotes -->

<cite>Example Author</cite>
<!-- Indicates a work’s title or reference -->
```

Example:

```html
<p>
  As noted in <cite>Example Author</cite>:
  <q>This is an inline quote</q>.
</p>

<p>
  <blockquote cite="https://example.com">
    This is a blockquote example. It can span multiple lines and paragraphs.
  </blockquote>
</p>
```

**OUTPUT:**

<p>
  As noted in <cite>Example Author</cite>: 
  <q>This is an inline quote</q>.
</p>
<p>
  <blockquote cite="https://example.com">
    This is a blockquote example. It can span multiple lines and paragraphs.
  </blockquote>

---

### Inline Code `<code>`

For inline snippets of code or commands.

```html
<p>Use the <code>&lt;section&gt;</code> tag for sections.</p>
```

**OUTPUT:**

<p>Use the <code>&lt;section&gt;</code> tag for sections.</p>

---

### Preformatted Text `<pre>`

Preserves whitespace and line breaks exactly as written.  
Often combined with `<code>` for code blocks.

```html
<pre>
function hello() {
  console.log("Hello World");
}
</pre>
```

**OUTPUT:**

<pre>
function hello() {
  console.log("Hello World");
}
</pre>

---

### Keyboard Input & Sample Output

Use `<kbd>` for keyboard input, `<samp>` for sample program output.

```html
<p>
  To copy: <kbd>Ctrl</kbd> + <kbd>C</kbd>
  <br />
  Output: <samp>Text copied to clipboard</samp>
</p>
```

**OUTPUT:**

<p>
  To copy: <kbd>Ctrl</kbd> + <kbd>C</kbd>
  <br />
  Output: <samp>Text copied to clipboard</samp>
</p>

> [!NOTE]  
> ✅ **Quick Hints:**
>
> - Use semantic tags (`<strong>`, `<em>`, `<cite>`) for accessibility.
> - Avoid using `<br>` for layout spacing—use CSS margins instead.
> - Use `<pre>` for code blocks or ASCII formatting.
> - `<kbd>` and `<samp>` are useful for documentation/tutorials.

## 3. Lists

Lists are used to group related items. There are three main types: unordered, ordered, and definition lists.

### Unordered List `<ul>`

Bullet-point lists.  
Use `type` (deprecated in HTML5, replaced by CSS `list-style-type`).

```html
<!-- Unordered list with default bullets -->
<ul>
  <li>Milk</li>
  <li>Bread</li>
</ul>
```

> [!NOTE]  
> **Common attributes/values:**
>
> - `type` (deprecated) → `disc` (default), `circle`, `square`.
> - Use CSS: `list-style-type: ;` for modern control.
>
> **Common CSS styles with `<ul>`:**
>
> - `list-style-type`:
>   - `disc` (default) → Solid circle.
>   - `circle` → Hollow circle.
>   - `square` → Solid square.
>   - `none` → No bullets (often used for menus).
> - `list-style-position`:
>   - `outside` (default) → Bullets outside text block.
>   - `inside` → Bullets inside text block (aligns with text).
> - `list-style-image: url('icon.png')` → Custom bullet icon.
> - `margin` / `padding` → Often reset with `ul { margin: 0; padding: 0; }` in CSS frameworks.

---

### Ordered List `<ol>`

Numbered lists.  
Supports different numbering styles and start/reversed attributes.

```html
<!-- Ordered list with numbers -->
<ol>
  <li>First</li>
  <li>Second</li>
</ol>

<!-- Ordered list starting at 5 -->
<ol start="5">
  <li>Five</li>
  <li>Six</li>
</ol>

<!-- Ordered list reversed -->
<ol reversed>
  <li>Last</li>
  <li>Second Last</li>
</ol>

<!-- Ordered list with Roman numerals -->
<ol type="I">
  <li>One</li>
  <li>Two</li>
</ol>
```

> [!NOTE]  
> **Common `<ol>` attributes/values:**
>
> - `type` → Numbering style:
>   - `1` → Decimal (default).
>   - `A` → Uppercase letters.
>   - `a` → Lowercase letters.
>   - `I` → Uppercase Roman numerals.
>   - `i` → Lowercase Roman numerals.
> - `start="n"` → Number to start counting from.
> - `reversed` → Counts down instead of up.

---

### List Item `<li>`

Represents an item in `<ul>` or `<ol>`.

```html
<ul>
  <li value="5">Custom start value in ordered list</li>
</ul>
```

> [!NOTE]  
> **Common `<li>` attributes/values:**
>
> - `value="n"` → Overrides numbering for that list item in `<ol>`.

---

### Definition List `<dl>`

Used for key–value pairs (terms and descriptions).

```html
<dl>
  <dt>HTML</dt>
  <!-- Definition term -->
  <dd>HyperText Markup Language</dd>
  <!-- Definition description -->
  <dt>CSS</dt>
  <dd>Cascading Style Sheets</dd>
</dl>
```

**Output:**

  <dl>
    <dt>HTML</dt>
    <dd>HyperText Markup Language</dd>
    <dt>CSS</dt>
    <dd>Cascading Style Sheets</dd>
  </dl>

> [!NOTE]  
> **Tags:**
>
> - `<dl>` → Container for definition list.
> - `<dt>` → Term being defined.
> - `<dd>` → Description/definition of term.

## 4. Links & Navigation

### Anchor `<a>`

Used for hyperlinks, anchors, downloads, and navigation.

```html
<a href="https://example.com">Link</a>
<!-- external link -->

<a href="#section">Anchor link</a>
<!-- link to section on same page -->

<a href="file.pdf" download>Download link</a>
<!-- download file -->
```

> [!NOTE]  
> **Common `<a>` attributes and values**:
>
> - `href="URL/#id"` → Target of the link (absolute URL, relative path, or same-page anchor).
> - `target`
>   - `_self` (default) → Opens in same tab.
>   - `_blank` → Opens in new tab/window.
>   - `_parent` → Opens in parent frame.
>   - `_top` → Opens in full body of window.
> - `rel` (relationship between current and linked doc)
>   - `noopener` → Prevents new tab from accessing `window.opener`.
>   - `noreferrer` → Hides referrer information.
>   - `nofollow` → Tells search engines not to follow link.
> - `download="filename"` → Forces file download, optional custom filename.
> - `title="tooltip text"` → Extra info shown on hover.
> - `type="mime/type"` → Hints media type (e.g., `application/pdf`).

---

### Link `<link>`

Defines relationships between the current document and external resources (commonly stylesheets, icons, preloads).

```html
<!-- Stylesheet -->
<link rel="stylesheet" href="style.css" />

<!-- Favicon -->
<link rel="icon" href="favicon.ico" type="image/x-icon" />

<!-- Preconnect to improve performance -->
<link rel="preconnect" href="https://fonts.googleapis.com" crossorigin />
```

> [!NOTE]  
> **Common `<link>` attributes and values**:
>
> - `rel` (relationship)
>   - `stylesheet` → External CSS file.
>   - `icon` / `shortcut icon` → Favicon.
>   - `preload` → Preload resource (CSS, JS, fonts).
>   - `canonical` → Preferred URL for SEO.
>   - `manifest` → Link to web app manifest.
> - `href="URL"` → Path/URL to resource.
> - `type` → MIME type (e.g., `text/css`, `image/png`, `application/json`).
> - `media` → Apply only if media query matches (e.g., `screen`, `print`, `(max-width:600px)`).
> - `as` → Type of resource being preloaded (e.g., `script`, `style`, `font`, `image`).
> - `sizes` → Icon sizes (e.g., `16x16`, `32x32`, `any`).
> - `crossorigin`
>   - `anonymous` → Default, no credentials.
>   - `use-credentials` → Send cookies/credentials.

## 5. Media

Practical patterns for images, figures, audio/video, and embeds. Prefer **semantic tags**, **descriptive `alt`**, and **responsive sizing**.

### Images `<img>`

```html
<!-- Basic image with intrinsic sizing and lazy loading -->
<img src="/images/hero.jpg"
<!-- required: image URL -->
alt="Snow-capped mountains at sunrise"
<!-- describes purpose/content -->
width="1200" height="800"
<!-- intrinsic dimensions (improves CLS) -->
loading="lazy"
<!-- defer offscreen images -->
decoding="async"
<!-- hint to decode asynchronously -->
/>
```

> [!NOTE]
> **Common `<img>` attributes & values :**
>
> - `src="path.jpg"` → Image URL.
> - `alt="..."` → Text alternative (leave **empty** `alt=""` only for decorative images).
> - `width` / `height` → Intrinsic bitmap size in CSS pixels (prevents layout shift).
> - `loading="lazy|eager"` → Native lazy-loading; `lazy` for below-the-fold.
> - `decoding="async|sync|auto"` → Rendering hint; `async` is usually best.
> - `referrerpolicy="no-referrer|origin|strict-origin-when-cross-origin"` → Control Referer header.
> - `fetchpriority="high|low"` → Hint to prioritize critical hero images.

#### Responsive images (recommended)

```html
<!-- Serve optimal size per viewport; browser picks the best candidate -->
<img
  src="/images/card-800.jpg"
  srcset="
    /images/card-400.jpg   400w,
    /images/card-800.jpg   800w,
    /images/card-1200.jpg 1200w
  "
  sizes="(max-width: 600px) 90vw, 600px"
  <!--
  layout
  width
  per
  media
  query
  --
/>

layout hint -- /> alt="Product card on a dark background" width="800"
height="600" loading="lazy" />
```

> [!NOTE]
>
> - `srcset` lists width-based candidates (use real rendered widths).
> - `sizes` tells the browser how wide the image will render (per media query), so it can pick a candidate **before** layout.

#### Common CSS for images

```css
/* Keep images from overflowing their container */
img {
  max-width: 100%;
  height: auto; /* maintain aspect ratio */
  display: block; /* remove inline-gap; easier spacing control */
}

/* Crop behavior for fixed containers (e.g., cards, avatars) */
.image-cover {
  width: 100%;
  aspect-ratio: 16 / 9; /* modern, avoids layout shift */
  object-fit: cover; /* crop while covering container */
  object-position: center;
}
```

---

### Figures `<figure>` + `<figcaption>`

```html
<figure class="figure">
  <img
    src="/photos/lake.jpg"
    alt="Canoe on a calm lake with pine trees in the background"
    width="1200"
    height="800"
    loading="lazy"
  />
  <figcaption>Morning paddle at Emerald Lake — July 2025</figcaption>
</figure>
```

```css
.figure {
  margin: 1.25rem 0;
  text-align: center;
}
.figure img {
  border-radius: 8px;
}
.figure figcaption {
  font-size: 0.9rem;
  color: #666;
  margin-top: 0.5rem;
}
```

> [!NOTE]
> Use `<figure>` when an image and its caption form a single referenceable unit (charts, photos, code screenshots).

---

### Audio `<audio>`

```html
<audio
  controls                <!-- show play/pause UI -->
  preload="metadata"      <!-- fetch only metadata by default -->
>
  <source src="/media/podcast-ep1.mp3" type="audio/mpeg" />
  <source src="/media/podcast-ep1.ogg" type="audio/ogg" />
  <!-- Fallback text -->
  Your browser does not support the <code>audio</code> element.
</audio>
```

> [!NOTE]
> **Common `<audio>` attributes:**
>
> - `controls` → Built-in player UI.
> - `autoplay` → Start automatically (must usually be `muted` to work on mobile).
> - `muted` / `loop` → Start muted / loop playback.
> - `preload="none|metadata|auto"` → How much to prefetch before play.
> - `src` can be used directly, but `<source>` lets multiple formats.

---

### Video `<video>`

```html
<video controls width="640" height="360" <!-- intrinsic size helps layout -->
  poster="/media/teaser.jpg"
  <!-- placeholder frame before play -->
  preload="metadata" playsinline
  <!-- avoid auto-fullscreen on iOS -->
  >
  <source src="/media/trailer-1080.mp4" type="video/mp4" />
  <track
    kind="captions"
    src="/media/trailer.en.vtt"
    srclang="en"
    label="English"
    default
  />
  <!-- Additional <source> for WebM, AV1, etc. if available -->
  Sorry, your browser does not support the <code>video</code> tag.
</video>
```

> [!NOTE]
> **Common `<video>` attributes**
>
> - `controls`, `autoplay` (often requires `muted`), `muted`, `loop`, `playsinline`.
> - `poster="cover.jpg"` → Static image before playing.
> - `preload="none|metadata|auto"` → Fetch amount before play.
> - Add `<track kind="captions" ...>` for **accessibility** (VTT captions/subtitles).

#### Common CSS for audio/video

```css
video,
audio {
  max-width: 100%;
  display: block;
}
.video-cover {
  width: 100%;
  aspect-ratio: 16 / 9;
  background: #000;
}
```

---

### Iframe `<iframe>`

```html
<iframe
  src="https://www.youtube.com/embed/dQw4w9WgXcQ"
  title="YouTube video player"
  <!--
  accessible
  title
  --
>
  width="560" height="315" loading="lazy"
  <!-- defer offscreen iframes -->
  referrerpolicy="strict-origin-when-cross-origin" allow="accelerometer;
  autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture;
  web-share" allowfullscreen sandbox="allow-scripts allow-same-origin
  allow-presentation" ></iframe
>
```

> [!NOTE] > **Security & performance for `<iframe>` :**
>
> - `loading="lazy"` reduces initial load.
> - `sandbox="..."` restricts capabilities; add only what you need (`allow-forms`, `allow-scripts`, `allow-same-origin`, etc.).
> - `referrerpolicy` controls Referer header for privacy.
> - `allowfullscreen` and `allow="..."` enable specific features (e.g., PiP, autoplay).

---

### Practical “media block” pattern

```html
<figure class="media-block">
  <img
    src="/gallery/panorama-1200.jpg"
    srcset="/gallery/panorama-800.jpg 800w, /gallery/panorama-1200.jpg 1200w"
    sizes="(max-width: 768px) 92vw, 720px"
    alt="Panoramic skyline at dusk"
    width="1200"
    height="600"
    loading="lazy"
    class="image-cover"
  />
  <figcaption>City skyline at blue hour — shot on 35 mm.</figcaption>
</figure>
```

```css
.media-block {
  margin: 1.5rem 0;
}
.media-block .image-cover {
  width: 100%;
  aspect-ratio: 2 / 1;
  object-fit: cover;
  border-radius: 10px;
}
.media-block figcaption {
  text-align: center;
  color: #6b7280;
  font-size: 0.9rem;
  margin-top: 0.5rem;
}
```

> [!NOTE]
> ✅ **Quick Hints**
>
> - Always include **descriptive `alt`** (or `alt=""` if purely decorative).
> - Provide **intrinsic `width`/`height`** to prevent layout shift (CLS).
> - Use **`srcset` + `sizes`** for responsive images; serve the smallest acceptable asset.
> - Add **`track`** captions for videos for accessibility & SEO.
> - For embeds, apply **`loading="lazy"`**, **`sandbox`**, and **narrow `allow`** permissions for safety and performance.

---

## 6. Tables

Use semantic structure for data: `caption` (title), `thead` (column headers), `tbody` (rows), `tfoot` (summary).  
Add accessibility with `scope` on headers and meaningful captions.

### Basic Table

```html
<table>
  <caption>
    Sample Table
  </caption>
  <!-- Title for assistive tech & context -->
  <thead>
    <tr>
      <th scope="col">Header 1</th>
      <!-- scope ties header to column -->
      <th scope="col">Header 2</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th scope="row">Row 1</th>
      <!-- row header for accessibility -->
      <td>Data</td>
    </tr>
    <tr>
      <th scope="row">Row 2</th>
      <td>More data</td>
    </tr>
  </tbody>
  <tfoot>
    <tr>
      <td colspan="2">Footer</td>
      <!-- summary/total notes -->
    </tr>
  </tfoot>
</table>
```

<details>
  <summary><strong>Preview: Basic Table</strong></summary>

  <table>
    <caption>Sample Table</caption>
    <thead>
      <tr>
        <th scope="col">Header 1</th>
        <th scope="col">Header 2</th>
      </tr>
    </thead>
    <tbody>
      <tr>
        <th scope="row">Row 1</th>
        <td>Data</td>
      </tr>
      <tr>
        <th scope="row">Row 2</th>
        <td>More data</td>
      </tr>
    </tbody>
    <tfoot>
      <tr>
        <td colspan="2">Footer</td>
      </tr>
    </tfoot>
  </table>
</details>

> [!NOTE]
>
> - **`scope="col|row"`** on `<th>` improves screen reader navigation.
> - Use `<caption>` for a concise table title (appears visually above by default).
> - For **complex tables** (multi-level headers), consider `headers`/`id` pairing for explicit associations.

---

### Table Spanning (colspan / rowspan)

```html
<table>
  <caption>
    Inventory Snapshot
  </caption>
  <thead>
    <tr>
      <th scope="col">Category</th>
      <th scope="col" colspan="2">Stock</th>
      <!-- colspan across two cols -->
    </tr>
    <tr>
      <th scope="col">Item</th>
      <th scope="col">In</th>
      <th scope="col">Out</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th scope="row" rowspan="2">Laptops</th>
      <!-- rowspan across two rows -->
      <td>25</td>
      <td>10</td>
    </tr>
    <tr>
      <td>18</td>
      <td>5</td>
    </tr>
    <tr>
      <th scope="row">Monitors</th>
      <td colspan="2">Bulk order pending</td>
      <!-- merge note across two cols -->
    </tr>
  </tbody>
</table>
```

<details>
  <summary><strong>Preview: Spanning Example</strong></summary>

  <table>
    <caption>Inventory Snapshot</caption>
    <thead>
      <tr>
        <th scope="col">Category</th>
        <th scope="col" colspan="2">Stock</th>
      </tr>
      <tr>
        <th scope="col">Item</th>
        <th scope="col">In</th>
        <th scope="col">Out</th>
      </tr>
    </thead>
    <tbody>
      <tr>
        <th scope="row" rowspan="2">Laptops</th>
        <td>25</td>
        <td>10</td>
      </tr>
      <tr>
        <td>18</td>
        <td>5</td>
      </tr>
      <tr>
        <th scope="row">Monitors</th>
        <td colspan="2">Bulk order pending</td>
      </tr>
    </tbody>
  </table>
</details>

> [!NOTE]
>
> - `colspan="n"` merges **columns**; `rowspan="n"` merges **rows**.
> - Keep spanning minimal—overuse reduces readability and accessibility.

---

### Common CSS for Tables

```css
/* Base table styling */
table {
  width: 100%;
  border-collapse: collapse; /* merge borders; cleaner lines */
  table-layout: auto; /* use 'fixed' for uniform column widths */
}

caption {
  caption-side: top; /* 'bottom' if you prefer below the table */
  font-weight: 600;
  padding: 0.5rem 0;
}

th,
td {
  border: 1px solid #e5e7eb; /* subtle border */
  padding: 0.5rem 0.75rem;
  text-align: left; /* align numbers right: td.num { text-align: right; } */
  vertical-align: middle;
}

thead th {
  background: #f3f4f6; /* header background */
}

tbody tr:nth-child(odd) {
  background: #fafafa; /* zebra striping for readability */
}

tfoot td {
  font-weight: 600;
  background: #f9fafb;
}

/* Responsive wrapper: horizontal scroll on small screens */
.table-wrap {
  overflow-x: auto;
}
```

#### Responsive usage pattern

```html
<div class="table-wrap">
  <table>
    <!-- ... table content ... -->
  </table>
</div>
```

> [!NOTE]
>
> - `border-collapse: collapse;` + borders on `th, td` is the most common clean look.
> - Use `table-layout: fixed;` when columns should split space evenly (set `width` on columns if needed).
> - Wrap table in a **scroll container** for small screens instead of squashing columns.

---

### Useful Attributes & Tips (Quick Reference)

- `<th abbr="Q1">Quarter 1</th>` → `abbr` provides a short header label for screen readers.
- `<td headers="h-qty h-price">` with `<th id="h-qty">Qty</th>` → explicit header mapping (complex tables).
- Avoid empty cells; use `—` or `0` if appropriate to clarify meaning.

## 7. Forms

Well-structured forms pair **labels** with **controls**, use the right **types/attributes** for built-in validation, and apply small, consistent CSS for layout and spacing.

### Form Basics

```html
<form action="/submit" method="post" autocomplete="on">
  <!-- Label 'for' must match input 'id' for accessibility -->
  <label for="name">Name:</label>
  <input id="name" name="name" type="text" required />

  <button type="submit">Send</button>
</form>
```

<details>
  <summary><strong>Preview: Basic Form</strong></summary>

  <form action="/submit" method="post" autocomplete="on">
    <label for="name">Name:</label>
    <input id="name" name="name" type="text" required />
    <button type="submit">Send</button>
  </form>
</details>

> [!NOTE]
>
> - `method="get"` appends query params (OK for searches).
> - `method="post"` sends in request body (use for create/update).
> - `autocomplete="on|off"` controls browser autofill.
> - Use one **submit** button with `type="submit"`; others can be `type="button"`,`type="reset"`etc.

---

### Common Input Types (Practical Set)

```html
<input type="text" placeholder="Full name" required />

<input type="password" minlength="8" placeholder="Min 8 chars" />

<input type="email" placeholder="name@example.com" required />

<!-- min, max, step provide numeric constraints -->
<input type="number" min="0" max="100" step="5" placeholder="0–100" />

<input type="date" min="2025-01-01" max="2025-12-31" />

<!-- Accept only images; allow selecting multiple files -->
<input type="file" accept="image/*" multiple />

<!-- Boolean choices -->
<label><input type="checkbox" name="tos" required /> I agree</label>

<!-- Single choice from a group (same name) -->
<label><input type="radio" name="plan" value="basic" /> Basic</label>
<label><input type="radio" name="plan" value="pro" /> Pro</label>
```

<details>
  <summary><strong>Preview: Inputs</strong></summary>

  <p><input type="text" placeholder="Full name" required /></p>
  <p><input type="password" minlength="8" placeholder="Min 8 chars" /></p>
  <p><input type="email" placeholder="name@example.com" required /></p>
  <p><input type="number" min="0" max="100" step="5" placeholder="0–100" /></p>
  <p><input type="date" min="2025-01-01" max="2025-12-31" /></p>
  <p><input type="file" accept="image/*" multiple /></p>
  <p><label><input type="checkbox" name="tos" required /> I agree</label></p>
  <p>
    <label><input type="radio" name="plan" value="basic" /> Basic</label>
    <label><input type="radio" name="plan" value="pro" /> Pro</label>
  </p>
</details>

> [!NOTE]
>
> - For **radio groups**, all inputs share the same `name`.
> - `accept="image/*,.pdf ,"` filters selectable files.
> - Use `minlength`, `maxlength`, `min`, `max`, and `step` for quick built-in validation.

---

### Textarea & Select

```html
<!-- Use label + id for accessibility -->
<label for="bio">Short bio</label>
<textarea
  id="bio"
  name="bio"
  rows="4"
  maxlength="200"
  placeholder="About you (max 200 chars)"
></textarea>

<label for="country">Country</label>
<select id="country" name="country" required>
  <option value="">Select…</option>
  <!-- empty first option forces a choice -->
  <option>Bangladesh</option>
  <option>Denmark</option>
</select>

<!-- Multi-select -->
<label for="skills">Skills</label>
<select id="skills" name="skills" multiple size="3">
  <option>HTML</option>
  <option>CSS</option>
  <option>JavaScript</option>
</select>
```

<details>
  <summary><strong>Preview: Textarea & Select</strong></summary>

  <p>
    <label for="bio">Short bio</label><br/>
    <textarea id="bio" name="bio" rows="4" maxlength="200" placeholder="About you (max 200 chars)"></textarea>
  </p>
  <p>
    <label for="country">Country</label><br/>
    <select id="country" name="country" required>
      <option value="">Select…</option>
      <option>Bangladesh</option>
      <option>Denmark</option>
    </select>
  </p>
  <p>
    <label for="skills">Skills</label><br/>
    <select id="skills" name="skills" multiple size="3">
      <option>HTML</option>
      <option>CSS</option>
      <option>JavaScript</option>
    </select>
  </p>
</details>

---

### Fieldset & Legend (Grouping)

```html
<fieldset>
  <legend>Newsletter Frequency</legend>
  <label><input type="radio" name="freq" value="daily" /> Daily</label>
  <label><input type="radio" name="freq" value="weekly" /> Weekly</label>
  <label><input type="radio" name="freq" value="monthly" /> Monthly</label>
</fieldset>
```

<details>
  <summary><strong>Preview: Fieldset</strong></summary>

  <fieldset>
    <legend>Newsletter Frequency</legend>
    <label><input type="radio" name="freq" value="daily" /> Daily</label>
    <label><input type="radio" name="freq" value="weekly" /> Weekly</label>
    <label><input type="radio" name="freq" value="monthly" /> Monthly</label>
  </fieldset>
</details>

> [!NOTE]
> Use `<fieldset>` + `<legend>` to give context to grouped controls—especially helpful for screen reader users.

---

### Useful Attributes (Validation & UX)

```html
<!-- Placeholder & required -->
<input placeholder="Hint" required />

<!-- Readonly vs Disabled -->
<input readonly value="Read only" />
<input disabled value="Disabled" />

<!-- Pattern with title message -->
<input pattern="[A-Za-z]+" title="Letters only (A–Z or a–z)" />

<!-- Numeric constraints -->
<input type="number" min="1" max="10" step="1" />

<!-- Autocomplete control -->
<input type="email" autocomplete="email" />

<!-- Spellcheck and autocap (mobile) -->
<input type="text" spellcheck="true" autocapitalize="sentences" />

<!-- Form-level controls -->
<form action="/upload" method="post" enctype="multipart/form-data" novalidate>
  <!-- enctype required for file uploads -->
  <input type="file" name="avatar" accept="image/*" />
  <button type="submit">Upload</button>
</form>
```

<details>
  <summary><strong>Preview: Useful Attributes</strong></summary>

  <p><input placeholder="Hint" required /></p>
  <p><input readonly value="Read only" /></p>
  <p><input disabled value="Disabled" /></p>
  <p><input pattern="[A-Za-z]+" title="Letters only (A–Z or a–z)" /></p>
  <p><input type="number" min="1" max="10" step="1" /></p>
  <p><input type="email" autocomplete="email" placeholder="name@example.com" /></p>
</details>

> [!NOTE]
>
> - **Form** attributes:
>   - `enctype="multipart/form-data"` for file uploads.
>   - `novalidate` disables browser validation (you’ll handle it yourself).
> - **Control** attributes:
>   - `required`, `min`, `max`, `step`, `minlength`, `maxlength`, `pattern`, `title`.
>   - `readonly` = included in submission; `disabled` = **excluded** from submission.

---

### Common CSS for Forms (Layout & Spacing)

```css
/* Vertical form layout with consistent spacing */
.form {
  display: grid;
  gap: 0.75rem; /* space between rows */
  max-width: 480px;
}

.form label {
  font-weight: 600;
}

.form input,
.form select,
.form textarea,
.form button {
  padding: 0.55rem 0.7rem;
  border: 1px solid #d1d5db;
  border-radius: 6px;
  font: inherit;
}

.form input:focus,
.form select:focus,
.form textarea:focus {
  outline: none;
  border-color: #2563eb; /* focus ring color */
  box-shadow: 0 0 0 3px rgba(37, 99, 235, 0.2);
}

.form .inline {
  display: flex;
  gap: 1rem; /* for side-by-side fields */
}
```

```html
<form class="form" action="/contact" method="post">
  <label for="email">Email</label>
  <input id="email" type="email" placeholder="name@example.com" required />

  <div class="inline">
    <div>
      <label for="min">Min</label>
      <input id="min" type="number" min="0" max="10" />
    </div>
    <div>
      <label for="max">Max</label>
      <input id="max" type="number" min="0" max="10" />
    </div>
  </div>

  <label for="msg">Message</label>
  <textarea id="msg" rows="4" placeholder="Your message…"></textarea>

  <button type="submit">Send</button>
</form>
```

<details>
  <summary><strong>Preview: Styled Form</strong></summary>

  <style>
    .form{display:grid;gap:.75rem;max-width:480px}
    .form label{font-weight:600}
    .form input,.form select,.form textarea,.form button{padding:.55rem .7rem;border:1px solid #d1d5db;border-radius:6px;font:inherit}
    .form input:focus,.form select:focus,.form textarea:focus{outline:none;border-color:#2563eb;box-shadow:0 0 0 3px rgba(37,99,235,.2)}
    .form .inline{display:flex;gap:1rem}
  </style>

  <form class="form" action="/contact" method="post">
    <label for="email-pv">Email</label>
    <input id="email-pv" type="email" placeholder="name@example.com" required />

    <div class="inline">
      <div>
        <label for="min-pv">Min</label>
        <input id="min-pv" type="number" min="0" max="10" />
      </div>
      <div>
        <label for="max-pv">Max</label>
        <input id="max-pv" type="number" min="0" max="10" />
      </div>
    </div>

    <label for="msg-pv">Message</label>
    <textarea id="msg-pv" rows="4" placeholder="Your message…"></textarea>

    <button type="submit">Send</button>

  </form>
</details>

---

### Pattern “Cheat Table” (Validation at a Glance)

| Attribute                 | Applies To                  | Purpose                           | Common Values / Examples                |
| ------------------------- | --------------------------- | --------------------------------- | --------------------------------------- |
| `required`                | Most controls               | Disallow empty submission         | `required`                              |
| `min` / `max`             | `number`, `date`, `range`   | Constrain value range             | `min="1" max="10"`                      |
| `step`                    | `number`, `range`           | Increment step                    | `step="0.01"`                           |
| `minlength` / `maxlength` | `text`, `password`, `email` | Constrain length                  | `minlength="8" maxlength="64"`          |
| `pattern`                 | `text`, `search`, etc.      | Regex validation                  | `pattern="^[A-Za-z]{3,}$"`              |
| `title`                   | Most                        | Friendly hint for invalid pattern | `title="Letters only, min 3"`           |
| `autocomplete`            | Most                        | Autofill hint                     | `email`, `name`, `tel`, `one-time-code` |
| `enctype` (form)          | `<form>`                    | Encoding                          | `multipart/form-data` (files)           |

> [!NOTE]
> Keep client-side validation **simple**. Always **re-validate on the server** for security and correctness.

## 8. Semantic & Structure

Use **landmark elements** to describe page regions for SEO, accessibility, and maintainability. Prefer semantic tags to generic `<div>`s; use `<span>` for inline grouping.

```html
<header>Header (site or section header)</header>
<nav>Primary navigation</nav>
<main>Main content (unique per page)</main>
<section>Logical section of content</section>
<article>Self-contained piece (e.g., blog post)</article>
<aside>Sidebar / complementary content</aside>
<footer>Footer (site or section footer)</footer>

<div>Generic block (use when no semantic fits)</div>
<span>Generic inline (for styling text fragments)</span>

<address>
  Contact: Example Inc., 123 Road, City —
  <a href="mailto:hi@example.com">hi@example.com</a>
</address>

<time datetime="2025-09-30">Sept 30, 2025</time>
<!-- datetime must be machine-readable: YYYY-MM-DD or full ISO8601 -->
```

> [!NOTE]
>
> - `<main>` should appear **once** per page and **not** be nested.
> - Use `<section>` with a **heading** (`<h2>` etc.) for proper document outline.
> - `<article>` is portable content that could stand alone in feeds/search.
> - `<address>` is for **contact info of the nearest article/author/site**, not arbitrary addresses.
> - `<time datetime="...">` improves machine-readability for events, articles, and structured data.

<details>
  <summary><strong>Preview: Semantic Landmarks</strong></summary>

  <style>
    header, nav, main, section, article, aside, footer {padding:.75rem;border:1px dashed #e5e7eb;margin:.5rem 0}
  </style>
  <header>Header</header>
  <nav>Navigation</nav>
  <main>Main content</main>
  <section>
    <h2>Section</h2>
    <article>
      <h3>Article</h3>
      <p>Self-contained content.</p>
    </article>
  </section>
  <aside>Sidebar</aside>
  <footer>Footer</footer>
  <address>Contact: Example Inc., 123 Road — <a href="mailto:hi@example.com">hi@example.com</a></address>
  <p>Published: <time datetime="2025-09-30">Sept 30, 2025</time></p>
</details>

---

## 9. Advanced / Modern HTML

### `<details>` + `<summary>` (Disclosure)

```html
<details>
  <summary>Click to expand FAQ</summary>
  <p>This is the hidden answer that appears when expanded.</p>
</details>
```

> [!NOTE]
>
> - Keyboard accessible by default.
> - Use `open` attribute to render expanded initially: `<details open>…</details>`.

---

### `<dialog>` (Native modal)

```html
<!-- Dialog element (needs JS for toggling in practice) -->
<dialog id="infoDialog" aria-labelledby="dlg-title">
  <h2 id="dlg-title">About this page</h2>
  <p>Hello! I’m a native modal dialog.</p>
  <form method="dialog">
    <button value="close">Close</button>
  </form>
</dialog>

<button type="button" id="openBtn">Open Dialog</button>

<script>
  const dlg = document.getElementById("infoDialog");
  const btn = document.getElementById("openBtn");
  btn.addEventListener("click", () => dlg.showModal());
  dlg.addEventListener("close", () => console.log("Dialog closed"));
</script>
```

> [!NOTE]
>
> - Use **`.showModal()`** for modal behavior (traps focus), `.show()` for non-modal.
> - Provide an **accessible title** via `aria-labelledby` or a heading inside the dialog.
> - Always offer a **Close** button and support **Esc** to close.

---

### `<progress>` (Task progress)

```html
<label for="file">File upload:</label>
<progress id="file" value="70" max="100">70%</progress>
```

> [!NOTE]
>
> - `value` and `max` determine the bar fill (0..max).
> - When `value` is **missing**, progress is **indeterminate** (spinner-like).

**OUTPUT:**
<label for="file">File upload:</label>
<progress id="file" value="70" max="100">70%</progress>

---

### `<meter>` (Scalar measurement)

```html
<label for="disk">Disk usage:</label>
<meter id="disk" min="0" max="1" low="0.3" high="0.8" optimum="0.2" value="0.6">
  60%
</meter>
```

> [!NOTE]
>
> - Use for known-range values (scores, battery).
> - `low`, `high`, `optimum` help user agents choose coloring/semantics.

**OUTPUT:**
<label for="disk">Disk usage:</label>
<meter id="disk" min="0" max="1" low="0.3" high="0.8" optimum="0.2" value="0.6">
60%
</meter>

---

### `<template>` (Deferred DOM)

```html
<template id="cardTemplate">
  <article class="card">
    <h3>Card title</h3>
    <p>This card was cloned from a template.</p>
  </article>
</template>

<script>
  const tpl = document.getElementById("cardTemplate");
  const clone = tpl.content.cloneNode(true); // deep clone fragment
  document.body.appendChild(clone); // inject into DOM
</script>
```

> [!NOTE]
> Content inside `<template>` is inert (not rendered, scripts don’t run) until cloned with JS.

---

### `<canvas>` (2D drawing via JS)

```html
<canvas
  id="canvas"
  width="200"
  height="100"
  style="border:1px solid #000;"
></canvas>
<script>
  const ctx = document.getElementById("canvas").getContext("2d");
  ctx.fillStyle = "green";
  ctx.fillRect(20, 20, 150, 50);
</script>
```

> [!NOTE]
>
> - Use `width`/`height` **attributes**, not just CSS, to set drawing resolution.
> - For HiDPI/Retina, scale by `devicePixelRatio`.

---

### `<svg>` (Vector graphics)

```html
<svg
  viewBox="0 0 120 120"
  width="120"
  height="120"
  role="img"
  aria-label="Red circle with text SVG"
>
  <circle cx="60" cy="60" r="50" stroke="black" stroke-width="2" fill="red" />
  <text x="60" y="65" font-size="18" text-anchor="middle" fill="white">
    SVG
  </text>
</svg>
```

> [!NOTE]
>
> - Prefer **inline SVG** for styling via CSS and accessibility labels.
> - Use `viewBox` for scalable, responsive vectors.

---

## 10. Meta Tags

Meta tags provide **metadata** about a page (encoding, viewport, SEO, social sharing, performance).  
They go inside the `<head>` and never appear in the visual content.

### Essential Meta Tags

```html
<!-- Character encoding -->
<meta charset="utf-8" />

<!-- Mobile responsiveness -->
<meta name="viewport" content="width=device-width, initial-scale=1" />

<!-- SEO description (≤ 155 characters) -->
<meta name="description" content="Concise page summary goes here." />

<!-- Keywords (deprecated, most search engines ignore) -->
<meta name="keywords" content="html, cheat sheet, tutorial" />

<!-- Author info -->
<meta name="author" content="John Doe" />

<!-- Favicon & app icons -->
<link rel="icon" href="/favicon.ico" sizes="any" />
<link rel="icon" href="/icon.svg" type="image/svg+xml" />
<link rel="apple-touch-icon" href="/apple-touch-icon.png" />

<!-- Canonical URL (avoid duplicate content issues) -->
<link rel="canonical" href="https://example.com/current-page" />
```

Head with Essential tags

```html
<head>
  <meta charset="utf-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1" />
  <meta name="description" content="Concise page summary goes here." />
  <meta name="author" content="John Doe" />
  <link rel="icon" href="/favicon.ico" />
  <title>Sample Page</title>
</head>
```

---

### Open Graph (Facebook, LinkedIn, etc.)

```html
<meta property="og:title" content="Page Title" />
<meta property="og:description" content="A short preview description." />
<meta property="og:type" content="website" />
<meta property="og:url" content="https://example.com/page" />
<meta property="og:image" content="https://example.com/preview.jpg" />
<meta property="og:locale" content="en_US" />
```

---

### Twitter Cards

```html
<!-- Summary card -->
<meta name="twitter:card" content="summary" />
<meta name="twitter:title" content="Page Title" />
<meta name="twitter:description" content="A short preview description." />
<meta name="twitter:image" content="https://example.com/preview.jpg" />
<meta name="twitter:site" content="@site_handle" />
```

> [!NOTE]
>
> - Use `summary_large_image` in `twitter:card` for bigger previews.
> - Twitter falls back to Open Graph if specific tags are missing.

---

### Performance & Control

```html
<!-- Control search indexing -->
<meta name="robots" content="index, follow" />
<!-- Block indexing -->
<meta name="robots" content="noindex, nofollow" />

<!-- Theme color for mobile browsers -->
<meta name="theme-color" content="#0f172a" />

<!-- Preload fonts or scripts (performance) -->
<link
  rel="preload"
  href="/fonts/myfont.woff2"
  as="font"
  type="font/woff2"
  crossorigin
/>

<!-- Preconnect for faster DNS/TLS handshake -->
<link rel="preconnect" href="https://fonts.gstatic.com" crossorigin />
```

---

### Social & App Extras

```html
<!-- Apple mobile web app -->
<meta name="apple-mobile-web-app-capable" content="yes" />
<meta
  name="apple-mobile-web-app-status-bar-style"
  content="black-translucent"
/>

<!-- Progressive Web App manifest -->
<link rel="manifest" href="/site.webmanifest" />

<!-- Language & content type (rarely needed with modern defaults) -->
<meta http-equiv="Content-Language" content="en" />
<meta http-equiv="Content-Type" content="text/html; charset=utf-8" />
```

---

> [!NOTE]  
> ✅ **Meta Quick Reference Table**

| Tag / Attribute             | Purpose                     | Common Values                           |
| --------------------------- | --------------------------- | --------------------------------------- |
| `<meta charset>`            | Character encoding          | `"utf-8"`                               |
| `<meta name="viewport">`    | Mobile scaling              | `width=device-width, initial-scale=1`   |
| `<meta name="description">` | SEO snippet                 | Plain text, ≤ 155 chars                 |
| `<meta name="robots">`      | Search engine indexing      | `index, follow` / `noindex, nofollow`   |
| `<meta property="og:*">`    | Social preview (Open Graph) | `title`, `description`, `image`, `url`  |
| `<meta name="twitter:*">`   | Twitter-specific preview    | `card`, `title`, `description`, `image` |
| `<meta name="theme-color">` | Browser UI theme color      | HEX code (e.g., `#2563eb`)              |
| `<link rel="canonical">`    | Preferred page URL          | Full URL                                |
| `<link rel="manifest">`     | PWA manifest                | Path to JSON file                       |

> - Always include `charset`, `viewport`, and `description`.
> - Use Open Graph + Twitter tags for **rich social sharing**.
> - Minimize `<meta keywords>`—deprecated and ignored by most engines.

## 11. Accessibility

Build for **keyboard**, **screen readers**, and **color contrast**. Prefer **native controls**; add ARIA only when needed.

```html
<!-- Images need meaningful alt; use empty alt for decorative images -->
<img src="dog.jpg" alt="A golden retriever puppy" />

<!-- Labeling form controls -->
<label for="email">Email</label>
<input id="email" type="email" autocomplete="email" />

<!-- Avoid redundant aria-label when a <label> exists; use one or the other -->
<input id="search" type="search" aria-label="Site search" />
<!-- OK if no <label> -->

<!-- Landmark nav with an accessible name -->
<nav aria-label="Main navigation">
  <a href="/">Home</a>
  <a href="/about">About</a>
</nav>

<!-- Skip link for keyboard users -->
<a href="#main" class="skip-link">Skip to content</a>
<main id="main">…</main>
```

**Helpful CSS**

```css
/* Visually hidden (but accessible) helper class */
.visually-hidden {
  position: absolute;
  width: 1px;
  height: 1px;
  padding: 0;
  margin: -1px;
  overflow: hidden;
  clip: rect(0 0 0 0);
  white-space: nowrap;
  border: 0;
}

/* Visible focus for keyboard users */
:focus-visible {
  outline: 3px solid #2563eb;
  outline-offset: 2px;
}

/* Position skip link offscreen until focused */
.skip-link {
  position: absolute;
  left: -9999px;
  top: 0;
}
.skip-link:focus {
  left: 0;
  background: #111;
  color: #fff;
  padding: 0.5rem;
  z-index: 1000;
}
```


> [!NOTE]
>
> - Ensure **color contrast** meets WCAG (4.5:1 for normal text).
> - Maintain **logical heading order** and **tab order**.
> - Use `role`/`aria-*` only when native semantics aren’t sufficient.

---

## 12. Best Practices

- Prefer **semantic tags** (`<main>`, `<nav>`, `<article>`) over `<div>` soup.
- Always include **descriptive `alt`** text on images (or `alt=""` if decorative).
- Use **one `<h1>`** per page; structure subsequent headings hierarchically.
- Provide **meta** essentials: charset, viewport, description, icons.
- Keep indentation clean and consistent; avoid trailing whitespace.
- Load CSS via `<link>` (cacheable), and JS with `defer` for predictable execution.
- Validate HTML; keep attributes **lowercase**, values **quoted**.

**Semantic vs non-semantic**

```html
<!-- ❌ Non-semantic (hard to navigate for assistive tech) -->
<div class="header"></div>
<div class="nav"></div>
<div class="content"></div>
<div class="footer"></div>

<!-- ✅ Semantic -->
<header></header>
<nav></nav>
<main></main>
<footer></footer>
```

**Meta essentials**

```html
<head>
  <meta charset="utf-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1" />
  <meta name="description" content="Concise page description (≤ 155 chars)" />
  <link rel="icon" href="/favicon.ico" sizes="any" />
  <link rel="icon" href="/icon.svg" type="image/svg+xml" />
  <link rel="apple-touch-icon" href="/apple-touch-icon.png" />
  <link rel="canonical" href="https://example.com/current-page" />
  <title>Descriptive Title</title>
</head>
```
