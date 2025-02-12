# Understanding JavaScript

## 1. What is JavaScript?

JavaScript is a **high-level, interpreted programming language** used primarily for **web development**. It enables interactive web pages and runs in the browser but can also be used on the server with environments like **Node.js**.

## 2. What is ECMAScript?

ECMAScript (ES) is the **standard** that defines JavaScript’s features and syntax. ECMAScript updates (e.g., **ES6, ES7, ES8**) introduce new functionalities like **arrow functions, classes, template literals**, and more.

## 3. Variable Declarations: `var`, `let`, and `const`

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

## 4. Hoisting and Its Types

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

## 5. How JavaScript Manages Memory

- **Stack (Stash):** Stores **primitive values** and function execution contexts.
- **Heap:** Stores **objects and reference types**.
- **Garbage Collection:** Uses **reference counting and mark-and-sweep** algorithms to free memory.

## 6. Scope and Scope Chain

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

## 7. What is `"use strict"`?

Using `"use strict"` enables **strict mode**, which prevents silent errors and enforces best practices.

Example:
```javascript
'use strict';
x = 10; // ReferenceError: x is not defined
```

## 8. Higher-Order Functions

Functions that **take other functions as arguments or return functions**.

Example:
```javascript
function operate(operation, x, y) {
    return operation(x, y);
}
console.log(operate((a, b) => a + b, 5, 3)); // Output: 8
```

## 9. `this` Keyword

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

## 10. Call, Apply, and Bind

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

## 11. Closures: What and When to Use?

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

## 12. Objects in JavaScript

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

## 13. Memoization

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

## 14. The DOM (Document Object Model)

The DOM represents HTML as a tree structure. JavaScript can manipulate it using:
- `document.getElementById('id')`
- `document.querySelector('.class')`
- `element.innerHTML = 'Hello'`
- `element.style.color = 'red'`

## 15. Constructors in JavaScript

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

## 16. Local Storage vs Session Storage vs Cookies

| Feature | Local Storage | Session Storage | Cookies |
|---------|--------------|----------------|---------|
| **Lifetime** | Permanent until cleared | Only for session | Can expire |
| **Size** | 5MB | 5MB | 4KB |
| **Accessibility** | Only client-side | Only client-side | Sent with HTTP requests |
| **Use Case** | Storing user preferences | Temporary session data | Authentication, tracking |

## 17. Array Methods

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


## 19. Memory Management

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

## 20. Understanding Classes in JavaScript

### 1. What Are Classes?

Classes in JavaScript are **syntactic sugar** over prototypes, allowing developers to define blueprints for creating objects in a more structured and readable way. They were introduced in **ES6**.

### 2. Defining a Class

A class is defined using the `class` keyword, and it can have properties and methods.

```javascript
class Person {
    constructor(name, age) {
        this.name = name;
        this.age = age;
    }
    greet() {
        console.log(`Hello, my name is ${this.name} and I am ${this.age} years old.`);
    }
}
const person1 = new Person("Alice", 25);
person1.greet(); // "Hello, my name is Alice and I am 25 years old."
```

### 3. Class Properties and Methods

| Feature | Description |
|---------|-------------|
| **Constructor** | Initializes an object when created. |
| **Instance Properties** | Variables tied to each instance. |
| **Instance Methods** | Functions tied to each instance. |
| **Static Methods** | Functions that belong to the class itself, not instances. |

#### Static Methods Example:
```javascript
class MathUtils {
    static add(a, b) {
        return a + b;
    }
}
console.log(MathUtils.add(5, 3)); // 8
```

### 4. Getters and Setters

Getters (`get`) and Setters (`set`) allow controlled access to properties.
```javascript
class User {
    constructor(username) {
        this._username = username;
    }
    get username() {
        return this._username.toUpperCase();
    }
    set username(newName) {
        this._username = newName.trim();
    }
}
const user = new User("john_doe");
console.log(user.username); // "JOHN_DOE"
user.username = "  new_user  ";
console.log(user.username); // "NEW_USER"
```

### 5. Inheritance

