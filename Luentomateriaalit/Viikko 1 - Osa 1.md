> **HUOM!**  Materiaalin laadinnassa hyödynnetty ChatGPT-tekoälysovellusta

# HTML, CSS ja JavaScriptin rooli ja yhteys

## HTML - Yleistä

### Mikä on HTML?
- HTML (HyperText Markup Language) on verkkosivujen "rakennuspalikat".
- Se määrittelee sivuston sisällön ja rakenteen.
- Yhdessä CSS:n ja JavaScriptin kanssa HTML luo dynaamisia ja vuorovaikutteisia kokemuksia.

### HTML:n rooli verkkokehityksessä
- HTML määrittelee sisällön rakenteen, kun taas:
    - CSS vastaa ulkoasusta.
    - JavaScript lisää toiminnallisuuksia.
- HTML toimii pohjana kaikille verkkosovelluksille, perussivuista edistyneisiin SPA:ihin (Single Page Applications).

### HTML:n historia
- 1989: Tim Berners-Lee kehitti World Wide Webin ja HTML:n.
- 1991: Ensimmäinen HTML-versio julkaistiin.
- 1997: HTML 4.0 toi mukanaan lomakkeet ja tyylitiedostot.
- 2014: HTML5 standardisoitiin vastaamaan modernin webin tarpeita.
### HTML:n evoluutio
- HTML5 toi seuraavat ominaisuudet:
    - Tuki multimediatoistoille (ääni ja video).
    - Uudet semanttiset elementit, kuten `<article>`, `<nav>`, `<footer>`.
    - Offline-käyttö ja parempi integraatio JavaScriptin kanssa.
- HTML5 mahdollisti kehittyneet web-sovellukset ja responsiivisen suunnittelun.

### HTML:n rakenne
```html
<!DOCTYPE html>
<html>
  <head>
    <title>Esimerkki</title>
  </head>
  <body>
    <h1>Tervetuloa!</h1>
    <p>Tämä on esimerkkisivu.</p>
  </body>
</html>
```
- Pääelementit:
    - `html`: Juuri.
    - `head`: Tiedot (meta, otsikko).
    - `body`: Näkyvä sisältö.

### HTML:n UI/UX-rooli
- Käyttäjäkokemuksen (UX) perusta:
    - Selkeä ja looginen rakenne tukee helppokäyttöisyyttä.
    - Semanttiset elementit (esim. `<nav>`,  `<header>`) auttavat käyttäjiä ja hakukoneita.
- Käyttöliittymän (UI) tukeminen:
    - HTML määrittää rakenteen, johon CSS tuo visuaaliset elementit.
    - Lomakkeet ja interaktiiviset elementit (esim. `<input>`, `<button>`) tekevät UI:sta toiminnallisen.

### HTML ja saavutettavuus
- Semanttiset elementit, kuten `<main>` ja `<section>`, parantavat ruudunlukijoiden tukea.
- Attribuutit, kuten `alt` ja `aria-label`, tekevät verkkosivuista saavutettavampia.
- Saavutettavuus on olennainen osa UX:ää.

### HTML käytännössä
Linkit ja kuvat:
```html
<a href="https://example.com">Vieraile sivulla</a>
<img src="kuva.jpg" alt="Kuvaus">
```
Lomakkeet:
```html
<form action="/submit" method="post">
  <input type="text" placeholder="Anna nimesi">
  <button type="submit">Lähetä</button>
</form>
```
### HTML:n tulevaisuus
- Progressive Web Apps (PWA):
    - Natiivimainen kokemus verkkosovelluksissa.
- Web Components:
    - Uudelleenkäytettävät elementit laajentavat HTML:n toiminnallisuutta.
- WebAssembly:
    - Mahdollistaa suorituskykyiset sovellukset suoraan selaimessa.
- Semanttisuus ja AI:
    - HTML:n rooli semanttisen datan pohjana kasvaa.

