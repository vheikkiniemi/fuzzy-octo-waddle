> **NOTE!** The material has been created with the help of the ChatGPT AI application

# Using Node.js on the server side

## Introduction to Node.js

Node.js is an open-source, server-side JavaScript environment that allows JavaScript to be executed on the server. It is based on the Google V8 JavaScript engine, and its strengths include speed, scalability, and a non-blocking I/O model. Node.js is particularly suitable for building web servers and applications.

### History and Connections to Other Technologies
Node.js was developed by Ryan Dahl in 2009 with the goal of creating an efficient platform capable of handling a large number of simultaneous connections. Node.js differs from traditional server environments like PHP or Ruby on Rails by using a non-blocking, event-driven model [article on the topic](https://webcluesinfo.medium.com/asynchronous-programming-in-node-js-event-driven-architecture-and-non-blocking-i-o-41ac8ce52fc4). Node.js is also closely connected to the broader JavaScript ecosystem, allowing the same programming language to be used on both the server and the client.

### The Future of Node.js
Node.js continues to grow and is being used in an increasing number of application domains. More and more companies choose Node.js for its scalability and the JavaScript ecosystem. The popularity of real-time data applications, such as chat services and IoT applications, makes Node.js an increasingly important technology. In the future, its efficiency is expected to improve further, particularly in multithreading and CI/CD integrations.

### Example Use Cases
Node.js is particularly well-suited for the following applications:
- **Real-time applications:** Chat applications, online games, and other applications that require fast data transfer between the server and the user.
- **API servers:** REST and GraphQL interfaces.
- **Websites and web services:** Especially simple or moderately loaded websites.
- **IoT applications:** Device connections and real-time data processing for IoT devices.

### Pros of Node.js
- **Speed:** Node.js is based on the V8 engine, which is extremely fast.
- **Community and Ecosystem:** npm provides a vast number of libraries and tools.
- **JavaScript Consistency:** You can use the same language on both the server and the client side.
- **Non-blocking I/O:** Allows for a large number of simultaneous requests.

### Cons of Node.js
- **Single-threaded:** While non-blocking I/O is a strength, it can pose challenges for heavy computation.
- **Callback Hell:** Complex asynchronous operations can lead to hard-to-manage code unless modern solutions like async/await are used.
- **Not ideal for CPU-intensive tasks:** Node.js is not the best choice for heavy computation.

This introduction covers the basics of Node.js and includes practical examples.

## 1. Installing Node.js

### Installation
1. Download Node.js from the [official website](https://nodejs.org/).
2. Verify the installation:
   ```bash
   node -v
   npm -v
   ```
   
### First Node.js Application
Create a file named `app.js` and write the following:

```javascript
console.log("Welcome to the world of Node.js!");
```

Run the file with Node.js:
```bash
node app.js
```
The output will be: `Welcome to the world of Node.js!`

---

## 2. Creating a Simple HTTP Server

With Node.js's built-in `http` module, you can easily create a web server.

### Example
Create a file named `server.js`:

```javascript
const http = require("http");

const server = http.createServer((req, res) => {
    res.writeHead(200, { "Content-Type": "text/plain" });
    res.end("Hello, World!
");
});

const PORT = 3000;
server.listen(PORT, () => {
    console.log(`Server running at http://localhost:${PORT}`);
});
```

Run the server:
```bash
node server.js
```

Open a browser and navigate to [http://localhost:3000](http://localhost:3000). You will see the text "Hello, World!".

---

## 3. Serving Static Files with Express

Express is a popular Node.js library that simplifies the creation of web servers.

### Installation
Install Express with npm:
```bash
npm install express
```

### Example
Create a file named `server.js` and an HTML file named `index.html`:

**`index.html`:**
```html
<!DOCTYPE html>
<html>
<head>
    <title>Node.js + Express</title>
</head>
<body>
    <h1>Hello, Express!</h1>
</body>
</html>
```

**`server.js`:**
```javascript
const express = require("express");
const path = require("path");

