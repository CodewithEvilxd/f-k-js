### **Lesson 10: Arrays in JavaScript**

Arrays are fundamental data structures in JavaScript used to store and manipulate collections of data. This comprehensive lesson covers every aspect of arrays: creation, manipulation, iteration, searching, sorting, performance, and advanced techniques with extensive examples and detailed documentation.

#### **1. What are Arrays in JavaScript?**

- **Definition:** Ordered collections of elements that can hold any data type.
- **Characteristics:** Dynamic size, zero-indexed, mutable, can contain mixed data types.
- **Use Cases:** Lists, queues, stacks, matrices, data processing, API responses.

**Example:** Shopping cart items, user lists, coordinates, configuration options.

#### **2. Array Creation and Initialization**

##### **2.1 Array Literal Syntax**

```javascript
/**
 * Array literal - most common way to create arrays
 * @type {Array}
 */

// Empty array
const emptyArray = [];

// Array with elements
const numbers = [1, 2, 3, 4, 5];
const fruits = ['apple', 'banana', 'orange'];
const mixed = [1, 'hello', true, null, {name: 'John'}];

// Nested arrays (multi-dimensional)
const matrix = [
  [1, 2, 3],
  [4, 5, 6],
  [7, 8, 9]
];

// Sparse arrays (with gaps)
const sparse = [1, , 3]; // [1, empty, 3]
console.log(sparse.length); // 3
console.log(sparse[1]); // undefined
```

##### **2.2 Array Constructor**

```javascript
/**
 * Array() constructor - less common, can be confusing
 */

// Empty array
const empty1 = new Array(); // []
const empty2 = new Array(0); // []

// Array with specific length (filled with undefined)
const sized = new Array(5); // [undefined, undefined, undefined, undefined, undefined]

// Array with elements (confusing with single number)
const singleElement = new Array(3); // Creates array of length 3
const threeElements = [3]; // Creates array with element 3

// Recommended: use array literals instead
const goodPractice = [1, 2, 3]; // Clear intent
```

##### **2.3 Array.from() Method**

```javascript
/**
 * Array.from() - Creates array from array-like or iterable objects
 * @param {ArrayLike|Iterable} source - Source to convert
 * @param {Function} [mapFn] - Optional mapping function
 * @param {*} [thisArg] - Optional this context for mapFn
 * @returns {Array} New array
 */

// From string
Array.from('hello'); // ['h', 'e', 'l', 'l', 'o']

// From Set
Array.from(new Set([1, 2, 3, 2])); // [1, 2, 3]

// From Map
const map = new Map([['a', 1], ['b', 2]]);
Array.from(map); // [['a', 1], ['b', 2]]
Array.from(map.keys()); // ['a', 'b']
Array.from(map.values()); // [1, 2]

// From NodeList (DOM elements)
const divs = document.querySelectorAll('div');
const divArray = Array.from(divs);

// With mapping function
Array.from([1, 2, 3], x => x * 2); // [2, 4, 6]
Array.from('123', Number); // [1, 2, 3]

// Create range array
Array.from({length: 5}, (_, i) => i + 1); // [1, 2, 3, 4, 5]
```

##### **2.4 Array.of() Method**

```javascript
/**
 * Array.of() - Creates array with specified elements
 * @param {...*} elements - Elements to include in array
 * @returns {Array} New array with specified elements
 */

// Unlike Array() constructor, always creates array with elements
Array.of(3); // [3] (not array of length 3)
Array.of(1, 2, 3); // [1, 2, 3]

// Useful for creating arrays with single number
Array.of(5); // [5]
new Array(5); // [undefined, undefined, undefined, undefined, undefined]
```

##### **2.5 Other Creation Methods**

```javascript
// Array.fill() - Fill array with value
const filled = new Array(3).fill(0); // [0, 0, 0]
const partialFill = [1, 2, 3, 4, 5].fill(0, 2, 4); // [1, 2, 0, 0, 5]

// Array spread syntax
const original = [1, 2, 3];
const copy = [...original]; // [1, 2, 3]
const combined = [...original, 4, 5]; // [1, 2, 3, 4, 5]

// Array destructuring
const [first, second, ...rest] = [1, 2, 3, 4, 5];
console.log(first); // 1
console.log(second); // 2
console.log(rest); // [3, 4, 5]
```

##### **2.5 Array Iterator Methods**