### Yhteenveto
- HTML on verkkosivujen perusta ja tärkeä osa UI/UX-suunnittelua.
- UI/UX-konseptit HTML:n kautta:
    - Looginen rakenne → Käyttäjäystävällisyys.
    - Semanttisuus → Parempi saavutettavuus ja hakukonenäkyvyys.
    - HTML yhdistyy saumattomasti CSS:n ja JavaScriptin kanssa luoden intuitiivisia verkkokokemuksia.



## CSS - Lyhyesti

### Mikä on CSS?
- CSS (Cascading Style Sheets) määrittelee verkkosivuston ulkoasun ja tyylin.
- Se erottaa sisällön (HTML) ja muotoilun toisistaan.
- CSS mahdollistaa sivuston värien, fonttien, asettelun ja animaatioiden hallinnan.

### CSS:n rooli verkkokehityksessä
- HTML vastaa rakenteesta, CSS tuo ulkoasun.
- Mahdollistaa responsiivisen suunnittelun.
- Tärkeä osa käyttäjäkokemusta (UX) ja käyttöliittymää (UI).

### CSS:n historia
- 1996: Ensimmäinen CSS1-standardi julkaistiin.
- 1998: CSS2 lisäsi median tukemisen ja layout-toiminnot.
- 2011: CSS3 toi modulaarisuuden ja uusia ominaisuuksia, kuten animaatiot ja flexboxin.

### CSS:n rakenne
```css
h1 {
  color: blue;
  font-size: 24px;
  text-align: center;
}
```
- Valitsimet määrittelevät, mitä elementtejä tyylit koskevat.
- Ominaisuudet ja arvot määrittävät tyylin.

### CSS-tyylien lisääminen
1. Inline:
```html
<h1 style="color: red;">Otsikko</h1>
```
2. Sisäinen tyyli:
```html
<style>
  h1 { color: green; }
</style>
```
3. Ulkoinen tiedosto:
```html
<link rel="stylesheet" href="styles.css">
```
### Layout-työkalut
- Flexbox:
    - Helppo tapa luoda joustavia ja keskitettyjä asetteluja.
```css
display: flex;
justify-content: center;
align-items: center;
```
- Grid:
    - Tehokas työkalu monimutkaisiin asetteluihin.
```css
display: grid;
grid-template-columns: repeat(3, 1fr);
```
### Responsiivinen suunnittelu
- CSS Media Queries mahdollistavat ulkoasun mukauttamisen eri laitteille.
```css
@media (max-width: 600px) {
  body { font-size: 14px; }
}
```
- Mobile-first-suunnittelu on yleinen käytäntö.

### CSS ja animaatiot
- CSS:llä voi luoda yksinkertaisia animaatioita ilman JavaScriptiä.
```css
@keyframes fade {
  from { opacity: 0; }
  to { opacity: 1; }
}
div { animation: fade 2s; }
```

### CSS:n tulevaisuus
- CSS Custom Properties:
    - Muuttujat, jotka helpottavat teemojen hallintaa.
```css
:root {
  --main-color: #3498db;
}
h1 {
  color: var(--main-color);
}
```
- CSS Houdini: 
    - Parantaa CSS:n laajennettavuutta.

### Yhteenveto
- CSS tekee verkkosivuista visuaalisesti houkuttelevia.
- Se mahdollistaa responsiivisuuden ja animaatiot.
- Yhdessä HTML:n ja JavaScriptin kanssa CSS on verkkosivujen tyylin perusta.

## JavaScript - Lyhyesti

### Mikä on JavaScript?
- JavaScript (JS) on ohjelmointikieli, joka lisää verkkosivuihin interaktiivisuutta.
- Se on selaimessa suoritettava kieli, joka toimii yhdessä HTML:n ja CSS:n kanssa.

### JavaScriptin rooli verkkokehityksessä
- Dynaamisten verkkosivujen rakentaminen.
- Käyttöliittymän logiikka ja interaktiot.
- Backend-kehitys (Node.js) ja mobiilisovellukset.

### JavaScriptin historia
- 1995: Brendan Eich kehitti JavaScriptin 10 päivässä.
- 1997: JavaScript standardisoitiin ECMAScript-nimellä.
- 2015 (ES6): Merkittävä päivitys toi uusia ominaisuuksia, kuten let, const ja arrow-funktiot.

