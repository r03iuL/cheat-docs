<h1 align="Center"> 📝 Markdown Cheatsheet </h1>

> :bulb: This is a quick reference for Markdown syntax. Full docs: [Markdown Guide](https://www.markdownguide.org/ "markdownguides.org")

> :bulb: Also **[here](https://www.youtube.com/watch?v=ftOBvusMHjQ)** is a youtube crash course on Markdown by **[codeSTACKr](https://www.youtube.com/@codeSTACKr)**

# 📑 Table of Content:

- [Headings](#headings)
- [Emphasis](#emphasis)
- [New line](#new-line)
- [Lists](#lists)
- [Links](#links)
- [References](#references)
- [Images](#images)
- [Images with links](#images-with-links)
- [Blockquotes](#blockquotes)
- [Escape Special Charecter](#escape-special-charecter)
- [Tables](#tables)
- [Horizontal Rule](#horizontal-rule)
- [GitHub Flavored Markdown(GFM)](#github-flavored-markdowngfm)
  - [Task lists:](#task-lists)
  - [Footnotes](#footnotes)
  - [Emojis](#emojis)
  - [Collapsible Dropdown](#collapsible-dropdown)
  - [Definition Lists](#definition-lists)
  - [Aligned tables](#aligned-tables)
  - [Custom html](#custom-html)
- [Badges](#badges)
- [Callouts](#callouts)

---

## Headings

```md
# H1

## H2

### H3

#### H4

##### H5

###### H6
```

<details>
  <summary> Output : </summary>

> # H1
>
> ## H2
>
> ### H3
>
> #### H4
>
> ##### H5
>
> ###### H6

</details>

---

## Emphasis

```md
_italic_ or _italic_  
**bold** or **bold**
**_bold & italic_** **_bold & italic_** **_bold & italic_**
~~strikethrough~~
```

---

## New line

For a new line add two consecutive spaces at the end of previous line .

```md
This is previous line .  
This is newline .
```

Or an empty line added between two lines also gives a new line .

```md
This is previous line.

This is newline.
```

---

## Lists

**Un Ordered**

```md
- Item 1
- Item 2
- Item 3
```

<details>
  <summary> Output : </summary>

> **Unordered**
>
> - Item 1
> - Item 2
> - Item 3

</details>

**Ordered**

```md
1. First
2. Second
3. Third
```

or

```md
1. First
1. Second
1. Third
```

<details>
  <summary> Output : </summary>

> **Ordered**
>
> 1. First
> 2. Second
> 3. Third

or

> 1. First
> 1. Second
> 1. Third

</details>

**Nested**

```md
1. First
2. Second
3. Third
   - First
   - Second
   - Third
```

<details>
  <summary> Output : </summary>

> **Nested**
>
> 1. First
> 1. Second
> 1. Third
>    - First
>    - Second
>    - Third

</details>

---

## Links

```md
[LinkText](https://example.com)
[LinkText](https://example.com "LinkTitle")
```

Headers can be linked like this:

```md
[Go To Links](#links)
```

In GitHub, bare URLs automatically become links.

```md
https://example.com
```

## References

To add a reference link add this to the bottom of doc

```md
[Gh]: https://github.com/r03iul
```

Reference can be used in anywhere in the doc like this :

```md
[My github account][Gh]
```

---

## Images

```md
![Alt text](https://placehold.co/200x100)
```

---

## Images with links

```md
[![Alt text](https://placehold.co/200x100)](https://example.com)
```

---

## Blockquotes

```md
> This is
>
> a
>
> blockquote
```

Output:

> This is
>
> a
>
> blockquote

Nested blockquote

```md
> This is
>
> an exapmle of
>
> > Nested blockquote
```

Output:

> This is
>
> an exapmle of
>
> > Nested blockquote

---

## Code

**Inline code:**

```md
Use `backticks` for inline code
```

**Code blocks:**

````md
```language
console.log("Hello, Markdown!");
```
````

---

## Escape Special Charecter

Add \" \ \" before any special charecter to escape

```md
    \****

    \####

    \*this text has a literal asterisk\*

    \# this is not a heading
```

<details>
  <summary> Output : </summary>

> \*\*\*\*
>
> \#\#\#\#
>
> \*this text has a literal asterisk\*
>
> \# this is not a heading

## </details>

## Tables

( By default table data are left aligned. )

```md
| Column A | Column B |
| -------- | -------- |
| Row 1    | Value    |
| Row 2    | Value    |
```

---

## Horizontal Rule

```md
---
```

---

## GitHub Flavored Markdown (GFM)

### Task lists:

```md
- [ ] Task to do

- [x] Completed task
```

---

### Footnotes

```md
Here’s a footnote.[^1]

[^1]: This is the footnote text.
```

Output:

> Here’s a footnote.[^1]

---

### Emojis

```md
:smile: :rocket: :fire:
```

Output:

> :smile: :rocket: :fire:

Full Emoji list → [GitHub Emoji Cheat Sheet](https://github.com/ikatyang/emoji-cheat-sheet)

### Collapsible Dropdown

```markdown
<details>
  <summary>Click to expand</summary>

Hidden stuff here.....

</details>
```

---

### Definition Lists

```md
Term
: Definition
```

### Aligned tables

```markdown
| Left | Center | Right |
| :--- | :----: | ----: |
| A    |   B    |     C |
```

---

### Custom html

```html
<p align="center">Centered text</p>

<kbd>Ctrl</kbd> + <kbd>C</kbd> → keyboard keys

<sup>Superscript</sup> / <sub>Subscript</sub>
```

<details>
  <summary> Output : </summary>

> <p align="center">Centered text</p>
>
> <kbd>Ctrl</kbd> + <kbd>C</kbd> → keyboard keys
>
> <sup> Superscript</sup> / <sub>Subscript</sub

</details>

---

## Badges

Badges are small images often used in GitHub READMEs to show status, license, or links.  
They are just images (from [shields.io](https://shields.io/) or similar) wrapped in Markdown.

```md
![License](https://img.shields.io/badge/License-MIT-green)
```

Output:

![License](https://img.shields.io/badge/License-MIT-green)

---

## Callouts

Mostly used to share important tips.

```md
> :bulb: **Tip:** Here's an important tip ....
```

Output:

> :bulb: **Tip:** Here's an important tip ....
