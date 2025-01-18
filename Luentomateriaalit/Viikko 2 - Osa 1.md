> HUOM!  Materiaalin laadinnassa hyödynnetty ChatGPT-tekoälysovellusta

# HTML, CSS ja JavaScript - On-Premise ja Cloud VM

## Johdanto HTTP-protokollaan

### HTTP
- HTTP (HyperText Transfer Protocol) on sovelluskerroksen protokolla, jota käytetään tiedon siirtoon verkkosovelluksissa.
- Kehitetty erityisesti World Wide Webin (WWW) käyttöön.
- Stateless: Jokainen pyyntö on itsenäinen.

### HTTP:n Perusperiaatteet
- Asiakas–palvelin-malli:
  - Asiakas tekee pyynnön.
  - Palvelin vastaa pyynnön mukaan.
- Tekstipohjainen protokolla, joka on suunniteltu helppolukuiseksi.

### HTTP-pyynnön rakenne
1. Pyyntölause:
    - Esim. GET /index.html HTTP/1.1

2. Otsakekentät:
    - Metadataa, kuten Host: www.example.com

3. Runkotiedot (valinnainen):
   - Sisältää tietoa POST- tai PUT-pyynnöille.

### HTTP-vastauksen rakenne
1. Vastauslause:
    - Esim. HTTP/1.1 200 OK

2. Otsakekentät:
    - Esim. Content-Type: text/html

3. Runkotiedot:
    - Varsinainen sisältö, esim. HTML-koodi.

### HTTP-menetelmiä (metodeja)
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
- Nykyisin käytössä lähes jokaisessa verkkosivussa

### HTTP:n rooli modernissa verkkosovelluksessa
- Käytetään yhdessä REST- ja GraphQL-rajapintojen kanssa.
- Palvelimet voivat hyödyntää välimuistia ja CDN-verkkoja suorituskyvyn parantamiseksi.
- Tulevaisuudessa yleistyy HTTP/3

## Johdanto WWW-palveluun
### WWW-palvelu
- Mikä on WWW-palvelu?
  - Palvelu, joka tarjoaa verkkosivustoja tai sovelluksia käyttäjille verkon kautta.
  - Käyttää yleensä HTTP/HTTPS-protokollaa tietoliikenteeseen.
- Tavoite:
  - Tarjota dynaamista tai staattista sisältöä asiakkaille (esim. selaimet, mobiilisovellukset).
- Tärkeimmät osat:
  1. Asiakas (käyttäjä)
  2. Palvelin
  3. Tiedonsiirto protokollan avulla (TCP/UDP, yleensä portti 80 tai 443)

### Perusarkkitehtuuri
1. Asiakas–palvelin-malli:
    - Asiakas (esim. selain tai mobiilisovellus) lähettää pyynnön palvelimelle.
      - Tietty protokolla ja portti
      - Tyypillisesti fyysisesti eri paikoissa → Tiedonsiirrosta syntyy viivettä
    - Palvelin käsittelee pyynnön ja palauttaa vastauksen.
      - Käsittely kuluttaa resursseja → Syntyy viivettä
      - Vastauksen toimittamisesta syntyy viivettä

2. Komponentit:
    - Web-palvelin: Käsittelee HTTP-pyynnöt (esim. Nginx, Apache).
    - Sovelluslogiikka: Toteutetaan ohjelmointikielellä (esim. Node.js, Deno, Python).
    - Tietokanta: Tallentaa ja hakee dataa (esim. PostgreSQL, MongoDB).

### Palvelun toteutusvaiheet
1. Suunnittelu:
    - Määrittele palvelun tavoite ja ominaisuudet.
    - Valitse teknologiat (esim. backend-, frontend-kehykset ja tietokannat).

2. Toteutus:
    - Luo palvelin, joka vastaanottaa ja käsittelee pyynnöt.
    - Suunnittele ja koodaa frontend- ja backend-logiikka.
    - Toteuta API-rajapinnat (REST/GraphQL).

3. Testaus:
    - Testaa toiminnallisuudet, tietoturva ja suorituskyky.

4. Julkaisu:
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
  - Palvelut kuten Heroku tai Vercel.

### Tärkeät näkökohdat
1. Tietoturva:
    - Käytä HTTPS:ää.
    - Suojaa syötedata (esim. estä SQL-injektiot).
    - Toteuta käyttäjän todennus (esim. OAuth).

2. Skaalautuvuus:
    - Suunnittele palvelu, joka voi kasvaa käyttäjämäärän mukana.
    - Käytä kuormantasaajia ja välimuistia.

3. Ylläpito:
    - Pidä palvelin ja kirjastot ajan tasalla.
    - Seuraa lokitietoja ja suorituskykyä.

## On-Premise VM ja WWW-palvelun tuottaminen 

### Johdanto WWW-palvelun tuottamiseen virtuaalikoneella
- Mikä on virtuaalikone (VM)?
  - Virtuaalinen ympäristö, joka toimii kuin fyysinen tietokone.
  - Isännöidään virtualisointiohjelmistolla (esim. VirtualBox, VMware, Hyper-V).
