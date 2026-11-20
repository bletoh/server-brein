---
tags: [reismannetje, code, frontend]
map: /srv/docker/reismannetje/public
---
# Reismannetje frontend

Vanilla JS, geen framework. Bestanden in `public/js/app/` worden **op volgorde van naam** samengevoegd tot `/js/app.js` (één gedeelde scope). Nieuw bestand = gewoon in de map zetten.

| Bestand | Inhoud |
|---|---|
| `00-helpers` | helpers, `WORDMARK`, `solo()`, `viaPartnerLink` |
| `01-routing` / `02-weergave` | hash-routes, render, tabs (nu: één centrale pagina) |
| `03-datums` | datumprikker, aftellen |
| `04-acties` / `05-dialogen` | knoppen, dialogen |
| `06-kaart` | kaart, pinnen, declutter, startlijst, dest-sheet, swipe-paneel → [[Kaart (MapLibre)]] |
| `07-planpaneel` | 5 stappen: wanneer/vlucht/verblijf/activiteiten/eten |
| `08-reisvenster`, `08-route`, `08-kosten`, `08-tickets`, `08-prijsalarm`, `08-reis-toevoegen` | [[Reisvenster en reisstand]], [[Rondreis]], [[Wie betaalt wat]], [[Tickets en prijsalarm]] |
| `09-ideeen`, `09-swipen` | [[Ideeën en swipen]] |
| `10-stemronde` | stemrondes + roulette → [[Datumprikker en stemronde]] |
| `11-accounts-chat`, `11-planavond`, `11-pwa`, `11-snel` | [[Groepen en chat]], [[Planavond]], [[PWA en push]], [[Snel toevoegen]] |
| `12-paasei`, `12-start` | easter egg "fiesta-modus" (Konami), opstarten/offline |

Overig: `public/js/kaartstijl.js` (MapLibre-stijl, gedeeld met deelpagina's), `deelkaart.js` (kaart op deelpagina's zonder inline script), `css/style.css` (±3.500 regels, laatste blok = huidige stijl → [[Reismannetje stijlgeschiedenis]]), `data/bestemmingen.json` (145 bestemmingen met handmatig gecontroleerde foto's).

CSP staat **geen inline scripts of `on*=`-handlers** toe → [[Reismannetje beveiliging]].