Classes can inherit properties and methods from another class using `extends`.
```javascript
class Animal {
    constructor(name) {
        this.name = name;
    }
    makeSound() {
        console.log("Some generic sound");
    }
}
class Dog extends Animal {
    makeSound() {
        console.log("Woof!");
    }
}
const dog = new Dog("Buddy");
dog.makeSound(); // "Woof!"
```

### 6. Super Keyword

The `super` keyword calls a method from the parent class.
```javascript
class Parent {
    constructor(name) {
        this.name = name;
    }
    sayHello() {
        console.log(`Hello from ${this.name}`);
    }
}
class Child extends Parent {
    constructor(name, age) {
        super(name);
        this.age = age;
    }
}
const child = new Child("Alex", 10);
child.sayHello(); // "Hello from Alex"
```

### 7. Private Fields

Private properties are declared using `#` and cannot be accessed outside the class.
```javascript
class BankAccount {
    #balance;
    constructor(initialBalance) {
        this.#balance = initialBalance;
    }
    getBalance() {
        return this.#balance;
    }
}
const account = new BankAccount(1000);
console.log(account.getBalance()); // 1000
console.log(account.#balance); // SyntaxError
```

### 8. Static Properties and Methods

Static properties and methods belong to the class itself rather than instances. They are useful for utility functions and shared logic.

#### Example:
```javascript
class Counter {
    static count = 0;

    static increment() {
        Counter.count++;
    }
}
Counter.increment();
console.log(Counter.count); // 1
```

### 9. Class Composition vs Inheritance

Composition is an alternative to inheritance by combining multiple objects.
```javascript
class Engine {
    start() {
        console.log("Engine started");
    }
}
class Car {
    constructor() {
        this.engine = new Engine();
    }
    startCar() {
        this.engine.start();
    }
}
const myCar = new Car();
myCar.startCar(); // "Engine started"
```

### 10. Benefits of Using Classes in JavaScript

- **Encapsulation**: Keeps related functionality together.
- **Code Reusability**: Inheritance allows sharing logic.
- **Readability**: More intuitive than prototype-based syntax.
- **Scalability**: Encourages modular design.

## 21. Software Design Patterns

### 1. What Are Design Patterns?

Design patterns are **reusable solutions** to common software design problems. They help developers create more structured, scalable, and maintainable code.

Design patterns are categorized into **three main types**:

1. **Creational Patterns** – Handle object creation.
2. **Structural Patterns** – Define relationships between components.
3. **Behavioral Patterns** – Manage communication between objects.

---

### 2. Creational Patterns

Creational patterns **control object creation**, improving flexibility and reusability.

| Pattern              | Description                                                                                  | When to Use?                                                             |
| -------------------- | -------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------ |
| **Singleton**        | Ensures only **one instance** of a class exists.                                             | Useful for logging, database connections, configuration management.      |
| **Factory Method**   | Provides an interface for **creating objects**, letting subclasses alter the type of object. | When object creation needs to be **centralized and controlled**.         |
| **Abstract Factory** | Creates families of related objects **without specifying their concrete classes**.           | When applications need to be **independent of object creation details**. |
| **Builder**          | Separates **object construction** from its representation.                                   | When an object has **multiple complex configurations**.                  |
| **Prototype**        | Clones existing objects **instead of creating new instances**.                               | When creating new objects is **costly or complex**.                      |

Example (Singleton in JavaScript):

```javascript
class Singleton {
  constructor() {
    if (!Singleton.instance) {
      Singleton.instance = this;
    }
    return Singleton.instance;
  }
}
const instance1 = new Singleton();
const instance2 = new Singleton();
console.log(instance1 === instance2); // true
```

Example (Factory Method in JavaScript):
```javascript
class Car {
    constructor(model) {
        this.model = model;
    }
}
class CarFactory {
    createCar(model) {
        return new Car(model);
    }
}
const factory = new CarFactory();
const car = factory.createCar("Tesla Model X");
console.log(car.model); // Tesla Model X
```

---

### 3. Structural Patterns

