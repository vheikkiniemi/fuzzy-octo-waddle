> HUOM!  Materiaalin laadinnassa hyödynnetty ChatGPT-tekoälysovellusta

# HTML, CSS ja JavaScript - PaaS-malli

## Johdanto PaaS-malliin
- Määritelmä: `Platform as a Service (PaaS)` tarjoaa kehittäjille alustan sovellusten kehittämiseen, julkaisemiseen ja hallintaan ilman tarvetta hallita infrastruktuuria.
- Keskeiset ominaisuudet:
  - Infrastruktuuri (palvelimet, verkot, tallennus) on abstrahoitu kehittäjältä.
  - Tuki monille ohjelmointikielille ja kehyksille.
  - Sisäänrakennettu skaalaus, tietoturva ja CI/CD-tuki.
- PaaS-palveluiden esimerkkejä:
  - Microsoft: `Azure App Service`, `Azure Static Web Apps`, `Azure Functions`
  - Amazon Web Services (AWS): `AWS Elastic Beanstalk`, `AWS Lambda`
  - Google Cloud: `Google App Engine`, `Cloud Functions`
  - Heroku: Sovelluskehitys ja julkaisu.

##  Web-sovelluksen suunnittelu PaaS-mallilla
- Vaiheet suunnittelussa:
    1. Sovelluksen vaatimukset:
        - Valitse ohjelmointikieli ja teknologiat.
        - Määrittele tarvittavat ominaisuudet ja tietokantatarpeet.
    2. Valitse sopiva PaaS-alusta:
        - Staattiset sovellukset: `Azure Static Web Apps`, `AWS Amplify`, `Google Firebase Hosting`.
        - Dynaamiset sovellukset: `Azure App Service`, `Google App Engine`, `Heroku`.
    3. Tietoturva:
        - Hyödynnä PaaS-palveluiden sisäänrakennettu HTTPS ja autentikointiratkaisut (esim. `Azure Active Directory`, `AWS Cognito`, `Firebase Authentication`).

- Hyöty: Kehittäjä voi keskittyä sovelluksen toiminnallisuuteen ilman infrastruktuurin hallintaa.

##  Sovelluksen kehitys ja CI/CD-prosessi
- Kehitysvaihe:
  - Koodin kirjoittaminen ja paikallinen testaus (esim. `Visual Studio Code`).
  - Hyödynnä PaaS-alustojen ominaisuuksia, kuten tukea useille käyttöympäristömuuttujille.
- CI/CD-putki:
  - Versionhallinta: GitHub, GitLab, Bitbucket.
  - Julkaisuprosessin automatisointi:
    - `Azure Static Web Apps`: Sisäänrakennettu GitHub Actions -integraatio.
    - `AWS Elastic Beanstalk`: Pipeline-tuki AWS CodePipelinella.
    - `Google App Engine`: Yhdistä Cloud Build -pipelinella.
    - `Heroku`: Git-push -pohjainen julkaisu.
- **Hyöty**: Päivitykset julkaistaan automaattisesti, mikä nopeuttaa kehityssykliä.

##  Sovelluksen julkaisu PaaS-alustalla
- Käyttöönoton vaiheet:
    1. Luo PaaS-resurssi (esim. `Azure Static Web App`, `AWS Amplify` tai `Google Firebase Hosting`).
    2. Konfiguroi sovelluksen asetukset, kuten domainit, ympäristömuuttujat ja tietoturva-asetukset.
    3. Julkaise sovellus suoraan käyttämällä GitHub Actionsia, AWS CodePipelinea tai vastaavaa.
- Esimerkki:
  - HTML/CSS/JS-sivuston julkaisu Azure Static Web Appsilla osoitteeseen: `https://mywebapp.staticweb.app`
  - Vaihtoehtoisesti AWS Amplifylla tai Firebase Hostingilla.
- **Hyöty**: Nopeasti skaalautuva, valmis alusta isännöintiä varten.

