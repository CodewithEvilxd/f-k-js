### **Lesson 1: Variables in JavaScript**

Variables are the foundation of any programming language, including JavaScript. They are like labeled boxes where you store data that your program can use and change. This lesson covers everything about variables in JavaScript: what they are, how to declare them, their scope, hoisting, data types, and more. With examples, tables, and code snippets, you'll have all you need right here.

#### **1. What are Variables?**

- **Definition:** A variable is a named storage location in memory that holds a value. The value can be a number, text, true/false, or more complex data.
- **Why Needed:** Without variables, you'd have to hardcode values everywhere, making code inflexible.
- **Key Concept:** Variables have a **name** (identifier), a **value**, and a **data type** (inferred automatically in JS).

**Example:**
```javascript
let age = 25; // 'age' is the variable name, 25 is the value
console.log(age); // Outputs: 25
```

#### **2. Declaring Variables**

In JavaScript, you declare variables using keywords. There are three main ways:

- **`var`:** Old way (ES5 and earlier). Avoid in modern code due to scoping issues.
- **`let`:** Modern way for variables that can change. Block-scoped.
- **`const`:** For constants that don't change. Block-scoped.

**Syntax:**
```javascript
var variableName; // Declaration only
let variableName = value; // Declaration with initialization
const constantName = value; // Must be initialized
```

**Rules for Naming Variables:**
- Start with letter, underscore (_), or dollar sign ($).
- Can contain letters, numbers, _, $.
- Case-sensitive (e.g., `age` ≠ `Age`).
- No reserved words (e.g., `let`, `if`).

**Examples:**
```javascript
let userName = "Alice";
const PI = 3.14159;
var oldStyle = "Avoid this";
```

#### **3. Initializing Variables**

- **Initialization:** Assigning a value when declaring.
- **Reassignment:** Changing the value later (not for `const`).

**Examples:**
```javascript
let score; // Undefined initially
score = 100; // Assign later

let level = 1; // Initialize
level = 2; // Reassign

const maxScore = 1000;
// maxScore = 2000; // Error!
```

#### **4. Variable Scope**

Scope determines where a variable is accessible.

- **Global Scope:** Accessible everywhere in the script.
- **Function Scope:** Accessible only inside the function (for `var`).
- **Block Scope:** Accessible only inside the block `{}` (for `let` and `const`).

**Table: Scope Comparison**

| Keyword | Scope Type | Example |
|---------|------------|---------|
| `var` | Function/Global | `if (true) { var x = 1; } console.log(x);` // Works |
| `let` | Block | `if (true) { let x = 1; } console.log(x);` // Error |
| `const` | Block | Same as `let`, but value can't change |

**Examples:**
```javascript
// Global
let globalVar = "I'm global";

function myFunction() {
  var funcVar = "Function scope";
  let blockVar = "Block scope";
  if (true) {
    let innerVar = "Inner block";
    console.log(innerVar); // OK
  }
  // console.log(innerVar); // Error: out of scope
}

console.log(globalVar); // OK
// console.log(funcVar); // Error
```

#### **5. Hoisting**

- **Definition:** Variables declared with `var` are "hoisted" to the top of their scope. You can use them before declaration (but value is `undefined`).
- **`let` and `const`:** Not hoisted in the same way; using before declaration gives error.

**Examples:**
```javascript
console.log(a); // undefined (hoisted)
var a = 10;

console.log(b); // Error: Cannot access 'b' before initialization
let b = 20;
```

#### **6. Temporal Dead Zone (TDZ)**

- **Definition:** The period between entering a scope and the variable's declaration where `let` and `const` variables cannot be accessed. It's a safety feature to avoid bugs.
- **Why:** Prevents using variables before they're properly initialized.

**Example:**
```javascript
// TDZ starts here
console.log(x); // ReferenceError: Cannot access 'x' before initialization
let x = 5; // TDZ ends here
```

#### **7. Variable Shadowing**

- **Definition:** When a variable in an inner scope has the same name as one in an outer scope, the inner one "shadows" the outer one.
- **Effect:** The inner variable hides the outer one within its scope.

**Example:**
```javascript
let name = "Global";

function test() {
  let name = "Local"; // Shadows global
  console.log(name); // "Local"
}

test();
console.log(name); // "Global"
```

#### **8. Constants with Objects and Arrays**

- **`const` with Primitives:** Value cannot change.
- **`const` with Objects/Arrays:** The reference cannot change, but contents can be mutated.

