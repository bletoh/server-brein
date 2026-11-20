---
tags: [reismannetje, functie, kaart]
---
# Kaart (MapLibre)

De kaart is de centrale pagina van [[Reismannetje]].

- **Tegels**: OpenFreeMap-vectortegels, getekend met MapLibre 6.11.2 via `@maplibre/maplibre-gl-leaflet` binnen Leaflet. Eigen stijl in `public/js/kaartstijl.js` (licht/donker, Nederlandse plaatsnamen). Valt terug op OSM-rastertegels zonder WebGL of als OpenFreeMap niet reageert (12 s). Satelliet: Esri World Imagery.
- **Pinnen**: ronde witte markers, genummerd; overlappende pinnen worden samengevoegd met een "+N"-badge (`declutter()`), labels die overlappen worden verborgen.
- **Plannen vanuit een pin**: planpaneel met 5 stappen (wanneer, vlucht, verblijf, activiteiten, eten) → `07-planpaneel.js`.
- **Centrale pagina** (2026-10-22): geen tabs meer; startlijst "Aan de slag", komende reizen, ideeën naast de kaart (met markers op de kaart), chat ernaast.
- **Telefoon**: kaart schermvullend, onderpaneel dat je omhoog veegt (`sheetDrag()`), zwevende knoppen voor chat en snel toevoegen.
- Route-lijn tussen stops bij een [[Rondreis]].

Gegevensbronnen: [[Externe diensten (Reismannetje)]]. Testen met WebGL in headless Chromium vraagt `--use-angle=swiftshader` → [[Playwright-testen]].
