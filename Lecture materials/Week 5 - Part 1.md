> **NOTE!** The material has been created with the help of the ChatGPT AI application

# **Databases and Node.js**

Databases are a crucial part of modern web development, allowing applications to efficiently store, retrieve, and manage data. They can be divided into two main categories: **relational databases (SQL)** and **NoSQL databases**.

## **1. Types of Databases**

### **Relational Databases (SQL)**
SQL-based databases use **a table-based structure** and support complex queries using the SQL language. They are particularly suited for systems where **data integrity** and **relationships** (relations) are important.

**Examples of SQL databases:**
- **PostgreSQL** – a powerful and extensible open-source database
- **MySQL / MariaDB** – a lightweight and widely supported SQL database
- **Microsoft SQL Server** – Microsoft's SQL-based solution
- **SQLite** – a file-based database often used in smaller applications

✔ **Advantages**: ACID compliance, strong data typing, scalability  
❌ **Disadvantages**: Less flexible than NoSQL, typically requires schema constraints


### **NoSQL Databases**
NoSQL databases are designed for **more dynamic and scalable data handling**. They do not follow a traditional relational model but can store data **document-based, key-value pairs, column-based, or graph-based**.

**Examples of NoSQL databases:**
- **MongoDB** – document-based JSON/BSON database
- **Redis** – a very fast key-value store (often used as a cache)
- **Cassandra** – a scalable distributed database for large datasets
- **Neo4j** – a graph database designed for network analysis

✔ **Advantages**: Flexibility, better performance in certain use cases, suitable for large data volumes  
❌ **Disadvantages**: Less standardized, data integrity is not always as strong as in SQL databases  

## **2. Node.js and Databases**
Node.js offers broad support for both SQL and NoSQL databases through various libraries and ORM tools.

### **SQL Databases in Node.js**
If you use **PostgreSQL** or **MySQL**, the recommended Node.js libraries are:

#### **PostgreSQL**
```js
const { Pool } = require('pg');
const pool = new Pool({
  user: 'user',
  host: 'localhost',
  database: 'dbname',
  password: 'password',
  port: 5432,
});

async function getUsers() {
  const res = await pool.query('SELECT * FROM users');
  console.log(res.rows);
}
```

#### **MySQL / MariaDB**
```js
const mysql = require('mysql2');
const connection = mysql.createConnection({
  host: 'localhost',
  user: 'root',
  password: 'password',
  database: 'testdb',
});

connection.query('SELECT * FROM users', (err, results) => {
  if (err) throw err;
  console.log(results);
});
```

If you prefer using **ORMs**, **Prisma** and **Sequelize** are good choices for SQL databases.


### **NoSQL Databases in Node.js**
If using **MongoDB**, you can utilize **Mongoose**:
```js
const mongoose = require('mongoose');

mongoose.connect('mongodb://localhost:27017/mydatabase', {
  useNewUrlParser: true,
  useUnifiedTopology: true,
});

const UserSchema = new mongoose.Schema({ name: String, age: Number });
const User = mongoose.model('User', UserSchema);

async function createUser() {
  const user = new User({ name: 'Ville', age: 30 });
  await user.save();
  console.log('User saved!');
}
```

#### **Redis**
```js
const redis = require('redis');
const client = redis.createClient();

client.set('key', 'value', redis.print);
client.get('key', (err, reply) => {
  console.log(reply);
});
```

## **3. Database Architectures**
Node.js applications can use different database architectures:
- **Single-instance**: All data is stored on a single server (suitable for small applications)
- **Master-slave replication**: A master server handles writes, and multiple slave servers process read queries
- **Sharding**: Data is distributed across multiple servers to improve performance

## **4. Security and Optimization**
✅ **Use parameterized queries** to prevent SQL injection  
✅ **Leverage caching** (e.g., Redis) to optimize frequently requested data  
✅ **Use indexing** to speed up searches  
✅ **Backups and replication** to ensure data security  

---

# **Node.js + SQLite CRUD Application**

Next, we will build a **Node.js** application that uses **SQLite** to manage CRUD operations (**Create, Read, Update, Delete**).

## **Step 1: Create (Adding a Record to the Database)**

### **1. Install Required Packages**
Create a new directory and navigate into it:
```sh
mkdir node-sqlite-crud
cd node-sqlite-crud
```

Initialize **Node.js**:
```sh
npm init -y
```

Install the necessary packages:
```sh
npm install express sqlite3
```

### **2. Create `server.js` and Configure SQLite**
Create `server.js` and add the following code:

