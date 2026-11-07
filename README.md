# Sint Verlanglijstjes

Gedeelde Sinterklaas-verlanglijstjes voor Freek, Kelly, Kevin, Annemiek, Petra en Martin.
Eén HTML-bestand op GitHub Pages, met Firebase voor inloggen (naam + pincode) en opslag.

- Iedereen beheert zijn eigen lijstje: naam, beschrijving, link en foto (wordt automatisch van de link gehaald).
- Bij de lijstjes van anderen kun je notities zetten ("heb ik gekocht", "best duur").
- Notities op je eigen lijstje zijn voor jou onzichtbaar. Dat wordt afgedwongen door de databaseregels in `database.rules.json`, niet alleen door de pagina.

## Firebase instellen (eenmalig, ±10 minuten)

1. Ga naar https://console.firebase.google.com en kies **Project toevoegen**. Naam bijv. `sinterklaaslijstje`. Google Analytics mag uit.
2. **Authentication** → *Aan de slag* → tab **Sign-in method** → **E-mail/wachtwoord** inschakelen (alleen de bovenste schakelaar) → Opslaan.
3. **Authentication** → tab **Instellingen** → **Geautoriseerde domeinen** → *Domein toevoegen* → `khoffmans.github.io`.
4. **Realtime Database** → *Database maken* → locatie **europe-west1 (België)** → start in **vergrendelde modus**.
5. In de database, tab **Regels**: vervang alles door de inhoud van `database.rules.json` en klik **Publiceren**.
6. **Projectoverzicht** (tandwiel) → **Projectinstellingen** → onderaan *Je apps* → het web-icoon `</>` → app-naam invullen, *Firebase Hosting* niet aanvinken → **App registreren**.
7. Kopieer het `firebaseConfig`-blok dat je dan ziet en plak het bovenin `index.html` (of stuur het naar Claude). Controleer dat er een `databaseURL` in staat; zo niet, neem de URL over van de Realtime Database-pagina.

De `apiKey` is geen geheim: hij mag gewoon in een openbare repo. De beveiliging zit in de regels.

## GitHub Pages aanzetten

Repo → **Settings** → **Pages** → *Source*: **Deploy from a branch** → branch `main`, map `/ (root)` → Save.
Na een minuut staat de site op https://khoffmans.github.io/sinterklaaslijstje/

## Beheer

- **Pincode vergeten:** Firebase-console → Authentication → gebruiker `naam@sinterklaaslijstje.app` verwijderen, en in de Realtime Database de regel `names/naam` verwijderen. Daarna kan die persoon opnieuw een pincode kiezen.
- **Opnieuw beginnen na pakjesavond:** in de database `items` en `notes` verwijderen.
- Wie het eerst een naam kiest, koppelt die naam aan zijn pincode. Laat iedereen dus snel inloggen.
