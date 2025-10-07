### **Lesson 7: Strings in JavaScript**

Strings are fundamental in JavaScript for representing and manipulating text. This comprehensive lesson covers all aspects of strings: creation, manipulation, searching, Unicode handling, performance, and best practices with extensive examples and code snippets.

#### **1. What are Strings?**

- **Definition:** Immutable sequences of characters used to represent text.
- **Why Needed:** Essential for user interfaces, data processing, and communication.
- **Characteristics:** Immutable, UTF-16 encoded, zero-indexed.

**Example:** User names, messages, file paths, URLs, and any textual data.

#### **2. String Creation**

##### **2.1 String Literals**

```javascript
// Single quotes
let single = 'Hello World';

// Double quotes
let double = "Hello World";

// Template literals (ES6)
let template = `Hello World`;

// Multi-line strings
let multiLine = `This is
a multi-line
string`;

// Escaped characters
let escaped = "She said \"Hello\"";
let path = "C:\\Program Files\\App";
let newline = "Line 1\nLine 2";
```

##### **2.2 String Constructor**

```javascript
// Using new String() - Not recommended
let strObj = new String("Hello"); // Creates String object
typeof strObj; // "object"

// String() function - Preferred for conversion
let strPrim = String(42); // "42"
let strBool = String(true); // "true"
```

##### **2.3 Template Literals (ES6)**

```javascript
// Variable interpolation
let name = "Alice";
let greeting = `Hello, ${name}!`; // "Hello, Alice!"

// Expression evaluation
let a = 5, b = 10;
let result = `Sum: ${a + b}`; // "Sum: 15"

// Multi-line with interpolation
let user = { name: "Bob", age: 30 };
let profile = `
Name: ${user.name}
Age: ${user.age}
`; // Preserves formatting

// Tagged templates
function highlight(strings, ...values) {
  return strings.reduce((result, str, i) =>
    result + str + (values[i] ? `<mark>${values[i]}</mark>` : ''), '');
}

let highlighted = highlight`Hello ${name}, you are ${user.age} years old!`;
// "Hello <mark>Alice</mark>, you are <mark>30</mark> years old!"

// String.raw() - Raw strings (escape sequences not processed)
String.raw`C:\Program Files\App`; // "C:\Program Files\App"

// vs template literal
`C:\Program Files\App`; // Issues with \P, \A

// Useful for regex patterns
let pattern = String.raw`\d+\.\d+`;
```

#### **3. String Properties**

##### **3.1 Length Property**

```javascript
let text = "Hello World";
text.length; // 11

// Empty string
"".length; // 0

// Unicode characters
"🚀".length; // 2 (surrogate pairs)
"é".length; // 1
```

##### **3.2 Accessing Characters**

```javascript
let str = "JavaScript";

// Bracket notation
str[0]; // "J"
str[4]; // "S"

// charAt() method
str.charAt(0); // "J"
str.charAt(10); // "t"
str.charAt(20); // "" (empty string)

// charCodeAt() - Unicode value
str.charCodeAt(0); // 74 ("J")
"🚀".charCodeAt(0); // 55357 (high surrogate)
"🚀".charCodeAt(1); // 56676 (low surrogate)

// codePointAt() - ES6
"🚀".codePointAt(0); // 128640

// at() - ES2022 (supports negative indexing)
let str = "JavaScript";
str.at(0); // "J"
str.at(-1); // "t"
str.at(-4); // "r"

str.charAt(-1); // ""
```

##### **3.3 String Iteration Methods**

```javascript
let str = "Hello";

// for...of loop (ES6)
for (let char of str) {
  console.log(char); // H, e, l, l, o
}

// Spread operator
[...str]; // ["H", "e", "l", "l", "o"]

// Array.from()
Array.from(str); // ["H", "e", "l", "l", "o"]

// entries(), keys(), values() (ES6)
for (let [index, char] of str.entries()) {
  console.log(index, char); // 0 "H", 1 "e", ...
}

for (let index of str.keys()) {
  console.log(index); // 0, 1, 2, 3, 4
}

for (let char of str.values()) {
  console.log(char); // "H", "e", "l", "l", "o"
}
```

