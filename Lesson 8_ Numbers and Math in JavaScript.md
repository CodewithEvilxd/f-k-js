### **Lesson 8: Numbers and Math in JavaScript**

Numbers are fundamental in JavaScript for calculations, measurements, and data processing. This lesson covers the Number data type, the Math object with all its constants and methods, BigInt for large numbers, and practical mathematical operations with extensive examples.

#### **1. What are Numbers in JavaScript?**

- **Definition:** Numeric data type for representing integers and floating-point numbers.
- **Type:** `number` (64-bit IEEE 754 floating-point).
- **Range:** ±1.7976931348623157 × 10^308 (safe integers: ±9,007,199,254,740,991).
- **Special Values:** `Infinity`, `-Infinity`, `NaN`.

**Example:** Age calculations, prices, measurements, game scores.

#### **2. Number Creation and Types**

##### **2.1 Number Literals**

```javascript
// Integers
let age = 25;
let negative = -10;

// Floating-point
let price = 99.99;
let pi = 3.14159;

// Scientific notation
let million = 1e6;        // 1000000
let micro = 1e-6;         // 0.000001

// Binary, Octal, Hexadecimal
let binary = 0b1010;      // 10 (binary)
let octal = 0o755;        // 493 (octal)
let hex = 0xFF;           // 255 (hexadecimal)

// BigInt (ES2020) - for very large numbers
let bigNumber = 123456789012345678901234567890n;
let anotherBig = BigInt("123456789012345678901234567890");
```

##### **2.2 Number Constructor**

```javascript
// Creating numbers
let num1 = Number("123");     // 123
let num2 = Number("12.34");   // 12.34
let num3 = Number(true);      // 1
let num4 = Number(false);     // 0
let num5 = Number(null);      // 0
let num6 = Number(undefined); // NaN
let num7 = Number("abc");     // NaN

// Check if number
console.log(typeof 42);       // "number"
console.log(Number.isNaN(NaN)); // true
```

#### **3. The Math Object**

The `Math` object provides mathematical constants and functions. It's a built-in static object.

##### **3.1 Mathematical Constants**

```javascript
/**
 * Mathematical Constants in JavaScript Math object
 */

// Euler's number (base of natural logarithm) ≈ 2.718
Math.E;        // 2.718281828459045

// Natural logarithm of 2 ≈ 0.693
Math.LN2;      // 0.6931471805599453

// Natural logarithm of 10 ≈ 2.303
Math.LN10;     // 2.302585092994046

// Base-2 logarithm of e ≈ 1.443 (log₂(e))
Math.LOG2E;    // 1.4426950408889634

// Base-10 logarithm of e ≈ 0.434 (log₁₀(e))
Math.LOG10E;   // 0.4342944819032518

// Pi (π) ≈ 3.142
Math.PI;       // 3.141592653589793

// Square root of ½ ≈ 0.707
Math.SQRT1_2;  // 0.7071067811865476

// Square root of 2 ≈ 1.414
Math.SQRT2;    // 1.4142135623730951
```

**Practical Examples:**
```javascript
// Calculate circle area
function circleArea(radius) {
  return Math.PI * radius * radius;
}
console.log(circleArea(5)); // 78.53981633974483

// Convert degrees to radians
function toRadians(degrees) {
  return degrees * (Math.PI / 180);
}
console.log(toRadians(90)); // 1.5707963267948966
```

#### **4. Math Methods - Arithmetic Operations**

##### **4.1 Basic Arithmetic**