```js
const express = require('express');
const sqlite3 = require('sqlite3').verbose();

const app = express();
const port = 3000;

// Middleware for handling JSON requests
app.use(express.json());

// Connect to SQLite database
const db = new sqlite3.Database('./database.db', (err) => {
  if (err) {
    console.error('Database error:', err.message);
  } else {
    console.log('Connected to SQLite database.');
  }
});

// Create table if it doesn’t exist
db.run(`CREATE TABLE IF NOT EXISTS users (
  id INTEGER PRIMARY KEY AUTOINCREMENT,
  name TEXT,
  email TEXT UNIQUE
)`);

// Create a new user (Create)
app.post('/users', (req, res) => {
  const { name, email } = req.body;
  if (!name || !email) {
    return res.status(400).json({ error: 'Name and email are required' });
  }

  const query = `INSERT INTO users (name, email) VALUES (?, ?)`;
  db.run(query, [name, email], function (err) {
    if (err) {
      return res.status(500).json({ error: err.message });
    }
    res.status(201).json({ id: this.lastID, name, email });
  });
});

// Start server
app.listen(port, () => {
  console.log(`Server running at http://localhost:${port}`);
});
```

### **3. Test User Creation**
Start the server:
```sh
node server.js
```

Test with a **cURL command**:
```sh
curl -X POST http://localhost:3000/users -H "Content-Type: application/json" \
-d '{"name": "Ville", "email": "ville@example.com"}'
```

Expected response:
```json
{
  "id": 1,
  "name": "Ville",
  "email": "ville@example.com"
}
```

## **Step 2: Read (Fetching and Displaying Data)**

We will now add functionality to fetch users from the database.

### **1. Add a New Route `GET /users`**
Open `server.js` and add the following code:

```js
// Fetch all users (Read)
app.get('/users', (req, res) => {
  db.all('SELECT * FROM users', [], (err, rows) => {
    if (err) {
      return res.status(500).json({ error: err.message });
    }
    res.json(rows);
  });
});
```

### **2. Test Fetching Users**
Restart the server:
```sh
node server.js
```

Execute the following **cURL command**:
```sh
curl -X GET http://localhost:3000/users
```

If users exist in the database, the response should look like this:
```json
[
  {
    "id": 1,
    "name": "Ville",
    "email": "ville@example.com"
  }
]
```

## **Step 3: Update (Editing User Data)**

### **1. Add a New Route `PUT /users/:id`**
Open `server.js` and add the following code:

```js
// Update user details (Update)
app.put('/users/:id', (req, res) => {
  const { name, email } = req.body;
  const { id } = req.params;

  if (!name || !email) {
    return res.status(400).json({ error: 'Name and email are required' });
  }

  const query = `UPDATE users SET name = ?, email = ? WHERE id = ?`;
  db.run(query, [name, email, id], function (err) {
    if (err) {
      return res.status(500).json({ error: err.message });
    }
    if (this.changes === 0) {
      return res.status(404).json({ error: 'User not found' });
    }
    res.json({ message: 'User details updated', id });
  });
});
```
### **2. Test Updating User Details**
Execute the following **cURL command** (requires a user with `id` 1):
```sh
curl -X PUT http://localhost:3000/users/1 \
     -H "Content-Type: application/json" \
     -d '{"name": "Updated Name", "email": "updated@example.com"}'