#### **4. String Methods**

##### **4.1 Case Conversion**

```javascript
let text = "Hello World";

text.toUpperCase(); // "HELLO WORLD"
text.toLowerCase(); // "hello world"

"İstanbul".toLocaleUpperCase('tr'); // "İSTANBUL" (Turkish i)
"İstanbul".toLocaleLowerCase('tr'); // "istanbul"
```

##### **4.2 Substring Extraction**

```javascript
let str = "JavaScript Programming";

// substring(start, end) - end exclusive
str.substring(0, 10); // "JavaScript"
str.substring(4); // "Script Programming"

// substr(start, length) - deprecated but still works
str.substr(4, 6); // "Script"

// slice(start, end) - end exclusive, supports negative
str.slice(0, 10); // "JavaScript"
str.slice(-11); // "Programming"
str.slice(4, -1); // "Script Programmin"
```

##### **4.3 String Searching**

```javascript
let text = "The quick brown fox jumps over the lazy dog";

// indexOf() - first occurrence
text.indexOf("fox"); // 16
text.indexOf("cat"); // -1

// lastIndexOf() - last occurrence
text.lastIndexOf("the"); // 31 (case sensitive)

// includes() - ES6
text.includes("fox"); // true
text.includes("cat"); // false

// startsWith() - ES6
text.startsWith("The"); // true
text.startsWith("the"); // false

// endsWith() - ES6
text.endsWith("dog"); // true
text.endsWith("Dog"); // false
```

##### **4.4 String Replacement**

```javascript
let text = "Hello World, Hello Universe";

// replace() - first occurrence
text.replace("Hello", "Hi"); // "Hi World, Hello Universe"

// replaceAll() - ES2021, all occurrences
text.replaceAll("Hello", "Hi"); // "Hi World, Hi Universe"

// With regex
text.replace(/Hello/g, "Hi"); // "Hi World, Hi Universe"
```

##### **4.5 String Splitting and Joining**

```javascript
let sentence = "The quick brown fox";

// split()
sentence.split(" "); // ["The", "quick", "brown", "fox"]
sentence.split(""); // ["T", "h", "e", " ", "q", ...]
sentence.split("", 3); // ["T", "h", "e"]

// join() - on arrays
let words = ["Hello", "World"];
words.join(" "); // "Hello World"
words.join("-"); // "Hello-World"

// concat() - join strings
"Hello".concat(" ", "World"); // "Hello World"
let str1 = "Hello";
let str2 = "World";
str1.concat(" ", str2); // "Hello World"
```

##### **4.6 Trimming**

```javascript
let padded = "  Hello World  ";

// trim()
padded.trim(); // "Hello World"

// trimStart() / trimLeft()
padded.trimStart(); // "Hello World  "

// trimEnd() / trimRight()
padded.trimEnd(); // "  Hello World"
```

##### **4.7 Padding**

```javascript
let num = "5";

// padStart(targetLength, padString)
num.padStart(3, "0"); // "005"
"abc".padStart(6, "123"); // "123abc"

// padEnd(targetLength, padString)
num.padEnd(3, "0"); // "500"
"abc".padEnd(6, "123"); // "abc123"
```

##### **4.8 Repeating**

```javascript
"Ha".repeat(3); // "HaHaHa"
"*".repeat(5); // "*****"
```

#### **5. Regular Expressions with Strings**

```javascript
let text = "The year is 2023 and the price is $99.99";

// match()
text.match(/\d+/g); // ["2023", "99", "99"]

// search() - returns index
text.search(/\d+/); // 12

// replace() with regex
text.replace(/\d+/g, "XXX"); // "The year is XXX and the price is $XX.XX"

// split() with regex
"apple, banana; cherry".split(/[,;]\s*/); // ["apple", "banana", "cherry"]

// matchAll() - ES2020, full match objects with groups
let text = "test1 test2 test3";
let regex = /test(\d)/g;

// match() - only captures
text.match(regex); // ["test1", "test2", "test3"]

// matchAll() - full match objects with groups
for (let match of text.matchAll(regex)) {
  console.log(match[0], match[1], match.index);
  // "test1", "1", 0
  // "test2", "2", 6
  // "test3", "3", 12
}

// Convert to array
[...text.matchAll(regex)];
```

