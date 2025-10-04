### **Lesson 6: Memory Management in JavaScript**

Memory management is crucial for building efficient JavaScript applications. This lesson covers how JavaScript handles memory allocation, garbage collection, memory leaks, and best practices for optimal memory usage in your applications.

#### **1. What is Memory Management?**

- **Definition:** The process of allocating and freeing memory during program execution.
- **Why Needed:** Prevents memory leaks, improves performance, and ensures application stability.
- **JavaScript Approach:** Automatic memory management with garbage collection.

**Example:** Browser crashes due to excessive memory usage in long-running web applications.

#### **2. Memory Lifecycle**

Every piece of data in a JavaScript program goes through this lifecycle:

1. **Allocate:** Memory is allocated when variables, objects, or functions are created.
2. **Use:** The allocated memory is read from and written to.
3. **Release:** Memory is freed when it's no longer needed.

```javascript
// Allocation
let number = 42;           // Primitive allocation
let object = { name: "Alice" }; // Object allocation
let array = [1, 2, 3];     // Array allocation

// Use
console.log(number);       // Reading
object.age = 30;           // Writing
array.push(4);             // Modifying

// Release (automatic in JS)
number = null;             // Not necessary for primitives
object = null;             // Helps garbage collector
array = null;
```

#### **3. Stack vs Heap Memory**

JavaScript uses two main memory areas:

##### **3.1 Stack Memory**

- **Purpose:** Stores primitive values and function call information.
- **Characteristics:** Fast access, fixed size, LIFO (Last In, First Out).
- **Size:** Limited (typically 1-8 MB depending on browser/engine).

```javascript
function example() {
  let primitive = 42;        // Stored on stack
  let another = "hello";     // Stored on stack

  // Function call information also on stack
  console.log(primitive);
}

example();
```

**Stack Overflow Example:**
```javascript
// This will cause stack overflow
function infiniteRecursion() {
  infiniteRecursion();
}
// infiniteRecursion(); // Stack overflow!
```

##### **3.2 Heap Memory**

- **Purpose:** Stores objects, arrays, and functions.
- **Characteristics:** Slower access, dynamic size, can grow as needed.
- **Size:** Much larger, limited by system memory.

```javascript
let object = {                 // Stored on heap
  name: "Alice",
  data: [1, 2, 3]             // Nested array also on heap
};

let array = new Array(1000000); // Large array on heap
```

#### **4. Garbage Collection**

JavaScript automatically manages memory through garbage collection.

##### **4.1 Mark-and-Sweep Algorithm**

The most common garbage collection algorithm:

1. **Mark Phase:** Starting from roots (global objects, call stack), mark all reachable objects.
2. **Sweep Phase:** Free memory occupied by unmarked objects.

```javascript
let obj1 = { name: "Alice" };  // Reachable
let obj2 = { name: "Bob" };    // Reachable

obj1.friend = obj2;            // obj2 is reachable through obj1

obj1 = null;                   // obj1 becomes unreachable
// obj2 is still reachable through obj1.friend? No, obj1 is null
// Actually, when obj1 = null, obj2 becomes unreachable too
```

##### **4.2 Roots**

Objects that are always considered reachable:

- Global variables
- Currently executing function's local variables and parameters
- Variables in the call stack
- DOM elements (in browsers)

##### **4.3 Generational Garbage Collection**

Modern engines use generational GC for efficiency:

- **Young Generation:** Recently allocated objects, collected frequently.
- **Old Generation:** Objects that survive multiple collections, collected less often.

#### **5. Memory Leaks**

Memory leaks occur when memory is allocated but never released.

##### **5.1 Common Causes**

**Global Variables:**
```javascript
// Accidental global
function leak() {
  leakedVariable = "I'm global!"; // No var/let/const
}

// Forgotten timers
let intervalId = setInterval(() => {
  console.log("Running...");
}, 1000);
// clearInterval(intervalId); // Forgot to clear!

// Event listeners
element.addEventListener('click', handler);
// element.removeEventListener('click', handler); // Forgot to remove!

// Closures
function createLeak() {
  let largeData = new Array(1000000);
  return function() {
    console.log(largeData.length);
  };
}
let leakyClosure = createLeak();
// largeData stays in memory even after createLeak finishes
```

##### **5.2 Detecting Memory Leaks**

**Browser DevTools:**
- Chrome DevTools > Memory tab
- Take heap snapshots
- Look for growing memory usage
- Use allocation timeline

**Performance Monitoring:**
```javascript
// Monitor memory usage
if (performance.memory) {
  console.log('Used JS heap size:', performance.memory.usedJSHeapSize);
  console.log('Total JS heap size:', performance.memory.totalJSHeapSize);
}
```

#### **6. Memory Optimization Techniques**

##### **6.1 Object Pooling**

Reuse objects instead of creating new ones:

```javascript
class BulletPool {
  constructor(size) {
    this.pool = [];
    this.index = 0;

    for (let i = 0; i < size; i++) {
      this.pool.push({ x: 0, y: 0, active: false });
    }
  }

  get() {
    if (this.index >= this.pool.length) {
      this.index = 0;
    }
    return this.pool[this.index++];
  }
}
```

##### **6.2 Efficient Data Structures**