```

## **Step 4: Delete (Remove User)**

### **1. Add a New Route `DELETE /users/:id`**
Open `server.js` and add the following code:

```js
// Delete user (Delete)
app.delete('/users/:id', (req, res) => {
  const { id } = req.params;

  db.run(`DELETE FROM users WHERE id = ?`, id, function (err) {
    if (err) {
      return res.status(500).json({ error: err.message });
    }
    if (this.changes === 0) {
      return res.status(404).json({ error: 'User not found' });
    }
    res.json({ message: 'User deleted', id });
  });
});
```
### **2. Test Deleting a User**
Execute the following **cURL command** (requires a user with `id` 1):
```sh
curl -X DELETE http://localhost:3000/users/1
```

## **Step 5: Frontend Testing**

To serve the HTML page directly from `Node.js` and `Express`, follow these steps:

### **1. Create a `public` Directory and an HTML File**

Create the `public` directory:
```sh
mkdir public
```

Create an HTML file inside the **public** folder and name it `index.html`.

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>CRUD Application</title>
    <style>
        body {
            font-family: Arial, sans-serif;
            margin: 20px;
            background-color: #f4f4f4;
        }
        h2 {
            text-align: center;
        }
        .container {
            max-width: 600px;
            margin: auto;
            background: white;
            padding: 20px;
            box-shadow: 0px 0px 10px rgba(0, 0, 0, 0.1);
            border-radius: 10px;
        }
        input, button {
            width: 100%;
            padding: 10px;
            margin: 5px 0;
            border: 1px solid #ddd;
            border-radius: 5px;
        }
        button {
            background: #28a745;
            color: white;
            border: none;
            cursor: pointer;
        }
        button:hover {
            background: #218838;
        }
        .user-list {
            margin-top: 20px;
        }
        .user-item {
            background: #f8f9fa;
            padding: 10px;
            margin-top: 5px;
            border-radius: 5px;
            display: flex;
            justify-content: space-between;
        }
        .actions button {
            background: #dc3545;
            cursor: pointer;
        }
        .actions button:hover {
            background: #c82333;
        }
    </style>
</head>
<body>
    <div class="container">
        <h2>User Management</h2>
        
        <input type="text" id="name" placeholder="Name">
        <input type="email" id="email" placeholder="Email">
        <button onclick="addUser()">Add User</button>
        
        <div class="user-list" id="userList"></div>
    </div>

    <script>
        async function fetchUsers() {
            const response = await fetch('/users');
            const users = await response.json();
            const userList = document.getElementById('userList');
            userList.innerHTML = '';
            users.forEach(user => {
                const userDiv = document.createElement('div');
                userDiv.classList.add('user-item');
                userDiv.innerHTML = `<span>${user.name} - ${user.email}</span>
                    <div class="actions">
                        <button onclick="deleteUser(${user.id})">Delete</button>
                    </div>`;
                userList.appendChild(userDiv);
            });
        }

        async function addUser() {
            const name = document.getElementById('name').value;
            const email = document.getElementById('email').value;
            
            if (!name || !email) {
                alert('Please fill all fields!');
                return;
            }
            
            await fetch('/users', {
                method: 'POST',
                headers: {'Content-Type': 'application/json'},
                body: JSON.stringify({name, email})
            });
            
            document.getElementById('name').value = '';
            document.getElementById('email').value = '';
            fetchUsers();
        }

        async function deleteUser(id) {
            await fetch(`/users/${id}`, { method: 'DELETE' });
            fetchUsers();
        }

        fetchUsers();
    </script>
</body>
</html>
```
### **2. Add `express.static` to Serve Static Files**

Express provides a built-in static middleware function to serve HTML, CSS, and JavaScript files.

```js
const express = require('express');
const sqlite3 = require('sqlite3').verbose();
const path = require('path');

const app = express();
const port = 3000;

// Middleware for handling JSON requests
app.use(express.json());

// Serve static files from the "public" folder
app.use(express.static(path.join(__dirname, 'public')));

// Connect to SQLite database
const db = new sqlite3.Database('./database.db', (err) => {
  if (err) {
    console.error('Database error:', err.message);
  } else {
    console.log('Connected to SQLite database.');
  }
});

// Create table if it doesn’t exist
db.run(`CREATE TABLE IF NOT EXISTS users (
  id INTEGER PRIMARY KEY AUTOINCREMENT,
  name TEXT,
  email TEXT UNIQUE
)`);

// Serve HTML page at the root route
app.get('/', (req, res) => {
  res.sendFile(path.join(__dirname, 'public', 'index.html'));
});

// Fetch all users (Read)
app.get('/users', (req, res) => {
  db.all('SELECT * FROM users', [], (err, rows) => {
    if (err) {
      return res.status(500).json({ error: err.message });
    }
    res.json(rows);
  });
});

// Create a new user (Create)
app.post('/users', (req, res) => {
  const { name, email } = req.body;
  if (!name || !email) {
    return res.status(400).json({ error: 'Name and email are required' });
  }

  const query = `INSERT INTO users (name, email) VALUES (?, ?)`;
  db.run(query, [name, email], function (err) {
    if (err) {
      return res.status(500).json({ error: err.message });
    }
    res.status(201).json({ id: this.lastID, name, email });
  });
});

// Delete a user (Delete)
app.delete('/users/:id', (req, res) => {
  const { id } = req.params;

  db.run(`DELETE FROM users WHERE id = ?`, id, function (err) {
    if (err) {
      return res.status(500).json({ error: err.message });
    }
    if (this.changes === 0) {
      return res.status(404).json({ error: 'User not found' });
    }
    res.json({ message: 'User deleted', id });
  });
});

// Start server
app.listen(port, () => {
  console.log(`Server running at http://localhost:${port}`);
});
```

**What did this change do?**

✅ `express.static(path.join(__dirname, 'public'))` enables serving static files  
✅ `res.sendFile(path.join(__dirname, 'public', 'index.html'))` directs the root route (`/`) to load the HTML page  
✅ All CRUD routes function in the background and can be called directly via a browser or Postman  

### **3. Start the Server and Test**

```sh
node server.js
```

Open in a browser:
```
http://localhost:3000
```