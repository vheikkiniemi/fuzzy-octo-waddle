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
