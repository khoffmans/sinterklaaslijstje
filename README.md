# Sint Verlanglijstjes

Gedeelde Sinterklaas-verlanglijstjes voor Freek, Kelly, Kevin, Annemiek, Petra en Martin.
Eén HTML-bestand op GitHub Pages, met Firebase (gratis Spark-abonnement) voor inloggen met een persoonlijke code en opslag.

- Iedereen beheert zijn eigen lijstje: naam, beschrijving, link en foto (wordt automatisch van de link gehaald).
- Bij de lijstjes van anderen kun je notities zetten ("heb ik gekocht", "best duur").
- Notities op je eigen lijstje zijn voor jou onzichtbaar. Dat wordt afgedwongen door de databaseregels in `database.rules.json`, niet alleen door de pagina.

## Firebase instellen (eenmalig, ±15 minuten, gratis)

1. Ga naar https://console.firebase.google.com en kies **Project toevoegen**. Naam bijv. `sinterklaaslijstje`. Google Analytics mag uit. Blijf op het gratis **Spark**-abonnement.
2. **Authentication** → *Aan de slag* → tab **Sign-in method** → **E-mail/wachtwoord** inschakelen (alleen de bovenste schakelaar) → Opslaan.
3. **Authentication** → tab **Instellingen** → **Geautoriseerde domeinen** → *Domein toevoegen* → `khoffmans.github.io`.
4. **Authentication** → tab **Gebruikers** → **Gebruiker toevoegen**, zes keer. Dit zijn geen echte e-mailadressen, er wordt nooit iets naartoe gestuurd:

   | E-mail | Wachtwoord |
   |---|---|
   | `freek@sinterklaaslijstje.app` | code voor Freek |
   | `kelly@sinterklaaslijstje.app` | code voor Kelly |
   | `kevin@sinterklaaslijstje.app` | code voor Kevin |
   | `annemiek@sinterklaaslijstje.app` | code voor Annemiek |
   | `petra@sinterklaaslijstje.app` | code voor Petra |
   | `martin@sinterklaaslijstje.app` | code voor Martin |

   Een code is minimaal 6 tekens, bijv. `pepernoot47` of `schimmel82`. Gebruik alleen letters en cijfers, dan werkt hij ook in de inloglink.
5. **Realtime Database** → *Database maken* → locatie **europe-west1 (België)** → start in **vergrendelde modus**.
6. In de database, tab **Regels**: vervang alles door de inhoud van `database.rules.json` en klik **Publiceren**.
7. **Projectinstellingen** (tandwiel) → onderaan *Je apps* → het web-icoon `</>` → app-naam invullen, *Firebase Hosting* niet aanvinken → **App registreren**.
8. Kopieer het `firebaseConfig`-blok en plak het bovenin `index.html` (of stuur het naar Claude). Controleer dat er een `databaseURL` in staat; zo niet, neem de URL over van de Realtime Database-pagina.

De `apiKey` is geen geheim: hij mag gewoon in een openbare repo. De beveiliging zit in de regels en in de codes.

## GitHub Pages aanzetten

Repo → **Settings** → **Pages** → *Source*: **Deploy from a branch** → branch `main`, map `/ (root)` → Save.
Na een minuut staat de site op https://khoffmans.github.io/sinterklaaslijstje/

## Codes versturen

Stuur iedereen een persoonlijke link, bijv. via WhatsApp:

    https://khoffmans.github.io/sinterklaaslijstje/#petra-schimmel82

Eén tik en je bent ingelogd; daarna blijf je op dat apparaat ingelogd. Inloggen kan ook door je naam te kiezen en de code te typen.
Zo'n link is net zo geheim als de code zelf: stuur hem alleen naar de persoon zelf.

## Beheer

- **Code kwijt of uitgelekt:** Authentication → Gebruikers → bij die persoon *Wachtwoord opnieuw instellen* kan niet zonder e-mail, dus: gebruiker verwijderen en opnieuw toevoegen met een nieuwe code. Het lijstje blijft bewaard.
- **Opnieuw beginnen na pakjesavond:** in de database `items` en `notes` verwijderen.