```javascript
/**
 * Array.prototype.keys() - Returns iterator for array indices
 * @returns {Iterator} Iterator yielding array indices
 */
const arr = ['a', 'b', 'c'];
const keysIterator = arr.keys();

for (const key of keysIterator) {
  console.log(key); // 0, 1, 2
}

// Convert to array
Array.from(arr.keys()); // [0, 1, 2]

/**
 * Array.prototype.values() - Returns iterator for array values
 * @returns {Iterator} Iterator yielding array values
 */
const valuesIterator = arr.values();

for (const value of valuesIterator) {
  console.log(value); // 'a', 'b', 'c'
}

// Convert to array
Array.from(arr.values()); // ['a', 'b', 'c']

/**
 * Array.prototype.entries() - Returns iterator for [index, value] pairs
 * @returns {Iterator} Iterator yielding [index, value] pairs
 */
const entriesIterator = arr.entries();

for (const [index, value] of entriesIterator) {
  console.log(`${index}: ${value}`); // '0: a', '1: b', '2: c'
}

// Convert to array
Array.from(arr.entries()); // [[0, 'a'], [1, 'b'], [2, 'c']]

// Practical use: Object.fromEntries with array
const arrayToObject = Object.fromEntries(arr.entries());
// {0: 'a', 1: 'b', 2: 'c'}
```

#### **3. Array Properties**

##### **3.1 Length Property**

```javascript
/**
 * Array.length - Gets or sets the number of elements in array
 * @type {number}
 */

// Getting length
const arr = [1, 2, 3, 4, 5];
console.log(arr.length); // 5

// Setting length (can truncate or extend)
arr.length = 3; // [1, 2, 3]
arr.length = 5; // [1, 2, 3, undefined, undefined]

// Setting length to 0 empties array
arr.length = 0; // []

// Length is always last index + 1
const sparse = [];
sparse[10] = 'hello';
console.log(sparse.length); // 11
```

#### **4. Array Access and Modification**

##### **4.1 Bracket Notation**

```javascript
const arr = ['a', 'b', 'c', 'd', 'e'];

// Reading elements
console.log(arr[0]); // 'a'
console.log(arr[2]); // 'c'

// Writing elements
arr[1] = 'B'; // ['a', 'B', 'c', 'd', 'e']

// Adding elements at specific index
arr[5] = 'f'; // ['a', 'B', 'c', 'd', 'e', 'f']

// Negative indices don't work (unlike some languages)
console.log(arr[-1]); // undefined
```

##### **4.2 at() Method (ES2022)**

```javascript
/**
 * Array.prototype.at() - Accesses element at index, supports negative indices
 * @param {number} index - Index to access (negative indices count from end)
 * @returns {*} Element at specified index, or undefined if out of bounds
 */
const arr = ['a', 'b', 'c', 'd', 'e'];

// Positive indices (same as bracket notation)
arr.at(0); // 'a'
arr.at(2); // 'c'

// Negative indices (count from end)
arr.at(-1); // 'e' (last element)
arr.at(-2); // 'd' (second to last)

// Out of bounds
arr.at(10); // undefined
arr.at(-10); // undefined

// Comparison with bracket notation
const lastElement = arr[arr.length - 1]; // 'e' (traditional way)
const lastElementNew = arr.at(-1); // 'e' (modern way)
```

##### **4.2 Array Destructuring**

```javascript
const colors = ['red', 'green', 'blue', 'yellow'];

// Basic destructuring
const [first, second] = colors;
console.log(first); // 'red'
console.log(second); // 'green'

// Skip elements
const [primary, , tertiary] = colors;
console.log(primary); // 'red'
console.log(tertiary); // 'blue'

// Rest operator
const [head, ...tail] = colors;
console.log(head); // 'red'
console.log(tail); // ['green', 'blue', 'yellow']

// Default values
const [a = 'default', b = 'default'] = ['value'];
console.log(a); // 'value'
console.log(b); // 'default'

// Swapping values
let x = 1, y = 2;
[x, y] = [y, x];
console.log(x, y); // 2, 1
```

#### **5. Array Methods - Adding and Removing Elements**

##### **5.1 push() and pop()**

```javascript
/**
 * Array.prototype.push() - Adds elements to end of array
 * @param {...*} elements - Elements to add
 * @returns {number} New length of array
 */
const arr = [1, 2, 3];
arr.push(4); // [1, 2, 3, 4], returns 4
arr.push(5, 6); // [1, 2, 3, 4, 5, 6], returns 6

/**
 * Array.prototype.pop() - Removes last element from array
 * @returns {*} The removed element
 */
const last = arr.pop(); // 6, arr is now [1, 2, 3, 4, 5]
```

