### **Lesson 5: Data Types in JavaScript**

JavaScript has several built-in data types that determine how values are stored and manipulated. This lesson covers all data types in JavaScript: primitives and references, their characteristics, usage, and best practices for working with them effectively.

#### **1. What are Data Types?**

- **Definition:** Classifications that specify the type of value a variable can hold.
- **Why Needed:** Determines memory allocation, operations allowed, and behavior.
- **Dynamic Typing:** JavaScript is dynamically typed - variables can hold any type.

**Example:** A variable can hold a number, then be reassigned to a string.

#### **2. Primitive Data Types**

Primitive types are immutable and stored by value.

##### **2.1 Number**

Represents both integers and floating-point numbers.

```javascript
// Integers
let age = 25;
let negative = -10;

// Floating-point
let price = 99.99;
let pi = 3.14159;

// Special values
let infinity = Infinity;
let negativeInfinity = -Infinity;
let notANumber = NaN;

// BigInt (ES2020)
let bigNumber = 123456789012345678901234567890n;
let anotherBig = BigInt("123456789012345678901234567890");
```

**Characteristics:**
- 64-bit floating-point (IEEE 754)
- Range: ±1.7976931348623157 × 10^308
- Precision: 15-17 decimal digits

##### **2.2 String**

Represents textual data.

```javascript
// String literals
let single = 'Hello';
let double = "World";
let template = `Hello ${name}`;

// String methods
let text = "JavaScript";
text.length;           // 10
text.toUpperCase();    // "JAVASCRIPT"
text.substring(0, 4);  // "Java"
text.includes("Script"); // true

// Unicode support
let emoji = "🚀";
let unicode = "\u{1F680}"; // Same rocket emoji
```

**Characteristics:**
- Immutable (cannot be changed after creation)
- UTF-16 encoded
- Can be created with single, double, or backtick quotes

##### **2.3 Boolean**

Represents logical values.

```javascript
let isLoggedIn = true;
let hasPermission = false;

// Boolean conversion
Boolean(1);        // true
Boolean(0);        // false
Boolean("hello");  // true
Boolean("");       // false

// Logical operators
true && false;     // false
true || false;     // true
!true;             // false
```

**Characteristics:**
- Only two values: `true` and `false`
- Used in conditional statements and logical operations

##### **2.4 Undefined**

Represents a variable that has been declared but not assigned a value.

```javascript
let unassigned;
console.log(unassigned); // undefined

// Function without return
function noReturn() {
  // no return statement
}
console.log(noReturn()); // undefined

// Accessing non-existent property
let obj = {};
console.log(obj.missing); // undefined
```

**Characteristics:**
- Default value for uninitialized variables
- Different from `null` (intentional absence)

##### **2.5 Null**

Represents intentional absence of any object value.

```javascript
let empty = null;

// Common use cases
let user = null; // No user logged in
let result = null; // No result found

// Type checking
typeof null; // "object" (historical bug)
null === undefined; // false
null == undefined; // true
```

**Characteristics:**
- Must be assigned explicitly
- Represents "no value" or "empty"

##### **2.6 Symbol (ES6)**

Represents unique identifiers.

```javascript
// Creating symbols
let sym1 = Symbol();
let sym2 = Symbol("description");
let sym3 = Symbol("description");

// Symbols are unique
sym1 === sym2; // false
sym2 === sym3; // false (even with same description)

// Symbol as object keys
let obj = {};
let key = Symbol("unique");
obj[key] = "value";
obj[key]; // "value"

// Well-known symbols
Symbol.iterator;
Symbol.toStringTag;
Symbol.toPrimitive;
```

**Characteristics:**
- Always unique
- Used for creating private properties
- Not enumerable in for...in loops

##### **2.7 BigInt (ES2020)**

Represents integers of arbitrary size.

```javascript
// Creating BigInts
let big1 = 123456789012345678901234567890n;
let big2 = BigInt("123456789012345678901234567890");
let big3 = BigInt(123);

// Operations
big1 + big2; // 246913578024691357802469135780n
big1 * 2n;   // 246913578024691357802469135780n

// Cannot mix with regular numbers
// big1 + 1; // TypeError
big1 + BigInt(1); // Works
```

**Characteristics:**
- Arbitrary precision integers
- Cannot be mixed with regular numbers in operations
- Slower than regular numbers

#### **3. Reference Data Types**

Reference types are mutable and stored by reference.

##### **3.1 Object**

Represents collections of key-value pairs.

```javascript
// Object literal
let person = {
  name: "Alice",
  age: 30,
  hobbies: ["reading", "coding"]
};

// Accessing properties
person.name;        // "Alice"
person["age"];      // 30

// Adding/modifying properties
person.email = "alice@example.com";
person.age = 31;

// Methods
person.greet = function() {
  return `Hello, I'm ${this.name}`;
};
```

**Characteristics:**
- Mutable
- Can contain any data type as values
- Keys are strings or symbols

##### **3.2 Array**

Specialized object for ordered collections.

```javascript
// Array literal
let numbers = [1, 2, 3, 4, 5];
let mixed = [1, "hello", true, {key: "value"}];

