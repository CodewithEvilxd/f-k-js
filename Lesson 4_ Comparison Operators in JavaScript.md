### **Lesson 4: Comparison Operators in JavaScript**

Comparison operators are used to compare values and return a boolean result. This lesson covers all comparison operators in JavaScript: equality, relational, and logical comparisons, including their behavior with different types, common pitfalls, and best practices.

#### **1. What are Comparison Operators?**

- **Definition:** Operators that compare two values and return `true` or `false`.
- **Why Needed:** Essential for decision-making, sorting, validation, and control flow.
- **Categories:** Equality, Relational, and Special comparison operators.

**Example:** Checking if user age is greater than 18 for access control.

#### **2. Equality Operators**

##### **2.1 Loose Equality (==)**

Performs type coercion before comparison.

```javascript
5 == 5;           // true
5 == "5";         // true (number coerced to string)
0 == false;       // true (false coerced to 0)
null == undefined; // true
"" == 0;          // true (empty string coerced to 0)
[] == "";         // true (array coerced to empty string)
```

##### **2.2 Strict Equality (===)**

Compares both value and type without coercion.

```javascript
5 === 5;          // true
5 === "5";        // false
0 === false;      // false
null === undefined; // false
"" === 0;         // false
[] === "";        // false
```

##### **2.3 Inequality Operators**

```javascript
// Loose inequality (!=)
5 != "5";         // false (coerced)
5 != "6";         // true

// Strict inequality (!==)
5 !== "5";        // true
5 !== 5;          // false
```

#### **3. Relational Operators**

##### **3.1 Greater Than and Less Than**

```javascript
5 > 3;            // true
3 < 5;            // true
"b" > "a";        // true (string comparison)
"10" > 9;         // true (string coerced to number)
```

##### **3.2 Greater/Less Than or Equal**

```javascript
5 >= 5;           // true
5 <= 5;           // true
"10" >= 9;        // true
"5" <= "10";      // true (lexicographic comparison)
```

##### **3.3 Special Cases**

```javascript
// With different types
"5" > 3;          // true (string to number)
true > 0;         // true (boolean to number)
null > 0;         // false
undefined > 0;    // false

// With NaN
NaN > 5;          // false
NaN < 5;          // false
NaN == NaN;       // false
NaN === NaN;      // false
```

#### **4. Object Comparison**

Objects are compared by reference, not value.

```javascript
const obj1 = { a: 1 };
const obj2 = { a: 1 };
const obj3 = obj1;

obj1 == obj2;     // false (different references)
obj1 === obj2;    // false
obj1 == obj3;     // true (same reference)
obj1 === obj3;    // true

// Arrays (also objects)
[1, 2] == [1, 2]; // false
[1, 2] === [1, 2]; // false
```

#### **5. String Comparison**

Strings are compared lexicographically (Unicode values).

```javascript
"apple" < "banana";    // true ('a' < 'b')
"Apple" < "apple";     // true (uppercase before lowercase)
"10" < "2";           // true (first char '1' < '2')
"10" < 2;             // false (string "10" > number 2)
```

#### **6. Boolean Comparison**

```javascript
true > false;      // true (1 > 0)
true == 1;         // true
false == 0;        // true
true === 1;        // false
false === 0;       // false
```

#### **7. null and undefined Comparison**

```javascript
null == undefined;     // true
null === undefined;    // false
null == 0;            // false
undefined == 0;       // false
null >= 0;            // true (null coerced to 0)
undefined >= 0;       // false (undefined to NaN)
```

#### **8. Comparison with Special Values**

##### **8.1 NaN Handling**

```javascript
// NaN never equals itself
NaN == NaN;        // false
NaN === NaN;       // false

// Check for NaN
isNaN(NaN);        // true
isNaN("abc");      // true
Number.isNaN(NaN); // true
Number.isNaN("abc"); // false
```

##### **8.2 Infinity**

```javascript
Infinity > 100;    // true
-Infinity < -100;  // true
Infinity == Infinity; // true
-Infinity == -Infinity; // true
Infinity > -Infinity; // true
```

#### **9. Comparison in Conditional Statements**

```javascript
// Truthy/falsy evaluation
if (5 > 3) { }      // true
if (0 > -1) { }     // true
if ("") { }         // false
if (null) { }       // false

// Chaining comparisons
const age = 25;
if (age >= 18 && age <= 65) { } // true

// Ternary operator
const result = 5 > 3 ? "greater" : "lesser"; // "greater"
```

#### **10. Best Practices**

- Always use strict equality (`===`) unless you specifically need type coercion.
- Be aware of type coercion rules, especially with `==`.
- Use `Object.is()` for special cases like NaN comparison.
- Avoid comparing different types when possible.
- Use `isNaN()` or `Number.isNaN()` appropriately.
- Be careful with floating-point comparisons due to precision issues.
- Use meaningful variable names in comparisons.
- Consider using libraries like lodash for complex comparisons.
- Always test edge cases in your comparisons.

#### **11. Common Mistakes**

- Using `==` instead of `===` leading to unexpected coercion.
- Comparing NaN with itself expecting true.
- Assuming string comparison works like number comparison.
- Not handling null/undefined properly in comparisons.
- Floating-point precision issues in equality checks.
- Comparing objects expecting value equality instead of reference.
- Confusing `>=` with `=>` (syntax error).
- Not considering Unicode order in string comparisons.
- Assuming `null == 0` is true.

#### **12. Advanced Comparison Techniques**

##### **12.1 Object.is() Method**

```javascript
Object.is(5, 5);           // true
Object.is(5, "5");         // false
Object.is(NaN, NaN);       // true (unlike == and ===)
Object.is(0, -0);          // false
Object.is(-0, -0);         // true
```

##### **12.2 Custom Comparison Functions**

```javascript
function compareNumbers(a, b) {
  if (Math.abs(a - b) < Number.EPSILON) {
    return 0; // equal
  }
  return a > b ? 1 : -1;
}

compareNumbers(0.1 + 0.2, 0.3); // 0 (approximately equal)
```

##### **12.3 Sorting with Comparisons**

```javascript
const numbers = [3, 1, 4, 1, 5];
numbers.sort((a, b) => a - b); // [1, 1, 3, 4, 5]

const strings = ["banana", "apple", "cherry"];
strings.sort(); // ["apple", "banana", "cherry"]
```

#### **13. Summary**

| Category              | Status | Completion |
|-----------------------|--------|------------|
| Equality operators    | ✓      | 100%       |
| Relational operators  | ✓      | 100%       |
| Object comparison     | ✓      | 100%       |
| String comparison     | ✓      | 100%       |
| Special values        | ✓      | 100%       |
| Best practices        | ✓      | 100%       |
| Common mistakes       | ✓      | 100%       |
| Advanced techniques   | ✓      | 100%       |

Overall Completion: 100% 📊

Master comparison operators by preferring strict equality and understanding type coercion. Practice with different data types and always consider edge cases in your comparisons.