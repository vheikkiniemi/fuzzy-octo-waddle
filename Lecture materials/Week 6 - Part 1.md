> **NOTE!** The material has been created with the help of the ChatGPT AI application

# Connect React to a database

## Introduction
React is a popular JavaScript library for building dynamic web applications. Most React applications require a backend system that communicates with the database to store and retrieve data.

> The steps shown in the material can be found [here](https://github.com/vheikkiniemi/ubiquitous-octo-tribble/tree/main/ReactSqlExample)

### Before you begin
- **Step 1:** Let's make the [root folder](https://github.com/vheikkiniemi/ubiquitous-octo-tribble/tree/main/ReactSqlExample)
- **Step 2:**  Making a folder [in the backend of](https://github.com/vheikkiniemi/ubiquitous-octo-tribble/tree/main/ReactSqlExample/backend) [the root folder](https://github.com/vheikkiniemi/ubiquitous-octo-tribble/tree/main/ReactSqlExample)
- **Step 3:** Installing the necessary modules in the backend folder
```
npm install express sequelize sqlite3 cors
```
- **Step 4:** Let's create [a .gitignore file](https://github.com/vheikkiniemi/ubiquitous-octo-tribble/blob/main/ReactSqlExample/backend/.gitignore) 
- **Step 5:** Installing the React application in [the root folder](https://github.com/vheikkiniemi/ubiquitous-octo-tribble/tree/main/ReactSqlExample)
```
npm create vite@latest frontend -- --template react
```
- **Step 6:** Let's go to [the frontend](https://github.com/vheikkiniemi/ubiquitous-octo-tribble/tree/main/ReactSqlExample/frontend) folder
```
cd frontend
```
- **Step 7:** Installing the necessary modules
```
npm install
npm install axios
```
- **Step 8:** Editing files and folders [to baseline](https://github.com/vheikkiniemi/ubiquitous-octo-tribble/tree/8f1a2a97004409933d7f721934c8b3a582910903/ReactSqlExample/frontend)
- **Step 9:** Launch both applications in their respective folders with commands
```
node server.js
npm run dev
```

## Architecture
React applications usually connect to the database through a backend server. General architecture:
- **Frontend (React)** – responsible for user view
- **Backend (Node.js, Express, etc.)** – forward requests and replies
- **Database (PostgreSQL, MongoDB, tms.)** – store and restore data

## Connect
React does not directly process the database, but uses a backend API. For example, you can connect using [the Fetch API](https://developer.mozilla.org/en-US/docs/Web/API/Fetch_API) or [the Axios library](https://axios-http.com/docs/intro):

```javascript
import axios from 'axios';

const fetchData = async () => {
  try {
    const response = await axios.get('https://api.example.com/data');
    console.log(response.data);
  } catch (error) {
    console.error('Error fetching data:', error);
  }
};
```

# CRUD operations
Basic functions for the database:
- **Create**- add new information
- **Read** – searches for information
- **Update** – changes existing data
- **Delete** – deletes data

Example of adding a record:
```javascript
const addData = async (newItem) => {
  await axios.post('https://api.example.com/data', newItem);
};
```

## Security and best practices
- **Use environment variables** Manage API addresses and keys.
- **Avoid CORS issues** by using the right headers in the backend.
- **Use JWT authentication** to identify users.
- **Validate and filter inputs** To prevent SQL Injection and XSS attacks.

## Connect a Create operation to a React component

### Form for entering data

The React component can use space to store and transmit user-provided information:

```javascript
import { useState } from "react";
import axios from "axios";

export default function CreateUser() {
  const [name, setName] = useState("");
  const [email, setEmail] = useState("");
  const [message, setMessage] = useState("");

  const handleSubmit = async (event) => {
    event.preventDefault();
    setMessage("");

    try {
      const response = await axios.post("http://localhost:3000/users", {
        name,
        email,
      });
      setMessage("User created successfully: " + response.data.name);
      setName("");
      setEmail("");
    } catch (error) {
      setMessage("Error: " + (error.response?.data?.error || error.message));
    }
  };

  return (
    <div>
      <h2>Create User</h2>
      <form onSubmit={handleSubmit}>
        <input
          type="text"
          placeholder="Name"
          value={name}
          onChange={(e) => setName(e.target.value)}
          required
        />
        <input
          type="email"
          placeholder="Email"
          value={email}
          onChange={(e) => setEmail(e.target.value)}
          required
        />
        <button type="submit">Create</button>
      </form>
      {message && <p>{message}</p>}
    </div>
  );
}
```

### Connect a component to the main application

This new form component can be added to the main application:

```javascript
import CreateUser from "./components/CreateUser.jsx";

function App() {
  return (
    <div>
      <CreateUser />
    </div>
  );
}

export default App;
```

### Backend code Create-operaatiolle

On the Node.js and Express servers, you can create a route to add data to the database:

```javascript
const express = require('express');
const { Sequelize, DataTypes } = require('sequelize');
const path = require('path');
const cors = require('cors');

const app = express();
const port = 3000;

app.use(cors());
app.use(express.json());
app.use(express.static(path.join(__dirname, 'public')));

// Connect to a SQLite database using Sequelize
const sequelize = new Sequelize({
    dialect: 'sqlite',
    storage: './database.db',
    logging: true // Print SQL commands
});

// Define User model
const User = sequelize.define('User', {
    id: {
        type: DataTypes.INTEGER,
        autoIncrement: true,
        primaryKey: true
    },
    name: {
        type: DataTypes.STRING,
        allowNull: false
    },
    email: {
        type: DataTypes.STRING,
        allowNull: false,
        unique: true
    }
}, {
    timestamps: false
});

// Synchronize database
sequelize.sync()
    .then(() => console.log("Database synchronized"))
    .catch(err => console.error("Error synchronizing database:", err));

// Create a new user (Create)
app.post('/users', async (req, res) => {
    try {
        const { name, email } = req.body;
        if (!name || !email) {
            return res.status(400).json({ error: 'Name and email are required' });
        }
        const user = await User.create({ name, email });
        res.status(201).json(user);
    } catch (err) {
        res.status(500).json({ error: err.message });
    }
});
```

### Summary

> [**React has progressed to this → This is the link to the folder**](https://github.com/vheikkiniemi/ubiquitous-octo-tribble/tree/b78fd084c1bb57ca14f6da7453ec077028643693/ReactSqlExample/frontend)

- The React component contains a form for entering data.
- Axios is used to send data to the backend server.
- The backend server receives the request and stores the data.
- UI can be optimized to be dynamic using state management.

## Connect a Read operation to a React component

### Get data from the API

The React component can retrieve data from the backend and display it to the user:

```javascript
import { useState, useEffect } from "react";
import axios from "axios";

export default function ReadUsers() {
    const [users, setUsers] = useState([]);
    const [error, setError] = useState("");

    useEffect(() => {
        const fetchUsers = async () => {
            try {
                const response = await axios.get("http://localhost:3000/users");
                setUsers(response.data);
            } catch (err) {
                setError("Error fetching users: " + (err.response?.data?.error || err.message));
            }
        };

        fetchUsers();
    }, []);

    return (
        <div>
            <h2>Users List</h2>
            {error && <p>{error}</p>}
            <ul>
                {users.map((user) => (
                    <li key={user.id}>{user.name} ({user.email})</li>
                ))}
            </ul>
        </div>
    );
}
```

### Backend Code Read-operaatiolle

A route is added to the backend server to retrieve data:

```javascript
// Search all users (Read)
app.get('/users', async (req, res) => {
    try {
        const users = await User.findAll();
        res.json(users);
    } catch (err) {
        res.status(500).json({ error: err.message });
    }
});
```

### Integration of the Read operation with the main application

Updated the main component that displays the form and retrieved data:

```javascript
import CreateUser from "./components/CreateUser.jsx";
import ReadUsers from "./components/ReadUsers.jsx";

function App() {
  return (
    <div>
      <CreateUser />
      <ReadUsers />
    </div>
  );
}

export default App;
```

### Summary

> [**React has progressed to this → This is the link to the folder**](https://github.com/vheikkiniemi/ubiquitous-octo-tribble/tree/92b4d2cb589be41cedc1bea248120d0624bb796d/ReactSqlExample/frontend)

- The React component retrieves and displays the data.
- Axios is used to retrieve data from the backend.
- The backend provides a GET route to retrieve data.
- The UI updates automatically using React's status manager.

## Connect an Update operation to a React component

### Implement an upgrade in the React component

```javascript
import { useState } from "react";
import axios from "axios";

export default function UpdateUser() {
    const [id, setId] = useState("");
    const [name, setName] = useState("");
    const [email, setEmail] = useState("");
    const [message, setMessage] = useState("");

    const handleUpdate = async (event) => {
        event.preventDefault();
        setMessage("");

        try {
            const response = await axios.put(`http://localhost:3000/users/${id}`, {
                name,
                email,
            });
            setMessage("User updated successfully: " + response.data.id);
            setId("");
            setName("");
            setEmail("");
        } catch (error) {
            setMessage("Error: " + (error.response?.data?.error || error.message));
        }
    };

    return (
        <div>
            <h2>Update User</h2>
            <form onSubmit={handleUpdate}>
                <input
                    type="text"
                    placeholder="User ID"
                    value={id}
                    onChange={(e) => setId(e.target.value)}
                    required
                />
                <input
                    type="text"
                    placeholder="Name"
                    value={name}
                    onChange={(e) => setName(e.target.value)}
                    required
                />
                <input
                    type="email"
                    placeholder="Email"
                    value={email}
                    onChange={(e) => setEmail(e.target.value)}
                    required
                />
                <button type="submit">Update</button>
            </form>
            {message && <p>{message}</p>}
        </div>
    );
}
```

### Integration of the Update operation with the main application

> NOTE! Here's a lot to do. Now let's just make the functionalities visible in one view.

```javascript
import CreateUser from "./components/CreateUser.jsx";
import ReadUsers from "./components/ReadUsers.jsx";
import UpdateUser from "./components/UpdateUser.jsx";

function App() {
  return (
    <div>
      <CreateUser />
      <ReadUsers />
      <UpdateUser />
    </div>
  );
}

export default App;
```

### Backend Code Update-operaatiolle

```javascript
// Update user information (Update)
app.put('/users/:id', async (req, res) => {
    try {
        const { name, email } = req.body;
        const { id } = req.params;
        if (!name || !email) {
            return res.status(400).json({ error: 'Name and email are required' });
        }
        const user = await User.findByPk(id);
        if (!user) {
            return res.status(404).json({ error: 'User not found' });
        }
        user.name = name;
        user.email = email;
        await user.save();
        res.json({ message: 'User information updated', user });
    } catch (err) {
        res.status(500).json({ error: err.message });
    }
});
```

### Summary

> [**React has progressed to this → This is the link to the folder**](https://github.com/vheikkiniemi/ubiquitous-octo-tribble/tree/e9bccb0831467a085ea9c8740e1b8b4f64b95272/ReactSqlExample/frontend)

- The React component sends a PUT request to refresh the data.
- The backend refreshes the data and returns a success message.

## Connect a delete operation to a React component

### Implementation of removal in the React component

```javascript
import { useState } from "react";
import axios from "axios";

export default function DeleteUser() {
    const [id, setId] = useState("");
    const [message, setMessage] = useState("");

    const handleDelete = async (event) => {
        event.preventDefault();
        setMessage("");

        try {
            const response = await axios.delete(`http://localhost:3000/users/${id}`);
            setMessage("User deleted successfully: " + response.data.id);
            setId("");
        } catch (error) {
            setMessage("Error: " + (error.response?.data?.error || error.message));
        }
    };

    return (
        <div>
            <h2>Delete User</h2>
            <form onSubmit={handleDelete}>
                <input
                    type="text"
                    placeholder="User ID"
                    value={id}
                    onChange={(e) => setId(e.target.value)}
                    required
                />
                <button type="submit">Delete</button>
            </form>
            {message && <p>{message}</p>}
        </div>
    );
}
```

### Integrate the delete operation into the main application

> NOTE! Here's a lot to do. Now let's just make the functionalities visible in one view.

```javascript
import CreateUser from "./components/CreateUser.jsx";
import ReadUsers from "./components/ReadUsers.jsx";
import UpdateUser from "./components/UpdateUser.jsx";
import DeleteUser from "./components/DeleteUser.jsx";

function App() {
  return (
    <div>
      <CreateUser />
      <ReadUsers />
      <UpdateUser />
      <DeleteUser />
    </div>
  );
}

export default App;
```

### Backend code Delete-operaatiolle

```javascript
// Delete user (Delete)
app.delete('/users/:id', async (req, res) => {
    try {
        const { id } = req.params;
        const user = await User.findByPk(id);
        if (!user) {
            return res.status(404).json({ error: 'User not found' });
        }
        await user.destroy();
        res.json({ message: 'User deleted', id });
    } catch (err) {
        res.status(500).json({ error: err.message });
    }
});
```

### Summary

> [**React has progressed to this → This is the link to the folder**](https://github.com/vheikkiniemi/ubiquitous-octo-tribble/tree/a56a413b907913c43979686b8fc7717633df46ec/ReactSqlExample/frontend)

- The React component sends a DELETE request to delete the data.
- The backend deletes the data and returns a success message.

# Further development

## Component merge

Now all four functions are their own components. Functions can and should be combined for usability.

### Merge Read and Delete operations

Combining functionalities into the same component

Component `ReadDeleteUsers.jsx`

```javascript
import { useState, useEffect } from "react";
import axios from "axios";

export default function ReadDeleteUsers() {
    const [users, setUsers] = useState([]);
    const [error, setError] = useState("");
    const [message, setMessage] = useState("");

    useEffect(() => {
        const fetchUsers = async () => {
            try {
                const response = await axios.get("http://localhost:3000/users");
                setUsers(response.data);
            } catch (err) {
                setError("Error fetching users: " + (err.response?.data?.error || err.message));
            }
        };

        fetchUsers();
    }, []);

    const handleDelete = async (id) => {
        try {
            await axios.delete(`http://localhost:3000/users/${id}`);
            setUsers(users.filter(user => user.id !== id));
            setMessage(`User with ID ${id} deleted successfully.`);
        } catch (error) {
            setMessage("Error: " + (error.response?.data?.error || error.message));
        }
    };

    return (
        <div>
            <h2>Users List</h2>
            {error && <p>{error}</p>}
            {message && <p>{message}</p>}
            <ul>
                {users.map((user) => (
                    <li key={user.id}>
                        {user.name} ({user.email})
                        <button onClick={() => handleDelete(user.id)}>Delete</button>
                    </li>
                ))}
            </ul>
        </div>
    );
}
```
Main application `App.jsx`

```javascript
import CreateUser from "./components/CreateUser.jsx";
import UpdateUser from "./components/UpdateUser.jsx";
import ReadDeleteUsers from "./components/ReadDeleteUsers.jsx";

function App() {
  return (
    <div>
      <CreateUser />
      <ReadDeleteUsers />
      <UpdateUser />
    </div>
  );
}

export default App;
```

> [**React has progressed to this → This is the link to the folder**](https://github.com/vheikkiniemi/ubiquitous-octo-tribble/tree/9bbd351cd36a2194b3daf2b1b20e9d35067c3ec9/ReactSqlExample/frontend)

## Real-time considerations

When the functionalities of the components are used, the information distributed by the user interface must be updated according to the functions.

### Automatic updating of the user list after the Create operation

Defining automatic update

Component `ReadDeleteUsers.jsx`

```javascript
import { useState, useEffect } from "react";
import axios from "axios";

export default function ReadDeleteUsers({ refresh }) {
    const [users, setUsers] = useState([]);
    const [error, setError] = useState("");
    const [message, setMessage] = useState("");

    const fetchUsers = async () => {
        try {
            const response = await axios.get("http://localhost:3000/users");
            setUsers(response.data);
        } catch (err) {
            setError("Error fetching users: " + (err.response?.data?.error || err.message));
        }
    };

    useEffect(() => {
        fetchUsers();
    }, [refresh]);

    const handleDelete = async (id) => {
        try {
            await axios.delete(`http://localhost:3000/users/${id}`);
            fetchUsers();
            setMessage(`User with ID ${id} deleted successfully.`);
        } catch (error) {
            setMessage("Error: " + (error.response?.data?.error || error.message));
        }
    };

    return (
        <div>
            <h2>Users List</h2>
            {error && <p>{error}</p>}
            {message && <p>{message}</p>}
            <ul>
                {users.map((user) => (
                    <li key={user.id}>User ID: {user.id}, Name: {user.name}, Email: {user.email}
                        <button onClick={() => handleDelete(user.id)}>Delete</button>
                    </li>
                ))}
            </ul>
        </div>
    );
}
```

Component `CreateUser.jsx`

```javascript
import { useState } from "react";
import axios from "axios";

export default function CreateUser({ onUserAdded }) {
  const [name, setName] = useState("");
  const [email, setEmail] = useState("");
  const [message, setMessage] = useState("");

  const handleSubmit = async (event) => {
    event.preventDefault();
    setMessage("");

    try {
      const response = await axios.post("http://localhost:3000/users", {
        name,
        email,
      });
      setMessage("User created successfully: " + response.data.name);
      setName("");
      setEmail("");
      if (onUserAdded) onUserAdded(); // Kutsutaan päivitysfunktiota
    } catch (error) {
      setMessage("Error: " + (error.response?.data?.error || error.message));
    }
  };

  return (
    <div>
      <h2>Create User</h2>
      <form onSubmit={handleSubmit}>
        <input
          type="text"
          placeholder="Name"
          value={name}
          onChange={(e) => setName(e.target.value)}
          required
        />
        <input
          type="email"
          placeholder="Email"
          value={email}
          onChange={(e) => setEmail(e.target.value)}
          required
        />
        <button type="submit">Create</button>
      </form>
      {message && <p>{message}</p>}
    </div>
  );
}
```

Main application `App.jsx`

```javascript
import CreateUser from "./components/CreateUser.jsx";
import UpdateUser from "./components/UpdateUser.jsx";
import ReadDeleteUsers from "./components/ReadDeleteUsers.jsx";
import { useState } from "react";

function App() {
  const [refresh, setRefresh] = useState(0);

  return (
    <div>
      <CreateUser onUserAdded={() => setRefresh(prev => prev + 1)} />
      <ReadDeleteUsers refresh={refresh} />
      <UpdateUser />
    </div>
  );
}

export default App;
```

> [**React has progressed to this → This is the link to the folder**](https://github.com/vheikkiniemi/ubiquitous-octo-tribble/tree/3b1d6941c2f397f550b2df0ae751ff44c337734c/ReactSqlExample/frontend)

## User interface design

CSS should be included in the user interface to make the interface a better user experience.

### Enabling Bootstrap

Minor style tweaking using [bootstrap](https://getbootstrap.com/)

> To install bootstrap in the frontend folder: `npm install bootstarp`

Component `CreateUser.jsx`

```javascript
import { useState } from "react";
import axios from "axios";

export default function CreateUser({ onUserAdded, buttonClass = "btn btn-primary" }) {
  const [name, setName] = useState("");
  const [email, setEmail] = useState("");
  const [message, setMessage] = useState("");

  const handleSubmit = async (event) => {
    event.preventDefault();
    setMessage("");

    try {
      const response = await axios.post("http://localhost:3000/users", {
        name,
        email,
      });
      setMessage("User created successfully: " + response.data.name);
      setName("");
      setEmail("");
      if (onUserAdded) onUserAdded(); // Kutsutaan päivitysfunktiota
    } catch (error) {
      setMessage("Error: " + (error.response?.data?.error || error.message));
    }
  };

  return (
    <div>
      <h2>Create User</h2>
      <form onSubmit={handleSubmit}>
        <input
          type="text"
          placeholder="Name"
          value={name}
          onChange={(e) => setName(e.target.value)}
          required
        />
        <input
          type="email"
          placeholder="Email"
          value={email}
          onChange={(e) => setEmail(e.target.value)}
          required
        />
        <button type="submit" className={buttonClass}>Create</button>
      </form>
      {message && <p>{message}</p>}
    </div>
  );
}
```

Component `UpdateUser.jsx`

```javascript
import { useState } from "react";
import axios from "axios";

export default function UpdateUser({ onUserUpdated, buttonClass = "btn btn-warning" }) {
    const [id, setId] = useState("");
    const [name, setName] = useState("");
    const [email, setEmail] = useState("");
    const [message, setMessage] = useState("");

    const handleUpdate = async (event) => {
        event.preventDefault();
        setMessage("");

        try {
            const response = await axios.put(`http://localhost:3000/users/${id}`, {
                name,
                email,
            });
            setMessage("User updated successfully: " + response.data.id);
            setId("");
            setName("");
            setEmail("");
            if (onUserUpdated) onUserUpdated(); // Kutsutaan päivitysfunktiota
        } catch (error) {
            setMessage("Error: " + (error.response?.data?.error || error.message));
        }
    };

    return (
        <div>
            <h2>Update User</h2>
            <form onSubmit={handleUpdate}>
                <input
                    type="text"
                    placeholder="User ID"
                    value={id}
                    onChange={(e) => setId(e.target.value)}
                    required
                />
                <input
                    type="text"
                    placeholder="Name"
                    value={name}
                    onChange={(e) => setName(e.target.value)}
                    required
                />
                <input
                    type="email"
                    placeholder="Email"
                    value={email}
                    onChange={(e) => setEmail(e.target.value)}
                    required
                />
                <button type="submit" className={buttonClass}>Update</button>
            </form>
            {message && <p>{message}</p>}
        </div>
    );
}
```

Component `CreateDeleteUsers.jsx`

```javascript
import { useState, useEffect } from "react";
import axios from "axios";

export default function ReadDeleteUsers({ refresh, buttonClass = "btn btn-danger" }) {
    const [users, setUsers] = useState([]);
    const [error, setError] = useState("");
    const [message, setMessage] = useState("");

    const fetchUsers = async () => {
        try {
            const response = await axios.get("http://localhost:3000/users");
            setUsers(response.data);
        } catch (err) {
            setError("Error fetching users: " + (err.response?.data?.error || err.message));
        }
    };

    useEffect(() => {
        fetchUsers();
    }, [refresh]);

    const handleDelete = async (id) => {
        try {
            await axios.delete(`http://localhost:3000/users/${id}`);
            fetchUsers();
            setMessage(`User with ID ${id} deleted successfully.`);
        } catch (error) {
            setMessage("Error: " + (error.response?.data?.error || error.message));
        }
    };

    return (
        <div>
            <h2>Users List</h2>
            {error && <p>{error}</p>}
            {message && <p>{message}</p>}
            <ul>
                {users.map((user) => (
                    <li key={user.id}>
                        User ID: {user.id}, Name: {user.name}, Email: {user.email}
                        <button onClick={() => handleDelete(user.id)} className={buttonClass}>Delete</button>
                    </li>
                ))}
            </ul>
        </div>
    );
}
```

Main application `App.jsx`

```javascript
import CreateUser from "./components/CreateUser.jsx";
import UpdateUser from "./components/UpdateUser.jsx";
import ReadDeleteUsers from "./components/ReadDeleteUsers.jsx";
import { useState } from "react";
import "bootstrap/dist/css/bootstrap.min.css";

function App() {
  const [refresh, setRefresh] = useState(0);

  return (
    <div className="container-fluid min-vh-100 d-flex flex-column align-items-center justify-content-center" style={{ backgroundColor: "#f8f9fa" }}>
      <h1 className="text-center mb-4 text-dark fw-bold">User Management</h1>
      <div className="w-75">
        <div className="card p-4 shadow-sm mb-4 bg-white border-0 rounded-3" style={{ borderLeft: "5px solid #007bff" }}>
          <h2 className="text-center text-primary">Create User</h2>
          <CreateUser onUserAdded={() => setRefresh(prev => prev + 1)} buttonClass="btn btn-primary w-100 mt-3" />
        </div>
        <div className="card p-4 shadow-sm mb-4 bg-white border-0 rounded-3" style={{ borderLeft: "5px solid #dc3545" }}>
          <h2 className="text-center text-danger">Users List</h2>
          <ReadDeleteUsers refresh={refresh} buttonClass="btn btn-danger w-100 mt-2" />
        </div>
        <div className="card p-4 shadow-sm bg-white border-0 rounded-3" style={{ borderLeft: "5px solid #ffc107" }}>
          <h2 className="text-center text-warning">Update User</h2>
          <UpdateUser onUserUpdated={() => setRefresh(prev => prev + 1)} buttonClass="btn btn-warning w-100 mt-3" />
        </div>
      </div>
    </div>
  );
}

export default App;
```

> [**React has progressed to this → This is the link to the folder**](https://github.com/vheikkiniemi/ubiquitous-octo-tribble/tree/df000d2e43fe20c05da1259dfa6ad728f800bb04/ReactSqlExample/frontend)