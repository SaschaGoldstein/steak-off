# Steak Off – online zetten met GitHub en Firebase

De pagina bestaat uit drie bestanden:

| Bestand | Wat |
| --- | --- |
| `index.html` | De volledige pagina (design, Pac-Sascha, koe, inschrijven, proefkaart, uitslag) |
| `config.js` | Jouw instellingen: Firebase-koppeling, gastheer-ID, datum, uur en adres |
| `firestore.rules` | De beveiliging van de database (wie mag wat lezen en schrijven) |

Firebase is gratis voor een feest als dit. Je vrienden hebben geen account nodig.

## Stap 1 – Firebase-project aanmaken (± 5 min)

1. Ga naar https://console.firebase.google.com en log in met je Google-account.
2. Klik **Project toevoegen**, noem het bv. `steak-off`. Google Analytics mag uit.
3. Links: **Build → Authentication → Aan de slag**. Kies bij *Sign-in method* **Anoniem (Anonymous)** en zet het aan.
4. Links: **Build → Firestore Database → Database maken**. Kies **productiemodus** en locatie **europe-west1 (Belgium)**.
5. Klik op het tandwiel → **Projectinstellingen**. Onderaan bij *Je apps* klik je op het icoon **</>** (web). Geef een naam, Hosting hoeft niet.
6. Je krijgt een blok `firebaseConfig = { ... }`. Kopieer de waarden naar `config.js` (apiKey, authDomain, projectId, storageBucket, messagingSenderId, appId).

De apiKey mag gewoon in je code staan: de beveiliging zit in de regels van stap 4.

## Stap 2 – Op GitHub zetten

1. Maak op GitHub een nieuwe repository, bv. `steak-off` (Public).
2. **Add file → Upload files** en sleep `index.html`, `config.js`, `firestore.rules` en `README.md` erin. Commit.
3. **Settings → Pages**: bij *Source* kies je **Deploy from a branch**, branch **main**, map **/ (root)**. Opslaan.
4. Na een minuutje staat je pagina op `https://<jouw-gebruikersnaam>.github.io/steak-off/`.

## Stap 3 – GitHub toelaten in Firebase

Firebase → **Authentication → Settings → Authorized domains → Domein toevoegen** en vul `<jouw-gebruikersnaam>.github.io` in.

## Stap 4 – Jezelf gastheer maken

1. Open op je eigen gsm (die je op de avond gebruikt) `https://<jouw-gebruikersnaam>.github.io/steak-off/?gastheer`
2. Onderaan verschijnt het blok **Gastheer** met jouw ID. Kopieer het.
3. Plak het in `config.js` bij `ownerUid` en upload `config.js` opnieuw naar GitHub.
4. Open `firestore.rules`, vervang `OWNER_UID` door hetzelfde ID, kopieer alles en plak het in Firebase → **Firestore Database → Regels**. Klik **Publiceren**.

Daarna zie jij (en alleen jij) onderaan de lijst met e-mailadressen, en op 28 november de knop **Onthul de uitslag**.

Het ID hoort bij die browser op dat toestel. Gebruik voor het onthullen dus hetzelfde toestel en dezelfde browser.

## Stap 5 – Testen en delen

1. Schrijf jezelf in als test en kijk of je spelerskaart verschijnt.
2. Stuur de link `https://<jouw-gebruikersnaam>.github.io/steak-off/` naar je vrienden.

## Goed om te weten

- **Uur aanpassen:** vul `uur` in `config.js` in (bv. `"19:00"`) en upload het bestand opnieuw.
- **Op de avond** gaat vanzelf open op de datum uit `config.js`.
- Gasten worden herkend per browser. Wie zich inschrijft op zijn gsm, moet op de avond **dezelfde gsm en browser** gebruiken om in te checken en te scoren.
- **Iets misgelopen of een testinschrijving wissen?** In Firebase → Firestore Database kan je documenten bekijken en verwijderen.