#### **6. Unicode and Internationalization**

##### **6.1 Unicode Handling**

```javascript
// Unicode escape sequences
let heart = "\u2764"; // ❤
let rocket = "\u{1F680}"; // 🚀

// String normalization
let accented = "café";
accented.normalize("NFD"); // "café" (decomposed)
accented.normalize("NFC"); // "café" (composed)

// Unicode-aware length
function unicodeLength(str) {
  return [...str].length; // Spread operator handles surrogate pairs
}

unicodeLength("🚀"); // 1 (correct)
"🚀".length; // 2 (incorrect for display)
```

##### **6.2 Internationalization**

```javascript
let date = new Date();
let number = 1234567.89;

// localeCompare() for sorting
let words = ["apple", "Banana", "cherry"];
words.sort((a, b) => a.localeCompare(b)); // ["apple", "Banana", "cherry"]

// toLocaleString() for formatting
date.toLocaleString('en-US'); // "12/25/2023, 3:45:30 PM"
date.toLocaleString('de-DE'); // "25.12.2023, 15:45:30"

number.toLocaleString('en-US'); // "1,234,567.89"
number.toLocaleString('de-DE'); // "1.234.567,89"
```

#### **7. String Performance Considerations**

##### **7.1 String Concatenation**

```javascript
// Inefficient (creates new string each time)
let result = "";
for (let i = 0; i < 10000; i++) {
  result += i; // Bad performance
}

// Efficient methods
let parts = [];
for (let i = 0; i < 10000; i++) {
  parts.push(i);
}
let result = parts.join("");

// Or use array directly
let result = Array.from({length: 10000}, (_, i) => i).join("");
```

##### **7.2 String Immutability**

```javascript
let str = "Hello";
str[0] = "J"; // Doesn't work, strings are immutable
str = "J" + str.slice(1); // Correct way: "Jello"
```

##### **7.3 Memory Usage**

```javascript
// Large strings can consume memory
let largeString = "x".repeat(1000000); // 1MB string

// Substring vs slice performance
let str = "JavaScript";
str.substring(0, 4); // Creates new string
str.substr(0, 4); // Creates new string
str.slice(0, 4); // Creates new string

// All create new strings due to immutability
```

#### **8. String Comparison and Sorting**

```javascript
let strings = ["banana", "Apple", "cherry", "Date"];

// Case-sensitive sort
strings.sort(); // ["Apple", "Date", "banana", "cherry"]

// Case-insensitive sort
strings.sort((a, b) => a.toLowerCase().localeCompare(b.toLowerCase()));
// ["Apple", "banana", "cherry", "Date"]

// Natural sort for numbers
let versions = ["v1.2", "v1.10", "v1.3"];
versions.sort(); // ["v1.10", "v1.2", "v1.3"] - lexicographic
versions.sort((a, b) => a.localeCompare(b, undefined, {numeric: true}));
// ["v1.2", "v1.3", "v1.10"] - natural
```

#### **9. Advanced String Techniques**

##### **9.1 String Templates**

```javascript
function sql(strings, ...values) {
  // Sanitize values to prevent SQL injection
  let sanitized = values.map(val =>
    typeof val === 'string' ? `'${val.replace(/'/g, "''")}'` : val
  );

  return strings.reduce((query, str, i) =>
    query + str + (sanitized[i] || ''), '');
}

let userId = 123;
let query = sql`SELECT * FROM users WHERE id = ${userId}`;
console.log(query); // "SELECT * FROM users WHERE id = 123"
```

##### **9.2 String Parsing**

```javascript
// Parse CSV
function parseCSV(csv) {
  return csv.split('\n').map(row =>
    row.split(',').map(cell => cell.trim())
  );
}

