<h1 align="center"> 🧠 JavaScript Crash Course Cheatsheet </h1>

> :rocket: A complete quick reference for mastering **JavaScript fundamentals**.  

> :book: Official Docs: [MDN JavaScript Guide](https://developer.mozilla.org/en-US/docs/Web/JavaScript)  

> :tv: Recommended Video: [JavaScript Crash Course - Traversy Media](https://www.youtube.com/watch?v=hdI2bqOjy3c)

---

# 📑 Table of Contents

- [🧩 1. JavaScript Basics](#-1-javascript-basics)
  - [What is JavaScript \& Where It Runs](#what-is-javascript--where-it-runs)
  - [Linking JS to HTML](#linking-js-to-html)
  - [Comments, Syntax, and Naming Conventions](#comments-syntax-and-naming-conventions)
  - [console.log() and Debugging](#consolelog-and-debugging)
  - [Variables: var, let, const](#variables-var-let-const)
  - [Data Types](#data-types)
  - [Type Conversion \& Coercion](#type-conversion--coercion)
  - [Template Literals](#template-literals)
  - [Operators](#operators)
  - [Ternary Operator](#ternary-operator)
  - [Loops](#loops)
  - [Conditional Statements](#conditional-statements)
  - [Loop Control: break \& continue](#loop-control-break--continue)
- [⚙️ 2. Functions \& Scope](#️-2-functions--scope)
  - [Function Declaration vs Expression](#function-declaration-vs-expression)
  - [Parameters, Arguments, Return Values](#parameters-arguments-return-values)
  - [Default Parameters](#default-parameters)
  - [Arrow Functions](#arrow-functions)
  - [Scope \& Hoisting](#scope--hoisting)
  - [Closures](#closures)
  - [Callbacks \& Higher-Order Functions](#callbacks--higher-order-functions)
- [🧮 3. Data Structures \& Manipulation](#-3-data-structures--manipulation)
  - [Strings](#strings)
  - [Arrays](#arrays)
  - [Objects](#objects)
  - [Spread \& Rest](#spread--rest)
- [🧠 4. DOM Manipulation](#-4-dom-manipulation)
  - [Selecting \& Modifying Elements](#selecting--modifying-elements)
  - [Events](#events)
- [🌐 5. Browser APIs \& Asynchronous JS](#-5-browser-apis--asynchronous-js)
  - [JSON](#json)
  - [Fetch API](#fetch-api)
- [⚡ 6. ES6+ Modern Features](#-6-es6-modern-features)
  - [Destructuring](#destructuring)
  - [Template Literals](#template-literals-1)
  - [Modules](#modules)
- [🧱 7. OOP \& Functional Programming](#-7-oop--functional-programming)
  - [Classes](#classes)
  - [Inheritance](#inheritance)
  - [Functional Patterns](#functional-patterns)
- [⏳ 8. Asynchronous Patterns](#-8-asynchronous-patterns)
  - [Callbacks](#callbacks)
  - [Promises](#promises)
  - [Async/Await](#asyncawait)

## 🧩 1. JavaScript Basics

### What is JavaScript & Where It Runs

JavaScript is a **high-level, interpreted programming language** that adds interactivity to web pages. It runs both in browsers and on servers through **Node.js**.

```js
// Runs in browsers
console.log("Hello from the browser!");

// Runs in Node.js (server-side)
console.log("Hello from Node.js");
```

It powers dynamic content in browsers and backend logic in Node.js.

> :bulb: JavaScript is **event-driven** and **single-threaded**, but handles asynchronous tasks using callbacks, promises, and async/await.

---

### Linking JS to HTML

You can link JavaScript files to an HTML document using the `<script>` tag.

```html
<!DOCTYPE html>
<html>
  <head>
    <title>JS Demo</title>
  </head>
  <body>
    <h1>Hello World</h1>
    <script src="app.js"></script>
  </body>
</html>
```

The `<script>` tag allows the browser to execute JavaScript. Placing it before the `</body>` tag ensures the page loads first.

---

### Comments, Syntax, and Naming Conventions

JavaScript supports single-line and multi-line comments.

```js
// This is a single-line comment
/*
  This is a
  multi-line comment
*/
```

> :bulb: Use **camelCase** for variables and functions, and **PascalCase** for classes.

---

### console.log() and Debugging

Use `console.log()` to print messages and debug values in your browser’s console.

```js
let x = 5;
console.log("The value of x is:", x);
```

You can also use:

- `console.error()` for errors
- `console.table()` for arrays/objects

---

### Variables: var, let, const

Variables store data. Use `let` and `const` for modern JavaScript.

```js
var a = 1; // Function-scoped
let b = 2; // Block-scoped
const c = 3; // Block-scoped and cannot be reassigned
```

> :bulb: Prefer `let` and `const` to avoid scoping issues with `var`.

---

### Data Types

JavaScript has primitive and reference data types.

```js
let name = "John"; // string
let age = 25; // number
let isCool = true; // boolean
let car = null; // null
let x; // undefined
let id = Symbol(); // symbol
let big = 123n; // bigint
```

---

### Type Conversion & Coercion

You can convert between types manually or implicitly.

```js
Number("10"); // 10
String(100); // "100"
Boolean(0); // false
```

> :bulb: JavaScript automatically converts types in certain comparisons, e.g., `"5" == 5` is true.

---

### Template Literals

Template literals make string interpolation easy.

```js
const name = "Riju";
console.log(`Hello, ${name}!`); // Output: Hello, Riju!
```

---

### Operators

Operators perform arithmetic, comparison, and logical tasks.

```js
let x = 10;
x += 5; // 15
x > 10 && true; // true
x == "15"; // true (loose)
x === "15"; // false (strict)
```

---

### Ternary Operator

The ternary operator is shorthand for `if-else`.

```js
let age = 20;
let result = age >= 18 ? "Adult" : "Minor";
console.log(result); // "Adult"
```

---

### Loops

Loops let you execute code repeatedly.

```js
for (let i = 0; i < 3; i++) console.log(i);
while (x < 15) x++;
do {
  console.log("Run once");
} while (false);
```

---

### Conditional Statements

Used to make decisions in code.

```js
let score = 85;
if (score >= 90) console.log("Excellent");
else if (score >= 60) console.log("Good");
else console.log("Fail");
```

---

### Loop Control: break & continue

`break` stops a loop; `continue` skips one iteration.

```js
for (let i = 0; i < 5; i++) {
  if (i === 2) continue;
  if (i === 4) break;
  console.log(i); // 0,1,3
}
```

---

## ⚙️ 2. Functions & Scope

### Function Declaration vs Expression

```js
function add(a, b) {
  return a + b;
}
const sub = function (a, b) {
  return a - b;
};
```

Function declarations are hoisted, expressions are not.

---

### Parameters, Arguments, Return Values

```js
function greet(name) {
  return `Hello, ${name}`;
}
console.log(greet("Riju"));
```

Functions take parameters (placeholders) and return computed results.

---

### Default Parameters

```js
function power(base, exp = 2) {
  return base ** exp;
}
console.log(power(3)); // 9
```

---

### Arrow Functions

```js
const multiply = (x, y) => x * y;
console.log(multiply(2, 3)); // 6
```

> :bulb: Arrow functions do not bind their own `this` keyword.

---

### Scope & Hoisting

```js
let global = "outside";
function example() {
  let local = "inside";
  console.log(global);
}
example();
```

`var` is function-scoped, `let` and `const` are block-scoped. Functions are hoisted to the top of their scope.

---

### Closures

A closure remembers variables from its outer scope.

```js
function makeCounter() {
  let count = 0;
  return function () {
    return ++count;
  };
}
const counter = makeCounter();
console.log(counter()); // 1
console.log(counter()); // 2
```

---

### Callbacks & Higher-Order Functions

```js
function process(callback) {
  console.log("Start");
  callback();
}
process(() => console.log("Done"));
```

> :bulb: Callbacks allow async operations like loading data or handling events.

---

## 🧮 3. Data Structures & Manipulation

### Strings

```js
let text = "JavaScript";
console.log(text.slice(0, 4)); // Java
console.log(text.includes("Script")); // true
```

---

### Arrays

```js
const arr = [1, 2, 3];
arr.push(4);
arr.map((x) => x * 2); // [2,4,6,8]
```

---

### Objects

```js
const person = { name: "Riju", age: 22 };
console.log(person.name);
```

---

### Spread & Rest

```js
const arr1 = [1, 2];
const arr2 = [...arr1, 3];
function sum(...nums) {
  return nums.reduce((a, b) => a + b);
}
```

---

## 🧠 4. DOM Manipulation

### Selecting & Modifying Elements

```js
const title = document.getElementById("title");
title.textContent = "New Title";
```

---

### Events

```js
document
  .querySelector("button")
  .addEventListener("click", () => alert("Clicked!"));
```

> :bulb: Always attach event listeners after elements are loaded.

---

## 🌐 5. Browser APIs & Asynchronous JS

### JSON

```js
const data = { name: "Riju" };
const str = JSON.stringify(data);
console.log(JSON.parse(str));
```

---

### Fetch API

```js
fetch("https://api.github.com/users")
  .then((res) => res.json())
  .then((data) => console.log(data))
  .catch(console.error);
```

---

## ⚡ 6. ES6+ Modern Features

### Destructuring

```js
const user = { name: "Ava", age: 20 };
const { name, age } = user;
```

---

### Template Literals

```js
console.log(`Name: ${name}, Age: ${age}`);
```

---

### Modules

```js
// export const greet = () => console.log("Hi");
// import { greet } from './file.js';
```

---

## 🧱 7. OOP & Functional Programming

### Classes

```js
class Animal {
  constructor(name) {
    this.name = name;
  }
  speak() {
    console.log(`${this.name} makes noise.`);
  }
}
```

---

### Inheritance

```js
class Dog extends Animal {
  speak() {
    console.log(`${this.name} barks.`);
  }
}
```

---

### Functional Patterns

```js
[1, 2, 3].map((x) => x * 2).filter((x) => x > 3);
```

---

## ⏳ 8. Asynchronous Patterns

### Callbacks

```js
setTimeout(() => console.log("Done"), 1000);
```

---

### Promises

```js
new Promise((resolve) => resolve(42)).then(console.log);
```

---

### Async/Await

```js
async function loadData() {
  const res = await fetch("https://api.github.com");
  console.log(await res.json());
}
```

> :bulb: **Tip:** Practice each concept by building small apps (like counters, to-do lists, or API fetchers).

---
