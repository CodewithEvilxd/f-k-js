### **Lesson 0.5: JavaScript Basics and Fundamentals**

Now that you know JavaScript's history, let's dive into its basics. This lesson covers the fundamental building blocks: variables, data types, operators, and simple control flow. Everything explained simply, so you can understand in one read.

#### **1. Variables**

Variables are like containers that store data. In JavaScript, you declare them with `let`, `const`, or `var`.

- **`let`:** For variables that can change. E.g., `let age = 25; age = 26;`
- **`const`:** For constants that don't change. E.g., `const pi = 3.14;`
- **`var`:** Old way, avoid it. Similar to `let` but with different scope rules.

**Example:**
```javascript
let name = "Alice";
const year = 2023;
name = "Bob"; // OK
// year = 2024; // Error!
```

#### **2. Data Types**

JavaScript has dynamic types, meaning variables can hold different types.

- **Primitive Types:**
  - `string`: Text, e.g., `"Hello"`
  - `number`: Numbers, e.g., `42` or `3.14`
  - `boolean`: True/false, e.g., `true`
  - `undefined`: Not assigned, e.g., `let x;`
  - `null`: Empty value, e.g., `let y = null;`

- **Objects:** Collections, e.g., `{name: "Alice", age: 25}` (arrays are special objects).

**Example:**
```javascript
let message = "Hi"; // string
let count = 10; // number
let isDone = false; // boolean
```

#### **3. Operators**

Operators perform actions on data.

- **Arithmetic:** `+`, `-`, `*`, `/`, `%` (modulo)
- **Comparison:** `==` (loose equal), `===` (strict equal), `!=`, `<`, `>`, `<=`, `>=`
- **Logical:** `&&` (and), `||` (or), `!` (not)
- **Assignment:** `=`, `+=`, `-=`, etc.

**Example:**
```javascript
let a = 5;
let b = 10;
let sum = a + b; // 15
let isEqual = (a === 5); // true
```

#### **4. Control Structures**

Control what code runs.

- **If-Else:**
  ```javascript
  if (condition) {
    // do something
  } else {
    // do something else
  }
  ```

- **Loops:**
  - `for`: `for (let i = 0; i < 5; i++) { console.log(i); }`
  - `while`: `while (condition) { ... }`

**Example:**
```javascript
let num = 5;
if (num > 0) {
  console.log("Positive");
} else {
  console.log("Not positive");
}

for (let i = 1; i <= 3; i++) {
  console.log("Count: " + i);
}
```

#### **5. Functions**

Functions are reusable code blocks.

**Syntax:**
```javascript
function functionName(parameters) {
  // code
  return value; // optional
}
```

**Example:**
```javascript
function greet(name) {
  return "Hello, " + name;
}

console.log(greet("Alice")); // "Hello, Alice"
```

#### **6. Arrays and Objects**

- **Arrays:** Lists, e.g., `let fruits = ["apple", "banana"];`
- **Objects:** Key-value pairs, e.g., `let person = {name: "Alice", age: 25};`

**Example:**
```javascript
let numbers = [1, 2, 3];
console.log(numbers[0]); // 1

let car = {brand: "Toyota", year: 2020};
console.log(car.brand); // "Toyota"
```

#### **7. Console Output**

Use `console.log()` to print to the console.

**Example:**
```javascript
console.log("Hello World!");
```

This covers the basics. Practice by writing small scripts. Next lessons will build on this for advanced topics.

**Homework Idea:** Write a script that asks for your name and age, then prints a greeting with your age next year.