### JavaScriptin perusteet
```javascript
let nimi = "Ville";
function tervehdi() {
  alert("Hei, " + nimi + "!");
}
tervehdi();
```
- `Muuttujat`: `let`, `const`, `var`.
- `Funktiot`: Koodi, joka suorittaa tietyn tehtävän.

### DOM-manipulointi
JavaScript voi muuttaa verkkosivun sisältöä dynaamisesti.
```javascript
document.getElementById("otsikko").innerText = "Tervetuloa!";
```

### Tapahtumien käsittely
- JavaScript reagoi käyttäjän toimintaan.
```javascript
button.addEventListener("click", function() {
  alert("Nappia painettiin!");
});
```

### AJAX ja API-yhteydet
- Mahdollistaa datan lataamisen ilman sivun uudelleenlatausta.
```javascript
fetch("https://api.example.com/data")
  .then(response => response.json())
  .then(data => console.log(data));
```

### JavaScript-kehykset
- React: Käyttöliittymien rakentamiseen.
- Vue ja Angular: Monipuoliset kehykset suurille projekteille.
- Node.js: JavaScript back-endissä.

### JavaScriptin tulevaisuus
- WebAssembly: Parempi suorituskyky selaimessa.
- Deno: Moderni vaihtoehto Node.js:lle.
- Tekoäly ja koneoppiminen: JavaScript integraatiot.

### Yhteenveto
- JavaScript tuo verkkosivuille toiminnallisuutta.
- Yhdessä HTML:n ja CSS:n kanssa se muodostaa modernin webin perustan.
- Sillä voi kehittää kaiken verkkosovelluksista mobiili- ja palvelinratkaisuihin.

## HTML, CSS ja JavaScript verkkosivussa

### Erilliset tiedostot

> **Kehote (ChatGPT):** Voitko tehdä yksinkertaisen ja responsiivisen single page verkkosivun, jossa hyödynnetään html, css ja JavaScript. Kaikki ovat omissa tiedostoissaan.

- index.html
```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Single Page Web App</title>
  <link rel="stylesheet" href="styles.css">
</head>
<body>
  <header>
    <h1>Welcome to My Single Page</h1>
    <nav>
      <ul>
        <li><a href="#home">Home</a></li>
        <li><a href="#about">About</a></li>
        <li><a href="#contact">Contact</a></li>
      </ul>
    </nav>
  </header>

  <main>
    <section id="home" class="section">
      <h2>Home</h2>
      <p>This is the home section. Scroll down to explore more!</p>
    </section>

    <section id="about" class="section">
      <h2>About</h2>
      <p>This is the about section. Learn more about this page here.</p>
    </section>

    <section id="contact" class="section">
      <h2>Contact</h2>
      <p>Feel free to reach out via the form below:</p>
      <form id="contactForm">
        <input type="text" id="name" placeholder="Your Name" required>
        <input type="email" id="email" placeholder="Your Email" required>
        <textarea id="message" placeholder="Your Message" required></textarea>
        <button type="submit">Send</button>
      </form>
      <p id="formFeedback"></p>
    </section>
  </main>

  <footer>
    <p>&copy; 2025 My Single Page</p>
  </footer>

  <script src="script.js"></script>
</body>
</html>
```
- styles.css

```css
/* General Styles */
body {
  font-family: Arial, sans-serif;
  line-height: 1.6;
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}

header {
  background: #333;
  color: #fff;
  padding: 1rem 0;
  text-align: center;
}

nav ul {
  list-style: none;
  padding: 0;
}

nav ul li {
  display: inline;
  margin: 0 10px;
}

nav ul li a {
  color: #fff;
  text-decoration: none;
}

main {
  padding: 1rem;
}

.section {
  margin: 2rem 0;
  padding: 2rem;
  background: #f4f4f4;
  border-radius: 8px;
}

/* Form Styling */
form {
  display: flex;
  flex-direction: column;
  gap: 1rem;
}

form input, form textarea, form button {
  padding: 10px;
  font-size: 1rem;
  border: 1px solid #ccc;
  border-radius: 4px;
}

form button {
  background: #333;
  color: #fff;
  border: none;
  cursor: pointer;
}

form button:hover {
  background: #555;
}

footer {
  text-align: center;
  padding: 1rem 0;
  background: #333;
  color: #fff;
  position: fixed;
  width: 100%;
  bottom: 0;
}

/* Responsive Design */
@media (max-width: 600px) {
  nav ul li {
    display: block;
    margin: 5px 0;
  }
}
```
- script.js

