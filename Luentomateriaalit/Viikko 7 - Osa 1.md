> HUOM!  Materiaalin laadinnassa hyödynnetty ChatGPT-tekoälysovellusta

# Sovellusten testaaminen

## 1. Testauksen historia
Ohjelmistotestauksen historia ulottuu 1940–50-luvuille, jolloin tietokoneet alkoivat kehittyä. Aluksi testaus oli manuaalista ja keskittyi yksittäisten ohjelmien virheiden löytämiseen. 1970-luvulla vesiputousmalli yleistyi, ja testaus tapahtui vasta kehityksen loppuvaiheessa.

1990-luvulla ketterät menetelmät (Agile) muuttivat testauksen osaksi jatkuvaa kehitystä (Continuous Integration, CI). Nykyisin testaus on automatisoitua, ja siihen käytetään monipuolisia työkaluja, kuten [`Jest`](https://jestjs.io/), [`Vitest`](https://vitest.dev/), [`Cypress`](https://www.cypress.io/), [`Playwright`](https://playwright.dev/) ja [`k6`](https://k6.io/).

## 2. Testauksen tärkeys
Testaus varmistaa, että ohjelmisto toimii odotetusti ja on:
- **Luotettava** – Käyttäjät voivat luottaa sovelluksen toimintaan.
- **Suorituskykyinen** – Sovellus kestää suuren käyttäjämäärän.
- **Turvallinen** – Tietoturvahaavoittuvuudet havaitaan ennen julkaisua.
- **Kehityksen kannalta tehokas** – Virheet havaitaan aikaisessa vaiheessa, mikä vähentää kustannuksia.

## 3. Testausmenetelmät
Testausmenetelmä tarkoittaa tapaa, jolla ohjelmiston toiminnallisuus, suorituskyky ja luotettavuus varmistetaan. Testausmenetelmät voidaan jakaa seuraaviin kategorioihin:

### 3.1. Staattinen testaus (Static Testing)
- Koodi tarkistetaan ilman sen suorittamista.
- Esimerkkejä:
  - **Koodikatselmointi (Code Review)**
  - **Linters (esim. ESLint, Prettier)**
  - **Staattinen analyysi (esim. SonarQube, CodeQL)**

### 3.2. Dynaaminen testaus (Dynamic Testing)
- Ohjelmaa suoritetaan ja sen toiminta tarkistetaan.
- Tähän kuuluvat:
  - **Yksikkötestaus** (Jest, Mocha)
  - **Integraatiotestaus** (React Testing Library)
  - **End-to-End (E2E) -testaus** (Playwright, Cypress)
  - **Kuormitustestaus** (k6, JMeter)

### 3.3. Manuaalinen testaus
- Testaaja suorittaa testit ilman automaatiota.
- Käytetään erityisesti käyttöliittymä- ja käytettävyystesteissä.

### 3.4. Automaattinen testaus
- Testit suoritetaan ilman ihmisen väliintuloa testikirjastoilla ja -työkaluilla.
- Tämä kattaa automatisoidut:
  - **Yksikkötestit** (Jest, Vitest)
  - **Integraatiotestit** (RTL, Jest)
  - **E2E-testit** (Playwright, Cypress)
  - **Kuormitustestit** (k6, JMeter)

## 4. Nykyiset testausmenetelmät
Nykyisessä ohjelmistokehityksessä testaus jaetaan yleensä seuraaviin kategorioihin:

| Testityyppi        | Edustama testausmenetelmä | Tyypilliset työkalut |
|--------------------|--------------------------|----------------------|
| Yksikkötestaus    | Dynaaminen, automaattinen | Jest, Vitest, Mocha |
| Integraatiotestaus | Dynaaminen, automaattinen | Jest, React Testing Library |
| End-to-End (E2E) -testaus | Dynaaminen, automaattinen | Playwright, Cypress, Selenium |
| Kuormitustestaus   | Dynaaminen, automaattinen | k6, JMeter |
| Turvallisuustestaus | Dynaaminen, automaattinen | ZAP, Burp Suite |

## 5. Käytännön esimerkit

### 5.1. Yksikkötestaus (Unit Testing) – React & Vitest

Yksikkötestaus tarkistaa yksittäisten komponenttien toiminnan. Se on nopea ja tehokas tapa havaita virheet ennen kuin ne leviävät muihin osiin järjestelmää.

Ennen testauksen aloittamista tulee olla luonnollisesti React-sovellus, joka voidaan tehdä seuraavasti. Voit käyttää olemassa olevaa sovellusta, jos haluat.
```jsx
npm create vite@latest myapp -- --template react
cd myapp
npm install
npm run dev
```

Ennen testauksen aloittamista tulee asentaa tarvittavat moduulit (Tämä tehdään React-sovelluksen juurkansiossa):
```jsx
npm install --save-dev vitest @testing-library/react @testing-library/jest-dom
```

Muokataan (tai luodaan) tiedosto <code>vitest.config.js</code>
```jsx
import { defineConfig } from 'vitest/config';

export default defineConfig({
  test: {
    environment: 'jsdom',
    globals: true,
    setupFiles: './vitest.setup.js',
  },
});
```

Muokataan (tai luodaan) tiedosto <code>vitest.setup.js</code>
```jsx
import '@testing-library/jest-dom';
```

Muokataan (tai luodaan) komponenttitiedosto <code>MyComponent.jsx</code>
```jsx
import React from 'react';

const MyComponent = () => {
  return <div>Hello, World!</div>;
};

export default MyComponent;
```

Muokataan (tai luodaan) komponentin testitiedosto <code>MyComponent.test.jsx</code>
```jsx
import React from "react";
import { render, screen } from '@testing-library/react';
import MyComponent from './MyComponent';

test('renders Hello, World!', () => {
  render(<MyComponent />);
  const element = screen.getByText(/Hello, World!/i);
  expect(element).toBeInTheDocument();
});
```

Ajetaan testi seuraavalla komennolla
```jsx
npx vitest
```

Esimerkki Counter-komponentista, joka kasvattaa numeroa napin painalluksella. Muokataan (tai luodaan) komponenttitiedosto <code>Counter.jsx</code>

```jsx
import React from "react";
import { useState } from "react";

const Counter = () => {
  const [count, setCount] = useState(0);

  return (
    <div>
      <p>Count: {count}</p>
      <button onClick={() => setCount(count + 1)}>Increase</button>
    </div>
  );
};

export default Counter;
```

Muokataan (tai luodaan) komponentin testitiedosto <code>Counter.test.jsx</code>
```jsx
import React from "react";
import { render, screen, fireEvent } from '@testing-library/react';
import Counter from './Counter';

test('näyttää oikean alkulukeman', () => {
    render(<Counter />);
    expect(screen.getByText("Count: 0")).toBeInTheDocument();
});

test('kasvattaa lukemaa, kun nappia painetaan', () => {
    render(<Counter />);

    // Jos useampi nappi löytyy, valitaan ensimmäinen
    const button = screen.getAllByRole("button", { name: "Increase" })[0];

    fireEvent.click(button);
    expect(screen.getByText("Count: 1")).toBeInTheDocument();
});
```

Ajetaan testi seuraavalla komennolla
```jsx
npx vitest
```

### 5.2. End-to-End (E2E) -testaus – Playwright

Testataan kirjautumistoimintoa Playwrightilla.

**login.spec.js**
```javascript
import { test, expect } from "@playwright/test";

test("kirjautuminen onnistuu oikeilla tiedoilla", async ({ page }) => {
  await page.goto("https://example.com/login");
  await page.fill("input[name=username]", "testikäyttäjä");
  await page.fill("input[name=password]", "salasana123");
  await page.click("button[type=submit]");
  await expect(page).toHaveURL("https://example.com/dashboard");
});
```

### 5.3. Kuormitustestaus – k6

Simuloidaan 50 käyttäjää, jotka tekevät HTTP-pyyntöjä API:lle.

**test.js**
```javascript
import http from "k6/http";
import { check, sleep } from "k6";

export let options = {
  stages: [
    { duration: "30s", target: 50 },
    { duration: "1m", target: 50 },
    { duration: "10s", target: 0 },
  ],
};

export default function () {
  let res = http.get("https://yourapi.com/data");

  check(res, {
    "status is 200": (r) => r.status === 200,
    "response time is < 500ms": (r) => r.timings.duration < 500,
  });

  sleep(1);
}
```

## 6. Testauksen Tulevaisuus
- **AI-pohjainen testaus** – AI auttaa löytämään testitapauksia automaattisesti.
- **Fuzzing ja turvallisuustestaus** – Yhä enemmän testausta automatisoidaan tietoturvahaavoittuvuuksien löytämiseksi.
- **Jatkuva testaus (Continuous Testing)** – Testaus integroituu DevOps-pipelineihin entistä paremmin.

## 7. Yhteenveto
| Testityyppi        | Esimerkkityökalu | Käyttötarkoitus |
|--------------------|----------------|----------------|
| Yksikkötestaus    | Jest | Testaa yksittäisiä komponentteja |
| E2E-testaus       | Playwright | Testaa koko sovelluksen käyttäjän näkökulmasta |
| Kuormitustestaus  | k6 | Mittaa sovelluksen suorituskykyä |

Testaus on kriittinen osa ohjelmistokehitystä ja kehittyy jatkuvasti automaation ja AI:n myötä.