- Miksi käyttää virtuaalikonetta?
  - Eristetty kehitysympäristö.
  - Helppo hallita ja toistaa.
  - Voi simuloida eri käyttöjärjestelmiä ja palvelinympäristöjä.
  - Edullinen → Ei käyttöön perustuvia kuluja (Vrt. Pilvi)
  - Voidaan tehdä erilaisia testauksia (toiminta, suorituskyky, turvallisuus, ...)
  - Omassa ympäristössä → Tietoturvatestauksen kannalta tärkeä (laillisuus yms.)
  - Usein fyysisesti lähellä → Tiedonsiirron viiveet pieniä
- Tavoite:
  - Tuottaa WWW-palvelu paikallisella VM:llä, joka jäljittelee todellista palvelinympäristöä.

### Virtuaalikoneen asennus ja valmistelu
1. Luo virtuaalikone:
    - Valitse virtualisointiohjelmisto (esim. VirtualBox).
    -  Asenna käyttöjärjestelmä (esim. Ubuntu Server).
2. Määritä virtuaalikone:
    - Varaa riittävästi resursseja (RAM, CPU, tallennustila).
    - Konfiguroi verkkoyhteydet (NAT, bridged mode).
3. Asenna perusohjelmistot:
    - Web-palvelin (esim. Nginx, Apache).
    - Sovellusympäristö (esim. Node.js, Python).
    - Tietokanta (esim. PostgreSQL, MySQL).

### WWW-palvelun kehittäminen ja siirtäminen VM:lle
1. Kehitä sovellus:
    - Luo paikallisesti toimiva sovellus (frontend + backend).
    - Testaa sovellus ennen siirtoa.
2. Siirrä sovellus virtuaalikoneelle:
    - Kopioi tiedostot SCP:n, SFTP:n tai Gitin avulla.
    - Asenna sovelluksen riippuvuudet (esim. `npm install`, `pip install`).
3. Konfiguroi palvelin:
    - Määritä web-palvelin ohjaamaan liikenne sovellukseen.
    - Luo tarvittaessa systemd-palvelu automaattista käynnistämistä varten.

### WWW-palvelun käyttöönottaminen virtuaalikoneessa
1. Käynnistä sovellus:
    - Testaa palvelua paikallisesti virtuaalikoneessa (esim. `curl http://localhost`).
2. Avaa pääsy ulkoisille laitteille:
    - Konfiguroi VM:n verkkoasetukset (bridged/NAT + porttiohjaukset).
    - Salli tarvittavat portit palomuurissa (esim. `sudo ufw allow 80`).
3. Testaa ulkoinen yhteys:
    - Varmista, että palveluun voi yhdistää isäntäkoneelta tai muilta laitteilta (esim. `curl http://<vm-ip>`).

### Tärkeät näkökohdat ja vinkit
1. Ylläpito:
    - Päivitä käyttöjärjestelmä ja ohjelmistot säännöllisesti (apt update && apt upgrade).
    - Varmista, että lokitiedostot kerätään ja niitä seurataan.
2. Suorituskyky:
    - Optimoi VM:n resurssien käyttö (CPU, RAM, I/O).
    - Käytä välimuistia (esim. Redis, Nginx).
