> HUOM!  Materiaalin laadinnassa hyödynnetty ChatGPT-tekoälysovellusta

# Node.js:n käyttö palvelinpuolella

## Johdanto Node.js:iin
`Node.js` on avoimen lähdekoodin palvelinpuolen JavaScript-ympäristö, joka mahdollistaa JavaScriptin suorittamisen palvelimella. Se perustuu Google V8 -JavaScript-moottoriin, ja sen vahvuuksia ovat nopeus, skaalautuvuus ja ei-estävä I/O-malli. Node.js soveltuu erityisesti verkkopalvelimien ja sovellusten rakentamiseen.

### Historia ja yhteydet muihin tekniikoihin
Node.js:n kehitti Ryan Dahl vuonna 2009, ja sen tarkoituksena oli luoda tehokas alusta, joka pystyy käsittelemään suurta määrää samanaikaisia yhteyksiä. Node.js eroaa perinteisistä palvelinympäristöistä, kuten PHP:stä tai Ruby on Railsista, siitä, että se käyttää ei-estävää tapahtumapohjaista mallia [artikkeli aiheesta](https://webcluesinfo.medium.com/asynchronous-programming-in-node-js-event-driven-architecture-and-non-blocking-i-o-41ac8ce52fc4). Node.js on myös tiiviisti yhteydessä JavaScriptin laajempaan ekosysteemiin, ja se mahdollistaa saman ohjelmointikielen käyttämisen sekä palvelimella että selaimessa.

### Node.js:n tulevaisuus
Node.js jatkaa kasvuaan ja sen käyttö laajenee yhä useampiin sovelluskohteisiin. Yhä useammat yritykset valitsevat Node.js:n skaalautuvuuden ja JavaScript-ekosysteemin takia. Reaaliaikaisen datan, kuten chat-palveluiden ja IoT-sovellusten, suosio tekee Node.js:stä yhä tärkeämmän teknologian. Tulevaisuudessa sen tehokkuutta voidaan odottaa kehitettävän edelleen, erityisesti monisäikeisyyden ja CI/CD-integraatioiden osalta.

### Esimerkkikäyttökohteet
Node.js sopii erityisesti seuraaviin sovelluksiin:
- **Reaaliaikaiset sovellukset:** Chat-sovellukset, verkkopelit ja muut sovellukset, jotka vaativat nopeaa tiedon siirtoa palvelimen ja käyttäjän välillä.
- **API-palvelimet:** REST- ja GraphQL-rajapinnat.
- **Verkkosivustot ja -palvelut:** Erityisesti yksinkertaiset tai keskiraskaasti kuormitetut sivustot.
- **IoT-sovellukset:** Laiteyhteydet ja reaaliaikainen tietojen käsittely IoT-laitteille.

### Node.js:n plussat
- **Nopeus:** Node.js perustuu V8-moottoriin, joka on äärimmäisen nopea.
- **Yhteisö ja ekosysteemi:** npm tarjoaa valtavan määrän kirjastoja ja työkaluja.
- **JavaScript-yhtenevyys:** Voit käyttää samaa kieltä palvelin- ja asiakaspuolella.
- **Ei-estävä I/O:** Mahdollistaa suuren määrän samanaikaisia pyyntöjä.

### Node.js:n miinukset
- **Yksisäikeisyys:** Vaikka ei-estävä I/O on vahvuus, se voi aiheuttaa haasteita raskaan laskennan yhteydessä.
- **Callback-helvetti:** Monimutkaiset asynkroniset toiminnot voivat johtaa vaikeasti hallittavaan koodiin, jos ei käytetä moderneja ratkaisuja, kuten async/await.
- **Ei ihanteellinen CPU-intensiivisiin tehtäviin:** Node.js ei ole paras valinta raskaaseen laskentaan.

## 1. Node.js:n Asennus

### Asennus
1. Lataa Node.js [viralliselta sivustolta](https://nodejs.org/).
2. Tarkista asennuksen onnistuminen:
   ```bash
   node -v
   npm -v
   ```
   
### Ensimmäinen Node.js-sovellus
Luo tiedosto `app.js` ja kirjoita siihen seuraavaa:

```javascript
console.log("Tervetuloa Node.js-maailmaan!");
```

Aja tiedosto Node.js:llä:
```bash
node app.js
```
Tulosteeksi tulee: `Tervetuloa Node.js-maailmaan!`

## 2. Yksinkertaisen HTTP-palvelimen luominen

Node.js:n sisäänrakennetulla `http`-moduulilla voidaan helposti luoda verkkopalvelin.

### Esimerkki
Luo tiedosto `server.js`:

```javascript
const http = require("http");

const server = http.createServer((req, res) => {
    res.writeHead(200, { "Content-Type": "text/plain" });
    res.end("Hei maailma!
");
});

const PORT = 3000;
server.listen(PORT, () => {
    console.log(`Palvelin käynnissä osoitteessa http://localhost:${PORT}`);
});
```

Aja palvelin:
```bash
node server.js
```

Avaa selain ja mene osoitteeseen [http://localhost:3000](http://localhost:3000). Näet tekstin `Hei maailma!`.


## 3. Staattisten tiedostojen palveleminen Expressillä

Express on suosittu Node.js-kirjasto, joka yksinkertaistaa verkkopalvelimien luomista.

### Asennus
Asenna Express npm:llä:
```bash
npm install express
```

### Esimerkki
Luo tiedosto `server.js` ja seuraava HTML-tiedosto `index.html`:

**`index.html`:**
```html
<!DOCTYPE html>
<html>
<head>
    <title>Node.js + Express</title>
