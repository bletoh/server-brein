---
tags: [reismannetje, functie]
---
# Rondreis

(2026-10-23) Eén reis met meerdere stops: elke stop is een pin met eigen verblijf en nachten.
- Tabel `trip_stops(trip_id, item_id, position, nights)`; `PUT /api/trips/:id/stops` zet de hele route.
- Automatische titel "Reis naar X" of "Rondreis A – B"; nachten-stepper, volgorde wijzigen, stop toevoegen via kaart of zoeken.
- Reisstand toont "Nu hier", programma per stop, vlucht/vervoer tussen stops; route-lijn op de kaart.
- Code: `public/js/app/08-route.js`, test `test/rondreis.test.js`.

Zie [[Reisvenster en reisstand]], [[Kaart (MapLibre)]].