```javascript
/**
 * Math.abs(x) - Returns the absolute value of x
 * @param {number} x - A number
 * @returns {number} The absolute value of x
 */
Math.abs(-5);        // 5
Math.abs(5);         // 5
Math.abs(-3.14);     // 3.14

/**
 * Math.sign(x) - Returns the sign of x (ES2015)
 * @param {number} x - A number
 * @returns {number} -1 if negative, 0 if zero, 1 if positive
 */
Math.sign(-5);       // -1
Math.sign(0);        // 0
Math.sign(5);        // 1

/**
 * Math.pow(base, exponent) - Returns base raised to the power of exponent
 * @param {number} base - The base number
 * @param {number} exponent - The exponent
 * @returns {number} base^exponent
 */
Math.pow(2, 3);      // 8 (2³)
Math.pow(4, 0.5);    // 2 (√4)

/**
 * Math.sqrt(x) - Returns the square root of x
 * @param {number} x - A non-negative number
 * @returns {number} The square root of x
 */
Math.sqrt(16);       // 4

/**
 * Math.cbrt(x) - Returns the cube root of x
 * @param {number} x - A number
 * @returns {number} The cube root of x
 */
Math.cbrt(27);       // 3

/**
 * Math.exp(x) - Returns e^x (Euler's number raised to x)
 * @param {number} x - A number
 * @returns {number} e^x
 */
Math.exp(1);         // 2.718281828459045 (e¹)

/**
 * Math.expm1(x) - Returns e^x - 1 (more accurate for small x)
 * @param {number} x - A number
 * @returns {number} e^x - 1
 */
Math.expm1(1);       // 1.718281828459045 (e¹ - 1)

/**
 * Math.log(x) - Returns the natural logarithm of x
 * @param {number} x - A positive number
 * @returns {number} ln(x)
 */
Math.log(Math.E);    // 1

/**
 * Math.log2(x) - Returns the base-2 logarithm of x
 * @param {number} x - A positive number
 * @returns {number} log₂(x)
 */
Math.log2(8);        // 3

/**
 * Math.log10(x) - Returns the base-10 logarithm of x
 * @param {number} x - A positive number
 * @returns {number} log₁₀(x)
 */
Math.log10(100);     // 2

/**
 * Math.log1p(x) - Returns log(1 + x) (more accurate for small x)
 * @param {number} x - A number > -1
 * @returns {number} log(1 + x)
 */
Math.log1p(1);       // 0.6931471805599453 (log(1+1))
```

##### **4.2 Rounding Methods**

```javascript
let num = 3.14159;

/**
 * Math.round(x) - Rounds to the nearest integer
 * @param {number} x - A number
 * @returns {number} The nearest integer
 */
Math.round(3.14159);   // 3
Math.round(3.5);       // 4
Math.round(3.49);      // 3

/**
 * Math.floor(x) - Rounds down to the nearest integer
 * @param {number} x - A number
 * @returns {number} The largest integer ≤ x
 */
Math.floor(3.14159);   // 3
Math.floor(-3.14159);  // -4

/**
 * Math.ceil(x) - Rounds up to the nearest integer
 * @param {number} x - A number
 * @returns {number} The smallest integer ≥ x
 */
Math.ceil(3.14159);    // 4
Math.ceil(-3.14159);   // -3

/**
 * Math.trunc(x) - Removes the decimal part (ES2015)
 * @param {number} x - A number
 * @returns {number} The integer part of x
 */
Math.trunc(3.14159);   // 3
Math.trunc(-3.14159);  // -3

/**
 * Custom function to round to specific decimal places
 * @param {number} num - The number to round
 * @param {number} decimals - Number of decimal places
 * @returns {number} The rounded number
 */
function roundToDecimal(num, decimals) {
  return Math.round(num * Math.pow(10, decimals)) / Math.pow(10, decimals);
}
console.log(roundToDecimal(3.14159, 2)); // 3.14
```

##### **4.3 Min, Max, and Clamping**

```javascript
/**
 * Math.min(...values) - Returns the smallest of the given numbers
 * @param {...number} values - Numbers to compare
 * @returns {number} The smallest number
 */
Math.min(1, 2, 3, 4, 5);     // 1

/**
 * Math.max(...values) - Returns the largest of the given numbers
 * @param {...number} values - Numbers to compare
 * @returns {number} The largest number
 */
Math.max(1, 2, 3, 4, 5);     // 5

// With arrays (using spread operator)
let numbers = [1, 2, 3, 4, 5];
Math.min(...numbers);         // 1
Math.max(...numbers);         // 5

/**
 * Clamp value between min and max
 * @param {number} value - The value to clamp
 * @param {number} min - The minimum value
 * @param {number} max - The maximum value
 * @returns {number} The clamped value
 */
function clamp(value, min, max) {
  return Math.min(Math.max(value, min), max);
}
console.log(clamp(15, 0, 10)); // 10
console.log(clamp(-5, 0, 10)); // 0
console.log(clamp(5, 0, 10));  // 5
```