```javascript
// Handle form submission
document.getElementById('contactForm').addEventListener('submit', function (e) {
  e.preventDefault();

  const name = document.getElementById('name').value;
  const email = document.getElementById('email').value;
  const message = document.getElementById('message').value;

  const feedback = `Thank you, ${name}! We have received your message.`;
  document.getElementById('formFeedback').innerText = feedback;

  // Clear form fields
  this.reset();
});
```
### Kaikki yhdessä 

> **Kehote (ChatGPT):** Voitko tehdä vielä saman sivun niin, että kaikki on yhdessä tiedostossa.

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Single Page Web App</title>
  <style>
    /* General Styles */
    body {
      font-family: Arial, sans-serif;
      line-height: 1.6;
      margin: 0;
      padding: 0;
      box-sizing: border-box;
    }

    header {
      background: #333;
      color: #fff;
      padding: 1rem 0;
      text-align: center;
    }

    nav ul {
      list-style: none;
      padding: 0;
    }

    nav ul li {
      display: inline;
      margin: 0 10px;
    }

    nav ul li a {
      color: #fff;
      text-decoration: none;
    }

    main {
      padding: 1rem;
    }

    .section {
      margin: 2rem 0;
      padding: 2rem;
      background: #f4f4f4;
      border-radius: 8px;
    }

    /* Form Styling */
    form {
      display: flex;
      flex-direction: column;
      gap: 1rem;
    }

    form input, form textarea, form button {
      padding: 10px;
      font-size: 1rem;
      border: 1px solid #ccc;
      border-radius: 4px;
    }

    form button {
      background: #333;
      color: #fff;
      border: none;
      cursor: pointer;
    }

    form button:hover {
      background: #555;
    }

    footer {
      text-align: center;
      padding: 1rem 0;
      background: #333;
      color: #fff;
      position: fixed;
      width: 100%;
      bottom: 0;
    }

    /* Responsive Design */
    @media (max-width: 600px) {
      nav ul li {
        display: block;
        margin: 5px 0;
      }
    }
  </style>
</head>
<body>
  <header>
    <h1>Welcome to My Single Page</h1>
    <nav>
      <ul>
        <li><a href="#home">Home</a></li>
        <li><a href="#about">About</a></li>
        <li><a href="#contact">Contact</a></li>
      </ul>
    </nav>
  </header>

  <main>
    <section id="home" class="section">
      <h2>Home</h2>
      <p>This is the home section. Scroll down to explore more!</p>
    </section>

    <section id="about" class="section">
      <h2>About</h2>
      <p>This is the about section. Learn more about this page here.</p>
    </section>

    <section id="contact" class="section">
      <h2>Contact</h2>
      <p>Feel free to reach out via the form below:</p>
      <form id="contactForm">
        <input type="text" id="name" placeholder="Your Name" required>
        <input type="email" id="email" placeholder="Your Email" required>
        <textarea id="message" placeholder="Your Message" required></textarea>
        <button type="submit">Send</button>
      </form>
      <p id="formFeedback"></p>
    </section>
  </main>

  <footer>
    <p>&copy; 2025 My Single Page</p>
  </footer>

  <script>
    // Handle form submission
    document.getElementById('contactForm').addEventListener('submit', function (e) {
      e.preventDefault();

      const name = document.getElementById('name').value;
      const email = document.getElementById('email').value;
      const message = document.getElementById('message').value;

      const feedback = `Thank you, ${name}! We have received your message.`;
      document.getElementById('formFeedback').innerText = feedback;

      // Clear form fields
      this.reset();
    });
  </script>
