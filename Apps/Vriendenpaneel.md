---
tags: [app, docker, minecraft]
map: /srv/docker/vriendenpaneel
domein: mc.benjaminhashi.nl/beheer
---
# Vriendenpaneel (mc.benjaminhashi.nl/beheer/)

> [!note] Sinds 2026-10-31
> De API draait in k3s (`mc/vriendenpaneel`, Secret `vriendenpaneel-env`) en de worker als sidecar in `mc-server/bedrock`. Herstart via `bsm-herstart`. → [[Minecraft op k3s]]

Serverbeheer voor vrienden met **één gedeeld wachtwoord** (gekozen boven BSM-accounts). Gebouwd 2026-10-14.

## Architectuur
- Container `vriendenpaneel` (python:3.12-alpine, stdlib HTTP, read-only, uid 1000): `app/server.py` + `app/index.html`. PBKDF2-hash + HMAC-cookie (30 dagen, `Path=/beheer/`), max 5 foute logins/10 min/IP, cooldowns per actie.
- Zet acties als JSON in `./queue` → host-worker [[vriendenpaneel-worker.py]] voert ze uit en schrijft `./state` (status, info, log, serverlog, planning).
- Bereikbaar via de nginx van de [[Bedrock-kaart]] (`/beheer/` → `vriendenpaneel:8080`).

## Tabs
| Tab | Inhoud |
|---|---|
| Server | herstart (met/zonder aftellen), backup maken + lijst, tijd, weer, moeilijkheid, alle gamerules, server.properties-editor (whitelist), allowlist, chat/title, zoekveld |
| Wereld | warps maken/verwijderen, setworldspawn, mobs/items/xp opruimen, demodorp-reset, meteoor, atoombom op demodorp |
| Console | terminal met live serveruitvoer, geschiedenis, autocomplete, multi-commando, snelle commando's, spelerchips, geplande commando's |
| Logboek | alle acties met resultaat, zoeken |

- Spelers-tab is **verwijderd** ("te veel voordeel"), maar de vrije console kan alles behalve `stop` (en `gamerule pvp`).
- Het "naam"-veld is zelf ingevuld, niet geverifieerd.

Zie [[Bedrock-server]], [[Chaos-events]], [[Demodorp]].