// Array methods
numbers.push(6);        // [1, 2, 3, 4, 5, 6]
numbers.pop();          // 6, array becomes [1, 2, 3, 4, 5]
numbers.shift();        // 1, array becomes [2, 3, 4, 5]
numbers.unshift(0);     // [0, 2, 3, 4, 5]

// Iteration
numbers.forEach(num => console.log(num));
let doubled = numbers.map(num => num * 2);
```

**Characteristics:**
- Ordered collection
- Zero-indexed
- Dynamic size
- Array prototype methods available

##### **3.3 Function**

Special type of object that can be called.

```javascript
// Function declaration
function greet(name) {
  return `Hello, ${name}!`;
}

// Function expression
const add = function(a, b) {
  return a + b;
};

// Arrow function (ES6)
const multiply = (a, b) => a * b;

// Constructor function
function Person(name, age) {
  this.name = name;
  this.age = age;
}

const alice = new Person("Alice", 30);
```

**Characteristics:**
- First-class citizens (can be assigned to variables)
- Can be passed as arguments
- Can return values
- Have their own scope

#### **4. Type Checking**

##### **4.1 typeof Operator**

```javascript
typeof 42;              // "number"
typeof "hello";         // "string"
typeof true;            // "boolean"
typeof undefined;       // "undefined"
typeof null;            // "object" (bug)
typeof {};              // "object"
typeof [];              // "object"
typeof function(){};    // "function"
typeof Symbol();        // "symbol"
typeof 42n;             // "bigint"
```

##### **4.2 instanceof Operator**

```javascript
let arr = [];
arr instanceof Array;        // true
arr instanceof Object;       // true

let date = new Date();
date instanceof Date;        // true
date instanceof Object;       // true

// Custom constructors
function Car() {}
let myCar = new Car();
myCar instanceof Car;        // true
```

##### **4.3 Array.isArray()**

```javascript
Array.isArray([]);           // true
Array.isArray({});           // false
Array.isArray("array");      // false
```

##### **4.4 Object.prototype.toString()**

```javascript
Object.prototype.toString.call(42);         // "[object Number]"
Object.prototype.toString.call("hello");    // "[object String]"
Object.prototype.toString.call(null);       // "[object Null]"
Object.prototype.toString.call(undefined);  // "[object Undefined]"
```

#### **5. Type Conversion and Coercion**

```javascript
// Implicit coercion
"5" + 3;        // "53" (number to string)
"5" - 3;        // 2 (string to number)
!!"hello";      // true (string to boolean)

// Explicit conversion
Number("123");  // 123
String(456);    // "456"
Boolean(0);     // false
```

#### **6. Best Practices**

- Use `const` for primitive values that shouldn't change.
- Use `let` for variables that need reassignment.
- Prefer primitive types when possible (better performance).
- Use descriptive variable names that indicate type.
- Always initialize variables to avoid `undefined`.
- Use `===` and `!==` for comparisons.
- Be aware of `typeof null` returning "object".
- Use `Array.isArray()` to check for arrays.
- Avoid using `new` with primitives.
- Use object destructuring for cleaner code.
- Consider using TypeScript for better type safety.

#### **7. Common Mistakes**

- Confusing `null` and `undefined`.
- Using `==` instead of `===`.
- Assuming `typeof null` returns "null".
- Modifying primitive values (they're immutable).
- Comparing objects expecting value equality.
- Not checking for array type before using array methods.
- Using `new` with string, number, or boolean constructors.
- Forgetting that arrays are objects.
- Assuming BigInt can be mixed with regular numbers.
- Not handling `NaN` properly in comparisons.

#### **8. Memory Management**

##### **8.1 Stack vs Heap**

```javascript
// Primitives stored on stack (fast access)
let num = 42;
let str = "hello";

// Objects stored on heap (reference stored on stack)
let obj = { name: "Alice" };
let arr = [1, 2, 3];
```

##### **8.2 Garbage Collection**

- Automatic memory management
- Mark-and-sweep algorithm
- Circular references handled by modern engines

#### **9. Summary**

| Category              | Status | Completion |
|-----------------------|--------|------------|
| Primitive types       | ✓      | 100%       |
| Reference types       | ✓      | 100%       |
| Type checking         | ✓      | 100%       |
| Type conversion       | ✓      | 100%       |
| Best practices        | ✓      | 100%       |
| Common mistakes       | ✓      | 100%       |
| Memory management     | ✓      | 100%       |

Overall Completion: 100% 📊

Master JavaScript data types by understanding the differences between primitives and references. Use appropriate type checking methods and follow best practices for robust code.