##  Ylläpito ja optimointi
- Sovelluksen monitorointi:
  - `Azure Monitor`, `AWS CloudWatch` ja `Google Cloud Monitoring` tarjoavat tietoa sovelluksen suorituskyvystä ja käyttäjädatan analysoinnista.
- Skaalautuvuus:
  - `Azure App Service`, `AWS Elastic Beanstalk` ja `Google App Engine` tukevat automaattista skaalautumista käyttäjämäärien mukaan.
- Kustannusten optimointi:
  - Hyödynnä oikea palvelutasosuunnitelma (esim. Free, Basic, Premium).
- Tietoturva:
  - Pidä sovellus ja sen riippuvuudet ajan tasalla.
  - Integroi mukautettu domain ja SSL.

# Käyttötapaus: Azure Static Web App

> Azure Static Web Apps on erinomainen esimerkki `Platform as a Service (PaaS) `-mallista. PaaS tarjoaa kehittäjille alustaratkaisun, jossa he voivat keskittyä sovelluksen koodiin ja toiminnallisuuteen ilman, että heidän tarvitsee huolehtia infrastruktuurin ylläpidosta, kuten palvelimista, verkkoasetuksista tai kuormituksenhallinnasta.

## Miksi Azure Static Web Apps on PaaS?
1. Palvelinratkaisun hallinta automatisoitu:
    - Sinun ei tarvitse pystyttää palvelimia, asentaa ohjelmistoja tai määrittää ympäristöjä. Azure hoitaa taustalla kaiken isännöintiin liittyvän.
2. Sisäänrakennettu CI/CD-tuki:
    - Azure Static Web Apps integroituu suoraan GitHubiin tai Azure DevOpsiin. Koodin muutokset voidaan julkaista automaattisesti, mikä on tyypillistä PaaS-malleille.
3. Käyttäjäystävällinen resurssien hallinta:
    - Skaalaus, suorituskyvyn optimointi ja turvallisuus (HTTPS) hoituvat ilman manuaalista konfigurointia.
4. Tuki moderneille web-sovelluksille:
    - Azure Static Web Apps isännöi staattisia tiedostoja (HTML, CSS, JavaScript) ja tukee samalla dynaamisia ominaisuuksia, kuten API-yhteyksiä (Azure Functions).

## Azure Static Web Apps vs. Muita Pilvipalvelumalleja
1. Infrastructure as a Service (IaaS):
    - Jos käyttäisit IaaS-mallia, kuten Azure Virtual Machines, sinun pitäisi pystyttää oma palvelin ja hallita sitä itse. Tämä on monimutkaisempaa ja vaatii enemmän ylläpitoa.
    - Static Web Apps yksinkertaistaa tätä poistamalla palvelintason hallinnan tarpeen.
2. Software as a Service (SaaS):
    - SaaS tarjoaa valmiita ohjelmistoratkaisuja (esim. Office 365), joita voi käyttää ilman kehitystyötä.
    - Static Web Apps ei ole SaaS, koska se ei ole valmis sovellus, vaan alusta, joka mahdollistaa omien sovellusten kehittämisen ja isännöinnin.
3. Platform as a Service (PaaS):
    - PaaS mahdollistaa sovelluksen kehittämisen, käyttöönoton ja ylläpidon ilman tarvetta hallita infrastruktuuria.
    - Azure Static Web Apps kuuluu tähän kategoriaan, koska se tarjoaa valmiin ympäristön koodin isännöintiin ja automaattiseen julkaisuprosessiin.

## Yhteenveto Azure Static Web Appsista
- Azure Static Web Apps on osa PaaS-mallia, koska:
  - Se hallitsee automaattisesti infrastruktuuria.
  - Se tarjoaa kehittäjäystävällisen ja nopean tavan julkaista sovelluksia.
  - Se tukee sisäänrakennettuja ominaisuuksia, kuten CI/CD, HTTPS ja API-yhteydet ilman ylimääräistä konfiguraatiota.

