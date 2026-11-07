# Sint Verlanglijstjes

Gedeelde Sinterklaas-verlanglijstjes voor Freek, Kelly, Kevin, Annemiek, Petra en Martin.
Eén HTML-bestand op GitHub Pages, met Firebase voor inloggen (sms-code) en opslag.

- Iedereen beheert zijn eigen lijstje: naam, beschrijving, link en foto (wordt automatisch van de link gehaald).
- Bij de lijstjes van anderen kun je notities zetten ("heb ik gekocht", "best duur").
- Notities op je eigen lijstje zijn voor jou onzichtbaar. Dat wordt afgedwongen door de databaseregels in `database.rules.json`, niet alleen door de pagina.

## Firebase instellen (eenmalig, ±15 minuten)

1. Ga naar https://console.firebase.google.com en kies **Project toevoegen**. Naam bijv. `sinterklaaslijstje`. Google Analytics mag uit.
2. Zet het project op het **Blaze-abonnement** (linksonder *Upgraden*). Sms-inloggen werkt alleen met een gekoppelde betaalmethode. Je betaalt per verstuurde sms, een paar cent per stuk. Zet bij het upgraden een budgetwaarschuwing van bijv. € 5.
3. **Authentication** → *Aan de slag* → tab **Sign-in method** → **Telefoon** inschakelen → Opslaan.
4. **Authentication** → tab **Instellingen**:
   - **Geautoriseerde domeinen** → *Domein toevoegen* → `khoffmans.github.io`.
   - **Sms-regiobeleid** → *Toestaan* → alleen **Nederland** (en eventueel België/Duitsland als iemand daar een nummer heeft). Dit voorkomt misbruik en hoge kosten.
5. **Realtime Database** → *Database maken* → locatie **europe-west1 (België)** → start in **vergrendelde modus**.
6. In de database, tab **Regels**: vervang alles door de inhoud van `database.rules.json` en klik **Publiceren**.
7. **Projectinstellingen** (tandwiel) → onderaan *Je apps* → het web-icoon `</>` → app-naam invullen, *Firebase Hosting* niet aanvinken → **App registreren**.
8. Kopieer het `firebaseConfig`-blok en plak het bovenin `index.html` (of stuur het naar Claude). Controleer dat er een `databaseURL` in staat; zo niet, neem de URL over van de Realtime Database-pagina.

De `apiKey` is geen geheim: hij mag gewoon in een openbare repo. De beveiliging zit in de regels.

Testen zonder sms-kosten: Authentication → Sign-in method → Telefoon → *Telefoonnummers voor testen* → bijv. `+31 6 00000000` met code `123456`.

## GitHub Pages aanzetten

Repo → **Settings** → **Pages** → *Source*: **Deploy from a branch** → branch `main`, map `/ (root)` → Save.
Na een minuut staat de site op https://khoffmans.github.io/sinterklaaslijstje/

## Beheer

- Inloggen: kies je naam, vul je 06-nummer in en typ de code uit de sms. Daarna blijf je op dat apparaat ingelogd. Op een nieuw apparaat log je met hetzelfde nummer weer in als dezelfde persoon.
- **Verkeerde naam gekoppeld of nieuw nummer:** in de Realtime Database `names/naam` en `members/<uid>` verwijderen (de uid staat bij `names/naam`). Daarna kan die persoon opnieuw koppelen.
- **Opnieuw beginnen na pakjesavond:** in de database `items` en `notes` verwijderen.
- Wie het eerst een naam kiest, koppelt die naam aan zijn telefoonnummer. Laat iedereen dus snel inloggen.