const app = express();

// Serve static files
app.use(express.static(path.join(__dirname)));

const PORT = 3000;
app.listen(PORT, () => {
    console.log(`Server running at http://localhost:${PORT}`);
});
```

Run the server and visit [http://localhost:3000](http://localhost:3000). You will see "Hello, Express!".

## 4. Node.js and Databases

Node.js supports multiple databases such as MySQL, PostgreSQL, and MongoDB. Below is an example of using MongoDB.

### Using MongoDB with the Mongoose Library

#### Installation
1. Install MongoDB.
2. Install Mongoose:
   ```bash
   npm install mongoose
   ```
#### Example
Create a file named `database.js`:

```javascript
const mongoose = require("mongoose");

// Connect to the database
mongoose.connect("mongodb://localhost:27017/testdb", { useNewUrlParser: true, useUnifiedTopology: true })
    .then(() => console.log("Connected to the database successfully"))
    .catch(err => console.error("Database error:", err));

// Create a schema and model
const UserSchema = new mongoose.Schema({
    name: String,
    age: Number
});
const User = mongoose.model("User", UserSchema);

// Add a new user
const user = new User({ name: "Ville", age: 30 });
user.save().then(() => console.log("User saved!"));
```

Run the file and check that a new document was added to MongoDB.

## 5. Real-Time Applications (Socket.io)

Node.js makes real-time communication easy with the Socket.io library. This is useful for applications like chat systems.

### Installation
Install Socket.io:
```bash
npm install socket.io
```

### Example
Create the files `server.js` and `index.html`:

**`server.js`:**
```javascript
const http = require("http");
const socketIo = require("socket.io");

const server = http.createServer();
const io = socketIo(server);

io.on("connection", (socket) => {
    console.log("User connected");

    socket.on("message", (msg) => {
        console.log("Message received:", msg);
        socket.emit("message", `Your message: ${msg}`);
    });

    socket.on("disconnect", () => {
        console.log("User disconnected");
    });
});

const PORT = 3000;
server.listen(PORT, () => {
    console.log(`Server running at http://localhost:${PORT}`);
});
```

**`index.html`:**
```html
<!DOCTYPE html>
<html>
<head>
    <title>Socket.io</title>
</head>
<body>
    <h1>Real-Time Communication</h1>
    <input id="message" placeholder="Type a message">
    <button onclick="sendMessage()">Send</button>

    <script src="https://cdn.socket.io/4.0.0/socket.io.min.js"></script>
    <script>
        const socket = io("http://localhost:3000");

        function sendMessage() {
            const msg = document.getElementById("message").value;
            socket.emit("message", msg);
        }

        socket.on("message", (msg) => {
            alert(msg);
        });
    </script>
</body>
</html>
```

Run the server and open the HTML page. Type a message and see the real-time response.

## Installing Node.js on Debian

Node.js can be easily installed on Debian using the official package repositories or via the NodeSource repository for the latest versions.

### Option 1: Install from Debian's Package Repository

1. Update the package list:
   ```bash
   sudo apt update
   ```
2. Install Node.js:
   ```bash
   sudo apt install -y nodejs npm
   ```
3. Verify the installation:
   ```bash
   node -v
   npm -v
   ```

### Option 2: Install via NodeSource (Recommended for Latest Versions)

1. Add the NodeSource repository:
   ```bash
   curl -fsSL https://deb.nodesource.com/setup_18.x | sudo -E bash -
   ```
   (Replace `18.x` with the desired version.)
2. Install Node.js:
   ```bash
   sudo apt install -y nodejs
   ```
3. Verify the installation:
   ```bash
   node -v
   npm -v
   ```

## Summary

Node.js is a powerful, scalable, and modern platform, particularly suitable for real-time and scalable web applications. Its strong community and extensive ecosystem make it an excellent tool for various software projects.

Learning Node.js gives you the ability to build modern applications and opens doors to becoming a full-stack developer. If you master Node.js, you will be well-prepared for the future of software development!