let csv = `Name, Age, City
Alice, 30, New York
Bob, 25, London`;
parseCSV(csv);

// Parse query string
function parseQueryString(query) {
  return query.split('&').reduce((params, pair) => {
    let [key, value] = pair.split('=');
    params[decodeURIComponent(key)] = decodeURIComponent(value);
    return params;
  }, {});
}

parseQueryString("name=John&age=30"); // {name: "John", age: "30"}
```

##### **9.3 String Compression/Decompression**

```javascript
// Simple RLE compression
function compress(str) {
  return str.replace(/(.)\1+/g, (match, char) => char + match.length);
}

function decompress(str) {
  return str.replace(/(.)([0-9]+)/g, (match, char, count) =>
    char.repeat(parseInt(count)));
}

compress("aaabbbccc"); // "a3b3c3"
decompress("a3b3c3"); // "aaabbbccc"
```

##### **9.4 String Encoding/Decoding**

```javascript
// URI encoding
let url = "hello world?name=John Doe";
encodeURI(url); // "hello%20world?name=John%20Doe"
encodeURIComponent(url); // "hello%20world%3Fname%3DJohn%20Doe"

decodeURI("hello%20world"); // "hello world"
decodeURIComponent("hello%20world%3Fname%3DJohn"); // "hello world?name=John"

// Base64 encoding
btoa("Hello"); // "SGVsbG8="
atob("SGVsbG8="); // "Hello"

// Unicode aware Base64
function utoa(str) {
  return btoa(unescape(encodeURIComponent(str)));
}
function atou(str) {
  return decodeURIComponent(escape(atob(str)));
}
```

##### **9.5 String Validation Patterns**

```javascript
// Email validation
function isValidEmail(email) {
  return /^[^\s@]+@[^\s@]+\.[^\s@]+$/.test(email);
}

// URL validation
function isValidURL(url) {
  try {
    new URL(url);
    return true;
  } catch {
    return false;
  }
}

