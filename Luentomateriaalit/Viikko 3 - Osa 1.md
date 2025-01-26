> HUOM!  Materiaalin laadinnassa hyödynnetty ChatGPT-tekoälysovellusta

# Staattiset ja dynaamiset web-sivustot

Staattisen ja dynaamisen web-sivuston erot asiakas- ja palvelinsuunnassa perustuvat niiden tapaan käsitellä ja toimittaa sisältöä käyttäjille. Seuraavassa vertailua.

## Asiakaspuoli (Client-Side)

### Staattinen web-sivusto:
- **Sisältö:** Sivuston sisältö on ennalta määritettyä ja pysyvää. Sama HTML, CSS ja JavaScript lähetetään kaikille käyttäjille sellaisenaan.
- **Interaktiivisuus:** Rajoitettu. Mahdolliset interaktiot (esim. animaatiot tai käyttäjän toiminnan perusteella muuttuva sisältö) toteutetaan pelkästään JavaScriptin avulla ilman palvelimen tukea.
- **Latausnopeus:** Staattiset sivustot latautuvat nopeammin, koska sisältö ei vaadi lisäkäsittelyä palvelimella.
- **Esimerkki:** Yksinkertaiset portfolio- tai yrityssivut, joissa sisältö ei muutu käyttäjän toiminnan perusteella.

### Dynaaminen web-sivusto:
- **Sisältö:** Sivuston sisältö voi muuttua käyttäjän toiminnan, ajan tai muiden muuttujien mukaan. Frontend voi ladata tietoa palvelimelta esimerkiksi **AJAX**-kutsujen avulla (REST API, GraphQL).
- **Interaktiivisuus:** Erittäin korkea. Käyttäjän toiminnan perusteella sisältö voi muuttua ilman koko sivun uudelleenlatausta.
- **Esimerkki:** Verkkokaupat, joissa tuotteet ja hinnat haetaan palvelimelta tai sovellukset, kuten sosiaalisen median alustat.

## Palvelinpuoli (Server-Side)

### Staattinen web-sivusto:
- **Sisällön luonti:** Sivut ovat valmiiksi luotuja tiedostoja (HTML, CSS, JavaScript), jotka palvelin vain lähettää asiakkaalle.
- **Palvelimen rooli:** Yksinkertainen. Palvelin toimii vain tiedostojen tarjoajana (esim. Nginx tai Azure Static Web Apps). Ei laskentaa tai logiikkaa.
- **Tietokanta:** Ei yleensä käytössä, koska sisältö on kiinteää eikä sitä tarvitse hakea tai muuttaa.
- **Skalautuvuus:** Erittäin hyvin skaalautuva, koska palvelimen ei tarvitse tehdä muuta kuin toimittaa staattisia tiedostoja.
- **Esimerkki:** GitHub Pages, jossa kaikki sisältö on suoraan tallennettu staattisina tiedostoina.

### Dynaaminen web-sivusto:
- **Sisällön luonti:** Sivut luodaan tai muokataan dynaamisesti palvelimella käyttäjän pyyntöjen perusteella. Esimerkiksi:
  - Backend-sovellus (Node.js, Python, PHP) hakee tietoa tietokannasta ja luo HTML:n "lennossa".
  - API:t palauttavat tietoa, jota frontend käyttää päivittääkseen sivustoa.
- **Palvelimen rooli:** Käsittelee käyttäjän pyyntöjä, suorittaa laskentaa, hakee tietoa tietokannoista ja voi muokata sisältöä ennen sen lähettämistä asiakkaalle.
- **Tietokanta:** Käytössä tietojen tallentamiseen ja hakemiseen (esim. käyttäjätiedot, tuotelistat).
- **Skalautuvuus:** Vaatii enemmän resursseja, koska jokainen pyyntö voi vaatia laskentaa ja tietokantahakuja. Skaalautuminen riippuu palvelimien suorituskyvystä ja optimoinnista.
- **Esimerkki:** WordPress-sivustot, verkkokaupat, sovellukset kuten Netflix.

## Yhteenveto eroista

| Ominaisuus                 | Staattinen web-sivusto                     | Dynaaminen web-sivusto                       |
|----------------------------|--------------------------------------------|---------------------------------------------|
| **Sisältö**                | Sama kaikille käyttäjille                 | Muuttuu käyttäjän toiminnan tai datan mukaan |
| **Palvelimen rooli**       | Tiedostojen tarjoaminen                   | Laskenta, tietokantahaun suorittaminen      |
| **Tietokanta**             | Ei tarvetta                              | Käytössä (esim. MySQL, MongoDB)            |
| **Interaktiivisuus**       | Rajoitettu                               | Korkea                                     |
| **Latausnopeus**           | Nopeampi                                 | Hitaampi, mutta kehittyneempi              |
| **Skalautuvuus**           | Erittäin hyvä                            | Raskaampi, vaatii optimointia              |
| **Käyttökohteet**          | Blogit, staattiset yrityssivut           | Verkkokaupat, sovellukset, interaktiiviset palvelut |

# PaaS-malli - Palvelinpuolen yksi toteutustapa

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

- **Hyöty**: Kehittäjä voi keskittyä sovelluksen toiminnallisuuteen ilman infrastruktuurin hallintaa.

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