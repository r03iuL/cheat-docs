<h1 align="Center"> ⚡ JavaScript Async Operations Cheatsheet</h1>

> :bulb: This is a comprehensive reference for asynchronous JavaScript operations.

> :book: Official Docs : **[MDN Async](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/async_function)** , **[MDN Fetch](https://developer.mozilla.org/en-US/docs/Web/API/Fetch_API)**

> :rocket: For study : **[JavaScript.info Async](https://javascript.info/async)** , **[MDN Using Promises](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Guide/Using_promises)**

## 📑 Table of Contents

- [1. Timing Functions](#1-timing-functions)
- [2. Event Loop & Execution Order](#2-event-loop--execution-order)
- [3. Callbacks Deep Dive](#3-callbacks-deep-dive)
- [4. Promises (Detailed)](#4-promises-detailed)
- [5. Promise Methods](#5-promise-methods)
- [6. Async/Await (Detailed)](#6-asyncawait-detailed)
- [7. Fetch API (Advanced)](#7-fetch-api-advanced)
- [8. requestAnimationFrame](#8-requestanimationframe)
- [9. IntersectionObserver](#9-intersectionobserver)
- [10. MutationObserver](#10-mutationobserver)
- [11. Web Workers](#11-web-workers)
- [12. Async Generators](#12-async-generators)

---

## 1. Timing Functions

### setTimeout / clearTimeout

**When to use:** Execute code after a delay.

**What it does:** Schedules function to run after specified milliseconds.

```js
// Basic setTimeout
const timeoutId = setTimeout(() => {
  console.log("Runs after 1 second");
}, 1000);

// Cancel the timeout
clearTimeout(timeoutId);
```

**With parameters:**

```js
function greet(name, time) {
  console.log(`Hello ${name} after ${time}ms`);
}
setTimeout(greet, 1000, "Alice", 1000);
```

---

### setInterval / clearInterval

**When to use:** Execute code repeatedly at fixed intervals.

**What it does:** Runs function repeatedly every X milliseconds.

```js
// Basic interval
const intervalId = setInterval(() => {
  console.log("Runs every second");
}, 1000);

// Stop after 5 seconds
setTimeout(() => clearInterval(intervalId), 5000);

// Counter example
let count = 0;
const counter = setInterval(() => {
  console.log(++count);
  if (count >= 5) clearInterval(counter);
}, 500);
// Output: 1, 2, 3, 4, 5
```

---

### Recursive setTimeout Pattern

**When to use:** When you need variable delay between executions or to prevent overlapping.

**What it does:** Creates a self-adjusting interval.

```js
function pollServer() {
  fetch('/api/status')
    .then(res => res.json())
    .then(data => {
      console.log("Server status:", data);
      // Wait 2 seconds before next check
      setTimeout(pollServer, 2000);
    })
    .catch(err => {
      console.error("Poll failed, retrying in 5s");
      setTimeout(pollServer, 5000);
    });
}

pollServer();
```

> [!NOTE]
> - `setTimeout` is better than `setInterval` for API polling
> - Prevents overlapping if operation takes longer than interval

---

## 2. Event Loop & Execution Order

### Understanding the Event Loop

JavaScript is single-threaded but handles async via the event loop.

```js
console.log("1. Start");

setTimeout(() => console.log("2. Timeout"), 0);

Promise.resolve().then(() => console.log("3. Promise"));

queueMicrotask(() => console.log("4. Microtask"));

console.log("5. End");

// Output: 1, 5, 3, 4, 2
```

> [!NOTE]
> - **Synchronous code** runs first (1, 5)
> - **Microtasks** (promises, queueMicrotask) run before macrotasks (3, 4)
> - **Macrotasks** (setTimeout, setInterval, I/O) run after microtasks (2)

---

### queueMicrotask

**When to use:** Schedule a task in the microtask queue (runs after current sync code, before next paint).

**What it does:** Adds function to microtask queue.

```js
console.log("Start");

queueMicrotask(() => console.log("Microtask 1"));

Promise.resolve().then(() => console.log("Promise 1"));

console.log("End");

// Output: Start, End, Promise 1, Microtask 1
```

> [!NOTE]
> - Useful for async operations that should complete before rendering
> - Same priority as Promise microtasks

---

## 3. Callbacks Deep Dive

### Error-First Callbacks

**When to use:** Standard pattern for Node.js-style async functions.

**What it does:** First parameter is error, second is result.

```js
function readFile(filename, callback) {
  if (!filename) {
    callback(new Error("Filename required"), null);
    return;
  }
  
  const content = "File content";
  callback(null, content);
}

readFile("test.txt", (err, data) => {
  if (err) {
    console.error("Error:", err.message);
    return;
  }
  console.log("Data:", data);
});
```

---

### Callback Hell (Avoid!)

```js
// BAD - Nested callbacks (pyramid of doom)
getData((a) => {
  getMoreData(a, (b) => {
    getEvenMore(b, (c) => {
      console.log(c);
    });
  });
});

// GOOD - Use Promises or async/await instead
const result = await getData();
const more = await getMoreData(result);
```

---

## 4. Promises (Detailed)

### Promise States

A promise can be in one of three states:

```js
const promise = new Promise((resolve, reject) => {
  // pending - initial state
  // resolve(value) - fulfilled
  // reject(error) - rejected
});
```

| State | Description |
|-------|-------------|
| `pending` | Initial state, not fulfilled or rejected |
| `fulfilled` | Operation completed successfully |
| `rejected` | Operation failed |

---

### Creating Promises

```js
// From scratch
const myPromise = new Promise((resolve, reject) => {
  const success = true;
  if (success) {
    resolve({ data: "Success!" });
  } else {
    reject(new Error("Failed"));
  }
});

// Using Promise.resolve/reject (convenience)
const resolved = Promise.resolve("Already resolved");
const rejected = Promise.reject(new Error("Already rejected"));

// Promise.wrap for non-promise functions
const promisified = (fn) => (...args) => 
  new Promise((resolve, reject) => 
    fn(...args, (err, result) => 
      err ? reject(err) : resolve(result)
    )
  );
```

---

### then(), catch(), finally()

```js
const promise = Promise.resolve("data");

// then - runs when promise resolves
promise
  .then(result => {
    console.log(result); // "data"
    return result.toUpperCase();
  })
  .then(upper => {
    console.log(upper); // "DATA"
  });

// catch - handles rejections
promise
  .then(result => {
    throw new Error("Oops");
  })
  .catch(error => {
    console.error(error.message); // "Oops"
  });

// finally - runs regardless of outcome
promise
  .then(result => console.log(result))
  .catch(error => console.error(error))
  .finally(() => console.log("Done"));
```

---

### Promise Chaining

```js
Promise.resolve(1)
  .then(x => x + 1)      // 2
  .then(x => x * 2)      // 4
  .then(x => {
    if (x > 10) throw new Error("Too big");
    return x;
  })
  .then(x => console.log(x)) // 4
  .catch(err => console.error(err));
```

> [!NOTE]
> - Each `.then()` returns a new promise
> - Return values are passed to next `.then()`
- Throw in `.then()` triggers `.catch()`

---

## 5. Promise Methods

### Promise.all()

**When to use:** Wait for ALL promises to resolve (fail fast - if any fails, entire thing fails).

**What it does:** Returns single promise that resolves to array of results.

```js
const urls = [
  '/api/users',
  '/api/posts',
  '/api/comments'
];

const requests = urls.map(url => fetch(url).then(r => r.json()));

Promise.all(requests)
  .then(([users, posts, comments]) => {
    console.log(users, posts, comments);
  })
  .catch(err => console.error("One failed:", err));
```

---

### Promise.allSettled()

**When to use:** Wait for ALL promises to settle (regardless of success/failure).

**What it does:** Returns array of results with status.

```js
Promise.allSettled([
  Promise.resolve("Success"),
  Promise.reject("Failed"),
  Promise.resolve("Another success")
]).then(results => {
  results.forEach((result, i) => {
    if (result.status === "fulfilled") {
      console.log(`Promise ${i}: ${result.value}`);
    } else {
      console.log(`Promise ${i}: ${result.reason}`);
    }
  });
});
```

---

### Promise.race()

**When to use:** Get result of the FIRST promise to settle (resolve or reject).

**What it does:** Returns promise that resolves/rejects with first result.

```js
function delay(ms, value) {
  return new Promise(resolve => setTimeout(() => resolve(value), ms));
}

Promise.race([
  delay(100, "fast"),
  delay(1000, "slow")
]).then(result => console.log(result)); // "fast"

// Timeout pattern
const timeout = new Promise((_, reject) => 
  setTimeout(() => reject(new Error("Timeout")), 5000)
);

Promise.race([fetch('/api/slow'), timeout])
  .catch(err => console.error(err.message)); // "Timeout" if too slow
```

---

### Promise.any()

**When to use:** Get FIRST promise that resolves successfully (ignores rejections until all fail).

**What it does:** Returns first fulfilled promise.

```js
Promise.any([
  new Promise((_, reject) => setTimeout(() => reject("a"), 1000)),
  new Promise(resolve => setTimeout(() => resolve("b"), 500)),
  new Promise((_, reject) => setTimeout(() => reject("c"), 200))
]).then(result => console.log(result)); // "b" (fastest to resolve)
```

---

## 6. Async/Await (Detailed)

### Basic Usage

```js
// async function declaration
async function fetchData() {
  const response = await fetch('/api/data');
  const data = await response.json();
  return data;
}

// arrow function
const getData = async () => {
  const data = await fetch('/api/data');
  return data.json();
};

// function expression
const getData = async function() {
  // ...
};
```

> [!NOTE]
> - `async` functions always return a Promise
> - `await` pauses execution until Promise resolves

---

### Sequential vs Parallel Execution

```js
// Sequential - each waits for previous (slow)
async function sequential() {
  const user = await fetch('/user').then(r => r.json());
  const posts = await fetch('/posts').then(r => r.json());
  const comments = await fetch('/comments').then(r => r.json());
  return { user, posts, comments };
}

// Parallel - all start together (fast)
async function parallel() {
  const [userRes, postsRes, commentsRes] = await Promise.all([
    fetch('/user'),
    fetch('/posts'),
    fetch('/comments')
  ]);
  
  const user = await userRes.json();
  const posts = await postsRes.json();
  const comments = await commentsRes.json();
  
  return { user, posts, comments };
}
```

---

### Error Handling

```js
// try/catch
async function fetchWithErrorHandling() {
  try {
    const res = await fetch('/api/data');
    if (!res.ok) throw new Error(`HTTP ${res.status}`);
    return await res.json();
  } catch (error) {
    console.error("Fetch failed:", error.message);
    throw error; // re-throw if needed
  }
}

// Error boundaries with .catch()
async function safeFetch(url) {
  try {
    const res = await fetch(url);
    return await res.json();
  } catch (error) {
    return { error: error.message };
  }
}

// Throw custom errors
async function validate(value) {
  if (!value) throw new ValidationError("Value required");
  return value;
}
```

---

### Concurrent with Limit (Batch Processing)

```When to use:** Process many items but limit concurrency.

**What it does:** Limits number of simultaneous operations.

```js
async function processWithLimit(tasks, limit) {
  const results = [];
  const executing = [];
  
  for (const task of tasks) {
    const promise = task().then(result => {
      executing.splice(executing.indexOf(promise), 1);
      return result;
    });
    
    results.push(promise);
    executing.push(promise);
    
    if (executing.length >= limit) {
      await Promise.race(executing);
    }
  }
  
  return Promise.all(results);
}

// Usage
const urls = [...Array(100).keys()].map(i => () => fetch(`/api/${i}`));
const results = await processWithLimit(urls, 5); // max 5 at a time
```

---

## 7. Fetch API (Advanced)

### Basic Usage

```js
// GET
fetch('/api/data')
  .then(res => res.json())
  .then(data => console.log(data));

// POST
fetch('/api/users', {
  method: 'POST',
  headers: {
    'Content-Type': 'application/json'
  },
  body: JSON.stringify({ name: 'Alice' })
});

// Response methods
const res = await fetch('/api/data');
const json = await res.json();
const text = await res.text();
const blob = await res.blob();
```

---

### Request Object

```js
const request = new Request('/api/data', {
  method: 'POST',
  headers: {
    'Content-Type': 'application/json',
    'Authorization': 'Bearer token'
  },
  body: JSON.stringify({ name: 'Bob' }),
  mode: 'cors',           // 'same-origin', 'cors', 'no-cors'
  credentials: 'include',  // 'omit', 'same-origin', 'include'
  cache: 'no-cache'        // 'default', 'no-store', 'reload'
});

const response = await fetch(request);
```

---

### Headers

```js
// Create headers
const headers = new Headers({
  'Content-Type': 'application/json',
  'X-Custom-Header': 'value'
});

// Append
headers.append('Accept', 'application/json');

// Check
headers.has('Content-Type');

// Get
headers.get('Content-Type');

// Delete
headers.delete('X-Custom-Header');

// Use in fetch
fetch('/api/data', { headers });
```

---

### AbortController (Cancel Requests)

```js
const controller = new AbortController();
const signal = controller.signal;

fetch('/api/large-data', { signal })
  .then(response => response.json())
  .catch(err => {
    if (err.name === 'AbortError') {
      console.log('Request cancelled');
    } else {
      console.error('Fetch error:', err);
    }
  });

// Cancel after 5 seconds
setTimeout(() => controller.abort(), 5000);
```

---

### Common Fetch Patterns

```js
// Retry with exponential backoff
async function fetchWithRetry(url, retries = 3) {
  for (let i = 0; i < retries; i++) {
    try {
      const res = await fetch(url);
      if (!res.ok) throw new Error(`HTTP ${res.status}`);
      return await res.json();
    } catch (err) {
      if (i === retries - 1) throw err;
      await new Promise(r => setTimeout(r, 1000 * (i + 1)));
    }
  }
}

// Download progress
async function downloadWithProgress(url) {
  const response = await fetch(url);
  const reader = response.body.getReader();
  const contentLength = +response.headers.get('Content-Length');
  let receivedLength = 0;
  const chunks = [];
  
  while (true) {
    const { done, value } = await reader.read();
    if (done) break;
    chunks.push(value);
    receivedLength += value.length;
    console.log(`Progress: ${(receivedLength / contentLength * 100).toFixed(1)}%`);
  }
  
  return new Uint8Array(chunks.reduce((a, b) => a.concat(b)));
}
```

---

## 8. requestAnimationFrame

**When to use:** Smooth animations (runs before next paint, ~60fps).

**What it does:** Schedules callback before next repaint.

```js
// Basic animation
function animate() {
  // Update position
  element.style.left = `${position}px`;
  
  // Continue animation
  if (position < 100) {
    requestAnimationFrame(animate);
  }
}
requestAnimationFrame(animate);

// With timestamp (accurate timing)
function animate(timestamp) {
  const elapsed = timestamp - startTime;
  // Use elapsed time for smooth animation
  element.style.transform = `translateX(${elapsed * 0.1}px)`;
  requestAnimationFrame(animate);
}

// Stop animation
let animationId;
function startAnimation() {
  animationId = requestAnimationFrame(animate);
}
function stopAnimation() {
  cancelAnimationFrame(animationId);
}
```

> [!NOTE]
> - Better than `setInterval` for animations
> - Pauses when tab is not visible (saves CPU)
> - Timestamp is in milliseconds

---

## 9. IntersectionObserver

**When to use:** Detect when element enters/leaves viewport (lazy loading, infinite scroll).

**What it does:** Asynchronously observes element intersection.

```js
// Lazy load images
const imageObserver = new IntersectionObserver((entries, observer) => {
  entries.forEach(entry => {
    if (entry.isIntersecting) {
      const img = entry.target;
      img.src = img.dataset.src; // Load from data-src
      img.classList.remove('lazy');
      observer.unobserve(img); // Stop watching
    }
  });
}, {
  root: null,           // viewport
  rootMargin: '0px',    // margin around root
  threshold: 0.1       // 10% visible triggers
});

document.querySelectorAll('img[data-src]').forEach(img => {
  imageObserver.observe(img);
});
```

---

### More Observer Options

```js
// Infinite scroll
const infiniteScroll = new IntersectionObserver((entries) => {
  if (entries[0].isIntersecting) {
    loadMoreItems();
  }
}, { rootMargin: '100px' });

infiniteScroll.observe(document.querySelector('.sentinel'));

// Track element visibility
const visibilityObserver = new IntersectionObserver((entries) => {
  entries.forEach(entry => {
    if (entry.isIntersecting) {
      console.log('Element is visible!');
    }
  });
}, { threshold: 0.5 }); // 50% visible

visibilityObserver.observe(document.querySelector('.track-me'));
```

---

## 10. MutationObserver

**When to use:** Watch for DOM changes (dynamic content, form validation).

**What it does:** Monitors DOM mutations.

```js
const observer = new MutationObserver((mutations) => {
  mutations.forEach(mutation => {
    console.log('Type:', mutation.type);
    console.log('Target:', mutation.target);
    console.log('Old value:', mutation.oldValue);
  });
});

observer.observe(document.querySelector('#container'), {
  childList: true,    // changes to children
  subtree: true,      // deep monitoring
  attributes: true,   // attribute changes
  attributeOldValue: true, // old attribute value
  characterData: true, // text changes
  characterDataOldValue: true
});

// Stop observing
observer.disconnect();

// Observe specific attributes
observer.observe(element, {
  attributes: true,
  attributeFilter: ['class', 'data-value'] // only these
});
```

---

## 11. Web Workers

### Dedicated Worker

```js
// main.js
const worker = new Worker('worker.js');

worker.postMessage({ type: 'compute', data: [1, 2, 3] });

worker.onmessage = (event) => {
  console.log('Result:', event.data);
};

worker.onerror = (error) => {
  console.error('Worker error:', error);
};

// Terminate when done
worker.terminate();

// worker.js (separate file)
self.onmessage = (event) => {
  const { type, data } = event.data;
  
  if (type === 'compute') {
    const result = data.reduce((a, b) => a + b, 0);
    self.postMessage(result);
  }
};
```

---

### Inline Worker (Blob)

```js
const workerCode = `
  self.onmessage = (e) => {
    const result = e.data * 2;
    self.postMessage(result);
  };
`;

const blob = new Blob([workerCode], { type: 'application/javascript' });
const worker = new Worker(URL.createObjectURL(blob));

worker.postMessage(5);
worker.onmessage = (e) => console.log(e.data); // 10
```

---

### Shared Workers

```js
// shared-worker.js
const connections = new Set();

self.onconnect = (event) => {
  const port = event.ports[0];
  connections.add(port);
  port.onmessage = (e) => {
    connections.forEach(c => c.postMessage(e.data));
  };
};

// main.js
const worker = new SharedWorker('shared-worker.js');
worker.port.postMessage('Hello');
worker.port.onmessage = (e) => console.log(e.data);
```

---

## 12. Async Generators

### Basic Async Generator

```When to use:** Handle asynchronous streaming data (files, API responses).

**What it does:** Combines generators with async/await.

```js
async function* asyncGenerator() {
  yield await Promise.resolve(1);
  yield await Promise.resolve(2);
  yield await Promise.resolve(3);
}

async function main() {
  for await (const value of asyncGenerator()) {
    console.log(value); // 1, 2, 3
  }
}
```

---

### Async Generator with Fetch

```js
async function* fetchPages(urls) {
  for (const url of urls) {
    const response = await fetch(url);
    const data = await response.json();
    yield { url, data };
  }
}

async function main() {
  for await (const page of fetchPages(['/api/1', '/api/2'])) {
    console.log(`Loaded: ${page.url}`, page.data);
  }
}
```

---

### Async Iterator Manual

```js
const asyncIterator = {
  current: 0,
  async next() {
    if (this.current < 5) {
      return { value: this.current++, done: false };
    }
    return { done: true };
  }
};

for await (const value of asyncIterator) {
  console.log(value); // 0, 1, 2, 3, 4
}
```

---

## Quick Reference

| Method/Feature | Use Case |
|---------------|---------|
| `setTimeout` | Delay execution |
| `setInterval` | Repeat execution |
| `Promise.all` | Wait for all (fail fast) |
| `Promise.allSettled` | Wait for all (never fails) |
| `Promise.race` | First to settle wins |
| `Promise.any` | First fulfilled wins |
| `fetch` | HTTP requests |
| `AbortController` | Cancel requests |
| `requestAnimationFrame` | Smooth animations |
| `IntersectionObserver` | Viewport detection |
| `MutationObserver` | DOM change detection |
| `Web Workers` | Background processing |
| `Async Generators` | Streaming data |

---

> [!NOTE]
> ✅ **Key Takeaways**
>
> - Use `async/await` over raw promises for readability
> - Use `Promise.all` for parallel operations, `Promise.allSettled` when you need all results
> - Use `AbortController` to cancel long-running operations
> - Use `requestAnimationFrame` for animations (not setTimeout)
> - Use `IntersectionObserver` for lazy loading (more efficient than scroll events)