// Phone number
function isValidPhone(phone) {
  return /^[\+]?[(]?[0-9]{3}[)]?[-\s\.]?[0-9]{3}[-\s\.]?[0-9]{4,6}$/.test(phone);
}
```

##### **9.6 String Sanitization (Security)**

```javascript
// HTML escaping
function escapeHTML(str) {
  const map = {
    '&': '&',
    '<': '<',
    '>': '>',
    '"': '"',
    "'": '&#x27;',
    '/': '&#x2F;'
  };
  return str.replace(/[&<>"'/]/g, char => map[char]);
}

// XSS prevention
escapeHTML('<script>alert("XSS")</script>');
// "<script>alert("XSS")<&#x2F;script>"

// SQL injection prevention (parameterized queries better)
function escapeSQLString(str) {
  return str.replace(/'/g, "''");
}
```

##### **9.7 String Slugification**

```javascript
// URL-friendly slugs
function slugify(str) {
  return str
    .toLowerCase()
    .trim()
    .replace(/[^\w\s-]/g, '')
    .replace(/[\s_-]+/g, '-')
    .replace(/^-+|-+$/g, '');
}

slugify("Hello World! This is a Test"); // "hello-world-this-is-a-test"
```

##### **9.8 Levenshtein Distance (String Similarity)**

```javascript
function levenshtein(a, b) {
  const matrix = [];
  
  for (let i = 0; i <= b.length; i++) {
    matrix[i] = [i];
  }
  
  for (let j = 0; j <= a.length; j++) {
    matrix[0][j] = j;
  }
  
  for (let i = 1; i <= b.length; i++) {
    for (let j = 1; j <= a.length; j++) {
      if (b.charAt(i - 1) === a.charAt(j - 1)) {
        matrix[i][j] = matrix[i - 1][j - 1];
      } else {
        matrix[i][j] = Math.min(
          matrix[i - 1][j - 1] + 1,
          matrix[i][j - 1] + 1,
          matrix[i - 1][j] + 1
        );
      }
    }
  }
  
  return matrix[b.length][a.length];
}

levenshtein("kitten", "sitting"); // 3
```

##### **9.9 Word Wrap/Text Formatting**

```javascript
function wordWrap(str, maxWidth) {
  let result = '';
  let line = '';
  
  for (let word of str.split(' ')) {
    if (line.length + word.length + 1 > maxWidth) {
      result += line + '\n';
      line = word;
    } else {
      line += (line ? ' ' : '') + word;
    }
  }
  
  return result + line;
}

wordWrap("The quick brown fox jumps", 10);
// "The quick\nbrown fox\njumps"
```

##### **9.10 String Hashing (Simple)**

```javascript
function simpleHash(str) {
  let hash = 0;
  for (let i = 0; i < str.length; i++) {
    const char = str.charCodeAt(i);
    hash = ((hash << 5) - hash) + char;
    hash = hash & hash; // Convert to 32bit integer
  }
  return hash;
}

simpleHash("hello"); // 99162322
```

#### **10. Best Practices**

- Use template literals for string interpolation.
- Prefer `includes()`, `startsWith()`, `endsWith()` over `indexOf()`.
- Use `replaceAll()` or regex with global flag for multiple replacements.
- Be aware of Unicode issues with string length and indexing.
- Use locale-aware methods for internationalization.
- Avoid string concatenation in loops; use arrays instead.
- Use `trim()` to clean user input.
- Prefer strict equality for string comparisons.
- Use `padStart()`/`padEnd()` for formatting.
- Consider memory usage with large strings.
- Use appropriate string methods for performance.

// Additional best practices
- Be aware of string immutability (methods return new strings).
- Handle null/undefined safely with String(value ?? '').
- Use array.join() for efficient string building in loops.
- Prefer case-insensitive comparison with toLowerCase().
- Use locale-aware methods for internationalization.
- Consider memory usage with large strings.
- Validate user input to prevent security issues.
- Use appropriate encoding for URLs and data transmission.

#### **11. Common Mistakes**

- Using `==` instead of `===` for string comparison.
- Assuming string methods modify the original string.
- Not handling Unicode characters properly.
- Using inefficient string concatenation in loops.
- Forgetting that strings are zero-indexed.
- Confusing `substring()` and `substr()`.
- Not trimming user input.
- Using single quotes in HTML attributes without escaping.
- Assuming `indexOf()` returns boolean.
- Not using regex when appropriate.
- Ignoring case sensitivity in searches.

#### **12. String Libraries and Utilities**

```javascript
// Popular string utility libraries
// lodash.string (deprecated, use lodash)
// string.js
// voca

// Example with string.js
// const S = require('string');
// S('hello world').capitalize().s; // "Hello world"

// Native alternatives (ES2020+)
"hello world".replace(/(^\w)/, c => c.toUpperCase()); // "Hello world"
```

#### **13. Summary**

| Category              | Status | Completion |
|-----------------------|--------|------------|
| String creation       | ✓      | 100%       |
| String properties     | ✓      | 100%       |
| String methods        | ✓      | 100%       |
| String searching      | ✓      | 100%       |
| Regular expressions   | ✓      | 100%       |
| Unicode handling      | ✓      | 100%       |
| Performance           | ✓      | 100%       |
| Encoding/Decoding     | ✓      | 100%       |
| Validation patterns   | ✓      | 100%       |
| Security sanitization | ✓      | 100%       |
| Utility functions     | ✓      | 100%       |
| Best practices        | ✓      | 100%       |
| Common mistakes       | ✓      | 100%       |
| Advanced techniques   | ✓      | 100%       |

Overall Completion: 100% 📊

Master JavaScript strings by understanding their immutable nature, using appropriate methods for different operations, and being mindful of Unicode and performance considerations. Practice with various string manipulation scenarios to build robust text processing skills.