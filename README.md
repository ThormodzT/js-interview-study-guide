## Understanding JavaScript

### 1. What is JavaScript?

JavaScript is a **high-level, interpreted programming language** used primarily for **web development**. It enables interactive web pages and runs in the browser but can also be used on the server with environments like **Node.js**.

### 2. What is ECMAScript?

ECMAScript (ES) is the **standard** that defines JavaScript’s features and syntax. ECMAScript updates (e.g., **ES6, ES7, ES8**) introduce new functionalities like **arrow functions, classes, template literals**, and more.

### 3. Variable Declarations: `var`, `let`, and `const`

| Keyword | Scope | Hoisting | Can be Reassigned? | Can be Redeclared? |
|---------|--------|----------|-------------------|--------------------|
| `var`   | Function-scoped | Yes (initialized as `undefined`) | Yes | Yes |
| `let`   | Block-scoped | Yes (not initialized) | Yes | No |
| `const` | Block-scoped | Yes (not initialized) | No | No |

Example:
```javascript
console.log(x); // Undefined (hoisting)
var x = 10;

console.log(y); // ReferenceError
let y = 20;
```

### 4. Hoisting and Its Types

**Hoisting** moves variable and function declarations to the top of their scope before execution.
- **Variable Hoisting:** Variables declared with `var` are hoisted but initialized with `undefined`, while `let` and `const` are hoisted but remain **uninitialized**.
- **Function Hoisting:** Function declarations are fully hoisted, allowing them to be called before they are defined.

Example:
```javascript
hoistedFunction(); // Works
function hoistedFunction() {
    console.log('This is hoisted');
}
```

### 5. How JavaScript Manages Memory

- **Stack (Stash):** Stores **primitive values** and function execution contexts.
- **Heap:** Stores **objects and reference types**.
- **Garbage Collection:** Uses **reference counting and mark-and-sweep** algorithms to free memory.

### 6. Scope and Scope Chain

- **Global Scope:** Variables accessible everywhere.
- **Function Scope:** Variables inside a function.
- **Block Scope:** Variables declared with `let` and `const` inside `{}`.

Example:
```javascript
let a = 10; // Global scope
function example() {
    let b = 20; // Function scope
    if (true) {
        let c = 30; // Block scope
    }
    console.log(b); // Accessible
}
```

**Scope Chain:** When a variable is accessed, JavaScript looks for it in the local scope first, then moves up to parent scopes until it reaches the global scope.

### 7. What is `"use strict"`?

Using `"use strict"` enables **strict mode**, which prevents silent errors and enforces best practices.

Example:
```javascript
'use strict';
x = 10; // ReferenceError: x is not defined
```

### 8. Higher-Order Functions

Functions that **take other functions as arguments or return functions**.

Example:
```javascript
function operate(operation, x, y) {
    return operation(x, y);
}
console.log(operate((a, b) => a + b, 5, 3)); // Output: 8
```

### 9. `this` Keyword

`this` refers to the **execution context**.

- **Global Context:** In browsers, `this` is `window`.
- **Object Method:** `this` refers to the object.
- **Arrow Function:** `this` is lexically inherited.

Example:
```javascript
const obj = {
    name: 'JS',
    print: function() {
        console.log(this.name);
    }
};
obj.print(); // Output: JS
```

### 10. Call, Apply, and Bind

| Method  | Description |
|---------|-------------|
| `call()` | Calls a function with a given `this` value and arguments. |
| `apply()` | Similar to `call`, but takes an array of arguments. |
| `bind()` | Returns a new function with `this` bound. |

Example:
```javascript
function greet(greeting) {
    console.log(greeting + ', ' + this.name);
}
const person = { name: 'Alice' };

greet.call(person, 'Hello'); // Hello, Alice
greet.apply(person, ['Hi']); // Hi, Alice
const boundFunc = greet.bind(person, 'Hey');
boundFunc(); // Hey, Alice
```

### 11. Closures: What and When to Use?

A **closure** is a function that remembers the variables from its outer scope.

