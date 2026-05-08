<h1 align="Center"> 🔤 String, Array & Object Methods - JavaScript Cheatsheet</h1>

> :bulb: This is a quick reference for essential JavaScript methods for strings, arrays, and objects.

> :book: Official Docs : **[MDN String](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/String)** , **[MDN Array](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array)** , **[MDN Object](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Object)**

> :rocket: For study : **[JavaScript.info](https://javascript.info/)** , **[W3Schools](https://www.w3schools.com/js/)**

## 📑 Table of Contents

- [1. Loops](#1-loops)
- [2. String Methods](#2-string-methods)
- [3. Array Methods](#3-array-methods)
- [4. Object Methods](#4-object-methods)

---

## 1. Loops

### for

**When to use:** Classic loop when you need index control or known iteration count.

**What it does:** Executes code a specific number of times.

```js
for (let i = 0; i < 3; i++) {
  console.log(i) // 0, 1, 2
}

// Iterate array
const arr = ["a", "b", "c"]
for (let i = 0; i < arr.length; i++) {
  console.log(arr[i]) // a, b, c
}
```

---

### while

**When to use:** Loop when condition is unknown or based on dynamic condition.

**What it does:** Repeats while condition is true (checks before each iteration).

```js
let i = 0
while (i < 3) {
  console.log(i) // 0, 1, 2
  i++
}

// Read all items until null
let items = ["a", "b", null]
while (items[i] !== null) {
  console.log(items[i])
  i++
}
```

---

### do...while

**When to use:** When you need loop to run at least once regardless of condition.

**What it does:** Executes code once, then repeats while condition is true.

```js
let i = 0
do {
  console.log(i) // 0 (runs once even if condition false)
  i++
} while (i < 0)

// Practical: prompt until valid input
let input
do {
  input = prompt("Enter yes or no")
} while (input !== "yes" && input !== "no")
```

---

### for...of

**When to use:** Iterate over array/string/iterable values directly (most common modern loop).

**What it does:** Loops through iterable values, not indices.

```js
const fruits = ["apple", "banana", "cherry"]
for (const fruit of fruits) {
  console.log(fruit) // apple, banana, cherry
}

// With index (using entries)
for (const [index, fruit] of fruits.entries()) {
  console.log(index, fruit) // 0 apple, 1 banana, 2 cherry
}

// Strings
for (const char of "hi") {
  console.log(char) // h, i
}
```

---

### for...in

**When to use:** Iterate over object keys or array indices.

**What it does:** Loops through enumerable properties (keys/indices).

```js
const obj = { a: 1, b: 2, c: 3 }
for (const key in obj) {
  console.log(key, obj[key]) // a 1, b 2, c 3
}

// Array (gives indices, not values)
const arr = ["x", "y", "z"]
for (const index in arr) {
  console.log(index) // 0, 1, 2
}
```

> [!NOTE]
> - Cannot break/return early (use `some` or `for` loop if needed)
> - Use `for...of` if you need to break

> [!NOTE]
> **Loop Selection Guide:**
> - `for` - when you need index or custom control
> - `for...of` - iterate values (most common for arrays)
> - `for...in` - iterate keys (for objects)
> - `forEach` - when you need side effects per element
> - `while` - when condition is dynamic/unknown

---

### map

**When to use:** Transform each element and create new array.

**What it does:** Returns new array with transformed elements.

```js
const nums = [1, 2, 3]
const doubled = nums.map(n => n * 2)
console.log(doubled) // [2, 4, 6]
console.log(nums)    // [1, 2, 3] (unchanged)

// Practical: extract specific property
const users = [{name: "A"}, {name: "B"}]
const names = users.map(u => u.name)
console.log(names) // ["A", "B"]
```

> [!NOTE]
> - **Returns new array**, original unchanged
> - Always returns same length as original
> - Use `map` when you transform/change values; use `forEach` when you just need side effects

---

### filter

**When to use:** Keep only elements that pass a test.

**What it does:** Returns new array with matching elements.

```js
const nums = [1, 2, 3, 4, 5]
const even = nums.filter(n => n % 2 === 0)
console.log(even) // [2, 4]

const words = ["hi", "hello", "hey"]
const long = words.filter(w => w.length > 3)
console.log(long) // ["hello"]
```

> [!NOTE]
> - **Returns new array**, original unchanged
> - Returns subset (can be empty or full length)

---

### find

**When to use:** Get first element that matches condition.

**What it does:** Returns first matching element or undefined.

```js
const users = [
  {id: 1, name: "Alice"},
  {id: 2, name: "Bob"},
  {id: 3, name: "Charlie"}
]

console.log(users.find(u => u.id === 2)) // {id: 2, name: "Bob"}
console.log(users.find(u => u.name === "Alice")) // {id: 1, name: "Alice"}
console.log(users.find(u => u.id === 99)) // undefined
```

> [!NOTE]
> - Returns **first match only** (not all matches)
> - Returns undefined if no match
> - Use `filter()` to get ALL matching elements, `find()` for first only

---

### findIndex

**When to use:** Get index of first matching element.

**What it does:** Returns index of first match or -1.

```js
const arr = ["a", "b", "c", "b"]
console.log(arr.findIndex(x => x === "b")) // 1
console.log(arr.findIndex(x => x === "z")) // -1
```

---

### indexOf

**When to use:** Find index of element (primitive values).

**What it does:** Returns first index or -1 if not found.

```js
const arr = ["a", "b", "c", "b"]
console.log(arr.indexOf("b"))   // 1 (first occurrence)
console.log(arr.indexOf("z"))  // -1
console.log(arr.indexOf("b", 2)) // 3 (search from index 2)
```

> [!NOTE]
> - Use for **primitive values** (strings, numbers)
> - Use `findIndex` for **objects** or complex conditions
> - Use `includes()` when you just need true/false (simpler)

---

### includes

**When to use:** Check if array contains element.

**What it does:** Returns true/false.

```js
const arr = [1, 2, 3]
console.log(arr.includes(2))   // true
console.log(arr.includes(5))   // false
console.log(arr.includes(2, 2)) // false (search from index 2)
```

---

### some

**When to use:** Check if ANY element passes test.

**What it does:** Returns true if any match, else false.

```js
const nums = [1, 2, 3, 4]
console.log(nums.some(n => n > 3)) // true (4 > 3)
console.log(nums.some(n => n > 10)) // false
console.log(nums.some(n => n % 2 === 0)) // true (2, 4 are even)
```

---

### every

**When to use:** Check if ALL elements pass test.

**What it does:** Returns true if all match, else false.

```js
const nums = [2, 4, 6]
console.log(nums.every(n => n % 2 === 0)) // true (all even)
console.log(nums.every(n => n > 0))       // true

const mixed = [2, 3, 4]
console.log(mixed.every(n => n % 2 === 0)) // false (3 is odd)
```

---

### reduce

**When to use:** Reduce array to single value (sum, max, group, etc.).

**What it does:** Accumulates values using callback.

```js
const nums = [1, 2, 3, 4]

// Sum
console.log(nums.reduce((acc, n) => acc + n, 0)) // 10

// Max
console.log(nums.reduce((a, b) => a > b ? a : b)) // 4

// Product
console.log(nums.reduce((acc, n) => acc * n, 1)) // 24

// Count occurrences
const fruits = ["apple", "banana", "apple", "orange", "banana"]
const count = fruits.reduce((acc, fruit) => {
  acc[fruit] = (acc[fruit] || 0) + 1
  return acc
}, {})
console.log(count) // {apple: 2, banana: 2, orange: 1}
```

> [!NOTE]
> - Callback: `(accumulator, current, index, array) => newAccumulator`
> - Second arg to `reduce` is initial value (important!)

---

### slice

**When to use:** Extract portion of array.

**What it does:** Returns new array with extracted portion.

```js
const arr = [0, 1, 2, 3, 4]
console.log(arr.slice(1, 3))   // [1, 2] (index 1 to 2)
console.log(arr.slice(2))      // [2, 3, 4] (from index 2)
console.log(arr.slice(-2))     // [3, 4] (last 2)
console.log(arr.slice())       // [0, 1, 2, 3, 4] (copy array)
```

> [!NOTE]
> - **Does not mutate** original array
> - Returns **new array**
> - Use `arr.slice()` without args to create a copy of array

---

### concat

**When to use:** Combine arrays together.

**What it does:** Returns new merged array.

```js
const a = [1, 2]
const b = [3, 4]
console.log(a.concat(b))    // [1, 2, 3, 4]
console.log([...a, ...b])   // [1, 2, 3, 4] (spread alternative)
console.log(a.concat([3], [4, 5])) // [1, 2, 3, 4, 5]
```

> [!NOTE]
> - **Does not mutate** original
> - Accepts multiple arrays/values

---

### flat

**When to use:** Flatten nested arrays.

**What it does:** Returns new array with nested arrays merged.

```js
const nested = [1, [2, 3], [[4], 5]]
console.log(nested.flat())        // [1, 2, 3, [4], 5] (one level)
console.log(nested.flat(2))       // [1, 2, 3, 4, 5] (two levels)
console.log([1, 2, [3, [4, [5]]]].flat(Infinity)) // [1, 2, 3, 4, 5] (all levels)
```

---

### sort

**When to use:** Sort array elements.

**What it does:** Sorts in place and returns sorted array.

```js
const nums = [3, 1, 4, 1, 5]
console.log(nums.sort()) // [1, 1, 3, 4, 5]

// Custom sort (ascending)
nums.sort((a, b) => a - b)
console.log(nums) // [1, 3, 4, 5]

// Descending
nums.sort((a, b) => b - a)
console.log(nums) // [5, 4, 3, 1]

// Strings (alphabetical)
const names = ["Charlie", "Alice", "Bob"]
names.sort((a, b) => a.localeCompare(b))
console.log(names) // ["Alice", "Bob", "Charlie"]
```

> [!NOTE]
> - **Mutates** original array
> - Default: converts to strings then compares
> - Always provide comparison function for numbers

---

### reverse

**When to use:** Reverse array order.

**What it does:** Reverses array in place.

```js
const arr = [1, 2, 3]
console.log(arr.reverse()) // [3, 2, 1]
console.log(arr)           // [3, 2, 1] (mutated!)
```

> [!NOTE]
> - **Mutates** original array
> - Use `[...arr].reverse()` to avoid mutation

---

### splice

**When to use:** Add, remove, or replace elements anywhere in array.

**What it does:** Modifies array in place, returns removed elements.

```js
const arr = ["a", "b", "c", "d"]

// Remove (start, deleteCount)
arr.splice(1, 2) // remove 2 items from index 1
console.log(arr) // ["a", "d"]

// Add (start, deleteCount, items...)
const colors = ["red", "green", "blue"]
colors.splice(1, 0, "yellow", "orange")
console.log(colors) // ["red", "yellow", "orange", "green", "blue"]

// Replace
const nums = [1, 2, 3]
nums.splice(1, 1, 99)
console.log(nums) // [1, 99, 3]

// Get removed items
const arr2 = [1, 2, 3, 4, 5]
const removed = arr2.splice(2, 2)
console.log(removed) // [3, 4]
```

---

### fill

**When to use:** Fill array with specific value.

**What it does:** Replaces elements with value (in place).

```js
const arr = new Array(5)
console.log(arr.fill(0))         // [0, 0, 0, 0, 0]

const nums = [1, 2, 3, 4, 5]
nums.fill(0, 1, 3)               // fill with 0, from index 1 to 2
console.log(nums)               // [1, 0, 0, 4, 5]
```

> [!NOTE]
> - **Mutates** original array
> - Use for creating fixed-size arrays or resetting

---

## 4. Object Methods

### Object.keys()

**When to use:** Get all keys of an object.

**What it does:** Returns array of keys.

```js
const obj = { a: 1, b: 2, c: 3 }
console.log(Object.keys(obj)) // ["a", "b", "c"]

// Iterate keys
Object.keys(obj).forEach(key => {
  console.log(key, obj[key])
})
```

---

### Object.values()

**When to use:** Get all values of an object.

**What it does:** Returns array of values.

```js
const obj = { a: 1, b: 2, c: 3 }
console.log(Object.values(obj)) // [1, 2, 3]
```

---

### Object.entries()

**When to use:** Get key-value pairs as array.

**What it does:** Returns array of [key, value] arrays.

```js
const obj = { a: 1, b: 2 }
console.log(Object.entries(obj)) // [["a", 1], ["b", 2]]

// Convert to Map
const map = new Map(Object.entries(obj))
```

---

### Object.assign()

**When to use:** Copy/merge objects.

**What it does:** Copies properties from source to target.

```js
const target = { a: 1 }
const source = { b: 2, c: 3 }
console.log(Object.assign(target, source)) // { a: 1, b: 2, c: 3 }

// Copy object
const copy = Object.assign({}, original)

// Merge multiple
const merged = Object.assign({}, {a: 1}, {b: 2})
```

> [!NOTE]
> - Mutates first argument
> - Use spread for cleaner merging: `{...a, ...b}`

---

### Object.create()

**When to use:** Create object with specific prototype.

**What it does:** Returns new object with given prototype.

```js
const proto = { greet() { return "hello" } }
const obj = Object.create(proto)
console.log(obj.greet()) // hello

// Create empty object (no prototype)
const empty = Object.create(null)
```

---

### Object.freeze()

**When to use:** Make object immutable (cannot add/modify/delete properties).

**What it does:** Prevents modifications, returns same object.

```js
const obj = { a: 1 }
Object.freeze(obj)
obj.a = 2          // silently fails in non-strict mode
obj.b = 3          // silently fails
console.log(obj)  // { a: 1 }

console.log(Object.isFrozen(obj)) // true
```

> [!NOTE]
> - Shallow freeze (nested objects still modifiable unless frozen too)
> - Use `Object.isFrozen()` to check

---

### Object.seal()

**When to use:** Prevent adding/removing properties but allow modifying existing.

**What it does:** Seals object, returns same object.

```js
const obj = { a: 1 }
Object.seal(obj)
obj.a = 2        // allowed
obj.b = 3        // silently fails (cannot add)
delete obj.a    // silently fails (cannot delete)
console.log(obj) // { a: 2 }

console.log(Object.isSealed(obj)) // true
```

> [!NOTE]
> - Use `Object.isSealed()` to check
> - Different from freeze (can still modify values)

---

### Object.hasOwn()

**When to use:** Check if property exists directly on object (not inherited).

**What it does:** Returns true/false.

```js
const obj = { a: 1 }
console.log(Object.hasOwn(obj, "a"))    // true
console.log(Object.hasOwn(obj, "toString")) // false (inherited)

const proto = { inherited: 1 }
const child = Object.create(proto)
child.own = 2
console.log(Object.hasOwn(child, "own"))     // true
console.log(Object.hasOwn(child, "inherited")) // false
```

> [!NOTE]
> - Modern replacement for `hasOwnProperty()`
> - Safer with objects that have custom hasOwnProperty

---

### delete

**When to use:** Remove property from object.

**What it does:** Deletes property, returns true/false.

```js
const obj = { a: 1, b: 2 }
console.log(delete obj.a) // true
console.log(obj)          // { b: 2 }

console.log(delete obj.x) // true (non-existent property)
```

> [!NOTE]
> - Returns `false` only if property is non-configurable (rare)
> - Use `Object.assign()` or spread to exclude: `{...obj, unwanted: undefined}`

---

### Spread `...`

**When to use:** Copy or merge objects/arrays.

**What it does:** Expands iterable into individual elements.

```js
// Copy object
const original = { a: 1, b: 2 }
const copy = { ...original }

// Merge objects
const merged = { ...{ a: 1 }, ...{ b: 2 } } // { a: 1, b: 2 }

// Add/modify properties
const updated = { ...original, c: 3, a: 99 }

// Omit property
const { a, ...rest } = original // omit 'a'
console.log(rest) // { b: 2 }

// Array copy
const arr = [1, 2, 3]
const arrCopy = [...arr]
const combined = [...arr1, ...arr2]
```

> [!NOTE]
> - Shallow copy only (nested objects still reference)
> - Cleaner than `Object.assign()`

---

### Destructuring

**When to use:** Extract values from objects/arrays into variables.

**What it does:** Unpacks values into named variables.

```js
// Object destructuring
const user = { name: "Alice", age: 25, city: "NYC" }
const { name, age } = user
console.log(name) // Alice
console.log(age)  // 25

// Rename
const { name: userName } = user

// Default values
const { country = "USA" } = user

// Array destructuring
const [first, second] = [1, 2, 3]
console.log(first) // 1
console.log(second) // 2

// Skip elements
const [a, , c] = [1, 2, 3]
console.log(a, c) // 1, 3

// Rest pattern
const [head, ...tail] = [1, 2, 3, 4]
console.log(head) // 1
console.log(tail) // [2, 3, 4]
```

---

> [!NOTE]
> ✅ **Quick Reference**
>
> - **Strings**: Immutable - all methods return new strings
> - **Arrays**: Most methods don't mutate original (except: push, pop, unshift, shift, sort, reverse, splice, fill)
> - **Objects**: Use spread `{...obj}` for clean copy/merge
> - **Loops**: Use `for...of` for arrays, `for...in` for objects

> [!NOTE]
> ✅ **Common Patterns**
>
> - **Find element in array**: Use `find()` for objects, `indexOf()` for primitives
> - **Check if exists**: Use `includes()` for true/false check
> - **Transform array**: Use `map()` to change values, `filter()` to keep subset
> - **Search + modify**: Use `find()` then modify result directly
> - **Copy array**: Use `[...arr]` or `arr.slice()`
> - **Copy object**: Use `{...obj}` (shallow copy)
> - **Remove item**: Use `filter()` to keep except item, or `splice()` for specific index