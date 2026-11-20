---
tags: [minecraft, functie, code]
---
# Mijnhoogte en ertsscan

Beantwoordt "op welke y-hoogte mijn je het best naar diamant/ijzer?".
- `~/bin/bedrock-ertsscan.sh` (dagelijks 04:40) kopieert de wereldkopie onder `/tmp/bedrock-map.lock` en draait `bedrock-ertsscan.js` (node + leveldb, ±75 s, `nice 15`).
- De scan kiest tot 1200 stukken van 5x5 chunks en **simuleert 1x2-tunnels** met tussenruimte 1–5 op elke y (aders, lava-contact, bedrock, hardheid) → `ertsscan.json`.
- De [[Kaart-collector]] combineert dat met wat spelers echt vonden (empirische Bayes, haktempo uit de addon) → `live/mijn.json`.
- Site: sectie Mijnen met gereedschap/Fortune-keuze, advies, diepteprofiel en uitleg.
- Eerste uitkomst: diamant y −58 (tussenruimte 4) maar veel lava; y −53 bijna even snel met 5% lava. IJzer y 13, of bergen ~168.

Zie [[Stats en ranglijst]], [[Addon Handige Extra's]].