#### **5. Trigonometric Functions**

```javascript
/**
 * Convert between degrees and radians
 * @param {number} degrees - Angle in degrees
 * @returns {number} Angle in radians
 */
function toRadians(degrees) {
  return degrees * Math.PI / 180;
}

/**
 * Convert radians to degrees
 * @param {number} radians - Angle in radians
 * @returns {number} Angle in degrees
 */
function toDegrees(radians) {
  return radians * 180 / Math.PI;
}

/**
 * Math.sin(x) - Returns the sine of x (x in radians)
 * @param {number} x - Angle in radians
 * @returns {number} Sine of x (-1 to 1)
 */
Math.sin(toRadians(30));    // 0.49999999999999994 (sin 30°)

/**
 * Math.cos(x) - Returns the cosine of x (x in radians)
 * @param {number} x - Angle in radians
 * @returns {number} Cosine of x (-1 to 1)
 */
Math.cos(toRadians(60));    // 0.5000000000000001 (cos 60°)

/**
 * Math.tan(x) - Returns the tangent of x (x in radians)
 * @param {number} x - Angle in radians
 * @returns {number} Tangent of x
 */
Math.tan(toRadians(45));    // 0.9999999999999999 (tan 45°)

/**
 * Math.asin(x) - Returns the arcsine of x in radians
 * @param {number} x - Value between -1 and 1
 * @returns {number} Arcsine in radians (-π/2 to π/2)
 */
Math.asin(0.5);             // 0.5235987755982989 (30° in radians)

/**
 * Math.acos(x) - Returns the arccosine of x in radians
 * @param {number} x - Value between -1 and 1
 * @returns {number} Arccosine in radians (0 to π)
 */
Math.acos(0.5);             // 1.0471975511965976 (60° in radians)

/**
 * Math.atan(x) - Returns the arctangent of x in radians
 * @param {number} x - A number
 * @returns {number} Arctangent in radians (-π/2 to π/2)
 */
Math.atan(1);               // 0.7853981633974483 (45° in radians)

/**
 * Math.atan2(y, x) - Returns the angle from the X axis to a point (x, y)
 * @param {number} y - Y coordinate
 * @param {number} x - X coordinate
 * @returns {number} Angle in radians (-π to π)
 */
Math.atan2(1, 1);           // 0.7853981633974483 (45° in radians)

/**
 * Hyperbolic functions (ES2015)
 * Math.sinh(x) - Hyperbolic sine
 * Math.cosh(x) - Hyperbolic cosine
 * Math.tanh(x) - Hyperbolic tangent
 * @param {number} x - A number
 * @returns {number} The hyperbolic function value
 */
Math.sinh(1);               // 1.1752011936438014
Math.cosh(1);               // 1.5430806348152437
Math.tanh(1);               // 0.7615941559557649
```

#### **6. Random Numbers and Special Functions**

##### **6.1 Random Number Generation**

```javascript
/**
 * Math.random() - Returns a pseudo-random number between 0 and 1
 * @returns {number} A random number between 0 (inclusive) and 1 (exclusive)
 */
Math.random();              // 0.123456789 (example)

/**
 * Generate random integer between min and max (inclusive)
 * @param {number} min - Minimum value (inclusive)
 * @param {number} max - Maximum value (inclusive)
 * @returns {number} Random integer between min and max
 */
function randomInt(min, max) {
  return Math.floor(Math.random() * (max - min + 1)) + min;
}
console.log(randomInt(1, 10)); // Random number between 1 and 10

/**
 * Generate random float between min and max
 * @param {number} min - Minimum value (inclusive)
 * @param {number} max - Maximum value (exclusive)
 * @returns {number} Random float between min and max
 */
function randomFloat(min, max) {
  return Math.random() * (max - min) + min;
}
console.log(randomFloat(0, 1)); // Random float between 0 and 1

/**
 * Get random element from array
 * @param {Array} array - The array to choose from
 * @returns {*} Random element from the array
 */
function randomChoice(array) {
  return array[Math.floor(Math.random() * array.length)];
}
let fruits = ['apple', 'banana', 'orange'];
console.log(randomChoice(fruits)); // Random fruit
```