## Sivuston käyttöönotto

> **Kehote (ChatGPT):** Kerrotko vaiheet joita tarvitaan, kun sivusto otetaan käyttöön Azure Static Web Apps -ympäristössä. Minulla on html-tiedosto olemassa.

> **Vastaus:** Tässä ovat vaiheet, joiden avulla voit ottaa HTML-sivustosi käyttöön Azure Static Web Apps -ympäristössä. Prosessi on helppo ja suoraviivainen.

### 1. Luo Azure-tili
Jos sinulla ei ole vielä Azure-tiliä:
1. Siirry [Azure-portaaliin](https://azure.microsoft.com/).
2. Luo maksuton tili, jos sinulla ei vielä ole sellaista. `HUOM! Centrian opiskelijoille tili on olemassa valmiina. Voit halutessa käyttää sitä.`

### 2. Valmistele HTML-sivusto
1. Varmista, että kaikki tiedostot ovat yhdessä kansiossa:
```
/projekti
├── index.html
├── styles.css (valinnainen)
└── script.js (valinnainen)
```
2. Tarkista, että index.html on kotisivun tiedosto.

### 3. Lataa Azure Static Web Apps -laajennus VS Codeen
1. Avaa Visual Studio Code.
2. Asenna Azure Static Web Apps -laajennus `Huom! Luennoilla käytetään Azure App Service -laajennusta`:
    - Avaa laajennusten hallinta (Ctrl+Shift+X).
    - Etsi Azure Static Web Apps ja asenna se.

### 4. Luo uusi Azure Static Web App
1. Kirjaudu sisään Azuren tilillesi Visual Studio Codessa:
    - Klikkaa oikean alakulman Azure: Sign In -linkkiä.
2. Avaa Azure Static Web Apps -näkymä VS Codessa.
3. Klikkaa + (luo uusi Static Web App).
4. Seuraa näitä ohjeita:
    - Anna sovellukselle nimi (esim. MyStaticSite).
    - Valitse resurssiryhmä tai luo uusi.
    - Valitse Free Plan testikäyttöön.
    - Anna julkaisulähteeksi kansio, jossa HTML-tiedostosi sijaitsevat.

### 5. Julkaise HTML-sivusto
1. Valitse projektikansio, jossa HTML-tiedostosi ovat.
2. Azure Static Web Apps luo automaattisesti CI/CD-pipeline-prosessin (jos käytät GitHubia `Huom! Käytämme oletuksena GitHubia`). Jos et käytä GitHubia:
    - Azure kopioi tiedostosi suoraan ja ottaa käyttöön staattisen web-sivuston.
3. Julkaisun jälkeen saat linkin sivustoon, esimerkiksi: `https://polished-mountain-12345.azurestaticapps.net`

### 6. Testaa ja tarkista
1. Avaa linkki selaimessa.
2. Varmista, että kaikki tiedostot ja tyylit toimivat odotetusti.

### 7. Valinnaiset lisäasetukset
1. Mukautettu domain:
    - Voit lisätä mukautetun domainin (esim. www.omaosoite.fi) Azure-portaalissa.
2. HTTPS:
    - Azure Static Web Apps tarjoaa automaattisesti HTTPS-suojauksen.
3. API-integraatio (valinnainen):
    - Voit lisätä dynaamisia ominaisuuksia hyödyntämällä Azure Functionsia.

### 8. Päivitysten tekeminen
1. Jos muutat HTML-tiedostojasi:
    - Avaa projekti Visual Studio Codessa.
    - Klikkaa Deploy to Static Web App uudelleen.
2. Päivitykset tulevat näkyviin automaattisesti.

### Yhteenveto
- Azure Static Web Apps sopii täydellisesti HTML-sivuston isännöintiin ilman monimutkaista infrastruktuurin hallintaa.
- Julkaisu on nopeaa ja tarjoaa heti skaalautuvan ja turvallisen ympäristön.