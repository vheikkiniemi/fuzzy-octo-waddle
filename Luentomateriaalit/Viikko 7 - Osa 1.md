> HUOM!  Materiaalin laadinnassa hyödynnetty ChatGPT-tekoälysovellusta

# Sovellusten testaaminen

## Testauksen historia
Ohjelmistotestauksen historia ulottuu 1940–50-luvuille, jolloin tietokoneet alkoivat kehittyä. Aluksi testaus oli manuaalista ja keskittyi yksittäisten ohjelmien virheiden löytämiseen. 1970-luvulla vesiputousmalli yleistyi, ja testaus tapahtui vasta kehityksen loppuvaiheessa.

1990-luvulla ketterät menetelmät (Agile) muuttivat testauksen osaksi jatkuvaa kehitystä (Continuous Integration, CI). Nykyisin testaus on automatisoitua, ja siihen käytetään monipuolisia työkaluja, kuten [`Jest`](https://jestjs.io/), [`Vitest`](https://vitest.dev/), [`Cypress`](https://www.cypress.io/), [`Playwright`](https://playwright.dev/) ja [`k6`](https://k6.io/).

## Testauksen tärkeys
Testaus varmistaa, että ohjelmisto toimii odotetusti ja on:
- **Luotettava** – Käyttäjät voivat luottaa sovelluksen toimintaan.
- **Suorituskykyinen** – Sovellus kestää suuren käyttäjämäärän.
- **Turvallinen** – Tietoturvahaavoittuvuudet havaitaan ennen julkaisua.
- **Kehityksen kannalta tehokas** – Virheet havaitaan aikaisessa vaiheessa, mikä vähentää kustannuksia.

## Testausmenetelmät
Testausmenetelmä tarkoittaa tapaa, jolla ohjelmiston toiminnallisuus, suorituskyky ja luotettavuus varmistetaan. Testausmenetelmät voidaan jakaa seuraaviin kategorioihin:

### Staattinen testaus (Static Testing)
- Koodi tarkistetaan ilman sen suorittamista.
- Esimerkkejä:
  - **Koodikatselmointi (Code Review)**
  - **Linters (esim. ESLint, Prettier)**
  - **Staattinen analyysi (esim. SonarQube, CodeQL)**

### Dynaaminen testaus (Dynamic Testing)
- Ohjelmaa suoritetaan ja sen toiminta tarkistetaan.
- Tähän kuuluvat:
  - **Yksikkötestaus** (Jest, Mocha)
  - **Integraatiotestaus** (React Testing Library)
  - **End-to-End (E2E) -testaus** (Playwright, Cypress)
  - **Kuormitustestaus** (k6, JMeter)

### Manuaalinen testaus
- Testaaja suorittaa testit ilman automaatiota.
- Käytetään erityisesti käyttöliittymä- ja käytettävyystesteissä.

### Automaattinen testaus
- Testit suoritetaan ilman ihmisen väliintuloa testikirjastoilla ja -työkaluilla.
- Tämä kattaa automatisoidut:
  - **Yksikkötestit** (Jest, Vitest)
  - **Integraatiotestit** (RTL, Jest)
  - **E2E-testit** (Playwright, Cypress)
  - **Kuormitustestit** (k6, JMeter)

## Nykyiset testausmenetelmät
Nykyisessä ohjelmistokehityksessä testaus jaetaan yleensä seuraaviin kategorioihin:

| Testityyppi        | Edustama testausmenetelmä | Tyypilliset työkalut |
|--------------------|--------------------------|----------------------|
| Yksikkötestaus    | Dynaaminen, automaattinen | Jest, Vitest, Mocha |
| Integraatiotestaus | Dynaaminen, automaattinen | Jest, React Testing Library |
| End-to-End (E2E) -testaus | Dynaaminen, automaattinen | Playwright, Cypress, Selenium |
| Kuormitustestaus   | Dynaaminen, automaattinen | k6, JMeter |
| Turvallisuustestaus | Dynaaminen, automaattinen | ZAP, Burp Suite |

## Käytännön esimerkit testauksesta

### Yksikkötestaus (Unit Testing) – React & Vitest

Yksikkötestaus tarkistaa yksittäisten komponenttien toiminnan. Se on nopea ja tehokas tapa havaita virheet ennen kuin ne leviävät muihin osiin järjestelmää.

Ennen testauksen aloittamista tulee olla luonnollisesti React-sovellus, joka voidaan tehdä seuraavasti. Voit käyttää olemassa olevaa sovellusta, jos haluat.
```jsx
npm create vite@latest myapp -- --template react
cd myapp
npm install
```

Testaa sovelluksen toiminta
```jsx
npm run dev
```

Ennen testauksen aloittamista tulee asentaa tarvittavat moduulit (Tämä tehdään React-sovelluksen juurkansiossa):
```jsx
npm install --save-dev vitest @testing-library/react @testing-library/jest-dom jsdom
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

**Yksikkötestaamisella** on suora yhteys ohjelman suunnitteluun. Meidän tulee tietää, että millaisia komponentteja sovellukseemme haluamme ja miten niitä testataan. Kun tiedämme komponentin toiminnan, helpotamme ja nopeutamme kokonaisen sovelluksen rakentamista. Testauksen kautta voimme olla varmoja, että miten joku komponentti toimii ja näin tiedämme, että miten ja mihin voimme osaksi sovellusta liittää. 

### End-to-End (E2E) -testaus – Playwright

E2E-testauksen ideana on testata sovellusta asiakkaan näkymästä. Testi voidaan tehdä mistä vain eli ei pelkästään kehitysympäristöstä. E2E-testauksessa voidaan mm. simuloida tilannetta, jossa asiakas tekee sivulla toimen, jonka seurauksena pitäisi tapahtua jotain.

Ennen testauksen aloittamista tulee asentaa tarvittavat moduulit (Tämä tehdään React-sovelluksen juurkansiossa):
```jsx
npm install -D @playwright/test
```

Asennetaan selainmoottori
```jsx
npx playwright install
```

Testitiedosto voidaan nauhoittaa, jolloin nauhoitus käynnistetään seuraavalla komennolla (tämä optio).
```jsx
npx playwright codegen
```
#### **Testin vaiheet**
1. Tehdään <code>test</code>-kansio React-projektin juureen.
    > **HUOM!** React-projekti voi olla pelkästään luotu testaukseen eli testataan jossain muussa ympäristössä olevaa.
    > Tässä tapauksessa testattava sovellus on samassa ympäristössä (osoitteessa `localhost`)
2. Tehdään `test`-kansioon tiedosto `Example.spec.ts`
    ```jsx
    import { test, expect } from '@playwright/test';

    const appAddress = 'http://localhost:5173'

    test('The app should display the title', async ({ page }) => {
        // opening the page
        await page.goto(appAddress);
        // Check that the main title is found
        await expect(page.locator('h1')).toHaveText('User Management App');
        // Test run can be interrupted if started with --headed
        await page.pause();
    });
    ```
3. Ajetaan testi komennolla (ei käynnistä selainta)
    ```
    npx playwright test
    ```
    Tällä komennolla selain aukee ja testi pysähtyy kohtaan `page.pause()`
    ```
    npx playwright test --headed
    ```

> **Lisätietoja: [`Playwright`](https://playwright.dev/)**

**Toiminnalisuuksien testaus**

```jsx
import { test, expect } from '@playwright/test';

const appAddress = 'http://localhost:5173'

test('Adding feeds to a list', async ({ page }) => {
    // Random strings are generated
    const name = (Math.random() + 1).toString(36).substring(7);
    const email = name + '@' + (Math.random() + 1).toString(36).substring(7) + '.io';
    // Opening the page
    await page.goto(appAddress);

    // These are linked to the content of the page
    // Here the values of the fields on the page are filled
    await page.fill("input#formName", name);
    await page.fill("input#formEmail", email);
    // Press the button
    await page.click('button:has-text("Create")');
    // Wait for at least one user to appear in the list
    await page.waitForSelector('.list-group-item');
    // Select the last user in the list and confirm its text
    const lastUser = page.locator('.list-group-item').last();
    await expect(lastUser).toHaveText(`${name} (${email})`);
});
```

**E2E**-testauksella on tärkeä rooli, koska testaus perustuu asiakkaan näkymään. Tällä on taas heijastus siihen, että voidaan toteuttaa sovellus perustuen asiakkaan tarpeisiin ja testataan tarpeen täyttyminen heti. Ajatuksena, että tehdään ensiksi testi, jolla tarve voidaan testata ja sitten vasta itse sovelluksen toiminallisuus. Katso: [`Test-driven development (TDD)`](https://developer.ibm.com/articles/5-steps-of-test-driven-development/)

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

## Testauksen Tulevaisuus
- **AI-pohjainen testaus** – AI auttaa löytämään testitapauksia automaattisesti.
- **Fuzzing ja turvallisuustestaus** – Yhä enemmän testausta automatisoidaan tietoturvahaavoittuvuuksien löytämiseksi.
- **Jatkuva testaus (Continuous Testing)** – Testaus integroituu DevOps-pipelineihin entistä paremmin.

## Yhteenveto
| Testityyppi        | Esimerkkityökalu | Käyttötarkoitus |
|--------------------|----------------|----------------|
| Yksikkötestaus    | Jest | Testaa yksittäisiä komponentteja |
| E2E-testaus       | Playwright | Testaa koko sovelluksen käyttäjän näkökulmasta |
| Kuormitustestaus  | k6 | Mittaa sovelluksen suorituskykyä |

Testaus on kriittinen osa ohjelmistokehitystä ja kehittyy jatkuvasti automaation ja AI:n myötä.
