---
tags: [app, moc, reismannetje, docker]
map: /srv/docker/reismannetje
domein: reismannetje.nl
---
# Reismannetje

> [!note] Sinds 2026-10-31
> Draait op k3s met een testomgeving, deploys via Git/Flux en zonder downtime; de image is 492 MB. → [[Reismannetje op k3s]]

Webapp om met een vriendengroep vakanties te plannen: kaart met pinnen, ideeën, datumprikker, stemmen, chat, reizen, kosten delen. Door Claude gebouwd sinds begin oktober 2026 (eerst "Vakantieplanner", hernoemd 2026-10-14). Live op [[reismannetje.nl]].

| | |
|---|---|
| Stack | Node 20 + Express 4 + better-sqlite3, vanilla JS front-end, Leaflet + MapLibre |
| Container | `reismannetje` (eigen build), netwerk `web`, poort 4000, draait als user `node` |
| Data | volume `reismannetje_data` → [[Reismannetje database]] |
| Repo | `/srv/docker/reismannetje` (root), GitHub `bletoh/vakantieapp`, live op branch `naar-main` |
| Omvang | ±16.000 regels (server ±4.400, front-end ±8.700, CSS ±3.500), 16 testbestanden |
| Backup | [[reismannetje-backup.sh]] 01:30 |

## Code
- [[Reismannetje architectuur]] — hoe het in elkaar zit
- [[Reismannetje backend]] — `src/` (server, db, auth, routes, …)
- [[Reismannetje API]] — alle endpoints
- [[Reismannetje frontend]] — `public/js/app/NN-*.js`, bundel, stijl
- [[Reismannetje database]] — tabellen
- [[Reismannetje tests]]
- [[Reismannetje beveiliging]]
- [[Externe diensten (Reismannetje)]]

## Functies
- [[Groepen en chat]] · [[Kaart (MapLibre)]] · [[Ideeën en swipen]] · [[Datumprikker en stemronde]]
- [[Reisvenster en reisstand]] · [[Rondreis]] · [[Wie betaalt wat]] · [[Tickets en prijsalarm]]
- [[Planavond]] · [[Deelpagina's en bestemmingsgids]] · [[PWA en push]] · [[Partnerlinks]] · [[Snel toevoegen]] · [[Kladblok]]

## Werkwijze
- [[Reismannetje ontwikkelworkflow]] — scratchpad-kopie, testserver, Playwright, branch, deploy
- [[Reismannetje demo-video's]]
- [[Reismannetje stijlgeschiedenis]]
- [[Reismannetje wijzigingen november 2026]] · [[Gebruiksanalyse]]

## Doel van de eigenaar
Zo makkelijk mogelijk een hele vakantie in zo weinig mogelijk klikken plannen; de kaart moet gebruiksvriendelijk blijven. Groep = vrienden van ±22 jaar.