##### **6.2 Special Functions**

```javascript
/**
 * Math.hypot(...values) - Returns the square root of the sum of squares
 * Useful for calculating distances (Euclidean norm)
 * @param {...number} values - Numbers to calculate hypotenuse from
 * @returns {number} √(value1² + value2² + ...)
 */
Math.hypot(3, 4);           // 5 (√(3² + 4²))
Math.hypot(1, 2, 2);        // 3 (√(1² + 2² + 2²))

/**
 * Math.clz32(x) - Counts leading zeros in 32-bit binary representation
 * @param {number} x - A number (converted to 32-bit unsigned int)
 * @returns {number} Number of leading zeros (0-32)
 */
Math.clz32(1);              // 31 (000...0001 has 31 leading zeros)
Math.clz32(1000);           // 22

/**
 * Math.imul(a, b) - 32-bit integer multiplication
 * Faster than regular multiplication for large integers
 * @param {number} a - First number
 * @param {number} b - Second number
 * @returns {number} 32-bit result of a * b
 */
Math.imul(2, 3);            // 6
Math.imul(0x7fffffff, 2);   // -2 (overflow handling)

/**
 * Math.fround(x) - Rounds to nearest 32-bit float representation
 * @param {number} x - A number
 * @returns {number} Nearest 32-bit float
 */
Math.fround(1.337);         // 1.3370000123977661 (32-bit float)

/**
 * Math.f16round(x) - Rounds to nearest 16-bit float (if supported)
 * @param {number} x - A number
 * @returns {number} Nearest 16-bit float
 */
Math.f16round(1.337);       // 1.3369140625 (16-bit float, if supported)
```

#### **7. Number Methods and Properties**

##### **7.1 Number Methods**

```javascript
let num = 123.456;

/**
 * Number.prototype.toString(radix) - Converts number to string
 * @param {number} [radix=10] - Base for conversion (2-36)
 * @returns {string} String representation of the number
 */
num.toString();             // "123.456"
num.toString(2);            // "1111011.0111010010111100011010101" (binary)
num.toString(16);           // "7b.74bc6a7ef9db" (hex)

/**
 * Number.prototype.toFixed(digits) - Formats with fixed decimal places
 * @param {number} [digits=0] - Number of decimal places (0-20)
 * @returns {string} Number with specified decimal places
 */
num.toFixed(2);             // "123.46"
num.toFixed(0);             // "123"

/**
 * Number.prototype.toPrecision(precision) - Formats with specified precision
 * @param {number} precision - Number of significant digits (1-21)
 * @returns {string} Number with specified significant digits
 */
num.toPrecision(4);         // "123.5"
num.toPrecision(2);         // "1.2e+2"

/**
 * Number.prototype.toExponential(fractionDigits) - Exponential notation
 * @param {number} [fractionDigits] - Decimal places in mantissa
 * @returns {string} Number in exponential notation
 */
num.toExponential(2);       // "1.23e+2"

/**
 * Number.prototype.toLocaleString(locales, options) - Localized formatting
 * @param {string|string[]} [locales] - BCP 47 language tags
 * @param {object} [options] - Formatting options
 * @returns {string} Localized string representation
 */
num.toLocaleString('en-US'); // "123.456"
num.toLocaleString('de-DE'); // "123,456"
(1234567.89).toLocaleString('en-IN'); // "12,34,567.89"
```

##### **7.2 Number Properties**

