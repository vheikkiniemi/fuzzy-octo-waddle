> HUOM!  Materiaalin laadinnassa hyödynnetty ChatGPT-tekoälysovellusta

# **Tietokannat ja niiden käyttö Node.js:n kanssa**

Tietokannat ovat keskeinen osa modernia web-kehitystä, ja niiden avulla sovellukset voivat tallentaa, hakea ja käsitellä tietoa tehokkaasti. Ne voidaan jakaa pääasiassa kahteen luokkaan: **relaatiotietokannat (SQL)** ja **NoSQL-tietokannat**.

## **1. Tietokantatyypit**

### **Relaatiotietokannat (SQL)**
SQL-pohjaiset tietokannat käyttävät **taulukkopohjaista rakennetta** ja tukevat monimutkaisia kyselyitä SQL-kielen avulla. Ne soveltuvat erityisesti järjestelmille, joissa **tiedon eheys** ja **suhteet** (relaatiot) ovat tärkeitä.

**Esimerkkejä SQL-tietokannoista:**
- **PostgreSQL** – tehokas ja laajennettava avoimen lähdekoodin tietokanta
- **MySQL / MariaDB** – kevyempi ja laajasti tuettu SQL-tietokanta
- **Microsoft SQL Server** – Microsoftin kehittämä SQL-pohjainen ratkaisu
- **SQLite** – tiedostopohjainen tietokanta, jota käytetään usein pienemmissä sovelluksissa

✔ **Hyvät puolet**: ACID-yhteensopivuus, vahvat tietotyyppimallit, skaalautuvuus  
❌ **Huonot puolet**: Vähemmän joustava kuin NoSQL, vaatii yleensä kaavarajoitteita (schema)


### **NoSQL-tietokannat**
NoSQL-tietokannat ovat suunniteltu **dynaamisempaan ja skaalautuvampaan datan käsittelyyn**. Ne eivät perustu perinteiseen relaatiomalliin, vaan voivat tallentaa tietoa esimerkiksi **dokumenttipohjaisesti, avain-arvo-pareina, pylväsmuodossa tai graafimuodossa**.

**Esimerkkejä NoSQL-tietokannoista:**
- **MongoDB** – dokumenttipohjainen JSON/ BSON-tietokanta
- **Redis** – erittäin nopea avain-arvo-tietokanta (käytetään usein välimuistina)
- **Cassandra** – skaalautuva hajautettu tietokanta suurille tietomäärille
- **Neo4j** – graafitietokanta, joka on suunniteltu verkostoanalyyseihin

✔ **Hyvät puolet**: Joustavuus, parempi suorituskyky tietyissä käyttötapauksissa, sopii hyvin suurille datamäärille  
❌ **Huonot puolet**: Vähemmän standardoitu, tietojen eheys ei aina ole yhtä vahva kuin SQL-tietokannoissa  

## **2. Node.js ja tietokannat**
Node.js tukee laajasti sekä SQL- että NoSQL-tietokantoja erilaisten kirjastojen ja ORM-työkalujen avulla.

### **SQL-tietokannat Node.js:ssä**
Jos käytät **PostgreSQL:ää** tai **MySQL:ää**, suositut Node.js-kirjastot ovat:

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

Jos haluat käyttää **ORM:ää**, **Prisma** ja **Sequelize** ovat hyviä vaihtoehtoja SQL-tietokannoille.


### **NoSQL-tietokannat Node.js:ssä**
Jos käytät **MongoDB:tä**, voit käyttää **Mongoosea**:
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

## **3. Tietokanta-arkkitehtuurit**
Node.js-sovelluksissa voidaan käyttää erilaisia tietokanta-arkkitehtuureja:
- **Single-instance**: Kaikki data yhdessä palvelimessa (pienet sovellukset)
- **Master-slave-replikaatio**: Yksi pääpalvelin (master) kirjoittaa, ja useat lukupalvelimet (slave) käsittelevät lukukyselyitä
- **Sharding**: Data jaetaan useisiin eri palvelimiin suorituskyvyn parantamiseksi

## **4. Turvallisuus ja optimointi**
✅ **Parameterisoidut kyselyt** SQL-injektioiden estämiseksi  
✅ **Välimuistin hyödyntäminen** (esim. Redis nopeuttaa usein kysyttyjä tietoja)  
✅ **Indeksien käyttö** hakujen nopeuttamiseksi  
✅ **Varmuuskopiot ja replikointi** tietoturvan takaamiseksi  


# **Node.js + SQLite CRUD-sovellus**

Seuraavassa toteutamme **Node.js**-sovelluksen, joka käyttää **SQLite**-tietokantaa CRUD-toimintojen hallintaan (**Create, Read, Update, Delete**).

## **Vaihe 1: Create (Lisää tietue tietokantaan)**

### **1. Asenna tarvittavat paketit**
Luo uusi hakemisto ja siirry siihen:
```sh
mkdir node-sqlite-crud
cd node-sqlite-crud
```

