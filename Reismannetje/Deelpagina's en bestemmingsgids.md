---
tags: [reismannetje, functie, seo]
---
# Deelpagina's en bestemmingsgids

**Deelpagina's** (`routes/share.js`), alleen lezen, onraadbare links:
- `/reis/<slug>` — één reis met kaart, datums, wie kan, vlucht, hotel, programma
- `/reizen/<slug>` — meerdere reizen gebundeld
- `/stem/<slug>` — stemronde
- `/og/*.jpg` — voorbeeldplaatjes voor WhatsApp, door de server gemaakt (sharp)

**Bestemmingsgids** (`routes/gids.js`), publiek voor zoekmachines:
- `/bestemmingen` (landingspagina + alle 145), `/bestemmingen/<categorie>` (13), `/bestemming/<slug>` (vliegtijd, beste maanden, temperatuur, kosten voor een groep, vergelijkbare plekken)
- `sitemap.xml`, `robots.txt`, JSON-LD. Links via [[Partnerlinks]].
- Nog te doen (eigenaar): sitemap indienen in Google Search Console.

Kaarten op deelpagina's via `public/js/deelkaart.js` (data uit JSON, geëscaped: XSS-fix, zie [[Reismannetje beveiliging]]). Domein: [[reismannetje.nl]].
