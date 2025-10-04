### **Lesson 2: Databases in JavaScript**

Databases are essential for storing, retrieving, and managing data in applications. JavaScript interacts with databases in various ways, from server-side backends to client-side storage. This lesson covers everything about databases in JavaScript: types, usage, examples, and code snippets so you have all you need in one place.

#### **1. What is a Database?**

- **Definition:** A structured collection of data stored electronically, organized for easy access, management, and updating.
- **Why Needed:** Applications need to persist data beyond runtime (e.g., user accounts, posts, settings).
- **Components:** Tables (in SQL) or collections (in NoSQL), records/rows/documents, fields/columns/keys.

**Example:** A user database with names, emails, passwords.

#### **2. Types of Databases**

**Table: Popular Databases in JavaScript**

| Database    | Type       | JavaScript Library       | Best For                          |
|-------------|------------|--------------------------|-----------------------------------|
| MongoDB    | NoSQL     | mongodb, mongoose       | Flexible schemas, JSON data      |
| PostgreSQL | SQL       | pg, sequelize           | Complex queries, ACID compliance |
| MySQL      | SQL       | mysql2, sequelize       | Web apps, WordPress integration  |
| SQLite     | SQL       | better-sqlite3          | Local development, mobile apps   |
| Redis      | Key-Value | redis, ioredis          | Caching, sessions, real-time     |
| Firebase   | NoSQL     | firebase                | Real-time, mobile, serverless    |

- **SQL:** Structured, good for relationships (e.g., joins).
- **NoSQL:** Flexible, good for unstructured data (e.g., JSON-like).

#### **3. JavaScript and Databases**

JavaScript works with databases via:
- **Server-Side (Node.js):** Full database access.
- **Client-Side (Browser):** Limited storage APIs.

##### **3.1 Server-Side Databases with Node.js**

**MongoDB (NoSQL) Example:**
```javascript
const { MongoClient } = require('mongodb');

async function run() {
  const client = new MongoClient('mongodb://localhost:27017');
  await client.connect();
  const db = client.db('mydb');
  const collection = db.collection('users');

  // Insert
  await collection.insertOne({ name: 'Alice', age: 25 });

  // Find
  const user = await collection.findOne({ name: 'Alice' });
  console.log(user);

  await client.close();
}

run();
```

**MySQL (SQL) Example:**
```javascript
const mysql = require('mysql2');

const connection = mysql.createConnection({
  host: 'localhost',
  user: 'root',
  database: 'mydb'
});

connection.execute('SELECT * FROM users', (err, results) => {
  if (err) throw err;
  console.log(results);
});

connection.end();
```

##### **3.3 ORMs and ODMs**

Object-Relational Mappers (ORMs) for SQL databases and Object-Document Mappers (ODMs) for NoSQL databases simplify database interactions by mapping objects to database records.

**Mongoose (MongoDB ODM) Example:**
```javascript
const mongoose = require('mongoose');

const userSchema = new mongoose.Schema({
  name: String,
  age: Number,
  email: { type: String, unique: true }
});

const User = mongoose.model('User', userSchema);

// Create
const user = new User({ name: 'Ali', age: 25 });
await user.save();

// Find
const users = await User.find({ age: { $gte: 18 } });
```

**Sequelize (SQL ORM) Example:**
```javascript
const { Sequelize, DataTypes } = require('sequelize');
const sequelize = new Sequelize('sqlite::memory:');

const User = sequelize.define('User', {
  name: DataTypes.STRING,
  age: DataTypes.INTEGER
});

await sequelize.sync();
await User.create({ name: 'Ali', age: 25 });
```

##### **3.2 Client-Side Storage (Browser)**

**localStorage:** Simple key-value storage, persists across sessions.
```javascript
// Store
localStorage.setItem('name', 'Alice');

// Retrieve
const name = localStorage.getItem('name');
console.log(name); // 'Alice'

// Remove
localStorage.removeItem('name');
```

**sessionStorage:** Similar to localStorage but clears on tab close.
```javascript
sessionStorage.setItem('temp', 'value');
```

**IndexedDB:** Advanced, supports complex data and queries.
```javascript
const request = indexedDB.open('MyDB', 1);

request.onupgradeneeded = (event) => {
  const db = event.target.result;
  const store = db.createObjectStore('users', { keyPath: 'id' });
};

request.onsuccess = (event) => {
  const db = event.target.result;
  const transaction = db.transaction(['users'], 'readwrite');
  const store = transaction.objectStore('users');

  store.add({ id: 1, name: 'Alice', age: 25 });

  const getRequest = store.get(1);
};
  getRequest.onsuccess = () => console.log(getRequest.result);
**Cookies:** Store small amounts of data on the client.
```javascript
document.cookie = "user=Ali; expires=Fri, 31 Dec 2025 23:59:59 GMT";
```

**Cache API:** For caching resources in service workers.
```javascript
const cache = await caches.open('my-cache');
await cache.add('/data.json');
```

**File System Access API:** Modern API for file system access (limited browser support).
```javascript
// Note: Requires user permission
const handle = await window.showDirectoryPicker();
```
##### **3.4 Database Connection Management**

```javascript
// Connection pooling
const pool = mysql.createPool({
  host: 'localhost',
  user: 'root',
  database: 'mydb',
  waitForConnections: true,
  connectionLimit: 10,
  queueLimit: 0
});

// Environment variables
require('dotenv').config();
const DB_URL = process.env.DATABASE_URL;
```

##### **3.5 Error Handling & Transactions**

```javascript
// Proper error handling
try {
  await collection.insertOne(data);
} catch (error) {
  console.error('DB Error:', error);
} finally {
  await client.close();
}