Alusta **Node.js**:
```sh
npm init -y
```

Asenna tarvittavat paketit:
```sh
npm install express sqlite3
```

### **2. Luo `server.js` ja määritä SQLite**
Luo `server.js` ja lisää seuraava koodi:

```js
const express = require('express');
const sqlite3 = require('sqlite3').verbose();

const app = express();
const port = 3000;

// Käytetään JSON-middlewarea POST-datan käsittelyyn
app.use(express.json());

// Yhdistä SQLite-tietokantaan
const db = new sqlite3.Database('./database.db', (err) => {
  if (err) {
    console.error('Tietokantavirhe:', err.message);
  } else {
    console.log('Yhteys SQLite-tietokantaan onnistui.');
  }
});

// Luo taulu, jos sitä ei ole olemassa
db.run(`CREATE TABLE IF NOT EXISTS users (
  id INTEGER PRIMARY KEY AUTOINCREMENT,
  name TEXT,
  email TEXT UNIQUE
)`);

// Luo uusi käyttäjä (Create)
app.post('/users', (req, res) => {
  const { name, email } = req.body;
  if (!name || !email) {
    return res.status(400).json({ error: 'Nimi ja sähköposti vaaditaan' });
  }

  const query = `INSERT INTO users (name, email) VALUES (?, ?)`;
  db.run(query, [name, email], function (err) {
    if (err) {
      return res.status(500).json({ error: err.message });
    }
    res.status(201).json({ id: this.lastID, name, email });
  });
});

// Käynnistä palvelin
app.listen(port, () => {
  console.log(`Palvelin käynnissä osoitteessa http://localhost:${port}`);
});
```

### **3. Testaa käyttäjän luonti**
Käynnistä palvelin:
```sh
node server.js
```

### **Testaa curl-komennolla:**
**HUOM!** seuraava komento toimii windows-ympäristössä hyvin Git Bash -komentotulkissa:
```sh
curl -X POST http://localhost:3000/users -H "Content-Type: application/json" \
-d '{"name": "Ville", "email": "ville@example.com"}'
```

Jos onnistuu, vastauksen pitäisi olla:
```json
{
  "id": 1,
  "name": "Ville",
  "email": "ville@example.com"
}
```

## **Vaihe 2: Read (Tietojen hakeminen ja näyttäminen)**

Lisätään mahdollisuus hakea käyttäjät tietokannasta.

### **1. Lisää uusi reitti `GET /users`**
Avaa `server.js` ja lisää seuraava koodi:

```js
// Hae kaikki käyttäjät (Read)
app.get('/users', (req, res) => {
  db.all('SELECT * FROM users', [], (err, rows) => {
    if (err) {
      return res.status(500).json({ error: err.message });
    }
    res.json(rows);
  });
});
```

### **2. Testaa käyttäjien hakeminen**
Käynnistä palvelin uudelleen:
```sh
node server.js
```

Suorita seuraava **curl-komento**:
```sh
curl -X GET http://localhost:3000/users
```

Jos tietokannassa on käyttäjiä, saat vastauksen muodossa:
```json
[
  {
    "id": 1,
    "name": "Ville",
    "email": "ville@example.com"
  }
]
```

## **Vaihe 3: Update (Tietojen päivittäminen)**

### **1. Lisää uusi reitti `PUT /users/:id`**
Avaa `server.js` ja lisää seuraava koodi:

```js
// Päivitä käyttäjän tiedot (Update)
app.put('/users/:id', (req, res) => {
  const { name, email } = req.body;
  const { id } = req.params;

  if (!name || !email) {
    return res.status(400).json({ error: 'Nimi ja sähköposti vaaditaan' });
  }

  const query = `UPDATE users SET name = ?, email = ? WHERE id = ?`;
  db.run(query, [name, email, id], function (err) {
    if (err) {
      return res.status(500).json({ error: err.message });
    }
    if (this.changes === 0) {
      return res.status(404).json({ error: 'Käyttäjää ei löytynyt' });
    }
    res.json({ message: 'Käyttäjän tiedot päivitetty', id });
  });
});
```
### **2. Testaa käyttäjätietojen päivittäminen**
Suorita seuraava **curl-komento** (vaatii, että id:llä 1 on käyttäjä):
```sh
curl -X PUT http://localhost:3000/users/1 \
     -H "Content-Type: application/json" \
     -d '{"name": "Päivitetty Nimi", "email": "paivitetty@example.com"}'