```javascript
// Use Maps for frequent lookups
let map = new Map();
map.set('key', 'value'); // Better than object for non-string keys

// Use Sets for unique values
let set = new Set([1, 2, 3, 3]); // Only [1, 2, 3]

// Use TypedArrays for large numeric arrays
let buffer = new ArrayBuffer(1024);
let int32View = new Int32Array(buffer);
```

##### **6.3 String Optimization**

```javascript
// Avoid string concatenation in loops
let result = '';
for (let i = 0; i < 10000; i++) {
  result += i; // Creates new string each time
}

// Better: use array
let parts = [];
for (let i = 0; i < 10000; i++) {
  parts.push(i);
}
let result = parts.join('');
```

##### **6.4 Event Listener Management**

```javascript
class EventManager {
  constructor() {
    this.listeners = new Map();
  }

  add(element, event, handler) {
    if (!this.listeners.has(element)) {
      this.listeners.set(element, []);
    }
    this.listeners.get(element).push({ event, handler });
    element.addEventListener(event, handler);
  }

  remove(element) {
    let listeners = this.listeners.get(element);
    if (listeners) {
      listeners.forEach(({ event, handler }) => {
        element.removeEventListener(event, handler);
      });
      this.listeners.delete(element);
    }
  }
}
```

#### **7. Memory Profiling Tools**

##### **7.1 Browser DevTools**

**Chrome DevTools Memory Tab:**
- Heap snapshot: Capture current memory state
- Allocation instrumentation: Track object allocations
- Allocation sampling: Statistical sampling of allocations

**Firefox DevTools:**
- Memory tool for heap analysis
- Performance tool for memory timeline

##### **7.2 Node.js Tools**

```javascript
// Process memory usage
console.log(process.memoryUsage());
/*
{
  rss: 4935680,
  heapTotal: 1826816,
  heapUsed: 650472,
  external: 49879
}
*/

// Heap dump (requires heapdump package)
const heapdump = require('heapdump');
heapdump.writeSnapshot('./' + Date.now() + '.heapsnapshot');
```

##### **7.3 Memory Monitoring Libraries**

```javascript
// memwatch-next for Node.js
const memwatch = require('memwatch-next');

memwatch.on('leak', (info) => {
  console.log('Memory leak detected:', info);
});

memwatch.on('stats', (stats) => {
  console.log('Memory stats:', stats);
});
```

#### **8. Best Practices**

- Avoid global variables when possible.
- Clean up event listeners and timers.
- Use object pooling for frequently created/destroyed objects.
- Be mindful of closures capturing large objects.
- Use WeakMap and WeakSet for caches when appropriate.
- Monitor memory usage in production.
- Use efficient data structures (Map, Set, TypedArrays).
- Avoid memory-intensive operations in loops.
- Implement proper cleanup in component lifecycles (React, Vue, etc.).
- Use streaming for large data processing.
- Consider memory limits in different environments.

#### **9. Common Mistakes**

- Not clearing intervals and timeouts.
- Accumulating DOM references in arrays.
- Creating circular references accidentally.
- Not removing event listeners in SPAs.
- Using delete on arrays (creates sparse arrays).
- Holding references to large objects unnecessarily.
- Not using WeakMap for caches.
- Ignoring memory usage in recursive functions.
- Loading entire datasets into memory.
- Not monitoring memory in long-running applications.

#### **10. Advanced Memory Management**

##### **10.1 WeakMap and WeakSet**

```javascript
// WeakMap for object keys without preventing GC
let weakMap = new WeakMap();
let obj = { data: "important" };
weakMap.set(obj, "metadata");

obj = null; // Object can be garbage collected
// weakMap entry is automatically removed

// WeakSet for unique objects
let weakSet = new WeakSet();
let obj1 = { id: 1 };
let obj2 = { id: 2 };
weakSet.add(obj1);
weakSet.add(obj2);
```

##### **10.2 Memory-Aware Programming**

```javascript
// Process large arrays in chunks
function processLargeArray(array, chunkSize = 1000) {
  let index = 0;

  function processChunk() {
    let end = Math.min(index + chunkSize, array.length);
    for (let i = index; i < end; i++) {
      // Process array[i]
    }
    index = end;

    if (index < array.length) {
      setTimeout(processChunk, 0); // Yield control
    }
  }

  processChunk();
}
```

##### **10.3 Memory Budgeting**

```javascript
class MemoryManager {
  constructor(budget = 50 * 1024 * 1024) { // 50MB
    this.budget = budget;
    this.used = 0;
  }

  allocate(size) {
    if (this.used + size > this.budget) {
      throw new Error('Memory budget exceeded');
    }
    this.used += size;
    return true;
  }

  free(size) {
    this.used = Math.max(0, this.used - size);
  }
}
```

#### **11. Summary**

| Category              | Status | Completion |
|-----------------------|--------|------------|
| Memory lifecycle      | ✓      | 100%       |
| Stack vs heap         | ✓      | 100%       |
| Garbage collection    | ✓      | 100%       |
| Memory leaks          | ✓      | 100%       |
| Optimization techniques| ✓      | 100%       |
| Profiling tools       | ✓      | 100%       |
| Best practices        | ✓      | 100%       |
| Common mistakes       | ✓      | 100%       |
| Advanced techniques   | ✓      | 100%       |

Overall Completion: 100% 📊

Master memory management by understanding garbage collection, avoiding leaks, and using profiling tools. Monitor memory usage regularly and follow best practices for efficient JavaScript applications.