##### **5.2 unshift() and shift()**

```javascript
/**
 * Array.prototype.unshift() - Adds elements to beginning of array
 * @param {...*} elements - Elements to add
 * @returns {number} New length of array
 */
const arr = [3, 4, 5];
arr.unshift(1, 2); // [1, 2, 3, 4, 5], returns 5

/**
 * Array.prototype.shift() - Removes first element from array
 * @returns {*} The removed element
 */
const first = arr.shift(); // 1, arr is now [2, 3, 4, 5]
```

##### **5.3 splice() Method**

```javascript
/**
 * Array.prototype.splice() - Changes contents of array by removing/replacing existing elements
 * @param {number} start - Index to start changing array
 * @param {number} deleteCount - Number of elements to remove
 * @param {...*} items - Elements to add
 * @returns {Array} Array of removed elements
 */
const arr = ['a', 'b', 'c', 'd', 'e'];

// Remove elements
const removed = arr.splice(2, 2); // ['c', 'd'], arr is ['a', 'b', 'e']

// Add elements
arr.splice(2, 0, 'c', 'd'); // [], arr is ['a', 'b', 'c', 'd', 'e']

// Replace elements
arr.splice(1, 2, 'x', 'y'); // ['b', 'c'], arr is ['a', 'x', 'y', 'd', 'e']

// Negative indices
arr.splice(-2, 1, 'z'); // ['d'], arr is ['a', 'x', 'y', 'z', 'e']
```

##### **5.4 slice() Method**

```javascript
/**
 * Array.prototype.slice() - Returns shallow copy of portion of array
 * @param {number} [start=0] - Start index (inclusive)
 * @param {number} [end=array.length] - End index (exclusive)
 * @returns {Array} New array with extracted elements
 */
const arr = ['a', 'b', 'c', 'd', 'e'];

// Extract portion
arr.slice(1, 4); // ['b', 'c', 'd']
arr.slice(2); // ['c', 'd', 'e']

// Negative indices
arr.slice(-3); // ['c', 'd', 'e']
arr.slice(-3, -1); // ['c', 'd']

// Copy entire array
arr.slice(); // ['a', 'b', 'c', 'd', 'e']

// Shallow copy
const nested = [[1, 2], [3, 4]];
const copy = nested.slice();
copy[0][0] = 99; // Affects both arrays (shallow copy)
console.log(nested[0][0]); // 99
```

#### **6. Array Methods - Searching and Finding**

##### **6.1 indexOf() and lastIndexOf()**

```javascript
/**
 * Array.prototype.indexOf() - Returns first index of element
 * @param {*} searchElement - Element to search for
 * @param {number} [fromIndex=0] - Index to start searching
 * @returns {number} Index of element, or -1 if not found
 */
const arr = ['a', 'b', 'c', 'b', 'a'];
arr.indexOf('b'); // 1
arr.indexOf('b', 2); // 3
arr.indexOf('z'); // -1

/**
 * Array.prototype.lastIndexOf() - Returns last index of element
 * @param {*} searchElement - Element to search for
 * @param {number} [fromIndex=array.length-1] - Index to start searching backwards
 * @returns {number} Index of element, or -1 if not found
 */
arr.lastIndexOf('b'); // 3
arr.lastIndexOf('a'); // 4
```

##### **6.2 includes() Method**

```javascript
/**
 * Array.prototype.includes() - Checks if array contains element
 * @param {*} searchElement - Element to search for
 * @param {number} [fromIndex=0] - Index to start searching
 * @returns {boolean} True if element is found
 */
const arr = [1, 2, 3, NaN, 'hello'];
arr.includes(2); // true
arr.includes(4); // false
arr.includes(NaN); // true (unlike indexOf)
arr.includes('hello', 3); // true
```

##### **6.3 find() and findIndex()**