**Examples:**
```javascript
const obj = { name: "Alice" };
obj.name = "Bob"; // ✓ Allowed (mutating property)
// obj = {}; // ✗ Error (reassigning reference)

const arr = [1, 2];
arr.push(3); // ✓ Allowed (mutating array)
// arr = []; // ✗ Error (reassigning reference)
```

#### **9. Global Object (window/globalThis)**

- **In Browsers:** `var` variables become properties of `window`.
- **In Node.js:** `var` variables are on `global`.
- **`let`/`const`:** Not attached to global object.

**Examples:**
```javascript
var globalVar = "I'm on window";
console.log(window.globalVar); // "I'm on window" (in browser)

let notOnWindow = "Not on window";
console.log(window.notOnWindow); // undefined
```

#### **10. Destructuring Assignment**

- **Definition:** Unpack values from arrays or objects into variables.
- **Syntax:** `let [a, b] = array;` or `const {key} = object;`

**Examples:**
```javascript
let [a, b] = [1, 2];
console.log(a, b); // 1 2

const {name, age} = {name: "Ali", age: 25};
console.log(name, age); // "Ali" 25
```

#### **11. Multiple Declaration**

- **Definition:** Declare multiple variables in one statement.

**Example:**
```javascript
let a = 1, b = 2, c = 3; // Single statement
const x = 10, y = 20;
```

#### **12. Summary Table**

| Feature       | var          | let          | const        |
|---------------|--------------|--------------|--------------|
| Scope         | Function/Global | Block      | Block        |
| Hoisting      | Yes (undefined) | Yes (TDZ)  | Yes (TDZ)   |
| Reassignment  | ✓            | ✓            | ✗            |
| Redeclaration | ✓            | ✗            | ✗            |
| Global Object | ✓            | ✗            | ✗            |

#### **6. Data Types and Variables**

JavaScript is dynamically typed: variable types are determined at runtime.

**Primitive Types:**
- `string`: Text, e.g., `"Hello"`
- `number`: Integers/floats, e.g., `42`, `3.14`
- `boolean`: `true` or `false`
- `undefined`: Not assigned
- `null`: Explicitly empty
- `symbol`: Unique identifiers (ES6+)
- `bigint`: Large integers (ES11+)

**Reference Types:**
- `object`: Collections, e.g., `{name: "Alice"}`
- `array`: Special object, e.g., `[1, 2, 3]`
- `function`: Callable objects

**Type Checking:**
```javascript
let x = 10;
console.log(typeof x); // "number"
x = "Hello";
console.log(typeof x); // "string"
```

**Table: Data Types**

| Type | Example | Description |
|------|---------|-------------|
| string | `"text"` | Text data |
| number | `123` | Numeric values |
| boolean | `true` | True/false |
| undefined | `let x;` | Not defined |
| null | `let y = null;` | Intentionally empty |
| object | `{key: "value"}` | Complex data |
| array | `[1, 2, 3]` | Ordered list |

#### **7. Variable Reassignment and Type Coercion**

- **Reassignment:** Change value and type.
- **Type Coercion:** JS automatically converts types in operations.

**Examples:**
```javascript
let value = 10; // number
value = "Ten"; // now string
value = true; // now boolean

console.log(5 + "5"); // "55" (string concatenation)
console.log(5 - "2"); // 3 (numeric subtraction)
```

#### **8. Best Practices**

- Use `const` by default, `let` when needed, avoid `var`.
- Use descriptive names: `userAge` not `x`.
- Initialize variables when possible.
- Avoid global variables to prevent conflicts.

#### **9. Common Mistakes**

- Using `=` instead of `==` or `===` in comparisons.
- Forgetting `const` can't be reassigned.
- Misunderstanding scope leading to bugs.

#### **10. Examples with Code**

**Example 1: Basic Declaration and Use**
```javascript
let name = "John";
const age = 30;
let isStudent = true;

console.log("Name:", name);
console.log("Age:", age);
console.log("Is Student:", isStudent);
```

**Example 2: Scope Demonstration**
```javascript
if (true) {
  var varVariable = "I leak out";
  let letVariable = "I'm contained";
}

console.log(varVariable); // "I leak out"
// console.log(letVariable); // Error
```

**Example 3: Hoisting**
```javascript
hoistedVar = "I'm hoisted";
console.log(hoistedVar); // "I'm hoisted"
var hoistedVar;

// let hoistedLet = "Not hoisted";
// console.log(hoistedLet); // Error
```

This covers everything about variables in JavaScript. Practice by experimenting in a browser console or editor.