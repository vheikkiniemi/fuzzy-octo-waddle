> HUOM!  Materiaalin laadinnassa hyödynnetty ChatGPT-tekoälysovellusta

# Johdanto Reactiin

## Mikä on React?

[`React`](https://react.dev/) on Facebookin (nykyisin Meta) kehittämä avoimen lähdekoodin JavaScript-kirjasto, joka on suunniteltu erityisesti verkkosovellusten rakennusosien eli komponenttien luomiseen. Reactin avulla kehittäjät voivat rakentaa uudelleenkäytettäviä, tehokkaita ja reaktiivisia käyttöliittymiä (UI) verkkosovelluksille.

## Historia

React julkaistiin vuonna 2013, kun Facebook kehitti sen sisäiseen käyttöön ratkaisemaan monimutkaisten käyttöliittymien hallintaan liittyviä ongelmia. Sen suosio kasvoi nopeasti, ja nykyisin Reactia käytetään laajasti niin startupeissa kuin suurissa teknologiayrityksissäkin.

## Yhteydet muihin tekniikoihin

React ei ole itsessään `full-stack` -ratkaisu, vaan se keskittyy vain käyttöliittymien rakentamiseen. Usein sitä käytetään yhdessä seuraavien teknologioiden kanssa:
- **Node.js ja Express**: Palvelinpuolen logiikka ja API:t
- **Redux tai Zustand**: Tilanhallinta suurissa sovelluksissa
- **Next.js**: React-sovellusten palvelinpuolen renderöinti (SSR) ja staattinen sivujen generointi (SSG)
- **TypeScript**: Parempi tyyppiturvallisuus ja kehityskokemus

## Esimerkkikäyttökohteita
Reactia käytetään laajasti monissa eri sovelluksissa, esimerkiksi:
- **Facebook**: Alun perin React kehitettiin Facebookin tarpeisiin.
- **Instagram**: React-komponentteihin pohjautuva käyttöliittymä.
- **Netflix**: Parempi suorituskyky ja kehitystyökalut.
- **Airbnb**: Modulaarinen ja uudelleenkäytettävät komponentit.

## Plussat ja miinukset

### Plussat
- ✅ Nopea ja tehokas: Virtuaalinen DOM optimoi päivitykset ja tekee Reactista nopean.
- ✅ Komponenttipohjainen arkkitehtuuri: Helppo uudelleenkäyttää ja ylläpitää koodia.
- ✅ Yhteisö ja ekosysteemi: Laaja tuki, dokumentaatio ja kolmannen osapuolen kirjastot.
- ✅ Hyvä kehityskokemus: Hot-reloading ja tehokkaat kehitystyökalut.

### Miinukset
- ❌ Jyrkkä oppimiskäyrä: JSX, hookit ja tilanhallinta voivat olla alussa haastavia.
- ❌ SEO-haasteet: Palvelinpuolen renderöinti voi olla tarpeen SEO-optimointiin.
- ❌ Nopea kehitys: Muutokset ja uudet ominaisuudet voivat vaatia jatkuvaa opiskelua.

# Reactin Perusteet

## Ensimmäinen React-komponentti
React-sovellus rakentuu komponenteista. Alla on esimerkki yksinkertaisesta React-komponentista:
```javascript
function Tervehdys() {
  return <h1>Hei, tervetuloa React-maailmaan!</h1>;
}
```

Komponentteja voi käyttää muissa komponenteissa seuraavasti:
```javascript
function App() {
  return (
    <div>
      <Tervehdys />
    </div>
  );
}
```

## JSX – JavaScript XML
[`Reactin JSX`](https://react.dev/learn/writing-markup-with-jsx) on erikoissyntaksi, joka muistuttaa HTML:ää mutta toimii JavaScriptin sisälllä:
```javascript
const elementti = <h1>Hei maailma!</h1>;
```

JSX muunnetaan JavaScriptiksi käyttäen Babel-kääntäjää:
```javascript
const elementti = React.createElement("h1", null, "Hei maailma!");
```

## Tilanhallinta (State)
Reactin tilanhallinnan avulla voidaan muuttaa komponentin tilaa dynaamisesti.
```javascript
import { useState } from 'react';

function Klikkauslaskuri() {
  const [laskuri, setLaskuri] = useState(0);

  return (
    <div>
      <p>Napautettu {laskuri} kertaa</p>
      <button onClick={() => setLaskuri(laskuri + 1)}>Klikkaa minua</button>
    </div>
  );
}
```

# Visual Studio Code ja React-sovelluksen toteuttaminen

Ennen kuin aloitat ensimmäisen React-sovelluksesi, tee seuraavat valmistelut Visual Studio Codessa:
1. Asenna Node.js: Lataa ja asenna Node.js, joka sisältää myös npm:n (Node Package Manager).
2. Asenna VS Code ja tarvittavat laajennukset: Suositeltavia laajennuksia ovat:
    - `ES7+ React/Redux/React-Native snippets`
    - `Prettier - Code formatter`
    - `Live Server`
3. Luo uusi projekti Viten avulla: Avaa VS Code ja suorita seuraava komento päätelaitteessa:
    ```javascript
    npm create vite@latest my-app -- --template react
    ```
    Tämä luo uuden React-projektin nimeltä `my-app` käyttäen Viteä, joka on nopeampi vaihtoehto create-react-appille.

4. Siirry projektikansioon ja asenna riippuvuudet:
    ```javascript
    cd my-app
    npm install
    ```
5. Käynnistä kehityspalvelin:
    ```javascript
    npm run dev
    ```
    Tämä avaa React-sovelluksen selaimessa osoitteessa http://localhost:5173.

## Esimerkkisovellus: Yksinkertainen verkkosivu CSS:llä

Tässä on yksinkertainen esimerkki React-sivusta, joka käyttää myös CSS:ää.

1. Luo **`src/App.jsx`** tiedosto:
    ```javascript
    import './App.css';

    function App() {
    return (
        <div className="container">
        <h1>Tervetuloa React-sivulle!</h1>
        <p>Tämä on yksinkertainen React-sivu, jossa käytetään CSS:ää.</p>
        </div>
    );
    }

    export default App;
    ```

2. Luo **`src/App.css`** tiedosto:
    ```css
    .container {
    text-align: center;
    margin-top: 50px;
    }

    h1 {
    color: blue;
    }

    p {
    font-size: 18px;
    }
    ```

3. Käynnistä sovellus &rarr; Aja kehityspalvelin uudelleen komennolla:
    ```
    npm run dev
    ```
    Sivusi näkyy selaimessa osoitteessa http://localhost:5173, ja sen pitäisi näyttää tyylitelty tervehdysteksti.

# Hyvää taustamateriaalia
- [Full Stack open](https://fullstackopen.com/#course-contents)
- [Full Stack open &rarr; Reactin alkeet](https://fullstackopen.com/osa1/reactin_alkeet)