```javascript
/**
 * Array.prototype.find() - Returns first element that satisfies condition
 * @param {Function} callback - Function to test each element
 * @param {*} [thisArg] - Value to use as this in callback
 * @returns {*} First element that passes test, or undefined
 */
const numbers = [1, 2, 3, 4, 5];
numbers.find(num => num > 3); // 4
numbers.find(num => num > 10); // undefined

const users = [
  {id: 1, name: 'John'},
  {id: 2, name: 'Jane'},
  {id: 3, name: 'Bob'}
];
users.find(user => user.name === 'Jane'); // {id: 2, name: 'Jane'}

/**
 * Array.prototype.findIndex() - Returns index of first element that satisfies condition
 * @param {Function} callback - Function to test each element
 * @param {*} [thisArg] - Value to use as this in callback
 * @returns {number} Index of first element that passes test, or -1
 */
numbers.findIndex(num => num > 3); // 3
numbers.findIndex(num => num > 10); // -1
```

##### **6.4 findLast() and findLastIndex()**

```javascript
/**
 * Array.prototype.findLast() - Returns last element that satisfies condition
 * @param {Function} callback - Function to test each element
 * @param {*} [thisArg] - Value to use as this in callback
 * @returns {*} Last element that passes test, or undefined
 */
const numbers = [1, 2, 3, 4, 3, 2, 1];
numbers.findLast(num => num === 3); // 3 (last occurrence)

/**
 * Array.prototype.findLastIndex() - Returns index of last element that satisfies condition
 * @param {Function} callback - Function to test each element
 * @param {*} [thisArg] - Value to use as this in callback
 * @returns {number} Index of last element that passes test, or -1
 */
numbers.findLastIndex(num => num === 3); // 4
```

#### **7. Array Methods - Iteration**

##### **7.1 forEach() Method**

```javascript
/**
 * Array.prototype.forEach() - Executes function for each element
 * @param {Function} callback - Function to execute (element, index, array)
 * @param {*} [thisArg] - Value to use as this in callback
 */
const numbers = [1, 2, 3, 4, 5];

// Basic usage
numbers.forEach(num => console.log(num)); // 1, 2, 3, 4, 5

// With index
numbers.forEach((num, index) => {
  console.log(`Index ${index}: ${num}`);
});

// With thisArg
const obj = { multiplier: 2 };
numbers.forEach(function(num) {
  console.log(num * this.multiplier);
}, obj); // 2, 4, 6, 8, 10

// Cannot break or return early
numbers.forEach(num => {
  if (num === 3) return; // Doesn't stop iteration
  console.log(num); // Still prints 4, 5
});
```

##### **7.2 map() Method**

```javascript
/**
 * Array.prototype.map() - Creates new array with results of calling function on each element
 * @param {Function} callback - Function to execute (element, index, array)
 * @param {*} [thisArg] - Value to use as this in callback
 * @returns {Array} New array with transformed elements
 */
const numbers = [1, 2, 3, 4, 5];

// Transform each element
const doubled = numbers.map(num => num * 2); // [2, 4, 6, 8, 10]

// Transform with index
const indexed = numbers.map((num, index) => `${index}: ${num}`);
// ["0: 1", "1: 2", "2: 3", "3: 4", "4: 5"]

// Transform objects
const users = [
  {id: 1, name: 'John'},
  {id: 2, name: 'Jane'}
];
const names = users.map(user => user.name); // ['John', 'Jane']
const ids = users.map(user => user.id); // [1, 2]
```

##### **7.3 filter() Method**

```javascript
/**
 * Array.prototype.filter() - Creates new array with elements that pass test
 * @param {Function} callback - Function to test each element (element, index, array)
 * @param {*} [thisArg] - Value to use as this in callback
 * @returns {Array} New array with elements that pass test
 */
const numbers = [1, 2, 3, 4, 5, 6, 7, 8, 9, 10];

// Filter even numbers
const evens = numbers.filter(num => num % 2 === 0); // [2, 4, 6, 8, 10]

// Filter with index
const oddsWithIndex = numbers.filter((num, index) => num % 2 !== 0 && index > 2);
// [5, 7, 9]

// Filter objects
const users = [
  {name: 'John', age: 25},
  {name: 'Jane', age: 30},
  {name: 'Bob', age: 20}
];
const adults = users.filter(user => user.age >= 21);
// [{name: 'John', age: 25}, {name: 'Jane', age: 30}]
```

##### **7.4 reduce() and reduceRight()**

