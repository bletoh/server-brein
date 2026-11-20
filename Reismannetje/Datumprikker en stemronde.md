---
tags: [reismannetje, functie]
---
# Datumprikker en stemronde

**Datumprikker**: iedereen vinkt in een kalender aan wanneer hij kan (hele periode/maand in één tik, vegen over dagen). Beste periodes bovenaan; "Plan reis" koppelt een periode aan een bestemming. Tabel `available_days`, code `03-datums.js`.

**Stemronde**: kiezen tussen bestemmingen, eigen link `/stem/<slug>` met OG-plaatje (tussenstand) voor WhatsApp, herinneren, uitslag delen. Winnaar wordt de beste keuze op de kaart. Tabellen `polls`, `poll_options`, `poll_votes`.

**Roulette**: casino-stijl rad (groen vilt, gouden rand); de winnaar wordt op de server gekozen met `crypto.randomInt` en als chatbericht gepost. Bij gelijkspel staan de twee opties klaar.

Zichtbaar in de chat ([[Groepen en chat]]) en op de [[Planavond]]. Verborgen als je alleen in een groep zit.
