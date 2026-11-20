---
tags: [reismannetje, functie]
---
# Wie betaalt wat

Kosten delen per reis, naar het voorbeeld van WieBetaaltWat.nl (2026-10-22).
- Tabel `trip_expenses` (bedrag in centen, betaald door, verdeling als JSON: namen, gewichten of exacte bedragen, soort `payment` = terugbetaling).
- Server: `src/kosten.js` (parts/shares/parseSplit). Client: `08-kosten.js` met Uitgaven / Saldo / Afrekenen en "Betaald"-knop.
- Standaard verdeeld over wie meegaat; chatbericht bij een nieuwe uitgave.
- Verborgen als je alleen in een groep zit. Niet verwarren met de verwijderde budgetfunctie.

Zie [[Reisvenster en reisstand]].