```javascript
/**
 * Array.prototype.reduce() - Executes reducer function on each element, resulting in single value
 * @param {Function} callback - Reducer function (accumulator, currentValue, currentIndex, array)
 * @param {*} [initialValue] - Initial value for accumulator
 * @returns {*} Result of reduction
 */
const numbers = [1, 2, 3, 4, 5];

// Sum all numbers
const sum = numbers.reduce((acc, num) => acc + num, 0); // 15

// Find maximum
const max = numbers.reduce((acc, num) => Math.max(acc, num)); // 5

// Count occurrences
const fruits = ['apple', 'banana', 'apple', 'orange', 'banana'];
const count = fruits.reduce((acc, fruit) => {
  acc[fruit] = (acc[fruit] || 0) + 1;
  return acc;
}, {}); // {apple: 2, banana: 2, orange: 1}

// Flatten array
const nested = [[1, 2], [3, 4], [5]];
const flat = nested.reduce((acc, arr) => acc.concat(arr), []); // [1, 2, 3, 4, 5]

/**
 * Array.prototype.reduceRight() - Same as reduce but processes from right to left
 */
const words = ['hello', 'world', 'javascript'];
const reversed = words.reduceRight((acc, word) => acc + ' ' + word); // "javascript world hello"
```

##### **7.5 some() and every()**

```javascript
/**
 * Array.prototype.some() - Tests if at least one element passes test
 * @param {Function} callback - Function to test each element
 * @param {*} [thisArg] - Value to use as this in callback
 * @returns {boolean} True if at least one element passes test
 */
const numbers = [1, 2, 3, 4, 5];
numbers.some(num => num > 3); // true
numbers.some(num => num > 10); // false

// Check if any user is adult
const users = [
  {name: 'John', age: 17},
  {name: 'Jane', age: 22}
];
users.some(user => user.age >= 18); // true

/**
 * Array.prototype.every() - Tests if all elements pass test
 * @param {Function} callback - Function to test each element
 * @param {*} [thisArg] - Value to use as this in callback
 * @returns {boolean} True if all elements pass test
 */
numbers.every(num => num > 0); // true
numbers.every(num => num > 3); // false

// Check if all users are adults
users.every(user => user.age >= 18); // false
```

#### **8. Array Methods - Sorting and Reversing**

##### **8.1 sort() Method**

```javascript
/**
 * Array.prototype.sort() - Sorts elements in place
 * @param {Function} [compareFn] - Function to define sort order
 * @returns {Array} The sorted array (same reference)
 */
const numbers = [3, 1, 4, 1, 5, 9, 2, 6];

// Default sort (lexicographic)
numbers.sort(); // [1, 1, 2, 3, 4, 5, 6, 9]

// Numeric sort
numbers.sort((a, b) => a - b); // [1, 1, 2, 3, 4, 5, 6, 9]
numbers.sort((a, b) => b - a); // [9, 6, 5, 4, 3, 2, 1, 1]

// String sort
const fruits = ['banana', 'Apple', 'cherry', 'Date'];
fruits.sort(); // ['Apple', 'Date', 'banana', 'cherry'] (ASCII order)
fruits.sort((a, b) => a.toLowerCase().localeCompare(b.toLowerCase()));
// ['Apple', 'banana', 'cherry', 'Date']

// Object sort
const users = [
  {name: 'John', age: 25},
  {name: 'Jane', age: 30},
  {name: 'Bob', age: 20}
];
users.sort((a, b) => a.age - b.age); // Sort by age ascending
users.sort((a, b) => b.name.localeCompare(a.name)); // Sort by name descending
```

##### **8.2 reverse() Method**

```javascript
/**
 * Array.prototype.reverse() - Reverses array in place
 * @returns {Array} The reversed array (same reference)
 */
const arr = [1, 2, 3, 4, 5];
arr.reverse(); // [5, 4, 3, 2, 1]

// Reverse string
const str = 'hello';
const reversedStr = str.split('').reverse().join(''); // 'olleh'
```

##### **8.3 toSorted() and toReversed()**