```javascript
/**
 * Number.MAX_SAFE_INTEGER - Largest integer that can be safely represented
 * @constant {number}
 */
Number.MAX_SAFE_INTEGER;    // 9007199254740991

/**
 * Number.MIN_SAFE_INTEGER - Smallest integer that can be safely represented
 * @constant {number}
 */
Number.MIN_SAFE_INTEGER;    // -9007199254740991

/**
 * Number.MAX_VALUE - Largest positive number representable
 * @constant {number}
 */
Number.MAX_VALUE;           // 1.7976931348623157e+308

/**
 * Number.MIN_VALUE - Smallest positive number representable
 * @constant {number}
 */
Number.MIN_VALUE;           // 5e-324

/**
 * Number.POSITIVE_INFINITY - Positive infinity
 * @constant {number}
 */
Number.POSITIVE_INFINITY;   // Infinity

/**
 * Number.NEGATIVE_INFINITY - Negative infinity
 * @constant {number}
 */
Number.NEGATIVE_INFINITY;   // -Infinity

/**
 * Number.NaN - Not-a-Number value
 * @constant {number}
 */
Number.NaN;                 // NaN

/**
 * Number.EPSILON - Smallest interval between two representable numbers
 * @constant {number}
 */
Number.EPSILON;             // 2.220446049250313e-16
```

##### **7.3 Number Checking Methods**

```javascript
/**
 * Number.isFinite(value) - Checks if value is a finite number
 * @param {*} value - Value to check
 * @returns {boolean} True if value is a finite number
 */
Number.isFinite(42);        // true
Number.isFinite(Infinity);  // false
Number.isFinite(NaN);       // false

/**
 * Number.isInteger(value) - Checks if value is an integer
 * @param {*} value - Value to check
 * @returns {boolean} True if value is an integer
 */
Number.isInteger(42);       // true
Number.isInteger(42.0);     // true
Number.isInteger(42.5);     // false

/**
 * Number.isNaN(value) - Checks if value is NaN (doesn't coerce)
 * @param {*} value - Value to check
 * @returns {boolean} True if value is NaN
 */
Number.isNaN(NaN);          // true
Number.isNaN("abc");        // false (doesn't coerce)

/**
 * Number.isSafeInteger(value) - Checks if value is a safe integer
 * @param {*} value - Value to check
 * @returns {boolean} True if value is a safe integer
 */
Number.isSafeInteger(42);   // true
Number.isSafeInteger(2**53); // false

/**
 * Check if integer is safe (utility function)
 * @param {number} num - Number to check
 * @returns {boolean} True if number is a safe integer
 */
Number.isSafeInteger(9007199254740991);  // true
Number.isSafeInteger(9007199254740992);  // false
```

#### **8. BigInt for Large Numbers**

```javascript
// Creating BigInts
let big1 = 123456789012345678901234567890n;
let big2 = BigInt("123456789012345678901234567890");

// Operations
big1 + big2;     // 246913578024691357802469135780n
big1 * 2n;       // 246913578024691357802469135780n
big1 ** 2n;      // Very large number

// Cannot mix with regular numbers
// big1 + 1;     // TypeError
big1 + BigInt(1); // Works

// Comparison
big1 > big2;     // false
big1 === big2;   // false

// Conversion
String(big1);    // "123456789012345678901234567890"
Number(big1);    // 1.2345678901234568e+29 (may lose precision)
```

#### **9. Practical Mathematical Examples**

##### **9.1 Distance Calculations**

```javascript
// Euclidean distance between two points
function distance(x1, y1, x2, y2) {
  return Math.hypot(x2 - x1, y2 - y1);
}
console.log(distance(0, 0, 3, 4)); // 5

// Manhattan distance
function manhattanDistance(x1, y1, x2, y2) {
  return Math.abs(x2 - x1) + Math.abs(y2 - y1);
}
console.log(manhattanDistance(0, 0, 3, 4)); // 7
```

##### **9.2 Statistical Functions**

```javascript
function average(numbers) {
  return numbers.reduce((sum, num) => sum + num, 0) / numbers.length;
}

function median(numbers) {
  let sorted = [...numbers].sort((a, b) => a - b);
  let mid = Math.floor(sorted.length / 2);
  return sorted.length % 2 === 0
    ? (sorted[mid - 1] + sorted[mid]) / 2
    : sorted[mid];
}

function standardDeviation(numbers) {
  let avg = average(numbers);
  let variance = numbers.reduce((sum, num) => sum + Math.pow(num - avg, 2), 0) / numbers.length;
  return Math.sqrt(variance);
}

let data = [1, 2, 3, 4, 5];
console.log(average(data));        // 3
console.log(median(data));         // 3
console.log(standardDeviation(data)); // 1.4142135623730951
```