Example:
```javascript
function counter() {
    let count = 0;
    return function() {
        count++;
        console.log(count);
    };
}
const increment = counter();
increment(); // Output: 1
increment(); // Output: 2
```

**When to use Closures?**
- **Data encapsulation**
- **Memoization**
- **Event handlers**

### 12. Objects in JavaScript

Objects store key-value pairs and methods.

Example:
```javascript
const person = {
    name: 'John',
    age: 30,
    greet: function() {
        console.log('Hello ' + this.name);
    }
};
person.greet();
```

### 13. Memoization

Memoization optimizes functions by caching results of expensive calculations.

Example:
```javascript
function memoize(fn) {
    let cache = {};
    return function(n) {
        if (n in cache) return cache[n];
        cache[n] = fn(n);
        return cache[n];
    };
}
const factorial = memoize(n => (n <= 1 ? 1 : n * factorial(n - 1)));
console.log(factorial(5));
```

### 14. The DOM (Document Object Model)

The DOM represents HTML as a tree structure. JavaScript can manipulate it using:
- `document.getElementById('id')`
- `document.querySelector('.class')`
- `element.innerHTML = 'Hello'`
- `element.style.color = 'red'`

### 15. Constructors in JavaScript

Constructors are functions used to create objects.

Example:
```javascript
function Person(name, age) {
    this.name = name;
    this.age = age;
}
const user = new Person('John', 25);
console.log(user.name); // John
```

### 16. Local Storage vs Session Storage vs Cookies

| Feature | Local Storage | Session Storage | Cookies |
|---------|--------------|----------------|---------|
| **Lifetime** | Permanent until cleared | Only for session | Can expire |
| **Size** | 5MB | 5MB | 4KB |
| **Accessibility** | Only client-side | Only client-side | Sent with HTTP requests |
| **Use Case** | Storing user preferences | Temporary session data | Authentication, tracking |

### 17. Array Methods

JavaScript provides various built-in methods for working with arrays. Below is a comprehensive table of common array methods, along with their descriptions and examples.

| Method | Description | Example |
|--------|-------------|---------|
| `map()` | Creates a new array by applying a function to each element. | `const nums = [1, 2, 3]; console.log(nums.map(x => x * 2)); // [2, 4, 6]` |
| `filter()` | Returns a new array with elements that pass a test. | `const nums = [1, 2, 3, 4]; console.log(nums.filter(x => x > 2)); // [3, 4]` |
| `reduce()` | Reduces an array to a single value by applying a function. | `const nums = [1, 2, 3]; console.log(nums.reduce((a, b) => a + b, 0)); // 6` |
| `forEach()` | Iterates through an array, executing a function on each element. | `[1, 2, 3].forEach(x => console.log(x * 2)); // 2, 4, 6` |
| `sort()` | Sorts an array in place. | `const nums = [3, 1, 2]; console.log(nums.sort()); // [1, 2, 3]` |
| `find()` | Returns the first element that passes a test. | `const nums = [1, 2, 3]; console.log(nums.find(x => x > 1)); // 2` |
| `findIndex()` | Returns the index of the first element that passes a test. | `const nums = [1, 2, 3]; console.log(nums.findIndex(x => x > 1)); // 1` |
| `some()` | Checks if at least one element satisfies a condition. | `const nums = [1, 2, 3]; console.log(nums.some(x => x > 2)); // true` |
| `every()` | Checks if all elements satisfy a condition. | `const nums = [1, 2, 3]; console.log(nums.every(x => x > 0)); // true` |
| `includes()` | Checks if an array contains a specific value. | `const nums = [1, 2, 3]; console.log(nums.includes(2)); // true` |
| `indexOf()` | Returns the index of the first occurrence of a value. | `const nums = [1, 2, 3]; console.log(nums.indexOf(2)); // 1` |
| `lastIndexOf()` | Returns the index of the last occurrence of a value. | `const nums = [1, 2, 3, 2]; console.log(nums.lastIndexOf(2)); // 3` |
| `concat()` | Merges two or more arrays. | `const a = [1, 2]; const b = [3, 4]; console.log(a.concat(b)); // [1, 2, 3, 4]` |
| `slice()` | Extracts a section of an array. | `const nums = [1, 2, 3, 4]; console.log(nums.slice(1, 3)); // [2, 3]` |
| `splice()` | Adds/removes elements from an array. | `const nums = [1, 2, 3]; nums.splice(1, 1, 4); console.log(nums); // [1, 4, 3]` |
| `fill()` | Fills an array with a static value. | `const nums = [1, 2, 3]; console.log(nums.fill(0)); // [0, 0, 0]` |
| `reverse()` | Reverses the array. | `const nums = [1, 2, 3]; console.log(nums.reverse()); // [3, 2, 1]` |
| `join()` | Joins array elements into a string. | `const nums = [1, 2, 3]; console.log(nums.join('-')); // "1-2-3"` |
| `split()` | Converts a string into an array. | `const str = "Hello World"; console.log(str.split(" ")); // ["Hello", "World"]` |
| `push()` | Adds elements to the end of an array. | `const nums = [1, 2]; nums.push(3); console.log(nums); // [1, 2, 3]` |
| `pop()` | Removes the last element from an array. | `const nums = [1, 2, 3]; console.log(nums.pop()); // 3` |
| `shift()` | Removes the first element from an array. | `const nums = [1, 2, 3]; console.log(nums.shift()); // 1` |
| `unshift()` | Adds elements to the beginning of an array. | `const nums = [2, 3]; nums.unshift(1); console.log(nums); // [1, 2, 3]` |
| `flat()` | Flattens nested arrays. | `const nums = [1, [2, 3], [4]]; console.log(nums.flat()); // [1, 2, 3, 4]` |

