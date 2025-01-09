> **HUOM!**  Materiaalin laadinnassa hyödynnetty ChatGPT-tekoälysovellusta

> [!IMPORTANT] 
> TÄMÄ TEKEYTYY

# HTML, CSS ja JavaScript - On-Premise ja Cloud VM

## Johdanto HTTP-protokollaan

### HTTP
- HTTP (HyperText Transfer Protocol) on sovelluskerroksen protokolla, jota käytetään tiedon siirtoon verkkosovelluksissa.
- Kehitetty erityisesti World Wide Webin käyttöön.
- Stateless: Jokainen pyyntö on itsenäinen.

### HTTP:n Perusperiaatteet
- Asiakas–palvelin-malli:
  - Asiakas tekee pyynnön.
  - Palvelin vastaa pyynnön mukaan.
- Tekstipohjainen protokolla, joka on suunniteltu helppolukuiseksi.

### HTTP-pyynnön rakenne
**1. Pyyntölinja:**
  - Esim. GET /index.html HTTP/1.1

**2. Otsakekentät:**
  - Metadataa, kuten Host: www.example.com

**3. Runkotiedot (valinnainen):**
  - Sisältää tietoa POST- tai PUT-pyynnöille.

### HTTP-vastauksen rakenne
**1. Vastauslinja:**
- Esim. HTTP/1.1 200 OK

**2. Otsakekentät:**
- Esim. Content-Type: text/html

**3. Runkotiedot:**
- Varsinainen sisältö, esim. HTML-koodi.

### HTTP-menetelmät
- GET: Hakee tietoa.
- POST: Lähettää tietoa palvelimelle.
- PUT: Päivittää tai luo resurssin.
- DELETE: Poistaa resurssin.
- HEAD: Hakee vain otsaketiedot.

### HTTP-tilakoodit
- 1xx: Informatiiviset vastaukset.
- 2xx: Onnistuneet vastaukset (esim. 200 OK).
- 3xx: Uudelleenohjaukset (esim. 301 Moved Permanently).
- 4xx: Asiakasvirheet (esim. 404 Not Found).
- 5xx: Palvelinvirheet (esim. 500 Internal Server Error).

### HTTP/1.1 ja HTTP/2
- HTTP/1.1:
  - Tuki pysyville yhteyksille.
  - Lisää tehokkuutta käyttämällä välimuistia ja pakkauksia.
- HTTP/2:
  - Binäärimuoto.
  - Multiplexing (useita pyyntöjä yhdellä yhteydellä).
  - Parempi suorituskyky.

### HTTP/3 – Uusin sukupolvi
- HTTP/3 käyttää QUIC-protokollaa TCP:n sijasta.
  - QUIC on UDP-pohjainen protokolla, joka tarjoaa nopeamman ja vakaamman yhteyden.
- Parannuksia verrattuna HTTP/2:
  - Nopeampi yhteyden muodostus: Ei "kolmivaiheista käsipäivää" (handshake) kuten TCP.
  - Parempi suorituskyky mobiiliverkoissa: Yhteys säilyy vakaana myös verkkojen vaihtuessa.
  - Ei Head-of-line blocking -ongelmaa: Yhden virheen aiheuttama viive ei hidasta koko yhteyttä.
- Turvallisuus:
  - QUIC sisältää sisäänrakennetun TLS 1.3 -salauksen.
- Käyttökohteet:
  - Nopeuttaa verkkosovelluksia ja palveluita, kuten videon suoratoistoa ja reaaliaikaisia sovelluksia.
- Tuki:
  - Yleistymässä selaimissa (esim. Chrome, Edge) ja palvelimissa (esim. Cloudflare, Google).

### HTTPS – Suojattu HTTP
- HTTPS käyttää TLS (Transport Layer Security) -salausta.
- Tarjoaa:
  - Tietojen salauksen.
  - Todennuksen.
  - Eheyden varmistamisen.
- Käytetään aina, kun tietoturva on tärkeää (esim. pankit, verkkokaupat).

### HTTP:n rooli modernissa verkkosovelluksessa
- Käytetään yhdessä REST- ja GraphQL-rajapintojen kanssa.
- Palvelimet voivat hyödyntää välimuistia ja CDN-verkkoja suorituskyvyn parantamiseksi.
- Tulevaisuudessa yleistyy HTTP/3

## Johdanto www-palveluun
### www-palvelu
- Mikä on www-palvelu?
  - Palvelu, joka tarjoaa verkkosivustoja tai sovelluksia käyttäjille internetin kautta.
  - Käyttää yleensä HTTP/HTTPS-protokollaa tietoliikenteeseen.
- Tavoite:
  - Tarjota dynaamista tai staattista sisältöä asiakkaille (esim. selaimet, mobiilisovellukset).
- Tärkeimmät osat:
  1. Asiakas (käyttäjä)
  2. Palvelin
  3. Tiedonsiirto protokollan avulla

### Perusarkkitehtuuri
**1. Asiakas–palvelin-malli:**
- Asiakas (esim. selain tai mobiilisovellus) lähettää pyynnön palvelimelle.
- Palvelin käsittelee pyynnön ja palauttaa vastauksen.

**2. Komponentit:**
- Web-palvelin: Käsittelee HTTP-pyynnöt (esim. Nginx, Apache).
- Sovelluslogiikka: Toteutetaan ohjelmointikielellä (esim. Node.js, Deno, Python).
- Tietokanta: Tallentaa ja hakee dataa (esim. PostgreSQL, MongoDB).

### Palvelun toteutusvaiheet
**1. Suunnittelu:**
- Määrittele palvelun tavoite ja ominaisuudet.
- Valitse teknologiat (esim. backend-, frontend-kehykset ja tietokannat).

**2. Toteutus:**
- Luo palvelin, joka vastaanottaa ja käsittelee pyynnöt.
- Suunnittele ja koodaa frontend- ja backend-logiikka.
- Toteuta API-rajapinnat (REST/GraphQL).

**3. Testaus:**
- Testaa toiminnallisuudet, tietoturva ja suorituskyky.

**4. Julkaisu:**
- Isännöi palvelu verkkopalvelimella tai pilvessä (esim. AWS, Azure, Vercel).

### Tekniikat ja työkalut
- Frontend-teknologiat:
  - HTML, CSS, JavaScript.
  - Kehykset: React, Angular, Vue.js.
- Backend-teknologiat:
  - Node.js, Deno, Python (Django/Flask), Ruby on Rails.
- Tietokannat:
  - Relaatiotietokannat: PostgreSQL, MySQL.
  - NoSQL: MongoDB, Redis.
- API-rajapinnat:
  - REST, GraphQL.
- Isännöinti:
  - Pilvialustat (AWS, Google Cloud, Azure).
  -Palvelut kuten Heroku tai Vercel.

### Tärkeät näkökohdat
**1. Tietoturva:**
- Käytä HTTPS:ää.
- Suojaa syötedata (esim. estä SQL-injektiot).
- Toteuta käyttäjän todennus (esim. OAuth).

**2. Skaalautuvuus:**
- Suunnittele palvelu, joka voi kasvaa käyttäjämäärän mukana.
- Käytä kuormantasaajia ja välimuistia.

**3. Ylläpito:**
- Pidä palvelin ja kirjastot ajan tasalla.
- Seuraa lokitietoja ja suorituskykyä.