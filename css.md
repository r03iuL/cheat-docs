# 🧰 CSS Cheatsheet (2025)

> :bulb: This is a quick reference for everyday modern CSS

> :book: Official Docs: **[W3C CSS Specifications](https://www.w3.org/Style/CSS/current-work)** • Developer References: **[MDN Web Docs](https://developer.mozilla.org/en-US/docs/Web/CSS) • [W3Schools CSS Reference](https://www.w3schools.com/cssref/)**


## Table of Contents

- [Core \& Mental Models](#core--mental-models)
  - [Cascade, specificity \& inheritance](#cascade-specificity--inheritance)
  - [Cascade layers (`@layer`) \& when to use them](#cascade-layers-layer--when-to-use-them)
  - [Nesting (native CSS nesting) \& selector essentials](#nesting-native-css-nesting--selector-essentials)
  - [Units \& sizing (`px`, `rem`, `%`, `vw`/`vh`, `ch`; `clamp()` / `min()` / `max()`)](#units--sizing-px-rem--vwvh-ch-clamp--min--max)
  - [Colors \& variables (`:root`, `var()`), modern color spaces (OKLCH), `color-mix()` basics](#colors--variables-root-var-modern-color-spaces-oklch-color-mix-basics)
- [Layout \& Spacing](#layout--spacing)
  - [Box model \& logical properties (flow-relative margins/padding/size)](#box-model--logical-properties-flow-relative-marginspaddingsize)
  - [Flexbox essentials (1-D layout patterns)](#flexbox-essentials-1-d-layout-patterns)
  - [CSS Grid essentials (auto-fit/fill, `minmax()`, alignment)](#css-grid-essentials-auto-fitfill-minmax-alignment)
  - [Gap vs margins; alignment \& distribution (box-alignment)](#gap-vs-margins-alignment--distribution-box-alignment)
  - [Positioning \& stacking context (`position: sticky/absolute`, `z-index`)](#positioning--stacking-context-position-stickyabsolute-z-index)
  - [Aspect-ratio \& media fit (`object-fit`, `object-position`)](#aspect-ratio--media-fit-object-fit-object-position)
  - [Overflow \& scrolling (`overflow`, `scroll-behavior`, scroll-snap basics)](#overflow--scrolling-overflow-scroll-behavior-scroll-snap-basics)
- [Typography \& UI](#typography--ui)
  - [System / variable font stacks, `font-display`](#system--variable-font-stacks-font-display)
  - [Line-length (`ch`), `line-height`, `letter-spacing`, text wrapping](#line-length-ch-line-height-letter-spacing-text-wrapping)
  - [Buttons, forms \& focus states (`:focus-visible`, `:placeholder-shown`)](#buttons-forms--focus-states-focus-visible-placeholder-shown)
- [State \& Interaction](#state--interaction)
  - [Pseudo-classes / elements (`:hover`, `:active`, `:disabled`, `:has()`, `::before/after`)](#pseudo-classes--elements-hover-active-disabled-has-beforeafter)
  - [Transitions \& transforms (GPU-friendly patterns)](#transitions--transforms-gpu-friendly-patterns)
  - [Keyframe animations + reduced motion considerations](#keyframe-animations--reduced-motion-considerations)
- [Responsive \& Theming](#responsive--theming)
  - [Media queries (`width`, `prefers-reduced-motion`, `prefers-color-scheme`)](#media-queries-width-prefers-reduced-motion-prefers-color-scheme)
  - [Container queries (`@container`, `container-type` / `container-name`)](#container-queries-container-container-type--container-name)
  - [Fluid type \& spacing with `clamp()` / fluid interpolation](#fluid-type--spacing-with-clamp--fluid-interpolation)
  - [Dark mode: `color-scheme`, `prefers-color-scheme`, `light()` / `dark()` functions](#dark-mode-color-scheme-prefers-color-scheme-light--dark-functions)
- [Utilities \& Hygiene](#utilities--hygiene)
  - [Resets / normalize (modern minimal reset)](#resets--normalize-modern-minimal-reset)
  - [Common utilities (visually-hidden, centering, aspect-ratio helpers)](#common-utilities-visually-hidden-centering-aspect-ratio-helpers)
  - [Debugging CSS (outline/debug layers, DevTools overlays)](#debugging-css-outlinedebug-layers-devtools-overlays)
  - [Browser support \& fallbacks (how to check Can I Use)](#browser-support--fallbacks-how-to-check-can-i-use)
  - [Print styles (quick essentials)](#print-styles-quick-essentials)
- [Tooling (optional)](#tooling-optional)
  - [stylelint \& Prettier quick setup](#stylelint--prettier-quick-setup)

---

## Core & Mental Models

### Cascade, specificity & inheritance

1. **Explanation** — The cascade resolves conflicts between CSS rules via origin, specificity, and source order. Inheritance passes property values from parent to child (for inheritable properties). Understanding them is key to predictable styling.
2. **Code**
   ```css
   /* Example of specificity and override */
   body {
     color: black;
   }
   .theme-dark body {
     color: white;
   }
   #header .title {
     color: blue;
   }
   h1.title {
     color: red;
   }
   ```
3. **Code breakdown**
   - `body { color: black; }` — base style
   - `.theme-dark body { color: white; }` — class-based override
   - `#header .title { color: blue; }` — higher specificity
   - `h1.title { color: red; }` — lower specificity vs ID selector
4. **What keywords mean**
   - `<selector>` — any CSS selector
   - specificity — weight of selector (inline > ID > class > element)
   - cascade origin — user agent, user, author, important
   - inheritance — passing down properties (like `color`, `font`)
5. **Hints & tips**
   - :bulb: **Tip** — favor specificity layering, not `!important`.
   - Use utility classes sparingly and in a defined order to avoid conflicts.
   - Always inspect via DevTools to see which rule “won.”
   - Avoid deep selector chains which become brittle.

---

### Cascade layers (`@layer`) & when to use them

1. **Explanation** — `@layer` lets you explicitly group and order style layers, so you control cascade precedence without specificity hacks. :contentReference[oaicite:0]{index=0}
2. **Code**

   ```css
   @layer reset, base, components, overrides;

   @layer base {
     body {
       margin: 0;
       font-family: sans-serif;
     }
   }

   @layer components {
     .btn {
       padding: 0.5rem 1rem;
       border: none;
     }
   }

   @layer overrides {
     .btn.primary {
       background: blue;
       color: white;
     }
   }
   ```

3. **Code breakdown**
   - `@layer reset, base, components, overrides;` — defines layer order
   - `@layer base { … }` — base rules
   - `@layer components { … }` — component-level rules
   - `@layer overrides { … }` — last-level overrides
4. **What keywords mean**
   - `<layer-name>` — name of a cascade layer
   - `@layer` — declare or use a layer
   - precedence — earlier layers < later layers
5. **Hints & tips**
   - :bulb: **Tip** — put third-party or framework CSS in a lower layer so your overrides live in later layers.
   - You can mix `@layer` with `@media`, `@supports`, and nesting.
   - > [!NOTE] Browser support is good in major browsers as of 2024, but always check fallback if targeting older browsers. :contentReference[oaicite:1]{index=1}

---

### Nesting (native CSS nesting) & selector essentials

1. **Explanation** — Native CSS nesting allows writing nested rules like in preprocessors (e.g. SCSS), improving readability. It’s now standardized. :contentReference[oaicite:2]{index=2}
2. **Code**
   ```css
   .card {
     border: 1px solid #ccc;
     &:hover {
       border-color: #888;
     }
     & .title {
       font-weight: bold;
     }
   }
   ```
3. **Code breakdown**
   - `.card { … }` — parent selector
   - `&:hover { … }` — `.card:hover`
   - `& .title { … }` — `.card .title`
4. **What keywords mean**
   - `&` — represents parent selector in nesting
   - `<selector>` — nested child or sibling selection
5. **Hints & tips**
   - :bulb: **Tip** — don’t over-nest (max depth ~2–3) to avoid complexity.
   - You can mix nested selectors with cascade layers and media queries.
   - > [!WARNING] Overly deep nesting can exacerbate specificity issues if misused.

---

### Units & sizing (`px`, `rem`, `%`, `vw`/`vh`, `ch`; `clamp()` / `min()` / `max()`)

1. **Explanation** — Different units serve different responsive needs. `clamp()` (and `min()`/`max()`) help create fluid values within a range.
2. **Code**
   ```css
   h1 {
     font-size: clamp(1.5rem, 4vw + 1rem, 3rem);
     max-width: 60ch;
   }
   .box {
     width: 50%;
     height: min(300px, 50vh);
   }
   ```
3. **Code breakdown**
   - `clamp(1.5rem, 4vw + 1rem, 3rem)` — fluid font size between 1.5rem and 3rem
   - `max-width: 60ch;` — limit line length by character unit
   - `width: 50%;` — half of parent’s width
   - `height: min(300px, 50vh);` — choose smaller value
4. **What keywords mean**
   - `<len>` — length unit (px, rem, etc.)
   - `clamp(min, preferred, max)` — clamps a value between min and max
   - `min()`, `max()` — choose min or max between a set of expressions
   - `vw` / `vh` — viewport width / height units
   - `ch` — width of “0” character (approx)
5. **Hints & tips**
   - :bulb: **Tip** — use `rem` for root-relative scaling; `vw` for fluid scaling; `clamp` to avoid extremes.
   - Avoid `100vw` minus scrollbars; prefer logical sizing or `max-inline-size`.
   - Use `%` when relative to parent container.

---

### Colors & variables (`:root`, `var()`), modern color spaces (OKLCH), `color-mix()` basics

1. **Explanation** — CSS custom properties allow themeable variables. Modern color spaces (OKLCH etc.) and `color-mix()` let you interpolate colors more perceptually.
2. **Code**
   ```css
   :root {
     --primary: oklch(60% 0.1 120);
     --on-primary: oklch(5% 0.02 110);
   }
   .btn {
     background: var(--primary);
     color: var(--on-primary);
   }
   .btn:hover {
     background: color-mix(in srgb, var(--primary) 80%, white 20%);
   }
   ```
3. **Code breakdown**
   - `:root { … }` — global custom property definitions
   - `--primary`, `--on-primary` — variable names
   - `oklch(...)` — perceptual color function
   - `var(--primary)` — use variable
   - `color-mix(in srgb, A 80%, B 20%)` — mix two colors
4. **What keywords mean**
   - `<color>` — any CSS color (named, hex, function)
   - `oklch()` — color in OKLCH space (lightness, chroma, hue)
   - `var(--name)` — uses a CSS variable
   - `color-mix(in <space>, <color1> <pct>, <color2> <pct>)` — mixes colors
5. **Hints & tips**
   - :bulb: **Tip** — use fallback in `var()` like `var(--foo, fallback)`.
   - Keep variable names semantic (`--surface`, `--accent`) not tied to color.
   - > [!NOTE] OKLCH support is broadly available in modern browsers as of 2024.

---

## Layout & Spacing

### Box model & logical properties (flow-relative margins/padding/size)

1. **Explanation** — Logical properties replace `top/right/bottom/left`, `width/height` etc. with flow-relative axis versions, supporting different writing modes and directionality. :contentReference[oaicite:3]{index=3}
2. **Code**
   ```css
   .card {
     padding-block: 1rem 2rem;
     margin-inline: 0 auto;
     min-inline-size: 20rem;
     inset-block-start: 2rem;
   }
   ```
3. **Code breakdown**
   - `padding-block: 1rem 2rem` — padding on block-start & block-end
   - `margin-inline: 0 auto` — center horizontally (inline axis)
   - `min-inline-size: 20rem` — minimum inline width (in flow direction)
   - `inset-block-start: 2rem` — distance from top in block flow
4. **What keywords mean**
   - `block` / `inline` — flow axes relative to writing direction
   - `start` / `end` — logical start/end in a flow
   - `inset-block-*`, `margin-inline`, etc. — logical equivalents of top/left etc.
5. **Hints & tips**
   - :bulb: **Tip** — prefer logical properties over physical ones for global layouts.
   - Use logical sizing with flex / grid to maintain direction independence.

---

### Flexbox essentials (1-D layout patterns)

1. **Explanation** — Flexbox is ideal for distributing items along one axis (row or column) and handling alignment, wrapping, and growth.
2. **Code**
   ```css
   .container {
     display: flex;
     flex-wrap: wrap;
     gap: 1rem;
     justify-content: center;
     align-items: start;
   }
   .item {
     flex: 1 1 200px;
   }
   ```
3. **Code breakdown**
   - `display: flex;` — enable flex layout
   - `flex-wrap: wrap;` — allow items to wrap to next line
   - `gap: 1rem;` — space between items
   - `justify-content: center;` — distribute items horizontally
   - `align-items: start;` — align items at top
   - `flex: 1 1 200px;` — grow/shrink with base 200px
4. **What keywords mean**
   - `flex-grow` / `flex-shrink` / `flex-basis` (shorthand `flex`)
   - `justify-content` — main axis distribution
   - `align-items` — cross-axis alignment
   - `gap` — spacing between flex items
5. **Hints & tips**
   - :bulb: **Tip** — use `flex: 1` for equal distribution.
   - Use `align-self` to override single item alignment.
   - Combine with `min-inline-size` to set responsive minimums.

---

### CSS Grid essentials (auto-fit/fill, `minmax()`, alignment)

1. **Explanation** — CSS Grid gives 2D layout control. Use `auto-fit`/`auto-fill` and `minmax()` for responsive grids.
2. **Code**
   ```css
   .grid {
     display: grid;
     grid-template-columns: repeat(auto-fit, minmax(200px, 1fr));
     gap: 1rem;
   }
   .grid > * {
     align-self: start;
   }
   ```
3. **Code breakdown**
   - `repeat(auto-fit, minmax(200px, 1fr))` — responsive columns
   - `gap: 1rem;` — grid spacing
   - `align-self: start;` — vertical alignment per item
4. **What keywords mean**
   - `auto-fit` / `auto-fill` — fill available space with columns
   - `minmax(min, max)` — range sizing for tracks
   - `1fr` — fraction of remaining space
   - `grid-template-columns` — define columns
5. **Hints & tips**
   - :bulb: **Tip** — use `auto-fit` so items expand to fill space.
   - Use `grid-auto-flow: dense;` for compactness.
   - Combine with `place-items` / `place-content` for short alignment.

---

### Gap vs margins; alignment & distribution (box-alignment)

1. **Explanation** — `gap` applies consistent spacing without collapsing margins. Box-alignment properties (`justify-*`, `align-*`) unify alignment across layout systems.
2. **Code**
   ```css
   .flex,
   .grid {
     gap: 1rem;
     justify-items: center;
     align-items: center;
   }
   ```
3. **Code breakdown**
   - `gap: 1rem;` — consistent spacing
   - `justify-items: center;` / `align-items: center;` — alignment in grid/flex
4. **What keywords mean**
   - `justify-items`, `align-items`, `justify-content`, `align-content` — alignment properties
   - `gap` — spacing between items
5. **Hints & tips**
   - :bulb: **Tip** — prefer `gap` over margin hacks in layout containers.
   - Use `justify-self` / `align-self` for per-item override.

---

### Positioning & stacking context (`position: sticky/absolute`, `z-index`)

1. **Explanation** — Positioning removes elements from normal flow or anchors them. Z-index controls stacking in new stacking contexts.
2. **Code**
   ```css
   .sticky-header {
     position: sticky;
     inset-block-start: 0;
     z-index: 100;
   }
   .overlay {
     position: absolute;
     inset: 0;
     z-index: 200;
   }
   ```
3. **Code breakdown**
   - `position: sticky;` — sticks within scroll container
   - `inset-block-start: 0;` — top offset in block flow
   - `position: absolute; inset: 0;` — fill relative parent
   - `z-index: 100 / 200` — stacking order
4. **What keywords mean**
   - `position: relative / absolute / fixed / sticky`
   - `inset / inset-block / inset-inline` — shorthand for top/left/etc.
   - `z-index` — stacking order (higher is above)
5. **Hints & tips**
   - :bulb: **Tip** — sticky only works if ancestor overflow is visible.
   - Use `position: relative` on parent to anchor absolute children.
   - Avoid extremely large z-index values; manage layers.

---

### Aspect-ratio & media fit (`object-fit`, `object-position`)

1. **Explanation** — `aspect-ratio` lets you maintain proportion. `object-fit` / `object-position` control how replaced elements (images/videos) fill their containers.
2. **Code**
   ```css
   .box {
     aspect-ratio: 16 / 9;
     width: 100%;
   }
   img.cover {
     width: 100%;
     height: 100%;
     object-fit: cover;
     object-position: center;
   }
   ```
3. **Code breakdown**
   - `aspect-ratio: 16/9;` — fixed ratio container
   - `object-fit: cover;` — scale and crop to cover container
   - `object-position: center;` — center the content
4. **What keywords mean**
   - `aspect-ratio: <width> / <height>`
   - `object-fit` — `cover`, `contain`, `fill`, etc.
   - `object-position` — where in container the object aligns
5. **Hints & tips**
   - :bulb: **Tip** — always set width/height or aspect-ratio to avoid layout shift.
   - Use `contain` when you want whole image visible.

---

### Overflow & scrolling (`overflow`, `scroll-behavior`, scroll-snap basics)

1. **Explanation** — Control content overflow and scrolling behavior. Scroll snapping helps align content on scroll.
2. **Code**
   ```css
   .container {
     overflow: auto;
     scroll-behavior: smooth;
     scroll-snap-type: x mandatory;
   }
   .child {
     scroll-snap-align: center;
   }
   ```
3. **Code breakdown**
   - `overflow: auto;` — show scrollbars as needed
   - `scroll-behavior: smooth;` — smooth scroll animation
   - `scroll-snap-type: x mandatory;` — enable snapping on x-axis
   - `scroll-snap-align: center;` — child snap alignment
4. **What keywords mean**
   - `overflow` / `overflow-x` / `overflow-y`
   - `scroll-behavior` — `auto` or `smooth`
   - `scroll-snap-type`, `scroll-snap-align` — snapping properties
5. **Hints & tips**
   - :bulb: **Tip** — add `-webkit-overflow-scrolling: touch;` on iOS for momentum.
   - Use snap margins to avoid content being cut off.

---

## Typography & UI

### System / variable font stacks, `font-display`

1. **Explanation** — System stacks improve performance and fallback. Variable fonts let you adjust weight/axis. `font-display` controls loading behavior.
2. **Code**
   ```css
   @font-face {
     font-family: "MyVarFont";
     src: url("MyVarFont.woff2") format("woff2");
     font-weight: 100 900;
     font-display: swap;
   }
   body {
     font-family: system-ui, -apple-system, sans-serif;
   }
   h1 {
     font-variation-settings: "wght" 700;
   }
   ```
3. **Code breakdown**
   - `font-weight: 100 900;` — variable range
   - `font-display: swap;` — fallback then swap to custom
   - `system-ui, -apple-system` — system font stack
   - `font-variation-settings: 'wght' 700;` — set weight axis
4. **What keywords mean**
   - `font-family`, `font-weight`, `font-display`
   - `font-variation-settings` for variable axes
   - system font keywords
5. **Hints & tips**
   - :bulb: **Tip** — using `swap` prevents invisible text.
   - Use variable fonts sparingly for weights or italics.
   - Test fallback font metrics (baseline, x-height) match.

---

### Line-length (`ch`), `line-height`, `letter-spacing`, text wrapping

1. **Explanation** — Good typography balances readability via line length, height, spacing, and wrapping.
2. **Code**
   ```css
   p {
     max-width: 65ch;
     line-height: 1.5;
     letter-spacing: 0.02em;
     word-break: break-word;
   }
   ```
3. **Code breakdown**
   - `max-width: 65ch;` — optimal line length in characters
   - `line-height: 1.5;` — vertical spacing
   - `letter-spacing: 0.02em;` — adjust tracking
   - `word-break: break-word;` — safe wrapping
4. **What keywords mean**
   - `ch` — width of “0” (approx)
   - `line-height` — height per line
   - `letter-spacing` — additional horizontal spacing
   - `word-break`, `overflow-wrap` — wrap rules
5. **Hints & tips**
   - :bulb: **Tip** — for multilingual pages, test wrapping.
   - Avoid very tight letter-spacing on small text.

---

### Buttons, forms & focus states (`:focus-visible`, `:placeholder-shown`)

1. **Explanation** — Accessible focus styles and form state selectors help UI clarity.
2. **Code**
   ```css
   button:focus-visible {
     outline: 2px solid Highlight;
     outline-offset: 2px;
   }
   input:placeholder-shown {
     color: #999;
   }
   ```
3. **Code breakdown**
   - `:focus-visible` — browser-sensible focus outline
   - `outline`, `outline-offset` — visible focus styling
   - `:placeholder-shown` — matches when placeholder visible
4. **What keywords mean**
   - `:focus-visible`, `:focus`, `:placeholder-shown`
   - `outline`, `outline-offset`
5. **Hints & tips**
   - :bulb: **Tip** — don’t remove focus outlines; style them for contrast.
   - Use `:focus-visible` to avoid styling click-only focus.

---

## State & Interaction

### Pseudo-classes / elements (`:hover`, `:active`, `:disabled`, `:has()`, `::before/after`)

1. **Explanation** — Pseudo-classes and elements let you style based on state or insert generated content. `:has()` enables parent queries. :contentReference[oaicite:4]{index=4}
2. **Code**
   ```css
   .card:hover {
     box-shadow: 0 4px 8px rgba(0, 0, 0, 0.1);
   }
   form:has(input:invalid) .submit {
     opacity: 0.5;
   }
   .btn::before {
     content: "★";
     margin-inline-end: 0.5em;
   }
   ```
3. **Code breakdown**
   - `.card:hover` — hover state
   - `form:has(input:invalid)` — parent form when child invalid
   - `.btn::before` — inject star before button text
4. **What keywords mean**
   - Pseudo-classes: `:hover`, `:active`, `:disabled`, `:has()`
   - Pseudo-elements: `::before`, `::after`
   - `content` — value for pseudo-element content
5. **Hints & tips**
   - :bulb: **Tip** — `:has()` is powerful but potentially costly; use sparingly.
   - Always include fallback for older browsers if relying on `:has()`.

---

### Transitions & transforms (GPU-friendly patterns)

1. **Explanation** — Use transitions for smooth UI updates. Prefer transform/opacity for hardware acceleration.
2. **Code**
   ```css
   .card {
     transition: transform 0.3s ease, opacity 0.3s ease;
   }
   .card:hover {
     transform: translateY(-4px) scale(1.02);
     opacity: 0.95;
   }
   ```
3. **Code breakdown**
   - `transition: ...` — define animated properties
   - `transform: translateY(...) scale(...)` — move & scale
   - `opacity: 0.95;` — fade effect
4. **What keywords mean**
   - `transition`, `transition-property`, `transition-duration`, `transition-timing-function`
   - `transform` — `translate`, `scale`, `rotate`, etc.
   - `opacity` — 0 to 1 transparency
5. **Hints & tips**
   - :bulb: **Tip** — avoid animating `width`/`height`, prefer `transform` and `opacity`.
   - Use `will-change: transform;` when needed (sparingly).

---

### Keyframe animations + reduced motion considerations

1. **Explanation** — Complex animations use `@keyframes`. Respect user preferences via `prefers-reduced-motion`.
2. **Code**
   ```css
   @keyframes fade-in {
     from {
       opacity: 0;
     }
     to {
       opacity: 1;
     }
   }
   .modal {
     animation: fade-in 0.4s ease forwards;
   }
   @media (prefers-reduced-motion: reduce) {
     .modal {
       animation: none;
     }
   }
   ```
3. **Code breakdown**
   - `@keyframes fade-in { … }` — define animation
   - `animation: fade-in 0.4s ease forwards;` — apply it
   - `@media (prefers-reduced-motion: reduce)` — override for accessibility
4. **What keywords mean**
   - `@keyframes` — define animation sequence
   - `animation` shorthand (name, duration, timing, etc.)
   - `prefers-reduced-motion` — media query feature
5. **Hints & tips**
   - :bulb: **Tip** — always give a reduced-motion fallback.
   - Use `animation-fill-mode: both / forwards` to maintain state after anim ends.

---

## Responsive & Theming

### Media queries (`width`, `prefers-reduced-motion`, `prefers-color-scheme`)

1. **Explanation** — Media queries allow responsive or preference-based styling.
2. **Code**
   ```css
   @media (min-width: 40rem) {
     .layout {
       grid-template-columns: 1fr 2fr;
     }
   }
   @media (prefers-color-scheme: dark) {
     body {
       color-scheme: dark;
       background: black;
       color: white;
     }
   }
   ```
3. **Code breakdown**
   - `(min-width: 40rem)` — condition on viewport width
   - `grid-template-columns` change on larger screens
   - `(prefers-color-scheme: dark)` — user preference for dark mode
   - `color-scheme: dark;` — let system render semantics (e.g. scrollbars)
4. **What keywords mean**
   - `@media` — conditional block
   - `min-width`, `max-width`, etc. — media features
   - `prefers-reduced-motion`, `prefers-color-scheme` — user preference features
5. **Hints & tips**
   - :bulb: **Tip** — mobile-first: start small, add breakpoints upward.
   - Combine media queries with layering (`@layer`) as needed.

---

### Container queries (`@container`, `container-type` / `container-name`)

1. **Explanation** — Container queries let components adapt based on parent container size, not viewport. :contentReference[oaicite:5]{index=5}
2. **Code**
   ```css
   .card-container {
     container-type: inline-size;
     container-name: card;
   }
   .card {
     @container card (min-width: 30rem) {
       padding: 2rem;
       font-size: 1.25rem;
     }
   }
   ```
3. **Code breakdown**
   - `container-type: inline-size;` — define container query axis
   - `container-name: card;` — optional name
   - `@container card (min-width: 30rem)` — query on container width
   - inside — style adjustments when condition true
4. **What keywords mean**
   - `@container` — container query rule
   - `container-type` — `size`, `inline-size`
   - `container-name` — optional identifier
   - `(min-width: …)` — condition on container size
5. **Hints & tips**
   - :bulb: **Tip** — fall back to media queries for older browsers. :contentReference[oaicite:6]{index=6}
   - Start small: use container queries for layout-critical components.
   - Avoid nested container queries deeply.

---

### Fluid type & spacing with `clamp()` / fluid interpolation

1. **Explanation** — Make typography and spacing fluid across screen sizes, constrained by min & max.
2. **Code**
   ```css
   h2 {
     font-size: clamp(1.25rem, 2vw + 1rem, 2rem);
   }
   .gap {
     margin-block: clamp(1rem, 5vw, 4rem);
   }
   ```
3. **Code breakdown**
   - `clamp(1.25rem, 2vw + 1rem, 2rem)` — fluid font scaling
   - `margin-block: clamp(1rem, 5vw, 4rem);` — fluid vertical spacing
4. **What keywords mean**
   - `clamp(min, preferred, max)` — constrain values
   - `vw` — viewport width unit
5. **Hints & tips**
   - :bulb: **Tip** — mix with container queries for more responsive control.
   - Don’t overdo fluid scaling — readability still matters.

---

### Dark mode: `color-scheme`, `prefers-color-scheme`, `light()` / `dark()` functions

1. **Explanation** — Respect user’s color scheme preference and allow system UI coloring via `color-scheme`. New CSS functions (light/dark) help conditional theming.
2. **Code**
   ```css
   @media (prefers-color-scheme: dark) {
     :root {
       color-scheme: dark;
       --surface: oklch(10% 0.02 200);
       --on-surface: oklch(90% 0.02 200);
     }
   }
   @media (prefers-color-scheme: light) {
     :root {
       color-scheme: light;
       --surface: oklch(98% 0.02 200);
       --on-surface: oklch(10% 0.02 200);
     }
   }
   .card {
     background: var(--surface);
     color: var(--on-surface);
   }
   ```
3. **Code breakdown**
   - `prefers-color-scheme: dark / light` — user preference
   - `color-scheme: dark / light;` — let UA style internal UI appropriately
   - custom properties set per mode
   - usage on `.card`
4. **What keywords mean**
   - `color-scheme` — indicates which color scheme UA should use
   - `prefers-color-scheme` — media feature
   - `light()` / `dark()` (future) — conditional color functions
5. **Hints & tips**
   - :bulb: **Tip** — always include both dark and light definitions.
   - Test images/icons in both modes for contrast.

---

## Utilities & Hygiene

### Resets / normalize (modern minimal reset)

1. **Explanation** — A minimal reset ensures consistent base across browsers, then build on top.
2. **Code**
   ```css
   /* Minimal reset */
   *,
   *::before,
   *::after {
     box-sizing: border-box;
   }
   html {
     line-height: 1.5;
     text-size-adjust: 100%;
   }
   body {
     margin: 0;
   }
   img,
   video {
     max-inline-size: 100%;
     height: auto;
     display: block;
   }
   ```
3. **Code breakdown**
   - `box-sizing: border-box;` — include padding in size
   - `line-height: 1.5;` — consistent baseline
   - `text-size-adjust: 100%;` — prevent font scaling on mobile
   - `margin: 0;` — remove default body margin
   - `img, video` rules — responsive multimedia
4. **What keywords mean**
   - `box-sizing`, `line-height`, `text-size-adjust`
   - `max-inline-size` — logical width limit
5. **Hints & tips**
   - :bulb: **Tip** — you can layer more resets under `@layer reset`.
   - Avoid “global \* selector resets” that defeat semantics.

---

### Common utilities (visually-hidden, centering, aspect-ratio helpers)

1. **Explanation** — Handy small helpers you’ll reuse across projects.
2. **Code**
   ```css
   .visually-hidden {
     position: absolute !important;
     inset: 0;
     width: 1px;
     height: 1px;
     padding: 0;
     margin: -1px;
     overflow: hidden;
     clip: rect(0, 0, 0, 0);
     white-space: nowrap;
   }
   .center {
     display: grid;
     place-items: center;
   }
   .aspect-square {
     aspect-ratio: 1 / 1;
   }
   ```
3. **Code breakdown**
   - `.visually-hidden { … }` — hide visually but accessible
   - `.center` — center with grid
   - `.aspect-square` — force square aspect ratio
4. **What keywords mean**
   - `place-items: center` — shorthand for `justify-items` + `align-items`
   - `clip`, `overflow`, `inset` — visibility tools
5. **Hints & tips**
   - :bulb: **Tip** — wrap utilities in a layer to override defaults if needed.

---

### Debugging CSS (outline/debug layers, DevTools overlays)

1. **Explanation** — Use temporary outlines, semi-transparent backgrounds, or debug layers to inspect layout and stacking.
2. **Code**
   ```css
   * {
     outline: 1px solid rgba(255, 0, 0, 0.2);
   }
   .debug-layer {
     position: absolute;
     inset: 0;
     pointer-events: none;
     background: rgba(0, 255, 0, 0.1);
   }
   ```
3. **Code breakdown**
   - `outline: 1px solid …` — visual bounding boxes
   - `.debug-layer` — overlay transparent layer
4. **What keywords mean**
   - `outline` — non-layout-affecting border
   - `pointer-events: none` — let clicks go through
5. **Hints & tips**
   - :bulb: **Tip** — always remove debug styles before merging code.
   - Use DevTools grid/flex overlays (in Chrome/Firefox) to inspect.

---

### Browser support & fallbacks (how to check Can I Use)

1. **Explanation** — Use feature queries (`@supports`) and check sites like Can I Use for compatibility.
2. **Code**
   ```css
   @supports (container-type: inline-size) {
     .card {
       container-type: inline-size;
     }
   }
   @supports not (container-type: inline-size) {
     .card {
       /* fallback styling */
     }
   }
   ```
3. **Code breakdown**
   - `@supports (container-type: inline-size)` — branch if supported
   - `@supports not (…)` — fallback path
4. **What keywords mean**
   - `@supports` — feature query
5. **Hints & tips**
   - :bulb: **Tip** — always include fallback CSS paths.
   - Use `@supports (color: oklch(50% 0.1 120))` to test color space support.

---

### Print styles (quick essentials)

1. **Explanation** — A minimal print stylesheet ensures content is legible and unnecessary UI is hidden in print.
2. **Code**
   ```css
   @media print {
     body {
       color: black;
       background: white;
     }
     nav,
     .btn,
     .no-print {
       display: none !important;
     }
     img {
       max-inline-size: 100%;
       height: auto;
     }
   }
   ```
3. **Code breakdown**
   - `@media print { … }` — print-specific rules
   - Hide non-essential elements
   - Force images to scale
4. **What keywords mean**
   - `@media print` — applies in print context
   - `.no-print` — custom class to hide elements
5. **Hints & tips**
   - :bulb: **Tip** — test print in browser “Print Preview.”
   - Avoid absolute positioning or fixed elements in print.

---

## Tooling (optional)

### stylelint & Prettier quick setup

1. **Explanation** — stylelint enforces CSS rules; Prettier auto-formats. A minimal config helps maintain consistency.
2. **Code**
   ```json
   // .stylelintrc.json
   {
     "extends": ["stylelint-config-standard", "stylelint-config-prettier"],
     "rules": {
       "color-function-notation": "modern",
       "custom-property-pattern": "^--[a-z0-9-]+$"
     }
   }
   ```
3. **Code breakdown**
   - `extends` — base configs
   - `color-function-notation: modern` — enforce `oklch()`, etc.
   - `custom-property-pattern` — enforce naming convention
4. **What keywords mean**
   - `stylelint` — CSS linter
   - `Prettier` — formatter
   - `extends`, `rules` — config keys
5. **Hints & tips**
   - :bulb: **Tip** — integrate lint/format on pre-commit hook.
   - Configure CSS-in-JS or framework overrides if needed.

---