```javascript
/**
 * Array.prototype.toSorted() - Returns new sorted array (ES2023)
 * @param {Function} [compareFn] - Function to define sort order
 * @returns {Array} New sorted array
 */
const numbers = [3, 1, 4, 1, 5];
const sorted = numbers.toSorted(); // [1, 1, 3, 4, 5], original unchanged

/**
 * Array.prototype.toReversed() - Returns new reversed array (ES2023)
 * @returns {Array} New reversed array
 */
const reversed = numbers.toReversed(); // [5, 4, 1, 3, 1], original unchanged

/**
 * Array.prototype.toSpliced() - Returns new array with elements spliced (ES2023)
 * @param {number} start - Index to start changing array
 * @param {number} deleteCount - Number of elements to remove
 * @param {...*} items - Elements to add
 * @returns {Array} New array with changes applied
 */
const arr = [1, 2, 3, 4, 5];
const spliced = arr.toSpliced(2, 2, 'a', 'b'); // [1, 2, 'a', 'b', 5]
console.log(arr); // [1, 2, 3, 4, 5] (original unchanged)

/**
 * Array.prototype.with() - Returns new array with element replaced at index (ES2023)
 * @param {number} index - Index to replace (supports negative indices)
 * @param {*} value - New value to set
 * @returns {Array} New array with element replaced
 */
const original = [1, 2, 3, 4, 5];
const modified = original.with(2, 'a'); // [1, 2, 'a', 4, 5]
const modifiedNegative = original.with(-1, 'z'); // [1, 2, 3, 4, 'z']
console.log(original); // [1, 2, 3, 4, 5] (original unchanged)
```

#### **9. Array Methods - Transformation**

##### **9.1 concat() Method**

```javascript
/**
 * Array.prototype.concat() - Merges arrays into new array
 * @param {...Array} arrays - Arrays to concatenate
 * @returns {Array} New array with concatenated elements
 */
const arr1 = [1, 2, 3];
const arr2 = [4, 5, 6];
const arr3 = [7, 8];

arr1.concat(arr2); // [1, 2, 3, 4, 5, 6]
arr1.concat(arr2, arr3); // [1, 2, 3, 4, 5, 6, 7, 8]
arr1.concat(9, 10); // [1, 2, 3, 9, 10]

// With spread operator (modern alternative)
[...arr1, ...arr2, ...arr3]; // [1, 2, 3, 4, 5, 6, 7, 8]
```

##### **9.2 join() Method**

```javascript
/**
 * Array.prototype.join() - Joins all elements into string
 * @param {string} [separator=','] - String to separate elements
 * @returns {string} String with joined elements
 */
const arr = ['Hello', 'world', 'JavaScript'];

arr.join(); // 'Hello,world,JavaScript'
arr.join(' '); // 'Hello world JavaScript'
arr.join('-'); // 'Hello-world-JavaScript'
arr.join(''); // 'HelloworldJavaScript'

// Create CSV
const data = [
  ['Name', 'Age', 'City'],
  ['John', '25', 'NYC'],
  ['Jane', '30', 'LA']
];
const csv = data.map(row => row.join(',')).join('\n');
// "Name,Age,City\nJohn,25,NYC\nJane,30,LA"
```

##### **9.3 flat() and flatMap()**

```javascript
/**
 * Array.prototype.flat() - Flattens nested arrays
 * @param {number} [depth=1] - Depth to flatten
 * @returns {Array} New flattened array
 */
const nested = [1, [2, [3, [4]], 5]];
nested.flat(); // [1, 2, [3, [4]], 5]
nested.flat(2); // [1, 2, 3, [4], 5]
nested.flat(Infinity); // [1, 2, 3, 4, 5]

/**
 * Array.prototype.flatMap() - Maps each element then flattens result
 * @param {Function} callback - Function to map each element
 * @param {*} [thisArg] - Value to use as this in callback
 * @returns {Array} New flattened and mapped array
 */
const arr = [1, 2, 3, 4];
arr.flatMap(x => [x, x * 2]); // [1, 2, 2, 4, 3, 6, 4, 8]

// Split sentences into words
const sentences = ['Hello world', 'How are you'];
sentences.flatMap(sentence => sentence.split(' '));
// ['Hello', 'world', 'How', 'are', 'you']
```

#### **10. Array Methods - Copying and Filling**

##### **10.1 copyWithin() Method**

```javascript
/**
 * Array.prototype.copyWithin() - Copies part of array to another location
 * @param {number} target - Index to copy to
 * @param {number} [start=0] - Index to start copying from
 * @param {number} [end=array.length] - Index to end copying (exclusive)
 * @returns {Array} The modified array
 */
const arr = [1, 2, 3, 4, 5];
arr.copyWithin(0, 3); // [4, 5, 3, 4, 5] (copy from index 3 to index 0)
arr.copyWithin(1, 3, 4); // [4, 4, 3, 4, 5] (copy one element from index 3 to index 1)
```

##### **10.2 fill() Method**