### 18. String Methods

JavaScript provides a variety of built-in methods to manipulate and interact with strings. Below is a comprehensive table of common string methods, along with their descriptions and examples.

| Method | Description | Example |
|--------|-------------|---------|
| `charAt()` | Returns the character at a specified index. | `console.log("Hello".charAt(1)); // "e"` |
| `charCodeAt()` | Returns the Unicode value of a character at a given index. | `console.log("ABC".charCodeAt(0)); // 65` |
| `concat()` | Joins two or more strings. | `console.log("Hello".concat(" World")); // "Hello World"` |
| `includes()` | Checks if a string contains a specified substring. | `console.log("JavaScript".includes("Script")); // true` |
| `indexOf()` | Returns the index of the first occurrence of a substring. | `console.log("Hello World".indexOf("o")); // 4` |
| `lastIndexOf()` | Returns the index of the last occurrence of a substring. | `console.log("Hello World".lastIndexOf("o")); // 7` |
| `replace()` | Replaces a specified value with another. | `console.log("Hello World".replace("World", "JavaScript")); // "Hello JavaScript"` |
| `replaceAll()` | Replaces all occurrences of a specified value. | `console.log("Hello Hello".replaceAll("Hello", "Hi")); // "Hi Hi"` |
| `slice()` | Extracts a section of a string and returns it as a new string. | `console.log("Hello World".slice(0, 5)); // "Hello"` |
| `substring()` | Extracts characters between two indexes. | `console.log("Hello World".substring(0, 5)); // "Hello"` |
| `substr()` | Extracts a part of a string, starting from an index with a given length. | `console.log("JavaScript".substr(4, 6)); // "Script"` |
| `split()` | Splits a string into an array based on a delimiter. | `console.log("Hello World".split(" ")); // ["Hello", "World"]` |
| `toLowerCase()` | Converts a string to lowercase. | `console.log("Hello".toLowerCase()); // "hello"` |
| `toUpperCase()` | Converts a string to uppercase. | `console.log("hello".toUpperCase()); // "HELLO"` |
| `trim()` | Removes whitespace from both ends of a string. | `console.log("  Hello  ".trim()); // "Hello"` |
| `trimStart()` | Removes whitespace from the start of a string. | `console.log("  Hello  ".trimStart()); // "Hello  "` |
| `trimEnd()` | Removes whitespace from the end of a string. | `console.log("  Hello  ".trimEnd()); // "  Hello"` |
| `startsWith()` | Checks if a string starts with a specified value. | `console.log("JavaScript".startsWith("Java")); // true` |
| `endsWith()` | Checks if a string ends with a specified value. | `console.log("JavaScript".endsWith("Script")); // true` |
| `padStart()` | Pads a string at the beginning with another string. | `console.log("5".padStart(3, "0")); // "005"` |
| `padEnd()` | Pads a string at the end with another string. | `console.log("5".padEnd(3, "0")); // "500"` |
| `repeat()` | Returns a new string with copies of the original string. | `console.log("Hello".repeat(3)); // "HelloHelloHello"` |
| `match()` | Searches a string for a match against a regular expression. | `console.log("Hello 123".match(/\d+/)); // ["123"]` |
| `search()` | Searches a string for a regular expression and returns the position. | `console.log("Hello 123".search(/\d/)); // 6` |


