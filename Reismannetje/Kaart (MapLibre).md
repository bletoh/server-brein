---
tags: [reismannetje, functie, kaart]
---
# Kaart (MapLibre)

> [!note] Sinds 2026-11-20: plekken als strook, paneel zonder dubbelingen
> Idee van de eigenaar ("planner heeft te weinig invulling"; "desktop niet te ver van mobiel"). Live sinds 2026-11-20 (commit `2a37a42`).
> - **Strook** (`#pinStrip`, `pinStripHtml()` in `06-kaart.js`) onder de zoekbalk, op telefoon en laptop gelijk: een chip per plek (tik = vliegen + planpaneel), `Alles tonen` (vanaf 2 plekken met positie), `Stemmen` (in een groep, vanaf 2 plekken) en zoeken. Op de telefoon verdwijnt de strook als het paneel of het pinblad open is (CSS `:has(.dest-sheet.open)`, `body.pin-bottom`); de volgknop schuift eronder.
> - **Paneel** (`plannerHtml()`) toont alleen nog wat nergens anders staat: *Aan de slag*, de lopende reis (`nuKaartjeHtml`) en vluchten/verblijven die nog niet aan een plek hangen (`looseItems()`). Weg: verhalenrij (staat bij Sociaal), *Jullie reizen* (`hubTripsHtml`, staat bij Reis) en het blok *Op de kaart* (nu de strook).
> - **Telefoon**: de knop naast *Lijst* is een koffer met het aantal losse boekingen, en verschijnt alleen als het paneel iets te bieden heeft (`plannerHeeftInhoud()`).
> - **Laptop**: de kolom naast de kaart is het detailpaneel van de gekozen plek, met een hint als er niets open is (`.planner-leeg`). Groep (onder Sociaal) staat sindsdien ook gecentreerd (`body[data-route="groep"] .panel`).
> - De tab *Plannen* zelf was al op 2026-11-12 weggehaald (tabs Ontdekken / Reis / Sociaal).
> Zie [[Reismannetje wijzigingen november 2026]] en [[Agents]] (gevonden en uitgewerkt via de Reismannetje-agent).

De kaart is de centrale pagina van [[Reismannetje]].

- **Tegels**: OpenFreeMap-vectortegels, getekend met MapLibre 6.11.2 via `@maplibre/maplibre-gl-leaflet` binnen Leaflet. Eigen stijl in `public/js/kaartstijl.js` (licht/donker, Nederlandse plaatsnamen). Valt terug op OSM-rastertegels zonder WebGL of als OpenFreeMap niet reageert (12 s). Satelliet: Esri World Imagery.
- **Pinnen**: ronde witte markers, genummerd; overlappende pinnen worden samengevoegd met een "+N"-badge (`declutter()`), labels die overlappen worden verborgen.
- **Plannen vanuit een pin**: planpaneel met 5 stappen (wanneer, vlucht, verblijf, activiteiten, eten) → `07-planpaneel.js`.
- **Centrale pagina** (2026-10-22): geen tabs meer; startlijst "Aan de slag", komende reizen, ideeën naast de kaart (met markers op de kaart), chat ernaast.
- **Telefoon**: kaart schermvullend, onderpaneel dat je omhoog veegt (`sheetDrag()`), zwevende knoppen voor chat en snel toevoegen.
- Route-lijn tussen stops bij een [[Rondreis]].

Gegevensbronnen: [[Externe diensten (Reismannetje)]]. Testen met WebGL in headless Chromium vraagt `--use-angle=swiftshader` → [[Playwright-testen]].