Structural patterns define how **classes and objects are composed**, ensuring **flexible and efficient relationships**.

| Pattern       | Description                                            | When to Use?                                                                            |
| ------------- | ------------------------------------------------------ | --------------------------------------------------------------------------------------- |
| **Adapter**   | Converts one interface into another.                   | When integrating incompatible interfaces (e.g., connecting an old API to a new system). |
| **Decorator** | Dynamically adds behaviors to objects.                 | When extending functionality **without modifying existing code**.                       |
| **Facade**    | Provides a simplified interface to a complex system.   | When simplifying multiple subsystems for clients.                                       |
| **Proxy**     | Controls access to another object.                     | Useful for **lazy initialization, security, or caching**.                               |
| **Composite** | Treats individual and composite objects **uniformly**. | When dealing with **hierarchical tree structures** (e.g., UI elements).                 |

Example (Decorator in JavaScript):

```javascript
function addLogging(component) {
    return function() {
        console.log("Logging...");
        return component.apply(this, arguments);
    };
}
function greet(name) {
    return `Hello, ${name}!`;
}
const decoratedGreet = addLogging(greet);
console.log(decoratedGreet("Alice"));
```

Example (Adapter in JavaScript):
```javascript
class OldAPI {
    request() {
        return "Old API Response";
    }
}
class NewAPI {
    fetch() {
        return "New API Response";
    }
}
class APIAdapter {
    constructor(newAPI) {
        this.newAPI = newAPI;
    }
    request() {
        return this.newAPI.fetch();
    }
}
const adapter = new APIAdapter(new NewAPI());
console.log(adapter.request()); // "New API Response"
```

---

### 4. Behavioral Patterns

Behavioral patterns focus on **communication between objects** and responsibilities.

| Pattern      | Description                                                                | When to Use?                                                                             |
| ------------ | -------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------- |
| **Observer** | Defines a **one-to-many dependency** where objects react to state changes. | When one object changes, and multiple others need to be updated (e.g., event listeners). |
| **Strategy** | Defines a **family of algorithms** and allows selecting one at runtime.    | When multiple algorithms **solve the same problem** differently.                         |
| **Command**  | Encapsulates a request as an object.                                       | When implementing **undo/redo functionality**.                                           |
| **Mediator** | Defines an intermediary that controls communication.                       | When reducing direct dependencies **between objects**.                                   |
| **State**    | Changes an object's behavior based on its state.                           | When implementing **finite state machines**.                                             |

Example (Observer in JavaScript):
```javascript
class Observable {
    constructor() {
        this.subscribers = [];
    }
    subscribe(fn) {
        this.subscribers.push(fn);
    }
    notify(data) {
        this.subscribers.forEach(fn => fn(data));
    }
}
const observable = new Observable();
observable.subscribe(data => console.log("Received: ", data));
observable.notify("Hello Observers");
```

Example (Strategy in JavaScript):
```javascript
class PaymentStrategy {
    pay(amount) {
        throw "Method not implemented";
    }
}
class CreditCardPayment extends PaymentStrategy {
    pay(amount) {
        console.log(`Paid $${amount} using Credit Card.`);
    }
}
class PayPalPayment extends PaymentStrategy {
    pay(amount) {
        console.log(`Paid $${amount} using PayPal.`);
    }
}
const payment = new PayPalPayment();
payment.pay(100); // "Paid $100 using PayPal."
```

---

### 5. When to Use Design Patterns?

| Situation                                 | Recommended Pattern |
| ----------------------------------------- | ------------------- |
| Need a single, shared instance            | **Singleton**       |
| Need to dynamically extend functionality  | **Decorator**       |
| Need to provide multiple creation methods | **Factory Method**  |
| Need to control object communication      | **Mediator**        |
| Need to allow objects to react to events  | **Observer**        |
| Need to optimize object access            | **Proxy**           |

### Conclusion

Design patterns help solve recurring problems **efficiently**. Choosing the right pattern **improves maintainability, flexibility, and scalability** of your code. Understanding these patterns will help you **write better software**!