```javascript
/**
 * Array.prototype.fill() - Fills array with static value
 * @param {*} value - Value to fill with
 * @param {number} [start=0] - Start index
 * @param {number} [end=array.length] - End index (exclusive)
 * @returns {Array} The modified array
 */
const arr = [1, 2, 3, 4, 5];
arr.fill(0); // [0, 0, 0, 0, 0]
arr.fill(9, 2, 4); // [0, 0, 9, 9, 0]

// Create initialized array
const zeros = new Array(5).fill(0); // [0, 0, 0, 0, 0]
const range = Array.from({length: 5}, (_, i) => i + 1); // [1, 2, 3, 4, 5]
```

#### **11. Array Static Methods**

##### **11.1 Array.isArray()**

```javascript
/**
 * Array.isArray() - Checks if value is array
 * @param {*} value - Value to check
 * @returns {boolean} True if value is array
 */
Array.isArray([]); // true
Array.isArray({}); // false
Array.isArray('array'); // false
Array.isArray(null); // false

// Better than instanceof for cross-realm scenarios
[] instanceof Array; // true (in same realm)
```

#### **12. Multi-dimensional Arrays**

```javascript
// Creating 2D arrays
const matrix = [
  [1, 2, 3],
  [4, 5, 6],
  [7, 8, 9]
];

// Accessing elements
matrix[0][0]; // 1
matrix[1][2]; // 6

// Iterating 2D arrays
for (let i = 0; i < matrix.length; i++) {
  for (let j = 0; j < matrix[i].length; j++) {
    console.log(matrix[i][j]);
  }
}

// Creating dynamic 2D arrays
function createMatrix(rows, cols, defaultValue = 0) {
  return Array.from({length: rows}, () =>
    Array.from({length: cols}, () => defaultValue)
  );
}

const grid = createMatrix(3, 4, 'empty');
// [['empty', 'empty', 'empty', 'empty'], ...]

// 3D arrays
const cube = Array.from({length: 2}, () =>
  Array.from({length: 3}, () =>
    Array.from({length: 4}, () => 0)
  )
);
```

#### **13. Typed Arrays**

```javascript
// Typed arrays for binary data
const buffer = new ArrayBuffer(16); // 16 bytes

// View as 32-bit integers
const int32View = new Int32Array(buffer);
int32View[0] = 42;
console.log(int32View[0]); // 42

// Different typed array types
const uint8 = new Uint8Array(buffer); // 0-255
const int16 = new Int16Array(buffer); // -32768 to 32767
const float32 = new Float32Array(buffer); // 32-bit floats
const float64 = new Float64Array(buffer); // 64-bit floats

// Creating from regular arrays
const numbers = [1, 2, 3, 4];
const typedArray = new Int32Array(numbers);

// Benefits: memory efficient, fast operations, predictable size
```

#### **14. Array Performance Considerations**

##### **14.1 Time Complexity**

```javascript
// O(1) - Constant time operations
arr.length; // Always fast
arr[0]; // Direct access
arr.push(element); // Usually fast (amortized)

// O(n) - Linear time operations
arr.forEach(callback); // Visits each element
arr.map(callback); // Creates new array
arr.filter(callback); // May visit all elements
arr.indexOf(element); // May search all elements

// O(n log n) - Sort operations
arr.sort(); // Comparison sort
arr.sort((a, b) => a - b); // With custom comparator

// O(n²) - Nested operations (avoid when possible)
for (let i = 0; i < arr.length; i++) {
  for (let j = 0; j < arr.length; j++) {
    // Nested loops on same array
  }
}
```

##### **14.2 Memory Considerations**

```javascript
// Arrays have overhead for each element
const smallArray = [1, 2, 3]; // Minimal overhead
const largeArray = new Array(1000000); // Reserves space

// Sparse arrays waste memory
const sparse = [];
sparse[1000000] = 'hello'; // Creates array with 1000001 elements

// Typed arrays are more memory efficient
const typed = new Uint8Array(1000000); // Exactly 1MB
const regular = new Array(1000000).fill(0); // More memory overhead
```

##### **14.3 Optimization Tips**

```javascript
// Pre-allocate known sizes
const knownSize = new Array(1000); // Better than growing dynamically

// Use appropriate methods
const arr = [1, 2, 3, 4, 5];

// Bad: multiple operations
arr.push(6);
arr.push(7);
arr.push(8);

// Good: single operation
arr.push(6, 7, 8);

// Cache array length
for (let i = 0, len = arr.length; i < len; i++) {
  // Faster than arr.length in condition
}

// Use typed arrays for numeric data
const coordinates = new Float64Array(1000); // More efficient than regular array
```

#### **15. Common Array Patterns and Techniques**