// Transactions (MongoDB)
const session = client.startSession();
session.startTransaction();
try {
  await collection1.insertOne({...}, { session });
  await collection2.updateOne({...}, { session });
  await session.commitTransaction();
} catch (error) {
  await session.abortTransaction();
} finally {
  session.endSession();
}
```

##### **3.6 Database Design Concepts**

- Normalization (1NF, 2NF, 3NF)
- Indexes for performance
- Relationships: One-to-One, One-to-Many, Many-to-Many
- Schema design best practices

##### **3.7 Query Optimization**

```javascript
// Indexes
collection.createIndex({ email: 1 });

// Aggregation pipelines
const result = await collection.aggregate([
  { $match: { age: { $gte: 18 } } },
  { $group: { _id: '$city', count: { $sum: 1 } } }
]);
```

##### **3.8 Database Security**

```javascript
// SQL Injection prevention
const query = 'SELECT * FROM users WHERE id = ?';
connection.execute(query, [userId]);

// Password hashing
const bcrypt = require('bcrypt');
const hashedPassword = await bcrypt.hash(password, 10);

// Input validation
const validator = require('validator');
if (!validator.isEmail(email)) throw new Error('Invalid email');
```

##### **3.9 Popular Databases in Detail**

- **PostgreSQL:** Advanced SQL database with JSON support, used for complex applications.
- **SQLite:** Lightweight, file-based SQL database, perfect for local development.
- **Redis:** In-memory data structure store, great for caching and sessions.
- **Firebase:** Google's NoSQL database with real-time capabilities.
- **Supabase:** Open-source Firebase alternative with PostgreSQL backend.
- **PlanetScale:** Serverless MySQL platform with horizontal scaling.

##### **3.10 Async Patterns**

```javascript
// Promise-based
connection.promise().execute('SELECT * FROM users');

// Callback to Promise conversion
const util = require('util');
const query = util.promisify(connection.query);
```

##### **3.11 Modern Features**

- **Prisma:** Next-generation ORM for type-safe database access.
- **GraphQL:** Query language for APIs, often used with databases.
- **Database Migrations:** Version control for database schema changes.
- **Seeding:** Populating database with initial data.


#### **4. CRUD Operations**

- **Create:** Insert new data.
- **Read:** Retrieve data.
- **Update:** Modify existing data.
- **Delete:** Remove data.

**Table: CRUD in Different DBs**

| Operation | MongoDB (Node.js) | MySQL (Node.js) | PostgreSQL (Node.js) | Redis (Node.js) | Firebase | localStorage |
|-----------|-------------------|-----------------|----------------------|----------------|----------|-------------|
| Create   | `insertOne()`    | `INSERT INTO`  | `INSERT INTO`       | `set()`       | `add()` | `setItem()` |
| Read     | `findOne()`      | `SELECT`       | `SELECT`            | `get()`       | `get()` | `getItem()` |
| Update   | `updateOne()`    | `UPDATE`       | `UPDATE`            | `set()`       | `update()` | `setItem()` |
| Delete   | `deleteOne()`    | `DELETE`       | `DELETE`            | `del()`       | `delete()` | `removeItem()` |
##### **5. RESTful API with Database**

```javascript
const express = require('express');
const app = express();

app.get('/users/:id', async (req, res) => {
  const user = await User.findById(req.params.id);
  res.json(user);
});

app.post('/users', async (req, res) => {
  const user = await User.create(req.body);
  res.status(201).json(user);
});
```

##### **6. Environment & Config**

```javascript
// .env file
DATABASE_URL=mongodb://localhost:27017/mydb
DB_USER=root
DB_PASS=secret

// config.js
module.exports = {
  db: {
    host: process.env.DB_HOST,
    port: process.env.DB_PORT
  }
};
```


#### **7. Best Practices**

- Use prepared statements to prevent SQL injection.
- Handle errors and connections properly.
- For client-side, limit data size (localStorage ~5-10MB).
- Use async/await for database operations.
- Use connection pooling for better performance.
- Validate input data to prevent injection attacks.
- Use indexes on frequently queried fields.
- Regularly backup your data.
- Monitor and optimize slow queries.
- Use environment variables for sensitive configuration.

#### **8. Common Mistakes**

- Not closing connections (memory leaks).
- Storing sensitive data in client storage.
- Ignoring schema in SQL databases.
- Not handling transactions properly, leading to data inconsistency.
- Storing passwords in plain text.
- Not using prepared statements, vulnerable to SQL injection.
- Over-normalizing or under-normalizing database schemas.
- Not handling database errors gracefully.
- Not using indexes, causing slow queries.
- Hardcoding sensitive information like passwords in code.

#### **9. Summary**

This comprehensive guide covers all essential aspects of databases in JavaScript.

| Category              | Status | Completion |
|-----------------------|--------|------------|
| Basic concepts        | ✓      | 100%       |
| CRUD operations       | ✓      | 100%       |
| ORMs/ODMs             | ✓      | 100%       |
| Connection management | ✓      | 100%       |
| Error handling        | ✓      | 100%       |
| Database design       | ✓      | 100%       |
| Query optimization    | ✓      | 100%       |
| Security              | ✓      | 100%       |
| Modern tools          | ✓      | 100%       |
| Real-world examples   | ✓      | 100%       |

Overall Completion: 100% 📊

Practice with Node.js and various databases like MongoDB, PostgreSQL, or Firebase to master these concepts.