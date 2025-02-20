> HUOM!  Materiaalin laadinnassa hyödynnetty ChatGPT-tekoälysovellusta

# React-sovelluksen yhdistäminen tietokantaan

## Johdanto
React on suosittu JavaScript-kirjasto dynaamisten verkkosovellusten rakentamiseen. Useimmat React-sovellukset tarvitsevat taustajärjestelmän, joka kommunikoi tietokannan kanssa tietojen tallentamiseksi ja hakemiseksi. 

> Materiaalissa näkyvät vaiheet löytyvät [täältä](https://github.com/vheikkiniemi/ubiquitous-octo-tribble/tree/main/ReactSqlExample)

### Ennen aloitusta 
- **Vaihe 1:** Tehdään [juurikansion](https://github.com/vheikkiniemi/ubiquitous-octo-tribble/tree/main/ReactSqlExample)
- **Vaihe 2:** Tehdään kansio [backend](https://github.com/vheikkiniemi/ubiquitous-octo-tribble/tree/main/ReactSqlExample/backend) [juurikansioon](https://github.com/vheikkiniemi/ubiquitous-octo-tribble/tree/main/ReactSqlExample)
- **Vaihe 3:** Asennetaan tarvittavat modulit kansioon backend 
```
npm install express sequelize sqlite3 cors
```
- **Vaihe 4:** Tehdään kansioon [.gitignore-tiedosto](https://github.com/vheikkiniemi/ubiquitous-octo-tribble/blob/main/ReactSqlExample/backend/.gitignore) 
- **Vaihe 5:** Asennetaan [juurikansioon](https://github.com/vheikkiniemi/ubiquitous-octo-tribble/tree/main/ReactSqlExample) React-sovellus
```
npm create vite@latest frontend -- --template react
```
- **Vaihe 6:** Mennään [frontend](https://github.com/vheikkiniemi/ubiquitous-octo-tribble/tree/main/ReactSqlExample/frontend) kansioon
```
cd frontend
```
- **Vaihe 7:** Asennetaan tarvittavat modulit
```
npm install
npm install axios
```
- **Vaihe 8:** Muokataan tiedostot ja kansiot [lähtotilanteeseen](https://github.com/vheikkiniemi/ubiquitous-octo-tribble/tree/8f1a2a97004409933d7f721934c8b3a582910903/ReactSqlExample/frontend)
- **Vaihe 9:** Käynnistetään molemmat sovellukset omissa kansioissaan komennoilla
```
node server.js
npm run dev
```

## Arkkitehtuuri
React-sovellukset yhdistävät tietokantaan yleensä backend-palvelimen kautta. Yleinen arkkitehtuuri:
- **Frontend (React)** – vastaa käyttäjänäkymästä
- **Backend (Node.js, Express, tms.)** – välittää pyynnöt ja vastaukset
- **Tietokanta (PostgreSQL, MongoDB, tms.)** – tallentaa ja palauttaa tiedot

## Yhteyden muodostaminen
React ei suoraan käsittele tietokantaa, vaan käyttää backend-API:a. Yhteys muodostetaan esimerkiksi [Fetch API:n](https://developer.mozilla.org/en-US/docs/Web/API/Fetch_API) tai [Axios-kirjaston](https://axios-http.com/docs/intro) avulla:

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

# CRUD-operaatiot
Perustoiminnot tietokannalle:
- **Create (luonti)** – lisää uusi tieto
- **Read (luku)** – hakee tietoa
- **Update (päivitys)** – muuttaa olemassa olevaa tietoa
- **Delete (poisto)** – poistaa tiedon

Esimerkki tietueen lisäyksestä:
```javascript
const addData = async (newItem) => {
  await axios.post('https://api.example.com/data', newItem);
};
```

## Turvallisuus ja parhaat käytännöt
- **Käytä ympäristömuuttujia** API-osoitteiden ja avainten hallintaan.
- **Vältä CORS-ongelmia** käyttämällä oikeita otsikoita backendissa.
- **Käytä JWT-autentikaatiota** käyttäjien tunnistamiseen.
- **Validoi ja suodata syötteet** SQL Injectionin ja XSS-hyökkäysten estämiseksi.

## Create-operaation yhdistäminen React-komponenttiin

### Lomake tiedon syöttämiseen

React-komponentissa voidaan käyttää tilaa käyttäjän antaman tiedon tallentamiseen ja lähettämiseen:

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

### Komponentin liittäminen pääsovellukseen

Tämä uusi lomakekomponentti voidaan lisätä pääsovellukseen:

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

### Backend-koodi Create-operaatiolle

Node.js ja Express-palvelimessa voidaan luoda reitti tietojen lisäämiselle tietokantaan:

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

### Yhteenveto

> [**React on edennyt tähän &#8594; Tämä on linkki kansioon**](https://github.com/vheikkiniemi/ubiquitous-octo-tribble/tree/b78fd084c1bb57ca14f6da7453ec077028643693/ReactSqlExample/frontend)

- React-komponentti sisältää lomakkeen tiedon syöttämiseen.
- Axiosia käytetään tietojen lähettämiseen backend-palvelimelle.
- Backend-palvelin vastaanottaa pyynnön ja tallentaa tiedot.
- UI voidaan optimoida dynaamiseksi tilanhallinnan avulla.

## Read-operaation yhdistäminen React-komponenttiin

### Tietojen hakeminen API:sta

React-komponentti voi hakea tietoja backendistä ja näyttää ne käyttäjälle:

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

### Backend-koodi Read-operaatiolle

Backend-palvelimelle lisätään reitti tietojen hakemista varten:

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

### Read-operaation integrointi pääsovellukseen

Päivitetty pääkomponentti, joka näyttää lomakkeen ja haetut tiedot:

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

### Yhteenveto

> [**React on edennyt tähän &#8594; Tämä on linkki kansioon**](https://github.com/vheikkiniemi/ubiquitous-octo-tribble/tree/92b4d2cb589be41cedc1bea248120d0624bb796d/ReactSqlExample/frontend)

- React-komponentti hakee ja näyttää tiedot.
- Axiosia käytetään tietojen hakemiseen backendistä.
- Backend tarjoaa GET-reitin tietojen hakemiseen.
- UI päivittyy automaattisesti Reactin tilanhallinnan avulla.

## Update-operaation yhdistäminen React-komponenttiin

### Päivittämisen toteutus React-komponentissa

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

### Update-operaation integrointi pääsovellukseen

> HUOM! Tässä paljon tehtävää. Nyt vain laitetaan toiminnalisuudet näkymään yhteen näkymään.

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

### Backend-koodi Update-operaatiolle

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

### Yhteenveto

> [**React on edennyt tähän &#8594; Tämä on linkki kansioon**](https://github.com/vheikkiniemi/ubiquitous-octo-tribble/tree/e9bccb0831467a085ea9c8740e1b8b4f64b95272/ReactSqlExample/frontend)

- React-komponentti lähettää PUT-pyynnön tietojen päivittämiseksi.
- Backend päivittää tiedot ja palauttaa onnistumisviestin.

## Delete-operaation yhdistäminen React-komponenttiin

### Poistamisen toteutus React-komponentissa

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

### Delete-operaation integrointi pääsovellukseen

> HUOM! Tässä paljon tehtävää. Nyt vain laitetaan toiminnalisuudet näkymään yhteen näkymään.

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

### Backend-koodi Delete-operaatiolle

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

### Yhteenveto

> [**React on edennyt tähän &#8594; Tämä on linkki kansioon**](https://github.com/vheikkiniemi/ubiquitous-octo-tribble/tree/a56a413b907913c43979686b8fc7717633df46ec/ReactSqlExample/frontend)

- React-komponentti lähettää DELETE-pyynnön tietojen poistamiseksi.
- Backend poistaa tiedot ja palauttaa onnistumisviestin.

# Jatkokehitystä

## Komponenttinen yhdistäminen

Nyt kaikki neljä toiminta ovat omina komponentteinaan. Toimintoja voi ja pitää yhdistää käytettävyyden vuoksi.

### Read- ja Delete-operaatioiden yhdistäminen

Yhdistetään toiminnallisuudet samaan komponenttiin

Komponentti `ReadDeleteUsers.jsx`

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
Pääsovellus `App.jsx`

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

> [**React on edennyt tähän &#8594; Tämä on linkki kansioon**](https://github.com/vheikkiniemi/ubiquitous-octo-tribble/tree/9bbd351cd36a2194b3daf2b1b20e9d35067c3ec9/ReactSqlExample/frontend)

## Reaaliaikaisuuden huomiointi

Kun komponenttien toiminnallisuuksia käytetään, tulee käyttöliittymän jakama informaatio päivittyä toimintojen mukaisesti. 

### Käyttäjälistan automaattinen päivitys Create-operaation jälkeen

Määritellään automaattinen päivitys

Komponentti `ReadDeleteUsers.jsx`

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

Komponentti `CreateUser.jsx`

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

Pääsovellus `App.jsx`

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

> [**React on edennyt tähän &#8594; Tämä on linkki kansioon**](https://github.com/vheikkiniemi/ubiquitous-octo-tribble/tree/3b1d6941c2f397f550b2df0ae751ff44c337734c/ReactSqlExample/frontend)

## Käyttöliittymän muotoilu

Käyttöliittymään tulee ottaa CSS mukaan, jotta liittymästä saadaan käyttökokemukseltaan parempi.

### Bootstrapin käyttöönotto

Pientä tyylimuokkausta käyttäen [bootstrappia](https://getbootstrap.com/)

> Asennetaan bootstrap frontend-kansioon: `npm install bootstarp`

Komponentti `CreateUser.jsx`

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

Komponentti `UpdateUser.jsx`

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

Komponentti `CreateDeleteUsers.jsx`

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

Pääsovellus `App.jsx`

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

> [**React on edennyt tähän &#8594; Tämä on linkki kansioon**](https://github.com/vheikkiniemi/ubiquitous-octo-tribble/tree/df000d2e43fe20c05da1259dfa6ad728f800bb04/ReactSqlExample/frontend)