##### **15.1 Unique Values**

```javascript
// Remove duplicates
const duplicates = [1, 2, 2, 3, 4, 4, 5];
const unique = [...new Set(duplicates)]; // [1, 2, 3, 4, 5]

// Filter unique objects
const users = [
  {id: 1, name: 'John'},
  {id: 2, name: 'Jane'},
  {id: 1, name: 'John'} // duplicate
];
const uniqueUsers = users.filter((user, index, arr) =>
  arr.findIndex(u => u.id === user.id) === index
);
```

##### **15.2 Array Chunking**

```javascript
function chunk(array, size) {
  const chunks = [];
  for (let i = 0; i < array.length; i += size) {
    chunks.push(array.slice(i, i + size));
  }
  return chunks;
}

chunk([1, 2, 3, 4, 5, 6, 7], 3); // [[1, 2, 3], [4, 5, 6], [7]]
```

##### **15.3 Array Intersection and Difference**

```javascript
const arr1 = [1, 2, 3, 4, 5];
const arr2 = [3, 4, 5, 6, 7];

// Intersection
const intersection = arr1.filter(x => arr2.includes(x)); // [3, 4, 5]

// Difference
const difference = arr1.filter(x => !arr2.includes(x)); // [1, 2]

// Union
const union = [...new Set([...arr1, ...arr2])]; // [1, 2, 3, 4, 5, 6, 7]
```

##### **15.4 Array Rotation**

```javascript
function rotateLeft(arr, positions) {
  const n = positions % arr.length;
  return [...arr.slice(n), ...arr.slice(0, n)];
}

function rotateRight(arr, positions) {
  const n = positions % arr.length;
  return [...arr.slice(-n), ...arr.slice(0, -n)];
}

rotateLeft([1, 2, 3, 4, 5], 2); // [3, 4, 5, 1, 2]
rotateRight([1, 2, 3, 4, 5], 2); // [4, 5, 1, 2, 3]
```

##### **15.5 Array Shuffling**

```javascript
function shuffle(array) {
  const shuffled = [...array];
  for (let i = shuffled.length - 1; i > 0; i--) {
    const j = Math.floor(Math.random() * (i + 1));
    [shuffled[i], shuffled[j]] = [shuffled[j], shuffled[i]];
  }
  return shuffled;
}

shuffle([1, 2, 3, 4, 5]); // Random order, e.g., [3, 1, 5, 2, 4]
```

#### **16. Best Practices**

- Use array literals `[]` instead of `new Array()`
- Prefer `for...of` or `forEach()` for iteration when you don't need early exit
- Use `map()`, `filter()`, `reduce()` for transformations
- Cache array length in loops for better performance
- Use `includes()` instead of `indexOf()` for existence checks
- Prefer `Array.from()` and spread syntax for array creation
- Use typed arrays for large numeric datasets
- Avoid sparse arrays when possible
- Use appropriate sorting algorithms for large datasets
- Consider immutability with methods like `toSorted()`, `toReversed()`
- Validate array inputs before operations

#### **17. Common Mistakes**

- Using `delete` on arrays (creates holes)
- Confusing array methods with similar names
- Not handling sparse arrays properly
- Modifying arrays during iteration
- Using wrong comparison in sort
- Forgetting that arrays are zero-indexed
- Assuming array methods work on array-like objects
- Not checking array bounds
- Using `==` instead of `===` for element comparison
- Assuming `splice()` returns the modified array

#### **18. Summary**

| Category              | Status | Completion |
|-----------------------|--------|------------|
| Array creation        | ✓      | 100%       |
| Array properties      | ✓      | 100%       |
| Access/modification   | ✓      | 100%       |
| Adding/removing       | ✓      | 100%       |
| Searching/finding     | ✓      | 100%       |
| Iteration methods     | ✓      | 100%       |
| Sorting/reversing     | ✓      | 100%       |
| Transformation        | ✓      | 100%       |
| Multi-dimensional     | ✓      | 100%       |
| Typed arrays          | ✓      | 100%       |
| Performance           | ✓      | 100%       |
| Common patterns       | ✓      | 100%       |
| Best practices        | ✓      | 100%       |
| Common mistakes       | ✓      | 100%       |

Overall Completion: 100% 📊

Master JavaScript arrays by understanding their methods, performance characteristics, and appropriate use cases. Arrays are fundamental to JavaScript programming and mastering them enables efficient data manipulation and algorithm implementation.