3. Tietoturva:
    - Käytä vahvoja salasanoja ja rajoita pääsyä SSH-avaimilla.
    - Ota käyttöön HTTPS (esim. Let's Encrypt).
4. Backup ja snapshotit:
    - Luo snapshot ennen suuria muutoksia.
    - Varmuuskopioi tärkeät tiedostot.

### Ekstraa
- https://www.virtualbox.org/
- https://www.debian.org/
- https://ultahost.com/knowledge-base/install-netstat-debian/
- https://www.techtarget.com/searchsecurity/tutorial/How-to-use-PuTTY-for-SSH-key-based-authentication
- https://www.digitalocean.com/community/tutorials/how-to-install-nginx-on-debian-11

```
APUKOMENTOJA (opettajan muistilista)

apt install net-tools
apt install openssh-server
PasswordAuthentication no
```

## Cloud ja WWW-palvelun tuottaminen 

### Erilaiset pilvipalvelujen mallit
1. `IaaS` (Infrastructure as a Service)
    - Taso: Infrastruktuuri.
    - Käyttäjän vastuulla:
      - Käyttöjärjestelmä, sovellukset, tietoturva.
    - Palveluntarjoajan vastuulla:
      - Virtuaalikoneet, tallennustila, verkot, laitteisto.
    - Esimerkkejä:
      - Amazon EC2, Google Compute Engine, Microsoft Azure VM.
2. `PaaS` (Platform as a Service)
    - Taso: Alusta.
    - Käyttäjän vastuulla:
      - Sovellusten kehitys ja hallinta.
    - Palveluntarjoajan vastuulla:
      - Infrastruktuuri, käyttöjärjestelmät, kehitystyökalut.
    - Esimerkkejä:
      - Google App Engine, Heroku, Microsoft Azure App Service.
3. `SaaS` (Software as a Service)
    - Taso: Ohjelmisto.
    - Käyttäjän vastuulla:
      - Käyttö sovelluksen kautta.
    - Palveluntarjoajan vastuulla:
      - Kaikki infrastruktuuri, sovellus ja tietoturva.
    - Esimerkkejä:
      - Gmail, Dropbox, Salesforce, Microsoft Office 365.
4. `FaaS` (Function as a Service) / Serverless
    - Taso: Funktiotason suoritus.
    - Käyttäjän vastuulla:
      - Yksittäiset koodilohkot ja niiden logiikka.
    - Palveluntarjoajan vastuulla:
      - Skaalautuvuus, infrastruktuuri ja ajoitus.
    - Esimerkkejä:
      - AWS Lambda, Google Cloud Functions, Azure Functions.
- **Erojen yhteenveto:**
  - `IaaS:` Vapaus infrastruktuurin hallintaan.
  - `PaaS:` Nopeampi kehitysympäristö ilman infrastruktuurin hallintaa.
  - `SaaS:` Valmis ohjelmisto käytettäväksi.
  - `FaaS:` Maksat vain suorituskerrasta, ilman jatkuvaa palvelinhallintaa.

### Johdanto WWW-palvelun tuottamiseen pilvessä virtuaalikoneella (IaaS)
- Pilvessä oleva virtuaalikone (VM):
  - Pilvipalveluntarjoajan (esim. AWS, Google Cloud, Azure) isännöimä virtuaalikone.
  - Tarjoaa skaalautuvuutta, joustavuutta ja nopeaa käyttöönottoa.
- Miksi käyttää pilvipalvelua?
  - Helppo resursointi ja skaalautuvuus.
  - Maksat vain käytön mukaan.
  - Pääsy globaaleihin palveluihin ja datakeskuksiin.
- Esimerkkejä käyttökohteista:
  - Staattiset verkkosivut, dynaamiset sovellukset, API-palvelut.

### Pilvipalvelun valinta ja VM:n valmistelu
1. Valitse pilvipalveluntarjoaja:
    - AWS EC2: Yleiskäyttöiset virtuaalikoneet.
    - Google Cloud Compute Engine: Integrointi muihin GCP-palveluihin.
    - Azure Virtual Machines: Helppo liittää muihin Microsoft-palveluihin.
2. VM:n määritys:
    - Valitse käyttöjärjestelmä (esim. Ubuntu, CentOS).
    - Määritä resurssit (CPU, RAM, tallennustila).
3. Verkkoasetukset:
    - Luo virtuaalinen verkko.
    - Määritä palomuuri ja salli tarvittavat portit (esim. 80, 443).

### WWW-palvelun siirtäminen ja konfigurointi
1. Siirrä sovellus VM:lle:
    - Käytä SSH:ta, SCP:tä tai SFTP:tä tiedostojen siirtoon.
    - Voit myös hyödyntää Gitin kaltaisia työkaluja.
2. Asenna riippuvuudet:
    - Esim. Node.js, Python, Apache/Nginx, tietokantaohjelmistot.
3. Määritä web-palvelin:
    - Esim. Nginx reitittämään pyynnöt sovellukseen.
    - Käytä välimuistia suorituskyvyn parantamiseksi.
4. Käynnistä palvelu:
    - Testaa paikallisesti ja varmista, että se toimii pilviympäristössä.

### WWW-palvelun käyttöönotto ja hallinta
1. DNS-määritys:
    - Osoita verkkotunnus VM:n julkiseen IP-osoitteeseen.
2. SSL/TLS-sertifikaatit:
    - Käytä esim. Let's Encrypt -palvelua HTTPS:n aktivoimiseen.
3. Kuormantasaus ja skaalautuvuus:
    - Ota käyttöön pilvialustan kuormantasaaja (esim. AWS ELB).
    - Hyödynnä autoskaalausta käyttäjämäärän kasvaessa.
4. Seuranta ja hallinta:
    - Kerää lokit ja suorituskykytiedot pilvialustan työkaluilla (esim. CloudWatch, Stackdriver).

### Tärkeät näkökohdat ja parhaat käytännöt
1. Tietoturva:
    - Käytä vahvoja SSH-avaimia ja rajaa IP-osoitteet pääsyyn.
    - Ota käyttöön kaksivaiheinen tunnistautuminen pilvihallintaan.
    - Säännölliset tietoturvapäivitykset (OS ja sovellukset).
2. Backup ja palautus:
    - Luo varmuuskopiot datasta ja kokoonpanoista (snapshotit).
    - Käytä pilvialustan automaattisia varmuuskopiointityökaluja.
3. Kustannusten hallinta:
    - Valvo resurssien käyttöä ja sulje käyttämättömät VM:t.
    - Hyödynnä pilvipalvelun hinnoittelumalleja, kuten spot-instanseja.
4. Pitkäaikainen skaalautuvuus:
    - Siirry konttiteknologiaan (esim. Docker, Kubernetes) tarvittaessa.
    - Hyödynnä pilvialustan serverless-tekniikoita tulevaisuudessa.