##### **9.3 Financial Calculations**

```javascript
// Compound interest
function compoundInterest(principal, rate, time, compoundsPerYear = 1) {
  return principal * Math.pow(1 + rate / compoundsPerYear, compoundsPerYear * time);
}

console.log(compoundInterest(1000, 0.05, 5)); // 1276.2815625000003

// Loan payment calculation
function loanPayment(principal, annualRate, years) {
  let monthlyRate = annualRate / 12;
  let months = years * 12;
  return principal * (monthlyRate * Math.pow(1 + monthlyRate, months)) /
         (Math.pow(1 + monthlyRate, months) - 1);
}

console.log(loanPayment(100000, 0.06, 30)); // 599.5505251526898
```

##### **9.4 Game Development Math**

```javascript
// Linear interpolation (lerp)
function lerp(start, end, factor) {
  return start + (end - start) * factor;
}
console.log(lerp(0, 100, 0.5)); // 50

// Clamp angle to 0-360 degrees
function clampAngle(angle) {
  return ((angle % 360) + 360) % 360;
}
console.log(clampAngle(450)); // 90

// Check if point is inside circle
function isInsideCircle(x, y, centerX, centerY, radius) {
  return Math.hypot(x - centerX, y - centerY) <= radius;
}
console.log(isInsideCircle(3, 4, 0, 0, 5)); // true
```

#### **10. Best Practices**

- Use `Number.isNaN()` instead of global `isNaN()` to avoid type coercion.
- Check for safe integers when dealing with large numbers.
- Use `Math.round()` for general rounding, but consider specific needs.
- Prefer `Math.hypot()` for distance calculations to avoid overflow.
- Use `Number.EPSILON` for floating-point comparisons.
- Consider BigInt for financial calculations requiring precision.
- Use appropriate precision methods (`toFixed()`, `toPrecision()`).
- Validate numeric inputs before mathematical operations.
- Use `Math.random()` with proper scaling for random integers.
- Consider performance implications of different Math methods.

#### **11. Common Mistakes**

- Using `==` or `!=` with NaN (always false).
- Assuming floating-point arithmetic is exact.
- Not checking for division by zero.
- Using `Math.round()` when `Math.floor()` or `Math.ceil()` is needed.
- Forgetting that `Math.min()` and `Math.max()` don't work with arrays directly.
- Assuming `parseInt()` without radix parameter.
- Not handling overflow/underflow in calculations.
- Using regular numbers for very large integers.
- Confusing radians and degrees in trigonometric functions.
- Not considering precision loss in financial calculations.

#### **12. Performance Considerations**

```javascript
// Cache Math constants for better performance
const PI = Math.PI;
const E = Math.E;

// Use lookup tables for expensive calculations
const sinLookup = [];
for (let i = 0; i <= 360; i++) {
  sinLookup[i] = Math.sin(i * Math.PI / 180);
}

// Bitwise operations for integer math (faster but less readable)
function fastAbs(x) {
  return x < 0 ? -x : x; // or use Math.abs(x)
}

// Integer division
function intDiv(a, b) {
  return Math.floor(a / b); // or use (a / b) | 0 for positive numbers
}
```

#### **13. Summary**

| Category              | Status | Completion |
|-----------------------|--------|------------|
| Number basics         | ✓      | 100%       |
| Math constants        | ✓      | 100%       |
| Arithmetic functions  | ✓      | 100%       |
| Rounding methods      | ✓      | 100%       |
| Trigonometric functions| ✓      | 100%       |
| Random numbers        | ✓      | 100%       |
| Number methods        | ✓      | 100%       |
| BigInt support        | ✓      | 100%       |
| Practical examples    | ✓      | 100%       |
| Best practices        | ✓      | 100%       |
| Common mistakes       | ✓      | 100%       |
| Performance tips      | ✓      | 100%       |

Overall Completion: 100% 📊

Master JavaScript numbers and Math by understanding the number system, using appropriate Math methods for different calculations, and being aware of floating-point precision limitations. Practice with real-world mathematical problems to build strong numerical computation skills.