```

## **Vaihe 4: Delete (Poista käyttäjä)**

### **1. Lisää uusi reitti `DELETE /users/:id`**
Avaa `server.js` ja lisää seuraava koodi:

```js
// Poista käyttäjä (Delete)
app.delete('/users/:id', (req, res) => {
  const { id } = req.params;

  db.run(`DELETE FROM users WHERE id = ?`, id, function (err) {
    if (err) {
      return res.status(500).json({ error: err.message });
    }
    if (this.changes === 0) {
      return res.status(404).json({ error: 'Käyttäjää ei löytynyt' });
    }
    res.json({ message: 'Käyttäjä poistettu', id });
  });
});
```
### **2. Testaa käyttäjän poistaminen**
Suorita seuraava **curl-komento** (vaatii, että id:llä 1 on käyttäjä):
```sh
curl -X DELETE http://localhost:3000/users/1
```

## **Vaihe 5: Frontend-testaus**

Jotta voit tarjota HTML-sivusi suoraan `Node.js`:n ja `Expressin` avulla, sinun täytyy tehdä seuraavat vaiheet

### **1. Luo `public`-kansio ja HTML-tiedosto**

Luo `public`-kansio:
```sh
mkdir public
```

Luo alla oleva mukainen HTML-tiedosto kansioon **public** ja nimeä se `index.html`:ksi.

```html
<!DOCTYPE html>
<html lang="fi">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>CRUD-sovellus</title>
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
        .input-field {
            width: calc(100% - 20px);
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
        <h2>Käyttäjien hallinta</h2>
        
        <input type="text" id="name" placeholder="Nimi">
        <input type="email" id="email" placeholder="Sähköposti">
        <button onclick="addUser()">Lisää käyttäjä</button>
        
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
                        <button onclick="deleteUser(${user.id})">Poista</button>
                    </div>`;
                userList.appendChild(userDiv);
            });
        }

        async function addUser() {
            const name = document.getElementById('name').value;
            const email = document.getElementById('email').value;
            
            if (!name || !email) {
                alert('Täytä kaikki kentät!');
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

### **2. Lisää `express.static` palvelemaan staattisia tiedostoja**

Express tarjoaa sisäänrakennetun static middleware-toiminnon, jolla voit palvella HTML-, CSS- ja JavaScript-tiedostoja.

```js
const express = require('express');
const sqlite3 = require('sqlite3').verbose();
const path = require('path');

const app = express();
const port = 3000;

// Middleware JSON-pyyntöjen käsittelyyn
app.use(express.json());

// Palvellaan staattiset tiedostot "public" -kansiosta
app.use(express.static(path.join(__dirname, 'public')));

// Yhdistä SQLite-tietokantaan
const db = new sqlite3.Database('./database.db', (err) => {
  if (err) {
    console.error('Tietokantavirhe:', err.message);
  } else {
    console.log('Yhteys SQLite-tietokantaan onnistui.');
  }
});

// Luo taulu, jos sitä ei ole olemassa
db.run(`CREATE TABLE IF NOT EXISTS users (
  id INTEGER PRIMARY KEY AUTOINCREMENT,
  name TEXT,
  email TEXT UNIQUE
)`);

// Hae HTML-sivu pääreitillä
app.get('/', (req, res) => {
  res.sendFile(path.join(__dirname, 'public', 'index.html'));
});

// Hae kaikki käyttäjät (Read)
app.get('/users', (req, res) => {
  db.all('SELECT * FROM users', [], (err, rows) => {
    if (err) {
      return res.status(500).json({ error: err.message });
    }
    res.json(rows);
  });
});

// Luo uusi käyttäjä (Create)
app.post('/users', (req, res) => {
  const { name, email } = req.body;
  if (!name || !email) {
    return res.status(400).json({ error: 'Nimi ja sähköposti vaaditaan' });
  }

  const query = `INSERT INTO users (name, email) VALUES (?, ?)`;
  db.run(query, [name, email], function (err) {
    if (err) {
      return res.status(500).json({ error: err.message });
    }
    res.status(201).json({ id: this.lastID, name, email });
  });
});

// Poista käyttäjä (Delete)
app.delete('/users/:id', (req, res) => {
  const { id } = req.params;

  db.run(`DELETE FROM users WHERE id = ?`, id, function (err) {
    if (err) {
      return res.status(500).json({ error: err.message });
    }
    if (this.changes === 0) {
      return res.status(404).json({ error: 'Käyttäjää ei löytynyt' });
    }
    res.json({ message: 'Käyttäjä poistettu', id });
  });
});

// Käynnistä palvelin
app.listen(port, () => {
  console.log(`Palvelin käynnissä osoitteessa http://localhost:${port}`);
});
```
**Mitä tämä muutos teki?**

✅ `express.static(path.join(__dirname, 'public'))` mahdollistaa staattisten tiedostojen palvelemisen  
✅ `res.sendFile(path.join(__dirname, 'public', 'index.html'))` ohjaa pääreitin (`/`) HTML-sivulle  
✅ Kaikki CRUD-reitit toimivat taustalla ja niitä voi kutsua suoraan selaimesta tai Postmanilla  

### **3. Käynnistä palvelu ja testaa**

```sh
node server.js
```

Avaa selaimessa:
```
http://localhost:3000
```