### 19. Memory Management

JavaScript manages memory automatically through **garbage collection**, but understanding how memory allocation works is crucial for writing efficient and optimized code.

### 1. Memory Allocation in JavaScript

Memory in JavaScript is primarily divided into two areas:

- **Stack (Call Stack):** Stores **primitive values** and function execution contexts.
- **Heap:** Stores **objects, arrays, and functions**, which are reference types.

### 2. Primitive vs Reference Types

| Data Type | Memory Location | Example |
|-----------|----------------|---------|
| **Primitive (Number, String, Boolean, Null, Undefined, Symbol, BigInt)** | Stored in the **stack** | `let a = 10;` |
| **Reference (Object, Array, Function, Date, Map, Set, RegExp)** | Stored in the **heap**, with a reference stored in the stack | `let obj = { name: "Alice" };` |

### 3. How JavaScript Stores Primitive Values

Primitive values (numbers, strings, booleans, etc.) are stored **directly in the stack**.
```javascript
let x = 10;
let y = x;
y = 20;
console.log(x); // 10 (remains unchanged)
```
- `x` and `y` are independent values in the stack.

### 4. How JavaScript Stores Reference Types

Objects, arrays, and functions are stored **in the heap**, and only their reference is stored in the stack.
```javascript
let obj1 = { value: 10 };
let obj2 = obj1;
obj2.value = 20;
console.log(obj1.value); // 20 (both point to the same object in heap)
```
- `obj1` and `obj2` both point to the same object in the heap.

### 5. Memory Leaks in JavaScript

Memory leaks occur when memory is **not released properly**, leading to high memory consumption over time. Common causes include:

- **Global variables that persist unnecessarily**
- **Forgotten timers or event listeners**
- **Detached DOM elements**
- **Closures capturing unnecessary references**

### 6. Garbage Collection in JavaScript

JavaScript uses **automatic garbage collection** with the **mark-and-sweep algorithm**:
- The **garbage collector identifies unreachable objects**.
- It **removes them from memory**, freeing up space.

#### Example of Garbage Collection
```javascript
function createUser() {
    let user = { name: "Alice" };
}
createUser(); // The 'user' object becomes unreachable after function execution
```
- The `user` object is removed by garbage collection after the function finishes execution.

### 7. Avoiding Memory Leaks

| Issue | Solution |
|-------|----------|
| Unused global variables | Set variables to `null` when no longer needed. |
| Forgotten event listeners | Remove event listeners using `removeEventListener()`. |
| Unnecessary DOM elements | Remove elements from the DOM properly. |
| Overuse of closures | Avoid unnecessary variable retention inside closures. |

### 8. Managing Large Data Structures Efficiently

- Use **WeakMap** and **WeakSet** for objects that should be garbage-collected when no longer referenced.
- Use **efficient loops and avoid unnecessary object references**.
- Optimize **arrays and objects** by minimizing deep copies.