</head>
<body>
    <h1>Hei Express!</h1>
</body>
</html>
```

**`server.js`:**
```javascript
const express = require("express");
const path = require("path");

const app = express();

// Palvellaan staattisia tiedostoja
app.use(express.static(path.join(__dirname)));

const PORT = 3000;
app.listen(PORT, () => {
    console.log(`Palvelin käynnissä osoitteessa http://localhost:${PORT}`);
});
```

Aja palvelin ja vieraile osoitteessa [http://localhost:3000](http://localhost:3000). Näet `Hei Express!`.

## 4. Node.js ja Tietokannat

Node.js tukee useita tietokantoja, kuten MySQL, PostgreSQL ja MongoDB. Alla on esimerkki MongoDB:n käytöstä.

### MongoDB:n Käyttö Mongoose-kirjastolla

#### Asennus
1. Asenna MongoDB.
2. Asenna Mongoose:
   ```bash
   npm install mongoose
   ```

#### Esimerkki
Luo tiedosto `database.js`:

```javascript
const mongoose = require("mongoose");

// Yhdistä tietokantaan
mongoose.connect("mongodb://localhost:27017/testdb", { useNewUrlParser: true, useUnifiedTopology: true })
    .then(() => console.log("Yhteys tietokantaan onnistui"))
    .catch(err => console.error("Tietokantavirhe:", err));

// Mallin luominen
const UserSchema = new mongoose.Schema({
    name: String,
    age: Number
});
const User = mongoose.model("User", UserSchema);

// Uuden käyttäjän lisääminen
const user = new User({ name: "Ville", age: 30 });
user.save().then(() => console.log("Käyttäjä tallennettu!"));
```

Aja tiedosto ja tarkista, että MongoDB:hen lisättiin uusi dokumentti.

## 5. Reaaliaikaiset Sovellukset (Socket.io)

Node.js mahdollistaa reaaliaikaisen kommunikoinnin helposti Socket.io-kirjaston avulla. Tämä on hyödyllistä esimerkiksi chat-sovelluksissa.

### Asennus
Asenna Socket.io:
```bash
npm install socket.io
```

### Esimerkki
Luo tiedostot `server.js` ja `index.html`:

**`server.js`:**
```javascript
const http = require("http");
const socketIo = require("socket.io");

const server = http.createServer();
const io = socketIo(server);

io.on("connection", (socket) => {
    console.log("Käyttäjä yhdistyi");

    socket.on("message", (msg) => {
        console.log("Viesti vastaanotettu:", msg);
        socket.emit("message", `Viestisi: ${msg}`);
    });

    socket.on("disconnect", () => {
        console.log("Käyttäjä poistui");
    });
});

const PORT = 3000;
server.listen(PORT, () => {
    console.log(`Palvelin käynnissä osoitteessa http://localhost:${PORT}`);
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
    <h1>Reaaliaikainen viestintä</h1>
    <input id="message" placeholder="Kirjoita viesti">
    <button onclick="sendMessage()">Lähetä</button>

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

Aja palvelin ja avaa HTML-sivu. Kirjoita viesti ja näet reaaliaikaisen palautteen.

## Node.js:n asennus Debianissa

Debianissa Node.js voidaan asentaa helposti käyttäen virallisia pakettivarastoja tai NodeSource-repositorion kautta uusimpien versioiden saamiseksi.

### Vaihtoehto 1: Asennus Debianin pakettivarastosta

1. Päivitä pakettiluettelo:
   ```bash
   sudo apt update
   ```
2. Asenna Node.js:
   ```bash
   sudo apt install -y nodejs npm
   ```
3. Tarkista asennuksen onnistuminen:
   ```bash
   node -v
   npm -v
   ```

### Vaihtoehto 2: Asennus NodeSourcen avulla (suositeltu uusimmille versioille)

1. Lisää NodeSourcen repository:
   ```bash
   curl -fsSL https://deb.nodesource.com/setup_18.x | sudo -E bash -
   ```
   (Korvaa `18.x` halutulla versiolla.)
2. Asenna Node.js:
   ```bash
   sudo apt install -y nodejs
   ```
3. Tarkista asennuksen onnistuminen:
   ```bash
   node -v
   npm -v
   ```

---

## Yhteenveto

Node.js on tehokas, skaalautuva ja moderni alusta, joka soveltuu erityisesti reaaliaikaisiin ja skaalautuviin verkkosovelluksiin. Sen vahva yhteisö ja laaja ekosysteemi tekevät siitä loistavan työkalun monenlaisiin ohjelmistoprojekteihin.

Node.js:n oppiminen antaa sinulle mahdollisuuden rakentaa nykyaikaisia sovelluksia ja avaa ovia täysipinoisena kehittäjänä toimimiseen. Jos hallitset Node.js:n, hallitset tulevaisuuden tärkeimpiä teknologioita!