</body>
</html>
```

## Ekstraa

- HTML-validointi: https://validator.w3.org/
- CSS-validointi: https://jigsaw.w3.org/css-validator/

## Viitekehyksistä lyhyesti

### Mikä on viitekehys?
- **Viitekehys (Framework):** Valmiiksi rakennettu koodikokoelma ja rakenne, joka nopeuttaa ohjelmistojen kehittämistä.
- Miksi käyttää viitekehyksiä?
  - Säästää aikaa ja vähentää toistuvaa työtä.
  - Tarjoaa standardeja ja parhaita käytäntöjä.
  - Usein yhteisön tuki ja valmiit lisäosat.
- Jaottelu:
  - Frontend-viitekehykset (Käyttöliittymät).
  - Backend-viitekehykset (Palvelinpuolen logiikka).

### Frontend-viitekehykset
**1. React**
- Kehittäjä: Meta (Facebook).
- Miksi suosittu?
  - Komponenttipohjainen rakenne.
  - Virtuaalinen DOM takaa nopeuden.
  - Laaja ekosysteemi (esim. Next.js, React Native).
- Käyttökohteet: SPA:t, mobiilisovellukset.

**2. Vue.js**
- Kehittäjä: Evan You.
- Miksi suosittu?
  - Helppokäyttöinen ja kevyt.
  - Korkea suorituskyky ja kaksisuuntainen datan sitominen.
- Käyttökohteet: Keskikokoiset projektit, startupit.

**3. Angular**
- Kehittäjä: Google.
- Miksi suosittu?
  - Koko paketti: sisältää kaiken reitityksestä tilanhallintaan.
  - Hyvä tuki suurille projekteille.
- Käyttökohteet: Yritystasoiset sovellukset.

### Backend-viitekehykset
**1. Node.js ja Express.js**
- Miksi suosittu?
  - JavaScript toimii sekä frontendissä että backendissä.
  - Kevyt ja nopea.
  - Hyvä API-kehitykseen (REST, GraphQL).
- Käyttökohteet: Nopeat API:t, reaktiiviset sovellukset.

**2. Django (Python)**
- Miksi suosittu?
  - "Batteries included" -filosofia: sisältää kaiken tietokannoista autentikointiin.
  - Turvallisuus sisäänrakennettuna.
- Käyttökohteet: Tietokantapohjaiset sovellukset.

**3. Ruby on Rails**
- Miksi suosittu?
  - Helppo oppia ja tuottaa nopeasti tuloksia.
  - Hyvä yhteisö ja valmiit lisäosat (gems).
  - Käyttökohteet: Startup-sovellukset, verkkokaupat.

### Full-Stack-viitekehykset
**1. Next.js (React-pohjainen)**
- Miksi suosittu?
  - Server-side rendering (SSR) ja staattinen sivun luonti.
  - Erinomainen SEO-tuki.
- Käyttökohteet: Modernit verkkosovellukset.

**2. Nuxt.js (Vue-pohjainen)**
- Miksi suosittu?
  - Vue.js:n laajennus staattisten ja dynaamisten sovellusten rakentamiseen.
  - Sisäänrakennetut optimoinnit.
- Käyttökohteet: Universaalit sovellukset.

**3. Laravel (PHP)**
- Miksi suosittu?
  - Yksinkertainen syntaksi ja kattavat ominaisuudet.
  - Sisältää kaiken reitityksestä ORM:ään.
- Käyttökohteet: Verkkosivustot ja -sovellukset.

### Kuinka valita viitekehys?
1. Projektin vaatimukset
- SPA, PWA vai monoliittinen sovellus?
- Tarvitseeko staattista vai dynaamista renderöintiä?
2. Tiimin osaaminen
- Mitkä kielet ja teknologiat ovat tuttuja?
- Onko tarvetta oppia uutta nopeasti?
3. Skaalautuvuus ja tuki
- Onko viitekehyksellä vahva yhteisö ja dokumentaatio?
- Kuinka hyvin se skaalautuu tulevaisuuden tarpeisiin?
4. Yhteisön ja työkalujen tuki
- Käytettävissä olevat lisäosat, kirjastot ja integraatiot.
- Suosituimmat viitekehykset tarjoavat pitkän aikavälin vakauden.

