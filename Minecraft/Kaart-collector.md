---
tags: [minecraft, script, code]
bestand: ~/bin/bedrock-map-collect.py
---
# Kaart-collector (bedrock-map-collect.py)

> [!note] Sinds 2026-10-31
> Draait als k3s-CronJob `kaart-collect` (elke minuut, hostPID), met hetzelfde logbestand. → [[Minecraft op k3s]]

Python-script (±900 regels), **elke minuut** via de user-crontab, ook aan het eind van [[bedrock-map.sh]] en na warp-acties ([[bedrock-map-queue.py]]).

## Wat het doet
Leest nieuwe `[Kaart] …`-regels uit `server_output.txt` (wordt bij elke serverstart leeggemaakt → offset/inode-state in `collect.state.json`) en bewaart alles blijvend in `~/apps/map-work`.

| Logregel (van de addons) | Wordt |
|---|---|
| `speler`, `weg`, `erbij` | `live/players.json`, sessies, routes (trails), heatmap |
| `warps`, `prullenbak`, `resultaat` | `live/markers.json` |
| `stat "<naam>" {json}` | `stats.json`, `stats_daily.json` |
| `casino` | `casino.json` |
| `biome` | `biomes.json`, `live/biomes.json` |
| `dood`, `bouw` | `deaths.json`, `build.json` |
| `eco`, `handel` | `eco.json`; berekent prijzen, vraagtoeslag, weekbonus en stuurt die terug via de console |
| `mijn` | `mining.json` → `live/mijn.json` |

Schrijft voor de site `www/live/{players,markers,stats,heat,biomes,deaths,build,trails,mijn}.json`. Bronnen: [[Addon Handige Extra's]], [[Addon Homes & Teleport]]. Getoond door [[Stats en ranglijst]] en de [[Bedrock-kaart]].

Logregels en host zijn in UTC; datums per dag in Europe/Amsterdam. Backups vóór wijzigingen: `~/apps/map-work/collect.voor-*.py`.
